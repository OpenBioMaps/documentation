.. _data-policy:

Data policy
***********

An OpenBioMaps project should have a documented data policy describing how
data are collected, managed, reviewed, accessed, shared, retained, and
eventually archived or deleted. The policy helps contributors, project
administrators, data users, and external partners understand what they may
expect from the project and what responsibilities they have.

This page provides a framework for preparing a project-specific data policy.
It is not itself a complete policy and does not constitute legal advice. The
appropriate rules depend on the purpose of the project, the organisations
involved, the categories of data being processed, the server operator, and
the applicable law.

The technical access settings of an OpenBioMaps project should implement the
published policy, but they do not replace it. Conversely, a policy must not
promise restrictions, retention periods, backups, or services that are not
actually implemented and regularly verified.

For information about configuring technical permissions, see
:doc:`Data access <../data_access>`.


Relationship to other documents
================================

A project data policy may be accompanied by several related documents. Their
scope should be distinguished clearly.

``Data policy``
   Describes the governance and lifecycle of project data, including
   collection, quality control, access, reuse, retention, and
   responsibilities.

``Privacy notice``
   Explains how personal data are processed, identifies the relevant
   controller or controllers, and informs data subjects about their rights.

``Terms and conditions``
   Define the contractual rules for using the server, project, application,
   or related services.

``Cookie notice``
   Describes cookies or similar browser-side technologies used by the web
   application.

``Licence or data-use agreement``
   Defines what recipients may do with data and any conditions attached to
   access or reuse.

``Contributor agreement``
   Defines what a contributor is authorised to submit and what permissions
   they grant to the project.

One document can cover more than one of these subjects, but each rule should
have a clear scope. Server-wide terms do not automatically define the
governance policy of every project hosted on that server.

The public OpenBioMaps service provides examples of
`terms and conditions <https://openbiomaps.org/terms/>`_,
a `privacy notice <https://openbiomaps.org/privacy/>`_, and a
`cookie notice <https://openbiomaps.org/cookies/>`_. These documents are
examples for a particular service and must not be copied to another server or
project without checking the organisations, processing operations,
jurisdiction, dates, and contact details.

.. TODO: Identify the server-wide terms, privacy notice, and cookie notice
   that apply to projects hosted on each OpenBioMaps server. Explain which
   provisions are inherited by a project and which must be defined by the
   project operator.

.. TODO: Establish whether OpenBioMaps can store or display a
   project-specific data policy, privacy notice, terms, and licence through
   the administration interface. Document the applicable configuration
   fields, templates, and fallback order.


Preparing a project data policy
===============================

A data policy should be prepared before routine data collection begins. It
should be reviewed whenever the project purpose, database structure, access
model, participating organisations, external integrations, or legal
requirements change.

The policy should be written in language that its intended users can
understand. If a project operates in several languages, the policy should
state which version is authoritative and how translations are maintained.

At a minimum, the policy should answer the following questions:

* What is the project for?
* Which data does it collect?
* Who operates the project and who can be contacted?
* Who is authorised to submit, view, modify, validate, export, or publish
  data?
* How is data quality assessed and documented?
* Which records or fields are sensitive?
* Under which conditions can data be reused?
* How should the project and its contributors be cited?
* How long are data, attachments, logs, and backups retained?
* How can errors, rights concerns, security incidents, or removal requests be
  reported?
* How and when can the policy be changed?

.. TODO: Decide whether projects should be provided with a standard policy
   template, a checklist, or both. If a standard template is introduced,
   identify which clauses are mandatory and which are optional.


Scope and purpose
=================

The policy should begin by identifying the project and defining its purpose.
This helps determine which data are relevant and prevents data collected for
one purpose from being used silently for an incompatible purpose.

The scope should include:

* the public name and database identifier of the project;
* the scientific, conservation, educational, or operational purpose;
* the geographical, taxonomic, and temporal scope;
* the data tables and major data categories covered;
* the web, mobile, API, and external-client interfaces covered;
* any related databases or services;
* the intended users and beneficiaries; and
* activities that are explicitly outside the scope of the project.

