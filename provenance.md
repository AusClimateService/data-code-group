## Semantic web for code provenance?

The [Semantic Web](https://en.wikipedia.org/wiki/Semantic_Web) is an extension of the World Wide Web,
through standards set by the World Wide Web Consortium (W3C).
The goal of the Semantic Web is to make internet data machine-readable. 

The Semantic Web is built on top of two main pillars:
the [RDF](https://www.w3.org/TR/2004/REC-rdf-primer-20040210/) (Resource Description Framework) data model
for building representations of the entities, people and processes
involved in producing a piece of data or thing in the world,
and the OWL standard for storing domain-specific vocabularies (or ontologies). 
(There's also a SPARQL query language for searching the metadata once you've created it.)

In recent years, there has been a move towards tracking weather/climate information
with Semantic Web technology (e.g. [Ma, et al](https://www.nature.com/articles/nclimate2141)).
The [Global Change Information System](https://data.globalchange.gov/) uses the technology to link together
all the assessments, reports, and tools produced by the US Global Change Research Program,
and it has also been used to publish a number of linked datasets, including ACORN-SAT
([Lefort et al, 2016](http://www.semantic-web-journal.net/content/acorn-sat-linked-climate-dataset-0)). 

More recently,
Semantic Web technology has been used to record the actual data processing steps
(i.e. down to the precise code/commands)
involved in producing climate products (i.e. maps, plots or any other climate research outcome stored in a file).
While Python packages such as [`rook`](https://rook-wps.readthedocs.io/en/latest/prov.html) and
[ESMValTool](https://docs.esmvaltool.org/en/latest/community/diagnostic.html#recording-provenance)
simply define their own bespoke/narrow adaptation of the [PROV](https://www.w3.org/TR/prov-primer/) / RDF
data model to suit their own needs,
there have been attempts to define a broad/comprehensive ontology for climate products
(e.g. [Bedia et al 2019](https://www.sciencedirect.com/science/article/pii/S1364815218305036),
[Zhang et al., 2020](https://www.sciencedirect.com/science/article/pii/S0098300419306120)).

The most widely used ontology is [METACLIP](http://metaclip.org/)
(METAdata for CLImate Products; see their
[website](http://www.metaclip.org/), 
[flyer](https://predictia.es/en/news/metaclip-climate-metadata-provenance) and
[paper](https://www.sciencedirect.com/science/article/pii/S1364815218305036)),
which was initially developed for the Copernicus
[QA4Seas](https://climate.copernicus.eu/quality-assurance-multi-model-seasonal-forecast-products)
seasonal forecasting project and is now also being used for the
[VALUE](http://www.value-cost.eu/) downscaling initiative.
At the METACLIP website you can interactively view the metadata for a given product.
The graphical representation is probably sufficient for many users,
but experts requiring a complex technical provenance description
can click to see more in the sidebar.
The METACLIP developers work in R
and have integrated their approach with the [climate4R](https://github.com/SantanderMetGroup/climate4R) package.
There isn't a Python implementation as yet,
but presumably one could implement the ontology using [`rdflib`](https://rdflib.readthedocs.io/en/stable/)
(see some tentative attempts [here](https://github.com/ClimResAus/code-roadmap/blob/main/metaclip.ipynb)).

In response to these developments,
those responsible for the [CF Conventions](http://cfconventions.org/index.html)
are discussing how these new ideas can be used/incorporated to improve metadata standards
(e.g. see [these notes](http://cfconventions.org/Meetings/2020-workshop/Metadata-handling-provenance-discussion-notes.pdf)
from the [2020 CF Workshop](http://cfconventions.org/Meetings/2020-workshop/Metadata-handling-provenance-discussion-notes.pdf)).  

