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

## Software installation
Now go to the folder where you have extracted the HEASOFT source code. Go to the `BUILD_DIR` folder and now open the terminal in this folder.
First, do the configuration, so run the code below in that terminal.
```shell
./configure > config.txt 2>&1
```
After configuration, open the `config.txt` file and check the end of the file. For successful configuration, the file ends with `Finished`. Now we need to build the software and thus run the code below.
```shell
make > build.txt 2>&1
```
It will take a longer time, maybe 40 minutes to 60 minutes. Check the long `build.txt` file; successful building ends with finished word. Now you need to install it. Run the code below for installation.
```shell
make install > install.txt 2>&1
```
Similarly, check `install.txt` for successful installation. If everything goes well, it will generate a platform folder inside the heasoft folder. The folder should look like `x86_64-pc-linux-gnu-libc2.39`.

## CALDB installation
We need to install the calibration database for the system and spacecraft.
Download the software caldb files from the [link](https://heasarc.gsfc.nasa.gov/FTP/caldb/software/tools/caldb_setup_files.tar.Z).
Create a folder named `caldb` in a safe location. Extract the software caldb file and copy the `software` folder inside the `caldb` folder. Create another folder named `data` inside the `caldb` folder. Now, inside the `data` folder, you need to download the mission-specific caldb files. The mission-specific caldb files can be downloaded from the [link](https://heasarc.gsfc.nasa.gov/docs/heasarc/caldb/caldb_supported_missions.html). For example, if you download the NuStar caldb files and extract them, copy the `nustar` folder inside that `data` folder. Similar way, download all the needed mission-specific caldb files.

## Variables initialization
Now open a new terminal and open the `.bashrc` file using the command `gedit .bashrc`. Now write the text in the file mentioned below.
```
export HEADAS=your_installation_path/x86_64-pc-linux-gnu-libc2.39
alias heainit=". $HEADAS/headas-init.sh"

export CALDB='your_caldb_path/caldb'
alias CALDB='source $CALDB/software/tools/caldbinit.sh'
export CALDBCONFIG='your_caldb_path/caldb/software/tools/caldb.config'
export CALDBALIAS='your_caldb_path/caldb/software/tools/alias_config.fits'
source $CALDB/software/tools/caldbinit.sh
```
Make sure to change the `your_installation_path` and `your_caldb_path` according to your installation.
Now save the file and close the terminal. Open a new terminal and type `heainit` to initialize the HEASOFT. To use any tool of HEASOFT, you need to `heainit` every time in the terminal.
