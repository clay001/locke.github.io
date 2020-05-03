---
layout: post
title: "Current research(3)"
date: 2019-11-09 15:42:22
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

## goals

This project will provide/develop two numerical methods to make use of RNA velocity 

1. Quasi potential from Freidline-Wentzell theory using ordered line method -- to estimate attractor cell states and compute transition pathways 

2. Fokker Planck equation in reduced space -- to model the dynamics and do virtual gene down- / up-regulation

## Store the after analysis object

into my_velocyto_analysis (main file for the following work)

the T-SNE coordinates in TSNE_replot

trying to embed in diffusion component through Scanpy or Pydiff ---> failed

## OLIM for quasi-potential

the chfiled parameter is select inbuilt examples, but we will have no exact solution.

## Generalizing RNA velocity to transient cell statesthrough dynamical modeling

## things to do

scanpy的基本使用，使用adata的数据结构，包括pl，pp，tl，tl里面有一个了leiden的算法，是louvain的改进版，Landscent是一个R包，方向的预测任务有点像运动员往哪儿跑的计算机视觉任务

t-SNE Markov-chain-based method (correlation kernel)

scScope文章中比较了scVI，scScope，PCA，auto-encoder，DCA做了比较

RNA-velo以小时为尺度，可以协助分析和揭示人类细胞的谱系发育和细胞内的动态变化。输入read count matrix，cell-type lineage，cluster coordinate，经过不同的模型假设，有一种是让剪接率固定

attention可以做seq到seq 的不完全信息决策，由其演变而来的transformer在ELMO，BERT，GPT里都有应用

CTP-net

预测表达量，单细胞转录数据，膜蛋白质数据

DREAM2017 joint learning

CITE，REAP seq

indrops方法测序

