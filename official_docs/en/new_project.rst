.. _new-project:

Creating a new OpenBioMaps project
==================================

An authorised member of an existing OpenBioMaps project can create a new
database project using the **Founding new project** form.

The new project is independent of the project from which it is created. The
founder becomes its initial owner and, until other users are invited, its
only member.

.. TODO: Document which permission is required to create a project and
   provide the current navigation path to the **Founding new project**
   form. Confirm whether project creation can be disabled at server level.


Before creating a project
-------------------------

Before completing the form, please consider the following:

* the purpose and scope of the project;
* the information that the project will manage;
* the required database tables and relationships;
* who should be able to view, submit, and modify data;
* whether any personal or sensitive biodiversity data will be processed; and
* the people responsible for project administration and data management.

For guidance on planning the data structure and governance of a project,
see:

* :doc:`Getting started <getting_started>`;
* :doc:`Data collection <data_collection>`;
* :doc:`Data management <data_management>`; and
* :doc:`Data policy <data_policy>`.


Completing the project-creation form
------------------------------------

The form requests the following settings.


Project identifier
..................

Enter a unique, short identifier for the project. This identifier is used
in the project URL and can also be used as a prefix or identifier in the
project's database configuration.

Use a short name consisting of lowercase letters, numbers, and underscores.
Avoid spaces, accented characters, punctuation, and quoted SQL identifiers.
Choose the identifier carefully because changing it after the project has
been created can affect URLs, database objects, configuration files, API
clients, and external integrations - so it is almost impossible.

.. TODO: Confirm the exact permitted characters, minimum and maximum length,
   uniqueness scope, and reserved identifiers. Document whether the project
   identifier is always used as the name or prefix of database tables.

.. TODO: Document whether renaming a project is supported. If it is,
   describe the complete migration procedure and its effect on URLs,
   database objects, map configuration, jobs, API clients, and external
   integrations.


Project title
.............

Enter a short, descriptive title for the project. This title appears in the
project header and other user-facing locations.

The title can be translated after the project has been created. Keep it
concise; two or three words are often sufficient, although a longer title
can be used where needed for clarity.

For information about project descriptions and translations, see:

* :ref:`Project description <project-description>`; and
* :ref:`Local translations <localisation>`.


Project description
...................

Enter a detailed description of the project and its purpose. The description
should help prospective contributors and data users understand:

* what the project collects;
* its geographical, temporal, and taxonomic scope;
* the organisations or people responsible for it;
* how the data are intended to be used; and
* where users can obtain further information.

The description can be updated after the project has been created.


Default data access
...................

Select the initial rules for viewing and modifying project data. These
settings determine the project's default access level.

A closed or group-restricted project can define more detailed row- and
column-level access rules after creation. The default settings can also be
changed later, but changes must be tested carefully to ensure that they do
not expose restricted data or prevent authorised users from accessing it.

For a description of the available access controls, see
:doc:`Data access <data_access>`.

.. TODO: Document the exact access options displayed on the
   project-creation form and map each option to the corresponding
   ``ACC_LEVEL`` and ``MOD_LEVEL`` configuration values.

.. TODO: Confirm whether changing the project-level defaults affects
   existing records or only changes how the current access rules are
   evaluated.


Initial map centre
..................

Specify the initial centre of the project's map. This setting determines the
area shown when users first open the map page.

The map centre can be changed later through the map-related administration
interface.


Map coordinate reference system
................................

Specify the spatial reference identifier (SRID) used by the project's base
map. The default is EPSG:4326 (WGS 84). Spatial reference systems can be
looked up at https://spatialreference.org/.

Use a different SRID only when the project has a clear technical requirement
for it and all relevant components support it. The configured reference
system must be compatible with the project's spatial data, OpenLayers
configuration, MapServer layers, query templates, exports, and external
clients.

Changing an SRID does not necessarily transform existing coordinates.
Assigning an incorrect SRID can place geometries in the wrong location or
make spatial queries invalid.

For related configuration information, see
:ref:`Map settings <map-settings>`.

.. TODO: Confirm whether this field defines the base-map projection, the
   project geometry SRID, the web-map display projection, or a combination
   of these. Document where coordinate transformations occur.


Creating the project
--------------------

After the form has been completed and submitted, OpenBioMaps creates the
project with an experimental status. This status informs users that the
project structure and configuration are still being developed; it does not
by itself prevent the project from operating.

.. TODO: Define the supported project states, their exact meaning, and how
   an administrator changes a project from experimental to testing, stable,
   archived, or another available state. Confirm whether a project state
   affects any application behaviour.

