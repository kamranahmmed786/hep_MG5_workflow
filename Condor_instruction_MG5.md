
# Cluster-wide Setup for MadGraph5 with HTCondor

This guide explains how to install system dependencies, Python, MadGraph5, and optionally LHAPDF on a Condor-based compute cluster. It also includes how to configure and test your MadGraph5 installation in cluster mode.

---

## Table of Contents

- [1. System Dependencies](#1-system-dependencies)
- [2. Install Python (Same Version on All Nodes)](#2-install-python-same-version-on-all-nodes)
- [3. Install MadGraph5](#3-install-madgraph5)
- [4. Install LHAPDF (Optional)](#4-install-lhapdf-optional)
- [5. Configure and Run MadGraph5 in Cluster Mode](#5-configure-and-run-madgraph5-in-cluster-mode)
- [6. Test Process Submission](#6-test-process-submission)

---

## 1. System Dependencies

Install the following system packages **on all cluster nodes** (submitter and workers):

```bash
sudo dnf install gcc-c++ gcc-fortran make cmake
````

These are required for compiling MadGraph and LHAPDF.

---

## 2. Install Python (Same Version on All Nodes)

Make sure all nodes have the **same Python version**. If not, follow the instructions in the guide below:

* [Python Installation Guide](Python3.9_install.md)

---

## 3. Install MadGraph5

To install MadGraph5 (MG5\_aMC) on all nodes or share it over NFS, follow this guide:

* [MadGraph5 Installation Guide](Mg5_install.md)

---

## 4. Install LHAPDF (Optional)

If you want to install LHAPDF as a standalone package (not from within MG5), you can follow the section in:

* [LHAPDF6 Installation Guide](lhapdf6_install.md)

Alternatively, install it directly within MadGraph using its internal script.

---

## 5. Configure and Run MadGraph5 in Cluster Mode

Once everything is installed:

```bash
cd /path/to/MG5
./bin/mg5_aMC
```

Inside the MG5 command line interface:

```text
set run_mode 1
set cluster_size 92       # Replace with total number of cores across all nodes
set cluster_type condor
```

> `run_mode 1` enables multicore/cluster running
> `cluster_type condor` uses HTCondor as the backend for job submission
> `cluster_size` is the total number of available cores across your cluster

---

## 6. Test Process Submission

Inside the MG5 prompt:

```text
generate p p > t t~ [QCD]
output pp_tt_NLO
launch
```

This will generate a basic NLO top quark pair production process and submit it to the Condor cluster.

---
