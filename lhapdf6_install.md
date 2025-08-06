# LHAPDF 6.5.4 Installation Guide

This guide provides step-by-step instructions to build and install [LHAPDF](https://lhapdf.hepforge.org/) version 6.5.4 from source with a custom installation directory. This is useful for physics software stacks requiring LHAPDF without interfering with system-wide packages.

## Table of Contents

- [1. Create Installation Directory](#1-create-installation-directory)
- [2. Download and Extract Source](#2-download-and-extract-source)
- [3. Configure the Build](#3-configure-the-build)
- [4. Compile and Install](#4-compile-and-install)
- [5. Set Up Environment Variables](#5-set-up-environment-variables)
- [6. Verify Installation](#6-verify-installation)
- [7. Manage PDF Sets](#7-manage-pdf-sets)

---

## 1. Create Installation Directory

Create a directory to hold the LHAPDF build and installation:

```bash
mkdir LHAPDF
````

---

## 2. Download and Extract Source

Download the LHAPDF 6.5.4 source tarball from HepForge and extract it:

```bash
sudo wget https://www.hepforge.org/archive/lhapdf/LHAPDF-6.5.4.tar.gz
sudo tar -xzf LHAPDF-6.5.4.tar.gz
cd LHAPDF-6.5.4
```

---

## 3. Configure the Build

Run the configuration script with a custom installation prefix:

```bash
./configure --prefix=/path/to/LHAPDF
```

Replace `/path/to/LHAPDF` with the full path where you want LHAPDF installed (e.g., `/home/username/LHAPDF` or `/opt/lhapdf`).

---

## 4. Compile and Install

Compile LHAPDF using all available cores, then install it:

```bash
sudo make -j$(nproc)
sudo make install
```

---

## 5. Set Up Environment Variables

Export the following environment variables to make LHAPDF tools available:

```bash
export PATH=$PATH:/path/to/LHAPDF/bin
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/path/to/LHAPDF/lib
export PYTHONPATH=$PYTHONPATH:/path/to/LHAPDF/lib/python3.12/dist-packages
export LHAPDF_DATA_PATH=/path/to/LHAPDF/share/LHAPDF
```

If using a different Python version, update the `python3.12` part accordingly.

To make these changes permanent, add them to your `.bashrc` or `.bash_profile`:

```bash
echo 'export PATH=$PATH:/path/to/LHAPDF/bin' >> ~/.bashrc
echo 'export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/path/to/LHAPDF/lib' >> ~/.bashrc
echo 'export PYTHONPATH=$PYTHONPATH:/path/to/LHAPDF/lib/python3.12/dist-packages' >> ~/.bashrc
echo 'export LHAPDF_DATA_PATH=/path/to/LHAPDF/share/LHAPDF' >> ~/.bashrc
source ~/.bashrc
```

---

## 6. Verify Installation

Confirm that LHAPDF is installed and functioning:

```bash
lhapdf --version
```

---

## 7. Manage PDF Sets

Update the PDF index and list/install sets:

```bash
lhapdf update
lhapdf list
lhapdf install NNPDF31_nlo_as_0118
```

This will download the `NNPDF31_nlo_as_0118` set into your `LHAPDF_DATA_PATH`.

---
