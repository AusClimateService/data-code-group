# ACS Data Standards

## Overview
The Australian Climate Service will produce a huge array of outputs, including a large number of climate datasets. 
This document is to set data standards that will apply across the various Work Packages in ACS Project 2, 
to ensure that data produced by ACS and shared among the climate community is both consistent, and meets the FAIR principles of data management.

Specifically, these standards will apply to any climate datasets to be inlcuded in the ACS Shared Data space, NCI project ia39, 
following the [ACS data roadmap](data_roadmap.md).

### Adopted standards & metadata conventions
Wherever possible, the [CORDEX-CMIP6](https://cordex.org/wp-content/uploads/2021/05/CORDEX-CMIP6_exp_design_RCM.pdf) and CMIP6 data standards will be adopted, 
in order to facilitate as much consistency between ACS and other state/international regional modelling efforts.

More generally, [CF conventions](https://cfconventions.org/Data/cf-standard-names/77/build/cf-standard-name-table.html) for standard_names,
and the [Attribute Convention for Data Discovery, ACDD](https://wiki.esipfed.org/Attribute_Convention_for_Data_Discovery_1-3) for metadata attributes, 
will be adopted where appropriate.

### File formats
All ACS climate datasets must be formatted in netCDF4, unless required by ACS customers (e.g. CSVs for use in online platforms), 
with one output variable per dataset. Output variables must should be written using single precision (NC_FLOAT), while coordinates written 
using double precision (NC_DOUBLE), according to [CMIP6 requirements](https://docs.google.com/document/d/1os9rZ11U0ajY7F8FWtgU4B49KcB59aFlBVGfLC4ahXs/edit) 
(and expected CORDEX-CMIP6 requirements).

### Variables (data request)
CORDEX-CMIP6 is currently ongoing, with its [data request](https://cordex.org/wp-content/uploads/2021/09/CORDEX_CMIP6_Data_Request_Atmos_v1.xlsx-Atmos.pdf)
recently undergoing a phase of community comment.
The [CMIP6 data request](http://clipc-services.ceda.ac.uk/dreq/index.html) will be used as a guide to help complete the ACS data standards.

### Controlled Vocabulary (CV) & Data Reference System (DRS)
A CORDEX-CMIP6 CV and DRS are yet to be circulated, but they are expect to be similar to those of [CORDEX-CMIP5](https://is-enes-data.github.io/cordex_archive_specifications.pdf).
The [CMIP6 CV](https://docs.google.com/document/d/1h0r8RZr_f3-8egBMMh7aqLwy3snpD6_MrDz1q8n5XUk/edit) will be referenced where appropriate.

### Licensing 
??? to be advised by legal. [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) as standard?


