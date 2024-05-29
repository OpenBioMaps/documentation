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
In Postgres you cannot specify the order of the fields, but in OBM you can. On the one hand, it is possible to specify a default order, which OBM uses for both data display and forms, and on the other hand, this order can be overridden on each form. If you do not specify any order, your fields will follow the Postgres default field order.
If we want to change the order of our fields in Postgres, one solution is to use a view or to redefine our table with the appropriate field order. In the latter case, we can use a CREATE TABLE ... SELECT FROM query to create a new table from the old one, then delete the old one and rename the new one to the old one, but also pay attention to the triggers, sequences and keys to be transferred!

Visible names
.............
OpenBioMaps uses a so-called display name stored in a metadata to display the field names instead of the field names visible in SQL, which is specified by the administrator who created the fields. By default, this is the same as the Postgres name of the field. If the field name starts with the prefix str_, these strings will be displayed with the translation according to the language settings of the client application, if we have specified translations for our strings. 



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

