Frequently Asked Questions
**************************

General information
===================

What is OpenBioMaps?
--------------------

OpenBioMaps is an open-source software platform and collection of services
for managing biological data. It can be used to create database-backed
projects that multiple users can access simultaneously from different
devices and with different permission levels.

Organisations can operate their own OpenBioMaps server. Some institutions
also provide hosted OpenBioMaps services for research or citizen-science
projects, so projects do not necessarily need to maintain their own server.
Availability, eligibility, and support conditions depend on the hosting
institution.

What is the OpenBioMaps Consortium?
-----------------------------------

The OpenBioMaps Consortium coordinates cooperation around the platform and
its development.

See :doc:`The OpenBioMaps Consortium <consortium>` for more information.

Where can I find existing OpenBioMaps servers?
----------------------------------------------

Registered servers are listed in the
`OpenBioMaps network database
<https://openbiomaps.org/projects/openbiomaps_network>`_.

The list may not include every independently operated OpenBioMaps server.

Projects and registration
=========================

How can I find or create a database project?
--------------------------------------------

Existing projects can be found through the project list of an OpenBioMaps
server or through information provided by the organisation operating that
server.

If you are already a member of a project, the server may allow you to request
or create another database project through the web interface. The exact
procedure and required permissions depend on the server configuration. Contact
the server administrator if the project-creation function is not available to
your account.

How can I register for an OpenBioMaps project?
----------------------------------------------

Registration normally requires an invitation. Depending on the project
configuration, existing members or only administrators may be permitted to
invite new users.

A project may also provide an invitation-request form on its login page. This
allows prospective users to ask the project administrators for access, but
submitting a request does not automatically grant membership.

Some servers support registration or login through an external OpenID Connect
provider, such as Google. The providers available and whether a new account
can be created through them depend on the server and project configuration.

For information about joining a particular project, contact its creators or
administrators.

Data upload and access
======================

How can I upload data?
----------------------

The standard method is to use a project-specific data upload form. Forms can
be used through the web interface and, when supported by the project, through
an OpenBioMaps mobile application.

See :doc:`Upload form management <upload_forms>` for information about form
configuration.

Large or specialised imports can also be performed with a PostgreSQL client.
Direct database imports should be carried out only by experienced users with
the necessary permissions because they can bypass application-level
validation and upload workflows.

How can I access data?
----------------------

Depending on the project configuration and your permissions, data can be
accessed in several ways:

* through map or text queries in the web interface;
* through downloads and exports in the web interface;
* through data-sharing functions;
* with a PostgreSQL client;
* with QGIS or another compatible GIS client;
* through an OpenBioMaps API;
* with the OpenBioMaps R package; or
* with the :doc:`PWA map-query application <pwa>`.

See :doc:`Data access <data_access>`, :doc:`API documentation <api>`, and
:doc:`Clients <clients>` for more information.

Which data download options are available?
------------------------------------------

Available download methods depend on the modules enabled for the project and
the current user's permissions. They may include:

* CSV, JSON, KML, GPX, SHP, and other export modules;
* access through QGIS or another PostgreSQL/PostGIS client;
* bookmarks, saved queries, and permanent links;
* API-based retrieval; and
* the OpenBioMaps R package.

Some projects require approval before a download is made available. Exports
remain subject to the project's row-level and column-level access rules.

Why can other users see data that I cannot query?
-------------------------------------------------

The records are probably restricted to specific users or groups. A project's
upload-form settings can define who receives read or modification access to
records uploaded with that form.

If records are uploaded without suitable access settings, they may be visible
only to project administrators. Project administrators can change access
rules later, but the exact procedure depends on the project's database schema
and rules configuration.

The following is an illustrative SQL example for adding the numeric role ID
``295`` to the read-access array of selected records:

.. code-block:: sql

   UPDATE mydatabase_rules AS rules
   SET read = rules.read || 295
   FROM (
       SELECT data.obm_id AS row_id
       FROM public.mydatabase AS data
       LEFT JOIN mydatabase_rules AS existing_rules
           ON data.obm_id = existing_rules.row_id
       WHERE data.observer ILIKE 'Smith%'
   ) AS selected
   WHERE selected.row_id = rules.row_id;

Replace all table names, column names, conditions, and role IDs with values
appropriate for the project.

This example updates only records that already have a corresponding rules
row. It does not create missing rules. It may also append the same role more
than once if that role is already present.

