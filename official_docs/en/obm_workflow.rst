.. _data-flow-database-integration:

OpenBioMaps data flow and database integration
**********************************************

This page describes how OpenBioMaps connects project configuration,
PostgreSQL database objects, metadata, upload workflows, access rules,
queries, and external clients.

It is intended for developers, server administrators, and experienced
project administrators who need to understand the technical implementation
behind the user-facing data-management workflow. For a general introduction
to collecting and managing data, see:

* :doc:`Getting started <getting_started>`;
* :doc:`Data collection <data_collection>`;
* :doc:`Data management <data_management>`; and
* :doc:`Data access <data_access>`.

The implementation details described here can vary between OpenBioMaps
versions and project configurations. Before changing database objects
directly, inspect the current project metadata, triggers, views, access
rules, and application source code. Test structural changes in a separate
project and create an appropriate backup before applying them to production
data.


Technical overview
==================

A typical OpenBioMaps data flow contains the following technical stages:

#. A project administrator defines PostgreSQL tables, columns, relationships,
   and OpenBioMaps metadata.
#. Upload forms expose selected columns to web, file-upload, API, or mobile
   clients.
#. A client submits records and, where applicable, attachments and upload
   metadata.
#. OpenBioMaps validates and transforms the submitted values according to the
   form definition.
#. The application inserts the accepted values into the destination table and
   records information about the upload.
#. Database triggers or background jobs can maintain history, access rules,
   taxonomic data, derived values, and other project-specific structures.
#. Query templates combine the project tables with access-control and module
   fragments.
#. The resulting data can be displayed through the web application or
   accessed through exports, APIs, SQL clients, and other integrations.
#. Backups, archives, and project policy determine how the data and associated
   configuration are preserved.

Not every project uses all these stages. For example, a small project may
use one observation table and one web form, while a monitoring project may
use separate tables for sites, events, observations, taxa, attachments, and
validation results.


PostgreSQL backend
==================

OpenBioMaps stores project data in PostgreSQL and commonly uses PostGIS for
spatial data. The database contains both ordinary PostgreSQL objects and
OpenBioMaps metadata describing how the application should use those
objects.

The existence of a PostgreSQL table or column does not by itself make that
object available in OpenBioMaps. The corresponding metadata must also
identify the object and describe its role in the project.


Database tables and metadata
----------------------------

Tables created through the project administration interface are created in
PostgreSQL and registered in the OpenBioMaps metadata. Registered tables can
then be used by upload forms, query templates, modules, administrative
tools, and other application components.

A table or view created with an SQL client is not registered automatically. 
It must be added to the relevant OpenBioMaps metadata before the application 
can use it safely and consistently.

The administration interface should be preferred for supported table
operations because it can update both the PostgreSQL object and the
associated metadata. Direct SQL changes can leave metadata, forms, queries,
triggers, or modules referring to an object that no longer exists.

For further information, see
:ref:`Database tables and columns <database-columns>`.

.. TODO: Document the exact metadata tables and columns used to register a
   project table or view in the current OpenBioMaps version.

.. TODO: Add a supported procedure for registering an existing PostgreSQL
   table or view without recreating it.

.. TODO: Verify what happens to OpenBioMaps metadata when a registered table
   is renamed or deleted directly through SQL. Do not rely on automatic
   metadata cleanup until this behaviour has been tested for the current
   version.


Table descriptions
------------------

A registered table can have a human-readable description. Table and column
descriptions form part of the project metadata and should explain the
meaning, provenance, units, expected values, and intended use of the data.

Descriptions are strongly recommended even when they are not technically
required. A database structure that is understandable only from its SQL
identifiers is difficult to maintain, exchange, and reuse.

For recommendations about metadata and provenance, see
:doc:`Data management <data_management>` and
:doc:`Data policy <data_policy>`.


Database columns
----------------

A project table consists of ordinary data columns and, where required,
OpenBioMaps system columns. PostgreSQL determines the physical data type,
constraints, and storage of each column. OpenBioMaps metadata determines how
the application interprets and uses the column.


