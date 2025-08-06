# MadGraph5 Cluster Installation and Configuration

This repository provides detailed step-by-step instructions for installing and configuring the following software components required for High Energy Physics simulations using **MadGraph5_aMC@NLO** on a Condor-based cluster.

Each guide is modular and focused on a specific part of the installation process.

---

## 📄 Installation Guides

### 1. Python Installation (3.9.19)

**File:** [`Python3.9_install.md`](Python3.9_install.md)

Install Python 3.9.19 from source with shared libraries enabled — required by LHAPDF and other tools.

---

### 2. LHAPDF6 Installation

**File:** [`lhapdf6_install.md`](lhapdf6_install.md)

Instructions to build and configure [LHAPDF6](https://lhapdf.hepforge.org/) from source. Covers setting environment variables and installing PDF sets like `NNPDF31_nlo_as_0118`.

---

### 3. MadGraph5_aMC@NLO Installation

**File:** [`Mg5_install.md`](Mg5_install.md)

Install and configure [MadGraph5_aMC@NLO](https://launchpad.net/mg5amcnlo) with multicore or Condor-based cluster support. Includes instructions for installing optional dependencies like LHAPDF and Pythia8 inside MG5.

---

### 4. Cluster-Wide Setup and Submission

**File:** [`cluster_mg5_setup.md`](Condor_instructions_MG5.md)

Instructions for installing system dependencies on both **submitter** and **worker nodes**, configuring MG5 for Condor execution, and testing NLO process generation.

---

### 5. Realistic Sample Generation

**File:** [`sample_generation.md`](sample_generation.md)

Best practices for generating realistic Monte Carlo samples with MadGraph, including:
- PDF and scale choices
- Cuts and filters
- Matching/merging settings
- Multi-parton final states

---

## ✅ Requirements

Ensure the following system-level tools are available on all cluster nodes:

```bash
sudo dnf install gcc-c++ gcc-fortran make cmake
