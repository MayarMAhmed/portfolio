+++
title = "Research"
+++

<nav class="pagenav" aria-label="On this page">
<a href="#drug-discovery">Drug Discovery</a>
<a href="#lignova">LIGNOVA</a>
<a href="#ml-evaluation">ML Evaluation</a>
<a href="#water-benchmark">Docking Benchmark</a>
<a href="#arginine-sensors">Reverse Screen</a>
<a href="#genomics">Genomics</a>
</nav>

Detailed write-ups of my projects, grouped by field: the question, approach, results, and the tools involved. For the condensed version, see my [CV](/cv/) or [publications](/publications/); for a skills overview, see [Skills](/about/#skills).

---

## Drug Discovery & Cheminformatics {#drug-discovery}

### LIGNOVA: Quality-Graded Protein–Ligand Data for ML {#lignova}

*Lead developer · Durrant Lab, University of Pittsburgh · Ongoing · [GitHub](https://github.com/durrantlab/lignova)*

**The problem.** Experimentally solved protein–ligand structures are scarce compared with the bioactivity data in PubChem, which limits the training data available for structure-based ML models.

**Approach.** I built a fully automated, open-source Python/SLURM pipeline that pairs PubChem bioactivity data with experimentally determined receptor structures from the PDB, automates receptor preparation and SMILES-to-3D ligand preparation, and docks each compound with GNINA on HPC. Data ingestion for all of LIGNOVA’s ligands and structures runs through [reqadence](#reqadence), my async REST client library, and validation filters keep only physically plausible poses. I also built similarity-based activity-cliff detection into the pipeline, with assay-quality filters that separate genuine SAR cliffs from assay mismatches.

**Quality grading.** Every protein–ligand pair is graded into Gold, Silver, or Bronze tiers on pose reliability and affinity confidence.

**Scale.** 258M+ docked poses across 5.86M protein–ligand pairs (243,805 ligands, 11,268 protein structures), with 89% of pairs carrying an experimental affinity label. Cliff detection flags 839,044 activity-cliff pairs across 6,356 targets, marking the close-analog cases that ML models tend to struggle with. Scaling is supported by an NSF ACCESS allocation (BIO260240) on Purdue Anvil and TAMU ACES.

**How it evolved.** In 2023 I presented a first workflow of ~350,000 modeled complexes, demonstrated on the oncogenic kinase CLK2 (CADD Gordon Conference). In 2024 I presented the next iteration of the database, validated on human aldose reductase and anaplastic lymphoma kinase (Computational Chemistry Gordon Conference). In 2026 I presented the complete automated, quality-graded pipeline at the Computational Medicinal Chemistry School. Along the way, I've used department seminars to lay out how LIGNOVA's receptor-bound data could support fragment-based lead optimization, both with the Durrant Lab's DeepFrag model and with ML models for fragment linking.

**Tools & methods.** Python, Bash, Linux, SLURM, NSF ACCESS HPC (Purdue Anvil, TAMU ACES), Git / GitHub; GNINA; RDKit, Gypsum-DL, Open Babel, Meeko, MGLTools, PDB2PQR, ProLIF; reqadence, httpx; PubChem, RCSB PDB, and UniProt REST APIs; Polars, PyArrow, Parquet; pose-score calibration, similarity search, pharmacophore search, SAR / activity-cliff detection.

### Stress-Testing a Deep-Learning Affinity Model {#ml-evaluation}

*Lead · Durrant Lab · Built on LIGNOVA data · Ongoing*

**The question.** When a deep-learning scoring function predicts binding affinity well, is it learning protein–ligand chemistry, or leaning on shortcuts?

**Approach.** I benchmarked GNINA's CNN affinity predictions against 5M+ experimental drug–target labels from LIGNOVA across 10,937 proteins, comparing them with AutoDock Vina and with a simple molecular-weight baseline, and used permutation and bootstrap controls to test whether the differences were real. I then used LIGNOVA's activity-cliff pairs to test whether the model can tell apart close analogs with very different potencies.

**Results.** The CNN outranked Vina, but its predicted affinity barely beats ranking by molecular weight (median per-protein ρ 0.29 vs. 0.24) and tracks ligand size, a shortcut the controls confirmed. On activity cliffs in the docked subset, the model is cliff-blind: it predicts ~0.25 pK gaps for 100-fold+ potency differences, and its edge over the molecular-weight baseline shrinks by ~60%.

**Tools & methods.** Python, GNINA (CNN scoring), AutoDock Vina, RDKit, NumPy, SciPy, Polars / pandas, Matplotlib, Seaborn; per-protein rank correlation, baseline comparison, permutation and bootstrap testing, statistical modeling, SAR / activity-cliff analysis.

### Explicit Water vs. Consensus Rescoring in Docking {#water-benchmark}

*Lead author · with A. M. Maldonado and J. D. Durrant · Manuscript in preparation*

**The question.** Explicit-water modeling is expensive and slows virtual screening. Can ligand consensus rescoring (ComBind) stand in for it in pose prediction?

**Approach.** I curated a benchmark of 215 high-quality X-ray complexes and 1,415 PubChem ligands, then compared Glide pose accuracy across three hydration conditions with paired statistical tests to find when consensus rescoring can replace explicit water while preserving screening throughput.

**Tools & methods.** Glide (Schrödinger Suite), ComBind, spyrmsd; similarity search, pose-accuracy (RMSD) benchmarking, paired statistical testing.

### Structure-Based Discovery of Arginine Sensors in Yeast {#arginine-sensors}

*Computational lead · Collaboration with the O'Donnell Lab*

**The question.** Human CASTOR1 is a known arginine sensor, but sequence homology misses candidate arginine-sensing proteins in *S. cerevisiae*.

**Approach.** I ran a structure-based reverse virtual screen: Foldseek structural search against human CASTOR1 structures to find structurally similar yeast proteins, AlphaFold3 modeling, and docking with [MolModa](#molmoda) (browser-based AutoDock Vina) to prioritize candidates. MD pose-stability simulations are ongoing.

**Results.** I nominated 4 candidates. Experimental follow-up by the O'Donnell Lab confirmed altered arginine-homeostasis phenotypes in a subset of them.

**Tools & methods.** Foldseek, AlphaFold3, MolModa / AutoDock Vina, MD simulation, MDAnalysis, UCSF ChimeraX; structural homology search, reverse virtual screening.

### Mentored Project: HIV Protease Conformations with AlphaFold2 {#hiv-protease}

*Co-mentor · TECBio REU, University of Pittsburgh · Summer 2024*

I co-mentored an undergraduate on a ten-week project applying AlphaFold2 to explore HIV protease conformations for drug design, and supervised the resulting research poster, presented at the Research Symposium at Duquesne University.

**Tools & methods.** AlphaFold2; protein conformational analysis, research mentoring.

### reqadence: Async REST Client Foundation {#reqadence}

*Lead developer · [GitHub](https://github.com/durrantlab/reqadence)*

A reusable async base class for REST API clients with retries, rate limiting, and RFC 9111 HTTP caching. It ships a built-in RCSB PDB client, and LIGNOVA's PubChem client subclasses it for large-scale data ingestion.

**Tools & methods.** Python (asyncio), httpx, pytest, Ruff, Black, GitHub Actions, pixi, MkDocs, Git / GitHub; Python packaging, REST APIs (RCSB PDB, PubChem), RFC 9111 HTTP caching, rate limiting and retries, object-oriented design.

### MolModa: Molecular Docking in a Web Browser {#molmoda}

*Co-author · Nucleic Acids Research 2024 · [Paper](https://doi.org/10.1093/nar/gkae406)*

A web-based docking tool that runs protein–ligand docking workflows directly in the browser, with no installation or advanced technical skills required, while preserving data privacy and reproducibility.

**My contribution.** I debugged MolModa during development and conducted the literature review for the paper. I later used it in the [arginine-sensor screen](#arginine-sensors).

**Tools & methods.** AutoDock Vina; browser-based molecular docking.

### Review: Molecular Dynamics Simulations and Drug Discovery {#md-review}

*First author · BMC Biology 2023 · [Paper](https://doi.org/10.1186/s12915-023-01791-z)*

A review of how advances in MD simulations, and their integration with machine learning and quantum approaches, can bridge computational modeling and experimental drug discovery.

**Topics.** Molecular dynamics, machine learning, quantum methods, drug discovery.

---

## Genomics & Bioinformatics {#genomics}

### Comparative Genomics of *Dictyostelium* {#dictyostelium}

*Co-first author · Collaboration with the Levin Lab · PNAS 2025 · [Paper](https://doi.org/10.1073/pnas.2520843122) · [Code](https://github.com/teralevin/dicty_genomes)*

**The question.** How does the social amoeba *Dictyostelium discoideum* maintain the extreme genetic diversity its self/non-self recognition system requires? This is a long-standing puzzle in the evolution of kin recognition known as Crozier's paradox.

**My contribution.** I led the computational genomics. I debugged and adapted the long-read assembly pipeline for SLURM, wrote the annotation and QC modules (tandem repeats, telomeres, transposable elements, rRNA, mtDNA, variant calling, CRAQ), and ran the targeted *tgrB1*/*tgrC1* locus analysis across 10 chromosome-length genomes.

**Results.** The recognition genes *tgrB1* and *tgrC1* sit in a hypermutable genomic hotspot that generates new alleles faster than selection can fix any one of them, resolving Crozier's paradox.

**Tools & methods.** Python, Bash, SLURM, Biopython; Flye (Nanopore / Illumina), minimap2, BWA, samtools, bcftools, bedtools, TRF, RepeatMasker, BLAST, BUSCO, CRAQ, FastQC, MCScanX; long-read genome assembly, variant calling, synteny analysis.

### Predicting Drug Sensitivity in Acute Myeloid Leukemia {#aml}

*Undergraduate thesis · Dr. Eman Badr, Zewail City · Jun 2020 – Apr 2021 · [GitHub](https://github.com/MayarMAhmed/Prediction-of-drug-Sensitivity-in-AML-patients)*

**Approach.** I trained Random Forest regression models (scikit-learn) on patient RNA-seq profiles to predict AML sensitivity to five ERBB inhibitors, and identified genetic markers correlated with differential drug response. Thesis: *Investigating the correlation between molecular variations within Acute Myeloid Leukemia (AML) patients and drug sensitivity*.

**Tools & methods.** Python, scikit-learn; Random Forest regression, supervised learning, feature engineering, RNA-seq / transcriptomics.

### Variant Interpretation in Alzheimer's Disease {#alzheimers-gwas}

*Summer intern · Zewail City · Jun – Dec 2020*

**My contribution.** I interpreted single-nucleotide variants from an ML-based GWAS analysis and ran gene and pathway enrichment analyses to link those variants to Alzheimer's disease progression.

**Tools & methods.** g:Profiler, KEGG; GWAS variant interpretation, gene and pathway enrichment.

### SNP Annotation in TRPV and BRCA Genes (R) {#snp-annotation}

*Undergraduate course project, Bioinformatics · Zewail City · [GitHub](https://github.com/MayarMAhmed/SNP-Calling-R-workflow)*

**Approach.** I built an R/Bioconductor workflow that extracts variants in the TRPV1–3 and BRCA1/2 genes from 1000 Genomes Project VCF files, locates each SNP (coding region, intron, splice site), classifies its consequence (synonymous, missense, frameshift), and predicts the resulting amino-acid changes.

**Results.** 51, 32, and 49 SNPs in TRPV1, TRPV2, and TRPV3 (28, 18, and 28 non-synonymous), 97 in BRCA1 (63 non-synonymous), and 173 in BRCA2 (90+ protein-impacting). Most fell in coding regions, where they could affect protein function, which matters most for the cancer-susceptibility genes BRCA1/2.

**Tools & methods.** R, Bioconductor (VariantAnnotation, TxDb.Hsapiens.UCSC.hg19.knownGene); VCF processing, variant consequence prediction, 1000 Genomes Project data.

### Read-Level Mismatch Detection (samtools) {#read-mismatches}

*Undergraduate course project, Bioinformatics · Zewail City · [GitHub](https://github.com/MayarMAhmed/Detection-and-Visualization-of-Genomic-Mismatches)*

**Approach.** I built a command-line pipeline for a public sequencing run from NCBI SRA: converted SAM to BAM, added MD tags against the reference with `samtools calmd`, then parsed CIGAR strings and MD tags with awk to extract the reads carrying mismatches, along with their positions, and bin them by mismatch count. I sorted and indexed the alignments for downstream viewing.

**Results.** Of ~8,200 alignment records, 659 carried mismatches, most of them (527) single-base.

**Tools & methods.** samtools, awk, Bash; SAM/BAM processing, CIGAR and MD-tag parsing, NCBI SRA data.

### Insulin-Gene SNP Detection with Clinical Lookup (Python) {#insulin-snps}

*Undergraduate course project, Python · Zewail City · Fall 2019 · with Muhammad Esadany · [GitHub](https://github.com/MayarMAhmed/Diabetes-Mellitus-associated-SNP-Detection-Algorithm)*

**What we built.** A Python package that takes a user-supplied insulin gene sequence, validates it (rejecting sequences with insertions or deletions), and compares it against the reference with a custom hash-table method to report each SNP and its position. It then queries a SNP database we built to report each variant's clinical significance.

**Tools & methods.** Python; hash-based sequence comparison, FASTA parsing, SNP database construction.

### UPGMA Phylogenetic Tree Builder (C++) {#upgma}

*Undergraduate course project, C++ programming · Zewail City · [GitHub](https://github.com/MayarMAhmed/Phylogenetic-Tree-Construction-using-UPGMA)*

**Approach.** I built an object-oriented C++ implementation of UPGMA clustering. Starting from a percent-identity matrix computed from NCBI sequences, a `UPGMA` class loads the symmetric matrix, repeatedly merges the two closest taxa by averaging their distances to every other cluster, and logs each merge and its distance. A second program reads that log into a node-based tree and prints the resulting phylogeny.

**Tools & methods.** C++ (object-oriented); UPGMA hierarchical clustering, percent-identity matrices, NCBI sequence data.