System columns
..............

Tables created by OpenBioMaps commonly contain columns with the ``obm_``
prefix. Depending on the OpenBioMaps version and project configuration,
these can include fields for:

``obm_id``
   The internal identifier of a record.

``obm_geometry``
   The spatial geometry associated with the record.

``obm_uploading_id``
   A reference to the upload through which the record was created.

``obm_validation``
   Validation-related information.

``obm_comments``
   Comments or annotations associated with the record.

``obm_modifier_id``
   Information identifying a user or process that modified the record.

``obm_files_id``
   A reference or references associated with uploaded attachments.

A basic table definition can resemble the following example:

.. code-block:: sql

   CREATE TABLE public.test_table (
       obm_id integer
           DEFAULT nextval(
               'public.test_table_obm_id_seq'::regclass
           )
           NOT NULL,
       obm_geometry public.geometry,
       obm_uploading_id integer,
       obm_validation numeric,
       obm_comments text[],
       obm_modifier_id integer,
       obm_files_id character varying(32),
       CONSTRAINT enforce_dims_obm_geometry
           CHECK (public.st_ndims(obm_geometry) = 2),
       CONSTRAINT enforce_srid_obm_geometry
           CHECK (public.st_srid(obm_geometry) = 4326)
   );

This example is illustrative and must not be treated as the authoritative
schema for every installation. Column types, constraints, attachment
handling, sequence definitions, and spatial-reference settings can differ
between versions and projects.

Do not delete or rename an ``obm_`` column merely because it appears unused.
Upload processing, triggers, modules, access rules, history, queries, or
external clients may depend on it.

.. TODO: Generate an authoritative reference for every system column created
   by the current administration interface. For each column, document its
   PostgreSQL type, nullability, default value, constraints, references, and
   application components that use it.

.. TODO: Verify whether all listed ``obm_`` columns are mandatory in every
   managed table or whether some are optional and created only for selected
   workflows.

.. TODO: Document the current attachment model and confirm whether
   ``obm_files_id`` contains one identifier, several identifiers, or a
   reference to another table.


PostgreSQL types and OpenBioMaps types
......................................

A PostgreSQL data type describes how a value is stored and which database
operations can be performed on it. Examples include ``text``, ``integer``,
``date``, ``timestamp``, arrays, and PostGIS geometry types.

An OpenBioMaps column type or semantic role describes how the application
uses the column. For example, a column can represent:

* a general data value;
* a scientific name;
* an alternative taxon name;
* an observation date;
* a number of individuals;
* a geometry;
* a coordinate;
* a citation; or
* an attachment.

Only registered columns that are made available through the OpenBioMaps
metadata can be selected by application components such as upload forms and
query interfaces.

The PostgreSQL type and the OpenBioMaps semantic role must be compatible.
Assigning a semantic role does not convert the physical data type or
validate existing values automatically.

.. TODO: Add a compatibility table mapping every OpenBioMaps semantic type
   to its supported PostgreSQL types and the core functions or modules that
   use it.

.. TODO: Document whether assigning or changing a semantic type affects
   existing upload forms, query templates, mobile clients, or cached form
   definitions.


Column identifiers and visible names
....................................

PostgreSQL identifiers should use lowercase letters, numbers, and
underscores. Avoid spaces, accented characters, quoted identifiers, and
other special characters. OpenBioMaps metadata can associate a separate
visible name with a column, so a database-safe identifier does not have to
be displayed directly to users.

For example, a database column can be named ``observation_date`` while its
visible name is displayed as ``Observation date`` or its translated
equivalent.

A visible name beginning with the ``str_`` prefix can be used as a
translation key where project-specific localisation is supported. The
client application displays the translation available for its current
language, with the configured fallback behaviour applying when a translation
is missing.

Renaming only a visible name does not rename the PostgreSQL column.
Renaming the PostgreSQL column can break forms, queries, triggers, views,
modules, exports, and external clients.

