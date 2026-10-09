# Transcriptomic Analysis of Active Tuberculosis vs Latent TB Infection

Differential gene expression analysis of whole-blood RNA-seq data comparing patients with **active tuberculosis (TB)** to individuals with **latent TB infection (LTBI)**, performed in Python.

## Dataset

- **Source:** NCBI GEO, [GSE101705](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE101705)
- **Study:** Leong S. et al., *Existing blood transcriptional classifiers accurately discriminate active tuberculosis from latent infection in individuals from south India*, Tuberculosis (2018)
- **Samples:** 44 whole-blood samples (28 active TB, 16 LTBI), Illumina NextSeq 500
- **Input:** NCBI-generated raw gene counts (GRCh38.p13)

## Workflow

1. **Data loading:** raw count matrix and sample metadata downloaded directly from GEO
2. **Quality control:** library size check (31–53 M reads per sample, no outliers), low-expression filtering (19,306 of 39,376 genes retained), CPM normalization, log2 transform, PCA
3. **Differential expression:** PyDESeq2 (Python implementation of DESeq2), TB vs LTBI, Benjamini–Hochberg correction
4. **Visualization:** volcano plot and z-scored heatmap of the top 30 genes
5. **Pathway enrichment:** Enrichr (GO Biological Process 2023, KEGG 2021) on genes up-regulated in TB

## Key results

- **1,173 differentially expressed genes** (padj < 0.05, |log2FC| > 1): **1,060 up-regulated** and **113 down-regulated** in active TB
- PCA showed partial separation of TB and LTBI along PC1 (43.9% of variance), with LTBI samples clustering tightly and TB samples more heterogeneous
- Top genes include **BATF2, ANKRD22, APOL4, FCGR1A (CD64), SERPING1, GBP1/5/6, C1QB/C1QC and S100A9**, which overlap with published blood transcriptional signatures of active TB
- Enriched pathways point to **innate immune activation**: defense response to bacterium, antimicrobial humoral response, neutrophil extracellular trap formation, complement activity and oxidative phosphorylation

![Volcano plot](figures/volcano_plot.png)

![Heatmap of top 30 genes](figures/heatmap_top30.png)

![Pathway enrichment](figures/pathway_enrichment.png)

## Interpretation

Active TB is associated with a strong, mostly up-regulated host immune response in blood, driven by interferon-inducible genes (GBP family, BATF2), complement components (C1Q, SERPING1), Fc-gamma receptor signaling (FCGR1A) and neutrophil-related inflammation (S100A9, NETs). These findings reproduce known TB host-response biomarkers and illustrate why blood gene signatures are being studied as non-sputum diagnostic tests for active TB.

## Tools

Python · pandas · NumPy · scikit-learn · matplotlib · seaborn · PyDESeq2 · mygene · GSEApy (Enrichr) · Google Colab

## Repository contents

- `TB_RNAseq_analysis.ipynb`: full analysis notebook
- `figures/`: QC, volcano, heatmap and pathway plots

## Author

**Zhuldyz Boshanova**, B.Sc. Biological Sciences, Nazarbayev University
