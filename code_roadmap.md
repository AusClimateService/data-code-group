# Code Roadmap

This discussion paper attempts to descibe how we might go about
managing the code underpinning the data and information that comes out of
Project 2 of the [Australian Climate Service](https://www.acs.gov.au/) (ACS).
It has been drafted by the "Data and Code Group" within Work Package 4,
which is the package responsible for monitoring the quality and consistency
of the outputs from Work Packages 1-3.

## Processed files

Much of the work in ACS Project 2 will involve taking an authoritative dataset
(e.g. the original data from a BARRA, BARPA, or CCAM run) and processing it to
produce data files or images that are shared with other ACS researchers and/or clients. 

A collection of shared processed files should have an associated code directory
(let's call it `code/` for now) that includes everything needed to reproduce those files.
This means providing the: 
1. **Code:** A copy of all the code written/used to produce the files (e.g. python scripts, jupyter notebooks, R files, etc)
2. **Environment:** Details of the software environment that the code was executed in
(e.g. a conda `environment.yml` or `requirements.txt` file listing the installed libraries)
3. **Data processing steps:** Details of how (e.g. in what order) the code was executed to produce each processed file
(e.g. a `Makefile` or `README`)

Provenance information can also be included in the metadata of the processed files,
so that a record of how they were created exists even if they become separated from
the associated `code/` directory (see Appendix 1).

Ideally, the `code/` directory should be a git repository that is hosted in the
[ACS GitHub organisation](https://github.com/AusClimateService) (Appendix 2)
so there's a place that users can submit issues and ask questions about the processed files.
At the point that a collection of shared processed files is modified or made available for the first time,
a [code release](https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository)
will be tagged in GitHub and if the collection is for public use then that release
will be published (i.e. to obtain a DOI) to the
[ACS community on Zenodo](https://zenodo.org/communities/ausclimateservice/) (Appendix 3). 

As an example, AGCD data has been processed (see `/g/data/ia39/agcd/post-processed/`) and the
`code/` directory is a git repository hosted at:
https://github.com/AusClimateService/agcd 

Before processed files are made available to other ACS researchers and/or clients,
the files and code will undergo peer review (see [`reivew.md`](review.md))
to ensure the code and data standards have been followed.

## Authoritative data

Unlike a processed dataet, an authoritative dataset is the original/source version.
For instance, the raw output (or raw with a minimal amount of post-processing)
from a model run or observing platform.
It is more challenging to make the associated code and data processing steps available
(and easily interpretable) for an authoritative dataset
(e.g. it would be difficult to make the entire BARRA or CCAM codebase available
with an easy to follow description of how each dataset was created)
so no definitive code guidelines/requirements for authoritative datasets
are being proposed at this stage.

## Shared code

It is possible that a small library of common code will be hosted
and maintained by the Data and Code Group
(e.g. for the calculation of complex hazard indicators, data standard checking, standard plotting style)
but it is unlikely to be very large or comprehensive.
In almost all instances individual groups within each Work Package will be doing their
own code development for data processing. 

We could explore the possibility of more systematic code sharing down the track,
but for now the focus is simply on getting individual groups comfortable with making
the details of code, environment and data processing steps available. 

## Appendices

### Appendix 1: Provenance tracking

The metadata associated with processed files can be edited to include
a log of all the commands/code that were run to produce that file.

The simplest way to do this is to follow the lead of the widely-used
[NCO](http://nco.sourceforge.net/) and [CDO](https://code.mpimet.mpg.de/projects/cdo) command line tools,
which insert a record of what was executed at the command line
into the history attribute of the output netCDF file.
For example, here's the global history attribute of an ACCESS-ESM1-5 CMIP6 data file
after CDO has been used to extract the 2010-2014 time period 
and NCO has been used to delete a second redundant history attribute
attached to the precipitation variable in that file:

```text
Tue Jan 12 14:50:35 2021: ncatted -O -a history,pr,d,, pr_Amon_ACCESS-ESM1-5_historical_r1i1p1f1_gn_201001-201412.nc
Tue Jan 12 14:48:10 2021: cdo seldate,2010-01-01,2014-12-31 /g/data/fs38/publications/CMIP6/CMIP/CSIRO/ACCESS-ESM1-5/historical/r1i1p1f1/Amon/pr/gn/latest/pr_Amon_ACCESS-ESM1-5_historical_r1i1p1f1_gn_185001-201412.nc pr_Amon_ACCESS-ESM1-5_historical_r1i1p1f1_gn_201001-201412.nc
2019-11-15T04:32:57Z ; CMOR rewrote data to be consistent with CMIP6, CF-1.7 CMIP-6.2 and CF standards.
```

If we write and run a Python script (e.g. called `plot_precipitation_climatology.py`) to plot the 2010-2014 SON climatology,
we need to update the command log and append it to the metadata of the PNG image file:

```text
Mon Feb 08 09:45:17 2021: plot_precipitation_climatology.py pr_Amon_ACCESS-ESM1-5_historical_r1i1p1f1_gn_201001-201412.nc SON pr_Amon_ACCESS-ESM1-5_historical_r1i1p1f1_gn_201001-201412-SON-clim.png (https://github.com/DamienIrving/ocean-analysis)
Tue Jan 12 14:50:35 2021: ncatted -O -a history,pr,d,, pr_Amon_ACCESS-ESM1-5_historical_r1i1p1f1_gn_201001-201412.nc
Tue Jan 12 14:48:10 2021: cdo seldate,2010-01-01,2014-12-31 /g/data/fs38/publications/CMIP6/CMIP/CSIRO/ACCESS-ESM1-5/historical/r1i1p1f1/Amon/pr/gn/latest/pr_Amon_ACCESS-ESM1-5_historical_r1i1p1f1_gn_185001-201412.nc pr_Amon_ACCESS-ESM1-5_historical_r1i1p1f1_gn_201001-201412.nc
2019-11-15T04:32:57Z ; CMOR rewrote data to be consistent with CMIP6, CF-1.7 CMIP-6.2 and CF standards.
```

The new entry also includes a GitHub URL to indicate where to access our script.

> **How to create and update your own command logs**
>
> Damien Irving (with the assistance of Mitchell Black) has developed
> a Python library called [cmdline-provenance](https://cmdline-provenance.readthedocs.io/en/latest/) 
> that can be used to simplify the process of creating and updating command logs.
> There are also associated [lesson materials](https://carpentrieslab.github.io/python-aos-lesson/09-provenance/index.html)
> for learning how to append and access metadata for different data and image file formats.
>
> We will continue to update and improve the package and lesson materials to fit the needs of the ACS project
> and are happy to work with others to help write similar packages in other languages.

### Appendix 2: The ACS GitHub organisation

While it probably won't be possible to have literally all our code in one place
(e.g. some code might be primarily used for other projects/collaborations),
the default should be for all ACS-related code to be hosted within the same GitHub organisation:  
https://github.com/AusClimateService

A GitHub organisation is essentially an umbrella under which to host a bunch of related GitHub repositories.
Having all our code in one place means that we can easily see what each other is working on,
which will facilitate collaboration and consistency across teams and institutions.
It also means we have a single place to point to if someone asks where the code is for ACS.

> **Moving code to a GitHub organisation**
>
> The process involved in moving code to a GitHub organisation
> depends on how that code is currently being managed:
> - If you've got an existing GitHub repository for your ACS-related work,
> you can transfer that GitHub repository to the new organisation following
> [these instructions](https://docs.github.com/en/github/administering-a-repository/transferring-a-repository)
> - If your local git repository isn't up on GitHub yet,
> you can create a new repository within the ACS organisation
> and then add that GitHub repository as a remote
> following [these instructions](https://docs.github.com/en/github/getting-started-with-github/managing-remote-repositories)

For those worried about privacy,
you can make your repositories within the ACS organisation private
(i.e. only members of the organisation will be able to see them).
You can even change your settings so that your membership to the ACS organisation itself 
is only visible to other members of the organisation.
   
### Appendix 3: Code publication

Hosting code on GitHub is ideal for collaborative code development,
but not for persistent long term storage of the precise version of the code
used to produce a given output (e.g. a journal paper, data product or stakeholder report).
The owner of the GitHub repository might change the name of the repo
(thus breaking the original URL)
or could even remove the repository altogether.
The solution is to publish the code with a platform
that is certified to issue DOIs
(you can't get DOI certification unless you guarantee persistent long term access).

Thanks to [GitHub/Zenodo integration](https://guides.github.com/activities/citable-code/),
the code publication process can be very easy.
Once you're ready to share your processed files,
you tag a formal release of your code on GitHub,
and then with the click of a button send that tagged release to Zenodo.
The ARC Centre of Excellence for Climate Extremes has created a
[Zenodo community](https://zenodo.org/communities/arc-coe-clex/)
to keep all their published code in the one place.

We could do the same at: https://zenodo.org/communities/ausclimateservice/

> **What to publish?**
> 
> For full transparancy,
> it's often a good idea to publish your command logs (from Step 2)
> and the details of your software environment along with the code you've written.
> [Chapter 13.2](https://merely-useful.tech/py-rse/provenance.html#provenance-code)
> of *Research Software Engineering in Python* explains in detail.
