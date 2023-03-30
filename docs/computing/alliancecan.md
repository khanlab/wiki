---
layout: default
title: Digital Alliance of Canada
parent: Computing
nav_order: 2
permalink: /computing/alliance-can
---

## Digital Alliance of Canada
{: .no_toc}
We make use of the Digital Alliance of Canada servers (specifically the 
_Graham_ server) for nearly all of our computing and storage needs. This is a 
specialized system with mainly _command-line_ access and submission of jobs for
computing. Through it, we have access to hundreds of CPUs, many GPUs, and 
hundreds of TB of storage. These tools allow you to access servers supported by
the Canadian government for research purposes, which are useful for jobs that 
are very computationally heavy.

{: .important}
You will need to sign up for an account to access this resource - see below
for more information.

## Table of Contents
{: .no_toc}
- TOC 
{:toc}


### Getting an account
Create an account at [CCDB].

Make sure you include your Sponsor, Ali Khan (CCRI: xkc-513-04). Once the 
sponsorship request has been accepted, you will be granted privleges to actually
use SHARCNET.

{: .note}
To log in to the system, use `ssh <user>@graham.computecanada`, replacing 
`<user>` with your SHARCNET user name in the terminal.

### Passwordless SSH
If you are using `sshfs`, you should always have passwordless ssh set-up, 
otherwise you may encounter issues with your IP becoming blacklisted due to too
many failed reconnection attempts.

If you are using the [CBS server](/computing/cbs), there is an automated process to set this up by running `setup_sshfs_alias`. If not, instructions to set this up can be found below (commands should be entered 
into a terminal):
1. Generate a ssh keyfile:
    ```bash
    ssh-keygen -t rsa
    ```

2. Copy this to the remote server
    ```bash
    ssh-copy-id -i ~/.ssh/id_rsa.pub <user>@graham.computecanada.ca
    ```


### Mounting Graham data locally with `sshfs`
#### Mac/Linux
Detailed instructions for mounting can be found 
[here](https://www.sharcnet.ca/help/index.php/SSHFS), however, make sure to use
the options highlighted below:

```bash
mkdir $HOME/graham;
sshfs -o reconnect,ServerAliveInterval=15,ServerAliveCountMax=3,follow_symlinks $USER@gra-dtn1.computecanada.ca:/home/$USER ~/graham;
```

#### Windows
For Windows, you can follow the instructions put together 
[here](https://github.com/greydongilmore/operating_system_installs_mods/blob/master/windows_docs/windows_sshfs.md)

### File transfer with Globus
The recommended way of transferring large amounts of data from your local 
filesystem and Graham is to use Globus. To do so, follow the instructions below:

1. Log on to [Globus]
1. Click "Endpoints" tab and subsequently subtab "administered by me". If no 
personal endpoints, add "Globus Connect Personal endpoint". Set a Display Name
and download the appropriate application for your operating system (note: this
is available through CBS).
1. Once successful, go to the "Transfer Files" tab and set Endpoints depending 
on the direction of transfer.
{: .note}
For transfer to/from Graham, use `computecanada#graham-dtn`

### Setting group read/write permissions
Run these commands the first time you login to a new cluster system to grant
group read/write to project folders (to allow easier debugging):
```bash
chgrp -R ctb-akhanf ~/projects/*/$USER;
chmod -R g+rwXs ~/projects/*/$USER;
```

To grant access to your home directory:
```bash
chgrp -R ctb-akhanf $HOME;
chmod -R g+rwXs $HOME;
```

### Running jobs
#### Neuroglia-helpers (legacy)
The `neuroglia-helpers` scripts provide an easier interface to submit jobs, 
including a BIDS-app job submission script (`bidsBatch`).

To install the `neuroglia-helpers` scripts, see the README 
[here](https://github.com/khanlab/neuroglia-helpers/blob/master/README.md).

#### kslurm
Newer helper and wrappers for running commands on Graham have been developed in
the utility package `kslurm`.

To install `kslurm`, see the README 
[here](https://github.com/pvandyken/kslurm/blob/master/README.md).

### Job-templates
It is importantto understand compute node specs and appropriately allocate
resources using some combination of parameters like `--mem`, `--cpus-per-task`,
`--ntasks`, etc. Node types and characteristics can be found
[here](https://docs.computecanada.ca/wiki/Graham).

The `neuroglia-helpers` and `kslurm` job templates are optimized for the size of
nodes and our allocation on Graham. Some examples are found below:

* Regular: 8cores/32GB/24hr (1/4 of a node)
* Short: 8cores/32GB/3hr (1/32 of a node)
* Fat: 32cores/128GB/24hours (1 node)

### Useful SLURM Commands
Here are some useful commands to help monitor usage on Graham.

* `sq` - See what is in the queue for your user (running / waiting)
* `sshare -U $USER` - See share usage
* `sshare | grep akhanf` - See share usage for entire lab
* `scancel <jobid>` - Remove job associated with `<jobid>`
* `scancel -u $USER` - Remove all your submitted jobs (BE CAREFUL)
* `sacct -j <jobid> --format JobID,ReqMem,MaxRSS,Timelimit,Elapsed` - Check
completed job ussage

Run the following to set-up your `.bashrc` to enable a more readable `sacct` 
output:

```bash
echo “export SLURM_TIME_FORMAT=relative” >> ~/.bashrc
echo “export SACCT_FORMAT=JobID%-20,Start%-10,Elapsed%-10,State,AllocCPUS%8,MaxRSS,NodeList” >> ~/.bashrc
```

### Visualization
You can also use X forwarding to visualize your data via SSH. To do so, run the
following command:

```bash
ssh -Y <user>@graham.computecanada.ca
```
{: .important}
By default, this brings you to the login node which **is not** a compute node. 
This should only be used for viewing images.


[CCDB]: https://ccdb.computecanada.ca/security/login
[Globus]: https://globus.computecanada.ca
