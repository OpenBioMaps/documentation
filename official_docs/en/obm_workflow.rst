OpenBioMaps workflow
********************

PostgreSQL Backend
==================

Database tables
---------------
Tables
......
OpenBioMaps only handles Postgres tables that are created through the OBM admin interface. When a table is created, it is registered with the tables managed in the project. If you rename your table via an SQL client, OBM loses the connection to the table. If you delete a table from an SQL client, OBM will automatically delete the associated metadata. You can also delete an empty table via the OBM admin interface.

Metadata
........
For database tables, a descriptive metadata can be specified, which is optional but highly recommended. It is basically good practice to provide descriptive information for your tables and fields!

Database columns
----------------
Default columns
...............
OpenBioMaps creates a number of default fields in each table it creates, the existence of which is mandatory for OBM to be able to manage the table.
These fields should never be deleted from our tables!

These fields are as follows:

.. code-block:: SQL
  
  CREATE TABLE public.test_table (
    obm_id integer DEFAULT nextval('public.test_table_obm_id_seq'::regclass) NOT NULL,
    obm_geometry public.geometry,
    obm_uploading_id integer,
    obm_validation numeric,
    obm_comments text[],
    obm_modifier_id integer,
    obm_files_id character varying(32),
    CONSTRAINT enforce_dims_obm_geometry CHECK ((public.st_ndims(obm_geometry) = 2)),
    CONSTRAINT enforce_srid_obm_geometry CHECK ((public.st_srid(obm_geometry) = 4326))
  );


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
Data can be loaded into the data tables via the upload forms or via any SQL client. When data is entered using the upload forms, the data is recorded as an upload event in the system.uploading table and the upload metadata is available with the data.

SQL ways
--------
You can also import large amounts of data with the `COPY FROM Postgres tool <https://www.postgresqltutorial.com/postgresql-tutorial/import-csv-file-into-posgresql-table/>`_ !

Data output
===========
OpenBioMaps output
------------------
The data can be queried via the web interface or API. It is also possible to download and export complete tables or filter, display and export data.

Other outputs
-------------
OpenBioMaps basically stores the data in simple strctures, so that the data can be easily queried and plotted via SQL clients, e.g. in QGIS.

Users
=====

