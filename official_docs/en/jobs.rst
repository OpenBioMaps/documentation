:author: Miklós Bán
:date: 2026-08-09

.. _jobs:

Background jobs
***************

Background jobs are standalone programs that perform scheduled or manually
initiated tasks for an OpenBioMaps project. They are suitable for operations
that do not need to run as part of an interactive web request, such as data
validation, maintenance, imports, exports, spatial processing, and sending
notifications.

Jobs are commonly written in PHP, although an OpenBioMaps server may also
support Python, R, Bash, or another language installed and enabled by the
server administrator.

Project administrators can manage jobs through **Profile > Project
administration > Background jobs**. Depending on their permissions and the
server configuration, administrators can:

* install predefined jobs from the central job repository;
* upload project-specific jobs;
* configure job parameters;
* configure execution schedules;
* enable or disable jobs;
* start jobs manually;
* inspect recent execution results; and
* edit job source code.

For an overview of the administration interface and a system-level scheduling
example, see :ref:`Background jobs <background-jobs>`.


Job repository
==============

The predefined OpenBioMaps jobs are maintained in the
`OpenBioMaps web-app-jobs repository
<https://gitlab.com/openbiomaps/web-app-jobs>`_.

The repository can change independently of this documentation. Review the
source code and configuration of the selected version before installing or
updating a job.

The repository README describes the traditional PHP job layout. A PHP job
typically consists of two files with the same name:

* an executable file placed in ``jobs/run/``; and
* a supporting library file placed in ``jobs/run/lib/``.

Jobs written in other languages may consist only of an executable file in
``jobs/run/``. The exact installation layout can depend on the OpenBioMaps
version and server configuration.


Installing and configuring a job
================================

Where supported, a predefined job can be installed from the central
repository through the background-job administration interface. A
project-specific job can also be uploaded or installed manually by an
authorised server administrator.

After installing a job:

#. review its source code;
#. review and set all project-specific parameters;
#. confirm that referenced tables, columns, modules, templates, and
   directories exist;
#. use **Run** to execute the job manually;
#. wait for the execution to finish;
#. inspect the result and server logs;
#. verify any changes made to the database or file system; and
#. enable recurring execution only after the manual test succeeds.

Job parameters and database assumptions are implementation-specific. A job
created for one project may not work in another project without changes.


Scheduling
==========

Recurring jobs use the scheduler configured for the project. The server's
system-level scheduler must invoke the OpenBioMaps project scheduler
regularly; otherwise, configured jobs will not start automatically.

The central repository provides the following traditional cron example:

.. code-block:: console

   */5 * * * * /usr/bin/php /var/www/html/biomaps/projects/YOUR-PROJECT/jobs.php > /dev/null 2>&1

The command may need to run as the web-server user, commonly ``www-data``.
Paths, execution users, containers, and PHP commands vary between
installations. Docker installations normally invoke the project scheduler
inside the application container instead.

The system-level invocation interval limits the effective scheduling
resolution. For example, if the project scheduler is invoked every five
minutes, a job cannot reliably start every minute.

See :ref:`Scheduling jobs <background-jobs>` for the administration overview
and a Docker-oriented example.


Monitoring and troubleshooting
==============================

The background-job administration interface shows recent execution status
and output where supported. More detailed information may be available under
**Project administration > Server logs**.

When diagnosing a job, check:

* whether the project scheduler is invoked by the system scheduler;
* whether the job is enabled;
* whether its schedule is due;
* whether another execution is still running;
* whether the execution user can read and write the required files;
* whether required programs and language packages are installed;
* whether the configured tables and columns exist;
* whether database privileges are sufficient;
* whether temporary and export directories have enough free space; and
* whether application, background-job, PHP, container, or system logs contain
  an error.

A job can complete without producing the intended result if its configuration
does not match the project schema. Validate the resulting records, files, or
notifications rather than relying only on a successful exit status.


Security
========

Installing or editing a job is equivalent to installing executable code on
the server. These functions must be restricted to trusted administrators.

Before installing a custom or updated job, review it for:

* SQL injection;
* operating-system command injection;
* unsafe file paths and file permissions;
* disclosure of database credentials or personal data;
* unbounded database queries;
* unbounded memory, CPU, or disk use;
* insecure network requests;
* missing access-control checks;
* unsafe handling of attachments and archives; and
* unintended repeated execution.

Create an appropriate backup before running jobs that update or delete data.
Export jobs must apply the project's data-access and privacy requirements to
the generated files. Generated archives and reports should be stored in a
protected location and removed when they are no longer required.


Jobs in the central repository
==============================

The following job directories are present in the central repository. Some
jobs are general-purpose, while others were developed for a particular
project or workflow.

The descriptions below summarise the purpose indicated by the repository
names and available repository metadata. Exact behaviour, configuration
parameters, database changes, notification recipients, and error handling
must be verified in the source code of the version being installed.


General data and file processing
--------------------------------

``clean_temp``
   Cleans temporary data or files created by OpenBioMaps workflows. Review
   the configured paths, tables, retention rules, and deletion conditions
   before enabling it. An incorrect cleanup configuration can remove files
   or data that are still required.

