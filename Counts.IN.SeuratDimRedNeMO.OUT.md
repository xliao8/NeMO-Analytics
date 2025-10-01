# Standardize and reformat the Multi-Omics data using NeMO Function

  This document explains how to prepare inputs and run the **NeMO function** (`Counts.IN.SeuratDimRedNeMO.OUT.R`).  

  Unlike **NeMO.TRIM function** (`Counts.IN.SeuratDimRedNeMO.OUT.TRIM.R`), which assumes your expression matrix is already processed and formatted, and requires you to prepare the input matrices ahead, this function is more flexible:
  - It can accept raw counts or non-normalized expression matrices.
  - It optionally applies normalization (Log2CPM), dimensionality reduction (t-SNE, UMAP), and dataset integration via Seurat.
  - It can perform startified random downsampling for handling large datasets. 
  - Finally, it produces `NeMOAnalytics.org`-compatible outputs (.xlsx metadata and .tar.gz data archive)
---
## 1. Requirement
Install and load required libraries:

```r
library(devtools)
install_github("CHuanSite/SJD")

library(dplyr)
library(Seurat)
library(SJD)
```

## 2. Prepare the inputs

### 2.1 Expression matrix
As previously stated, (`Counts.IN.SeuratDimRedNeMO.OUT.R`) does not require a fully processed dataset. However, it is still required to be formatted as gene X cell/samples.

```r
# To extract the normalized count matrix from a fully processed Seurat object
exprs_all_cell_types <- as.matrix(seuratobj@assays$RNA@data)
# Check the dimensions of the expression matrix 
dim(exprs_all_cell_types) 
```

### 2.2 cellMETA data
The cellMETA data stores all sample- and cell-level metadata associated with your dataset. This can include experimental group labels, genotypes, additional annotations, cell type labels (for scRNA-seq), or spatial coordinates (for spatial profiling). In short, anything you know about your samples or cells can be captured here.

Each column in cellMETA represents a variable (categorical or continuous) that can later be used to customize visualizations in the NeMO platform. Crucially, cellMETA should also include dimensional reduction coordinates (e.g., PCA, UMAP, t-SNE), so that these embeddings can be carried over and used for corresponding visualization within NeMO.

For scRNAseq data that has been processed with Seurat, the metadata can be extracted from the metadata slot, and the dimensionality reduction coordinates can be easily accessed under the reduction slots. The first two columns of embedding coordinates can then be concatenated together with the original metadata. 

```r
cell_metadata_all_cell_types <- cbind(seuratobj@meta.data,
                                      seuratobj@reductions$pca@cell.embeddings[,1:2],
                                      seuratobj@reductions$umap@cell.embeddings[,1:2],
                                      seuratobj@reductions$tsne@cell.embeddings[,1:2]) 
```

### 2.3 geneMETA data

The geneMETA data is the returned dataset of the `getMatch` function. The getMatch function from the SJD package maps gene identifiers between formats or species. Given a list of gene names, it returns a metadata table with two columns: the corresponding gene symbols and Ensembl IDs. The input species and identifier type (e.g., symbol, ensembl) must be specified to ensure accurate mapping. 

```r
gene_metadata_all_cell_types <- getMatch(rownames(logNormalized_10k_all_cell_types), 
                                         inSpecies = 'mouse', 
                                         inType = 'symbol', 
                                         newSpecies = 'mouse')
```

## 3. Run the function

`Counts.IN.SeuratDimRedNeMO.OUT.TRIM.R` prepares processed expression data and associated metadata for upload to the NeMO Analytics platform. It takes in a gene expression matrix, cell/sample metadata, and gene metadata, and then packages these inputs into NeMO-compatible outputs. The function generates both an .xlsx metadata file and a .tar.gz data archive, which can be uploaded to NeMO Platform. 

The next section will explain each of the arguments in the `Counts.IN.SeuratDimRedNeMO.OUT.R` function

#### Core Inputs
  - sampLAB: Short label for filenames.
  - cnts: Expression matrix (genes × samples). Can be raw counts or normalized values. If raw counts, set Log2CPM.flag = TRUE.
  - cellMETA: Metadata table for samples/cells (rows = cells, columns = metadata).
  - geneMETA: Metadata table for genes (rows = genes, columns = metadata).

