# Checklist for sharing ACS data in ia39

- Metadata: does your data contain the required metadata? (see [ACS Data Standards](https://github.com/AusClimateService/data-code-group/blob/main/data_standards.md))

- Documentation and README: there will need to be a README file along with your release data, that preferably points to documentation of the data, and links to any published papers.

- File system management & permissions: ACLs to set up correctly (globally readable, but with an ia39_w mask for writing). To confirm the best setup for this.

- Clarifying the DRS: we must do a final check to ensure that the CV in use is aligned with other models and as best with CORDEX as possible (noting that the CORDEX specifications don't exist yet for CMIP6).

- Advertising: will you be advertising the dataset widely/locally?

- Assigning a data custodian: who will be responsible for the ongoing management of this data, including requests, updates, etc?

- Intake catalogue: are your data catalogued in an intake-esm catalogue for ease of access and use?

- Post-processing code under version control: is the code and schemas used to generate the final datasets in the ACS Github, or otherwised version controlled?

- Licensing: does your data contain a license in the metadata? This should be CC-BY v4.0 unless otherwise agreed or directed by ACS leadership.
