Freytag et al. have produced a nice research article on assessing methods for clustering scRNA-seq data from the 10x Genomics platform. I was excited to read the article to learn about what they recommend using. I have made some suggestions below for improvements that are mostly related to providing more intuition and higher-level summaries. This is mostly because as a user of these methods, at the end of the paper, I still felt a little confused about which method the authors would recommend using. I hope the authors can update the article with some of the suggestions:

While the authors have provided detailed comparisons (running time, cluster stability, use of different aligners, different genes, etc), the biggest suggestion would be that the authors provide a higher-level summary of what the authors would suggest a user use to cluster his/her data. At the end of reading this paper, I felt a little overwhelmed at the amount of comparisons across various datasets. It's hard to look at Figs 1-7 and get an overall summary of which method to use. The authors do state in the abstract "We found that some methods, including Seurat and Cell Ranger, outperform other methods, although performance seems to be dependent on the complexity of the studied system", but it would be great if the authors could somehow provide a visual high-level summary of how they came to that conclusion, or elaborate in the discussion on that. 

For the "gold standard" data, what was the percent of each human lung cell lines (HCC827, H1975, H2228) that were mixed together? Equal proportions? Was the reason you needed to use demuxlet was because the cell lines were mixed up for sequencing? It would be great if the authors could elaborate on the experimental design. 

Is the "gold standard" data available with the SNVs called for each cell. It would be useful to have this count matrix and corresponding phenotypic information about each cell in a SingleCellExperiment object for others to have access to. 

It would be great if the authors could include another example dataset with a batch effect in it or something with a slightly less clean design, given most datasets are not quite this "clean". Also, maybe different clustering methods would perform better / worse depending on they data contained rare vs common cell types or included more or less diversity. 

There is a TENxPBMCsData package (https://github.com/kasperdanielhansen/TENxPBMCData) that has been submitted to Bioconductor (similar to the TENxBrainData). This includes all PBMC 10X datasets currently listed on their site and loads in a SingleCellExperiment object into R. For the Silver Standard Datasets, you might incorporate this into your workflow. 

How did you (or Cell Ranger) deal with empty droplets or swapped barcodes on the 10x platform? This seems relevant for discovering cell types using some form of clustering.

Supplemental Table 1 could use a caption and a label at the top saying "Supplemental Table 1". I had many tabs open with different supplemental figures and tables, and was getting confused about which was which one. 

Why did Linnorm and Monocle "continually failed to run"? Did the authors contact the original authors of Linnorm and Monocle to determine if there was a problem with the actual software or if it was a problem with the implementation of the software? It would be great if the authors could elaborate. 

I agree with this statement: " We concede that it is possible that more care in the upstream data handling and selection of parameters could result in different results." This is true for almost all benchmarking papers. Given the authors are working within the R/Bioconductor framework, it would be great if the authors could use something like SummarizedBenchmark (http://bioconductor.org/packages/release/bioc/vignettes/SummarizedBenchmark/inst/doc/SummarizedBenchmark.html) to keep track of these parameters. 

Could the authors elaborate on how they decided which performance metrics to use? 

What does this mean: "The impact of different aligners and preprocessing was assessed using all appropriate combinations of programs"? Could the authors be more specific?

I'm a little concerned about how much the solutions differ between methods and parameter choices. I understand the point of this paper is to make comparisons between already published methods, but as the authors are now very familiar with these methods, it would be great if they could provide some more practical guidance. What would the authors suggest using? 

Fig 1 -- Could the authors hypothesize on why Seurat, TSCAN, RCA, SC3, RaceID, RaceID2 are estimating so many clusters? Also, why does countClust tend to underestimate the number of clusters? It would be great if the authors could provide some intuition. 

Fig 3 -- If I'm understanding, ascend and countClust produce clusters that are very different than the rest? 

Thank you to the authors for making their code publicly available!