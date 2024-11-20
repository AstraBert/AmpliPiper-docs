---
layout: default
title: Prepare for the pipeline
nav_order: 3
---

# Prepare for the pipeline
{:.no_toc }
You must supply the raw basecalled reads as fastq files, either gzipped or not, with fastq or fq extension. This will then be followed by some simple steps that are described below.
{:.fs-6.fw-300 }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {:.text-delta }
- TOC
{:toc}
</details>

## Primers
First, you need to provide a csv file containing primers and their features, specifically:

* **ID**: The name of the primer/locus
* **FWD**: The forward primer sequence (5'-3')
* **REV**: The reverse primer sequence (5'-3')
* **SIZE**: The expected size of the sequence associated with the locus

You need to pass all the required data in this exact format, and the file will look like this:

```csv
ID,FWD,REV,SIZE
sl_an,CAAGCCCTCCTAGTGCTCAA,ATGATTTTCACAAGCATACCTCAA,780
sl_hue,CAAGCCCTCCTAGTGCTCAA,AAGATTTCCACGAGCATACCTC,780
sl_can,GGATGATGTCTCAAGCCCTTC,TTTTCACGAGCATACCTCAATG,780
sl_6n_per,GATGCCTCAAGCCCTCCTA,AAGATTTCCACGAGCATACCTC,780
```
{: .note }
> _⚠️BE CAREFUL!⚠️: If you are working with Cytochrome c oxidase subunit I, you should set the ID to **COX1**; if you are working with Internal transcribed spacer, you should set the ID to **ITS**;  If you are working with maturase K and/or ribulose 1,5-biphosphate carboxylase, you should set the ID to **MATK_RBCL**. This is needed for the BOLD or BLAST species identification analysis to start! If you do not wish the species identification to take place, just name the locus differently (for instance, instead iof `COX1` you can call it `COI`)_

There is no need to explicitly trim adapters from your fastq files, as the demultiplexing steps take into account their presence. However, make sure not to provide adapters+primers if you have already removed adapters.

## Samples
The input data for the pipeline are fastq files, but to allow multiple fastq files input, you have to list them into a csv document. This document should not have a header and should have the first column representing the name of the sample and the second column reporting the path to the fastq file.

In the end, your samples file will look like this:

```csv
ON_A29_2,/media/user/projects/reads/ON_A29_2.fq.gz
ON_A30_28,/media/user/projects/reads/ON_A30_28.fq.gz
ON_A4_2h,/media/user/projects/reads/ON_A4_2h.fq.gz
ON_A5_29,/media/user/projects/reads/ON_A5_29.fq.gz
ON_A5_3,/media/user/projects/reads/ON_A5_3.fq.gz
```
There is no need for the sample names to match the basenames of the fastq files.

## Usage

{: .warning }
> On 7th November 2024 BOLD upgraded from v4 to v5, causing a dismission of the old API service. The API services are currently migrating, thus they are not available at the moment. If you want to perform species idenfication, we suggest you use BLAST with the `--blast` flag. 

#### Required Arguments

* `-s` or `--samples`: Provide the path to a CSV file containing the names and paths to the raw FASTQ files for each sample.
* `-p` or `--primers`: Provide the path to a CSV file containing the IDs, forward and reverse sequences, and ploidy (1 for haploid, 2 for diploid) of each primer.
* `-o` or `--output`: Specify the path to the output folder.

**Optional Arguments**

* `-b` or `--blast`: Enable BLAST search for species identification. When setting this parameter, you need to provide an email address (e.g., `--blast your@email.com`) for using NCBI entrez to retrieve taxonomic information for the BLAST hits (default: disabled).
* `-c` or `--similar_consensus`: Specify the threshold percentage similarity at which two sequences get clustered together to form a single consensus (default: 97)
* `-e` or `--exclude`: Provide a text file with samples and loci to exclude from the analysis. Each row should contain the ID of a sample to be excluded. Names need to be identical to the IDs in `samples.csv`
* `-f` or `--force`: Force overwrite the output folder if it already exists (default: cowardly refusing to overwrite).
* `-i` or `--partition`: Use partition model for iqtree with combined dataset. :warning: may take very long :warning: (default: disabled)
* `-k` or `--kthreshold`: Define the threshold *k* for the maximum allowed proportion of mismatches for primer alignment during demultiplexing (default: 0.05).
* `-m` or `--minreads`: Set the minimum number of reads required for consensus sequence reconstruction (default: 100).
* `-n` or `--nreads`: Provide the absolute number or percentage of top-quality reads to consider for consensus sequence generation and variant calling (default: 500).
* `-o` or `--outgroup`: Provide the ID of an sample that gets to be considered as an outgrouop by ASTRAL in the combined tree reconstruction.
* `-q` or `--quality`: Specify the minimum PHRED quality score for read filtering (default: 10).
* `-r` or `--sizerange`: Define the allowed size buffer in basepairs around the expected locus length (default: 100).
* `-t` or `--threads`: Specify the number of threads to be used for parallel processing (default: 10).
* `-w` or `--nowatermark`: Remove the watermark from the phylogenetic tree images (default: disabled).
* `-y` or `--freqthreshold`: Retain consensus sequences for further analyses which are supported by raw reads, whose frequency in the total pool of reads is larger or equal to this threshold (default: 0.1).

#### Example command

⚠️ In the following command, make sure to **replace `<path_to>` with the actual path to your files** ⚠️

```bash
bash <path_to>/shell/AmpliPiper.sh \
    --samples <path_to>/testdata/data/samples.csv \
    --primers <path_to/testdata/data/primers.csv \
    --output <path_to>/testdata/results/demo \
    --quality 10 \
    --nreads 1000 \
    --blast your@email.com \
    --similar_consensus 97 \
    --threads 200 \
    --kthreshold 0.05 \
    --minreads 50 \
    --sizerange 100 \
    --outgroup He_mor_41 \
    --force
```

This will execute the pipeline and save the output in the `demo` folder. 

If you want to test the pipeline on a test dataset, please check out the `testdata/` folder within our repository and execute the commands in the `testdata/main.sh` shell script.

## Best practices

The following section provides some advice on how to set the parameters for the pipeline:

* `-k` or `--kthreshold` should be set as quite strict (< 0.1) to ensure improved adherence of the demultiplexed sequences to the desired ones.
* `-r` or `--sizerange` can be set liberally (> 200), but be cautious when defining it, as we want to avoid including very short PCR byproducts or very long chimeras.
* `-n` or `--nreads`: 500 reads is generally a sweet spot for the underlying consensus-generating software. However, consider exploring other possibilities if this does not produce the desired output.
* `-m` or `--minreads`: a minimum threshold of less than 100 reads can lead to a lack of output from the underlying consensus generation software.
* `-c` or `--similar_consensus`: setting this flag too high (>98) or too low (90>) can result in an excess of reconstructed haplotypes on one hand and in a loss of them on the other.

If you are having a hard time with the pipeline's output, always try experimenting with the parameter settings. If the problems persist, check out [troubleshooting](./search.md) or [flag an issue on GitHub](https://github.com/nhmvienna/AmpliPiper/issues).
