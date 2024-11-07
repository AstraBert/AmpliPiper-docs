---
layout: default
title: Home
nav_order: 1
description: "AmpliPiper is a comprehensive modular pipeline that is able to perform a wide variety of downstream tasks on raw, basecalled, Oxford Nanopore long reads."
permalink: /
---

# AmpliPiper
{: .fs-9 }

AmpliPiper is a comprehensive yet modular pipeline that is able to perform a wide variety of downstream tasks on raw, basecalled, Oxford Nanopore long reads.
{: .fs-6 .fw-300 }

[Get started now](#quickstart){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 }
[View it on GitHub](https://github.com/nhmvienna/AmpliPiper){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 }

---

<div align="center">
    <img src="https://img.shields.io/badge/Language-Bash-Green" alt="Static Badge">
   <img src="https://img.shields.io/badge/Production_status-Beta-green" alt="Static Badge">
   <img src="https://img.shields.io/badge/Release-v0.2.0_beta-purple" alt="Static Badge">
   <img src="https://img.shields.io/badge/Requires-Mamba_and_Conda-red" alt="Static Badge">
   <img src="https://img.shields.io/badge/Supported_platforms-linux/macOS-brown" alt="Static Badge">
   <div>
        <a href="https://github.com/nhmvienna/AmpliPiper"><img src="./assets/images/AmpliPiper_logo.png" alt="AmpliPiper Logo" align="center"></a>
   </div>
   <br>
    <div style="display: flex;">
        <img src="./assets/images/tettris.png" alt="TETTRIS project logo" style="width: 60%; height: auto; padding-right: 20px;">
        <img src="./assets/images/nhm.svg.png" alt="NHM logo" style="width: 40%; height: auto; padding-left: 20px;">
    </div>
    <br>
</div>

---

{: .warning }
> This website documents the features of the current release (v0.2.0-beta) of AmpliPiper. See [the CHANGELOG]({% link CHANGELOG.md %}) for a list of releases, new features, and bug fixes.

**AmpliPiper** is a pipeline developed by the Naturhistorisches Museum Wien to tackle most of the challenges posed by amplicon sequencing, and its ultimate goal is to provide the user with a comprehensive tool that is able to automatically perform the following tasks in a single run:

* Quality filtering and size selection
* Demultiplexing
* Consensus sequence generation
* Variant calling
* Haplotype calling
* Phylogenetic reconstruction
* Species delimitation
* Species identication


Browse the documentation to learn more about how to use this pipeline!

## Quickstart

Here you'll get a quick tour of the pipeline:

* **Installation**: To install the pipeline you should have mamba and conda up and running on your machine. Once you are all set, clone [the GitHub repository](https://github.com/nhmvienna/AmpliPiper):

```bash
git clone https://github.com/nhmvienna/AmpliPiper
cd AmpliPiper
```

Then run:

```bash
bash shell/setup.sh
```

* **Installation test**: To test that everything is working and get information on the options you can input the pipeline with, run:

```bash
bash shell/AmpliPiper.sh -h
```

* **Your first usage**: Now that you had a rapid tour of the pipeline's usage, get ready for the first trial. You can use the test data that our repository offers, just make sure to **replace `<path_to>` with the actual path to your files**. You can then run:

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

* **Read your results**: This previous command will generate all the outputs in the `results/demo` folder: to see a summary of them, run:

```bash
firefox <path_to>/testdata/results/demo/results.html
```

{: .note }
See the repository [README][Pipeline README] for a more detailed quickstart.

## About the project

### Contributors

**AmpliPiper** is developed, distributed and maintained by Martin Kapun (NHMW), Sonja Steindl (NHMW) and Astra Clelia Bertelli (NHMW, University of Pavia).

### Acknowledgments

The present documentation is written with Just the Docs, which is &copy; 2017-{{ "now" | date: "%Y" }} Jekyll theme by [Patrick Marsceill](https://patrickmarsceill.com).

We wish to thank all the amazing people that supported the project and shared advice or opinions about it, as well as all the teams and people behind the software employed in our pipeline.

{: .note }
This project is being developed as part of [TETTRIs - Task 6.2, WP6](https://tettris.eu/).

### License

**AmpliPiper** is [an open source project](https://github.com/nhmvienna/HAPLOTYES/blob/main/LICENSE) distributed under GPL-3.

### Contributing

When contributing to this repository, please first discuss the change you wish to make via issue,
email, or any other method with the owners of this repository before making a change. 

----

[^1]: The [source file for this page] uses all three markup languages.

[^2]: [It can take up to 10 minutes for changes to your site to publish after you push the changes to GitHub](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll#creating-your-site).

[Jekyll]: https://jekyllrb.com
[Markdown]: https://daringfireball.net/projects/markdown/
[Liquid]: https://github.com/Shopify/liquid/wiki
[Front matter]: https://jekyllrb.com/docs/front-matter/
[Jekyll configuration]: https://jekyllrb.com/docs/configuration/
[source file for this page]: https://github.com/just-the-docs/just-the-docs/blob/main/index.md
[Just the Docs Template]: https://just-the-docs.github.io/just-the-docs-template/
[Just the Docs]: https://just-the-docs.com
[Just the Docs repo]: https://github.com/just-the-docs/just-the-docs
[Pipeline README]: https://github.com/nhmvienna/AmpliPiper/blob/main/README.md
[GitHub Pages]: https://pages.github.com/
[Template README]: https://github.com/just-the-docs/just-the-docs-template/blob/main/README.md
[GitHub Pages / Actions workflow]: https://github.blog/changelog/2022-07-27-github-pages-custom-github-actions-workflows-beta/
[customize]: {% link docs/customization.md %}
[use the template]: https://github.com/just-the-docs/just-the-docs-template/generate
