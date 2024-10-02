Data retrieval
**************

Data retrieval options
======================

* File download

  Supported formats: 

  - Plain text files: csv, json
  - Image files export: one by one or in bulk
  - Spreadsheet formats: ods (Libreoffice), xls (Excel), xlsx (Excel)
  - Spatial formats: esri shape (.shp, .dbf, .cpg, .prj, .shx together), gpx (GPS data format (xml)), sqlite

* Web query

  - Text filtered query
  - Spatial query

* External applications
  - Use API interface (e.g. R-package)
  - Use SQL connection (e.g. QGIS)


Data access control
===================

The lowest level of regulation defined at the inception of the project is

local_vars.php.inc

file:

.. code-block:: php

  define('ACC_LEVEL','group'); // can be set to 'public' or 'login'
  define('MOD_LEVEL','group');

The ACC_LEVEL variable defines the default level of data access in the project. It can be public or only accessible to logged in users (login or group). Login is more of a theoretical option, usually group is used in this case.

MOD_LEVEL is the control for modifying data in a similar way to above. If MOD_LEVEL is public, then anyone can modify the data without logging in! 

If the data access (ACC_LEVEL)/download and modify (MOD_LEVEL) levels are "group", then we will have additional control options in the

*_rules* table.

Our *_rules* table has a one-to-one relationship with each data table we want to control by setting the obm_id - row_id foreign key.
Data rows for which there is no *_rules* entry are only available to project hosts (for ACC_LEVEL='group').

The functionality of the *_rules* table can be found in the [Project administration] -> [Functions] menu [Create access rules]

Here you can create and modify the trigger function, and enable or disable the trigger which will automatically update our _rules table after each record addition, modification and deletion.

The access to each record can be defined individually if groups are added in the group read and write fields. This can be done automatically by the *_rules* trigger based on the data access settings of the uploading forms, which values are entered in the system.uploadings table based on the uploading forms settings.

The *_rules* table can also be regenerated manually:

- one at a time, without group settings:

.. code-block:: sql

  DELETE FROM abc_rules WHERE data_table='abc';
  INSERT INTO abc_rules (row_id,sensitivity,data_table) SELECT obm_id,'sensitive','abc' FROM abc
..

- or with a row-by-row group setting:

.. code-block:: sql

  DELETE FROM abc_rules WHERE data_table='abc';
  INSERT INTO abc_rules (row_id,sensitivity,data_table,read,write) 
      SELECT obm_id, 'sensitive', 'abc', s.group, s.owner 
      FROM abc a LEFT JOIN system.uploadings s ON (s.id = a.obm_uploading_id)

In the *_rules* table, the *sensitivity* field is used to specify the public availability of a given dataset in closed ('group') projects. The value of *'sensitivity'* may also be 'sensitive' or 'restricted'. These have the same meaning. The 'sensitive' lines can only be read or modified by members of the specified groups.

Access to data can be further controlled by setting rules for each field using the *allowed_columns* module.
If your project is set to 'group' and there are no rows in the *_rules* table, you can still use the *allowed_columns* module to make your data fields publicly accessible or accessible to specified user groups. That is, the 'allowed_columns' module is also the highest level of access control.

In each case, the most detailed access rule determines the access to the data, if more than one rule could apply.

That is, if we have a 'group' level project and no other rules are specified, then only the project administrators will have access to the data. If table *_rules* is specified, then the data is subject to rules on a row-by-row basis, i.e. we can grant broader access to individual rows.


Finally, with a module allowed_columns we have the possibility to control column level access. Allowed_columns can be used in the group access setting and when using the rules table, by granting permission to view (or download) the contents of certain fields from an otherwise queryable row of data in which no field is accessible.