``export_attachments``
   Creates an export from project attachments. This job can be used by
   workflows that prepare attachment archives in the background. Verify how
   records are selected, how access rules are applied, where the archive is
   written, and how long it remains available.

``export_data``
   Creates a background data export. The selected tables, columns, filters,
   output format, access checks, output location, and download mechanism
   depend on the job configuration and source version.

``intersect_data``
   Performs a spatial intersection workflow between configured data sets.
   Verify the source and target tables, geometry columns, spatial reference
   systems, and update behaviour before running it.

``valid_list_values``
   Checks or processes values associated with configured list fields. Review
   the source to determine whether invalid values are only reported or are
   also modified.


Observation-list processing
---------------------------

``observation_lists``
   Processes observation lists using the standard observation-list workflow.
   Its database assumptions and treatment of temporary data must be checked
   against the project schema.

``observation_lists_without_temp``
   Provides an observation-list processing variant intended for workflows
   that do not use the standard temporary-data stage.

``incomplete_observation_lists``
   Processes incomplete observation lists. The workflow may use the
   ``incomplete_list_processed`` and ``incomplete_list_unprocessed`` message
   templates to report whether processing succeeded. Verify the actual
   template usage and recipients in the installed source version.


Taxonomic processing
--------------------

``species_name_validation``
   Validates scientific names used by project data. Review the configured
   taxon table, source fields, accepted-name rules, and whether the job only
   reports problems or also changes records.

``superspecies_autonames``
   Generates or maintains names used by a superspecies workflow. This job
   depends on project-specific taxonomic conventions and should not be
   enabled without reviewing its configured tables and naming rules.

``linnaeus_job``
   Implements a Linnaeus-related, project-specific processing workflow. Its
   exact taxonomic operation and required schema are not described by the
   repository overview and must be determined from its source and
   configuration.


Imports and external integrations
---------------------------------

``iNatHarvester``
   Harvests observation data from iNaturalist for import or processing in an
   OpenBioMaps project. Review the remote API settings, taxon and user
   mappings, duplicate detection, geographic filters, rate limiting, and
   destination-table configuration before use.

``hunviphab_tracklogs``
   Processes tracklogs for the HunVipHab workflow. This is a specialised job
   whose required tables, tracklog format, and output fields must be
   confirmed from the source.

``chirovox_rename``
   Performs a rename operation for the ChiroVox workflow. Review the source
   to identify the affected files or records, the naming convention, and
   collision handling before running it.


Database maintenance and custom SQL
-----------------------------------

``sql_daily``
   Runs configured SQL as a recurring maintenance or processing task. SQL
   jobs can modify or delete arbitrary project data, so inspect every
   statement, test it in a non-production environment, and create a backup
   where appropriate.

``sql_maintenance``
   Performs PostgreSQL maintenance using ``ANALYZE`` and/or ``VACUUM``.
   These operations update planner statistics and reclaim or make reusable
   storage associated with obsolete row versions. Review the selected
   relations and options, and coordinate resource-intensive maintenance with
   the server administrator.


Project-specific workflows
--------------------------

``kaszalasi_bejelento``
   Implements a project-specific mowing-report workflow. This variant
   includes notification-related processing. Confirm the affected records,
   message templates, recipients, and conditions from the source before use.

``kaszalasi_bejelento_ertesites_nelkul``
   Implements a variant of the mowing-report workflow without notifications.
   Other data-processing behaviour may be shared with
   ``kaszalasi_bejelento`` and must be verified in the source.

``telepules_hozzarendeles``
   Assigns a municipality or settlement to configured records. This is
   likely to depend on spatial data and project-specific fields. Verify the
   boundary data, geometry columns, spatial reference systems, matching
   rules, and handling of records outside or on the boundary of a
   municipality.


Development and testing
-----------------------

``job_teszt``
   A test job intended for checking job installation or execution. It should
   not be treated as a production data-processing job without reviewing its
   source.


Updating jobs
=============

Updating a job can change its required parameters, database assumptions, and
side effects. Before replacing an installed version:

#. preserve the current source and configuration;
#. review the changes in the central repository;
#. check for schema migrations or new dependencies;
#. disable the recurring schedule;
#. install the update in a test project where possible;
#. run it manually and inspect the result; and
#. restore the schedule only after validation.

Local modifications may be overwritten by an update from the central
repository. Keep project-specific changes under version control or maintain
them as a separate custom job.


Writing custom jobs
===================

A custom job should:

* have a clearly documented purpose;
* validate all configuration before changing data;
* use parameterised SQL;
* avoid embedding credentials in source code;
* log enough information to diagnose failures without exposing sensitive
  data;
* return a non-zero exit status on failure where supported;
* be safe to retry or clearly document when it is not;
* prevent or safely handle overlapping executions;
* use bounded queries and resource limits;
* clean up temporary files after successful and failed runs; and
* document all database, module, executable, and language-package
  dependencies.

Where possible, test custom jobs in a separate project with representative
data before installing them in production.
