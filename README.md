## 🎬 EboGen
A comprehensive pipeline for the genomic analysis of Ebola virus, the causative agent of Ebola virus disease

## 🏆 About
EboGen is a modular and automated pipeline designed to simplify and standardize the genomic analysis of Ebola Virus. It integrates quality control, variant calling, consensus genome generation, clade typing, and phylogenetic analysis into a streamlined workflow.

![workflow](EBoGen.png)

## 🏷️ Key Features:

1. Quality Control: Automatically cleans and filters raw sequencing reads to ensure data accuracy.
2. Variant Calling: Accurately identifies SNPs and indels using GATK, providing enhanced genomic insights.
3. Consensus Genome Generation: Produces high-quality, reference-based genome assemblies for downstream analysis.
4. Phylogenetic Analysis: Generates robust phylogenetic trees using maximum likelihood and neighbor-joining methods.

## ⚙️  Installation

Make sure you have [Miniconda](https://conda.io/miniconda.html) or [Anaconda](https://docs.anaconda.com/free/anaconda/install/linux/) on your Linux system using the links provided
Clone the software from the offical repository using: 


`conda activate base`

`cd && git clone https://github.com/MicroBioGenoHub/EboGen.git`

`cd EboGen`

`conda env create -n EboGen --file EboGen_installer.yml`

`bash setup.sh`

Run the program to make sure you have access to all the plug-ins using the command `EboGen -h` to view output below:

```bash

This is EboGen $version
Developed and maintained by Stephen Kanyerezi, Ivan Sserwadda, & Gerald Mboowa

Synopsis:
        EboGen is a modular and automated pipeline designed to simplify and standardize the genomic analysis of Ebola Virus. It integrates quality control, variant calling, consensus genome generation, and phylogenetic analysis into a streamlined workflow.

Usage: 
        Given paired reads, to perform variant calling and generate a consensus genome; EboGen [options] -R1 <path of forward read> -R2 <path of reverse read> -o <output directory to be created> --varcall true
        Given a multifasta file, to perform phylogeny; EboGen [options] --multifasta <path of multifasta file> --phylogeny true -o <output directory to be created> 

General:
        -h/--help       Show this help menu
        -v/--version    Print version and exit
        -x/--citation   Show citation and exit

Mandatory options for paired reads:
        -R1/--forward-read       Path of the forward reads [either .fastq or .fastq.gz]

        -R2/--reverse-read       Path of the reverse reads [either .fastq or .fastq.gz]

        --multifasta             Path of mulitfasta file. Applicable if you want to perform phylogenetics

        -o/--output-dir         Directory to be created for results


        --varcall               [true or false (default)] Genrate variants and consensus genome only.

        --phylogeny             [true or false (default)] construct a phylogenetic tree. Applicable only with --consensus option and if --varcall and --typing not set to true

Other options:

        --cores                 Number of cpus to use. Default=16
                     
For further explanation please visit: https://github.com/MicroBioGenoHub/VaricellaGen

```

## How ro Run

If you want to perform variant calling and consensus genome generation only, run the command below

```
EboGen -o <output_dir> -R1 <forward read path> -R2 <reverse read path> --varcall true
```

If you have a multi fasta file and you want to perform phylogenetics, run the command below

```
EboGen -o <output_dir> --multifasta <path to multi fasta file> --phylogeny true
```

## Output Files

Here we describe the output files generated from the analysis pipeline. The outputs are organized into different directories based on their function.

### Directory Structure

| Directory      | File(s)               | Description |
|--------------|----------------------|-------------|
| **alignment/**  | BAM File | Contains the aligned sequencing reads, used for downstream variant calling and consensus genome generation. |
| **consensus/**  | Consensus FASTA File | Contains the final consensus genome sequence. |
|              | Metrics File | Reports genome coverage and N-content statistics. |
| **qc/**  | HTML Files | Contain quality control (QC) reports. |
|              | trimmed_fastq/ | A subdirectory containing trimmed FASTQ files after quality filtering and adapter removal. |
| **variants/**  | GVCF File | Stores variant calls in genomic variant call format (gVCF). |
|              | Decomposed VCF File | A normalized version of the variant call file. |
|              | Fixed & Ambiguous VCF Files | Processed VCF files having fixed and ambiguous variants. |
|              | mask.txt | A text file listing masked regions in the consensus genome. |
| **phylogeny/**  | msa | A subdirectory containing an MSA file |
|                 | tree | A subdirectory containing the nexus tree |

