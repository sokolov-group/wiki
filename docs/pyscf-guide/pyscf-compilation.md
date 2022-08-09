---
layout: default
title: PySCF Compilation Guide
parent: PySCF Guide
nav_order: 3
---

# PySCF Compilation Guide
{: .no_toc}

Tutorials for installation of PySCF by compilation.
{: .fs-6 .fw-300 }

---
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## PySCF Compilation Guides
### PySCF 2.0.1 compilation using our Conda environments
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

### PySCF 2.0.1 compilation from scratch
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

To run compiled PySCF, follow [this procedure]({{ site.baseurl }}{% link docs/pyscf-guide/pyscf-usage.md %}#running-compiled-pyscf).