If the project has experimental, test, and production environments, the
policy should clarify which environments contain real data and which rules
apply to each one.

.. TODO: Define the current OpenBioMaps terminology for an experimental,
   test, stable, archived, and discontinued project. Confirm whether these
   are formal project states implemented by the application or only
   governance concepts.

.. TODO: Add a short example scope statement for a biodiversity occurrence
   project and another for a monitoring project based on repeated
   observation events.


Definitions
===========

Terms used in the policy should be defined consistently. Depending on the
project, useful definitions may include:

``Project``
   The OpenBioMaps database, its configured interfaces, and the associated
   data-management workflow.

``Server operator``
   The organisation responsible for operating the OpenBioMaps server and
   its underlying infrastructure.

``Project operator``
   The person or organisation responsible for governing a particular
   project.

``Contributor``
   A person or organisation that submits data to the project.

``Data owner`` or ``rights holder``
   The person or organisation holding specified rights in submitted data.
   The exact meaning should be defined rather than assumed.

``Data steward``
   A person responsible for maintaining data and metadata according to the
   project policy.

``Validator`` or ``curator``
   A person authorised to review, annotate, accept, correct, or reject
   submitted data.

``Data user``
   A person or application that views, queries, downloads, or otherwise
   processes project data.

``Record``
   A row or logically connected set of rows representing an observation,
   event, taxon, location, sample, or other project entity.

``Attachment``
   A file associated with a record, such as a photograph, sound recording,
   document, or data file.

``Metadata``
   Information describing the project, its tables and columns, a data set,
   an upload, or an individual record.

``Personal data``
   Information relating to an identified or identifiable person, as defined
   by the law applicable to the relevant processing operation.

``Sensitive biodiversity data``
   Data whose disclosure could create a risk to a species, habitat,
   protected area, landowner, contributor, research activity, or
   conservation action.

Definitions should not imply that a project has acquired ownership of data
merely because it stores them. Copyright, database rights, confidentiality
obligations, employment agreements, and other rights can apply differently
in different jurisdictions.

.. TODO: Harmonise the terms ``project owner``, ``project founder``,
   ``project host``, ``operator``, ``administrator``, ``data owner``, and
   ``uploader`` across the OpenBioMaps documentation and user interface.

.. TODO: Obtain legal review of the terms ``data owner`` and ``ownership of
   data``. Where appropriate, replace them with more precise concepts such
   as rights holder, contributor, custodian, controller, or source.


Governance and responsibilities
===============================

A project can involve several organisations and administrative levels.
Responsibilities should be assigned explicitly rather than inferred from
technical permissions.

The policy should identify responsibility for:

* operating and securing the server;
* governing the project;
* defining the database structure and metadata;
* approving contributors and group membership;
* creating and maintaining upload forms;
* reviewing data-access rules;
* validating and correcting records;
* responding to data-subject and rights-holder requests;
* reviewing export or data-access requests;
* maintaining licences and attribution information;
* backups, restoration, and disaster recovery;
* incident response;
* retaining or deleting data;
* maintaining external integrations; and
* reviewing and publishing policy changes.

Administrative access should follow the principle of least privilege. For
example, user managers need not automatically receive permission to execute
SQL, edit background jobs, or export all attachments.

For an overview of assignable administrative functions, see
:doc:`Administrative settings <../admin_settings>`.

.. TODO: Create a responsibility matrix covering the server operator,
   project founder, project operator, administrator, data steward, curator,
   contributor, and data user.

.. TODO: Document which administrative actions are recorded in an audit
   trail and how long that audit information is retained.

.. TODO: Define a procedure for transferring responsibility when a project
   founder or operator leaves the participating organisation.


Data collection
===============

The policy should describe which data can be submitted, by whom, and through
which interfaces. OpenBioMaps projects may accept data through web forms,
file uploads, mobile applications, the API, direct database connections, or
automated imports.

For each collection workflow, document:

