# TCF_Knockout
## Setup:
### Chunk 1: setup
Adjusts maximum size, sets seed, and loads required packages.

### Chunk 2: functions
merge.matrices() - Merges matrices by row names.

findgenes() - Search Seurat object for genes starting with specific string

## Whole Liver
### Chunk 3: load_data
Loads in first 20 samples from Chromium-SC3Pv3, and for each sample loads cell barcodes, gene ids (features), counts, and metadata.

### Chunk 4: seurat_obj_plus_QC
Creates a Seurat object from data, calculates the percentage of genes that come from the mitochondria in each cell, and filters out doublets, cells with less than 500 genes, and cells with more than 2% mitochondrial genes.

### Chunk 5 & 6: integrate_fns & integrate
normalize_integrate() - Given a Seurat object, list of variables to regress, and number of features for integration, performs SCTransform normalization and integrates.
postintegrate() - Given an integrated Seurat object, number of PCA dimensions, and resolution, runs PCA, UMAP, finds neighbors and clusters.
Normalizes the data with SCTransform across samples, regressing for mitochondrial percentage, counts, and genes. Integrates over the most variable 3000 genes, runs PCA and UMAP(12 dimensions), and clusters with a resolution of 0.15. 

### Chunk 7: celltypeheatmap
Plots and saves heatmap of expression of known cell type markers from [Lin et al](https://journals.lww.com/hep/fulltext/2024/09000/single_cell_and_spatially_resolved_transcriptomics.18.aspx) by cluster. 

### Chunk 8: cell_type_assignment
After manually obtaining a consensus cell type assignment list from the results of chunk 7, creates a new metadata category for cell type and plots and saves UMAP with labels by cell type.

### Chunk 9: S3D
Creates and saves cell type heatmap for supplement figure 3D. 

### Chunk 10: S3E
Creates and saves plot of cell count by genotype and cluster for supplement figure 3E.

### Chunk 11: F2B
Creates and saves cluster UMAP plot for figure 2B.

### Chunk 12: S3A-C
Creates and saves UMAP plots by mouse, condition, and cell cycle phase for supplement figures 3A-C. Also plots UMAP colored by the # of genes per cell.

## Hepatocytes Only
### Chunk 13: subsetheponly
Subsets integrated Seurat object to only include hepatocyte clusters.

### Chunk 14: umap
Creates and saves cluster UMAP plot by cluster for just the hepatocyte clusters.

### Chunk 15: F2C
Creates and saves UMAP plot colored by the average of z scores of [pericentral and periportal](https://febs.onlinelibrary.wiley.com/doi/full/10.1111/j.1742-4658.2006.05503.x) gene expression.

### Chunk 16: F3A_S4A
Gets average expression data by mouse in the pericentral (HEP2) and periportal (HEP1) hepatocyte clusters for use with MSigDB.

### Chunk 17: WTvsKOvsPCvsPP
Gets average expression data, the number of cells expressing the genes, and p values from t-Tests between genotypes and clusters (HEP1, HEP2). Also adjusts p values using Benjamini Hochberg correction.

### Chunk 18: F2D
Uses results of chunk 17 to plot the log2 fold change of expression in HEP2 compared to HEP1 in both CON and L-KO for figure 2D. 

## Reintegrated Hepatocyte Object
### Chunk 19 reintegrate: 
Normalizes the hepatocyte object into a second hepatocyte object with SCTransform across samples, regressing for mitochondrial percentage, counts, and genes. Integrates over the most variable 3000 genes, runs PCA and UMAP(30 dimensions), and clusters with a resolution of 0.9.


### Chunk 20: dpt
Calculates the diffusion map using PCAs 1-12 and from this calculates diffusion pseudotime values for each cell. Incorporates these values into the hepatocyte object and creates a scatterplot of the first two eigenvectors from the diffusion map. Subclusters 14, 15, 17, and 18 were excluded due to distance from the main body of hepatocytes in the UMAP analysis.

### Chunk 21: getzonatedgenes gam
Runs GAM on plot of DPT vs expression for each gene, then saves genes with significant Bonferroni adjusted p values. 

### Chunk 22: F2E
Counts number of significantly zonated genes by genotype for use in figure 2E.

### Chunk 23: F2F
Creates 8 DPT bins and plots heatmap of all significantly zonated genes clustered by row, creating modules. 

### Chunk 24: F2F cont
Saves modules with gene names for use with Enrichr. 

### Chunk 25: bcatColnotlists
Reads in lists of [$\beta$-Catenin regulated genes](https://aasldpubs.onlinelibrary.wiley.com/doi/pdf/10.1002/hep.26924).

### Chunk 26: F2G
Performs a hypergeometric test on each module with both $\beta$-Catenin lists. 

### Chunk 27: ST2
Creates supplement table 2.

### Chunk 28: F3B
Creates heatmap of glutamine and glutamate gene expression across the lobule for figure 3B. 

### Chunk 29: S4B
Calculates average and standard deviation of gene expression across 8 DPT bins for Pck1 and G6pc for supplement figure 4B
