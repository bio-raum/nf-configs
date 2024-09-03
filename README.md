# nf-configs

Welcome to the bio-raaum central config repository. We are developing and curating workflows for various applications in food safety monitoring, including taxonomic profiling of food stuff as well as assembly, annotation and profiling of bacterial isolates. And possibly more to come over the next months.

All pipelines are developed in [Nextflow](https://nextflow.io/), using a common [template](https://github.com/marchoeppner/nf-template) with a focus on portability, high standard of implementation, ease of use and version control. Some of us have previously developed within the [nf-core](https://github.com/nf-core) project and most of the coding framework used here is based on conventions originally developed by nf-core for the Nextflow community. As such, nf-core developers will find it immediately familiar and users will appreciate the overall robustness.

We provide a detailed documentation with each pipeline (see below) as well as a general [setup guide](doc/installation.md) to prepare your system for running them. We have also collected [answers](doc/faq.md) to some common questions

**Finally, here are [instructions](doc/config.md) on how to actually set up your config file and contribute it.**

The config files hosted here can be jointly used across the following pipelines:

## GABI 

[GABI](https://github.com/bio-raum/gabi), short for '**g**enomic **a**nalysis of **b**acterial **i**solates' is a workflow for the assembly of bacterial genomes from quality-controlled read data and downstream characterization (annotation, MLST typing, etc). GABI supports short reads, Nanopore long reads as well as Pacbio HiFi reads. 

## FooDMe2

[FooDMe2](https://github.com/bio-raum/FooDMe2) performs taxonomic profiling of mitochondrial amplicon data to detect and quantify eukaryote species from mixed samples. The main application is in detecting food fraud, such as mis-labelled ingredients or use of endangered animals in (processed) foods. 


