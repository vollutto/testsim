# RNA-seq analysis of E. coli with over-expressed DNA-damage handling proteins.

## Introduction

In this project, you will be analysing RNA-seq data from Escherichia coli bacteria.
These bacteria have had some DNA-damage handling proteins over-expressed, and you
would like to perform a transcriptome-wide study of its effects.

## Setting up your environment

### Conda

You should create a new, empty conda repository. Make sure you have set up 
Bioconda to be able to install the necessary packages. [See this link for details
on setting up conda and bioconda](http://bioconda.github.io/user/install.html).

### Git repository

Your working directory will be under git control. You will first copy this repository
to your GitHub account, and then work on this new copy using it as your remote.

#### Forking this repository

You should start by forking this repository. A git **fork** creates a copy
of the repository *on your own GitHub account*. This copy will become the remote
repository where you will eventually save your work.

You can find the fork button on the top right corner of the repository webpage on GitHub.

Once you fork the project, you will have a copy of the repository on a new URL:

`https://github.com/<your_username>/testsim`

#### Adding your instructor as a collaborator

You should now add your instructor as a collaborator in your copy of the repository,
so that she/he can interact with you during the development.

#### Getting help

You can now ask for help from your instructor by creating a new issue in the GitHub
repository (click on the "Issues" tab on the top left of the GitHub repo page),
adding a relevant title and description, **and assigning the issue to your instructor**.

You can assign the issue by clicking on the "Assignees" title on the top right.

> Make sure to check that your instructor appears on the list of possible assignees.

#### Cloning your fork and starting work

You should now **clone** this new repository to obtain a local copy in your machine.

You can then start working on your local copy of the repository.

> Remember to commit often. Don't go crazy about it, but do generate a history of your work.

### Organisation of your files

The repository already contains a folder structure to help you organise your files.
It also contains the data files for three different E. coli samples, and the pipeline
script you wrote in class that runs cutadapt, the star indexing, and the star alignment.

> You may need to create extra directories to store some files.

## Your tasks

Your job is to develop a pipeline to analyse this data by doing some quality checks
on the reads, removing sequencing adapters, aligning the adapter-free reads to the
E. coli genome, and generating a report about the whole process.

When complete, your pipeline should be able to automatically do the following (list not necessarily in order):

- Download the E. coli genome
    - You can get if from
    `ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/005/845/GCF_000005845.2_ASM584v2/GCF_000005845.2_ASM584v2_genomic.fna.gz`
- QC the data using the FastQC software (fastqc in conda)
- Remove the adapters from the data (cutadapt in conda)
- Index the genome (star in conda)
- Align the adapter-free reads to the genome (also with star)
- Generate a report with MultiQC (multiqc in conda)

> Keep in mind that you should only repeat for each sample those commands that
> analyse samples. There are other, generic commands that should only be run once.

> **This may require modifying the provided script to analyse samples.**

## Once you are done

Once you are done, you should first export a file with your conda environment information.

```shell
mkdir envs
conda env export > envs/rna-seq.yaml
```

You should **add** the new files to the staging area, **commit** them to the local repository,
and **push** your changes to the remote repository.

## Hints

### Getting the list of samples

You can obtain the list of samples from the sample files with this command:

```shell
ls data/*.fastq.gz | cut -d "_" -f1 | sed 's:data/::' | sort | uniq
# Bonus brownie points if you replace the "sed" with something else.
```

### Organising your scripts

You can structure your program as you like. Here's an example for a parent
script that will call a sample-analysing script for each sample:

```shell
# place here any commands that need to be run before analysing the samples
for sid in $(<list of samples>)
do
   # place here the script with commands to analyse each sample
   # this command should receive the sample ID as the only argument
done
# place here any commands that need to run after analysing the samples
```
