# SSc Lung scRNA-seq Analysis (GSE212109)

## Project Overview
This project performs a comprehensive single-cell RNA-seq (scRNA-seq) analysis on lung tissue samples from Systemic Sclerosis (SSc) patients. The pipeline processes raw 10X Genomics data to identify distinct cell populations and analyze gene expression variability across samples.

**Data Source:** [GEO Accession GSE212109](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE212109)
**Language** R
**Status:** Research Pipeline

## Analysis Workflow
This script (`SSc Lung.R`) executes an end-to-end bioinformatics pipeline:

### 1. Data Ingestion & Merging
* Imports raw count matrices (HDF5 format) for 5 distinct SSc lung samples.
* Initializes Seurat objects with baseline filtering (min.cells=3, min.features=200).
* Merges individual datasets into a single unified object for comparative analysis.

### 2. Quality Control (QC)
Implemented rigorous filtering criteria to remove low-quality cells and doublets:
* **Library Size:** `1,000 < nCount_RNA < 20,000`
* **Gene Detection:** `nFeature_RNA > 1,000`
* **Mitochondrial Content:** `percent.mt < 20%` (to exclude dying/stressed cells)

### 3. Normalization & Integration
* **Preprocessing:** Log-normalization and scaling of gene expression values.
* **Feature Selection:** Identification of highly variable features for downstream analysis.
* **Integration:** utilized **RPCA (Reciprocal PCA) Integration** to correct for batch effects between samples, ensuring that clusters represent biological differences rather than technical variation.

### 4. Clustering & Dimensionality Reduction
* **PCA:** Linear dimensionality reduction.
* **UMAP:** Non-linear visualization to project high-dimensional data into 2D space.
* **Graph-based Clustering:** `FindNeighbors` and `FindClusters` (resolution 0.5) to delineate cell types.

## Dependencies
* R (4.0+)
* Seurat
* SeuratObject

## How to Run
1.  Download the raw `.h5` files from GSE212109.
2.  Update the file paths in `SSc Lung.R` to match your local directory.
3.  Run the script in RStudio or via command line:
    ```
    source("SSc Lung.R")
    ```

## Outputs
* **Integrated Seurat Object:** A processed R object containing the cleaned, batch-corrected dataset.
* **UMAP Visualization:** A dimensionality reduction plot showing the clustering of distinct lung cell populations.
* CPM - Normalized counts of reads in CPM format.


