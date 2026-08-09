:author: Miklós Bán
:date: 2026-08-09

Data collection
***************

Biodiversity data collection records the occurrence, abundance, condition,
or other characteristics of living organisms together with the context in
which the information was obtained. This context commonly includes the
location and time of collection, the observer or data source, the sampling
method, and the amount of sampling effort.

The design of a data-collection process determines which scientific
questions the resulting data can support. A record of a species occurrence
may document that the species was detected at a particular place and time,
but estimating absence, abundance, distribution, or temporal change
generally requires a structured sampling design and information about
sampling effort [MacKenzie2002]_ [Isaac2014]_.

OpenBioMaps does not prescribe a single data model or sampling protocol.
Instead, it provides configurable database tables, data-entry forms,
validation rules, spatial fields, and access controls that can be adapted to
different biodiversity projects. The sampling design and the meaning of the
recorded fields must therefore be defined by the project before its database
and forms are configured.

This page provides general guidance for connecting a biodiversity
data-collection design to an OpenBioMaps project. Detailed instructions for
configuring forms are provided in
:doc:`Upload form management <upload_forms>`.


Planning a data collection
==========================

Before creating database tables or data-entry forms, define the purpose of
the collection and the questions the data are expected to answer. Important
design decisions include:

* which organisms, taxonomic groups, habitats, or environmental variables
  will be recorded;
* whether observations will be collected opportunistically or according to
  a predefined protocol;
* whether non-detection or zero-observation events must be retained;
* which spatial and temporal units will be used;
* whether sampling effort, methodology, and environmental conditions must
  be recorded;
* whether sampling will be repeated at the same locations;
* who will collect, validate, manage, and use the data;
* which controlled vocabularies and taxonomic references will be used; and
* which metadata and provenance information must be preserved.

These decisions should be made before the technical structure of the
database is finalised. Adding a missing field later may allow new
information to be collected, but it cannot reconstruct contextual
information that was not recorded during previous surveys.

Projects intended to contribute to wider biodiversity assessments should
also consider how their observations relate to established concepts and
standards. Essential Biodiversity Variables provide one framework for
connecting local observations to broader biodiversity monitoring
[Pereira2013]_. Darwin Core provides a widely used vocabulary for exchanging
information about taxa, occurrences, events, locations, and related
biodiversity data [Wieczorek2012]_.


Main data-collection approaches
===============================

Biodiversity observations can be collected in several ways. The following
categories are not mutually exclusive: a single OpenBioMaps project may use
different forms and tables for several approaches.


Opportunistic observations
--------------------------

An opportunistic, incidental, or occasional observation records an organism
encountered without following a predefined sampling design. Examples
include a rare bird noticed during a walk, a photograph of an unfamiliar
plant, or a road-killed animal reported by a member of the public.

A useful opportunistic observation should normally include:

* the observed taxon;
* the date and, where available, time of the observation;
* the location;
* the observer or source of the record;
* an indication of abundance or number of individuals where relevant; and
* supporting evidence, such as a photograph, sound recording, specimen
  reference, or comment where available.

Opportunistic records can document occurrences, expand knowledge of where a
species has been detected, and support follow-up surveys. They may also
contribute to distribution modelling or trend analysis when their sampling
biases are explicitly considered.

However, a collection of reported occurrences does not normally show where
observers searched but failed to detect a species. It may also be affected
by uneven recording effort, accessibility, observer preferences, and
variation in identification skills. Consequently, raw opportunistic records
alone should not generally be interpreted as unbiased estimates of
occupancy, abundance, population size, distribution, or temporal change
[Isaac2014]_.

A protocol can improve the consistency of occasional observations by
defining required fields, acceptable evidence, taxonomic validation, and
spatial or temporal precision. Such requirements improve the records but do
not by themselves turn opportunistic collection into a probability-based or
systematic survey.


Sampling and observation events
-------------------------------

A sampling or observation event represents a defined data-collection
activity at a particular place and time. The event may also specify a
method, duration, sampled area, transect length, number of traps, number of
observers, or another measure of sampling effort.

One event may contain:

* no organism observations, when the survey was completed but none of the
  target organisms were detected;
* one observation; or
* several observations associated with the same sampling activity.

Retaining events with no detections is important when the absence of a
record has a defined meaning. A documented non-detection shows that sampling
took place under a specified protocol, whereas the absence of an
opportunistic record does not show that anybody searched at that location.
Repeated detection and non-detection data can support occupancy modelling
and the estimation of imperfect detection when the study design and model
assumptions are appropriate [MacKenzie2002]_.