For further information about local translations, see
:ref:`Local translations <localisation>`.

.. TODO: Document the exact fallback behaviour when a ``str_`` translation
   key or a translation for the active language is missing.

.. TODO: Confirm which clients use visible names and which expose raw
   PostgreSQL identifiers in forms, exports, API responses, or error
   messages.


Column order
............

PostgreSQL preserves a physical column order in table definitions but does
not provide a simple supported operation for reordering existing columns.
OpenBioMaps metadata and upload forms can define a presentation order
independently of the physical database order.

The project-level order can be used as a default by data displays and forms.
An individual upload form can override that order for its own workflow. If
no application-level order is defined, the interface may fall back to the
database or metadata order.

Do not recreate a production table only to change the visible order of its
columns unless there is a verified technical requirement. Recreating a
table can affect:

* sequences and default values;
* primary and foreign keys;
* indexes and constraints;
* ownership and privileges;
* triggers and rules;
* comments and metadata;
* views and materialised views;
* access-rule tables;
* upload forms and query templates; and
* external applications.

Use the OpenBioMaps presentation-order settings where possible.

.. TODO: Confirm the precise fallback order used by every web, API, export,
   and mobile interface when no explicit column order is configured.


Data input
==========

Project data can enter PostgreSQL through OpenBioMaps upload workflows or
through direct database operations. These routes are not equivalent.


OpenBioMaps upload workflows
----------------------------

Upload forms define the destination table, exposed columns, required fields,
input controls, default values, validation rules, supported clients, and
access settings.

Depending on its configuration, a form can be used by:

* a web-based data-entry interface;
* a file-upload workflow;
* the OpenBioMaps API;
* a mobile application; or
* another compatible client.

A typical form-based insertion has the following stages:

#. The client obtains or displays a form definition.
#. The contributor enters or uploads values.
#. The application validates the submitted structure and values.
#. Warnings or soft validation errors are presented where supported.
#. Accepted values are written to the destination table.
#. Upload metadata are recorded.
#. Attachments and their associations are stored where applicable.
#. Database triggers perform configured follow-up operations.

For detailed form configuration, see
:doc:`Upload form management <upload_forms>`.


Upload events and provenance
----------------------------

When data are submitted through an OpenBioMaps upload workflow, the
application records information about the upload in the
``system.uploadings`` table. Records written to a managed data table can
refer to that upload through ``obm_uploading_id``.

Upload metadata can be used to associate records with information such as:

* the contributor or owner;
* the destination table;
* the form used for the upload;
* the submission time;
* group access assignments;
* the source file or data-entry workflow; and
* processing or completion status.

The exact stored fields and their meaning are version-specific. A direct SQL
insertion does not automatically create an equivalent upload event unless
the caller implements the required workflow explicitly.

.. TODO: Document the complete current schema of ``system.uploadings`` and
   identify which columns are stable public interfaces and which are
   internal implementation details.

.. TODO: Describe the transaction boundaries of an upload. Clarify whether
   insertion of upload metadata, data records, attachments, and access rules
   succeeds or fails as a single transaction.

.. TODO: Document how interrupted uploads, draft uploads, rejected rows,
   completed uploads, and deleted uploads are represented.


Validation and transformation
-----------------------------

Validation can occur in several layers:

* client-side form controls;
* server-side upload processing;
* PostgreSQL types and constraints;
* database triggers;
* background jobs; and
* later curator review.

Client-side validation improves usability but must not be treated as a
security boundary. Values received through the API, file uploads, or direct
database connections require appropriate server-side validation.

Transformations can normalise values, construct geometry, resolve taxonomic
names, assign defaults, or derive other fields. If a transformation changes
the scientific meaning of submitted data, the project should preserve the
original value or sufficient provenance to reconstruct the change.

For background processing, see :doc:`Background jobs <jobs>`.


Direct SQL input
----------------

