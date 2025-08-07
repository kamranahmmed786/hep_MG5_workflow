#  Build and Install Python 3.9.19 from Source (with Shared Libraries)

A step-by-step guide to compile and install Python 3.9.19 with shared library support (suitable for LHAPDF, ROOT, and other scientific libraries).

---

## Table of Contents
- [Step 1: Download Python Source](#step-1-download-python-3919-source-code)
- [Step 2: Extract and Navigate](#step-2-extract-the-archive-and-enter-source-directory)
- [Step 3: Configure and Build](#step-3-configure-and-build-python-with-shared-libraries)
- [Step 4: Setup Shared Libraries](#step-4-configure-dynamic-linker-to-find-python-shared-library)
- [Step 5: Verify Shared Libs](#step-5-confirm-shared-library-is-installed)
- [Step 6: Environment Setup](#step-6-add-python-39-to-your-environment)

---


## Installing Python 3.9.19 from Source (with Shared Library)

### Step 1: Download Python 3.9.19 source code

```bash
cd /usr/src
sudo wget https://www.python.org/ftp/python/3.9.19/Python-3.9.19.tgz
```

* Navigate to the system source directory.
* Download the official source tarball from python.org.

---

### Step 2: Extract the archive and enter source directory

```bash
sudo tar xzf Python-3.9.19.tgz
cd Python-3.9.19
```

* Extract the tarball.
* Enter the extracted source directory to build Python.

---

###  Step 3: Configure and build Python with shared libraries

```bash
sudo ./configure --enable-optimizations --enable-shared CFLAGS="-fPIC"
```

* `--enable-optimizations`: Enables PGO (Profile-Guided Optimization) for better performance.
* `--enable-shared`: Builds Python as a shared library (`libpython3.9.so`) needed by tools like LHAPDF.
* `CFLAGS="-fPIC"`: Ensures position-independent code, required for shared libraries on x86\_64.

```bash
sudo make -j$(nproc)
```

* Compile using all available CPU cores (`$(nproc)` returns the number of cores).

```bash
sudo make altinstall
```

* Install Python without overwriting the system's default `python3` binary.

  * This will create `/usr/local/bin/python3.9`.

---

### Step 4: Configure dynamic linker to find Python shared library

```bash
echo "/usr/local/lib" | sudo tee /etc/ld.so.conf.d/python3.9.conf
sudo ldconfig
```

* Adds `/usr/local/lib` to the dynamic linker config so it can find `libpython3.9.so`.
* `ldconfig` updates the cache with the new path.

---

### Step 5: Confirm shared library is installed

```bash
ls /usr/local/lib | grep libpython3.9.so
```

* Check that `libpython3.9.so` and its versioned symlinks exist in `/usr/local/lib`.

---

### Step 6: Add Python 3.9 to your environment

```bash
export PATH="/usr/local/bin:$PATH"
alias python3=/usr/local/bin/python3.9
alias python=/usr/local/bin/python3.9
alias pip3=/usr/local/bin/pip3.9
```

* Add `/usr/local/bin` to your path so custom Python binaries are found first.
* Set aliases to use Python 3.9 and pip 3.9 by default **in the current shell**.

To make this permanent, add the above lines to your `~/.bashrc` or `~/.bash_profile`.
```bash
echo 'export PATH="/usr/local/bin:$PATH"' >> ~/.bashrc
echo 'alias python3=/usr/local/bin/python3.9' >> ~/.bashrc
echo 'alias python=/usr/local/bin/python3.9' >> ~/.bashrc
echo 'alias pip3=/usr/local/bin/pip3.9' >> ~/.bashrc
source ~/.bashrc
```
