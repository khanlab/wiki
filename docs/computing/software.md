---
layout: default
title: Software
parent: Computing
nav_order: 3
permalink: /computing/software
---

## Software
{: .no_toc}
We use a variety of software tools in the lab. This page will describe some 
commonly used tools with information about setting them up.

## Table of Contents
{: .no_toc}
- TOC 
{:toc}

## Git + GitHub
[GitHub] is a hosting service that makes use of Git (a distributed version
control system) and is used to store code (and potentially documentation).
Here is some documentation to help you 
[get familiar](https://swcarpentry.github.io/git-novice).

{: .important} 
Both are **required** tools in the lab. Be sure to create a GitHub account and 
inform Dr. Khan of your username to be added to the lab organization.

Another recommendation to get familiar is to create your user profile on the 
lab website (if you haven't already) and creating a pull request.

## Python
Python is one of the most popular programming languages and can be used to
build software, automate tasks, and conduct data analysis. Python is available
on both CBS and Graham. You will see that many of the tools that we use, make 
use of Python in the backend. 

Here are some resources for learning Python:
* [Python Novice Inflammation]
* [Python Intermediate Gapminder]

Another useful concept to learn are virtual environments. These are isolated
Python environments that help avoid dependency incompatabilities across 
projects. More details can be found 
[here](https://realpython.com/python-virtual-environments-a-primer/).

## Jupyter
Jupyter is a web-based application that can provide an interactive notebook, 
useful for performing analysis. These notebooks allow code in different 
programming languages to be run. Assuming this is set up in a virtual 
environment, all installed packages in the environment are made available 
through this application, and simple tasks such as statistical analysis or 
plotting of data can performed. See more information on the [Jupyter website].

### Installing JupyterLab 
The following provides instructions on setting up JupyterLab in a virtual 
environment:

1. Install Jupyter & JupyterLab to your virtual environment
```bash
source <path_to_virtualenv>/bin/activate
pip install jupyter jupyterlab
```

#### Local
If this environment is installed locally, a Jupyter session can be 
started by running the following:
```bash
jupyter lab
```

#### Graham
If on Graham, you can submit a job for a Jupyter session. Before submitting
please ensure your virtual environment is activated.

{: .warning}
Calling an interactive Jupyter session is slightly different depending on
helper script used (e.g. neuroglia-helpers vs kslurm). Refer to their 
documentations for the appropriate commands.

## Snakemake
[Snakemake] is a workflow management system that enables the ability to create
reproducible and scalable data analyses. These workflows are described in a 
human readable way and is based in Python. Pros of using a workflow management
tool, like Snakemake, include the ease of changing parameters and 
simplifying the management of complex workflows.

Here is a [video](https://www.youtube.com/watch?v=hPrXcUUp70Y&amp;feature=youtu.be)
on Snakemake, as well as neuroimaging-related Snakemake 
[tutorial](https://snakemake-neuroimaging-intro.netlify.app/).

You can also checkout the `#snakemake` channel on Slack!

## Datalad
[Datalad] is a tool for downloading, working with, and searching through online
datasets. For a list of available datasets, see 
[here](https://datasets.datalad.org).

Datalad datasets are git repositories that you can download, where the large
files are symlink placeholders until you use the `datalad get` command on them 
to download the full file.


[GitHub]: https://www.github.com
[Python Novice Inflammation]: https://swcarpentry.github.io/python-novice-inflammation/
[Python Intermediate Gapminder]: http://swcarpentry.github.io/python-novice-gapminder/
[Jupyter Website]: https://jupyter.org/
[Snakemake]: https://snakemake.readthedocs.io/en/stable/
[Datalad]: http://datalad.org