#### Seurat Processing & Integration

  - SEUR.flag: If TRUE, compute non-integrated t-SNE and UMAP embeddings using Seurat.
  - splitANDintegrate.flag: If TRUE, perform Seurat integration (e.g., across individuals, batches). Requires rownames of cellMETA to match colnames of cnts.
  - splitANDintegrateBY: Column name in cellMETA that defines groups for integration (e.g., sample IDs).
  - useSeuratExprs4nemo.flag:
    - FALSE: Use your own counts (logged if Log2CPM.flag=TRUE) for NeMO export.
    - TRUE: Use Seurat’s processed (log-normalized) expression values.

  #### Normalization & Transformation
  - Log2CPM.flag: If TRUE, raw counts are converted to log2(CPM+1).
    - Should be TRUE when input is raw counts.
    - Skips Seurat normalization if FALSE (when SEUR.flag=TRUE).
   
  #### Visualization & Outputs
  - JPG.flag / PDF.flag: If TRUE, generate plots of embeddings.
  - xx, yy: Column names in cellMETA for the X/Y axes of plots (e.g., "UMAP_1", "UMAP_2").
  - cellClassColumn: Metadata column to color cells by in the plot.
  - cellColorColumn: Specific colors to use for cell groups.
  - saveRDATA.flag: If TRUE, save intermediate .RData object.
  - NeMO.flag: If TRUE, output NeMO-formatted files. 
  - TARball.flag: If TRUE, generate .tar.gz archive of output files.

  #### Feature & Dimensionality Reduction Settings
  - Nfeat: Number of variable features to use (default = 7500).
  - nPCs: Number of principal components for dimensionality reduction (default = 40).


  #### Output Paths
  - baseDIR: Directory where outputs are written.
  - dirNeMO: Directory specifically for NeMO-compatible files.
  
  #### NeMO Metadata (These fields populate the metadata.xlsx file that can be uploaded to NeMO:
  - nemoMETA.title: Title for dataset.
  - nemoMETA.summary: Summary/description.
  - nemoMETA.dataset_type: e.g., "scRNA-seq".
  - nemoMETA.annotation_source: Source of gene annotation (e.g., "Ensembl").
  - nemoMETA.annotation_release_number: Version of annotation (e.g., "103").
  - nemoMETA.geo_accession, pubmed_id: Dataset references.
  - nemoMETA.contact_ fields*: Contact info for dataset owner.
  - nemoMETA.sample_taxid: Organism taxonomy ID (9606 = human, 10090 = mouse).
  - nemoMETA.sample_organism: Organism name (e.g., "Homo sapiens").
  - nemoMETA.platform_id, instrument_model, library_ fields*: Sequencing platform/library info.
  - nemoMETA.tags: Keywords describing dataset.
  - Gene Metadata Columns
  - geneMETA.symbol.column: Column in geneMETA with gene symbols (default "GeneSymbol").
  - geneMETA.ensembl.column: Column in geneMETA with Ensembl IDs (default "ensemblGeneID").

  #### Other Options
  - dropDUPna.flag: Drop duplicates/NA values if TRUE.
  - cnvrtDUPna.flag: Convert duplicates/NA values if TRUE.
  - downS.flag: If TRUE, downsample cells before processing.
  - NcellsDOWN: Number of cells to keep when downsampling (default = 25,000).
  - DOWNsampClusters: Optionally restrict downsampling within specific clusters.

    
```r
CntsIN.seurNeMOoutTRIM(
    sampLAB ="Green_Nature_2024_microglia", 
    exprs = exprs_all_cell_type,           
    cellMETA= cellMETA_all_cell_types,      
    geneMETA = geneMETA_all_cell_types,    
    geneMETA.symbol.column="genes",
    geneMETA.ensembl.column="Gene.stable.ID.human",      
    baseDIR=/path/to/file/
    cnvrtDUPna.flag=TRUE,
    nemoMETA.title="Title for the dataset,
    nemoMETA.summary="short description for the study and dataset, preferably including the study design, number of control and        experimental groups, number of cell types, number of cells, etc. ",
    nemoMETA.dataset_type="scRNA-seq",
    nemoMETA.annotation_source="Ensembl",
    nemoMETA.annotation_release_number="103",
    nemoMETA.geo_accession="NA",
    nemoMETA.contact_email="",
    nemoMETA.contact_institute="",
    nemoMETA.contact_name="",
    nemoMETA.sample_taxid=9606,# 10090 for mouse
    nemoMETA.sample_organism="Homo sapiens",# Mus musculus
    nemoMETA.platform_id="",
    nemoMETA.instrument_model="Illumina NovaSeq 6000",
    nemoMETA.library_selection="",
    nemoMETA.library_source="",
    nemoMETA.library_strategy="",
    nemoMETA.units="LogCPM",
    nemoMETA.pubmed_id="39198642",
    nemoMETA.tags="Human, scRNA-seq, AD, cognitive function, ageing")

```





