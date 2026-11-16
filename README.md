# Genomics & transcriptomics analyses

Two analyses from the *Genomics and Transcriptomics Analysis* course (MSc Bioinformatics): the algorithms behind read assembly and alignment, implemented from scratch, and a complete single-cell RNA-seq workflow.

## 1. Sequence algorithms for genome assembly and read analysis
[`notebooks/01_sequence_algorithms.ipynb`](notebooks/01_sequence_algorithms.ipynb)

Implemented in plain Python, using few libraries, together with worked solutions by hand:

| Topic | What's implemented |
|---|---|
| Read overlap | `overlap(x, y)`: largest suffix–prefix overlap between two reads; suffix array by hand |
| Graphs | `DiGraph` class with nodes, labelled edges and path search (`has_path`) |
| Assembly | Overlap graph and Hamiltonian paths; de Bruijn graph (k = 3) and Eulerian-path conditions |
| Motifs | Motif likelihood and posterior along a sequence with a sliding window, plotted with matplotlib |
| Read formats | FASTQ/FASTA construction, Phred score ↔ error probability ↔ ASCII encoding |
| Indexing | `BWT` and `IBWT` (Burrows–Wheeler transform and its inverse); substring search with BWT (`give_starting_position`) |
| Sequencing | Base-calling signal of Illumina vs a long-read technology; Phred quality along the read |
| HMM | Likelihood of hidden state paths given emissions |

## 2. Single-cell RNA-seq of the human intestine
[`notebooks/02_single_cell_intestine_scvi.ipynb`](notebooks/02_single_cell_intestine_scvi.ipynb)

A scanpy workflow on a multi-sample subset of intestinal scRNA-seq data:

1. **QC:** genes and counts per cell, mitochondrial fraction, **Scrublet** doublet scores. Filtering at < 5 % MT, doublet score < 0.3 and > 250 counts.
2. **Preprocessing:** median-count normalisation, log1p, 2,000 highly variable genes (batch-aware), PCA, neighbours, UMAP.
3. **Batch integration with scVI:** latent representation learned across samples (`batch_key = sanger_sample_id`), UMAP before and after integration to check that batch effects are removed.
4. **Annotation:** **CellTypist** with the `Adult_Human_Intestine` model, broad marker genes (e.g. *EPCAM*), and **Leiden** clustering on the scVI embedding.

The input data were provided on the course server and aren't included here. The notebook is kept with its outputs (plots) so it can be read without re-running.

**Stack:** Python, scanpy, scvi-tools, CellTypist, pandas, matplotlib.
