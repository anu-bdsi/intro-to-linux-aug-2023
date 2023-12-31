# Setting Up for The Variant Calling Workflow    

1. Install Anaconda
2. Create an conda environment
3. Install packages using conda 
4. Download data 
5. Install IGV 

## About Anaconda 

Anaconda is an open-source package management system and environment management system commonly used in data science, scientific computing, and machine learning projects. It allows you to install, update, and manage software packages and dependencies for your projects. It supports packages written in various programming languages, with a focus on Python packages. 

## Install Anaconda on MacOS 

__If you have an ANU managed MacOS:__ 

You can download Anaconda from the university software manager. 

__If you have a personal MacOS:__ 

Go to this [website](https://www.anaconda.com/download#downloads) and pick the suitable installer for your device, please choose the graphical installer. 

Instuctions when installing:

1. Introduction - `Continue`
2. Read Me - `Continue`
3. Licence - `Continue` then `Agree`
4. Destination Select - `Install for me only`
5. Installation Type - `Install` then an Anaconda window will pop up
6. Code in the Cloud - `Continue` 
7. Summary - `Close`

After installation, open a new terminal and run the following code to check if Anaconda has been successfully installed. 

```sh
conda --version 
```

You should see the version number printed on your screen. 

## Install Anaconda on WSL 

First, let's start a Ubuntu terminal. 

Then, run the following codes in your terminal:

```sh
# change directory to home 
cd ~

# wget is a command to download files from the internet
curl -O https://repo.anaconda.com/archive/Anaconda3-2023.03-1-Linux-x86_64.sh 

# run the installer to install 
bash Anaconda3-2023.03-1-Linux-x86_64.sh 
```

You will be prompted with some questions in the installation process, just press `enter` or type `yes` then `enter` to continue. When you see `--MORE--` at the bottom of the terminal, press `space` key to move to the next page of the document. When you are asked to decide the installation location, just press `enter` to use the default path. 

After you finish the installation, use `exit` command to exit the terminal and restart a new one.

In the new terminal, run the following command to check if Conda has been successfully installed:

```sh
conda --version
```

You should see `conda 23.3.1` printed on screen. 

## About conda environments 

A conda environment is a self-contained directory that contains a specific collection of software packages, along with the necessary dependencies and their respective versions. 

Using conda environments can avoid conflicts between projects or applications that may require different versions of libraries or dependencies. This isolation ensures that your projects have a consistent and reproducible environment, making it easier to share and collaborate with others. 

In this short course, we will do a small project where we find the variants of some DNA sequencing data of E.coli. This bioinformatic process is called variant calling. So, we can create a new conda environment called `ecoli-vc`, and install the needed packages in this environment. 

## Create an conda environment (both MacOS and WSL)

```sh
conda create --name ecoli-vc
```

You will be prompted with a question asking if you want to proceed, type `y` and `enter` to continue. 

After creating the environment, the next step is to activate the environment. If we don't activate the environment, we can't use the software we installed in it nor to install something into the environment. 

```sh
conda activate ecoli-vc
```

__For MacOS with Apple M1/M2 chips, there is one additional step:__

```sh
conda config --env --set subdir osx-64
```

## Install packages using conda (both MacOS and WSL) 

After activating the environment, we can start to install packages. There are 5 packages we are going to use for this workflow, they are FastQC, Trimmomatic, BWA, Samtools, and Bcftools. 

The code to install all five packages, please run them line by line: 

```sh
conda install -c bioconda fastqc
conda install -c bioconda trimmomatic
conda install -c bioconda bwa
conda install -c bioconda samtools=1.9
conda install -c bioconda bcftools=1.9
```

You will be prompted with question asking if you want to proceed, type `y` and press `enter` to continue. 

After the process finished, run the following commands to verify if the packages have been successfully installed. 

```sh
fastqc --version
trimmomatic -version
bwa # prompt with some commands 
samtools --version
bcftools --version
```

## Downloading Data (both MacOS and WSL)

The data we are going to work with in this workshop is DNA sequencing data from E.coli, it is part of a long-term evolution experiment led by [Richard Lenski](https://en.wikipedia.org/wiki/E._coli_long-term_evolution_experiment). We will talk more background about the data later in the class. 

In your terminal, run the following codes to download the needed files:

```sh
# create a new directory where we store the files 
mkdir -p ~/workshops/variant-calling/raw-fastq/

# go into the directory we just created 
cd ~/workshops/variant-calling/raw-fastq/

# curl is a command to download files from the internet 
curl -O ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR258/004/SRR2589044/SRR2589044_1.fastq.gz
curl -O ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR258/004/SRR2589044/SRR2589044_2.fastq.gz
curl -O ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR258/003/SRR2584863/SRR2584863_1.fastq.gz
curl -O ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR258/003/SRR2584863/SRR2584863_2.fastq.gz
curl -O ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR258/006/SRR2584866/SRR2584866_1.fastq.gz
curl -O ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR258/006/SRR2584866/SRR2584866_2.fastq.gz
```

It takes approximately 15 minutes to finish downloading. 

## Install IGV (both MacOS and WSL)

Integrative Genomics Viewer (IGV) is a powerful and widely used visualisation tool for exploring and analysing genomic data, it allows researchers to interactively visualise and analyse various types of genomic data, including DNA sequencing data, gene expression data, epigenetic data, and more. 

We are going to use IGV to look at the results we get from variant calling. 

Go to this [page](https://software.broadinstitute.org/software/igv/download) and pick the right one to download for your device. Choose the one with Java included. Windows users to download the Windows version not the Linux version. 