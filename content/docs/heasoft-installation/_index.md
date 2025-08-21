---
weight: 1
bookCollapseSection: true
title: "Heasoft Installation"
---

# Fermi LAT Analysis
{{< badge style="info" title="Written by" value="Joysankar Majumdar" >}}

**HEASOFT (High Energy Astrophysics Software)** is a comprehensive software package developed by NASA's High Energy Astrophysics Science Archive Research Center (HEASARC) for analyzing data from X-ray and gamma-ray astronomy missions. The suite includes tools for data reduction, spectral analysis, timing analysis, and image processing from missions like Chandra, XMM-Newton, Swift, NuSTAR, and many others. It provides both command-line utilities and interactive analysis environments, with core components like XSPEC for spectral fitting, XIMAGE for image analysis, and mission-specific tools for various high-energy observatories. HEASOFT is freely available and runs on Unix/Linux and macOS systems, making it an essential toolkit for researchers studying black holes, neutron stars, supernova remnants, and other high-energy astrophysical phenomena.

I will explain the installation in Ubuntu 24.

## Download installation file
Download the source code from the [link](https://heasarc.gsfc.nasa.gov/lheasoft/download.html). I recommend that you download the _Complete HEASoft source code (all mission & general-use software)_ from the page stated above.

Then extract it and put that extracted folder in a safe location where HEASOFT is to be installed.

## Prerequisites installation
Run the command below in the terminal.

```shell
sudo apt-get -y install libreadline-dev libncurses5-dev ncurses-dev curl \
libcurl4 libcurl4-gnutls-dev xorg-dev make gcc g++ gfortran perl-modules \
libdevel-checklib-perl libfile-which-perl python3-dev python3-pip python3-setuptools \
python3-astropy python3-numpy python3-scipy python3-matplotlib
```
I recommend installing `gedit` in the system. Thus, run the command below.
```
sudo apt install gedit
```
Now open the terminal in the root folder or just click the terminal icon. Write the variables below in the `.bashrc` file.
Open the `.bashrc` file using the command below.
```
gedit .bashrc
```
Now write the text in the `.bashrc` file.
```
export CC=/usr/bin/gcc
export CXX=/usr/bin/g++
export FC=/usr/bin/gfortran
export PERL=/usr/bin/perl
export PYTHON=/usr/bin/python3
```
