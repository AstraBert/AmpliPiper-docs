---
layout: default
title: Troubleshooting
nav_order: 6
---

# Troubleshooting
{:.no_toc }

## Table of contents
{:.no_toc.text-delta }

1. TOC
{:toc}

---

## Installation

Here is a showcase of known potential installation issues, with possible workarounds.

### R

Unable to fix conflicts with libtiff and libdeflate, even though they are uninstalled locally and globally. Switched to manual apt installation (works for Ubuntu, not sure for other Linux distributions):

```bash
## Create an R environment
mamba create -p./envs/R

## Activate the R environment
mamba activate./envs/R

## Install R
sudo apt-get install r-base=4.1.*

## Install R packages
mamba install \
    -y \
    -c conda-forge \
    -c bioconda \
    -c r \
    bioconductor-ggtree r-tidyverse bioconductor-treeio r-phytools

mamba deactivate
```
Unfortunately, only version 4.1.2 is available with apt installation, but it is fine for the pipeline.

### Timeout errors

It is not impossible for mamba installation to fail due to timeout errors. In these cases, it is advised to reinstall the environment manually, running the same command in `setup.sh`.

## Pipeline

We won't discuss all the potential exceptions and problems that one could run into during the pipeline execution. Instead, we will provide general advice on best troubleshooting practices.

### General advice

* If you are not getting the expected results, always check the input data, collate them with the primers, and look at their quality.
* If you are unsure what is causing the problem(s), always check the demultiplexing logs and outputs to start.
* If the visualized MSA does not look good, check for the presence of outliers in the demultiplexed files, specifically look for short PCR byproducts and long chimeric reads.
* Try playing around with the parameters: the pipeline can be really sensitive, so make sure to test some parameter combinations before surrendering to the problems!

## Didn't find what you are looking for?

Check the [issues page on GitHub](https://github.com/nhmvienna/AmpliPiper/issues) and, if you can't find any similar issue, flag one yourself. We'll be on your back as soon as possible!