In OpenBioMaps, shared event information can be stored once in an event or
observation-list record, while individual taxon observations are linked to
that record through a common identifier. This avoids unnecessary repetition
and makes it possible to retain an event even when it contains no organism
observations.

For a more detailed explanation of the distinction, see
:doc:`Observation events vs. occasional observations <observation_events>`.


Repeated monitoring
-------------------

Monitoring involves observations collected repeatedly to evaluate status or
change. It commonly uses fixed or selected sampling locations, a documented
method, a defined schedule, and comparable measures of effort.

A monitoring design may need to record:

* the identity and location of the sampling site;
* the start and end of each sampling event;
* the protocol and equipment used;
* the duration, area, distance, or other measure of effort;
* detections and explicit non-detections;
* counts, cover, biomass, condition, or another response variable;
* environmental conditions and factors affecting detectability;
* changes to the protocol or sampling site; and
* quality-control and validation information.

The database should distinguish stable entities, such as sampling sites and
protocols, from repeated events and the observations made during those
events. This generally requires related tables rather than one table
containing every type of information.

OpenBioMaps can represent such relationships through project-specific
tables, identifiers, upload forms, queries, and data-processing workflows.
The appropriate structure depends on the monitoring design and should be
reviewed by people familiar with both the scientific method and relational
data modelling.


Other sources of biodiversity data
----------------------------------

Projects may also manage data originating from specimens, laboratory
analyses, acoustic recorders, camera traps, tracking devices, remote
sensing, external databases, or other automated systems.

These sources can require additional entities and metadata, such as:

* specimen, sample, or media identifiers;
* deployment and retrieval events;
* device identity and configuration;
* calibration and processing information;
* laboratory methods and derived measurements;
* links between source material and derived records;
* automated identification results and confidence values; and
* the version of the software, model, or reference database used for
  processing.

OpenBioMaps can store or link such information, but the project must define
the required data model, file-storage strategy, validation process, and
provenance rules.


Representing a collection in OpenBioMaps
========================================

An OpenBioMaps implementation should preserve the concepts and relationships
defined by the data-collection design. Database convenience should not
replace the scientific distinction between a sampling activity, an
observation, a taxon, a location, a person, and a processing step.


Tables and relationships
------------------------

A simple opportunistic collection may be represented by a single main
observation table. More structured collections may require separate tables
for:

* sampling sites;
* sampling or observation events;
* individual organism observations;
* taxa or taxon concepts;
* protocols;
* observers and organisations;
* specimens, samples, or media;
* devices or deployments; and
* validation and processing results.

Stable identifiers should be used to connect related records. They should
not be inferred only from names, coordinates, or display labels because
those values can change or may not be unique.

Table and field descriptions should explain the meaning, unit, vocabulary,
and expected content of the data. These descriptions form part of the
project metadata and help users interpret and reuse the collection.


Forms and workflows
-------------------

A project can define multiple upload forms for the same table. Separate
forms may be useful for:

* opportunistic observations;
* structured field surveys;
* observations belonging to a sampling event;
* importing historical datasets;
* public or citizen-science submissions;
* expert validation; and
* mobile data collection.

Each form should expose only the fields relevant to its workflow. Required
fields, controlled lists, defaults, validation rules, and help text should
reflect the collection protocol.

Descriptions should be provided for forms and fields. These descriptions
can help users understand what to enter and may also be made available to
compatible mobile clients.

.. TODO: Confirm which OpenBioMaps mobile applications display form and
   field descriptions, which description fields they use, and whether the
   descriptions are available offline.


Recommended core information
============================

The exact fields required by a project depend on its purpose, but most
observation collections should consider the following categories.


Taxon information
-----------------

Taxon names should preferably be selected from a controlled and documented
taxonomic list. An autocomplete field can help users find accepted
scientific names and, where configured, common or national names.

The project should record which taxonomic reference or checklist is used
and, where possible, preserve a stable identifier for the taxon concept.
Recording only a name string can create ambiguity when names change or the
same name is interpreted differently by different authorities.

Projects may allow users to submit names that are not yet present in the
controlled list. Such values should be clearly marked for subsequent review
rather than silently treated as accepted taxon names. Automatic name
validation can assist this process, but uncertain matches and corrections
should remain traceable.

OpenBioMaps projects may use taxon-related semantic column roles,
autocomplete sources, extensible lists, and background validation jobs to
support these workflows.

Read more about `Superspecies <https://gitlab.com/superspecies/>`_.

