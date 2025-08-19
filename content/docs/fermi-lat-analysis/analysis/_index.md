---
weight: 11
---

# Analysis

I will be explaining how you can analyze the point sources detected by Fermi LAT.

## Data download
Download the data for your specified source from the [link](https://fermi.gsfc.nasa.gov/cgi-bin/ssc/LAT/LATDataQuery.cgi).

<img width="610" height="290" alt="image" src="https://github.com/user-attachments/assets/c0af4537-753e-4d11-9a81-8fbb9a390b0b" />

For time conversion, you can use the [xTime](https://heasarc.gsfc.nasa.gov/cgi-bin/Tools/xTime/xTime.pl) tool.

Conventionally, we choose a search radius of 20$`\degree`$. Fermi LAT operates in the energy range ~20 MeV to >300 GeV, but we can generally choose 100 MeV to 500 GeV. We need the spacecraft file also for analysis.

## Background model download
We need to download the latest Galactic interstellar emission model and the Isotropic spectral template from this [page](https://fermi.gsfc.nasa.gov/ssc/data/access/lat/BackgroundModels.html). So download the _gll_iem_v07.fits_ and _iso_P8R3_SOURCE_V3_v1.txt_ for Event Selection of Pass 8 Source.

Additionally, I will suggest downloading the latest Fermi LAT catalog in FITS format from this [link](https://fermi.gsfc.nasa.gov/ssc/data/access/lat/14yr_catalog/).

Keep all these files in a separate folder, so that we can use them for each analysis.
