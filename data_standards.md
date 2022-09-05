# ACS Data Standards

## Overview
The Australian Climate Service will produce a huge array of outputs, including a large number of climate datasets. 
This document is to set data standards that will apply across the various Work Packages in ACS Project 2, 
to ensure that data produced by ACS and shared among the climate community is both consistent, and meets the FAIR principles of data management.

Specifically, these standards will apply to any climate datasets to be included in the ACS Shared Data space, NCI project ia39, 
following the [ACS data roadmap](data_roadmap.md).  
Authoritative ACS datasets must be CMORised; i.e. post-processed through a standardised and version controlled 
data pipeline to meet CORDEX-level compliance standards, and formatted into a documented directory and filename structure (DRS).
CMORisation pipeline tools must adhere to the ACS [`code_roadmap.md`](code_roadmap.md).

#### Adopted standards & metadata conventions
Wherever possible, the [CORDEX-CMIP6](https://cordex.org/wp-content/uploads/2021/05/CORDEX-CMIP6_exp_design_RCM.pdf) and CMIP6 data standards will be adopted, 
in order to facilitate as much consistency between ACS and other state/international regional modelling efforts.

More generally, [CF conventions](https://cfconventions.org/Data/cf-standard-names/77/build/cf-standard-name-table.html) for standard_names,
and the [Attribute Convention for Data Discovery (ACDD)](https://wiki.esipfed.org/Attribute_Convention_for_Data_Discovery_1-3) for metadata attributes, 
will be adopted where appropriate.

#### File formats
All ACS climate datasets must be formatted in netCDF4, unless required by ACS customers (e.g. CSVs for use in online platforms), 
with one output variable per dataset. Output variables should be written using single precision (NC_FLOAT), with coordinates written 
using double precision (NC_DOUBLE), according to [CMIP6 requirements](https://docs.google.com/document/d/1os9rZ11U0ajY7F8FWtgU4B49KcB59aFlBVGfLC4ahXs/edit) 
(and expected CORDEX-CMIP6 requirements).

#### Variables (data request)
CORDEX-CMIP6 is currently in a late stage of development, with its [data request](https://cordex.org/wp-content/uploads/2021/09/CORDEX_CMIP6_Data_Request_Atmos_v1.xlsx-Atmos.pdf)
recently undergoing a phase of community comment.
The [CMIP6 data request](http://clipc-services.ceda.ac.uk/dreq/index.html) will be used as a guide to help complete the ACS data standards.

#### Controlled Vocabulary (CV) & Data Reference System (DRS)
A CORDEX-CMIP6 CV and DRS are yet to be circulated, but they are expected to be similar to those of [CORDEX-CMIP5](https://is-enes-data.github.io/cordex_archive_specifications.pdf).
The [CMIP6 CV](https://docs.google.com/document/d/1h0r8RZr_f3-8egBMMh7aqLwy3snpD6_MrDz1q8n5XUk/edit) will be referenced where appropriate.

#### Licensing 
To be advised by ACS Data Governance Framework. [CC-BY v4.0](https://creativecommons.org/licenses/by/4.0/) as standard.

## DRSs

### CORDEX-CMIP6+
*Adopted from [CORDEX-CMIP5 archive specifications](http://is-enes-data.github.io/cordex_archive_specifications.pdf).*

#### Directory structure:  

/g/data/ia39/australian-climate-service/\<**status**\>/\<**activity**\>/\<**product**\>/\<**domain**\>/\<**RCM-institution**\>/\<**GCM-model-name**\>/\<**CMIP6-experiment-name**\>/\<**CMIP6-ensemble-member**\>/\<**RCM-model-name**\>/\<**RCM-version-ID**\>/\<**frequency-or-category**\>/\<**variable-name**>

#### Filenaming:  

\<**variable-name**\>\_\<**domain**\>\_\<**GCM-model-name**\>\_\<**CMIP6-experiment-name**\>\_\<**CMIP6-ensemble-member**\>\_\<**RCM-model-name**\>\_\<**RCM-version-id**\>\_\<**frequency-or-category**\>[\_\<**StartTime-EndTime**\>].nc
  
#### Controlled Vocabulary:

| **key** = | [*restriction*:] { item1 item2 ... }  |
| ------------ | ------------ | 
| **status** | { `test-data`, `release` }  |
| **activity** | { `CORDEX-CMIP6` }  |
| **product** | { `output`, `bias-adjusted-output`, `indices`, `bias-adjusted-indices` }  |
| **domain** | { AUS-11i AUS-17i  }  |
|  **RCM-institution** | { BOM CSIRO QLD-DES? ??? }  |
|**GCM-model-name** | refer to [CMIP6 CV](https://github.com/WCRP-CMIP/CMIP6_CVs/blob/master/CMIP6_source_id.json); format=institution_id-source_id (e.g. CSIRO-ARCCS-ACCESS-CM2) |
| **CMIP6-experiment-name** | *CMIP6*: { historical ssp126 ssp245 ssp370 ssp585 } <br/> *ERA5*: { evaluation }  |
| **CMIP6-ensemble-member** | { r?i?p?f? (e.g. r6i1p1f1) } |
| **RCM-model-name** | { CCAM-???? BARPA-R CCAM-Qld }  |
| **RCM-version-id** | { v1 v2 ... }  |
| **frequency-or-category** | *output, bias-corrected-output*: { mon day 6hr 1hr 15min } <br/> *indices, bias-corrected-indices*: { climdex gev fire heat coasts trop-cyclones ... } |
| **variable-name** | *output*: see [CORDEX-CMIP6 Atmosphere Variable List](https://docs.google.com/spreadsheets/d/1qUauozwXkq7r1g-L4ALMIkCNINIhhCPx/edit#gid=1672965248) <br/> *indices*: { cdd cwd fd r10mm r95ptot rx1day txn txx ... } <br/> *bias-adjusted-output, bias-adjusted-indices*: add 'Adjust' to end of output variable-name (e.g. pr -> prAdjust); see [CORDEX-Adjust DRS](http://is-enes-data.github.io/CORDEX_adjust_drs.pdf) |

### ESCI
*Adopted from [CORDEX-CMIP5 archive specifications](http://is-enes-data.github.io/cordex_archive_specifications.pdf).*  
See https://github.com/AusClimateService/ESCI-data-collection

#### Directory structure:  

\<**activity**\>/\<**product**\>/\<**domain**\>//\<**GCM-model-name**\>/\<**CMIP5-experiment-name**\>/\<**CMIP5-ensemble-member**\>/\<**RCM-model-name**\>/\<**RCM-version-ID**\>/\<**frequency**\>/\<**variable-name**>

#### Filenaming:  

\<**variable-name**\>\_\<**domain**\>\_\<**GCM-model-name**\>\_\<**CMIP5-experiment-name**\>\_\<**CMIP5-ensemble-member**\>\_\<**RCM-institute-and-model-name**\>\_\<**RCM-version-id**\>\_\<**frequency**\>[\_\<**StartTime-EndTime**\>].nc
  
#### Controlled Vocabulary:

| **key** = | [*restriction*:] { item1 item2 ... }  |
| ------------ | ------------ | 
| **activity** | { ESCI }  |
| **product** | { output bias-adjusted-output }  |
| **domain** | { AUS-ESCI AUS-ESCI-noWA }  |
|**GCM-model-name** | { CSIRO-BOM-ACCESS1-0 CCCMA-CanESM2 CNRM-CERFACS-CNRM-CM5 NOAA-GFDL-ESM2M MIROC-MIROC5 NCC-NorESM1-M }  |
| **CMIP6-experiment-name** | { historical rcp45 rcp85 } |
| **CMIP6-ensemble-member** | { r1i1p1 } |
| **RCM-institute-and-model-name** | { CSIRO-CCAM-???? BOM-BARPA-R NSW-NARCliMJ NSW-NARCliMK none }  |
| **RCM-version-id** | *output*: { v1 } <br/> *bias-corrected-output*: { v1-QME }  |
| **frequency** | { day 3hr 30min } |
| **variable-name** | *output*: { tasmax tasmin pr ps clt dni scfWindDir WindDir150 WindDir250 Wind150 Wind250 sfcWind tdry tdew hurs ghi } <br/> *bias-adjusted-output*: { tasmaxAdjust tasminAdjust prAdjust FFDI } |

