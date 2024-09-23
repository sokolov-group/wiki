---
layout: default
title: Bash Config
parent: Bash Guide
nav_order: 1
---

# Bash Usage
{: .no_toc}

Useful bash commands and a how-to on setting up a .bashrc file.
{: .fs-6 .fw-300 }

---
## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Using Bash
### Setting Up Bash Shell
Bash is both a Unix shell (a command-line interface) and a scripting language. It provides interactive features like job control, command-line editing, command history and aliases, as well as non-interactive features such as executing commands read from a file.

Whenever a new shell is opened, Bash runs the `.bashrc` file to initialize the shell session. Commands that need to be run at the start of every session can be placed in Bash's configuration file to automate this process.

The `.bashrc` file is located in your home directory, but is hidden (indicated by the period at the beginning of the file name). To view hidden files, use the terminal command **ls -a**:
```shell
(base) [user@hostname ~]$ ls -a
```
> **WARNING:** Hidden files are often integral to your system's proper operation. Do **NOT** move or edit these files unless you fully understand the consequences.
___

### Example Bash Script

Your `.bashrc` file should include the following commands:

```bash
# .bashrc

# Load Modules and Environments
module load intel

# Temporary Directory
export TMPDIR=/scratch/local

# Number of CPUs
export OMP_NUM_THREADS=$(nproc)
export MKL_NUM_THREADS=$(nproc)

# PySCF Variables
export PYTHONPATH=$pyscf-path:$PYTHONPATH
export PYSCF_TMPDIR=/scratch/local/$USER

# User Specific Aliases and Functions
alias load_miniconda="source /home/cbc-sokolov-group/python-3.9-miniconda-4.12/load_miniconda"
```

#### Loading Modules
In order to use a compiled version of PySCF, MKL libraries must be loaded. The `module load` command allows you to load specific software modules (like Intel compilers). 

#### Setting Temporary Directory 
Temporary directories provide storage locations for programs that need to store intermediate data during execution. Setting `$TMPDIR` to local or scrach storage improves speed and avoids filling the main storage space.

#### Setting Number of CPUs
Define the number of CPUs that PySCF can use for efficient parallel processing by setting `$OMP_NUM_THREADS` and `$MKL_NUM_THREADS`, which can automatically be set to the number of available CPU cores with the `$nproc` command.

#### Setting PySCF variables
A compiled version of PySCF requires specific environment variables. Add the PySCF installation path (`$pyscf-path`) to the `$PYTHONPATH` variable and set the scratch directory for PySCF jobs using `$PYSCF_TMPDIR`. Replace `$pyscf-path` with the path to your installation. Additionally, if you have installed Python programs or libraries in a custom location, ensure that those directories are also included in `$PYTHONPATH` so that Python can locate and use them. For example, if your other packages are stored a folder called "Programming":
```bash
export PYTHONPATH = $pyscf-path:$HOME/Programming:$PYTHONPATH
```
___

#### User-Defined Aliases
Aliases allow you to create custom shortcutes for commonly used commands. For example, instead of always typing `ls -alF` when you want to list files with detailed information, you could create an alias `ll`:
```bash
alias ll='ls -alF'
```
This means executing `ll` is the same as executing `ls -al F`. Aliases can also be set for common SSH points.
```bash
alias owens_osc='ssh username@owens.osc.edu'
``` 
In the example file, the alias `load_miniconda` uses a `source` command that reads and executes a file to load our Conda environments system.

Aliases can be checked from command-line using the `type` command, which displays information about the command type.
```bash
(base) [user@hostname ~]$ type load_miniconda
load_miniconda is aliased to `source /home/cbc-sokolov-group/python-3.9-miniconda-4.12/load_miniconda`
```

### Checking Environment Variables
You can check the value of environment variables, such as `$PYTHONPATH`, by using the following command:
```shell
(base) [user@hostname ~]$ echo $PYTHONPATH
```

<!--
When using compiled PySCF installation, it's required to load MKL libraries and setup Python variables. The full path to your PySCF installation `$pyscf-path` should be added to the `$PYTHONPATH` variable. It's recommended to define the scratch directory `$PYSCF_TMPDIR` and the number of CPUs.
```bash
# Load modules and environments
module load intel
conda activate python-3.9

# Setting up PySCF Variables
export PYTHONPATH=$pyscf-path:$PYTHONPATH
export PYSCF_TMPDIR=/scratch/local/$USER

# Setting up number of CPUs
export OMP_NUM_THREADS=8
export MKL_NUM_THREADS=8
```

### Using _load_local_pyscf_2.2.1_ script
A compiled version of PySCF 2.2.1 is available at `cbc-sokolov-group/python-packages/pyscf-2.2.1/` folder. It can be easily loaded using the `load_local_pyscf_2.2.1` script:
```bash
source /home/cbc-sokolov-group/python-3.9-miniconda-4.12/load_local_pyscf_2.2.1
```

This script can also be added as a alias in the `~/.bashrc` file:
```bash
echo 'alias load_local_pyscf_2.2.1="source /home/cbc-sokolov-group/python-3.9-miniconda-4.12/load_local_pyscf_2.2.1"' >> ~/.bashrc
source ~/.bashrc
```

### Using _load_local_pyscf_2.1.1_ script
A compiled version of PySCF 2.1.1 is available at `cbc-sokolov-group/python-packages/pyscf-2.1.1/` folder. It can be easily loaded using the `load_local_pyscf_2.1.1` script:
```bash
source /home/cbc-sokolov-group/python-3.9-miniconda-4.12/load_local_pyscf_2.1.1
```

This script can also be added as a alias in the `~/.bashrc` file:
```bash
echo 'alias load_local_pyscf_2.1.1="source /home/cbc-sokolov-group/python-3.9-miniconda-4.12/load_local_pyscf_2.1.1"' >> ~/.bashrc
source ~/.bashrc
```

### Using _load_local_pyscf_2.0.1_ script
A compiled version of PySCF 2.0.1 is available at `cbc-sokolov-group/python-packages/pyscf-2.0.1/` folder. It can be easily loaded using the `load_local_pyscf_2.0.1` script:
```bash
source /home/cbc-sokolov-group/python-3.9-miniconda-4.12/load_local_pyscf_2.0.1
```

This script can also be added as a alias in the `~/.bashrc` file:
```bash
echo 'alias load_local_pyscf_2.0.1="source /home/cbc-sokolov-group/python-3.9-miniconda-4.12/load_local_pyscf_2.0.1"' >> ~/.bashrc
source ~/.bashrc
```
-->

