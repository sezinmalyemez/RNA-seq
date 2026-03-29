# RNA-seq Pipeline - Learning Notes
Sapienza University of Rome / Department of Experimental Medicine / Neuroepigenetics Lab


## About
This repository documents my learning process as an undergraduate research assistant. I followed and observed a complete RNA-seq pipeline run by a PhD student,and ran the DESeq2 differential expression analysis together in RStudio. 

This repository is based on a pipeline recommended by a PhD student in our lab, originally developed by CebolaLab (Imperial College London).

## What I learned
- Quality control of raw sequencing data using FastQC and MultiQC
- Read trimming to remove low quality sequences and adapters (fastp)
- Genome indexing and read alignment using STAR
- Assessment of alignment quality using SAMtools and Qualimap
- Visualization of aligned reads using IGV
- Transcript quantification using Salmon (alignment-based mode)
- Differential gene expression analysis using DESeq2 in R/Studio
- Visualization of results: PCA plots and MA plots


### 0. Setting Up the Environment — Conda

Tools like FastQC, STAR, and Salmon all have different versions and dependencies. Installing them all directly on the computer can cause conflicts. Conda (a virtual environment) solves this by creating an isolated environment for each project, where all tools run independently without interfering with each other.

To create and activate the environment:
```bash
conda create -n RNA-seq
conda activate RNA-seq
```
```bash
conda install -n RNA-seq -c bioconda fastqc
conda install -n RNA-seq -c bioconda fastp
conda install -n RNA-seq -c bioconda samtools
conda install -n RNA-seq -c bioconda deeptools
conda install -n RNA-seq -c bioconda salmon
```


### 1.Quality Control - FastQC & MultiQC

After sequencing, the machine returns raw data consisting of millions of short DNA sequences called "reads". During sequencing, the machine assigns a confidence score to each base it reads - this is called a quality score (Phred score).
Low quality bases mean the machine was uncertain, and including them in the analysis can lead to incorrect results. 

FastQC evaluates the quality of these raw reads by checking:
- Per base quality scores
- Adapter contamination
- GC content
- Duplication rates

```bash
fastqc sample1.fastq.gz -o ./fastqc_results/
# You can add multiple files separated by a space
# fastqc sample1.fastq.gz sample2.fastq.gz -o ./fastqc_results/
```


MultiQC combines FastQC reports from multiple samples into a single summary report, making it easier to compare samples at a glance.
```bash
# Combine all FastQC reports into one summary
multiqc .
# The dot means: use the current working directory
```