Create a backup and inspect the affected rows before running an access-rule
update. Whenever possible, perform the change through a supported
administration interface. Incorrect SQL changes can unintentionally disclose
or restrict project data.

Mobile access
=============

How can I retrieve data with a mobile device?
---------------------------------------------

The :doc:`PWA map-query application <pwa>` can query project records and make
previously fetched records available offline. Its availability and
configuration depend on the project.

OpenBioMaps also provides mobile applications for field data collection. See
:doc:`Mobile applications <mobile_applications>` for the available options.

How do I use the OpenBioMaps mobile application?
------------------------------------------------

The offline mobile application is designed for Android and iOS devices. To
begin using it:

#. Select the OpenBioMaps server that hosts your project.
#. Select the project.
#. Log in with your project account.
#. Open the required data collection forms while online so that they are
   downloaded to the device.
#. After the forms have been downloaded successfully, use them for offline
   data collection.
#. Reconnect to the network and synchronise the collected records with the
   server.

The servers and projects displayed by the application depend on the
registered servers, server configuration, and the user's access permissions.

Previously viewed base-map tiles may remain available in a device or browser
cache, but offline base-map availability is not guaranteed unless the
application and map provider explicitly support downloading maps for offline
use.

See :doc:`Mobile applications <mobile_applications>` for detailed
instructions and limitations.

How can I access photos captured with the mobile application?
-------------------------------------------------------------

Depending on your permissions and the project's configuration, attachments
can be accessed:

* individually from a record's data-sheet page;
* from the files tab of the project administration interface;
* through the available bulk-download function;
* through an API that supports attachment downloads; or
* through the project file-management functions available to authorised
  administrators in Supervisor.

The exact options depend on the enabled modules and OpenBioMaps version.
Photos may contain sensitive location, project, or personal information, so
downloaded files must be stored and shared securely.

Developer interfaces and clients
================================

Is there a programmable interface for developers?
--------------------------------------------------

Yes. OpenBioMaps provides APIs for accessing project and user data, subject to
authentication and project permissions.

The Project Data Service (PDS) supports URL-based requests. For example, the
following request returns the available project list on a server:

``https://openbiomaps.org/pds.php?scope=get_project_list``

See the :doc:`API documentation <api>` for supported endpoints,
authentication requirements, parameters, and response formats.

Where can I find the OpenBioMaps R package?
-------------------------------------------

The development version of the OpenBioMaps R package is available in the
`OpenBioMaps obm.r repository <https://github.com/OpenBioMaps/obm.r>`_.

Check the repository documentation for installation instructions, current
status, and compatibility information before using it in a production
workflow.

Languages and contributions
===========================

Which languages does OpenBioMaps support?
-----------------------------------------

OpenBioMaps is designed to support translated user interfaces and
project-specific content. The completeness of each translation can differ
between application components and releases.

The platform currently includes translations for several languages, including
Hungarian, English, Romanian, Spanish, Portuguese, Russian, German, and
French. Some translations may be incomplete.

Individual projects can select their own languages and provide translations
for project-specific labels and content.

Translations can be contributed through the
`OpenBioMaps translation platform <https://translate.openbiomaps.org>`_.

How can I contribute to OpenBioMaps?
------------------------------------

You can contribute by:

* creating or maintaining an OpenBioMaps database project;
* collecting or uploading data to a project;
* operating an OpenBioMaps server;
* hosting projects on your server;
* adding new translations or improving existing ones;
* improving documentation;
* reporting and investigating issues;
* contributing software development; or
* providing financial support.

Before contributing data or code, review the relevant project's policies and
the contribution requirements of the corresponding source-code repository.

Do I have to pay to use OpenBioMaps?
------------------------------------

OpenBioMaps software is open source and can be used without a software licence
fee. However, operating a server, developing project-specific features,
hosting data, providing support, and maintaining infrastructure may involve
costs.

Some institutions host eligible projects free of charge, while others may
apply their own conditions or service fees. Contact the relevant server
operator for details.

Development and maintenance include both voluntary and funded work. Financial
and in-kind contributions to OpenBioMaps development are welcome.

Storage, backup, and account recovery
=====================================

Where does OpenBioMaps store data?
----------------------------------

Each OpenBioMaps server stores its project data in its own PostgreSQL
databases and file storage. This can include database records, attachments,
project configuration, map files, logs, and generated exports.

OpenBioMaps does not maintain a single central database containing all data
from every server.

Is there a backup solution?
---------------------------

