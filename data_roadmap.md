# ACS Data Roadmap

Many ACS researchers working at CSIRO will be able to store data and code
in ACS-related projects on NCI (`xv83` and `ia39`).
Similar projects have been established for Bureau researchers
(`mn51` for general analysis, `tp28`/`hd50` for BARPA/BARRA compute and raw data storage).
This document contains our current plans for managing those spaces.

[**A schematic representation of this roadmap by activity**](schematics/ACS-WP2_data_activities_roadmap.png)  
This schematic represents the input datasets,
and resulting output datasets to indicate the flow of data between various activities in ACS Project 3, Work Package 2.
The numbers in square brackets refer to the data levels in the
[ACS data hierarchy](https://github.com/AusClimateService/AusClimateService/blob/main/technical_notes/data_hierarchy.md).

Below we define here a three level strucure of ACS projects on NCI:
- Level A: 'working space' (`xv83` or `mn51`) and 'modelling space' (`tp28` and `hd50`)
- Level B: 'shared data' (`ia39`)
- Level C: 'public data' (TBD; e.g. `pd00`).

## Level A spaces

### Working space (xv83 and mn51)

CSIRO (`xv83`) and Bureau (`mn51`) researchers and small teams can essentially 
do what they like in their own `users` or `projects` directory on `xv83`/`mn51`.
Access is restricted to ACS researchers and most of the general compute 
allocation for ACS would be associated with these projects.
In other words, these spaces are for general data processing and analysis.

The desired directory structure of `xv83` is as follows:

```
xv83/
├── datasets/
|   ├── agcd-csiro
|   ├── dcfp
|   |   ├── CAFE60v1/
|   |   ├── CAFE-f5/
|   |   └── CAFE-f6/
├── users/
|   ├── abc123
|   ├── efg456
|   └── etc
```


### Modelling space (tp28 and hd50)

The compute and storage (of raw model output) allocations for
BARPA and BARRA are associated with `tp28` and `hd50` respectively.


## Level B spaces

### Shared data (ia39)

The `ia39` project is a place to share data among researchers working with ACS-related material.
For example, this might include a dataset that needs to be used by ACS researchers
even though it hasn't been formally published yet (e.g. CAFE-f6),
a reanalysis dataset downloaded and regridded for easy use (e.g. JRA-55),
or processed data that needs to be shared.
Given the broader audience using the data,
there needs to be some standards and guidelines to ensure usability,
transparency and reproducibility.
These standards differ depending on the type of dataset. 

Authoritative datasets:
- Description: An authoritative dataset is the original/source version of a dataset.
  For instance, the CMORised output from a model run, bias-correction process, or observing platform.
  Authoritative datasets will have the highest contraints applied with respect to standardisation and documentation.
- Requirements: [`data_standards.md`](data_standards.md)
- Location: `/g/data/ia39/australian-climate-service/`

Replica datasets: 
- Description: Many analyses conducted for the ACS will involve authoritative datasets
  that aren't already available on NCI (e.g. a global reanalysis).
  If there isn't a natural home elsewhere on NCI,
  it may be necessary to download a (partial or complete) replica
  of such a dataset and store it in `ia39`
  as part of the [Australian Community Reference Climate Data Collection](https://github.com/aus-ref-clim-data-nci).
- Requirements: There's a [documentation page](https://aus-ref-clim-data-nci.github.io/aus-ref-clim-data-nci/collection/howto.html#add-a-new-dataset)
  that describes the documentation requirements for a dataset to be part of the Reference Climate Data Collection.
- Location: `/g/data/ia39/aus-ref-clim-data-nci/`

Processed data:
- Description: While it isn't always necessary to store and share processed data
  (because if you make the code and raw/original data available the processed data can be recreated),
  it many cases it can be useful.  
  Examples of shared processed data might be simple manipulations of authoritative datasets
  to achieve a desired grid resolution, temporal frequency or file format,
  through to more complex processing to calculate a statistical quantity or climate diagnostic.
  While the simple manipulations are likely to only be of use to other researchers within the ACS,
  the complex products might be made available to stakeholders and/or the public.
- Requirements: [`data_standards.md`](data_standards.md)
- Location: `/g/data/ia39/australian-climate-service/`


## Level C spaces

### Public data (pd00)

`pd00` projects (we will probably end up with more than one) would be official NCI
[data collections](https://opus.nci.org.au/display/NDP/NCI+Data+Collections+and+Publishing).

A listing on the [NCI data catalogue](https://geonetwork.nci.org.au) requires the authors to provide
a bunch of detail about the dataset (data description, contact information, license, etc)
for the public catalogue entry.
Upon publication the dataset is issued with a DOI.

These datasets might also have an entry in the
[CSIRO Data Access Portal](https://data.csiro.au/collections).

If the dataset has undergone significant post-processing
then the same code, environment and data processing
requirements that apply to post-processed data in `ia39` should apply in `pd00` too.
