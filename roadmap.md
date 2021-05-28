# Code Roadmap

This discussion paper attempts to descibe how we might go about
managing the code that underpins the data and information the
[Australian Climate Service](https://www.acs.gov.au/) (ACS) makes available to end-users. 

## Step 1: Get all (or at least most of) our code in one place

As it currently stands,
the code associated with ACS is spread across
many different teams and individuals across a number of institutions.
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
(i.e. only members of the organisation will be able to see them)
and you can even change your settings so that your membership to the ACS organisation itself 
is only visible to other members of the organisation.

## Step 2: Provenance tracking

Once we've got our code in one place,
we need to know how that code was used to produce the products we provide to end-users.
In other words,
every data and image file needs to come with a log of all the commands/code
that were run to produce that file.

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
> for learning how to append and access metadata for different file formats.
>
> We will continue to update and improve the package and lesson materials to fit the needs of the ACS project
> and are happy to work with others to help write similar packages in other languages.

While command logs are an adequate solution to provenace tracking for those working closely with project code,
they are difficult to decipher for most project clients and managers.
An increasingly popular solution to this issue is the semantic web.
It can allow for the visualisation of data processing workflows (e.g. [METACLIP](http://www.metaclip.org/))
and also for searching/querying project metadata.
There would be a bit of work involved in figuring out precisely how to implement semantic web provenance tracking across the ACS,
so at the moment this is an idea that is being actively explored but has not yet been committed to.
There's some extended notes on the topic at
[provenance.md](https://github.com/AusClimateService/code-roadmap/blob/main/provenance.md).

## Step 3: Publication

Hosting code on GitHub is ideal for collaborative code development,
but not for persistent long term storage of the precise version of the code
used to produce a given output (e.g. a journal paper, data product or stakeholder report).
The owner of the GitHub repository might change the name of the repo
(thus breaking the original URL)
or could even remove the repository altogether.
The solution is to publish the code with a platform like
[Zenodo](https://zenodo.org/) or [Figshare](https://figshare.com/),
which are certified to issue DOIs
(you can't get DOI certification unless you guarantee persistent long term access).

Thanks to [GitHub/Zenodo integration](https://guides.github.com/activities/citable-code/),
the code publication process is very easy.
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

## Step 4: Quality control

During the initial 6-month showcase phase of ACS,
we should expect that everyone hosts their code with the ACS GitHub organisation
and that a number of ACS scientists put their hand up
to start incorporating provenance tracking (via command logs) into their ACS workflows.
Once ACS starts delivering products that are used to make real decisions
(i.e. beyond the initial 6-month period),
provenance tracking (with Zenodo integration) alone isn't enough.
There also needs to be processes in place to ensure the quality/reliability of the code we use
(and the consistency of the metadata associated with the data files we produce).
Different products might require different levels of quality control
(e.g. [Harrison et al, 2021](https://doi.org/10.5281/zenodo.4761866)),
but in general for products that we're producing/reproducing regularly
(i.e. operationalised as opposed to one-off products)
we'll need to adopt practices such as
continuous integration to run unit tests,
formal code review for all changes to the code base,
adoption of widely used file conventions
(e.g. CF-compliance via tools like [CMOR](https://cmor.llnl.gov/)), etc.
Once there's a clearer picture of what products we'll be producing (and for who),
as a team we can decide exactly what quality control measures we want to put in place.
In the meantime,
we should be on the look out for sub-projects within ACS
that could start to implement quality control measures to help guide
our decisions regarding standards to implement across the board.
