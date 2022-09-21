---
layout: default
title: Orca Usage
parent: Orca Guide
nav_order: 1
---

# Orca Basic Usage
{: .no_toc}

Useful commands and tutorials about installation and use of Orca.
{: .fs-6 .fw-300 }

---
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Initiating the Orca setup
### Loading Orca 5.0.3 script
```bash
source /home/cbc-sokolov-group/orca_5_0_3_linux_x86-64_shared_openmpi411/load_orca_5.0.3
```

An alias can be added to the `~/.bashrc` file:
```bash
echo 'alias load_orca_5.0.3="source /home/cbc-sokolov-group/orca_5_0_3_linux_x86-64_shared_openmpi411/load_orca_5.0.3"' >> ~/.bashrc
source ~/.bashrc
```

And the script can be executed in the command line by:
```bash
load_orca_5.0.3
```

### Running Orca 5.0.3
After [initiating the Orca setup]({{ site.baseurl }}{% link docs/orca/orca-usage.md %}#initiating-the-orca-setup), you can use the command `orca503` to run a Orca 5.0.3 calculation. Using a `$orca-input` file, containing any extension (as `.in`, `.inp`, etc.):
```bash
orca503 $INPUT &
```
