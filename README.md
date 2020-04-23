## What is scTPA
### Introduction
scTPA is a web tool for single-cell transcriptome analysis and annotation based on biological pathway activation in human and mice. We collected a large number of biological pathways with different functional and taxonomic classifications, which facilitates the identification of key pathway signatures for cell type annotation and interpretation. 
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
>Seurat
>foreach
>bigstatsr
>data.table
dplyr
scales
ggplot2
cowplot
pheatmap

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
                                                           -o /path/output/results \
```
Once the program has run successfully, a series of results files and folders will appear in the results folder.
### Command

```
Rscript /path/to/you/scTPA/scTPA.R -h
Options:
    -f FILE, --file=FILE
        gene expression profile, genes X cells
    --cellType=CELLTYPE
        cell type file. First column is cell name (same as the colnames of gene expression profile), second column is cell type. No header names.[default= NULL]
    --work_dir=WORK_DIR
        Workshop direction. [default= ./]
    --normalize=NORMALIZE_METHOD
        methods used for normalization. "log", "CLR", "RC" or "scran"[default= none]
    --min_cells=MIN_CELLS
        genes must be in a minimum number of cells. Used for filtering genes[default= 3]
    --min_features=MIN_FEATURES
        cells must have at least the minimum number of genes. Used for filtering cells[default= 200]
    --species=SPECIES
        species. "homo" or "mus"[default= homo]
    --imputation=IMPUTATION
        Imputation method. "scImpute", "magic" or "none"[default= none]
    --data_type=FILE
        data type of gene expression profile，"TPM" or "count"[default= TPM]
    --pathway_database=PATHWAY_DATABASE
        pathway databasem, detials see http://github[default= kegg]
    --user_pathway=USER_PATHWAY
        user defined pathway file，only for gmt format[default = NULL]
    --pas_method=PAS_METHOD
        method for calculating PAS. "gsva", "ssgsea", "zscore" or "plage"[default= ssgsea]
    --para_size=PARA_SIZE
        number of kernels used for parallel[default= 4]
    --cluster_method=CLUSTER_METHOD
        clustering method. "seurat", "hclust", "simlr", "kmedoids", "kmeans" or "dbscan"[default= seurat]
    --seurat_dims=SEURAT_DIMS
        dimensions used in Seurat clustering[default= 8]
    --seurat_resolution=SEURAT_RESOLUTION
        resolution used for Seurat clustering[default= 0.5]
    --k_cluster=K_CLUSTER
        number of clusters, useless if clustering method is Seurat or dbscan[default= 5]
    --min_pts=MIN_PTS
        parameter in DBSCAN[default= 3]
    --dims=DIMS
        number of PCA dimensionas used for TSNE or UMAP[default= 20]
    --marker_method=FIND_MAKER_METHOD
        method of finding siginificant markers[default= wilcox]
    --logFC_thre=THRESHOLD_LOGFC
        threshold of logFC (Detail see Seurat)[default= 0.25]
    --min_pct=MIN_PCT
        only test genes that are detected in a minimum fraction of min.pct cells in either of the two populations.[default= 0.1]
    --pic_type=PIC_TYPE
        type of picture, png or pdf [default= png]
    -o OUT_DIR, --out_dir=OUT_DIR
        output folder[default= NULL]
    -h, --help
        Show this help message and exit
```
#### Details
**`--normalize`:**
***log:*** Log transform. Feature counts output for each cell is divided by the total counts for that cell and multiplied by 1e4. This is then natural-log transformed.
***CLR:*** Centered log ratio. A commonly used Compositional Data Analysis (CoDA) transformation method.
***RC:*** Relative counts. Feature counts output for each cell are is divided by the total counts for that cell and multiplied by 1e4 (for TPM/CPM/FPKM/RPKM this value is 1e6).
***scran:*** The normalization strategy for scRNA-seq is implemented based on the deconvolutional size factor using the scran R package. Detials see [scran](https://github.com/MarioniLab/scran)
***none***: Do not implement normalization
**`--imputation`:**
***scImpute***: Imputing missing value od data matrix following filtering and normalization steps and this function is performed using scImpute R package
***none***: Do not implement imputation.
**`--data_type`:**
***count***:
***TPM***:
**`--pathway_database`:**
when "--species" is "homo", "--pathway_database" can be select as follow:
***kegg***: 
***reactome***:
***biocarta***:
***smpdb***:
***humancyc***:                        
***nci***:
***panther***:
***pharmgkb***:
***acsn2***:
***rb***:
***c2.cgp***:
***c2.cp***:
***c4.cgn***:
***c4.cm***:
***c5.bp***:
***c5.mf***:
***c5.cc***:
***c6.all***:
***c7.all***:
***h.all***:
when "--species" is mus, "--pathway_database" can be select as follow:
***kegg***: 
***reactome***:
***smpdb***:
***pathbank***:
***c5.bp***:
***c5.mf***:
***c5.cc***:
***other***:
**`--cluster_method`:**
***seurat***:
***hclust***:
***simlr***:
***kmeans***:
***kmedoids***:
### Output


