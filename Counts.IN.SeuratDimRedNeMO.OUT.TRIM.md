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
2.1 Expression Matrix input stores the processed count matrix data, which is specifically formatted as genes x cells/samples (i.e. rows=genes names and columns = sample names). Different from the `Counts.IN.SeuratDimRedNeMO.OUT.R'function, 
the `Counts.IN.SeuratDimRedNeMO.OUT.TRIM.R' does not have built-in   