Authorised database users can insert or import records with PostgreSQL
clients and tools such as ``COPY``. This can be useful for controlled bulk
migration or administrative data repair.

For example, PostgreSQL supports importing data with ``COPY FROM``. See the
`PostgreSQL COPY documentation
<https://www.postgresql.org/docs/current/sql-copy.html>`_.

Direct SQL operations can bypass application-level behaviour, including:

* upload-form validation;
* automatic creation of upload metadata;
* attachment processing;
* access-rule assignments;
* history or audit information;
* project-specific transformations;
* notifications; and
* application-level error handling.

Database triggers still execute unless they are disabled, but their
behaviour can depend on values normally supplied by the application. A
record inserted without ``obm_uploading_id`` or another expected field can
therefore produce incomplete metadata or access rules.

When importing data directly, the best practice is to create an empty upload, 
assign the upload ID (``obm_uploading_id``) to the uploaded data afterwards, 
and specify the direct upload method and source in the upload metadata.

Before a direct import:

#. review the destination table, constraints, triggers, and rules;
#. determine whether a corresponding upload record is required;
#. validate and transform the source data explicitly;
#. use a transaction where appropriate;
#. test the import in a non-production project;
#. verify row-level and column-level access after insertion;
#. verify history, attachment, and taxonomic workflows; and
#. record the source and transformation of the imported data.

Do not disable triggers merely to make an import succeed without first
understanding their purpose. Access-control, history, or integrity triggers
can be security-critical.

.. TODO: Provide a supported bulk-import procedure that creates compatible
   upload metadata and access rules while retaining the performance
   advantages of PostgreSQL ``COPY``.

.. TODO: Document which application service or API should be preferred over
   direct SQL for automated integrations.


Triggers, rules, and derived processing
=======================================

OpenBioMaps projects can use PostgreSQL triggers and rules to maintain
project-specific behaviour when records are inserted, updated, or deleted.

Documented trigger workflows include:

* taxon-list maintenance;
* record history;
* row-level access rules; and
* project-specific validation or derived values.

A trigger operates inside a database transaction and can reject or modify a
change. A background job normally runs separately and is better suited to
long-running, scheduled, retryable, or resource-intensive processing.

The distinction is important:

``Constraint``
   Enforces a database invariant and rejects values that do not satisfy it.

``Trigger``
   Executes automatically as part of a database modification.

``Rule``
   Rewrites or redirects selected PostgreSQL operations, including
   operations on configured views.

``Background job``
   Executes separately on a schedule or after manual initiation.

``Application validation``
   Checks or transforms values in the OpenBioMaps application workflow.

The same requirement should not be implemented inconsistently in several
layers. If several layers are necessary, their responsibilities and failure
behaviour should be documented.

For trigger administration, see
:ref:`Functions <trigger-functions>`.

.. TODO: Document the execution order and dependencies of the standard
   OpenBioMaps triggers.

.. TODO: Identify which standard triggers are created automatically for a
   new project table and which require explicit administrator action.

.. TODO: Define a supported method for testing triggers and inspecting their
   effects before enabling them in production.


Access-rule integration
=======================

Project data access can be controlled through project-level defaults,
row-level rules, column-level restrictions, group membership, and
administrative roles.

A row-level access workflow commonly connects:

* the record's ``obm_id``;
* a corresponding ``row_id`` in a project rules table;
* the destination table name;
* read and write assignments;
* a sensitivity value; and
* upload or owner metadata.

An access-rules trigger can derive assignments from the upload form and the
associated entry in ``system.uploadings``. Records created through direct
SQL do not necessarily have the metadata required for this derivation.

A query template must also include the appropriate access-control fragments.
Correct rules in the database do not protect data if an application query
or external connection bypasses them.

For the access model, see :doc:`Data access <data_access>`.
For query-template configuration, see
:ref:`SQL query settings <sql-query-settings>`.

.. TODO: Document the authoritative permission-resolution algorithm from
   project settings through rules-table joins and column restrictions.

