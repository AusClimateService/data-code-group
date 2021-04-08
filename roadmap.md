# CaRSA Code Roadmap

This discussion paper attempts to descibe how we might go about
managing the code that underpins the data and information CaRSA makes available to end-users. 

## Step 1: Get all (or at least most of) our code in one place

As it currently stands,
the code associated with CaRSA is spread across
many different teams and individuals across a number of institutions.
While it probably won't be possible to have literally all our code in one place
(e.g. some code might be primarily used for other projects/collaborations),
the default should be for all CaRSA-related code to be hosted within the same GitHub organisation:  
https://github.com/ClimResAus

A GitHub organisation is essentially an umbrella under which to host a bunch of related GitHub repositories.
Having all our code in one place means that we can easily see what each other is working on,
which will facilitate collaboration and consistency across teams and institutions.
It also means we have a single place to point to if someone asks where the code is for CaRSA.

> **Moving code to a GitHub organisation**
>
> The process involved in moving code to a GitHub organisation
> depends on how that code is currently being managed:
> - If you've got an existing GitHub repository for your CaRSA-related work,
> you can transfer that GitHub repository to the new organisation following
> [these instructions](https://docs.github.com/en/github/administering-a-repository/transferring-a-repository)
> - If your local git repository isn't up on GitHub yet,
> you can create a new repository within the CaRSA organisation
> and then add that GitHub repository as a remote
> following [these instructions](https://docs.github.com/en/github/getting-started-with-github/managing-remote-repositories)

For those worried about privacy,
you can make your repositories within the CaRSA organisation private
(i.e. only members of the organisation will be able to see them)
and you can even change your settings so that your membership to the CaRSA organisation itself 
is only visible to other members of the organisation.

## Step 2: Provenance

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

The new entry also includes a GitHub URL to indicate where to access our script,
which could be replaced with a DOI if we published our code
(e.g. using [GitHub/Zenodo integration](https://guides.github.com/activities/citable-code/))
to ensure long term persistent access.

> **How to create and update your own command logs**
>
> Damien Irving (with the assistance of Mitchell Black) has developed
> a Python library called [cmdline-provenance](https://cmdline-provenance.readthedocs.io/en/latest/) 
> that can be used to simplify the process of creating and updating command logs.
> There are also associated [lesson materials](https://carpentrieslab.github.io/python-aos-lesson/09-provenance/index.html)
> for learning about how to append and access metadata for different file formats.
>
> We will continue to update and improve the package and lesson materials to fit the needs of the CaRSA project
> and are happy to explore the possibility of similar packages in other languages.
