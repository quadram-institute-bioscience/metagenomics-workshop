---
title: Backmapping
---

When you have an assembly - that is generated using algorithms that focus on some information of your reads but not all of it (for example *k*-mer based assemblers will not make use of the full length of the reads, but only of their *k*-mers) - it is often useful to map back the original reads to the assembly, in order to retrieve information that was not used during the assembly process. This process is called **backmapping** or
**reads recruitment**.

A key concept when backmapping is the **coverage** of the contigs by the reads. Coverage is defined as the average number of reads that align to, or "cover" each base position in a contig. 
High coverage indicates that a contig is well-supported by the original sequencing data, while low coverage may suggest that a contig is less reliable or represents a rare sequence in the sample.

In metagenomics, coverage information is crucial for several reasons:

* **Abundance estimation**: Coverage can be used to estimate the relative abundance of different organisms in a metagenomic sample. Contigs with higher coverage are likely to originate from more abundant organisms.
* **Binning**: Coverage patterns across multiple samples can help in binning contigs into putative genomes, as contigs from the same organism are expected to have similar coverage profiles.
* **Quality assessment**: Coverage can help identify potential assembly errors or chimeric contigs. 

### Gathering the tools

One of the tools we can use (for both Illumina and long reads) is [minimap2](https://github.com/lh3/minimap2). Another popular tool - for shorts reads only - is [BWA](http://bio-bwa.sourceforge.net/).

We can use mamba to install it (alongside with another aligner and utilities):

```bash
mamba create -n mapping -c conda-forge -c bioconda \
  minimap2 bwa samtools bamtocov coverm multiqc
```

### Backmapping Illumina reads with Minimap2

