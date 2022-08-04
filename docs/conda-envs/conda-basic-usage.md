---
layout: default
title: Conda Basic Usage
parent: Conda Guide
nav_order: 1
---

# Conda Basic Usage
{: .no_toc}

Useful commands and tutorials about installation and use of Conda Environments.
{: .fs-6 .fw-300 }

---
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Initiating the Conda environments system
### Loading Conda manually
```bash
eval "$(/home/cbc-sokolov-group/python-3.9-miniconda-4.12/bin/conda shell.bash hook)"
```

### Using _load_miniconda_ script to load Conda
Alternativaly, we provide a BASH script to load our Conda environments system:
```bash
source /home/cbc-sokolov-group/python-3.9-miniconda-4.12/load_miniconda
```

An alias can be added to the `~/.bashrc` file:
```bash
echo 'alias load_miniconda="source /home/cbc-sokolov-group/python-3.9-miniconda-4.12/load_miniconda"' >> ~/.bashrc
source ~/.bashrc
```
And the script can be executed in the command line by:
```bash
load_miniconda
```

---

## Managing Conda Environments
### Activating Conda Environment
A environment named `$conda-env` can be activated by:
```bash
conda activate $conda-env
```

### List Conda Environments Available
A list of the Conda environments installed can be found by:
```bash
conda env list
```

### Deactivate Conda Environment
```bash
conda deactivate
```

---