* the purpose of the collection;
* the expected data source;
* required and optional fields;
* permitted file and attachment types;
* applicable validation rules;
* required attribution and provenance;
* the legal or organisational authority to submit the data;
* whether anonymous or unauthenticated submission is allowed;
* the initial access classification of new records; and
* what happens when a submission is incomplete or rejected.

Contributors should submit only data that they are authorised to provide.
This includes checking rights and confidentiality obligations associated
with photographs, sound recordings, reports, data copied from another
database, and information about identifiable people.

Upload forms are described in :doc:`Upload form management
<../upload_forms>`.

.. TODO: Document whether OpenBioMaps can require contributors to accept a
   project-specific contributor agreement before submission and whether the
   accepted agreement version is recorded with the upload.

.. TODO: Define the behaviour and ownership or custodianship rules for data
   submitted without authentication. Confirm whether anonymous uploads are
   supported by all current interfaces.

.. TODO: Add guidance for importing data from external services such as
   GBIF or iNaturalist, including provenance, licence compatibility,
   duplicate detection, and subsequent updates.


Metadata and provenance
=======================

Data should be accompanied by enough metadata to make their meaning, source,
quality, and permitted use understandable.

Project-level metadata should normally include:

* the project title and description;
* responsible organisations and contacts;
* geographical, temporal, and taxonomic coverage;
* data collection methods;
* quality-control processes;
* access and reuse conditions;
* licences;
* preferred citations; and
* update frequency.

Table- and column-level metadata should explain the meaning, units, allowed
values, coordinate reference systems, taxonomic conventions, missing-value
representation, and any transformations applied to the data.

Record- or upload-level provenance may include:

* the contributor or source organisation;
* the collector or observer;
* the original record identifier;
* the submission and observation dates;
* the upload form or import process used;
* the source data set and its version;
* transformations performed during import;
* validation status; and
* links to derived or superseded records.

Descriptions entered for database tables and columns form part of the
project metadata. See :ref:`Database tables and columns
<database-columns>`.

.. TODO: Define the minimum metadata required for an OpenBioMaps project to
   be considered ready for production or publication.

.. TODO: Map OpenBioMaps project, table, column, upload, and record metadata
   to relevant standards such as Darwin Core, Ecological Metadata Language,
   DataCite, and ISO 19115 where applicable.

.. TODO: Document which provenance information OpenBioMaps records
   automatically and which fields must be added to the project schema.


Data quality and validation
===========================

The policy should explain that storing a record does not necessarily confirm
its correctness. It should define the available validation states and who
may assign or change them.

Quality controls may include:

* required-field and data-type validation;
* controlled lists and range checks;
* taxonomic-name validation;
* date and coordinate consistency checks;
* duplicate detection;
* verification of coordinate reference systems;
* review of attachments or supporting evidence;
* expert identification;
* automated spatial or temporal checks;
* comparison with external reference data; and
* contributor or reviewer comments.

Corrections should preserve relevant provenance. Where feasible, the project
should distinguish the originally submitted value from a later
normalisation, interpretation, or correction.

Published data should carry appropriate qualifications. The absence of a
warning or validation flag must not be presented as a guarantee of
accuracy, completeness, fitness for a particular purpose, or current
taxonomic interpretation.

.. TODO: Document the data-evaluation model implemented by OpenBioMaps,
   including record, upload, and user evaluations and the exact meaning of
   any numeric scores or validation states.

.. TODO: Explain whether record history stores previous and new values,
   editor identities, timestamps, and reasons for changes. Define who can
   inspect and restore historical values.

.. TODO: Add a recommended correction workflow covering reported errors,
   curator review, contributor consultation, correction, rejection,
   withdrawal, and notification of previous data recipients.


Access and disclosure
=====================

The policy should state which data are public, restricted to authenticated
users, restricted to groups, available only after approval, or accessible
only to project administrators.

OpenBioMaps can combine:

* project-level access settings;
* row-level access rules;
* column-level restrictions;
* group membership;
* administrative roles; and
* export-authorisation workflows.

