Many ACS researchers working at CSIRO will be able to store data and code in ACS-related projects on NCI
(`xv83` and `ia39` at the moment).
This document contains initial/draft thoughts on how we might manage those spaces.
To start the conversation,
here's a representation of how things might be organised,
using (mostly) the existing content in `xv83` as an example:

```
ia39/
├── admin/
├── AWAP/
│   ├── post-processed/
│   │   ├── code/
│   │   └── data/
├── CAFE60v1/
│   ├── authoritative/
│   │   ├── README
│   │   ├── code/
│   │   └── data/
├── CAFE-f5/
│   ├── authoritative/
│   │   ├── README
│   │   ├── code/
│   │   └── data/
├── CAFE-f6/
│   ├── authoritative/
│   │   ├── README
│   │   ├── code/
│   │   └── data/
├── CCI_fire/
│   ├── replica/
│   │   ├── README
│   │   └── *.nc
├── HadISST/
│   ├── post-processed/
│   │   ├── code/
│   │   └── data/
└── JRA-55/
    └── post-processed/
        ├── code/ 
        └── data/

xv83/
├── projects/
│   ├── ACS
│   │   ├── work_package_1/
│   │   ├── work_package_2/
│   │   ├── work_package_3/
│   │   ├── work_package_4/
│   │   └── work_package_5/
│   ├── ESCI
│   │   ├── code/
│   │   └── data/
└── users/
    ├── bxn599/
    ├── cm2704/
    ├── dbi599/
    ├── dr6273/
    ├── ds0092/
    ├── kd7073/
    ├── mxt599/
    └── tm4888/

pd00/
├── dataset1/
└── dataset2/
```
What's described above is essentially a three level strucure that goes from 'working space' (`xv83`)
to 'shared data' (`ia39`) to 'public data' (`pd00`; placeholder name because it doesn't exist yet).

## Working space (xv83)

Researchers and small teams can essentially do what they like in their own `users` or `projects` directory on `xv83`.
Access to `xv83` would be restricted to ACS researchers and
most of the compute allocation for ACS would be associated with `xv83`.

## Shared data (ia39)

The `ia39` project is a place to share data among researchers working with ACS-related material.
For example, this might include a dataset that needs to be used by ACS researchers
even though it hasn't been formally published yet (e.g. CAFE-f6),
a reanalysis dataset downloaded and regridded for easy use (e.g. JRA-55),
or processed data that needs to be shared.
Given the broader audience using the data,
there needs to be some standards and guidelines to ensure usability,
transparency and reproducibility.
These standards differ depending on the type of dataset: 

### Authoritative datasets

**Description**:
An authoritative dataset is the original/source version of a dataset.
For instance, the raw output (or raw with a minimal amount of post-processing)
from a model run or observing platform.

**Requirements**:
A README file that describes the dataset in detail.
The data in `ia39` isn't published on the [NCI data catalogue](https://geonetwork.nci.org.au),
but we could require that most of the information required for a catalogue entry
is included in the README?
An outline of data standards for ACS, the requirements of a dataset
to be included in ia39, has been drafted: [`data_standards.md`](data_standards.md). 
More information will be added as consultation by the Data & Code Group continues.

### Replica datasets 

**Description**:
Many analyses conducted for the ACS will involve authoritative datasets
that aren't already available on NCI (e.g. a global reanalysis).
If there isn't a natural home elsewhere on NCI,
it may be necessary to download a (partial or complete) replica
of such a dataset and store it in `ia39`.

**Requirements**:
A README file explaining when, how and what was downloaded from the authoritative source,
the maintenance plan (i.e. is this replica static or is it being regularly updated and how),
and links to dataset documentation. 

### Post processed data  

**Description**:
While it isn't always necessary to store and share processed data
(because if you make the code and raw/original data available the processed data can be recreated),
it many cases it can be useful.
Examples of shared processed data might be simple manipulations of authoritative datasets
to achieve a desired grid resolution, temporal frequency or file format,
through to more complex processing to calculate a statistical quantity or climate diagnostic.
While the simple manipulations are likely to only be of use to other researchers within the ACS,
the complex products might be made available to stakeholders and/or the public. 

**Requirements**:
See [`code_roadmap.md`](code_roadmap.md)

## Public data (pd00)

The `pd00` project would be the official ACS
[data collection](https://opus.nci.org.au/display/NDP/NCI+Data+Collections+and+Publishing)
under which all our publicly available data would sit.
Each dataset would also have an entry in the
[CSIRO Data Access Portal](https://data.csiro.au/collections).

A listing on the [NCI data catalogue](https://geonetwork.nci.org.au) requires the authors to provide
a bunch of detail about the dataset (data description, contact information, license, etc)
for the public catalogue entry.
Upon publication the dataset is issued with a DOI.

If the dataset has undergone significant post-processing
then the same code, environment and data processing
requirements that apply to post-processed data in `ia39` should apply in `pd00` too.