.. TODO: Verify whether access control is enforced in PostgreSQL, in
   generated application queries, or in both places for each supported
   interface.

.. TODO: Add tested examples comparing a form-based insertion with a direct
   SQL insertion in a group-restricted project.


Data output
===========

OpenBioMaps can expose project data through its web interface, maps, APIs,
exports, saved results, and external database clients. Each route must be
evaluated separately for access control, metadata, field naming, and output
format.


Web queries and maps
--------------------

The web application uses configured SQL query templates to assemble textual
and spatial query results. Templates can include placeholders for:

* selected fields;
* geometric filtering;
* additional module filters;
* taxonomic joins;
* upload metadata;
* access-rule joins; and
* other project-specific SQL fragments.

MapServer layers can use dynamically generated queries to render the same
project data on a map. The PostgreSQL query, MapServer mapfile, web-map
layer, and OpenBioMaps query configuration must remain consistent.

An incorrectly configured query can omit records, duplicate rows, expose
restricted fields, or bypass an expected access-rule join. Every query
configuration should be tested as:

* an unauthenticated visitor;
* a normal authenticated user;
* a member of each relevant group;
* a record owner or contributor; and
* an administrator.

For details, see :ref:`SQL query settings <sql-query-settings>` and
:ref:`Map settings <map-settings>`.


Exports
-------

Query results or complete tables can be exported in supported formats.
Small exports can be generated during an interactive request, while larger
exports can be delegated to a background job.

An export workflow should preserve or include:

* the selected records and fields;
* the applied filters;
* the query or export time;
* project and data-set metadata;
* licence and attribution information;
* applicable coordinate-reference information;
* provenance; and
* any sensitivity or reuse conditions that recipients must understand.

Generated files can remain accessible after the original user session ends.
Their storage location, download permissions, expiration, and cleanup are
therefore part of the security model.

.. TODO: Document which export paths apply the same row- and column-level
   restrictions as the web query interface.

.. TODO: Document the storage, naming, access control, expiration, and
   deletion of generated export files.


API access
----------

The OpenBioMaps API provides programmatic access to supported project
operations. API clients can retrieve form definitions, submit data, query
records, or perform other authorised operations depending on the API
version and granted scope.

An API submission using a published upload form should follow the
server-side form workflow. A direct database integration is not equivalent
to an API submission and can produce different metadata and trigger
behaviour.

For details, see :doc:`API documentation <api>`.


SQL clients and external applications
-------------------------------------

External SQL clients such as QGIS can connect directly to PostgreSQL when
the server and project operator explicitly provide credentials and network
access.

Direct database access can expose more information than the web interface
if PostgreSQL privileges, views, and row-level security do not reproduce the
application's access model. Application-level group membership and
column restrictions must not be assumed to apply automatically to arbitrary
SQL connections.

Prefer dedicated read-only database roles, restricted views, or an API over
sharing an administrative project account.

For supported integrations, see :doc:`Clients <clients>`.

.. TODO: Document the privileges granted to PostgreSQL users created through
   the OpenBioMaps profile or administration interface.

.. TODO: Clarify whether direct SQL clients are restricted by PostgreSQL
   row-level security, filtered views, ordinary grants, or another
   mechanism in the current implementation.


Users, roles, and database identities
=====================================

OpenBioMaps application users, project roles, groups, OAuth clients, and
PostgreSQL roles are related concepts but are not interchangeable.

``Application user``
   A person or service represented by an OpenBioMaps account.

``Project membership``
   Associates an application user with a particular project and status.

``Project group``
   Groups application users for form, data, module, or administrative
   access.

``Administrative role``
   Grants access to selected project-administration functions.

``OAuth client or token``
   Authorises a client application to act within granted scopes.

``PostgreSQL role``
   Controls direct database authentication and SQL privileges.

A user who can query a record through the web application does not
automatically have direct PostgreSQL access. Conversely, a PostgreSQL role
with broad table privileges can bypass restrictions implemented only in the
application.

