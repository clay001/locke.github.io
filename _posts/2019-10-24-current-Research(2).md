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

The embedding was computed on the correlation similarity matrix using [pagoda2](https://www.jianshu.com/p/f4d79b91d448) (pathway and gene set overdispersion analysis), which classifies cells based on known important signaling pathways to improve statistical effectiveness. The distance is determined as $1-r_{ij}$ (r is pearson linear correlation of cell i,j on the first 100 principle compoinents of the top 3000 variable genes). Cluster was performed using Louvain community detection algorithm on the nearest neighbor cell graph.(k = 30)

Explore with code: 

if %matplotlib inline turns error, you should put in front of the matplotlib import command, because some default setting things in jupyter notebook.

![procedure](https://github.com/clay001/blog/blob/gh-pages/_posts/posts_picture/Research(2)/procedure.png?raw=true)

There is two steps which I think is the most important, one is SVR, another is KNN. 

After KNN, we will get:

- knn contiguity matrix
- the weights used for the smoothing
- smoothed spliced
- smoothed unspliced

Then use Sx and Ux to fit gamma to get the kinetic equations, plot the predict result for checking. Calculate the transition probability (here I fixed a bug about the stacking), project the direction (figure with small arrows) and use regular grid and gaussian kernel to smooth (figure with big arrows). We can access these two things in **flow_embedding** and **delta_embedding** attribute. (flow_grid and flow)

![small_arrow](https://github.com/clay001/blog/blob/gh-pages/_posts/posts_picture/Research(2)/small_arrow.png?raw=true)

![big_arrow](https://github.com/clay001/blog/blob/gh-pages/_posts/posts_picture/Research(2)/big_arrow.png?raw=true)

 Then is some different plot styles and some particular regions zoom in module.(To be continued.... )

---------------------------------------------------------------------------------------------

## Fundamental limits paper

A short conclusion of Fundamental limits on dynamic inference from single-cell snapshots:

Due to sequencing method constrains, we can only obtain single cell expression profiling in a snapshot way. However, the information of dynamics is extremely important. There are lots of methods trying to model the change of the continuous cell states, which have a common limit on the uniqueness of the solution. Thus, it needs to be identified some assumptions to constrain. What is more, the sparsity and high dimensionality of single cell data is an obstacle in front of us. This paper applied recent innovations in spectral graph theory to devise a simple and asymptotically exact algorithm for inferring the unique dynamic solution under defined approximations and apply it to data from bone marrow stem cells.

​     The cell state changings are asynchrony in their dynamics. What we want is to infer some rules from the corresponding gene expression space, better if they could be explained in a probabilistic way. They first provide a framework, which is a general, model-independent, mathematical formulation. It states that in each small region of gene expression space, the rate of change in the number of cells equals the net cell flux into and out of the region plus cell accumulation and cell death. This statement introduces some specific hidden assumptions about the nature of cell state space. First it approximates cell state attributes as continuous variables. Second, it assumes that the changes in cell state attributes are continuous in time. 

​     However, it still leaves some ambiguity. First, it assumed that cell entry and exit points will strongly influence inferred dynamics, which means alternative assumptions on cell entry and exit rates across gene expression space count a lot. Second, we didn’t take the stochasticity into account, which means cells in the same molecular can’t follow different paths. Third, rotations and oscillations do not alter cell density, this can be reflected by the invariance of derivate term. Fourth, hidden features of cell state can lead to a superposition of different dynamic processes, which means the chromatin state or tissue location may also contribute to the cell state transitions.

​     Therefore, in order to ensure the uniqueness of the solution, they mainly made two assumptions. They first assumed that the properties of the cell available for measurement fully encode the probability distribution, and the cell trajectories are Markovian based. Then generalize the description back to chemical master equations, combining the deterministic and stochastic component with a diffusion matrix D. Another assumption is that there are no rotational gene expression dynamics, experiments indicate that ignoring cost is relatively small comparing to the simplification of the computation. Due to the unknown of the net change, a description provided by a potential field F is the best way to describe the change term. According to experience, we can’t solve diffusion equations on more than two dimensions. What they do is to draw on a recent theorem by Ting et al. in the spectral graph theory, avoid simplification of data by extending to arbitrarily dimension. With the generated Markov chain, it is possible to calculate the temporal ordering of states by mean first-passage times, and the fate bias by absorbing fate probabilities.

​     Finally, we can see from the result part that there both exists strength and limitation, and the performance on hematopoietic progenitor cells is good. The rigorous basis for dynamic interpretation is quite solid and convincible, which brings me with great inspirations. 

### some interesting tools:

1. [Spring](https://kleintools.hms.harvard.edu/tools/spring.html): KNN layout interface website
2. [Immunological Genome Project](https://www.immgen.org): It is a collaborative scientific research project that is currently building a gene-expression database for all characterized immune cells in the mouse. The overarching goal of the project is to computationally reconstruct the gene regulatory network in immune cells.