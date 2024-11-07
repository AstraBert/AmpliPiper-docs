---
layout: default
title: Results
nav_order: 5
---

# Results
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

---

{: .warning }
> SECTION NOT COMPLETED!


## What to expect

After you run the pipeline, the output folder you chose at the beginning should look like this:

```
.
├── data
│   ├── demultiplexed
│   ├── filtered
│   └── raw
├── log
│   ├── SpecDelim
│   ├── SpecID
│   ├── ampliconsorter
│   ├── demulti
│   ├── html
│   ├── summary
│   ├── tree
│   └── variantcalling
├── results
│   ├── SpeciesDelim
│   ├── SpeciesID
│   ├── astraltree
│   ├── consensus_seqs
│   ├── haplotypes
│   ├── html
│   ├── summary
│   ├── tree
|   └── results.html
└── shell
    ├── demult1
    └── demult2
```

## Explanation

### `data` subfolder
This subfolder contains:

* **raw**: raw fastq files, which are a copy of the ones contained in the samples csv file.
* **filtered**: quality-filtered fastq files.
* **demultiplex**: demultiplexed files (with a subfolder for each sample, containing a file for each demultiplexed locus).

### `shell` subfolder
This subfolder contains:

* **demult1**: shell script files for quality filtering and demultiplexing (executed in parallel when allowed).
* **demult2**: shell script files for consensus generation and summarization (executed in parallel when allowed).

### `results` subfolder
This subfolder contains:

* **consensus_seqs**: in this sub-subfolder, we can find a directory for each sample, with a subdirectory for each locus: the Amplicon Sorter-generated consensus sequences are contained in this last level.
* **haplotypes**: in this sub-subfolder, we can find a directory for each locus. In this, we will have a fasta file with the concatenated consensus sequences across all samples for the specific locus, along with their alignments and the MSA visualization image.
* **tree**: in this sub-subfolder, we can find an ML tree for each locus, contained in a dedicated folder. You can also find the tree comparison heatmap and csv file.
* **astral**: in this sub-subfolder, we can find the Astral-generated tree for the concatenated loci, both in pdf and png format.
* **SpeciesDelim**: in this sub-subfolder, we can find the species delimitation outputs by ASAP for each locus and for Astral-concatenated loci. Here, there are partition-based representations, distance-based histograms and cumulative distributions, and text-based reports.
* **SpeciesID**: in this sub-subfolder, we can find the species identification outputs divided according to the database from which they were obtained and subdivided among the loci. For what concerns BOLD outputs, we'll have to pay attention to the _final.csv_ output, which summarizes the overall species identification results.
* **html**: in this sub-subfolder, we can find the html file to ease access to MSA visualization images.
* **results.html**: more about this file in the [Visualization](#visualization) section.

### `log` subfolder

This subfolder contains all the logs for the processes executed throughout the pipeline. It is advised that, if there is any problem with the pipeline, you trace it back here before reporting it, if possible.

## Visualization

The pipeline produces a `results.html` file to facilitate the visualization of the large amount of data output by the pipeline. Note that there are some compatibility issues with Chrome, so it is recommended to access it through other browsers, such as Firefox:

```bash
firefox results.html
```
