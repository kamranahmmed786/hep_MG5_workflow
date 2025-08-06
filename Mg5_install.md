# MadGraph5 Multicore Setup Guide

This guide provides instructions for setting up system dependencies, installing Python and LHAPDF, and running MadGraph5 (MG5_aMC) in multicore mode.

---

## Table of Contents

- [1. Install System Packages](#1-install-system-packages)
- [2. Install Python](#2-install-python)
- [3. Install MadGraph5](#3-install-madgraph5)
- [4. Install LHAPDF (Optional)](#4-install-lhapdf-optional)
- [5. Install External Tools from MG5 Interface](#5-install-external-tools-from-mg5-interface)
- [6. Configure MadGraph5 for Multicore Mode](#6-configure-madgraph5-for-multicore-mode)
- [7. Test Process Submission](#7-test-process-submission)
- [8. Generate Realistic Physics Samples](#8-generate-realistic-physics-samples)
 
---

## 1. Install System Packages

Install the required system packages:

```bash
sudo dnf install gcc-c++ gcc-fortran make cmake
````

OR

```bash
sudo apt install gcc-c++ gcc-fortran make cmake
````

These are needed for compiling MadGraph5 and LHAPDF.

---

## 2. Install Python

Make sure you have a Python version that is compatible with MadGraph5.

If not, follow this guide:

* [Python Installation Guide](Python3.9_install.md)

---

## 3. Install MadGraph5

Download and extract MadGraph5 from the official site:

* [Launchpad](https://launchpad.net/mg5amcnlo)

---

## 4. Install LHAPDF (Optional)

You can install LHAPDF either as a standalone tool or from within MadGraph5.

* [LHAPDF6 Installation Guide](lhapdf6_install.md)

Alternatively, you can install it later from inside MG5.

---

## 5. Install External Tools from MG5 Interface

Once MG5 is installed, launch it:

```bash
cd /path/to/MG5
./bin/mg5_aMC
```

Inside the MG5 prompt, install the following:

```text
install pythia8
install lhapdf6   # Only if you didn’t install LHAPDF separately
```

---

## 6. Configure MadGraph5 for Multicore Mode

From within the MG5 prompt, run:

```text
set run_mode 2
```

* `run_mode 2`: Enables multicore execution on a single machine.

You can now generate and launch processes using all available CPU cores.

---

## 7. Test Process Submission

Inside the MG5 prompt, try the following:

```text
generate p p > t t~ [QCD]
output pp_tt_NLO
launch
```

This will generate and run a basic NLO process for top quark pair production.

---

## 8. Generate Realistic Physics Samples

To understand how to generate realistic physics samples correctly using MG5, see the following guide:

* [Sample Generation Guide](sample_generation.md)
