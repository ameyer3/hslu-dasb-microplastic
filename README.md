# The plastic drift

This repository contains the Shiny application and data processing scripts for analyzing and visualizing the drift of microplastics in marine environments. It processes buoy movement data and marine microplastic concentration data to explore their relationship and patterns.

# Repository structure

```sh
├── README.md
├── data-cleaning # preparation of datasets
│   ├── Marine Microplastic Concentrations-left.csv
│   ├── Marine Microplastic Concentrations-right.csv
│   ├── clean_microplastics.R
│   ├── cluster_currents.R
│   ├── currents_by_buoy_time.R
│   └── link_closest_microplastic.R
├── install.R # all R-package dependencies
└── plastic-drift-app # shiny app itself
    ├── assets # media assets
    │   └── equirectangular_projection.jpg
    ├── datasources # cleaned datasets used for shiny app
    │   ├── binned_currents.parquet
    │   ├── cleaned_microplastics.parquet
    │   ├── currents_by_buoy_time.parquet
    │   └── currents_with_microplastics.parquet
    ├── helpers # helper functions for the visualization
    │   ├── visualize-attributes.R
    │   ├── visualize-buoyes.R
    │   ├── visualize-correlations.R
    │   ├── visualize-forecasting.R
    │   └── visualize-movement.R
    ├── server.R
    └── ui.R
```

# Install Dependencies

Run the [`install.R`](/install.R) script to install all required dependencies to run this application.

# Run shiny app

Invoke the following command to run the Shiny App: `R -e "shiny::runApp('plastic-drift-app')"`.

# Data Cleaning

All the scripts used to clean and transform the datasets can be found in [data-cleaning](/data-cleaning/).
The output of each data-cleaning script is in [plastic-drift-app/datasources](/plastic-drift-app/datasources), so that the app works out of the box.

Some data cleaning scripts require a dataset which isn't embedded in this repository due to the large size, but it can be manually downloaded using R (this might take a while):

```R
options(timeout = 100000)
download.file(
  url = "https://www.aoml.noaa.gov/ftp/phod/buoydata/buoydata_15001_current.dat.gz",
  destfile = "data-cleaning/buoydata_15001_jul24.dat.gz"
)
library(R.utils)
gunzip("data-cleaning/buoydata_15001_jul24.dat.gz", remove = TRUE)
```