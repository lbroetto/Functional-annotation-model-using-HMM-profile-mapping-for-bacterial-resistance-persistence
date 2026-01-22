# Functional-annotation-model-using-HMM-profile-mapping-for-bacterial-resistance-persistence

This repository contains custom pHMM (profile Hidden Markov Model) libraries for identifying bacterial resistance and persistence-associated protein domains. 

Functional annotation model using (deep-dense) mapping guided by HMM (Hidden Markov Models) profiles (Rational design of functional annotation models based on pHMMs for genome prospecting).
Source databases: two custom pHMM libraries were constructed de novo for this study. Reference pHMMs representing protein families with established roles in antimicrobial resistance (e.g., efflux pumps, beta-lactamases, ribosomal protection proteins) and bacterial persistence (e.g., toxin-antitoxin systems, stress response regulators, metabolic regulators) were retrieved from curated public databases. These included Pfam v36.0, TIGRFAMs/NCBIFAMs, and PANTHER v18.0. Retrieval was performed via the InterPro resource using targeted keyword searches (e.g., "multidrug efflux," "TA system") and specific accession numbers.

Libraries were compiled by Leonardo Broetto (leonardo.broetto@arapiraca.ufal.br, Lbroetto@gmail.com)

These libraries were developed and validated in the study:

**Exploring the Molecular Basis of Potassium Usnate Activity Against Staphylococcus warneri Persistence and Resistance Through Protein Interaction Networks and Molecular Docking**  
*Submitted to: Network Modeling Analysis in Health Informatics and Bioinformatics (Springer Nature)*

# Contact
**Authors:** Leonardo Broetto
**Correspondence:** Lbroetto@gmail.com, leonardo.broetto@arapiraca.ufal.br
**Affiliation:** Núcleo de Pesquisa em Bioinformática e Filogenômica, Universidade Federal de Alagoas, Brasil

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

# Output Processing Example:  

import pandas as pd

# Parse HMMER tabular output
columns = ['target', 'accession', 'query', 'accession_q', 'E-value', 
           'score', 'bias', 'domain_E', 'domain_score', 'domain_bias',
           'exp', 'reg', 'clu', 'ov', 'env', 'dom', 'rep', 'inc']

results = pd.read_csv('resistance_results.txt', 
                      comment='#',
                      delim_whitespace=True,
                      names=columns,
                      header=None)

# Filter significant hits (E-value ≤ 1e-03, coverage ≥ 50%)
significant = results[results['E-value'] <= 1e-03]
print(f"Significant resistance hits: {len(significant)}")

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
This project is licensed under the MIT License:
Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the “Software”), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED “AS IS”, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

Please cite:
- Primary Citation (this resource): Marcio Renan Santos Tavares, Nayara Andreo, Teresa de Lisieux Guedes Ferreira Lôbo, Chirles Araújo de França, Wagner Pereira Felix, Maria Aparecida Scatamburlo Moreira, Vasco Ariston de Carvalho Azevedo, Bertram Brenig, Leonardo Broetto, Mateus Matiuzzi da Costa (2026). Exploring the Molecular Basis of Potassium Usnate Activity Against Staphylococcus warneri Persistence and Resistance Through Protein Interaction Networks and Molecular Docking. Network Modeling Analysis in Health Informatics and Bioinformatics (under review).
- HMMER Software: Eddy, S. R. (2011). Accelerated Profile HMM Searches. PLoS Computational Biology, 7(10), e1002195. https://doi.org/10.1371/journal.pcbi.1002195
