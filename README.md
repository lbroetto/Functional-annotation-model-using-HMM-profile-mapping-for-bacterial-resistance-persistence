# Functional annotation model using HMM profile mapping for bacterial resistance-persistence

[![Article](https://img.shields.io/badge/Article-Published-green.svg)](https://doi.org/10.1007/s13721-026-00767-7)

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.18944678.svg)](https://doi.org/10.5281/zenodo.18944678)

This repository contains custom pHMM (profile Hidden Markov Model) libraries for identifying bacterial resistance and persistence-associated protein domains. 

Functional annotation model using (deep-dense) mapping guided by HMM (Hidden Markov Models) profiles (Rational design of functional annotation models based on pHMMs for genome prospecting).
Source databases: two custom pHMM libraries were constructed de novo for this study. Reference pHMMs representing protein families with established roles in antimicrobial resistance (e.g., efflux pumps, beta-lactamases, ribosomal protection proteins) and bacterial persistence (e.g., toxin-antitoxin systems, stress response regulators, metabolic regulators) were retrieved from curated public databases. These included Pfam v36.0, TIGRFAMs/NCBIFAMs, and PANTHER v18.0. Retrieval was performed via the InterPro resource using targeted keyword searches (e.g., "multidrug efflux," "TA system") and specific accession numbers.

Libraries were compiled by Leonardo Broetto (leonardo.broetto@arapiraca.ufal.br, Lbroetto@gmail.com)

These libraries were developed and validated in the published manuscript:

**Exploring the Molecular Basis of Potassium Usnate Activity Against Staphylococcus warneri Persistence and Resistance Through Protein Interaction Networks and Molecular Docking**

**Published in:** *Network Modeling Analysis in Health Informatics and Bioinformatics* (Springer Nature), 2026  
**Article DOI:** [10.1007/s13721-026-00767-7](https://doi.org/10.1007/s13721-026-00767-7)

# Contact
**Authors:** Leonardo Broetto
**Correspondence:** Lbroetto@gmail.com, leonardo.broetto@arapiraca.ufal.br
**Affiliation:** Núcleo de Pesquisa em Bioinformática e Filogenômica (NPBF), Universidade Federal de Alagoas, Brasil

---

# Repository Contents
pHMM Libraries Included:
1. Resistance-pHMM-library_72.hmm - Profile HMMs for antibiotic resistance-associated protein families. Includes ABC transporters, efflux pumps, beta-lactamases, and other resistance determinants curated from experimentally validated resistance protein families.
2. Persitence-pHMM-library_23.hmm - Profile HMMs for persistence/tolerance-associated protein families Includes toxin-antitoxin systems, stress response regulators, and dormancy-related proteins compiled from known curated persistence mechanisms across bacterial species.

# Usage Instructions
1. Prerequisites
Install HMMER 3.4 from http://hmmer.org/
HMMER Documentation: http://hmmer.org/documentation.html

2. Basic Search Command:
- For resistance protein identification  
$ hmmsearch --tblout resistance_results.txt -E 1e-03 --max Resistance-pHMM-library_72.hmm your_proteome.faa
- For persistence protein identification  
$ hmmsearch --tblout persistence_results.txt -E 1e-03 --max Persitence-pHMM-library_23.hmm your_proteome.faa

# For Reproducibility and Reuse:
Search command: the search was executed with stringent parameters to ensure high-confidence hits:  
$ hmmsearch --tblout <output_file.txt> -E 1e-03 --max <library.hmm> <proteome.faa>
Execution: this command was run independently for each combination of pHMM library (resistance, persistence) and each of the eight predicted proteomes analized on project, generating 16 individual output files.

# Expected Output Format
- The tabular output includes: Target sequence identifier, Query pHMM identifier, E-value (statistical significance), Bit score (alignment quality), Domain boundaries, Alignment coordinate

# Statistical Validation Parameters
- Search Parameters Used in Original Study:
E-value threshold: 1e-03 (statistical significance cutoff)
Database size correction: Applied via HMMER's built-in mechanisms
Multiple testing adjustment: Bonferroni correction for proteome-wide searches
Coverage requirement: ≥50% of pHMM model length
Independent executions: 2 libraries × 8 proteomes = 16 searches

- Justification of Stringent Parameters:
The 1e-03 E-value threshold was selected based on:
Benchmarking studies showing optimal balance of sensitivity/specificity
Domain architecture conservation in resistance/persistence proteins
Reduction of false positives in large-scale proteome analyses
Comparability with established functional annotation pipelines

# Integration with Other Tools
These pHMM libraries are compatible with:
AntiSMASH (for biosynthetic gene cluster analysis)
Prokka (for prokaryotic genome annotation)
Roary (for pangenome analysis)
Custom Python/R scripts via Biopython/Bioconductor

# License and Citation
### Please cite:
- Primary Citation: Exploring the Molecular Basis of Potassium Usnate Activity Against Staphylococcus warneri Persistence and Resistance Through Protein Interaction Networks and Molecular Docking. *Network Modeling Analysis in Health Informatics and Bioinformatics*. https://doi.org/10.1007/s13721-026-00767-7

- Broetto, L. (2026). Functional annotation model using HMM profile mapping for bacterial resistance-persistence (v1.1.0) Version associated with published article [Computer software]. Zenodo. https://doi.org/10.5281/zenodo.18944678

- HMMER Software: Eddy, S. R. (2011). Accelerated Profile HMM Searches. PLoS Computational Biology, 7(10), e1002195. https://doi.org/10.1371/journal.pcbi.1002195

If you use this annotation model in your research, please cite:

### For the pHMM libraries:
```bibtex
@software{broetto_phmm_libraries_2026,
  author       = {Leonardo Broetto},
  title        = {{Functional annotation model using HMM profile mapping for bacterial resistance-persistence}},
  month        = jan,
  year         = 2026,
  publisher    = {Zenodo},
  version      = {v1.0.0},
  doi          = {10.5281/zenodo.18944678},
  url          = {https://doi.org/10.5281/zenodo.18944678}
}
```

This project is licensed under the **GNU General Public License v3.0**.

### Terms for Academic/Research Use:
- Free to use, study, and modify
- Must distribute derivatives under GPLv3
- Must provide source code when distributing binaries
- Must preserve copyright notices and license text

### Terms for Commercial Use:
For commercial applications or proprietary integration, please contact the author (Lbroetto@gmail.com, leonardo.broetto@arapiraca.ufal.br) to discuss alternative licensing options.

**Full license text:** [LICENSE](LICENSE)

### Copyright and Licensing
- **Copyright Holder:** Leonardo Broetto  
- **License:** GNU General Public License v3.0  
- **Year:** 2026

### Research Attribution
The computational methodologies implemented in this software were developed as part of research activities conducted by Leonardo Broetto. Associated research work is linked to Universidade Federal de Alagoas.

### Usage Terms
- **Academic/Research Use:** Permitted under GPLv3 with mandatory citation
- **Commercial Use:** Requires alternative licensing (contact author)
- **Derivative Works:** Must be released under GPLv3

### Contact for Licensing
Leonardo Broetto  
Lbroetto@gmail.com, leonardo.broetto@arapiraca.ufal.br
(Associated with Universidade Federal de Alagoas)
