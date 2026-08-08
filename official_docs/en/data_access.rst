Data access
***********

OpenBioMaps provides several ways to query, view, and download project
data. The records and fields available through these interfaces depend on
the project's access rules and on the permissions of the current user.

This page provides an overview of the available data retrieval methods and
the mechanisms used to control access to project data.


Retrieving data
===============

Data can be retrieved through the web application, downloaded in supported
file formats, or accessed from external applications.


File download
-------------

Query results and other accessible project data can be downloaded in several
formats. Depending on the type of data and the project configuration, the
available formats may include:

* text and structured data: CSV and JSON;
* images, downloaded individually or in bulk;
* spreadsheets: ODS, XLS, and XLSX;
* spatial data: ESRI Shapefile, GPX, and SQLite.

An ESRI Shapefile export may consist of several related files, including
``.shp``, ``.dbf``, ``.cpg``, ``.prj``, and ``.shx`` files.

.. TODO: Document where downloads can be started in the web interface and
   whether the available formats depend on the query, the database table, or
   the configuration of an export module.

.. TODO: List the supported image formats and explain how images are
   packaged for bulk download. The structure and spatial capabilities of
   SQLite exports should also be documented.


Web queries
-----------

The web application provides tools for filtering and retrieving accessible
records. Depending on the project configuration, users can perform:

* attribute-based queries using text, lists, dates, and other configured
  fields;
* spatial queries using geometries selected or drawn on the map; or
* combined spatial and attribute-based queries.

For an overview of the query interfaces, see
:doc:`User interfaces <user_interface>`.

.. TODO: Document how query results can be viewed, refined, saved, cited,
   and exported. It should also be clarified whether all projects support
   combined spatial and attribute-based queries.


External applications
---------------------

Project data can also be accessed from external applications:

* the OpenBioMaps API can be used by scripts, the OpenBioMaps R package,
  and other API clients;
* an authorised SQL connection can provide direct database access for
  applications such as QGIS; and
* supported client applications can provide their own query and download
  interfaces.

Access through an external application is subject to the project's access
rules and the permissions associated with the authenticated user or
connection.

For more information, see:

* :doc:`OpenBioMaps API <api>`; and
* :doc:`Client applications <clients>`.


Controlling access to data
==========================

OpenBioMaps can control access at several levels:

* project-level settings define the default access and modification policy;
* row-level rules control access to individual records; and
* column-level rules control which fields can be viewed or downloaded.

The effective permissions may therefore depend on several settings. Project
administrators should test the resulting access with users belonging to
different groups, as well as without authentication where public access is
enabled.

.. TODO: Provide a complete permission evaluation model showing the exact
   precedence and interaction of project-level, row-level, column-level, and
   user-group rules.


Project-level access
--------------------

The default project-level access settings are defined in the
``local_vars.php.inc`` configuration file:

.. code-block:: php

   define('ACC_LEVEL', 'group'); // Can be set to 'public' or 'login'.
   define('MOD_LEVEL', 'group');

``ACC_LEVEL`` defines the default level at which project data can be
accessed. The documented values are:

``public``
   Data are publicly accessible, subject to any more specific access rules.

``login``
   Data are accessible to authenticated users, subject to any more specific
   access rules.

``group``
   Access is controlled through project groups and additional access rules.

``MOD_LEVEL`` defines the default level at which data can be modified. It
uses a similar access model.

Setting ``MOD_LEVEL`` to ``public`` allows data to be modified without
requiring the user to sign in. This setting should only be used when
unauthenticated modification is explicitly intended and its security
implications have been considered.

.. TODO: Confirm all valid values of ``ACC_LEVEL`` and ``MOD_LEVEL`` and
   document their exact behaviour. In particular, clarify how ``login``
   differs from ``group`` and whether additional values are supported.

.. TODO: Explain whether these constants apply to the entire project, how
   configuration changes take effect, and whether they can be managed
   through the project administration interface.


Row-level access
----------------

When ``ACC_LEVEL`` or ``MOD_LEVEL`` is set to ``group``, access to
individual records can be controlled through a project-specific
``*_rules`` table. Here, ``*`` represents the name or prefix used by the
project.

A rules table is associated with a data table. A data record is linked to
its corresponding rule through the ``obm_id`` value in the data table and
the ``row_id`` value in the rules table.

In a project using group-level access, records without a corresponding
entry in the rules table are available only to project hosts.

.. TODO: Confirm whether a data record can have exactly one corresponding
   rules-table row or multiple rows. Also confirm whether “project host” is
   the current name of the role that can access records without a rule.

The rules-table functionality can be configured in the project
administration interface under **Project administration > Functions >
Create access rules**. This interface can be used to create or update the
trigger function and to enable or disable it.

When enabled, the trigger maintains the rules table after records are
created, modified, or deleted.

