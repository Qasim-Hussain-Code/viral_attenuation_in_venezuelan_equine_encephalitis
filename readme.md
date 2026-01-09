# Mapping the Genetic Basis of Viral Attenuation in Venezuelan Equine Encephalitis

## About
This repository provides a reproducible bioinformatics workflow to identify and analyze the genetic mutations responsible for attenuation in Venezuelan Equine Encephalitis Virus (VEEV). By comparing the wild-type Trinidad Donkey (TRD) strain with the live-attenuated TC-83 vaccine strain, the project highlights key regulatory and coding changes that drive the loss of virulence, with a focus on rational vaccine design and evolutionary genomics.

## Abstract
This repository contains a comprehensive bioinformatics pipeline analyzing the genomic determinants of attenuation in **Venezuelan Equine Encephalitis Virus (VEEV)**. 

By systematically comparing the virulent **Trinidad Donkey (TRD)** strain against its derivative, the live-attenuated **TC-83 vaccine** strain, this project elucidates the specific molecular changes—particularly the critical 5' UTR G3A mutation—that drive the trade-off between pathogenicity and immunogenicity. This analysis serves as a case study in **Rational Vaccine Design** and **In Silico Sensitivity Analysis**.

---

## Scientific Context
VEEV is a mosquito-borne alphavirus that can cause severe encephalitis in equids and humans. The TC-83 vaccine was derived from the virulent TRD strain via serial passage in guinea pig heart cells. 

This notebook answers the following research questions:
1.  **Genomic Mapping**: What are the precise Single Nucleotide Polymorphisms (SNPs) separating virulence from attenuation?
2.  **Proteomic Impact**: Which mutations result in non-synonymous (amino acid) changes versus synonymous (silent) changes?
3.  **Evolutionary Dynamics**: What do transition/transversion ratios tell us about the selection pressures applied during attenuation?
4.  **Feature Sensitivity**: Using machine learning (Fisher's Linear Discriminant), which genomic features (e.g., UTR content, dinucleotide bias) are most robustly distinct between virulent and attenuated quasi-species?

---

## Computational Pipeline

The analysis is encapsulated in `veev.ipynb` and follows a modular architecture:

### 1. Data Acquisition & Metadata
*   **NCBI Entrez Integration**: Automated retrieval of GenBank records for L01442 (TRD) and L01443 (TC-83).
*   **Metadata Extraction**: Parsing of taxonomy, organismal source, and collection dates.

### 2. Sequence Alignment & Mutation Detection
*   **Global Pairwise Alignment**: Using Biopython's `PairwiseAligner` to establish homology.
*   **Context-Aware Variant Calling**:
    *   Maps SNPs to specific genomic features (e.g., *nsP1*, *E2*, *3' UTR*).
    *   **Translation Engine**: Translates codons *in silico* to determine functional impact (Synonymous vs. Missense).
    
### 3. Structural & Statistical Analysis
*   **GC Landscape**: Sliding window analysis to visualize genomic stability regions.
*   **Evolutionary Statistics**: Calculation of Ts/Tv ratios and P_N/P_S proxies to estimate purifying selection.
*   **Secondary Structure**: Thermodynamic stability prediction of the critical 5' UTR stem-loop.

### 4. *In Silico* Sensitivity Analysis (Machine Learning)
*   **Quasi-Species Simulation**: Addressing the small sample size (n=2) by generating synthetic mutant swarms (n=200) based on biological constraints.
*   **Feature Sensitivity**: Application of Fisher's Linear Discriminant Analysis to identify genomic features (e.g., CpG suppression, UTR entropy) that fundamentally constrain the virulent phenotype.

---

## Key Findings

1.  **The "Smoking Gun" Mutation**: The analysis confirms a critical transition (G→A) at **position 3** in the 5' UTR. This mutation disrupts the untranslated region's secondary structure, increasing the virus's sensitivity to the host's innate immune response (specifically IFIT1 restriction).
2.  **High Conservation**: The strains share >99.9% identity, highlighting that attenuation is driven by a small number of high-impact regulatory changes rather than broad genomic drift.
3.  **Purifying Selection**: The dominance of synonymous mutations suggests strong evolutionary pressure to maintain the viral proteome structure while altering regulatory elements.

---

## Dependencies

To run this analysis locally, ensure the following Python packages are installed:

```bash
pip install biopython pandas numpy matplotlib seaborn plotly scikit-learn scipy
```

*Note: The notebook includes an automated dependency checker to ensure environment compatibility.*