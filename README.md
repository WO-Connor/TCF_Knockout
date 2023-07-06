# TCF_Knockout
## TCF.Rmd:
### Chunk 1: setup
Adjusts maximum size, sets seed, and loads required packages.

### Chunk 2: functions
merge.matrices() - Merges matrices by row names.

### Chunk 3: load_data
Loads in first 20 samples from Chromium-SC3Pv3, and for each sample loads cell barcodes, gene ids (features), counts, and metadata.

### Chunk 4: seurat_obj_plus_QC
Creates a Seurat object from data, calculates the percentage of genes that come from the mitochondria in each cell, and filters out doublets, cells with less than 500 genes, and cells with more than 2% mitochondrial genes.

### Chunk 5 & 6: integrate_fns & integrate
normalize_integrate() - Given a Seurat object, list of variables to regress, and number of features for integration, performs SCTransform normalization and integrates.
postintegrate() - Given an integrated Seurat object, number of PCA dimensions, and resolution, runs PCA, UMAP, finds neighbors and clusters.
Normalizes the data with SCTransform across samples, regressing for counts and genes. Integrates over the most variable 3000 genes, runs PCA and UMAP(12 dimensions), and clusters with a resolution of 0.15. 

### Chunk 7: visualize_clusters
Plots UMAP with labels by cluster. Plots UMAP by perturbation and sample, and calculates and plots UMAP by cell cycle based on markers for G2M and S phases. Optionally creates feature plots for mitochondrial percentage, number of transcripts, number of genes, and G2M and S scores with UMAP reductions.

### Chunk 8: cell_type_functions
geneset_marker_overlap.f() - Calculates geneset marker overlap, including the percent of known markers for each cell type that are present in each cluster, and the list of those genes. Also includes reformatting to clean up the data before writing to CSV and creating a barplot for each cluster of cell type and percentage. Saves barplots.

### Chunk 9: find_markers
Sets active identity to clusters, and finds markers that separate each cluster from the rest using MAST and with a logFC threshold of 0.5. Filters these markers to eliminate any downregulated genes (average log2FC value of 0 or less). 

### Chunk 10: cell_type_markers
Reads in 5 sets of cell type markers from [MacParland](https://www.nature.com/articles/s41467-018-06318-7#Sec16), [Aizarani](https://www.nature.com/articles/s41586-019-1373-2#data-availability), [Halpern](https://www.embopress.org/doi/full/10.15252/msb.20209682), and [Zhu](). Performs geneset_marker_overlap.f() on each dataset.

### Chunk 11: module_expression
Creates and saves dot plots for each set of cell type markers using cumulative expression scores for each cluster and cell type. Expression scores are calculated using AddModuleScore() and account for cell complexity by averaging expression of control genes and comparing to the set of interest (https://www.waltermuskovic.com/2021/04/15/seurat-s-addmodulescore-function/). 

### Chunk 12: cell_type_assignment
After manually obtaining a consensus cell type assignment list from the results of chunks 9 and 10, creates a new metadata category for cell type and plots and saves UMAP with labels by cell type.

### Chunk 13: feature_plots
Plots feature plots of pericentral and periportal gene expression using UMAP reductions. ??Need citation for markers??

### Chunk 14: load_hep_data
Subsets integrated Seurat object to only include hepatocyte clusters and save.

### Chunk 15: do_dpt
Calculates the diffusion map using PCAs 1-12 and from this calculates diffusion pseudotime values for each cell. Incorporates these values into the hepatocyte object and creates a scatterplot of the first two eigenvectors from the diffusion map. 

### Chunk 16: one_gene_dpt_fn
plot_gene_dpt_solo() - Splits Seurat object by perturbation and calculates a line of best fit for normalized expression as it relates to diffusion pseudotime using loess for knockout and wild genotypes. Plots these lines on the same plot. 

### Chunk 17: list_genes_dpt_fn
plot_gene_dpt_list() - Runs plot_gene_dpt_solo() for a given list of genes on a given object

### Chunk 18: plot_dpt
Runs plot_gene_dpt_list() on the hepatocyte object for pericentral and periportal marker lists, and Axin and Gpr49 are excluded due to not being in the hepatocyte object.

### Chunk 19 & 20: cumulative_dpt_fn & plot_cumulative_dpt
plot_gene_dpt_cumulative() - Given a Seurat object, genelist, and title, calculates a line of best fit for normalized expression as it relates to diffusion pseudotime using loess for the sum of all expressions of the genes in the list for both wild and knockout genotypes and plots these traces on the same plot.
Plots cumulative normalized expression for lists of pericentral and periportal markers using plot_gene_dpt_cumulative(), with Axin and Gpr49 excluded due to not being in the hepatocyte object.
