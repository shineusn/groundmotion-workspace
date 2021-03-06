ground Status
=======
[![Build Status](https://travis-ci.org/usgs/groundmotion-database.svg?branch=master)](https://travis-ci.org/usgs/groundmotion-database)

[![Codacy Badge](https://api.codacy.com/project/badge/Grade/46cce5f95a564e50bfc43cd6ab82e51f)](https://www.codacy.com/app/hschovanec-usgs/groundmotion-database?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=usgs/groundmotion-database&amp;utm_campaign=Badge_Grade)

[![Codacy Badge](https://api.codacy.com/project/badge/Coverage/46cce5f95a564e50bfc43cd6ab82e51f)](https://www.codacy.com/app/hschovanec-usgs/groundmotion-database?utm_source=github.com&utm_medium=referral&utm_content=usgs/groundmotion-database&utm_campaign=Badge_Coverage)


groundmotion-database
=====

Fetch and process ground motion waveform/peak amplitude data.

# Introduction

groundmotion-database is a project designed to facilitate the loading of
ground motion time series data and parametric data into databases.
This repository includes the following tools:

 * `getpgm` : gathers pgm values from a directory of ground motion files and
and outputs simple flatfiles and tables of IMC and IMT values.

# Installing

#### If you already have a miniconda or anaconda Python 3.5 environment:

Automated install:
- `git clone https://github.com/usgs/groundmotion-database.git`
- `cd groundmotion-database`
- `bash intall.sh`
- `conda activate gmdb`

Manual install:
 - `conda install numpy`
 - `conda install pandas`
 - `conda install openpyxl`
 - `conda install lxml`
 - `conda install amptools`
 - `pip install git+https://github.com/usgs/groundmotion-database.git`


#### If you do not have anaconda or miniconda, but have Python 3.5 installed with pip:
 - `pip install numpy`
 - `pip install pandas`
 - `pip install openpyxl`
 - `pip install lxml`
 - `pip install git+https://github.com/usgs/shakemap-amp-tools.git`
 - `pip install git+https://github.com/usgs/groundmotion-database.git`

## Updating

Updating automated install:
- `cd groundmotion-database`
- `git pull --ff-only https://github.com/usgs/groundmotion-database.git master`
- `bash install.sh`

Updating manually installed:
 - `pip install --upgrade git+https://github.com/usgs/groundmotion-database.git`

# Tools

## getpgm

This tool presumes there is a directory containing files of ground
motion data as time series, in a format supported by amptools. At this time
time series must be acceleration.

Supported formats include:git reset --hard upstream/master
- [COSMOS](https://strongmotioncenter.org/vdc/cosmos_format_1_20.pdf
)
- CWB
- [DMG](ftp://ftp.consrv.ca.gov/pub/dmg/csmip/Formats/DMGformat85.pdf
) (synonymous to CSMIP)
- [GEONET](https://www.geonet.org.nz/data/supplementary/strong_motion_file_formats)
- [KNET](http://www.kyoshin.bosai.go.jp/kyoshin/man/knetform_en.html
)
- [SMC](https://escweb.wr.usgs.gov/nsmp-data/smcfmt.html
)
- [USC](https://strongmotioncenter.org/vdc/USC_Vol1Format.txt)

### Use
getpgm [-h] -c COMPONENTS [COMPONENTS ...] -m MEASUREMENTS
              [MEASUREMENTS ...] [-t] [-p]
              input_source output_directory

Get requested PGM values.


#### Positional arguments

  input_source:          The directory of all input files.

  output_directory:      The directory of all output files.

#### Optional arguments

  -h, --help:            show this help message and exit

  -c COMPONENTS [COMPONENTS ...], --components COMPONENTS [COMPONENTS ...]:
                        The IMC parameters to get.


  -m MEASUREMENTS [MEASUREMENTS ...], --measurements MEASUREMENTS [MEASUREMENTS ...]:
                        The IMT parameters to get.


  -t, --timeseries:      Writes out the uncorrected time series for each
                        station in miniseed.


  -p, --parametric:      Writes out the parametric data for each station.

  usage: getpgm [-h] -c COMPONENTS [COMPONENTS ...] -m MEASUREMENTS
              [MEASUREMENTS ...] [-t] [-p]
              input_source output_directory

    Get requested PGM values.

#### PGM Parameters
Available IMTs:
- pga
- sa
- pgv
- arias (arias intensity)

Available IMCs:
- greater_of_two_horizontals
- channels
- gmrotd
- rotd

#### For parameters with specific percentiles or periods, append the number on the end of the parameter string.

Example spectral amplitude: sa1.0

Example geometric mean rotation: gmrotd50


The [resulting files](https://github.com/usgs/groundmotion-database/tree/master/tests/output_examples) will contain each requested IMT for each component requested.
Units of returned IMTs are as follows:
- PGA: %g
- PGV: cm/s
- arias: m/s
- sa: %g

#### For further information refer to additional [notebooks](https://github.com/usgs/groundmotion-database/tree/master/notebooks)