.. TODO: Confirm the current labels and location of the access-rules
   administration interface. Document what happens to existing rules when
   the trigger is disabled, recreated, or modified.


Assigning read and write groups
-------------------------------

Read and write access can be assigned to individual records through the
group-related fields of the rules table.

These values can be populated automatically by the rules-table trigger.
The assigned groups may be derived from the access settings of the upload
form used to create the record. Information about completed uploads and
their configured owner and group values is stored in the
``system.uploadings`` table.

.. TODO: Document the data types and accepted values of the rules table's
   ``read`` and ``write`` fields. Clarify whether they contain one group,
   multiple groups, user identifiers, or a combination of these.

.. TODO: Explain how upload-form access settings are transferred to
   ``system.uploadings`` and then to the rules table. The behaviour for
   records created outside an upload form, such as through SQL or the API,
   should also be documented.


Regenerating a rules table
--------------------------

A rules table can also be regenerated manually. The following examples use
``abc`` as the data table and ``abc_rules`` as its rules table.

The following statements recreate rules without assigning read or write
groups:

.. code-block:: sql

   DELETE FROM abc_rules
   WHERE data_table = 'abc';

   INSERT INTO abc_rules (row_id, sensitivity, data_table)
   SELECT obm_id, 'sensitive', 'abc'
   FROM abc;

The following statements derive the group and owner values from the
corresponding entry in ``system.uploadings``:

.. code-block:: sql

   DELETE FROM abc_rules
   WHERE data_table = 'abc';

   INSERT INTO abc_rules (row_id, sensitivity, data_table, read, write)
   SELECT a.obm_id, 'sensitive', 'abc', s."group", s.owner
   FROM abc AS a
   LEFT JOIN system.uploadings AS s
       ON s.id = a.obm_uploading_id;

These examples must be adapted to the actual table names, schema, column
types, and access policy of the project. Administrators should back up the
existing rules table and verify the generated permissions before using the
statements in a production database.

.. TODO: Confirm that the example column names and value types match the
   current schema. In particular, verify the types of ``sensitivity``,
   ``read``, ``write``, ``system.uploadings.group``, and
   ``system.uploadings.owner``.

.. TODO: Explain whether deleting and rebuilding a rules table can
   temporarily expose or hide data, whether the operation should run inside
   a transaction, and whether there is an administration command that
   performs the same task safely.


Sensitivity settings
--------------------

The ``sensitivity`` field in the rules table affects the public availability
of a record in a project using group-level access.

The documented values include:

``sensitive``
   The record can be read or modified only by members of the groups
   specified by the applicable access rules.

``restricted``
   This value currently has the same documented meaning as ``sensitive``.

``no-geom``
   The record may be accessible at the public level, but its geometry is not
   displayed publicly.

``only-owner``
   Only the project owner can access the record.

.. TODO: Confirm the complete list of accepted ``sensitivity`` values and
   define their exact effects on viewing, querying, downloading, and
   modifying records.

.. TODO: Clarify whether ``restricted`` and ``sensitive`` are true aliases
   or whether they differ in some interfaces. For ``no-geom``, explain
   whether geometry is removed, generalised, replaced, or merely hidden in
   the map. Also define which user is considered the owner for
   ``only-owner`` records.


Column-level access
-------------------

Access can be further controlled for individual database fields by using the
``allowed_columns`` module. This module determines which columns can be
viewed or downloaded by public users or specified user groups.

In a project where ``ACC_LEVEL`` is set to ``group``, the module can be used
to make selected fields accessible even when the project does not otherwise
provide general access to every field. It can also restrict the visible
fields of records that are accessible through row-level rules.

This makes it possible, for example, to allow users to discover that a
record exists while exposing only an approved subset of its fields.

.. TODO: Document how the ``allowed_columns`` module is enabled and
   configured, whether it controls queries as well as displayed and
   downloaded results, and how it treats geometry columns.

.. TODO: Confirm whether ``allowed_columns`` can make fields publicly
   accessible when a record has no corresponding rules-table entry. This
   interaction is security-sensitive and should be described with concrete
   examples.


How access rules interact
-------------------------

If only group-level project access is configured and no more specific rules
grant access, project data are available only to the administrative role
that is allowed to bypass those restrictions.

A rules table adds row-level control, allowing different records to be made
available to different groups. The ``allowed_columns`` module adds
column-level control, allowing only selected fields of an accessible record
to be viewed or downloaded.

Where several rules apply, the effective permissions are determined by
their combined project-, row-, and column-level restrictions. Administrators
should not assume that a broader rule automatically overrides a more
specific restriction.

.. TODO: Replace this general description with the exact access-resolution
   algorithm implemented by OpenBioMaps. Include examples covering public,
   authenticated, group, owner, row-level, and column-level access, as well
   as conflicting read and write permissions.
