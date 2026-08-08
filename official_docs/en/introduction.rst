Introduction
************

Why OpenBioMaps?
================

One of the major challenges in biodiversity research and nature conservation is not collecting observations in the field, but reliably documenting, managing, and using the data collected. Field observations need to be recorded in a structured way, stored securely, checked for errors, and made accessible for later analysis and use. When these tasks are handled through disconnected tools and manual processes, data management can become unnecessarily complicated and time-consuming.

OpenBioMaps was developed to address this problem. It connects field data collection with data storage, management, validation, visualisation, analysis, and access within a single, flexible data management framework.

For fieldworkers, this means that observations can be recorded and transferred into a structured database without extensive post-processing. For researchers and data managers, it means that data can be checked, organised, queried, analysed, and shared using a consistent system. The aim is not to replace the tools used by researchers, but to connect them into a coherent and reproducible workflow.

What is OpenBioMaps?
====================

OpenBioMaps is an open-source biodiversity data management system and framework developed in collaboration with conservation professionals and researchers. It is designed primarily for managing observations and associated data on living organisms, particularly in biodiversity research and nature conservation.

An OpenBioMaps installation provides a PostgreSQL-based data management environment that can be configured to the requirements of a particular project. The database structure, data entry interfaces, access rules, workflows, and data management processes can all be adapted to the needs of the project.

OpenBioMaps can be operated on an organisation's own server or used through a server maintained by a trusted partner. This makes it possible to establish a long-term data management environment without being dependent on a centrally controlled database or a single predefined data model.

Connecting data collection and data use
=======================================

A central principle of OpenBioMaps is that data collection should not be separated from subsequent data management and use.

A typical workflow may include:

* collecting observations in the field;
* uploading or entering observations into the database;
* validating and documenting the data;
* organising and managing the data within the project;
* querying and filtering the data;
* visualising and analysing the data using external tools such as QGIS or R;
* publishing or sharing selected data; and
* reusing the data for research, monitoring, conservation planning, or other purposes.

Because these activities are connected through a common data management environment, many operations that would otherwise require manual data transfer or repeated data processing can be automated. This reduces the risk of errors and allows fieldworkers and researchers to spend less time on administrative tasks.

OpenBioMaps is therefore not simply a database for storing observations. It provides a framework for building a complete and reproducible data management workflow around biodiversity data.

The OpenBioMaps approach
========================

The OpenBioMaps approach is based on several principles:

* **Flexibility:** projects can define their own database structures, data fields, workflows, and access rules.
* **Integration:** data can be accessed by and transferred to other systems and tools, including QGIS, R, and external databases.
* **Reproducibility:** queries and data processing can be documented, repeated, and cited.
* **Long-term data management:** data are stored in a structured database rather than being tied to individual spreadsheets or isolated files.
* **Automation:** validation, data transfer, and other repetitive operations can be automated to reduce manual work and errors.
* **Openness:** OpenBioMaps is based on open-source software and provides freely accessible community services.
* **Decentralisation:** databases can be operated by independent organisations without requiring central control of the data.
* **Community development:** the system is developed and maintained in collaboration with researchers, conservation professionals, and other users.

OpenBioMaps is intended to adapt to changing requirements rather than impose a fixed workflow on every project. A project can start with a relatively simple data structure and evolve as its monitoring programme, research questions, or data management requirements develop.


Main properties
===============
* Free and openly accessible OpenBioMaps services.
* Customisable database structures, data entry interfaces, workflows, and access rules.
* Web-based data upload in a variety of formats (ods, xls, xlsx, gpx, shp, csv, etc.).
* API access for querying and uploading data.
* Repeatable and citable queries.
* Persistent identifiers (DOIs) for databases and queries.
* Data export in various formats (shp, csv, gpx, json, etc.).
* Integration with R, QGIS, remote databases, and other external systems.
* Integration with field-based mobile data collection applications.
* Customisable data management interfaces.
* Links to external biodiversity databases and platforms such as GBIF and iNaturalist.


OpenBioMaps workflow
====================
The OpenBioMaps workflow connects field data collection, data management,
validation, analysis, publication, and reuse.

:doc:`OBM Workflow <../obm_workflow>`

:download:`Query scheme (pdf) <docs/query_scheme.pdf>` 
:download:`Query scheme (odp) <docs/query_scheme.odp>`

OpenBioMaps Consortium
======================

OpenBioMaps is developed and maintained by a consortium of research institutions, conservation organisations, and other partners. The consortium coordinates software development and maintains the community services.

:doc:`OpenBioMaps Consortium <consortium>`

:doc:`Getting started with OpenBioMaps <getting_started>`
