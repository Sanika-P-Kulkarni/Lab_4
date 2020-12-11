# This is the `master` branch -- the code that runs your site is in the `gh-pages` branch!

This repository was originally forked from the **[Beautiful Jekyll](https://github.com/daattali/beautiful-jekyll)** theme, by Dean Attali.  The README for the Beautiful Jekyll theme follows below:

***

# Beautiful Jekyll

[![Donate](https://img.shields.io/badge/Donate-PayPal-green.svg)](https://www.paypal.me/daattali/20)
[![Gem Version](https://badge.fury.io/rb/beautiful-jekyll-theme.svg)](https://badge.fury.io/rb/beautiful-jekyll-theme)

> *Copyright 2018 [Dean Attali](https://deanattali.com)*

**Beautiful Jekyll** is a ready-to-use template to help you create an awesome website quickly. Perfect for personal sites, blogs, or simple project websites.  [Check out a demo](https://deanattali.com/beautiful-jekyll) of what you'll get after just two minutes.  You can also look at [Dean's personal website](https://deanattali.com) to see it in use, or see examples of websites other people created using this theme [here](#showcased-users-success-stories).

**If you enjoy this theme, please consider [supporting Dean](https://www.paypal.me/daattali/20) for developing and maintaining this template.**

<p align="center">
  <a href="https://www.paypal.me/daattali">
    <img src="https://www.paypalobjects.com/en_US/i/btn/btn_donate_LG.gif" />
  </a>
</p>

### Contents

- [Prerequisites](#prerequisites)
- [What we thought we were doing versus what we are](#what-we-thought-we-were-doing-versus-what-we-are)
- [Installing Packages](#installing-packages)
- [Running FastaQC](#running-fastqc)
- [Running MultiQC](#running-multiqc)
- [Running Trimmomatic](#running-trimmomatic)
- [Running Velvet](#running velvet)
- [Running Diversity Analyses](#running-diversity-analyses)

## Prerequisites

- You should have access to a high-performance computing cluster or a Unix terminal. If you have a Windows computer, you will need to translate all these commands into something else entirely. Use Google to translate. Sorry. Also, install miniconda.

## What we thought we were doing versus what we are

So  we thought we were running some analyses on these T-cell sequences to support a project related to predicting sepsis in children. We are actually examining diversity of T-cell receptors in samples before and after virus-targeted immunotherapy. Unfortunately, we will not be able to disclose our data.

### 1. Installing Packages

First, give these commands in your terminal:

$ conda install -c bioconda fastaqc
$ conda install -c bioconda multiqc
$ conda install -c bioconda trimmomatic
$ conda install -c bioconda velvet

### 2. Running FastaQC

Iterate through all the sequences running the command below:

$ fastqc nameOfFile.fastq

This will create an HTML report of read quality and a zipped folder of a machine-readable version of the report.

### 3. Running MultiQC

Collect all of the reports and folders of all your sequences in a single folder. Run the following command, to generate a single summary of all the reports for all the sequences:

$ multiqc .

## 4. Running Trimmomatic

You'll find that the reads from this restricted dataset are in tip-top condition. Just trim 'em a bit here and there to make them perfect for contig assembly:

$ trimmomatic PE -threads 4 -phred33 file_R1.fastq file_R2.fastq\
              file_R1.trimmed.fastq file_R1un.trimmed.fastq\
              file_R2.trimmed.fastq file_R2un.trimmed.fastq\
              ILLUMINACLIP:TruSeq3-PE.fa:2:30:10  SLIDINGWINDOW:4:20
              
Run through this for all your paired end sequences.

## Note! If you find a way to create a loop for this, contact me immediately!

## 5. Running Velvet

Collect all your trimmed reads into a folder. Still trying to figure this one out. This must correct?

$ velveth indices 61 \ -short -separate -fastq \ file_R1.trimmed.fastq \  file_R2.trimmed.fastq

## Running Diversity Analyses

Hasn't happened yet. Stay tuned!