.. TODO: Explain whether “superspecies” is the current name of a specific
   OpenBioMaps taxon database, module, table, or autocomplete service. If it
   is an implementation-specific term, replace it with its current official
   name and link to its configuration documentation.

.. TODO: Document the current purpose and configuration of the
   ``auto_species_name`` column or option. Clarify whether it stores the
   submitted name, a validated name, a taxon identifier, or the result of an
   automatic matching process.


Observer and attribution information
------------------------------------

The person or organisation responsible for an observation should be
recorded when this is legally and ethically appropriate. The authenticated
OpenBioMaps account can be used to associate a submission with its uploader,
but the uploader is not necessarily the observer, recorder, identifier, data
owner, or rights holder.

These roles should be stored separately when they differ. Projects should
also define how personal data are displayed, exported, retained, and shared.

A form may populate a field automatically from the signed-in user's account
to reduce repeated data entry.

.. TODO: Confirm the exact behaviour of the ``login_name`` upload-form
   option. Document which user attribute it inserts, whether the user can
   edit the value, and how records submitted through the API or without
   authentication are handled.


Date and time
-------------

An observation should include the date and, where relevant, the time at
which it occurred. A sampling event may require both a start and an end
time.

Projects should define:

* whether time is required;
* which time zone is used;
* how uncertain, approximate, or incomplete dates are represented;
* whether the recorded value refers to observation, submission, import, or
  processing time; and
* how timestamps supplied by devices or imported files are validated.

The observation time should not be replaced by the database insertion
timestamp. Both may be useful, but they describe different events.


Location and geometry
---------------------

Location can be represented by coordinates, an OpenBioMaps geometry field,
a sampling-site identifier, a named locality, or a combination of these.

The ``obm_geometry`` field is commonly used for the spatial geometry of a
record. Depending on the collection, it may contain a point, line, or
polygon. The project should also document:

* the coordinate reference system - default is WGS84;
* the method used to obtain the location;
* coordinate uncertainty or spatial precision;
* whether coordinates have been transformed or generalised;
* any restrictions applied to sensitive locations; and
* whether the geometry represents the organism, the observer, a route, a
  sampled area, or another spatial concept.

Coordinates obtained from a mobile device should not automatically be
treated as exact. Accuracy can vary according to the device, environment,
positioning method, and time allowed for obtaining a fix.


Quantity and detection
----------------------

Where relevant, the collection should record the number of individuals,
percentage cover, biomass, presence, detection status, or another defined
quantity. The unit and interpretation of the value must be explicit.

A value of zero should be used only when the protocol establishes that
sampling occurred and the target was not detected. It should not be used as
a replacement for missing information.


Method and sampling effort
--------------------------

Structured surveys should record enough information to interpret and, where
possible, repeat the sampling activity. This may include the protocol,
duration, distance, area, number of traps, observer effort, equipment, and
environmental conditions.

Method and effort information should be associated with the sampling event
when it applies to all observations within that event.


Evidence, validation, and provenance
------------------------------------

Photographs, sound recordings, specimens, comments, and other supporting
material can help validate an observation. Projects should preserve the
relationship between an observation and its evidence, together with the
origin and rights information of the attached material.

Validation should not silently overwrite the originally submitted
information. Where practical, projects should retain:

* the submitted value;
* the accepted or corrected value;
* the identity or role of the validator;
* the date of validation;
* the validation status and comments; and
* the method or reference used to make the decision.

Maintaining provenance makes corrections understandable and supports later
reuse. More generally, biodiversity data should be managed so that they are
findable, accessible under defined conditions, interoperable, and reusable
[Wilkinson2016]_.


Field naming and interoperability
=================================

Clear and stable field names make a project easier to maintain. Field names
should be accompanied by descriptions and should not rely on abbreviations
whose meaning is known only to the original project team.

Where data will be exchanged with external systems, projects should consider
mapping their fields to established vocabularies such as Darwin Core
[Wieczorek2012]_. Using Darwin Core-inspired names can make mappings easier,
but assigning a familiar name to a field is not sufficient by itself. The
meaning, unit, cardinality, vocabulary, and relationship of the field must
also be compatible with the corresponding term.

A project does not need to store all data directly in an exchange format.
It can use a structure suited to its collection workflow and create a
documented export or transformation that maps its records to the required
standard.


Practical checklist
===================

Before a collection form is made available, verify that:

* the scientific purpose and target population are defined;
* opportunistic observations and structured sampling events are
  distinguished where necessary;
