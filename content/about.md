+++
title = "About Me"
+++

<nav class="pagenav" aria-label="On this page">
<a href="#about">About</a>
<a href="#journey">Journey</a>
<a href="#research">Research</a>
<a href="#software">Software</a>
<a href="#skills">Skills</a>
</nav>

<span id="about"></span>

I'm a final-year Ph.D. candidate (expected April 2027) in the [Durrant Lab](https://durrantlab.pitt.edu/) at the University of Pittsburgh, with five years of drug discovery research at the intersection of computational chemistry and machine learning. My work centers on building large, quality-graded protein–ligand datasets for ML training and testing ML models against experimental data to find where they succeed and where they take shortcuts. Before that, I trained in computational biology and genomics, and I still bring that toolkit to collaborative projects. I'm now seeking industry roles in computational drug discovery, ML for chemistry, and cheminformatics / scientific software, and I'm open to relocation. Here is how I got here.

<span id="journey"></span>

## Journey {#journey}

{{< journey >}}
For the full record, see my [CV](/cv/) and [publications](/publications/).

## Research Highlights {#research}

Each project below has a full write-up (question, approach, results, and tools) on my [Research](/research/) page, alongside my [genomics and bioinformatics work](/research/#genomics).

**[LIGNOVA](/research/#lignova):** An automated, open-source pipeline that has generated 258M+ quality-graded docked poses across 5.86M protein–ligand pairs, 89% of them labeled with experimental affinities, for ML training.

**[ML evaluation](/research/#ml-evaluation):** Benchmarked a deep-learning affinity model against 5M+ experimental labels across 10,937 proteins and exposed a molecular-size shortcut and activity-cliff blindness, confirmed with permutation and bootstrap controls.

**[Docking benchmark](/research/#water-benchmark):** Tested whether consensus rescoring (ComBind) can replace explicit-water modeling in Glide pose prediction on 215 X-ray complexes. Manuscript in preparation.

**[Reverse virtual screen](/research/#arginine-sensors):** Led a structure-based search (Foldseek, AlphaFold3, docking) for yeast arginine sensors that sequence homology misses; a subset of my 4 candidates was experimentally validated by the O'Donnell Lab.

**[Comparative genomics](/research/#dictyostelium):** Led the computational genomics for a co-first-author PNAS paper on how *Dictyostelium* recognition genes evolve so rapidly.

## Software {#software}

Write-ups for each repository are on the [Research](/research/) page.

<div class="repos">

{{< repo name="LIGNOVA" full="durrantlab/lignova" lang="Python · Bash · SLURM" url="https://github.com/durrantlab/lignova" >}}
Fully automated pipeline that turns PubChem bioactivity and PDB data into quality-graded docked protein–ligand complexes for ML training: 258M+ poses across 5.86M pairs. **Lead developer.**
{{< /repo >}}

{{< repo name="reqadence" full="durrantlab/reqadence" lang="Python" url="https://github.com/durrantlab/reqadence" >}}
Async base class for REST API clients with retries, rate limiting, and RFC 9111 caching. Ships a built-in RCSB PDB client and powers LIGNOVA's large-scale PubChem ingestion. **Lead developer.**
{{< /repo >}}

{{< repo name="dicty_genomes" full="teralevin/dicty_genomes" lang="Python · Bash · SLURM" url="https://github.com/teralevin/dicty_genomes" >}}
Long-read assembly, annotation, QC, and targeted *tgrBC* locus analysis in *Dictyostelium* genomes; the pipeline behind the PNAS paper. I adapted it for SLURM and wrote the annotation and QC modules. **Contributor.**
{{< /repo >}}

</div>

## Skills {#skills}

Linked skills jump to the project on my [Research](/research/) page where I used them.

<div class="skills">

<div class="skill-col">

<div class="skill-group">
<h4>Cheminformatics</h4>
<div class="skill-pills"><span><a href="/research/#lignova">RDKit</a></span><span><a href="/research/#lignova">Open Babel</a></span><span><a href="/research/#lignova">Gypsum-DL</a></span><span><a href="/research/#lignova">Meeko</a></span><span><a href="/research/#lignova">PDB2PQR</a></span><span><a href="/research/#lignova">MGLTools</a></span><span><a href="/research/#lignova">ProLIF interaction fingerprints</a></span><span><a href="/research/#lignova">Chemical dataset curation</a></span><span><a href="/research/#lignova">Similarity search</a></span><span><a href="/research/#ml-evaluation">SAR / activity-cliff analysis</a></span><span><a href="/research/#lignova">Pharmacophore search</a></span></div>
</div>

<div class="skill-group">
<h4>ML &amp; Evaluation</h4>
<div class="skill-pills"><span><a href="/research/#ml-evaluation">Model evaluation</a></span><span><a href="/research/#ml-evaluation">Benchmarking vs. baselines</a></span><span><a href="/research/#ml-evaluation">Shortcut / failure-mode analysis</a></span><span><a href="/research/#ml-evaluation">Bootstrap, permutation &amp; paired tests</a></span><span><a href="/research/#lignova">Calibration</a></span><span><a href="/research/#aml">scikit-learn</a></span><span><a href="/research/#aml">Random Forest</a></span><span><a href="/research/#aml">Supervised learning</a></span><span><a href="/research/#aml">Feature engineering</a></span><span>PyTorch</span><span>Graph Neural Networks</span></div>
</div>

<div class="skill-group">
<h4>Programming</h4>
<div class="skill-pills"><span><a href="/research/#lignova">Python</a></span><span><a href="/research/#reqadence">Async Python</a></span><span><a href="/research/#reqadence">Object-oriented design</a></span><span><a href="/research/#reqadence">Python packaging</a></span><span><a href="/research/#lignova">Bash</a></span><span><a href="/research/#snp-annotation">R</a></span><span><a href="/research/#upgma">C++</a></span><span>MATLAB</span></div>
</div>

<div class="skill-group">
<h4>Software Engineering &amp; HPC</h4>
<div class="skill-pills"><span><a href="/research/#lignova">SLURM</a></span><span><a href="/research/#lignova">Linux</a></span><span><a href="/research/#reqadence">REST APIs (PubChem, RCSB PDB, UniProt)</a></span><span><a href="/research/#reqadence">httpx</a></span><span><a href="/research/#reqadence">pytest</a></span><span><a href="/research/#reqadence">GitHub Actions</a></span><span><a href="/research/#reqadence">pixi</a></span><span><a href="/research/#reqadence">Git / GitHub</a></span><span><a href="/research/#reqadence">Ruff</a></span><span><a href="/research/#reqadence">Black</a></span><span><a href="/research/#reqadence">MkDocs</a></span><span>LaTeX</span></div>
</div>

</div>

<div class="skill-col">

<div class="skill-group">
<h4>Docking &amp; Structural Modeling</h4>
<div class="skill-pills"><span><a href="/research/#lignova">GNINA</a></span><span><a href="/research/#water-benchmark">Glide (Schrödinger)</a></span><span><a href="/research/#arginine-sensors">AutoDock Vina</a></span><span><a href="/research/#molmoda">MolModa</a></span><span><a href="/research/#water-benchmark">ComBind rescoring</a></span><span><a href="/research/#water-benchmark">spyrmsd</a></span><span><a href="/research/#arginine-sensors">Virtual screening</a></span><span><a href="/research/#arginine-sensors">Foldseek</a></span><span><a href="/research/#arginine-sensors">AlphaFold3 (co-folding)</a></span><span><a href="/research/#hiv-protease">AlphaFold2</a></span><span><a href="/research/#arginine-sensors">MD simulation</a></span><span><a href="/research/#arginine-sensors">MDAnalysis</a></span><span><a href="/research/#arginine-sensors">UCSF ChimeraX</a></span></div>
</div>

<div class="skill-group">
<h4>Data &amp; Scientific Computing</h4>
<div class="skill-pills"><span><a href="/research/#lignova">Polars</a></span><span><a href="/research/#lignova">PyArrow</a></span><span><a href="/research/#lignova">Parquet</a></span><span><a href="/research/#ml-evaluation">pandas</a></span><span><a href="/research/#ml-evaluation">SciPy</a></span><span><a href="/research/#ml-evaluation">NumPy</a></span><span><a href="/research/#dictyostelium">Biopython</a></span><span><a href="/research/#ml-evaluation">Statistical modeling</a></span><span><a href="/research/#ml-evaluation">Matplotlib</a></span><span><a href="/research/#ml-evaluation">Seaborn</a></span></div>
</div>

<div class="skill-group">
<h4>Genomics &amp; Bioinformatics</h4>
<div class="skill-pills"><span><a href="/research/#dictyostelium">Genome assembly (Flye; Nanopore / Illumina)</a></span><span><a href="/research/#dictyostelium">Alignment (minimap2, BWA, samtools)</a></span><span><a href="/research/#dictyostelium">Variant calling (bcftools, bedtools)</a></span><span><a href="/research/#dictyostelium">Annotation (TRF, RepeatMasker, BLAST)</a></span><span><a href="/research/#dictyostelium">QC (BUSCO, CRAQ, FastQC)</a></span><span><a href="/research/#dictyostelium">Synteny (MCScanX)</a></span><span><a href="/research/#snp-annotation">Variant annotation (R / Bioconductor)</a></span><span><a href="/research/#read-mismatches">Read-level analysis (samtools, awk)</a></span><span><a href="/research/#alzheimers-gwas">GWAS</a></span><span><a href="/research/#alzheimers-gwas">Pathway enrichment (g:Profiler, KEGG)</a></span><span><a href="/research/#aml">RNA-seq / transcriptomics</a></span><span><a href="/research/#upgma">Phylogenetics (UPGMA)</a></span></div>
</div>

<div class="skill-group">
<h4>Languages</h4>
<div class="skill-pills"><span>Arabic — native</span><span>English — fluent</span></div>
</div>

</div>

</div>