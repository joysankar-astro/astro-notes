---
weight: 11
---

# Analysis

I will be explaining how you can analyze the point sources detected by Fermi LAT.

## Background model download
We need to download the latest Galactic interstellar emission model and the Isotropic spectral template from this [page](https://fermi.gsfc.nasa.gov/ssc/data/access/lat/BackgroundModels.html). So download the _gll_iem_v07.fits_ and _iso_P8R3_SOURCE_V3_v1.txt_ for Event Selection of Pass 8 Source.

Additionally, I will suggest downloading the latest Fermi LAT catalog in FITS format from this [link](https://fermi.gsfc.nasa.gov/ssc/data/access/lat/14yr_catalog/).

Keep all these files in a separate folder, so that we can use them for each analysis.

## Data download
Download the data for your specified source from the [link](https://fermi.gsfc.nasa.gov/cgi-bin/ssc/LAT/LATDataQuery.cgi).

<img width="610" height="290" alt="image" src="https://github.com/user-attachments/assets/c0af4537-753e-4d11-9a81-8fbb9a390b0b" />

For time conversion, you can use the [xTime](https://heasarc.gsfc.nasa.gov/cgi-bin/Tools/xTime/xTime.pl) tool.

Conventionally, we choose a search radius of 20$`\degree`$. Fermi LAT operates in the energy range ~20 MeV to >300 GeV, but we can generally choose 100 MeV to 500 GeV. We need the spacecraft file also for analysis.

Now download all the files in a separate folder. Some files will contain _PH_, and some will contain _SC_ in their names. The _PH_ files hold the photon data, and _SC_ will hold the spacecraft data during that observation. Now, create a file that contains the list of _PH_ files using the code in the terminal opened in the same folder
```
ls *PH* > ph_list.dat
```
It will create a `ph_list.dat` file, which will list the _PH_ files.

> [!CAUTION]
> Make sure that the folder you create does not contain any spaces; otherwise, your analysis will fail.

## Configuration file
You need to create a `config.yaml` file in that folder where the data is located. It is like a simple text file, which contains the configuration information. This file will be structured as below

```YML
data:
  evfile : ph_list.dat
  scfile : L250815080059DAC8B79833_SC00.fits

binning:
  roiwidth   : 20.0
  binsz      : 0.1
  binsperdec : 8

selection :
  emin : 100
  emax : 500000
  zmax    : 90
  evclass : 128
  evtype  : 3
  tmin : 757382405.0
  tmax : 776908805.0
  filter : 'DATA_QUAL>0 && LAT_CONFIG==1'
  target : '3C 138'

gtlike:
  edisp: true
  irfs: 'P8R3_SOURCE_V3'
  edisp_disable : ['isodiff','galdiff']

model:
  src_radius : 15.0
  catalogs : '/home/joysankar/fermi-catlog/gll_psc_v35.fit'
  galdiff  : '/home/joysankar/fermi-catlog/gll_iem_v07.fits'
  isodiff  : '/home/joysankar/fermi-catlog/iso_P8R3_SOURCE_V3_v1.txt'
```

The `evfile` is the name of the _PH_ file list, which we have created previously. `scfile` is the spacecraft file you have already downloaded. Make sure to set emin (MeV), emax(MeV), tmin (MET), and tmax (MET). In `target`, put the object name, but better to use the 4FGL name. Make sure to give the appropriate path of catalogs, galdiff, and isodiff. `binsperdec` is a factor that determines the binning.

## Notebook analysis
Now open a terminal in that folder and activate the `fermipy` environment.
```
conda activate fermipy
```
Then open a Jupyter Notebook and run the code attached below step by step.

```python
from fermipy.gtanalysis import GTAnalysis
gta = GTAnalysis('config.yaml',logging={'verbosity' : 3})
gta.setup()
```
It will take time and perform the initial analysis.
```python
gta.optimize()
```
It will fit the spectral parameters of the source.

```python
gta.print_roi()
```
It will show the sources with TS values
Now we'll free the sources within the 3$`\degree`$ of ROI.

```python
gta.free_sources(free=False)
gta.free_sources(distance=3.0,pars='norm')
gta.free_source('4FGL J2321.9+2734')
gta.free_source('galdiff')
gta.free_source('isodiff')
```
You need to fit the parameters by running the code below
```python
gta.fit()
```

#### SED analysis
```python
sed = gta.sed('4FGL J2321.9+2734',make_plots=True)
```
It will generate a file like `4fgl_j0521.2+1637_sed.fits` which will be used for SED plotting.

#### Light curve analysis
```python
lc = gta.lightcurve('4FGL J2321.9+2734', binsz=21600.0,outdir='6hrs_dir', multithread=True, nthread=3, write_fits=True)
```
It will generate a file like `4fgl_j1310.5+3221_lightcurve.fits` which will be used for light curve plotting. The binsz is the binning time in seconds. The multithread is for parallel calculation. The outdir is the directory where each bin file will be generated. The nthread is the number of parallel threads. It will take time based on the binning size.
