---
layout: default
title: Welcome to DiD
nav_order: 1
description: "Welcome to the DiD repository"
image: "/assets/images/DiD.jpg"
permalink: /
---

<img src="./assets/images/DiD_banner.jpg">

# Welcome!

This repository tracks the recent developments in the **Difference-in-Difference (DiD)** literature. It serves two purposes. First, it is an organized dump of my bookmarks from Twitter, GitHub, YouTube etc. The aim here is to keep track of the DiD updates. The second is to make sense of the different packages from an end-user perspective. This part has to do with how to apply these methods in our research work. On the theory side, several really useful notes already exist (see the [Resources](https://asjadnaqvi.github.io/DiD/docs/resources) section).

I will keep adding content to this website. It might contain errors or the language might not be precise enough. This probably reflects my own poor understanding of what is going on. So please give feedback! The aim of this repository is to collectively build up notes and a code base that we can all use.

Some thoughts below from my own perspective (these are also subject to change over time):


## What happened? The DiD renaissance

Several DiD innovations came out simultaneously in 2020 and 2021 resulting in collective confusion online. At the core of this new-DiD literature is the premise that the classic Twoway Fixed Effects (TWFE) model gives wrong estimates of treatment effects. This is especially true if the treatments are heterogeneous (differential treatment timings, different treatment sizes, different treatment status over time) which can result in "negative weights" that dilute the true treatment effects. The negative weights can be derived by comparing combinations of late-treated with early-treated, and treated versus not-treated groups (Bacon decomposition). There is also broad agreement that these biases still persist *even if* treatments are not staggered. 

Starting from TWFE-bashing, the different DiD packages uses different methodological innovations to "correct" for TWFE biases. Within these packages are different ways of handing different DiD aspects like parallel trends, negative weights, and covariates. As a result, various methods have been utilized in different packages ranging from bootstrapping, inverse probability weights, matching, influence functions, and imputations. 

Here also lies my own confusion in terms of which package to use for which problem. Based on online conversations, it seems like it all boils down the research question what really we are trying to estimate. This sort of makes the package choice for analysis a bit subjective. Hopefully, more will be written on comparing the utility of each package by the experts out there. But at the time of writing this, more innovations are expected to come out in the coming months.


## Why should we invest in DiD?

Because not everything can be evaluated using an RCT. Even though RCTS are methodologically very clean, they have high time and money costs. Plus they require some level of social and political capital to execute, especially in a developing-country setting. In contrast, applications of quasi-experimental methods like IVs and RDDs are hard to find. This makes DiDs, in terms of applicability, a very power methodology. If one has access to detailed primary or secondary micro data, it is also relatively easy to find interventions with differential timings (that is basically all policy implementations). Therefore, going from data to results is fairly fast (as compared to RCTs) and the straggered treatment graphs are just visually very easy to interpret. Furthemore, my hunch is that the methodological issues identified with TWFEs, that led to new DiD papers, will also spillover into IV and RDD papers in the coming years. So investing in the DiD literature now will provide a strong foundation for keeping track of the the upcoming methodological innovations.


## Misc info

This is a working document. If you want to report errors or contribute, just [open an issue](https://github.com/AsjadNaqvi/DiD/issues), or [start a discussion](https://github.com/asjadnaqvi/DiD/discussions), or e-mail at asjadnaqvi@gmail.com. Since paths and links are also subject to change, please report them to keep this repository as up-to-date as possible. I might add a discussion section below posts to allow for direct comments.

I will slowly build up this website with some Stata code. This is to help me (and you) navigate the literature and figure out the code structure for different packages.



