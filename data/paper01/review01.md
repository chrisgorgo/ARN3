Freytag and colleagues provide a comprehensive comparison of clustering methods - specifically designed for scRNA-Seq data - on data collected using the popular droplet-based 10x Genomics platform. A total of four datasets, comprising a Gold standard mixture of cell lines as well as three Silver standard PBMC datasets, were compared in terms of accuracy, stability as well as other metrics like runtime and ease of use. Freytag et al also perform an analysis to try to determine the factors influencing the resulting clusterings for the Silver standard datasets.

It is a very challenging task to perform a comprehensive characterization and comparison of clustering methods on such types of high-dimensional data, due to the sheer number of choices that need to be made, the difficulty in establishing ideal performance, and the relative lack of ground truth. Freytag et al do a great job of addressing these challenges and working towards providing an overall recommendation of clustering methods for non-expert practitioners, while stressing the need for careful interpretation of such results. 

With this in mind, I have some comments/suggestions, as well as a number of minor comments/suggestions, as follows:

**Comments to authors**

Linnorm and Monocle failed - expand on why? I understand that this is indeed a limitation especially for a non-expert practitioner, but it would be good to have an understanding towards what the issue might have been.

Could use a flowchart to summarise the study and various comparisons, as well which methods could no longer be compared (e.g. methods that could not work within the scPipe framework).

Different upstream data handling was performed for each clustering method. How much of a difference was observed just due to this preprocessing, as opposed to the actual clustering step? I understand that each method provides their own preprocessing as *part* of the method, but at least some of these methods would have been developed with plate-based and/or non-UMI-based scRNA-Seq in mind, so may not be intended for the context of 10x Genomics data. Again I understand that you're comparing methods 'out of the box' but it would be insightful to see what differences there are. I suggest a figure like an upsetR plot for the genes/cells filtered and a correlation heatmap of the expression values themselves.

Could you summarise the distance metrics used in the clustering and if there is a general flavour to the clustering algorithm? e.g. hierarchical, k-means, density-based etc. How do these relate in terms of overall accuracy, stability and other metrics?

Stability assessment - mentions that half of the 58,302 genes were randomly selected, but Table 1 says 24,654 total genes detected. There's a big discrepancy between these two so please clarify; if half of the 58,302 genes were selected then a large proportion of genes would have identically zero rows. Also Table 1 shows Dataset 3 had the highest number of 'total genes detected', so how was Dataset 1 the one with "most number of non-zero genes after filtering"?

Run time section - What do you mean by 'overridden'? And for which aspects of the analysis steps was this done?

Figure 4 - These boxplots show ARI among multiple clustering solutions, so a method that gives a consistently bad result is still high (e.g. in this case the RCA method). Suggest an analogous set of boxplots but with ARI_truth, is there a similar variability observed, as seen in these boxplots?

Gene-wise stability analysis - I'm actually unsure how realistic this particular comparison is. It would be insightful to assess clusterings depending on different levels of gene filtering stringency (in the initial Cell Ranger read processing), or stringency on selection of features based on various criteria like highly variable genes.

Figure 7 - Please clarify how 'total number of features' is a cell-specific quantity. Do you mean total number of non-zero features? Was this analysis also performed on the Gold Dataset and what overall similarities could be observed?

Factors influencing clustering solutions - It would be interesting to consider the factors associated with 'correct' cluster assignment for cells. Optionally suggest to perform this for either the Gold Dataset or the Silver datasets and perform a logistic regression with the response being success/failure of a cell to belong to the cluster most associated with the 'true' cell type group. There is an added subtlety as far as matching clusters with cell type groups goes, but I think there are a few reasonable ways to perform this (e.g. assign candidate clusters to the 'true' groups by taking the higher proportion of cell overlap, and allow multiple candidate clusters to match to a single true group). Performing this kind of analysis could shed light on properties of cells that don't tend to cluster correctly, and if there is consistency in this across multiple disparate datasets.

**Minor comments**

Table 1 - countClust 'version' formatted with verbatim.

Table 1 - I would suggest the 'properties' column could be better presented in a checklist format, with ticks/crosses for fulfilling various criteria listed.

Section beginning "silver standard" - 10x is capitalised.

Supplementary Figure 1 - legend fallen off panel a), needs a higher resolution or larger points

NMI definition - trailing parenthesis in denominator

typo - assess the effect**

Figure 2a - I found this quite busy, hard to interpret. Suggest to add shading that covers the points for same method or to facet by dataset. I don't believe the ARI values are particularly comparable between datasets so I would prefer facetting by dataset.

Figure 3 - rows/columns are ordered differently between panels, what's driving this difference?

Supplementary Figure 3 was not mentioned in the main text

Supplementary Figure 4 is a two page pdf, with the first page blank

Figure 6 - Figure caption says Dataset 1 but reports 29,151 genes. Do you mean the Gold Dataset and 29,451 genes? If not, please clarify which data and how many genes.

Discussion - One instance of "Seurat" is missing verbatim format
Is the work clearly and accurately presented and does it cite the current literature?

