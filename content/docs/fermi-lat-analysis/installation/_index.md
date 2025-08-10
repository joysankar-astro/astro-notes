---
weight: 10
---

# Installation

{{< badge style="info" title="Written by" value="Joysankar Majumdar" >}}

The Fermi mission provides a suite of tools called the _[Fermitools](https://fermi.gsfc.nasa.gov/ssc/data/analysis/documentation/)_ for the analysis of LAT. We are not going to use _Fermitools_ directly; rather, we are going to use _[FermiPy](https://fermipy.readthedocs.io/en/latest/index.html)_.

A Linux-based operating system is best for Fermi LAT analysis. We are going to follow the installation procedure for Ubuntu 24.04.2 LTS.

{{% steps %}}
1. We need to install the conda-forge distribution from the [GitHub](https://github.com/conda-forge/miniforge) repository. From the latest [release](https://github.com/conda-forge/miniforge/releases), download the _Miniforge**-Linux-x86_64.sh_ file. 

2. Run this script file with the _bash_ command.
   ```bash
   bash Miniforge3-25.3.1-0-Linux-x86_64.sh 
   ```
   It will be installed in your system. Generally, it creates a folder _miniforge_ in the home directory.

3. You need to export the path of the installed _miniforge_.
   ```bash
   export PATH=path_to_the_diretory/miniforge/condabin:$PATH
   ```
   And now, in that same terminal, you need to initialise conda.
   ```bash
   conda init
   ```
   Now close this terminal and open another terminal, and it should look like below
   <img width="1632" height="91" alt="image" src="https://github.com/user-attachments/assets/603fd95f-2e1c-48ac-a3e3-72e070026607"/>
   The (base) indicates the activation of the base environment in conda.

4. We have to create another environment for FermiPy. Run the command below in the terminal.
   ```bash
   mamba create --name fermipy -c conda-forge -c fermi python=3.9 "fermitools>=2.2.0" healpy gammapy
   ```
   After this, to activate the new _fermipy_ environment, run
   ```bash
   mamba activate fermipy
   ```
5. You have to install the fermipy package inside the fermipy environment
   ```bash
   pip install fermipy
   ```
   Additionally, you should install the Jupyter Notebook for better coding
   ```bash
   pip install notebook
   ```
{{% /steps %}}

You have successfully installed fermitools and FermiPy. Make sure to use FermiPy; you need to activate the _fermipy_ environment each time.
