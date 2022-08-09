---
layout: default
title: Conda System Management
parent: Conda Guide
nav_order: 3
---

# Conda System Management
{: .no_toc}

Conda Environments System management commands and general notes. Administrator privilegies are required for management tasks.
{: .fs-6 .fw-300 }

---
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Creating new Conda environments
First, it's required to [load the Conda Environments System]({{ site.baseurl }}{% link docs/conda-envs/conda-basic-usage.md %}#initiating-the-conda-environments-system). Then, a new environment named `$conda-env` with the Python version number `$python-version` can be created by:
```bash
conda create -n $conda-env python=$python-version
```

## Installing packages in a Conda environment
After [activating the Conda Environments System]({{ site.baseurl }}{% link docs/conda-envs/conda-basic-usage.md %}#activating-conda-environment), a Python package named `$python-package` can be installed using:
```bash
conda install $python-package
```

To install an especific version `$package-version-num` of the Python package:
```bash
conda install $python-package=$package-version-num
```

## Installing packages in a Conda environment using pip
In a similar procedure, to install a Python package named `$python-package` in an active Conda environment, it's recommended to use:
```bash
python -m pip install $python-package
```

To install an especific version `$package-version-num` of the Python package:
```bash
python -m pip install $python-package=$package-version-num
```

## Example: Installation Procedure for PySCF 2.0.1 via Conda
```bash
# Create the Conda environment 'pyscf-2.0.1'
conda create -n pyscf-2.0.1 python=3.9
conda activate pyscf-2.0.1

# Install PySCF 2.0.1 requirements
conda install numpy scipy h5py mkl opt_einsum

# Install PySCF 2.0.1 via pip
python -m pip install pyscf
```

## Example: Local Installation Procedure for PySCF 2.0.1 via Compilation using our Conda environments
```bash
# Load Intel and CMake modules
module load intel cmake

# Load Conda environment 'python-3.9'
conda activate python-3.9

# Create PySCF directory
mkdir $HOME/python-packages
cd $HOME/python-packages
git clone https://github.com/pyscf/pyscf.git pyscf-2.0.1

# Install PySCF 2.0.1 via local compilation
cd pyscf-2.0.1/pyscf/lib/
mkdir build
cd build/
cmake -DBLA_VENDOR=Intel10_64lp_seq ..
make
```

### Running compiled PySCF
When using compiled PySCF installation, it's required to load MKL libraries and setup Python variables:
```bash
# Load modules and environments
module load intel
conda activate python-3.9

# Setting up PySCF Variables
export PYTHONPATH=$HOME/python-packages/pyscf-2.0.1:$PYTHONPATH
export PYSCF_TMPDIR=/scratch/local/$USER

# Setting up number of CPUs
export OMP_NUM_THREADS=8
export MKL_NUM_THREADS=8
```

## Example: Installation Procedure for PySCF 2.0.1 via Intel Compilation from scratch
```bash
# Load Intel and CMake modules
module load intel cmake

# Create the Conda environment 'python-3.9'
conda create -n python-3.9 python=3.9
conda activate python-3.9

# Install PySCF 2.0.1 requirements
conda install numpy scipy h5py mkl opt_einsum

# Create PySCF directory
mkdir $HOME/python-packages
cd $HOME/python-packages
git clone https://github.com/pyscf/pyscf.git pyscf-2.0.1

# Install PySCF 2.0.1 via local compilation
cd pyscf-2.0.1/pyscf/lib/
mkdir build
cd build/
cmake -DBLA_VENDOR=Intel10_64lp_seq ..
make
```
To run compiled PySCF, follow [this procedure]({{ site.baseurl }}{% link docs/conda-envs/conda-management.md %}#running-compiled-pyscf).

## Conda Environments System Notes and Recommendations

- (08/04/2022): Miniconda distribution was chosen based on the flexibility of the minimal environments for our usage.
- (08/04/2022): NumPy isn't ready for Python 3.10 (C compiled files not available yet). Python 3.9 was chosen as our current by now.
- (08/04/2022): PySCF distribution in Conda is outdated. Our installations were done using [Pip](https://pyscf.org/install.html#installation-with-pip).
- (08/04/2022): To improve the long-term stability of our Conda Environment System, the primary installation package system should be Conda. The pip package installer should be use only if the package need is not available in Conda. Package requirements must be installed using Conda, if available.
- (08/04/2022): Development (local) versions of PySCF can be run using the Conda environment **python-3.9**.