Service accounts and automated integrations should use dedicated
credentials with only the privileges required for their function. Tokens
and database passwords should not be embedded in source code or shared
between unrelated applications.

.. TODO: Map application users, project memberships, groups, administrative
   permissions, OAuth identities, and PostgreSQL roles to the current
   database tables and authentication services.

.. TODO: Document account creation, credential rotation, revocation, expiry,
   and audit behaviour for every supported integration type.


Safe schema changes
===================

Changes to a managed table can affect both PostgreSQL and OpenBioMaps
configuration. Before renaming, replacing, or deleting a table or column:

#. identify upload forms that use the object;
#. search query templates and MapServer mapfiles;
#. inspect triggers, rules, views, indexes, constraints, and foreign keys;
#. inspect semantic column roles and project metadata;
#. inspect access-rule and history configuration;
#. identify modules and background jobs that refer to the object;
#. identify API, mobile, QGIS, R, and direct SQL clients;
#. create and verify an appropriate backup;
#. test the migration in a separate project;
#. define a rollback procedure; and
#. validate all supported interfaces after the migration.

Use the administration interface for operations it supports. If direct SQL
is necessary, update the corresponding OpenBioMaps metadata and dependent
configuration as part of the same controlled migration.

Renaming an object is not necessarily safer than deleting and recreating it:
both can break dependencies that store the original identifier as text.

.. TODO: Create supported migration procedures for adding, renaming,
   changing the type of, and deleting a managed column.

.. TODO: Create a supported procedure for replacing a managed table with a
   view and for reversing that change.

.. TODO: Add an administrative dependency report listing forms, query
   templates, modules, jobs, triggers, rules, map layers, and metadata that
   refer to a selected table or column.


Backups, archives, and reproducibility
=====================================

A complete OpenBioMaps project consists of more than its primary data
tables. Depending on the installation, restoration can require:

* project and system database tables;
* sequences, constraints, indexes, triggers, and rules;
* OpenBioMaps metadata;
* project configuration files;
* upload forms and their versions;
* attachments and generated derivatives;
* MapServer and web-map configuration;
* modules and local source files;
* background jobs and schedules;
* translations and message templates; and
* credentials or secrets restored through a separate secure process.

A PostgreSQL table dump alone may preserve observation records while losing
the configuration required to interpret, edit, query, or protect them.

Backups should be tested through restoration. Archives intended for
long-term reuse should also preserve documentation, licences, provenance,
software versions, and enough schema information to interpret the data
outside the original server.

For governance and retention considerations, see
:doc:`Data policy <data_policy>`.

.. TODO: Define the minimum set of database and file-system resources
   required for a complete project backup and restoration.

.. TODO: Add a versioned project-export format suitable for migration
   between compatible OpenBioMaps servers.


Technical verification checklist
================================

After creating or changing a project data workflow, verify that:

* every managed PostgreSQL object has the required OpenBioMaps metadata;
* system columns have the expected types, constraints, and defaults;
* sequences, keys, indexes, triggers, and rules are valid;
* form definitions refer to existing destination columns;
* form validation is also enforced appropriately on the server;
* upload metadata are created and linked to inserted records;
* attachments are linked to the intended records;
* direct imports receive appropriate provenance and access rules;
* history and taxonomic triggers produce the expected results;
* public and group-specific queries enforce row restrictions;
* restricted columns are absent from every unauthorised output;
* map layers and textual queries return consistent records;
* API and mobile submissions use the intended published form version;
* SQL roles cannot read or modify more data than intended;
* generated exports are protected and removed according to policy;
* background jobs run with the required dependencies and least privilege;
* backups include database data, configuration, and attachments where
  promised; and
* a restoration test reproduces a working and access-controlled project.

Document the tested OpenBioMaps version, project configuration, test users,
queries, and expected results. Repeat the checks after application updates,
schema migrations, or material changes to access policy.
