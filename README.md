# TCF_Knockout

## TCF_1
### Chunk 1: functions
merge.matrices() - 

group.split() - 

### Chunk 2: load_data
Load in first 20 samples from Chromium-SC3Pv3, and for each sample load cell barcodes, gene ids (features), counts, and metadata.

### Chunk 3: seurat_obj_plus_QC
Create a Seurat object from data, calculate the percentage of genes that come from the mitochondria in each cell, and filter out doublets, cells with less than 500 genes, and cells with more than 2% mitochondrial genes.

### Chunk 3 & 4: sctransform & integrate
Normalize the data with SCTransform across samples, counts, and genes. Integrate, run PCA and UMAP, and cluster. Plot UMAP with labels by cluster.

### Chunk 5: visualize_clusters
Plot UMAP by perturbation and sample and calculate and plot UMAP by cell cycle based on markers for G2M and S phases. Optionally create feature plots for mitochondrial percentage, number of transcripts, number of genes, and G2M and S scores.

### Chunk 6: diff_eq
????

### Chunk 7: cell_type_functions
geneset_marker_overlap.f() - Calculate geneset marker overlap, including the percent of known markers for each cell type that are present in each cluster, and the list of those genes. Also includes reformatting to clean up the data before writing to CSV and creating a barplot for each cluster of cell type and percentage.

### Chunk 8: find_markers
Set active identity to clusters, and find markers that separate each cluster from the rest using MAST and with a logFC threshold of 0.5. Filter these markers to eliminate any downregulated genes (average log2FC value of 0 or less). 

### Chunk 9: cell-type-markers
Read in 5 sets of cell type markers from ***, ***, ***, and ***. Perform geneset_marker_overlap.f() on each dataset.

### Chunk 10: module-expression
Create dot plots for each set of cell type markers using expression scores for each cluster and cell type. Expression scores are calculated using AddModuleScore() and account for cell complexity by averaging expression of control genes and comparing to the set of interest (https://www.waltermuskovic.com/2021/04/15/seurat-s-addmodulescore-function/). 

### Chunk 11: cell-type-assignment
After manually obtaining a consensus cell type assignment list from the results of chunks 9 and 10, create a new metadata category for cell type and plot UMAP with labels by cell type.

## TCF_2:
### Chunk 1: load_hep_data
### Chunk 2: recluster
### Chunk 4: do_dpt
### Chunk 5: scatter_plots
### Chunk 6: feature_plots
### Chunk 7: one_gene_dpt
### Chunk 8: list_genes_dpt
### Chunk 9: plot_dpt
### Chunk 10 & 11: cumulative_dpt & plot_cumulative_dpt