The effective technical configuration should be tested using accounts
representing each relevant user group and, where public access is enabled,
without authentication.

For details of the available controls, see :doc:`Data access
<../data_access>`.

The policy should distinguish among:

* discovering that a record exists;
* viewing a record on a map;
* viewing its attributes;
* viewing its exact geometry;
* querying and filtering it;
* downloading it;
* viewing or downloading attachments;
* modifying or deleting it;
* obtaining it through the API;
* accessing it through SQL or an external application; and
* receiving it through an approved data request.

These actions can expose different amounts of information and need not have
the same permissions.

.. TODO: Document the exact OpenBioMaps permission-resolution algorithm and
   use it to create tested policy examples for public, authenticated, group,
   owner-only, and column-restricted data.

.. TODO: Confirm how attachment previews, attachment exports, API results,
   map layers, cached files, and direct SQL connections apply row- and
   column-level access rules.

.. TODO: Define a periodic access review procedure covering group
   membership, administrative permissions, API credentials, direct database
   accounts, and generated download links.


Sensitive biodiversity data
============================

Exact locations, collection methods, observer identities, or other
attributes can create risks for threatened species, habitats, landowners,
contributors, and conservation activities. A project should define how such
risks are assessed and which protections are applied.

Possible protections include:

* withholding selected fields;
* restricting entire records to specified groups;
* hiding exact geometry from public users;
* publishing generalised coordinates;
* delaying publication;
* requiring individual approval for exports;
* separating public and restricted attachments; and
* recording a reason and review date for the restriction.

Restrictions should be proportionate, documented, and reviewed. A record
should not remain restricted indefinitely merely because its status has
never been reassessed.

The rules table supports sensitivity-related values such as ``sensitive``,
``restricted``, ``no-geom``, and ``only-owner`` in some project
configurations. Their exact behaviour must be verified before relying on
them.

.. TODO: Confirm the complete list and precise effect of supported
   sensitivity values in the web interface, maps, queries, downloads, API,
   attachments, and write operations.

.. TODO: Document whether OpenBioMaps supports coordinate generalisation or
   only hides geometry. If generalisation is supported, describe the
   algorithm, precision, consistency, and treatment of derived exports.

.. TODO: Develop a sensitivity-assessment procedure identifying who can
   classify a record, which reasons can be used, how decisions are
   recorded, and when restrictions must be reviewed.

.. TODO: Add examples covering threatened species, active nests, private
   land, archaeological or cave locations, embargoed research, and
   contributor safety.


Personal data and privacy
=========================

Biodiversity data can contain personal data even when the project is not
primarily intended to collect information about people. Examples may include:

* contributor, observer, collector, validator, and photographer names;
* email addresses and user profile information;
* precise locations linked to a person's home or movements;
* mobile-application tracklogs;
* photographs, sound recordings, and free-text notes;
* IP addresses and application logs;
* record ownership and edit history; and
* comments or evaluations associated with users.

The applicable privacy notice should identify the relevant controller or
controllers, processing purposes, legal bases, data categories, recipients,
retention periods, international transfers, security measures, contact
details, and data-subject rights as required by the applicable law.

The project data policy should refer to the applicable privacy notice rather
than attempting to replace it. Statements about legal bases and statutory
rights should be reviewed by a qualified person for the relevant
jurisdiction.

Special care is required where data concern children, vulnerable people,
private residences, employee monitoring, continuous location tracking, or
special categories of personal data.

.. TODO: Determine the respective privacy roles and responsibilities of the
   server operator, project operator, participating organisations,
   contributors, and external service providers for each processing
   workflow.

.. TODO: Update and legally review the default privacy notice. The available
   example is dated 2022 and may not reflect current organisations,
   processing operations, technologies, retention periods, or applicable
   data-protection requirements.

.. TODO: Inventory all personal data processed by the current web
   application, mobile applications, API, authentication service, logs,
   background jobs, backups, email service, and external integrations.

