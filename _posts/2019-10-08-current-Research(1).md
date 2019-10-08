---
layout: post
title: "Current research(1)"
date: 2019-10-07 14:22:44
image: '/assets/img/'
description: 'My current research topic record'
tags:
- research 
- PDE 
- RNA velocity 
categories:
- research 
twitter_text: 'New research progress of Locke!'
---

## Preface 
While waiting for transfering blog articles from other platform, I think create more is more important. \\
Currently I devote myself to research, and hope to have a publication at the end of this year. So I start to write this series of blogs, aim to record and clear up my thoughts, also can be seen as my psychological journel, the article's birth witness and evidence.\\
Finally, hope it can provide some inspiration to readers.
## First paper in RNA velocity
We all know RNA-seq, but this approach captures only a static snapshot at a point in time. When we want to analyze time-resolved phenomena such as embryogenesis or tissue regeneration, we need something more.  \\
RNA abundance is a powerful indicator of the state of individual cells. This paper use this indicator to define a new feature called RNA velocity—the time derivative of the gene expression state.
This feature can be directly estimated by distinguishing between unspliced and spliced mRNAs in common single-cell RNA sequencing protocols. \\
Here I captured some important points and listed together:
- RNA velocity is a high-dimensional vector that predicts the future state of individual cells on a timescale of hours. 
- This paper validate its accuracy in the neural crest lineage, demonstrate its use on multiple published datasets and technical platforms, reveal the branching lineage tree of the developing mouse hippocampus, and examine the kinetics of transcription in human embryonic brain.
- We expect RNA velocity to greatly aid the analysis of developmental lineages and cellular dynamics, particularly in humans.

There is many theoritical and analysis detail in that origin paper, but maybe we don't need to really go into the detail of it. RNA velocity basically is to reuse the information from reads to expression, in its demo they use DentateGyrus.loom.
{% highlight ruby %}
Loom is an efficient file format for large omics datasets. Loom files contain a main matrix, optional additional layers, a variable number of row and column annotations, and sparse graph objects. Under the hood, Loom files are HDF5 and can be opened from many programming languages, including Python, R, C, C++, Java, MATLAB, Mathematica, and Julia
{% endhighlight %}
HDF5 is a file format and h5py is a package to process it in python, for more you can see this blog: [blog link](https://www.jianshu.com/p/de9f33cdfba0).

In another paper's souce code I can tell that the original data need go through cellranger pipeline to give this velocity code needed loom format.\\
So what is cellranger? [Cellranger](https://support.10xgenomics.com/single-cell-gene-expression/software/pipelines/latest/what-is-cell-ranger) is a 10X genomic's software, 