During project creation, the system creates the required configuration and
database objects. When the process finishes, it displays a message
containing the name and password of the project's SQL administrator.

Store these credentials in an approved password manager or another secure
location. Do not send them through unencrypted email, include them in
documentation, or commit them to a source-code repository. The SQL
administrator can modify or delete project data and database objects.

.. TODO: Document whether the generated SQL administrator password can be
   displayed again, rotated through OpenBioMaps, or recovered through the
   Supervisor. Add the recommended credential-rotation procedure.

The founder can access the new project using the same OpenBioMaps username
and password used in the original project. SQL administrator credentials
are separate from the founder's web-application credentials and should be
used only for database-administration tasks that require them.


Initial database structure
--------------------------

When the project is created, OpenBioMaps creates an initial project data
table containing the system columns required by that OpenBioMaps version.
The initial table can then be extended with project-specific columns, and
additional tables or views can be registered through the administration
interface.

Do not delete or rename system columns merely because they appear unused.
Upload processing, access rules, history, attachments, modules, or external
clients may depend on them.

For technical details, see:

* :ref:`Database tables and columns <database-columns>`; and
* :doc:`OpenBioMaps data flow and database integration <obm_workflow>`.

.. TODO: Document the exact objects created for a new project, including
   databases, schemas, tables, system columns, sequences, rules tables,
   roles, configuration files, mapfiles, directories, and default modules.


Configuring the new project
---------------------------

A newly created project requires additional configuration before routine
data collection or public use begins.

A typical setup process includes the following steps:

#. **Define the data model.**

   Add the required columns to the initial data table and create or register
   any additional tables, views, relationships, constraints, indexes, and
   metadata.

   See :ref:`Database tables and columns <database-columns>`.

#. **Configure access rules and groups.**

   Create the required user groups and verify project-, row-, and
   column-level access using representative user accounts.

   See :doc:`Data access <data_access>` and
   :ref:`Groups <group-settings>`.

#. **Create upload forms.**

   Define separate forms for the required web, file-upload, API, or mobile
   workflows. Configure obligatory fields, validation, defaults, access
   assignments, and published form versions.

   See :doc:`Upload form management <upload_forms>`.

#. **Configure SQL query templates.**

   Create the query templates used by textual queries and spatial map
   layers. Include the required access-control and module placeholders.

   See :ref:`SQL query settings <sql-query-settings>`.

#. **Configure the map interface.**

   Define the initial map view, base maps, overlay layers, MapServer
   configuration, coordinate reference systems, styles, and connections
   between map layers and query templates.

   See :ref:`Map settings <map-settings>`.

#. **Enable and configure modules.**

   Install or enable only the modules required by the project. Common
   query and visualisation modules can include ``text_filter``,
   ``identify_points``, ``results_asStable``, ``results_buttons``, and
   ``results_summary``, depending on the OpenBioMaps version and project
   requirements.

   See :doc:`Modules <modules>`.

#. **Configure supporting workflows.**

   Where required, configure history, access-rule and taxonomic triggers,
   message templates, background jobs, attachment handling, translations,
   and external integrations.

   See :ref:`Functions <trigger-functions>` and
   :doc:`Background jobs <jobs>`.

#. **Add project information and governance documents.**

   Review the project title and description, responsible organisations,
   contact information, data policy, privacy information, licences,
   attribution requirements, and terms of use.

   See :doc:`Data policy <data_policy>`.

#. **Test the complete workflow.**

   Submit representative records through every supported client. Test valid
   and invalid values, attachments, geometries, interrupted uploads,
   validation, history, access restrictions, queries, maps, API responses,
   exports, and deletion or correction procedures.

#. **Prepare backups and monitoring.**

   Confirm that the database, attachments, configuration, modules, jobs, and
   map settings are covered by the intended backup procedure. Test
   restoration before making commitments about recoverability.


Pre-release checklist
---------------------

Before inviting routine contributors or making the project public, verify
that:

* the data model represents the intended collection methodology;
* every table and column has meaningful metadata;
* upload forms use the intended published versions;
* validation is enforced on the server where required;
* public and restricted access have been tested independently;
* sensitive locations and personal data receive the intended protection;
* map and textual queries return consistent records;
* downloads and API responses contain only authorised fields;
* licences, attribution, and citation guidance are available;
* administrators and data stewards have clearly assigned responsibilities;
* background jobs and notifications have been tested;
* generated files and interrupted uploads have a cleanup procedure;
* server and project logs can be inspected by authorised administrators;
* backups include all promised data and files; and
* a restoration test has been completed successfully.

Keep the project in an experimental or testing state until the structure,
access model, data-entry workflows, and recovery procedure have been
validated.
