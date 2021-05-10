## Provenance

While the command log approach to data provenance adopted by
[NCO](http://nco.sourceforge.net/),
[CDO](https://code.mpimet.mpg.de/projects/cdo),
[`cmdline_provenance`](https://cmdline-provenance.readthedocs.io/en/latest/),
[`xclim`](https://xclim.readthedocs.io/en/latest/api.html?highlight=history#xclim.core.formatting.update_history),
and others
does the job,
the raw text format is difficult to parse by eye (especially for non-experts)
and the logs can get quite long if multiple input files are involved.

In recent years, there has been growing interest in using the 
the [Provenance Data Model](https://www.w3.org/TR/prov-primer/) (PROV) from the World Wide Web Consortium (W3C)
to capture the provenance of climate data products.
It defines a core data model (PROV-DM) for building representations of the entities, people and processes
involved in producing a piece of data or thing in the world,
along with corresponding serialisations (e.g., PROV-JSON, PROV-XML, PROV-O).

The [`prov`](https://prov.readthedocs.io/en/latest/) Python library supports
PROV-O, PROV-XML, PROV-JSON import/export.
There's a good [tutorial](https://nbviewer.jupyter.org/github/trungdong/notebooks/blob/master/PROV%20Tutorial.ipynb)
on how to use it.

A PROV document consists of *agents*, *activities* and *entities* that are all connected by *relations*.
In order to label these things, various URIs and namespaces are used.
For example, the `rook` package (which allows remote access to climate data)
[describes in detail](https://rook-wps.readthedocs.io/en/latest/prov.html) how they decide on labels.
[ESMValTool](https://docs.esmvaltool.org/en/latest/community/diagnostic.html#recording-provenance)
also outputs PROV-XML files.

Rather than create a labelling system in isolation,
some groups have published their domain-specific extensions
to the PROV standards for describing climate products. 
For instance, METACLIP (see their
[website](http://www.metaclip.org/), 
[flyer](https://predictia.es/en/news/metaclip-climate-metadata-provenance) and
[paper](https://www.sciencedirect.com/science/article/pii/S1364815218305036))
was initially developed in the project QA4Seas (framed in the Copernicus Climate Change Service)
as a way of dealing with seasonal forecast product provenance description.
That project also provides a website for visualising workflows.
The developers work in R,
so there isn't a Python implementation as yet.
There are similiar/competing vocabularies for describing geoscientific outputs
(e.g. [Zhang et al., 2020](https://www.sciencedirect.com/science/article/pii/S0098300419306120))
but it's fair to say none have widespread adoption at this stage.

### Implementing a provenance system for ACS

https://provenance.readthedocs.io/en/latest/  
https://github.com/bmabey/provenance/issues/59  
https://github.com/roocs/rook/blob/master/rook/provenance.py  
http://cfconventions.org/Meetings/2020-workshop/Metadata-handling-provenance-discussion-notes.pdf  

### Definitons

- An *entity* is a physical, digital, conceptual, or other kind of thing with some fixed aspects; entities may be real or imaginary.
- An *activity* is something that occurs over a period of time and acts upon or with entities; it may include consuming, processing, transforming, modifying, relocating, using, or generating entities.
- An *agent* is something that bears some form of responsibility for an activity taking place, for the existence of an entity, or for another agent’s activity.
- A *Uniform Resource Identifier (URI)* is a unique sequence of characters that identifies a logical or physical resource used by web technologies. URIs may be used to identify anything, including real-world objects, such as people and places, concepts, or information resources such as web pages and books.
