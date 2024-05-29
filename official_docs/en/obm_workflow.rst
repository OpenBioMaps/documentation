OpenBioMaps workflow
********************

PostgreSQL Backend
==================

Database tables
---------------

Metadata
........

Database columns
----------------

SQL columns vs OpenBioMaps columns
..................................
The fields in the SQL database are managed by OpenBioMaps in all tables. Only those fields for which we approve the use of the field by OBM. The approval is done by specifying the OBM type of the field in the administrative interface.
The OBM type, unlike the postgres type, does not refer to the content of the field, but to the way it is used.

Column names
............
The naming of fields is limited in OBM compared to Postgres. OBM does not allow capital letters and special characters in field names, only underscores. However, it assigns a visible name metadata to each field, which can be an automatically translatable string, so that each field can be displayed with its name on forms or during data queries. Only when querying raw data will the user see the original field names, otherwise they will see the string specified when the field was created, or its automatic translation.

Column order
............

Visible names
.............




Data input
==========
OpenBioMaps way
---------------

SQL ways
--------


Data output
===========
OpenBioMaps output
------------------

Other outputs
-------------


Users
=====

