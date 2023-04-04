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

{: .important}
As a prerequisite, the passwordless SSH has to be configured beforehand, refer to the section *Passwordless SSH* under *Digital Alliance of Canada*.

##### JupyterLab
1. Install [`kslurm`](https://github.com/pvandyken/kslurm) if not previously done.
2. In a terminal, ssh to Graham. 
    1. Create a virtual environment using `kpy create <name>` (from [`kslurm`](https://github.com/pvandyken/kslurm) tool). 
    2. Load the venv and install `jupyterlab` plus any other packages you need.
    3. Save the env (`kpy save <name of your venv>`) and deactivate the venv (`deactivate`). 
    4. Run `kjupyter` with any required specifications and using the created venv (refer to the instructions [here](https://github.com/pvandyken/kslurm)).
    5. Copy the SSH tunneling command shown in the terminal after the previous step was completed successfully. **DO NOT** close this terminal.
3. In a new terminal (without ssh to Graham), execute the previously copied SSH tunneling command.
4. Copy the localhost URL shown in the terminal after running `kjupyter` in step 2.d and paste it in your local computer browser.

You should now be able to run Jupyter Notebooks using the JupyterLab session opened in your browser. 
>
You will only be able to access files from folder where you executed the `kjupyter` command. Therefore, if you where located in `/home/<user>/scratch` when running this command in Graham, you will only be able to access files and folders located inside `scratch`. If you want to access all of your files, make sure to be in your home folder before running the command. 
{: .note}

##### VS Code
To be able to run Jupyter Notebooks in Visual Studio Code from your local machine, using a file and kernel from Graham, refer to the following instructions:
1. Open your local VS Code and install the `Remote - SSH` extension.
2. Hit `Ctrl+Shift+p` and type `Remote-SSH: Open SSH configuration file...`. Select the file in your home directory and set it to:
    ```
    Host graham.sharcnet.ca
        HostName graham.computecanada.ca
        User <username>
        IdentityFile ~/.ssh/<file>
    ```
    Replace `<username>` with your corresponding Graham username and `<file>` with the file generated when setting the passwordless SSH connection.
3. Before connecting to the server, go to the settings of the Remote-SSH extension and set the Connect Timeout value to a higher value than the default, for example, 10000 (since Graham usually responds slowly).
4. Use `Ctrl+Shift+p` again, type `Remote-SSH: Connect to Host...` and use the previous config file. This will enable the SSH connection between VS Code and Graham. You should now be able to see your Graham folders in VS Code.
5. In a terminal, ssh to Graham. 
    1. Create a virtual environment using `kpy create <name>` (from [`kslurm`](https://github.com/pvandyken/kslurm) tool). 
    2. Load the venv and install `jupyterlab` plus any other packages you need.
    3. Save the env (`kpy save <name of your venv>`) and deactivate the venv (`deactivate`). 
    4. Run `kjupyter` with any required specifications and using the created venv (refer to the instructions [here](https://github.com/pvandyken/kslurm)).
6. Return to the VS Code window from step 5 and open the Jupyter file that you want to run.
7. Use `Ctrl+Shift+p` and type `Jupyter: Specify Jupyter Server for Connections`. Paste the URL given by kjupyter for the server connection.

>
- If kjupyter command doesn't work after step 6, try installing `jupyterlab` in your local Python in Graham (without any venv activated, run `pip install jupyterlab`).
- Running Jupyter Notebooks through SSH Tunneling is usually faster. 
{: .note}

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