.. TODO: Document how requests for access, correction, restriction,
   portability, objection, and deletion are received, authenticated,
   assigned, completed, and recorded.

.. TODO: Clarify how account deletion affects uploaded records, attribution,
   history, comments, evaluations, API tokens, active sessions, scheduled
   jobs, logs, backups, and copies already exported by other users.


Rights, licences, and permitted reuse
====================================

The policy should state what rights contributors must have in submitted
data and what permissions they grant to the project. It should also state
the licence or other conditions under which recipients can reuse data.

Different rights may apply to:

* individual observations;
* compiled databases;
* photographs and sound recordings;
* reports and other attachments;
* taxonomic or geographic reference data;
* map tiles and base maps;
* metadata;
* software and form definitions; and
* content imported from an external source.

A project should not describe data as open unless recipients have clear
permission to reuse them. Public visibility alone is not a licence.

Where several licences apply, exports should preserve enough information to
determine the applicable licence and attribution for each record or
attachment. Incompatible source licences should not be combined under a new
licence without permission.

.. TODO: Define the licences supported or recommended by OpenBioMaps for
   data, metadata, and media. Explain the differences among public access,
   restricted access, CC0, CC BY, CC BY-NC, and custom data-use agreements.

.. TODO: Document where project-, table-, upload-, record-, and
   attachment-level licence information can be stored and whether it is
   included automatically in exports and API responses.

.. TODO: Establish a procedure for resolving conflicting ownership,
   authorship, licence, confidentiality, or removal claims.

.. TODO: Legally review any rule that transfers rights in anonymously
   submitted data to the project operator. Ensure that the user interface
   presents the applicable terms before submission.


Citation and attribution
========================

The policy should provide a preferred citation for the project and explain
how contributors, source organisations, data sets, and OpenBioMaps should be
acknowledged.

A citation should normally identify:

* the data publisher or responsible organisation;
* the project or data-set title;
* the OpenBioMaps server or repository;
* a version, publication date, or query date;
* the date of access;
* a persistent identifier, where available; and
* the applicable licence.

Where a data set or saved query has a DOI or another persistent identifier,
that identifier should be preferred over a URL that may change.

Record-level attribution should be preserved when required by the applicable
licence or contributor agreement. Users should not be instructed to publish
personal contact details unnecessarily.

.. TODO: Define and implement a standard machine-readable citation format
   for OpenBioMaps projects, saved queries, and exports.

.. TODO: Confirm which OpenBioMaps objects can currently receive a DOI, how
   versions are frozen, and what changes remain possible after publication.

.. TODO: Add tested citation examples for a complete project, a filtered
   query, an API result, a downloaded attachment, and data aggregated from
   several contributors.


Data requests and exports
=========================

Some projects require users to request permission before downloading
restricted data. The policy should describe:

* who may submit a request;
* what information the requester must provide;
* which criteria are used to decide;
* who makes the decision;
* expected response times;
* permitted and prohibited uses;
* required security measures;
* whether onward sharing is allowed;
* expiry and deletion requirements;
* reporting and citation requirements; and
* the process for appeal, amendment, or renewal.

Decisions should be consistent and recorded. Exported files should contain
only the approved records and fields, and their download links should be
protected and expire after an appropriate period.

.. TODO: Document the Export or download-request module, including its
   workflow, roles, message templates, audit records, generated files,
   access checks, link expiry, and cleanup procedure.

.. TODO: Determine whether approval conditions can be stored with a request
   and presented to the requester before download.

.. TODO: Define how a project can notify previous recipients when exported
   data are corrected, withdrawn, reclassified, or found to present a
   conservation or privacy risk.


Sharing and external integrations
=================================

Data may leave the OpenBioMaps web interface through downloads, APIs, direct
SQL connections, QGIS, R, mobile clients, background jobs, interconnection
services, or publication to external repositories.

The policy should identify regular data recipients and integrations, the
data sent to them, the purpose, applicable access controls, update
frequency, licences, and deletion or correction process.

