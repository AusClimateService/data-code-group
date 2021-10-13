# Code Roadmap

This discussion paper attempts to descibe how we might go about
managing the code underpinning the data and information that comes out of
Project 2 of the [Australian Climate Service](https://www.acs.gov.au/) (ACS).
It has been drafted by Work Package 4,
which has been tasked with monitoring the quality and consistency of the outputs from Work Packages 1-3.

Much of the work in ACS Project 2 will involve taking an authoritative dataset
(e.g. the original data from a BARRA, BARPA, or CCAM run) and processing it to
produce data files or images that are shared with other ACS researchers and/or clients. 

There are essentially two main principles we want to follow in relation to processed files:
1. Make the associated code available
2. Shared code for common tasks

## 1. Making code available

The `code/` directory associated with a given collection of processed files
should include everything needed to reproduce those files.
This means providing the: 
1. **Code:** A copy of all the code written/used to produce the files (e.g. python scripts, jupyter notebooks, R files, etc)
2. **Environment:** Details of the software environment that the code was executed in
(e.g. a conda `environment.yml` or `requirements.txt` file listing the installed libraries)
3. **Data processing steps:** Details of how (e.g. in what order) the code was executed to produce each processed file
(e.g. a `Makefile` or `README`)

Provenance information can also be included in the metadata of the processed files,
so that a record of how they were created exists even if they become separated from
the associated `code/` directory (see Appendix 1).

Ideally the `code/` directory should be a git repository that is hosted in the
[ACS GitHub organisation](https://github.com/AusClimateService) (Appendix 2)
so there's a place that users can submit issues and ask questions about the processed data.

As an example, AGCD data has been processed (see `/g/data/xv83/dbi599/agcd`) and the
`code/` directory is a git repository hosted at:
https://github.com/AusClimateService/agcd 

Before processed files are made available to other ACS researchers and/or clients,
the associated code will need to undergo peer review (Appendix 3).

For some processed files it might be desirable to go one step further and formally publish
the code (Appendix 4).


## 2. Shared code for common tasks

In some instances the same data processing will be conducted across the ACS Project 2 Work Packages (WPs).
For instance, an index of extreme fire weather might be calculated using BARRA2 (Work Package 1)
and CCAM data (Work Package 2).
In these cases we should try and use the same code to process both datasets.
Work Package 4 will provide programming support for the development and running
of shared code for common tasks.


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

### Appendix 3: Code review

There needs to be processes in place to ensure the quality/reliability of the code
used to produce the processed files in ACS Project 2.

Starting out, the review criteria could be as simple as follows:

1. Has the code, along with details of the software environment and data processing steps,
   been archived in an online repository that can be accessed by
   the target audience (e.g. a public repository in the ACS GitHub organisation)?
2. Would someone familiar with the programming language/s used be able to re-run the analysis?
3. Would someone unfamiliar with the programming language/s used be able to broadly understand
   how the analysis was conducted?
4. Does the code need to be published with a DOI? (Appendix 4)
   
Downstream users of the associated data could conduct the review if appropriate,
or else Work Package 4 can provide support for code review.
   
### Appendix 4: Publication

Hosting code on GitHub is ideal for collaborative code development,
but not for persistent long term storage of the precise version of the code
used to produce a given output (e.g. a journal paper, data product or stakeholder report).
The owner of the GitHub repository might change the name of the repo
(thus breaking the original URL)
or could even remove the repository altogether.
The solution is to publish the code with a platform
that is certified to issue DOIs
(you can't get DOI certification unless you guarantee persistent long term access).
Some institutions have their own platform
(e.g. the [CSIRO Data Access Portal](https://data.csiro.au/collections/)),
otherwise [Zenodo](https://zenodo.org/) and [Figshare](https://figshare.com/)
are two generic (and free) platforms that are widely used by the research community.

Thanks to [GitHub/Zenodo integration](https://guides.github.com/activities/citable-code/),
the code publication process can be very easy.
Once you're ready to publish your paper / data product
you tag a formal version of your GitHub repository,
and then with the click of a button send that tagged version to Zenodo.
The ARC Centre of Excellence for Climate Extremes has created a
[Zenodo community](https://zenodo.org/communities/arc-coe-clex/)
to keep all their published code in the one place.
We could do the same for ACS.

> **What to publish?**
> 
> For full transparancy,
> it's often a good idea to publish your command logs (from Step 2)
> and the details of your software environment along with the code you've written.
> [Chapter 13.2](https://merely-useful.tech/py-rse/provenance.html#provenance-code)
> of *Research Software Engineering in Python* explains in detail.
