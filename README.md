## What is scTPA
### Introduction
The scTPA is a web tool for single-cell transcriptome analysis and annotation based on biological pathway activation in human and mouse. We collected a large number of biological pathways with different functional and taxonomic classifications, which facilitates the identification of key pathway signatures for cell type annotation and interpretation.
### What can scTPA do
* pre-processing of scRNA-seq data
* calculating pathway activity score
* dimension reduction of scRNA-seq data
* clustering of cell population by different methods
* finding significantly activate pathway in supervised pr unsupervised manner
* overview of associated gene expression profiles in pathways
## Usage
### Install
* **step1 Download scTPA**
scTPA can be download directly  from `Download ZIP` button. Alternatively, scTPA can be installed through github: enter the directory where you would like to install scTPA and run
```
git clone https://github.com/yupenghe/methylpy.git
cd scTPA/
```
* **step2 Install dependent R packages**
For using scTPA, user must install following packages,:
```
## for analysis
Seurat
## for parallel
foreach
bigstatsr
data.table
## for visualization
dplyr
scales
ggplot2
cowplot
pheatmap
```
To install this packages, start "R" and enter:
```
if (!requireNamespace(c("Seurat","bigstatsr","data.table","foreach","dplyr","scales","ggplot2","cowplot","pheatmap"), quietly = TRUE))
    install.packages(c("Seurat","bigstatsr","data.table","foreach","dplyr","scales","ggplot2","cowplot","pheatmap"))
```
* **step3 Install optional R packages**
If user want to use some specialized method in scTPA, the following R packages are required.
1. `scran` for "scran" normalization method
2. `scImpute` for "scImpute" imputation method
3. `SIMLR` for "simlr" clustering method
4. `dbscan` for "dbscan" clustering method 
**scran**
```
if (!requireNamespace("BiocManager", quietly = TRUE))
    install.packages("BiocManager")
if (!requireNamespace("scran", quietly = TRUE))
    BiocManager::install("scran")
```
**scImpute**
```
if (!requireNamespace("devtools", quietly = TRUE))
    install.packages("devtools")
if (!requireNamespace("scImpute", quietly = TRUE))
    devtools::install_github("Vivianstats/scImpute")
```
**SIMLR**
```
if (!requireNamespace("devtools", quietly = TRUE))
    install.packages("devtools")
if (!requireNamespace("scImpute", quietly = TRUE))
    devtools::install_github("Vivianstats/scImpute")
```
**dbscan**
```
if (!requireNamespace("dbscan", quietly = TRUE))
    BiocManager::install("dbscan")
```
### Test scTPA
```
Rscript /path/to/you/scTPA/scTPA.R -f /path/to/you/scTPA/test/test.csv \
                                                           --work_dir /path/to/you/scTPA/ \
                                                           --species homo \
                                                           --pathway_database kegg \
                                                           --para_size 1 \
                                                           --pas_method gsva \
                                                           --cluster_method seurat \
                                                           --pic_type png \
                                                           -o /path/to/you/scTPA/test/results \
```
Once the program has run successfully, a series of results files and folders will appear in the results folder.
### Command
 
### Output
