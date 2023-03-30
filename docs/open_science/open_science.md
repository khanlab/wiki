---
layout: default
title: Open Science
nav_order: 5
description: "Open-science practices of the Khan Lab"
has_children: false
permalink: /open-science
---

## Open Science

Here at the Khan Lab, we encourage and support open-science practices.

## Data
We strive to release the raw, de-identified data for any study where we are 
collecting data, or any derived data that we have generated. The [BIDS] (Brain
Imaging Data Standard) is an open standard for describing neuroimaging data. We
have tools that help to automatically convert acquired data in to this standard
(tar2bids, autobids)

## Reproducible Methods
To support reproducibility, we strongly encourage the containerization of 
workflows so that processing can be reproduced on any system, regardless of 
software / hardware dependencies. Singularity is a container software designed
for scientific computing and used for:
1. Ensuring the same software setup can be used on different machines
1. Deploying and sharing applications (BIDS Apps) for standardized image
processing

We also encourage the use of Snakemake for end-to-end workflow management. This
is a tool for scripting your entire workflow, from raw data to figures in your
papers. Snakemake allows you to easily scale up your analysis from a single 
subjec to an entire dataset.

## Publications
We generally publish pre-prints of all new manuscripts on [biorxiv] - this is
done at the same time as submission to a journal.

## Registered Reports
These are documents, written, and registered (not visible to the public until
released) either before you collect data or carry out analyses, which will 
describe the analyses that you will do. This is to ensure that one does not
hypothesize about the data after the results are known (HARKing), and more 
clearly delineates hypotheses from post-hoc tests. While this has not yet become 
common practice in our lab, we are moving towards this!


[BIDS]: https://bids.neuroimaging.io
[biorxiv]: https://www.biorxiv.org/
