# 🧬 Unsupervised Learning in Endometrial Cancer: Discovering Molecular Subtypes

Endometrial cancer affects over 65,000 women annually, yet current clinical classification relies on crude histological grade and surgical stage—measures that fail to predict treatment response or prognosis in many patients. This project applies unsupervised machine learning to RNA-seq gene expression data from 566 endometrial cancer patients to discover **molecular subtypes with distinct survival outcomes**.

By combining dimensionality reduction (PCA), consensus clustering (K-Means and Hierarchical methods), and statistical biomarker discovery, we identify three robust patient clusters that differ significantly in survival rates and have distinct genetic signatures. The goal: move toward precision medicine by linking transcriptional heterogeneity to clinical outcomes.

## Approach

**Dimensionality Reduction (PCA)**: Reduce 60,660 genes to 25 principal components while retaining interpretability.

**Cluster Identification**: Apply both K-Means and Hierarchical clustering to find optimal patient groupings. Validate agreement between methods (concordance analysis).

**Cluster Validation**: Compare clustering solutions using silhouette scores, elbow method, and dendrogram inspection. Prove clusters reflect true biology, not algorithm artifacts.

**Clinical Integration**: Link molecular clusters to survival outcomes using Kaplan-Meier analysis and Log-Rank tests. Assess whether clusters differ by stage, age, and vital status.

**Biomarker Discovery**: Identify differentially expressed genes per cluster using one-vs-rest t-tests with Benjamini-Hochberg FDR correction. Highlight top 15 master-regulator genes per cluster.

**Literature Comparison**: Compare discovered subtypes and biomarkers against the established TCGA 2013 molecular classification (POLE, MSI, CN-Low, CN-High) and other studies.

## Dataset

- **RNA-seq Gene Expression**: 60,660 protein-coding genes from 566 endometrial cancer patients (log₂ TPM+1 transformed, TCGA-UCEC cohort)
- **Clinical Metadata**: Patient age, FIGO stage, tumor grade, vital status, days-to-death (survival proxy)
- **Preprocessing**: Highly variable gene selection (1,500 genes), robust scaling, outlier investigation

*Note: Raw TCGA-UCEC data files are referenced in the notebook but are externally hosted. Access via GDC Portal or analyze directly in the notebook environment.*

## Key Findings

- **Three robust molecular clusters** identified with distinct gene expression profiles and survival rates
- **Cluster 1**: Likely corresponds to genomically unstable (CN-High) subtype—intermediate survival, higher stage concentration
- **Cluster 2**: Likely corresponds to low-copy-number or MSI subtypes—better survival, indolent phenotype
- **Cluster 0**: Rare outliers with extreme expression patterns—potential ultra-high or ultra-low risk subgroup
- **Top biomarkers per cluster** discovered (e.g., genes most consistently upregulated in each cluster), validated with FDR < 0.05 (also applying benjamini Hochberg).
- **PCA reveals** that first 25 components capture 51% of variance; biological clustering emerges on 2D/3D projections

## Limitations & Future Work

**Limitations**:
- PCA's linearity may obscure non-linear cluster boundaries (future: apply UMAP, t-SNE)
- Extreme sample size imbalance in Cluster 2 (n=4) limits statistical power
- Missing genomic annotations (TP53 mutations, MSI status, PTEN loss) prevents direct TCGA subtype mapping
- Cross-sectional design limits causal claims about gene-phenotype relationships
- Do different clustering techniques like dbmaps, on density clustering or different techniques.
- Reducing 1,500 High-Variance Genes to 25 Principal Components captured 51% of the total variance.

**Future Directions**:
- Validate clusters in independent endometrial cancer cohorts (ICGC, recent TCGA batches)
- Obtain molecular annotations (POLE mutations, MSI testing, copy number profiles) for functional validation
- The cluster 0's small sample size (n=7) (probably reduced by the outlier reduction done of the value > 800) is an inherent limitation. Future work should recruit additional CN-High UCEC cases to confirm or refute this subtype's boundaries. 
- Perform CRISPR knockdowns on top biomarkers to establish causality
- Expand clinical correlations (recurrence patterns, treatment response, chemotherapy toxicity)

## Files

| File | Description |
|------|-------------|
| **[unsupervised_genes.ipynb](./unsupervised_genes.ipynb)** | Full Jupyter Notebook — Data exploration, PCA, K-Means, hierarchical clustering, concordance analysis, clinical integration, biomarker discovery, literature review, and conclusions |
| **[unsupervised_genes.html](./unsupervised_genes.html)** | Static HTML export — Readable without running code; includes all visualizations and results |
| **TCGA-UCEC RNA-seq data** | Gene expression matrix (60,660 genes × 566 patients). Access via [GDC Portal](https://portal.gdc.cancer.gov/) or analyze directly in the notebook environment |
| **TCGA-UCEC Clinical Data** | Patient demographics, staging, survival outcomes. Included in notebook; reference TCGA documentation for full data dictionary |
   
## References 
1. The Clinical Gold Standard (The 2013 TCGA Benchmark)
**Cancer Genome Atlas Research Network. (2013).** *Integrated genomic characterization of endometrial carcinoma.* **Nature**, 497(7447), 67–73. https://doi.org/10.1038/nature12113

2. Yin, H., et al. (2022). Novel DNA Damage-Related Subtypes Characterization Identifies Uterine Corpus Endometrial Carcinoma (UCEC) Based on Machine Learning. Journal of Oncology, 2022, 3588117. https://doi.org/10.1155/2022/3588117

3. The Impact of Endometriosis on Women's Health
**Zondervan, K. T., Becker, C. M., & Missmer, S. A. (2020).** *Endometriosis.* **The New England Journal of Medicine**, 382(13), 1244–1256. https://doi.org/10.1056/NEJMra1810764

4. The Biological Subtypes (POLE, MSI, CN-Low, CN-High)
**Cancer Genome Atlas Research Network. (2013).** *Integrated genomic characterization of endometrial carcinoma.* **Nature**, 497(7447), 67–73. [https://www.nature.com/articles/nature12113](https://www.nature.com/articles/nature12113)

5. Siegel, R. L., Miller, K. D., Wagle, N. S., & Jemal, A. (2023). *Cancer
statistics, 2023.* **CA: A Cancer Journal for Clinicians**, 73(1), 17–48.
https://doi.org/10.3322/caac.21763
