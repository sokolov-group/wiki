---
layout: default
title: PySCF Usage
parent: PySCF Guide
nav_order: 1
---

# PySCF Usage
{: .no_toc}

Useful commands and tutorials about installation and use of PySCF.
{: .fs-6 .fw-300 }

---
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Managing PySCF Installations
### Running compiled PySCF
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
