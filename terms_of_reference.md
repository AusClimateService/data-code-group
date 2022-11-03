## Data & Code Group - Terms of Reference

### Context

The Australian Climate Service (ACS) was established by the Australian Government in 2021
to support better planning and preparedness for climate and natural hazards,
and better response and recovery to disasters when they strike.
The ACS will connect and leverage the Commonwealth’s extensive climate and natural hazard information into a single national view.
The ACS is funding several programs of work to develop the data and platforms
that will provide government with intelligence relating to natural disasters
to aid in prevention, preparedness, emergency response, recovery, relief, and resilience. 
Program 3 of ACS is a collaboration between the Bureau of Meteorology and CSIRO Climate Science Centre
and will focus on developing natural hazard predictions and projections,
with a large focus on the preparation of climate and weather simulation data. 

It has become standard in climate modelling to publish model output data
in a standardised format with a common naming system and data structure,
and best practice to store and share code used for the generation of this data in version control systems.
Documentation, provenance, and accessibility are also a key part of data and software preparation to enable reuse and reproduction.
It is anticipated that 30-100 PB of raw data will be generated for ACS Program 3,
a large portion of which will require processing, management, documentation, and publication.
These will include primary/model datasets from models
(such as CORDEX simulations, coastal projections, and hazard modelling),
and secondary/derived datasets
(such as bias-adjusted data, hazard metrics and extremes indices).
While CORDEX has defined a Data Reference Syntax (DRS) for data to be published to the ESGF,
this only applies to a small subset of ACS products;
all other datasets will require tailored a DRS to be defined.
This will enable the seamless analysis and prediction set out as a key aim for ACS.
Additionally, there will be many pieces of code created in the project,
including post-processing tools, bias-adjustment software, and codes to calculate derived variables,
which require version control, publication and documentation.

### Scope

The primary role of the Data and Code Group is to ensure that all data and code produced by ACS Program 3 meets
establshed best practices in the climate science community and
any requirements for delivery into the ACS.   
This includes oversight and support of the following tasks:
-	The standardisation of model output and derived datasets
-	Code sharing, documentation, and publication
-	Data storage planning and provision

The following tasks are to be led and carried out by the Data and Code Group:
-	Management of associated NCI projects
-	Provision and management of code repositories
-	Data publication & documentation
-	Cataloguing of ACS datasets
-	Development of the ACS DRS for the various modelling and analysis activities
-	Development of software tools for file metadata standarisation, including user training
-	Support for ACS project members to understand and implement the DRS and data catalogues in their work

### Governance

The Data and Code Lead coordinates the activities of the Group.
This role reports to the Program 3 leads (Richard Matear, CSIRO, and David Jones, BoM).
Additional consultation will be required with the
CSIRO ACS coordinator (Mark Hemer),
CSIRO O&A Digital Lead (Chloe Mackallah, CSIRO),
the ACS Data Governance Framework Lead (Clare Richards, BoM) and
Program 3 Work Package leads.
Furthermore, the ACS Data Governance framework will provide general guidance and oversight
to the decisions of the Data and Code Group via its representatives from Program 3 (Chloe Mackallah, CSIRO, and Doerte Jakob, BoM).

### Licencing and availability of data and code

All data intended for external sharing must comply with FAIR principles of data management.
Data must be Findable (published with a DOI minted and registered in a climate catalogue),
Accessible (available via THREDDS, public cloud, or direct download),
Interoperable (uses netCDF4, and is organised into a structure and naming scheme that follows CF conventions and ACDD recommendations),
and Reusable (open license, and metadata that fully describes the origin, provenance, context, and structure of the data).
All data are to be licensed with CC-BY v4.0.

All software (executables, python scripts, and Jupyter notebooks; excluding HPC job scripts, models, and codes sourced from outside ACS)
that are used to prepare final data products are to be version controlled
(preferably in a Data and Code Group supported repository),
with the MIT open-source software license applied (unless otherwise agreed upon),
and be published or catalogued with a persistent identifier (e.g., Zenodo, [CSIRO Data Access Portal](https://data.csiro.au/)).

### Member roles and responsibilities

There are a number of formal roles associated with the Data and Code Group.
Each role has core responsibilities that are expected to be completed by the appointees to those roles,
as well as desirable/extra responsibilities that could be performed by the appointees
(provided they are given extra FTE allocation)
or by others working on the ACS.

#### Data and Code Lead - 1 person

Core responsibilities (1/2 day per fortnight; 0.05 FTE)
- Schedule and chair regular Data and Code Group meetings
- Liaise with ACS staff and management on behalf of the Data and Code Group

(The Data and Code Lead will probably also take on one of the roles below.)

#### Data Custodian - 2 people across CSIRO/BoM

Core responsibilities (1 day per fortnight; 0.1 FTE per person):
- Maintain the [data roadmap](https://github.com/AusClimateService/data-code-group/blob/main/data_roadmap.md),
  which describes in broad terms how data produced by ACS Project 3 will be managed
  (e.g. data processing workflows, storage locations)
- Maintain the [data standards](https://github.com/AusClimateService/data-code-group/blob/main/data_standards.md),
  which describe standards for individual data files relating to file formats and metadata (e.g. DRSs and Controlled Vocabularies)
- Manage NCI project storage allocations
- Manage the ACS Project 3 datasets that are for sharing and publication (e.g. via NCI project [ia39](https://my.nci.org.au/mancini/project/ia39))
- Ensure appropriate licensing of ACS data products
- Report on storage usage to the Data and Code Lead
- Maintain documentation on currently available datasets

Desirable responsibilities:
- Build and maintain an ACS Project 3 data catalogue (e.g. using [Intake](https://intake.readthedocs.io/en/latest/))
  with accompanying documentation (e.g. example Jupyter notebooks)

#### Software Custodian - 2 people across CSIRO/BoM

Core responsibilities (1/2 day per fortnight; 0.05 FTE per person):
- Maintain the [code roadmap](https://github.com/AusClimateService/data-code-group/blob/main/code_roadmap.md),
  which describes in broad terms how the code produced by ACS Project 3 will be managed
- Manage the [ACS Program 3 GitHub Organisation](https://github.com/AusClimateService)
- Advise scientists about how to bring their code up to ACS standards
- Advise scientists on code publication as required (e.g. via the [CSIRO Data Access Portal](https://data.csiro.au/) or Zenodo)
- Coordinate code reviews as required

Desirable responsibilities:
- Assist scientists to get their code up to ACS standards
  (i.e. in addition to providing advice, this may involve writing code)*
- Perform code reviews as required

*This level of assistance would typically be reserved for software critical to the success of ACS Project 3
that needs to be used by many people across the project.

#### Software Engineer (Axiom) - 1 person

Core responsibilities (1/2 day per fortnight; 0.05 FTE):
- Maintain [Axiom](https://github.com/AusClimateService/axiom) (i.e. bug fixes, basic documentation)
  and related tools used for the CMORisation of published datasets
- Advise users of Axiom (e.g. answer simple usage questions)

Desirable responsibilities:
- Build new functionality into Axiom
- Develop detailed documentation (e.g. examples, tutorials)
- Assist users of Axiom (e.g. answer detailed questions), including providing training if required
