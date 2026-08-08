Clients
*******

QGIS
====
QGIS (formerly Quantum GIS) is a free, open-source geographic information system 
(GIS) that enables the display, editing and analysis of geographic data, as well as 
the creation of professional maps. Developed as part of the OSGeo project, the software 
is one of the world’s most popular desktop GIS applications, offering a complete alternative 
to expensive, licence-based commercial alternatives (such as ArcGIS).

The OpenBioMaps QGIS plugin provides access to OpenBioMaps data from QGIS.

`OpenBioMaps QGIS plugin <https://plugins.qgis.org/plugins/obm_connect/>`_


R usage
=======
R is a free programming language and software environment designed for statistical computing, 
data analysis, and graphics. Created in 1993 by Ross Ihaka and Robert Gentleman at the University 
of Auckland, it is widely used by researchers, data miners, and statisticians.

The ``obm`` R package provides tools for accessing and working with OpenBioMaps data from R.

`obm on CRAN <https://cran.r-project.org/web/packages/obm/index.html>`_

PostgreSQL clients
==================
Cross-platform, full database management

`pgAdmin is professional PostgreSQL client which can be used managing OBM Postgres databases <https://www.pgadmin.org/>`_

Mapserver clients
=================
MapServer clients refer to software interfaces, desktop GIS applications, or web mapping libraries 
that consume OGC web services (like WMS, WFS, and WCS) served out by MapServer. Common clients 
include desktop tools like QGIS and ArcGIS, web libraries like OpenLayers and Leaflet, and 
MapServer's own internal capability to act as a client to remote servers.
OpenBioMaps is primarily rendered using MapServer, so MapServer client programmes are able to connect 
to the OpenBioMaps map services, although this depends largely on the project’s configuration.

Oauth clients
=============
JWT (JSON Web Token) is a compact, self-contained token format used to securely transmit data. 
OAuth 2.0 is an authorization framework that delegates access. They are not competing options; 
OAuth frequently uses a signed JWT as its access token or ID token format to pass user claims statelessly.

Appsmith
========
Appsmith is an open-source, low-code development platform that enables the extremely rapid creation of internal business tools, administrative interfaces, dashboards and custom workflows. We have our own instance!
`OBM Appsmith <https://appsmith.openbiomaps.org/user/login>`_

Nextcloud
=========
Nextcloud is an open-source, self-hosted content collaboration platform that gives you full control 
over your own data. It is an excellent, privacy-focused alternative to popular cloud services such as 
Google Drive, Microsoft OneDrive and Dropbox. Nextcloud can, of course, be integrated with OpenBioMaps, 
as demonstrated by the Camptrap database, where users upload images to a Nextcloud account; an application 
built on the OBM project then analyses these images and uploads them back to the Nextcloud account.

API clients
===========
OpenBioMaps also provides programmatic interfaces for external client
applications. One of our largest client applications is the OpenBioMaps field mobile app, 
developed by ECOLLAB.

:doc:`OpenBioMaps API <../api>`

