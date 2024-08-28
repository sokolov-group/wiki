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

## Recommendations on using the Conda system:

1. python-X.X.X environments should contain only the most important python packages (numpy, scipy, h5py, etc)
2. Always load conda with the load_miniconda script:
```bash
echo 'alias load_miniconda="source /home/cbc-sokolov-group/python-3.9-miniconda-4.12/load_miniconda"' >> ~/.bashrc
source ~/.bashrc
```
3. Before switching between two environments, always run `conda deactivate` first to deactivate the current environment, then activate the new one
4. Please do not install anything in the base conda environment
5. Please do not install a python module with pip if it is available for installation (or already installed) in the conda environment itself
6. If a pip installation is requesting to install new packages, interrupt the installation, check if these packages are available in the conda environment, and (if available) install with conda, then restart the pip installation
7. Simply put, try to avoid using pip in a conda environment as much as possible. Conda is smarter and safer than pip
8. Please do not install psi4, pyscf or other important comp chem packages in the python-X.X.X environments. Those should be installed in the dedicated environments (e.g., pyscf-X.X, psi4-X.X)
9. Conda has a way to install custom personal environments, you can do that if you need one that is tailored for your needs. Pip also allows to install packages locally for a specific user
10. If you need a new package to be installed but don’t know how to do it properly, please consult with a more senior member of the group

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

## Conda Environments System Notes and Recommendations

- (08/04/2022): Miniconda distribution was chosen based on the flexibility of the minimal environments for our usage.
- (08/04/2022): NumPy isn't ready for Python 3.10 (C compiled files not available yet). Python 3.9 was chosen as our current by now.
- (08/04/2022): PySCF distribution in Conda is outdated. Our installations were done using [Pip](https://pyscf.org/install.html#installation-with-pip).
- (08/04/2022): To improve the long-term stability of our Conda Environment System, the primary installation package system should be Conda. The pip package installer should be use only if the package need is not available in Conda. Package requirements must be installed using Conda, if available.
- (08/04/2022): Development (local) versions of PySCF can be run using the Conda environment **python-3.9**.