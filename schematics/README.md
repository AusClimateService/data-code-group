# Data schematics of proposed workflows and data structures

### [A schematic representation of the data roadmap by activity](ACS-WP2_data_activities_roadmap.png)  
This schematic representation of the [ACS data roadmap](../main/data_roadmap.md) indicates the flow of data between various activities in ACS Project 3, Work Package 2, including the input datasets and resulting output datasets. The numbers in square brackets refer to the data levels in the [ACS data hierarchy](https://github.com/AusClimateService/AusClimateService/blob/main/technical_notes/data_hierarchy.md).

### [A proposed operational workflow](ACS-WP2_dataflow-processes.png)  
This schematic presents a proposed operational workflow of data products, from RCM simulation, through bias correction, and into the ACS DRS (Data Reference Syntax; a controlled vocabulary, directory structure and filenaming convention) which all ACS data products will adhere to (see below). The 'levels' refer to those of the [ACS data hierarchy](https://github.com/AusClimateService/AusClimateService/blob/main/technical_notes/data_hierarchy.md).

### [An example of the various data products in the proposed ACS DRS](ACS_DRS_example.png)  
This diagram presents an example structure for the storage and naming scheme for the data from an RCM simulation. The ACS DRS, of which this is an example, covers model output (adopted from CORDEX), bias adjusted model output (adopted from CORDEX-Adjust), a standard verification/evaluation procedure (e.g. creation of bias maps, calculation of added value), and a suite of extremes & hazard indices required for ACS. The later two are yet to be defined in detail.
We intend to use the [Axiom](https://github.com/AusClimateService/axiom) software package to conform all data to this DRS and related controlled vocabulary (Axiom is currently operational for conforming data to the CORDEX DRS).  
A longer description of this DRS and is contained in the [ACS data standards](data_standards.md).
