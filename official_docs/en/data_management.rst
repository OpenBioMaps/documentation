:author: Miklós Bán
:date: 2026-08-08


Data management
***************

Data management in OpenBioMaps covers the processes used to organise,
document, validate, maintain, process, and reuse biodiversity data
throughout their lifecycle.

The aim is to ensure that data remain understandable, reliable,
traceable, and usable beyond the original data collection activity.

OpenBioMaps provides tools for managing both the structure of the data
and the processes through which data are collected, checked, transformed,
queried, and used.

Database structure and metadata
===============================

OpenBioMaps stores data in structured database tables rather than in
independent files or spreadsheets.

The database structure defines what types of information can be stored
and how different types of information are related.

Metadata can be associated with tables and fields to describe their
meaning, content, and intended use. Good metadata are essential for
understanding and reusing data, particularly when a project is maintained
over a long period or by multiple people.

:ref:`Administrative settings: Database columns <database-columns>`

Data quality and validation
===========================

Data quality can be improved by checking data as they enter the system
and by applying validation rules during data management.

Depending on the project configuration, OpenBioMaps can check values,
required fields, relationships between data, spatial information, and
other project-specific constraints.

Validation can be performed during data entry or upload, as well as
during subsequent data processing.

* :doc:`Background jobs <../jobs>`
* :doc:`Modules <../modules>`

Data processing and harmonisation
=================================

Data collected from different sources may use different formats,
terminology, taxonomies, coordinate systems, or other conventions.

OpenBioMaps can be used as part of workflows that harmonise and transform
data while preserving the original information and documenting the
processing steps.

Data processing may include standardising values, transforming spatial
data, resolving taxonomic names, combining datasets, or preparing data
for analysis and publication.

Data provenance and documentation
=================================

Reliable biodiversity data require more than the recorded observation
itself. It is also important to retain information about when, where,
how, and by whom the observation was collected and how the data have
subsequently been processed.

OpenBioMaps supports the documentation of data collection and management
processes through structured fields, metadata, queries, and project-specific
workflows.

Keeping this information together with the data improves traceability
and makes later verification and reuse possible.

Queries and derived data
========================

Queries can be used to select, filter, combine, and transform data
without modifying the original records.

This makes it possible to create project-specific views of the data for
different purposes, such as analysis, reporting, visualisation, or
publication.

Repeatable queries can also provide a documented and reproducible way of
producing derived datasets.

Data export and reuse
=====================

OpenBioMaps data can be exported or accessed by external applications
for analysis, visualisation, publication, and other purposes.

Data can be used directly from OpenBioMaps or transferred to tools such
as QGIS and R, depending on the requirements of the workflow.

:doc:`Data access <../data_access>`

Data lifecycle
==============

OpenBioMaps can support the different stages of a biodiversity data
lifecycle, from the initial field observation to later analysis,
publication, and reuse.

A typical workflow may include:

* data collection;
* storage in a structured database;
* validation and quality control;
* documentation and metadata management;
* data processing and harmonisation;
* analysis and visualisation;
* publication or controlled sharing; and
* reuse for further research or conservation activities.

These stages do not necessarily form a strictly linear process. Data may
return to earlier stages as errors are identified, new information becomes
available, or project requirements change.