Automated publication should not expose fields that would be hidden from the
same user through the web interface. Credentials used by integrations
should be assigned only the required permissions and should be rotated or
revoked when no longer needed.

.. TODO: Inventory supported external interfaces and document whether each
   one applies project-, row-, and column-level restrictions consistently.

.. TODO: Define a procedure for approving, documenting, monitoring, and
   disabling automated data transfers.

.. TODO: Explain how corrections and deletions propagate to external
   services such as GBIF, iNaturalist, cached map layers, or replicated
   databases.


Retention, deletion, and archiving
==================================

The policy should define retention periods or review criteria for all major
information categories, including:

* active project records;
* rejected and withdrawn submissions;
* record history;
* taxonomic and validation annotations;
* user accounts and profiles;
* invitations and group membership;
* interrupted uploads and temporary files;
* attachments and generated thumbnails;
* comments, evaluations, and messages;
* data-access requests and decisions;
* generated exports and download links;
* application and server logs;
* background-job logs;
* API tokens and sessions;
* backups; and
* archived project versions.

Deletion from the active database does not necessarily remove information
from backups, external exports, logs, caches, or copies previously obtained
by users. The policy should explain these limitations accurately.

Where long-term scientific reproducibility requires preservation, deletion
may need to be replaced by restriction, pseudonymisation, withdrawal, or
publication of a tombstone record. Such decisions should be based on a
documented legal and scientific assessment.

.. TODO: Create a retention schedule for the default OpenBioMaps
   installation and identify which periods are configurable at server and
   project level.

.. TODO: Document the exact effect of deleting a record, upload,
   attachment, user account, group, project, and generated export.

.. TODO: Define a supported project-closure workflow covering final export,
   metadata publication, transfer to a new operator, read-only archiving,
   deletion, user notification, and removal of credentials.


Backups and restoration
=======================

A data policy should distinguish backups from archives.

A backup is maintained primarily to restore a system after accidental loss,
corruption, or technical failure. An archive is retained for long-term
preservation and continued interpretation of data. A backup is not a
substitute for a documented archive, and a successful backup job does not
prove that restoration will work.

The policy should state:

* which database objects and files are backed up;
* whether attachments are included;
* backup frequency;
* retention period;
* storage location and geographical jurisdiction;
* encryption and access controls;
* responsibility for monitoring backup success;
* restoration priorities and expected time frames;
* restoration testing frequency; and
* what happens to deleted or restricted data in retained backups.

The available example terms state that SQL project tables on certain
OpenBioMaps services are backed up daily and retained for two weeks, while
attachments are excluded. This must not be presented as a general
OpenBioMaps guarantee without verification for the server in question.

.. TODO: Confirm and document the current backup arrangements separately
   for every supported OpenBioMaps server type, including Docker
   installations and independently operated servers.

.. TODO: Add a tested backup and restoration procedure covering the
   PostgreSQL database, project configuration, uploaded attachments,
   generated files, message templates, modules, jobs, and map
   configuration.

.. TODO: Define recovery-point and recovery-time objectives and establish a
   schedule for documented restoration tests.


Security and incident response
==============================

The policy should summarise the organisational and technical measures used
to protect data without publishing information that would itself weaken
security.

Relevant controls may include:

* encrypted network connections;
* secure authentication and session handling;
* least-privilege group and administrative access;
* protected database and API credentials;
* server and dependency updates;
* logging and monitoring;
* backup protection;
* restrictions on executable background jobs;
* file-type and attachment controls;
* periodic access reviews; and
* vulnerability and incident management.

A documented incident procedure should define how suspected unauthorised
access, accidental publication, data loss, malicious uploads, compromised
credentials, or incorrect access rules are reported and handled.

.. TODO: Define the security responsibilities of the server operator and
   project operator, including patching, monitoring, credential management,
   access review, and incident communication.

.. TODO: Add an incident-response process covering detection, containment,
   evidence preservation, risk assessment, correction, notification,
   recovery, and post-incident review.

.. TODO: Document how project administrators can report a vulnerability
   securely without disclosing it through a public bug-reporting channel.


