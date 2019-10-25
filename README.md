# RNA-seq analysis of E. coli with over-expressed DNA-damage handling proteins.

In this project, you will be analysing RNA-seq data of Escherichia coli bacteria.
These bacteria have had some DNA-damage handling proteins over-expressed, and you
would like to perform a transcriptome-wide study of its effects.

You should start by forking this repository. A git fork basically creates a copy
of the repository on your own GitHub account. You can find the fork button on the
top left corner of the repository webpage on GitHub.

Once you fork the project, you will have a copy of the repository on a new URL:

https://github.com/<your_username>/testsim

You should now clone this new repository to obtain a local copy in your machine.

The repository already contains a folder structure to help you organise your files.
It also contains the data files for three different E. coli samples.

Your job is to develop a pipeline to analyse this data by doing some quality checks
on the reads, removing sequencing adapters, aligning the adapter-free reads to the
E. coli genome, and generating a report about the whole process.

When complete, your pipeline should be able to automatically:

- Download the E. coli genome
    - You can get if from ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/005/845/GCF_000005845.2_ASM584v2/GCF_000005845.2_ASM584v2_genomic.fna.gz
- QC the data using the FastQC software (fastqc in conda)
- Remove the adapters from the data (cutadapt in conda)
- Index the genome (star in conda)
- Align the adapter-free reads to the genome (also with star)
- Generate a report with MultiQC (multiqc in conda)

Take into account that you should only repeat for each sample those commands that
analyse samples.

> You can obtain the list of samples from the sample files with this command:
> 
> ```shell
> $(ls data/*.fastq.gz | cut -d "_" -f1 | sed 's:data/::' | sort | uniq)
> # Bonus brownie points if you replace the "sed" with something else.
> ```

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

> Remember to commit often. Don't go crazy about it, but do generate a history of your work.
