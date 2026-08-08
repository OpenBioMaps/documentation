Getting started
***************

Choose how to use OpenBioMaps
=============================
To create an OpenBioMaps project, you need access to an OpenBioMaps server. This 
can be your own server, a rented server, or a server already maintained by someone 
else for hosting OpenBioMaps.

Join an existing server
-----------------------
The easiest way to create a new project (sometimes referred to as a database) is to 
use an existing OpenBioMaps server. Check the list of known servers to see whether you 
have access to one of them. There are dedicated public servers that host many different 
databases.

Set up your own server
----------------------
If you need more capacity or want to control access to the entire
server, you can install your own OpenBioMaps server.

:doc:`OpenBioMaps server installation <../server_install>`

For a Docker-based installation, see:

:doc:`Docker installation <../tutorials>`


Create an OpenBioMaps project
=============================
An OpenBioMaps server can host multiple (database) projects. Before creating a project, you 
need access to an existing project on the server. Once access has been granted, you can create 
and configure your project according to the requirements of your data collection.

The required steps are described in the tutorial here: https://openbiomaps.org/documents/en/tutorials.html#new-project, and
here: https://openbiomaps.org/documents/en/new_project.html

Understand the observation data model
=====================================
Before designing your database and data collection forms, it is useful
to understand how OpenBioMaps represents biodiversity observations.

:doc:`Observation events vs. occasional observations <../observation_events>`


Set up your data
================
Once your project has been created, the next step is to define how your
data will be structured and collected.

OpenBioMaps allows you to create and manage project-specific database
tables and fields. The database structure should reflect the information
you want to record and the relationships between different types of data.

Define your database structure
------------------------------

Project tables and their columns are managed through the administrative
interface. Tables and fields registered there become available to the
OpenBioMaps interfaces and can be used for queries and data collection.

It is recommended to provide descriptions for tables and fields. These
descriptions form part of the project's metadata and help users understand
the meaning and intended use of the data.

:doc:`Administrative settings <../admin_settings>`

Create data collection forms
----------------------------

Once the database structure has been defined, you can create upload forms
for entering and collecting data.

An upload form determines which fields are available to users, which
fields are required, how values are entered, and how data are collected.
Forms can be used for web-based data entry, file uploads, and access
through the API.

:doc:`Upload form management <../upload_forms>`

The database structure and the data collection forms together define the
basic data collection workflow of an OpenBioMaps project.

Data management and access
==========================

Before starting data collection, consider how the data will be managed
and how access to the data will be controlled.

* :doc:`Data access <../data_access>`
* :doc:`Data management policy <../data_policy>`


Connect to your project
=======================
OpenBioMaps projects can be accessed through several interfaces and
tools, depending on how the data are collected, managed, or analysed.

Web interface
-------------
The web interface is the central tool for managing an OpenBioMaps
project. It provides tools for data management, user management,
configuration, and administration.

:doc:`User interface <../user_interface>`

:doc:`Admin interface <../admin_settings>` 

OpenBioMaps also provides programmatic interfaces for external client
applications.

:doc:`OpenBioMaps API <../api>`


QGIS integration
----------------
The OpenBioMaps QGIS plugin provides access to OpenBioMaps data from QGIS.

`OpenBioMaps QGIS plugin <https://plugins.qgis.org/plugins/obm_connect/>`_

R package
---------
The ``obm`` R package provides tools for accessing and working with
OpenBioMaps data from R.

`obm on CRAN <https://cran.r-project.org/web/packages/obm/index.html>`_

Other integrations
------------------
Appsmith, Nextcloud, Do you need something else?


Start collecting and managing data
==================================
Your OpenBioMaps project is now ready for data collection.

Depending on your workflow, data can be entered through the web
interface, uploaded from files, collected using mobile applications,
or transferred through the OpenBioMaps API.

Once data are in the system, they can be validated, managed, queried,
visualised, analysed, and shared according to the project's data
management workflow and rules.

For information on specific data collection workflows, see
:doc:`OpenBioMaps example data collections: <../data_collection_examples>`.
