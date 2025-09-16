# Standardize and reformat the Multi-Omics data using NeMO Function

  This document explains how to prepare inputs and run the **NeMO.TRIM function** (`Counts.IN.SeuratDimRedNeMO.OUT.TRIM.R`). The output of the (`Counts.IN.SeuratDimRedNeMO.OUT.TRIM.R`and `Counts.IN.SeuratDimRedNeMO.OUT.R`)
  can then be directly uploaded onto (`NeMOanalytics.org`)

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
The expression matrix stores the processed count data, formatted as genes × cells/samples (i.e., rows represent gene names, columns represent sample or cell identifiers).

Unlike the `Counts.IN.SeuratDimRedNeMO.OUT.R function`, the `Counts.IN.SeuratDimRedNeMO.OUT.TRIM.R` function does not include a built-in normalization argument for raw datasets. Therefore, it is essential to ensure that your dataset has already been fully processed  before extracting and providing the expression matrix as input.

Here, we demonstrate two commonly encountered examples for scRNA-seq and BulkRNA-seq, respectively. 
- scRNA-seq: If your dataset has been processed in Seurat and saved as a Seurat object, the normalized count matrix stored in the assay’s "data" slot is already formatted as genes × cells.
- Bulk RNA-seq: Processed bulk RNA-seq data are typically stored as genes × samples. As long as the dataset has been properly normalized, it can be used directly as the expression matrix input.

```r
# To extract the normalized count matrix from a fully processed Seurat object
logNormalized_10k_all_cell_types <- as.matrix(seuratobj@assays$RNA@data)
# Check the dimensions of the expression matrix 
dim(logNormalized_10k_all_cell_types) 
```

### 2.2. CellMETA data
The cellMETA object stores all sample- and cell-level metadata associated with your dataset. This can include experimental group labels, genotypes, additional annotations, cell type labels (for scRNA-seq), or spatial coordinates (for spatial profiling). In short, anything you know about your samples or cells can be captured here.

Each column in cellMETA represents a variable (categorical or continuous) that can later be used to customize visualizations in the NeMO platform. Crucially, cellMETA should also include dimensional reduction coordinates (e.g., PCA, UMAP, t-SNE), so that these embeddings can be carried over and used for corresponding visualization within NeMO.

For scRNAseq data that has been processed with Seurat, the dimensionality reduction coordinates can be easily accessed in the reduction slot under the assay 



