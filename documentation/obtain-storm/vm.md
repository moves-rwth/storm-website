---
title: Use Virtual Machine
layout: default
documentation: true
category_weight: 6
categories: [Obtain Storm]
---

<h1>Use a Virtual Machine (VM)</h1>

{% include includes/toc.html %}

{:.alert .alert-danger}
The virtual machine images are outdated. We strongly suggest to use a [Docker container](docker.html){:.alert-link} instead.

On this page we provide (old) virtual machine images containing pre-installed versions of Storm.

When you have downloaded an OVA image, you can import it into, for example, [VirtualBox](https://www.virtualbox.org){:target="_blank"}. Before the first run, you should review the hardware resources allocated to the VM. E.g., for VirtualBox open *Settings → System* and adjust the memory size and CPU count under *Motherboard* and *Processor*, respectively.

{:.alert .alert-info}
For all VMs on this page, the username and password are both *storm* 

## How to create your own VM
Since the VMs on this page might be outdated, we also provide the steps to create your own VM:

* Download an `.iso` file for the operating system. In the following, we assume [Ubuntu](https://ubuntu.com/download/desktop){:target="_blank"}. Other linux-based systems are [supported](build.html#supported-operating-systems) as well, but might need different [preparations](dependencies.html#os-specific-preparations).
* Set up a virtual machine using the `.iso` file and a virtualization software such as [VirtualBox](https://www.virtualbox.org/){:target="_blank"}.

{:.alert .alert-danger}
Make sure to assign enough resources to the VM. Since the build process is quite memory-intensive, we recommend to set the memory limit to more than 4 GB.

* Once the operating system inside the VM is ready, open a terminal and (assuming Ubuntu) execute the following command to install the dependencies of Storm:
```console
sudo apt-get install build-essential git cmake libboost-all-dev libcln-dev libgmp-dev libginac-dev automake libglpk-dev libhwloc-dev libz3-dev libxerces-c-dev libeigen3-dev
```

* We are now ready to download and compile the source code by executing:
``` console
git clone https://github.com/moves-rwth/storm.git
cd storm
git checkout stable
mkdir build
cd build
cmake .. -DSTORM_LOAD_QVBS=ON
make binaries
echo "export PATH=\$PATH:$(realpath bin)" >> ~/.bashrc
source ~/.bashrc
```
To build Storm in a specific version, just replace the line `git checkout stable` above with `git checkout 1.4.1` or any other version.
For more information on these steps, see our guide for [building Storm from source](build.html)

The build process takes roughly one hour. After that, you should be able to run
```console
storm --qvbs crowds
```
which checks an instance of the [Crowds protocol](https://qcomp.org/benchmarks/index.html#crowds){:target="_blank"}.

To check your installation, you may also run:
```console
cd ~/storm/build
make check
```

{:.alert .alert-danger}
If any problems occurr during this process (in particular when using a standard Ubuntu version) please [let us know](troubleshooting.html#file-an-issue){:.alert-link}.

## Storm 1.6.3 (2020/12)

A VM running Ubuntu 20.04 and Storm 1.6.3 can be found at [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.4304439.svg)](https://doi.org/10.5281/zenodo.4304439). The root password is *storm*.

Storm is located at `/home/storm/storm` and the binaries can be found in `/home/storm/storm/build/bin`. For your convenience, the path containing the binaries is added to the `PATH`, meaning that you can run the Storm binaries from any location in the terminal. Moreover, the benchmarks from the [Quantitative Verification Benchmark Set](https://qcomp.org/benchmarks/) are included such that you can run, for example,
```console
storm --qvbs crowds
```
to check an instance of the [Crowds protocol](https://qcomp.org/benchmarks/index.html#crowds){:target="_blank"}.


## Storm 1.4.1 (2019/12)

A VM running Ubuntu 19.10 and Storm 1.4.1 can be found at [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.3585795.svg)](https://doi.org/10.5281/zenodo.3585795). The root password is *storm*.

Storm is located at `/home/storm/storm` and the binaries can be found in `/home/storm/storm/build/bin`. For your convenience, the path containing the binaries is added to the `PATH`, meaning that you can run the Storm binaries from any location in the terminal. Moreover, the benchmarks from the [Quantitative Verification Benchmark Set](https://qcomp.org/benchmarks/) are included such that you can run, for example,
```console
storm --qvbs crowds
```
to check an instance of the [Crowds protocol](https://qcomp.org/benchmarks/index.html#crowds){:target="_blank"}.

