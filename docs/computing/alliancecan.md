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
After setting up the passwordless SSH, follow the next steps:
1. Create a new bash file (location doesn't matter) with the following content:
    ```bash
    #!/bin/bash
    mount_dir="<MOUNT_DIR>"
    if (! mountpoint -q $mount_dir); then
        sshfs <user>@graham.sharcnet.ca:/home/<user>/ $mount_dir -o   ServerAliveInterval=15,ServerAliveCountMax=3,Compression=no,follow_symlinks
    else
        umount $mount_dir
    fi
    ```
    Replace `<MOUNT_DIR>` with the directory to which you want to mount your Graham home folder. Also, substitute `<user>` with your corresponding user. \
    The name of the file will be the command that you will use to mount and unmount your Graham folder, so make sure to use an easy to remember; for example, `graham_sshfs.sh`.
2. Rename the file to remove the `.sh` extension.
3. Create a new folder in your local home folder: `mkdir -p ~/bin`. 
4. Copy the previous file to that location (`cp <file_name> ~/bin`) and add execution permissions to it (`chmod 755 ~/bin/<file_name>`).
5. Add the following line at the end of your bashrc file:
    ```bash
    export PATH=$PATH:~/bin
    ```
6. Reload your bashrc file: `source ~/.bashrc`.

Now, you should be able to mount or unmount your Graham home folder by running `<file_name>` in the terminal.

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

### Run Jupyter Notebooks in your local VS Code
To be able to run Jupyter Notebooks in Visual Studio Code from your local machine, use the following instructions:
1. Follow the instructions above to set the passwordless SSH.
2. Open your local VS Code and install the `Remote - SSH` extension.
3. Hit `Ctrl+Shift+p` and type `Remote-SSH: Open SSH configuration file...`. Select the file in your home directory and set it to:
    ```
    Host graham.sharcnet.ca
        HostName graham.sharcnet.ca
        User <username>
        IdentityFile ~/.ssh/<file>
    ```
    Replace `<username>` with your corresponding Graham username and `<file>` with the file generated when setting the passwordless SSH connection.
4. Before connecting to the server, go to the settings of the Remote-SSH extension and set the Connect Timeout value to a higher value than the default, for example, 10000 (since Graham usually responds slowly).
5. Use `Ctrl+Shift+p` again, type `Remote-SSH: Connect to Host...` and use the previous config file. This will enable the SSH connection between VS Code and Graham. You should now be able to see your Graham folders in VS Code.
6. In a terminal, ssh to Graham. 
    1. Create a virtual environment using `kpy create <name>` (from [kslurm](https://github.com/pvandyken/kslurm) tool). 
    2. Load the venv and install `jupyterlab` plus any other packages you need.
    3. Save the env (`kpy save <name of your venv>`) and deactivate the venv (`deactivate`). 
    4. Run `kjupyter` with any required specifications and using the created venv (refer to the instructions [here](https://github.com/pvandyken/kslurm)).
7. Return to the VS Code window from step 5 and open the Jupyter file that you want to run.
8. Use `Ctrl+Shift+p` and type `Jupyter: Specify Jupyter Server for Connections`. Paste the URL given by kjupyter for the server connection.

>
- If kjupyter command doesn't work after step 6, try installing `jupyterlab` in your local Python in Graham (without any venv activated, run `pip install jupyterlab`).
- Running Jupyter Notebooks through SSH Tunneling is usually faster. When running `kjupyter`, this option is provided.  
{: .note}

### Visualization of Compute Nodes
In Graham, it is possible to run a VNC server in a compute node, which allows the visualization of results, such as plots, or using GUI applications as MATLAB. Follow these instructions to get a VNC connection to a compute node in Graham (based on the information found [here](https://docs.alliancecan.ca/wiki/VNC#VDI_Nodes)):
1. If using Linux or MacOs, download TigerVNC from the [official download page](https://sourceforge.net/projects/tigervnc/files/stable/). If using Windows, download and install VNC Viewer from the [official website](https://sourceforge.net/projects/tigervnc/files/stable/). Refer to the instructions [here](https://docs.alliancecan.ca/wiki/VNC#Setup) for more details.
2. Use ssh to connect to Graham login node. 
    1. Install `neuroglia-helpers` if not already done, refer to the [repository](https://github.com/khanlab/neuroglia-helpers) for more instructions.
    2. Run `regularInteractive` indicating the needed resources. Refer to the [repository](https://github.com/khanlab/neuroglia-helpers) for more instructions.
    3. Once the interactive session is opened, take note of the node to which you are connected and then run:
        ```
        export XDG_RUNTIME_DIR=${SLURM_TMPDIR}
        ```
    4. Run `vncserver`.
    5. Finally, run the followind command to know the connection port of the server:
        ```bash
        grep /home/<username>/.vnc/<log_file>.log
        ```
    This path will be shown in the terminal after executing `vncserver` in previous step. 

    {: .important}
    If you are configuring the VNC connection for the first time, make sure that you **DO NOT** leave the password empty. Save this password somewhere safe. 
    
3. In a new terminal, run the following command to set the ssh tunnel between your computer and the server configured in the previous step.
    ```bash
    ssh <username>@graham.sharcnet.ca -L <port on your computer>:<allocated node>:<port from the node> 
    ```
    Fill in the corresponding information. For the port on your computer, you can use the 5902. In `<allocated node>`, put the node that you allocated after step 3, starting with `gra` followed by a few numbers. Fill `<port from the node>` input the port from step 2.e.
4. Finally, open your VNC viewer application and connect to the local port that you decided in the previous step (for example: `localhost:5902`) and click on 'Connect'. Use the password that you configured in the step 2.d.

[CCDB]: https://ccdb.computecanada.ca/security/login
[Globus]: https://globus.computecanada.ca