There is no centralised backup service for all OpenBioMaps installations
because data management is decentralised. Each server operator is responsible
for implementing, monitoring, and testing an appropriate backup procedure.

Some server operators cooperate by storing encrypted or access-controlled
archives on one another's infrastructure. Backup arrangements vary between
servers.

Project owners should ask their server operator about:

* backup frequency and retention;
* whether databases, attachments, and configuration files are included;
* off-site storage;
* encryption and access control; and
* how often restoration is tested.

A backup should not be considered verified until it has been restored
successfully in a test environment.

I have lost my password. How can I set a new one?
-------------------------------------------------

Use the **Lost password** link on the login page.

Enter the email address associated with your account and submit the form. If
the server can send email and the address belongs to an account, the system
will send a link that can be used to access the account and set a new
password.

If the message does not arrive:

* check the spam or junk folder;
* verify that you entered the correct email address;
* wait a few minutes before requesting another message; and
* contact the project or server administrator.

For security reasons, the interface may not confirm whether an email address
is registered.

Troubleshooting
===============

Why do pink squares appear on the map?
--------------------------------------

Pink squares usually indicate that a map tile or layer could not be rendered.
Possible causes include:

* an error in a MapServer mapfile;
* an invalid or unavailable data source;
* incorrect database credentials or network settings;
* a projection or geometry problem;
* an incorrect layer name;
* a MapServer or MapCache error; or
* an invalid map-query configuration.

Try reloading the page and checking whether the problem affects every layer or
only one layer. Project or server administrators should inspect the
application and MapServer logs and validate the affected mapfile.

Data management
===============

How can I delete data?
----------------------

The standard OpenBioMaps web interface may not provide a general-purpose
record deletion function. When deletion is necessary, an authorised database
administrator can remove records through SQL or another supported
administrative workflow.

Each upload has a corresponding entry in the system upload metadata. Records
in a project table can refer to that upload through an upload identifier. If
a correctly configured foreign key with cascading deletion connects the
metadata and data tables, deleting the metadata row may also delete the
related records. This relationship is not guaranteed to exist, so do not rely
on cascading deletion without inspecting the database schema.

It is usually safer to identify and explicitly delete the required records.
For example:

.. code-block:: sql

   DELETE FROM your_table
   WHERE uploading_id = x;

Replace ``your_table``, ``uploading_id``, and ``x`` with the actual table,
upload-reference column, and upload ID used by the project.

Before executing a deletion:

#. Create and verify a database backup.
#. Run an equivalent ``SELECT`` query and inspect every row that would be
   affected.
#. Check related tables, attachments, rules, and audit requirements.
#. Run the operation in a transaction where practical.
#. Verify the result before committing the transaction.
#. Record who performed the deletion and why.

Deletion can affect audit history, access-rule rows, attachments, linked
records, summaries, and external copies. Consult the project's data policy
and retention requirements before permanently removing data.

RUM openness model
==================

What is RUM?
------------

RUM is part of the RUM/FILH model for describing the operational capabilities
and openness of biodiversity databases. See the publication
`RUM/FILH: a standardized operational capability model for biodiversity
databases <https://doi.org/10.1093/database/baag044>`_.

RUM stands for:

* **R — Read**
* **U — Upload**
* **M — Modify**

Each capability can have one of three values:

.. list-table::
   :header-rows: 1
   :widths: 15 30 55

   * - Value
     - Meaning
     - Traditional display colour
   * - ``-``
     - Not public
     - Black
   * - ``0``
     - Partially public
     - Red
   * - ``+``
     - Public
     - Green

For example, a database can provide partially public read access, public
upload access, and no public modification access. The three capabilities
should always be interpreted together with the project's detailed access
policy.

DOIs and citation
=================

Can a DOI be assigned to a database?
------------------------------------

Yes. A database or a defined dataset in a sufficiently stable and documented
state can be assigned a DOI through the DataCite DOI service, subject to the
procedure of the organisation operating the OpenBioMaps server.

OpenBioMaps databases can provide a DOI metadata page. For example:

``https://dinpi.openbiomaps.org/projects/danubefish/index.php?metadata``

The OpenBioMaps DataCite prefix is ``10.18426``. DOI suffixes are generated
uniquely.

A project can also assign additional DOIs to individual datasets. Before
minting a DOI, verify the dataset version, authors, title, publication year,
licence, access conditions, publisher, and landing-page persistence. A DOI
should resolve to a stable landing page containing sufficient metadata and
access information.