Changes to the policy
=====================

The policy should contain a version number, publication date, effective
date, responsible editor, and change history. Material changes should be
communicated before they take effect where required.

The project should define:

* who can approve a policy change;
* how affected users are notified;
* whether renewed acceptance is required;
* how acceptance is recorded;
* how previous versions remain accessible; and
* what happens if a contributor or user rejects the new terms.

Changes to technical access settings, licences, retention periods, purposes,
or responsible organisations should trigger a policy review.

.. TODO: Document whether OpenBioMaps can record the version of terms or
   policy accepted by each user and request renewed acceptance after a
   material change.

.. TODO: Define a versioning and publication process for server-wide and
   project-specific policy documents.


Suggested project-policy structure
==================================

A project-specific policy can use the following structure:

#. **Document information** — title, version, owner, approval date, effective
   date, and review date.
#. **Project identity and purpose** — project name, server, scope, and
   intended use.
#. **Contacts and responsibilities** — server operator, project operator,
   data steward, and request contacts.
#. **Definitions** — project-specific terminology.
#. **Data collected** — records, metadata, attachments, provenance, and
   personal data.
#. **Submission rules** — authorised contributors, accepted sources, and
   contributor responsibilities.
#. **Quality management** — validation, correction, history, and
   qualifications.
#. **Access classification** — public, authenticated, group-restricted,
   sensitive, and embargoed data.
#. **Rights and licences** — contributor permissions and recipient reuse.
#. **Citation and attribution** — preferred citations and persistent
   identifiers.
#. **Requests and external sharing** — exports, integrations, and approval
   workflows.
#. **Retention and archiving** — active retention, deletion, backups, and
   project closure.
#. **Privacy and security** — references to the privacy notice and incident
   process.
#. **Complaints and requests** — contacts and response procedure.
#. **Policy changes** — approval, notification, acceptance, and version
   history.

.. TODO: Convert this structure into a separately downloadable policy
   template with clearly marked mandatory and optional clauses.

.. TODO: Add example text only after each example has been checked against
   current OpenBioMaps functionality and reviewed for the jurisdictions in
   which it is intended to be used.


Implementation checklist
========================

Before publishing a project data policy, the project operator should verify
that:

* the project purpose and scope are accurate;
* responsible organisations and contacts are current;
* technical roles match the stated responsibilities;
* upload forms collect only intended data;
* required metadata and provenance are recorded;
* validation states and quality statements are understandable;
* public, authenticated, and group access have been tested;
* map, query, API, export, attachment, and SQL access behave consistently;
* sensitive records and fields receive the intended protection;
* licences and attribution are included in exports;
* personal-data processing matches the privacy notice;
* retention and deletion statements match actual system behaviour;
* backups include the promised database objects and files;
* a restoration test has been completed;
* external integrations are documented;
* incident and request contacts are monitored;
* the effective policy version is available to users; and
* a date has been set for the next review.

A policy should be tested against real workflows rather than reviewed only
as text. In particular, administrators should use representative accounts
to test upload, query, map, download, API, attachment, correction, and
deletion operations.

.. TODO: Develop an automated or administrator-assisted audit report that
   compares the published project policy with access settings, enabled
   modules, export paths, retention settings, and external integrations.


Open questions
==============

Several areas require confirmation in the OpenBioMaps application and
governance model before this page can be considered complete:

* the exact relationship between server operators and project operators;
* the authoritative definitions of project and data-management roles;
* the complete access-resolution algorithm;
* the storage and presentation of licences and policy versions;
* the scope and retention of audit and history information;
* the treatment of personal data embedded in biodiversity records;
* the exact deletion behaviour of each interface;
* backup coverage and restoration guarantees;
* the propagation of corrections and deletions to external systems; and
* the supported lifecycle for closing or transferring a project.

.. TODO: Resolve these questions with the OpenBioMaps maintainers, server
   operators, representative project administrators, and appropriate legal
   or data-governance specialists. Replace resolved TODO blocks with tested,
   version-specific documentation.
