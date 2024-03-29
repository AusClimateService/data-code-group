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
Wherever possible, the [CORDEX-CMIP6](https://cordex.org/wp-content/uploads/2021/05/CORDEX-CMIP6_exp_design_RCM.pdf)
and CMIP6 data standards will be adopted, 
in order to facilitate as much consistency between ACS and other state/international regional modelling efforts.

More generally, [CF conventions](https://cfconventions.org/Data/cf-standard-names/77/build/cf-standard-name-table.html) for standard_names,
and the [Attribute Convention for Data Discovery (ACDD)](https://wiki.esipfed.org/Attribute_Convention_for_Data_Discovery_1-3) for metadata attributes, 
will be adopted where appropriate.

#### File formats
All ACS climate datasets must be formatted in netCDF4,
unless required by ACS customers (e.g. CSVs for use in online platforms), 
with one output variable per dataset.
Output variables should be written using single precision (NC_FLOAT),
with coordinates written  using double precision (NC_DOUBLE),
according to [CMIP6 requirements](https://docs.google.com/document/d/1os9rZ11U0ajY7F8FWtgU4B49KcB59aFlBVGfLC4ahXs/edit) 
(and expected CORDEX-CMIP6 requirements).

#### Variables (data request)
CORDEX-CMIP6 is currently in a late stage of development,
with its [data request](https://cordex.org/wp-content/uploads/2021/09/CORDEX_CMIP6_Data_Request_Atmos_v1.xlsx-Atmos.pdf)
recently undergoing a phase of community comment.
The [CMIP6 data request](http://clipc-services.ceda.ac.uk/dreq/index.html) will be used as a guide to help complete the ACS data standards.

#### Controlled Vocabulary (CV) & Data Reference System (DRS)
A CORDEX-CMIP6 CV and DRS are yet to be circulated,
but they are expected to be similar to those of [CORDEX-CMIP5](https://is-enes-data.github.io/cordex_archive_specifications.pdf).
The [CMIP6 CV](https://docs.google.com/document/d/1h0r8RZr_f3-8egBMMh7aqLwy3snpD6_MrDz1q8n5XUk/edit) will be referenced where appropriate.

#### Licensing 
To be advised by ACS Data Governance Framework.
[CC-BY v4.0](https://creativecommons.org/licenses/by/4.0/) as standard.

## DRSs

### **CORDEX-CMIP6+**
*Adopted from [CORDEX-CMIP6 archive specifications SOD](https://drive.google.com/file/d/1r1oHCaOfL_kWqjqtTBrLlmow7p7Fe6Mz/view).*  
*updated 21/11/2023*

### Directory structure:  

\<**project_id**\>/\<**mip_era**\>/\<**activity_id**\>/\<**domain_id**\>/\<**institution_id**\>/\<**driving_source_id**\>/\<**driving_experiment_id**\>/\<**driving_variant_label**\>/\<**source_id**\>/\<**version_realization**\>/\<**frequency**\>/\<**variable_id**>/\<**version**\>

### Filenaming:  

\<**variable_id**\>\_\<**domain_id**\>\_\<**driving_source_id**\>\_\<**driving_experiment_id**\>\_\<**driving_variant_label**\>\_\<**institution_id**\>\_\<**source_id**\>\_\<**version_realization**\>\_\<**frequency**\>[\_\<**StartTime-EndTime**\>].nc
  
### Controlled Vocabulary:

| **key** = | [*restriction*:] { item1 item2 ... }  | notes |
| ------------ | ------------ | --------- |
| **project_id** | { `CORDEX`, `output` }  | |
| **mip_era** | { `CMIP6` }  | |
| **activity_id** | *Model output*: { `DD` } | |
| **domain_id** | format = \<**region**\>-\<**grid[i]**> <br/> { `AUS-10i`, `AUS-15`, `AUS-18`, `AUS-20i`, `AUS-r005`, `GLOBAL-gn` }  | `AUS-20i` is a CORDEX-Australasia example. <br/> `AUS-r005` is a AGCD indices example. <br /> `GLOBAL-gn` is a global climate model example where `gn` is the CMIP6 native grid abbreviation. |
| **institution_id** | { `BOM`, `CSIRO`, `NSW-DPE`, `QLD-DES`, `none` } | |
| **driving_source_id** | (e.g. `ERA5`, `ACCESS-CM2`, `ACCESS-ESM1.5`, `NorESM2-MM`, `EC-Earth3`, `CMCC-ESM2`, `CNRM-ESM2-1`, `CESM2`) | <br/> Refer to [CORDEX-CMIP6 CV](https://github.com/WCRP-CORDEX/cordex-cmip6-cmor-tables/blob/main/Tables/CORDEX_CV.json) for valid source names. |
| **driving_experiment_id** | *CMIP6*: { `historical`, `ssp126`, `ssp245`, `ssp370`, `ssp585`  } <br/> *ERA5*: { `evaluation` }  | Use `historical` when driving with an observational dataset like `AGCD` or `BARRA2` |
| **driving_variant_label** | { `r?i?p?f?`, `hres`, `eda`} | For CMIP6-driven simulations, use the ensemble string from the driving dataset (e.g. `r6i1p1f1`). <br/> `BARRA-R2` uses ERA5's HRES (deterministic) forcing while `BARRA-RE2` uses ERA5's EDA (ensemble of DA) forcing. |
| **source_id** | {  `BARPA-R`, `BARRA-R2`, `BARRA-RE2`, `CCAM-v2203-SN`, `none` }  | See https://opus.nci.org.au/display/CMIP/CMIP6-CORDEX+datasets for full list of Australian CORDEX models.
| **version_realization** | { `v?-r?`, `none`, `<RCMVersionID>-<BCname>-<OBSname>-<REFperiod>`} | (e.g. `v1-r1`, `v1-ecdfm-AGCD-1985-2014`) |
| **frequency** | *output, bias-corrected-output*: { `mon`, `day`, `6hr`, `3hr`, `1hr`, `15min` } <br/> *indices, bias-corrected-indices*: { `climdex`, `fire`, `heat`, `coasts`, `tropical-cyclones`, ... } | There are categories for [climdex indices](https://www.climdex.org/learn/indices/) and also each of the ACS hazard teams.
| **variable_id** | *output*: see [CORDEX-CMIP6 Atmosphere Variable List](https://docs.google.com/spreadsheets/d/1qUauozwXkq7r1g-L4ALMIkCNINIhhCPx/edit#gid=1672965248) <br/> *indices*: see [climdex indices list](https://www.climdex.org/learn/indices/) <br/> *bias-adjusted-output, bias-adjusted-indices*: add 'Adjust' to end of output variable-name (e.g. pr -> prAdjust); see [CORDEX-Adjust DRS](http://is-enes-data.github.io/CORDEX_adjust_drs.pdf) |
| **version** | { `vYYYYMMDD` }  | (e.g. `v20231117` ) |
---
---

### PREVIOUS CORDEX-CMIP5 ACS DRS

*Adopted from [CORDEX-CMIP5 archive specifications](http://is-enes-data.github.io/cordex_archive_specifications.pdf).*

#### Directory structure:  

/g/data/ia39/australian-climate-service/\<**status**\>/\<**activity**\>/\<**product**\>/\<**domain**\>/\<**RCM-institution**\>/\<**GCM-model-name**\>/\<**experiment-name**\>/\<**ensemble-member**\>/\<**RCM-model-name**\>/\<**RCM-version-ID**\>/\<**frequency-or-category**\>/\<**variable-name**>

#### Filenaming:  

\<**variable-name**\>\_\<**domain**\>\_\<**GCM-model-name**\>\_\<**experiment-name**\>\_\<**ensemble-member**\>\_\<**RCM-model-name**\>\_\<**RCM-version-id**\>\_\<**frequency-or-category**\>[\_\<**StartTime-EndTime**\>].nc
  
#### Controlled Vocabulary:

| **key** = | [*restriction*:] { item1 item2 ... }  | notes |
| ------------ | ------------ | --------- |
| **status** | { `test-data`, `staged`, `release` }  | |
| **activity** | { `CORDEX-CMIP6`, `ACS-DOWNSCALING`, `ACS-BARRA2` }  | `CORDEX-CMIP6` can include additional grids that are not required by the CORDEX initiative. |
| **product** | { `output`, `bias-adjusted-output`, `indices`, `bias-adjusted-indices` }  | |
| **domain** | format = \<**region**\>-\<**grid**> <br /> { `AUS-11`, `AUS-15`, `AUS-17i`, `AUS-22`, `AUS-r005`, `GLOBAL-gn` }  | `AUS-15` is a CORDEX-Australasia example. <br /> `AUS-r005` is a AGCD indices example. <br /> `GLOBAL-gn` is a global climate model example where `gn` is the CMIP6 native grid abbreviation. |
|  **RCM-institution** | { `BOM`, `CSIRO`, `none` } |  |
|**GCM-model-name** | format = \<**institution_id**\>-\<**source_id**> <br/>  | (e.g. `CSIRO-ARCCSS-ACCESS-CM2`) <br/> Refer to [CMIP6 CV](https://github.com/WCRP-CMIP/CMIP6_CVs/blob/master/CMIP6_source_id.json) for valid institution and source names. |
| **experiment-name** | *CMIP6*: { `historical`, `ssp126`, `ssp245`, `ssp370`, `ssp585`  } <br/> *ERA5*: { `evaluation` }  | Use `historical` when driving with an observational dataset like `AGCD` or `BARRA2` |
| **ensemble-member** | { `r?i?p?f?`, `hres`, `eda`} | For CMIP6-driven simulations, use the ensemble string from the driving dataset (e.g. `r6i1p1f1`). <br/> `BARRA-R2` uses ERA5's HRES (deterministic) forcing while `BARRA-RE2` uses ERA5's EDA (ensemble of DA) forcing. |
| **RCM-model-name** | {  `BOM-BARPA-R`, `BOM-BARRA-R2`, `BOM-BARRA-RE2`, `CSIRO-CCAM-????`, `none` }  |
| **RCM-version-id** | { `v?`, `none`, `<RCMVersionID>-<BCname>-<OBSname>-<REFperiod>`} | (e.g. `v2`, `v1-ecdfm-AGCD-1985-2014`) TODO: Determine process for updating version when data is corrected / updated. |
| **frequency-or-category** | *output, bias-corrected-output*: { `mon`, `day`, `6hr`, `3hr`, `1hr`, `15min` } <br/> *indices, bias-corrected-indices*: { `climdex`, `fire`, `heat`, `coasts`, `tropical-cyclones`, ... } | There are categories for [climdex indices](https://www.climdex.org/learn/indices/) and also each of the ACS hazard teams.
| **variable-name** | *output*: see [CORDEX-CMIP6 Atmosphere Variable List](https://docs.google.com/spreadsheets/d/1qUauozwXkq7r1g-L4ALMIkCNINIhhCPx/edit#gid=1672965248) <br/> *indices*: see [climdex indices list](https://www.climdex.org/learn/indices/) <br/> *bias-adjusted-output, bias-adjusted-indices*: add 'Adjust' to end of output variable-name (e.g. pr -> prAdjust); see [CORDEX-Adjust DRS](http://is-enes-data.github.io/CORDEX_adjust_drs.pdf) |

---
---
### **ESCI**
*Adopted from [CORDEX-CMIP5 archive specifications](http://is-enes-data.github.io/cordex_archive_specifications.pdf).*  
See https://github.com/AusClimateService/ESCI-data-collection

### Directory structure:  

/g/data/ia39/australian-climate-service/\<**status**\>/\<**activity**\>/\<**product**\>/\<**domain**\>/\<**GCM-model-name**\>/\<**CMIP5-experiment-name**\>/\<**CMIP5-ensemble-member**\>/\<**RCM-model-name**\>/\<**RCM-version-ID**\>/\<**frequency**\>/\<**variable-name**>

### Filenaming:  

\<**variable-name**\>\_\<**domain**\>\_\<**GCM-model-name**\>\_\<**CMIP5-experiment-name**\>\_\<**CMIP5-ensemble-member**\>\_\<**RCM-institute-and-model-name**\>\_\<**RCM-version-id**\>\_\<**frequency**\>[\_\<**StartTime-EndTime**\>].nc
  
### Controlled Vocabulary:

| **key** = | [*restriction*:] { item1 item2 ... }  |
| ------------ | ------------ | 
| **activity** | { `ESCI` }  |
| **product** | { `output`, `bias-adjusted-output` } |
| **domain** | { `AUS-ESCI`, `AUS-ESCI-noWA` }  |
| **GCM-model-name** | { `CSIRO-BOM-ACCESS1-0`, `CCCMA-CanESM2`, `CNRM-CERFACS-CNRM-CM5`, `NOAA-GFDL-ESM2M`, `MIROC-MIROC5`, `NCC-NorESM1-M` }  |
| **CMIP5-experiment-name** | { `historical`, `rcp45`, `rcp85` } |
| **CMIP5-ensemble-member** | { `r?i?p?` } (e.g. `r1i1p1`) |
| **RCM-institute-and-model-name** | { `CSIRO-CCAM-????`, `BOM-BARPA-R`, `NSW-NARCliMJ`, `NSW-NARCliMK`, `none` }  |
| **RCM-version-id** | *output*: { `v?`, `none` } <br/> *bias-corrected-output*: { `v?-QME`, `none` }  |
| **frequency** | { `day`, `3hr`, `30min` } |
| **variable-name** | *output*: { `tasmax`, `tasmin`, `pr`, `ps`, `clt`, `dni`, `scfWindDir`, `WindDir150`, `WindDir250`, `Wind150`, `Wind250`, `sfcWind`, `tdry`, `tdew`, `hurs`, `ghi` } <br/> *bias-adjusted-output*: { `tasmaxAdjust`, `tasminAdjust`, `prAdjust`, `FFDI` } |