* completed events with no detections can be retained when required by the
  protocol;
* taxa are linked to an appropriate controlled list or review workflow;
* observation and submission timestamps are not confused;
* geometries have a defined meaning and coordinate reference system;
* spatial uncertainty and sensitive locations can be represented;
* observer, uploader, identifier, owner, and rights-holder roles are
  distinguished where necessary;
* quantities and units are documented;
* sampling methods and effort can be recorded;
* required fields and validation rules reflect the protocol;
* original values and subsequent corrections remain traceable;
* form and field descriptions are understandable to data collectors;
* access rules and personal-data requirements have been reviewed;
* test records have been submitted through every intended interface; and
* the resulting records can be queried, exported, and interpreted without
  relying on undocumented knowledge.

The structure should be tested with realistic examples, including missing
values, uncertain identifications, observations outside the expected area,
events with no detections, multiple observations within one event, and
records submitted from each supported web, mobile, or API client.


Example data collections
========================

Worked examples can illustrate how different collection designs are
represented using OpenBioMaps tables and forms.

See :doc:`OpenBioMaps example data collections <data_collection_examples>`.


References
==========

.. [Isaac2014] Isaac, N. J. B., van Strien, A. J., August, T. A.,
   de Zeeuw, M. P., and Roy, D. B. (2014). Statistics for citizen science:
   extracting signals of change from noisy ecological data. *Methods in
   Ecology and Evolution*, 5(10), 1052–1060.
   https://doi.org/10.1111/2041-210X.12254

.. [MacKenzie2002] MacKenzie, D. I., Nichols, J. D., Lachman, G. B.,
   Droege, S., Royle, J. A., and Langtimm, C. A. (2002). Estimating site
   occupancy rates when detection probabilities are less than one.
   *Ecology*, 83(8), 2248–2255.
   https://doi.org/10.1890/0012-9658(2002)083%5B2248:ESORWD%5D2.0.CO;2

.. [Pereira2013] Pereira, H. M., Ferrier, S., Walters, M., Geller, G. N.,
   Jongman, R. H. G., Scholes, R. J., Bruford, M. W., Brummitt, N.,
   Butchart, S. H. M., Cardoso, A. C., Coops, N. C., Dulloo, E.,
   Faith, D. P., Freyhof, J., Gregory, R. D., Heip, C., Höft, R.,
   Hurtt, G., Jetz, W., Karp, D. S., McGeoch, M. A., Obura, D.,
   Onoda, Y., Pettorelli, N., Reyers, B., Sayre, R., Scharlemann,
   J. P. W., Stuart, S. N., Turak, E., Walpole, M., and Wegmann, M.
   (2013). Essential Biodiversity Variables. *Science*, 339(6117),
   277–278. https://doi.org/10.1126/science.1229931

.. [Wieczorek2012] Wieczorek, J., Bloom, D., Guralnick, R., Blum, S.,
   Döring, M., Giovanni, R., Robertson, T., and Vieglais, D. (2012).
   Darwin Core: An evolving community-developed biodiversity data standard.
   *PLOS ONE*, 7(1), e29715.
   https://doi.org/10.1371/journal.pone.0029715

.. [Wilkinson2016] Wilkinson, M. D., Dumontier, M., Aalbersberg, I. J.,
   Appleton, G., Axton, M., Baak, A., Blomberg, N., Boiten, J.-W.,
   da Silva Santos, L. B., Bourne, P. E., Bouwman, J., Brookes, A. J.,
   Clark, T., Crosas, M., Dillo, I., Dumon, O., Edmunds, S., Evelo,
   C. T., Finkers, R., Gonzalez-Beltran, A., Gray, A. J. G.,
   Groth, P., Goble, C., Grethe, J. S., Heringa, J.,
   't Hoen, P. A. C., Hooft, R., Kuhn, T., Kok, R., Kok, J.,
   Lusher, S. J., Martone, M. E., Mons, A., Packer, A. L.,
   Persson, B., Rocca-Serra, P., Roos, M., van Schaik, R.,
   Sansone, S.-A., Schultes, E., Sengstag, T., Slater, T.,
   Strawn, G., Swertz, M. A., Thompson, M., van der Lei, J.,
   van Mulligen, E., Velterop, J., Waagmeester, A., Wittenburg, P.,
   Wolstencroft, K., Zhao, J., and Mons, B. (2016). The FAIR Guiding
   Principles for scientific data management and stewardship.
   *Scientific Data*, 3, 160018.
   https://doi.org/10.1038/sdata.2016.18
