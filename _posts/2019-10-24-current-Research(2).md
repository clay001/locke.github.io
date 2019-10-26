---
layout: post
title: "Current research(2)"
date: 2019-10-24 23:42:22
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

##  Mouse hippocampus

It is related with brain memory. 

The embedding was computed using pagoda2, the distance is determined as $1-r_{ij}$ (r is pearson linear correlation of cell i,j on the first 100 principle compoinents of the top 3000 variable genes). Cluster was performed using Louvain community detection algorithm on the nearest neighbor cell graph.

Explore with code: 

if %matplotlib inline turns error, you should put in front of the matplotlib import command, because some default setting things in jupyter notebook.

![procedure](https://github.com/clay001/blog/blob/gh-pages/_posts/posts_picture/Research(2)/procedure.png?raw=true)

There is two steps which I think is the most important, one is SVR, another is KNN. 

After KNN, we will get:

- knn contiguity matrix
- the weights used for the smoothing
- smoothed spliced
- smoothed unspliced

Then use Sx and Ux to fit gamma to get the kinetic equations, plot the predict result for checking. Calculate the transition probability (here I fixed a bug about the stacking), project the direction (figure with small arrows) and use regular grid and gaussian kernel to smooth (figure with big arrows). We can access these two things in **delta_embedding** and **flow** attribute.

![small_arrow](https://github.com/clay001/blog/blob/gh-pages/_posts/posts_picture/Research(2)/small_arrow.png?raw=true)

![big_arrow](https://github.com/clay001/blog/blob/gh-pages/_posts/posts_picture/Research(2)/big_arrow.png?raw=true)

 Then is some different plot styles and some particular regions zoom in module.(To be continued.... )