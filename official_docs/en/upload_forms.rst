.. _manage-upload-forms:

Upload form management
======================

Upload forms define how users and external clients can submit data to a
project. A form specifies its destination table, availability, access
settings, supported clients, fields, validation rules, default values, and
relationships between fields.

.. TODO: Add an introductory workflow explaining how to create, test,
   publish, copy, block, and retire an upload form.

.. TODO: Explain which administrative permission is required to manage
   upload forms and provide the current navigation path to this page.

.. TODO: Clarify which settings are shared by web, file-upload, API, and
   mobile clients, and identify settings that are supported only by a
   particular client.


List of available forms
-----------------------

Existing forms can be selected for editing, deletion, or blocking.

Data cannot be uploaded using blocked forms, and these forms are not visible 
to clients in the list of forms. Offline clients cannot upload data using deleted 
forms, and deleted forms cannot be restored.
By editing forms, you can change their scope (web, API or file upload), their 
relationship with database table fields, their description and access rules, as well 
as whether they operate in observation event or ad hoc mode.

Blocked forms appear with a grey background in the list.

Forms can also be set to read-only, which is indicated by a padlock icon in the list. 
(To do this, set the value of the ‘active’ field in the ‘project_forms’ table to 3.)


Form header definition
----------------------

Destination table
.................

Select the project table to which data submitted through the upload form
will be written.

You can only select SQL tables registered by OpenBioMaps within the project, 
which contain the basic OpenBioMaps fields such as obm_id, obm_uploading_id, etc.
The selected table cannot be changed afterwards, as the form fields are linked 
to the fields in the selected table.

The forms are sensitive to changes in the table structure. For this reason, it is 
strongly advised not to edit the tables using a tool other than OpenBioMaps, as 
this will cause the form to lose its link to the fields. In such cases, saving the 
changes to the form may resolve the inconsistency, but clients will not be able to 
upload the offline data!


Name of the form
................

Enter a name for the upload form. The name should be unique within the
project (as the name is part of the unique identifier of the forms).

A form can be copied by renaming it. In this case, the original form retains its 
original name; in other words, it is not possible to rename a form, only to create 
a new one, which affects the operation of offline clients!

The name can be multilingual when a translation key with the ``str_`` prefix
is used. For more information, see :ref:`Translations <localisation>`.


Form access
...........

Define who can view and use the form:

* public users;
* all logged-in users; or
* only specified groups.

If **only specified groups** is selected, the user and group selection field
becomes active, allowing access to be granted to selected users or groups.

.. TODO: Confirm the current labels used by the administration interface
   and whether access can be assigned directly to individual users as well
   as groups.

.. TODO: Explain whether public form access permits unauthenticated data
   submission and how the uploader, ownership, read access, write access,
   rate limiting, and abuse prevention are handled in that case.

.. TODO: Clarify whether nested group membership grants access to the form
   and how changes to group membership affect active or saved uploads.


Data access
...........

Data uploaded through the form will be available only to the groups
specified here. By default, the uploader can read and edit the uploaded
data.

.. TODO: Document how the form's data-access settings are transferred to
   the project's row-level access rules, including the exact meaning and
   format of read and write assignments.

.. TODO: Confirm the behaviour when no group is selected and whether the
   uploader is always granted read and write access.

.. TODO: Explain how these settings interact with ``ACC_LEVEL``,
   ``MOD_LEVEL``, sensitivity settings, the access-rules trigger, and the
   ``allowed_columns`` module. Include examples for public, logged-in, and
   group-restricted projects.

.. TODO: Document what happens when the form's data-access settings are
   changed. Clarify whether the new settings affect only subsequent uploads
   or also update existing records.


Form type
.........

At least one of the following form types must be selected:

* web form;
* file-upload form; or
* API form, for access by external clients such as the mobile application.

.. TODO: Explain the capabilities and limitations of each form type,
   including whether several types can be enabled simultaneously.

.. TODO: Document authentication, version selection, and compatibility
   requirements for API clients and mobile applications.


Form description
................

Enter a short or detailed description of the form. The description can
provide instructions to contributors.

.. TODO: Explain where the description is displayed in web, file-upload,
   API, and mobile interfaces; whether it supports translations or markup;
   and whether there is a maximum length.


Form SRID
.........

Select the spatial reference system used by data submitted through the form.
Spatial reference systems can be looked up at
https://spatialreference.org/. The default is EPSG:4326 (WGS 84).

If a list of spatial reference systems is specified, uploaders can select
only from the listed options. Define the list as comma-separated EPSG
identifiers and visible labels, using the following format:

.. code-block:: text

   4326:wgs84,23700:eov

.. TODO: Confirm whether the form SRID describes the coordinates supplied
   by the uploader, the storage SRID of the destination geometry column, or
   both. Explain when and how coordinate transformation is performed.

.. TODO: Document how the form SRID affects WKT geometry, latitude and
   longitude fields, imported spatial files, web-map drawing, and mobile
   application coordinates.

.. TODO: Confirm the accepted syntax and validation of the SRID list,
   including whether spaces, translated labels, non-EPSG authorities, or
   case-sensitive labels are supported.


Form grouping
.............

Forms can be organised into groups in the web form-selection interface.
Group names can be defined or selected here.

This option is not currently available in the mobile application.

.. TODO: Explain how form groups are created, ordered, renamed, translated,
   and removed. Clarify whether grouping affects access or only
   presentation.

.. TODO: Confirm whether form grouping remains unsupported in the current
   mobile application version.


Form publication
................

A form can be locked by publishing it with the orange publish button in the
form-header area. Updating a published form creates a new version. Previous
versions remain available to API clients such as the mobile application.

A draft can be created from a published form for testing by using the
**Create a draft version** button at the bottom of the page. By default, the
draft is available only to its creator. The draft can subsequently be
published to the form's published branch.

.. TODO: Define the complete form-versioning model, including drafts,
   published versions, branches, version identifiers, and the meaning of
   locking a form.

.. TODO: Explain whether publishing takes effect immediately and how web,
   file-upload, API, and mobile clients select or cache a form version.

.. TODO: Document who can view and test a draft, how draft access can be
   changed, and whether more than one draft can exist for a form.

.. TODO: Explain how an administrator can compare versions, revert to an
   earlier version, retire a published version, or resolve submissions made
   with an old version.


Observation event settings
..........................

For an explanation of observation events and the difference between
occasional and event-based observations, see
:doc:`Observation events and occasional observations <observation_events>`.

A time limit, expressed in minutes, can be set for an observation event.
When the limit is reached, the mobile application alerts the user that the
time has expired. The alert does not end the event, and the user can
continue recording observations.

A **forced observation event** means that the form can be launched only in
event mode. If observation-event support is enabled but not forced, the user
can choose between event mode and occasional-observation mode.

.. TODO: Document all observation-event settings and explain how event
   identifiers, start and end times, shared field values, and individual
   observations are stored.

.. TODO: Explain whether the time limit is advisory in every supported
   client and what happens when the application is offline, suspended, or
   restarted during an event.

.. TODO: Confirm the current labels for enabling and forcing observation
   events and identify which settings are supported by the web interface,
   API, and mobile application.


.. _tracklog:

Tracklog
........

This option enables automatic route-log recording while the form is being
used. Tracklog recording can be mandatory or optional and is available only
in event mode.

.. TODO: Explain how frequently locations are recorded, which location
   permissions are required, and how offline recording, accuracy, battery
   use, and interrupted events are handled.

.. TODO: Document where tracklogs are stored, who can access them, how they
   are linked to events and observations, and whether their access rules
   differ from those of the submitted records.

.. TODO: Add a privacy and security note explaining that tracklogs may
   reveal a contributor's movements and can therefore constitute personal
   or sensitive data.


.. _periodic-notification:

Periodic notification
.....................

At the specified interval, in minutes, the application reminds the observer
to record a new observation. The timer runs continuously and restarts
whenever the user records an observation.

.. TODO: Confirm whether periodic notifications are available only in the
   mobile application and whether they operate while the application is in
   the background.

.. TODO: Explain when the first interval begins, what happens when a
   notification is dismissed, and whether recording or editing an
   observation restarts the timer.


Form column definitions
-----------------------

The column-definition section specifies which destination-table columns
appear on the form and how submitted values are displayed and validated.

.. TODO: Explain how database-column metadata and data types determine the
   initial form-column settings.

.. TODO: Document how changes to destination-table columns affect existing
   draft and published form versions.


Included
........

If selected, the column appears on the form.

.. TODO: Explain whether a non-included column can still receive a default,
   generated, or API-supplied value.


Column order
............

The small input field next to the **Included** option defines the order of
the column on the form. It is empty by default.

.. TODO: Document the accepted values, ordering direction, treatment of
   duplicate or missing values, and whether order can be changed by
   drag-and-drop.


Column
......

Two names are displayed: the visible name of the column, which can be edited
for the form, and the original database-column name.

.. TODO: Explain whether the visible name supports ``str_`` translation
   keys and how it is presented in file templates, validation messages,
   exports, API definitions, and mobile clients.

.. TODO: Clarify whether changing the visible name affects only the form or
   also modifies database metadata.


Obligatory
..........

Three options are available: **yes**, **no**, and **soft error**.

``Yes`` (burgundy)
   The form cannot be submitted without a value in this column.

``No`` (grey)
   The form can be submitted with an empty value in this column.

``Soft error`` (pink)
   Empty values or values that do not satisfy a restriction can be
   submitted, but the uploader must confirm every affected row.

.. TODO: Explain how confirmation of a soft error works in web forms, file
   uploads, API clients, and the mobile application.

.. TODO: Document whether a soft-error confirmation is recorded in the
   database or upload metadata and whether administrators can distinguish
   confirmed values from values that passed validation.

.. TODO: Clarify how form-level obligatory settings interact with database
   ``NOT NULL`` constraints, column relations, and hidden or read-only
   fields.


Column description
..................

Enter a short description of the field.

.. TODO: Explain where column descriptions are displayed, whether they
   support translations or markup, and whether they are inherited from
   database-column comments.


Column type
...........

The following form column types are available:

``text``
   Arbitrary text. Minimum and maximum lengths can be specified.

``numeric``
   A numeric value. Minimum and maximum values or lengths can be specified.

``list``
   A drop-down list with one selectable item by default.

``true-false``
   A Boolean false/true value. The order of the values can be controlled in
   the list-definition field, for example ``false, true``.

``date``
   A date with the year, month, and day separated by an accepted character.
   It is stored using a database date type.

``date and time``
   A date followed by a space and a time in
   ``hour:minute:second`` format. If seconds are omitted, the application
   automatically treats them as ``00`` and asks the uploader to accept the
   change. If minutes are omitted, the application treats them as ``00``
   and also asks for confirmation. The value is stored using a database
   date-time type.

``time (timetominutes)``
   A value in ``hours:minutes`` format that the application converts to an
   integer. It is stored using a database integer type.

``time``
   A value in ``hours:minutes`` format that is stored using a database time
   type.

``time interval (timeinterval)``
   A time interval, for example
   ``2014-02-25 12:00:00 2014-02-25 13:00:00``. It is stored using a
   database time-interval type.

``autocomplete``
   Generates autocomplete suggestions from the SQL table column specified
   in the list-definition field. The documented shorthand syntax is
   ``table_name.column``. By default, the table is searched for in the
   ``public`` schema of the ``gisdata`` database.

``autocompletelist``
   Similar to ``autocomplete``, but allows multiple autocomplete values to
   be entered in one field.

``photo id``
   If the photo module is enabled, the application stores uploaded photo
   identifiers in this field.

``geometry: point``
   A point geometry represented as WKT ``POINT(...)``.

``geometry: line``
   A line geometry represented as WKT ``LINESTRING(...)``.

``geometry: polygon``
   A polygon geometry represented as WKT ``POLYGON(...)``.

``geometry: any``
   A geometry represented in WKT using a supported geometry type. See
   `an example form
   <https://openbiomaps.org/projects/checkitout/upload/?form=736&type=web>`_.

``colour rings``
   Allows a colour-ring combination to be specified. The section in square
   brackets defines the maximum number of rings that can be specified for
   the different leg sections. It is followed by the individual codes and
   labels of the available colours, for example
   ``[XX],Blue:B,red:R,green:G``.

   The documented colour codes are:

   * ``R`` — red;
   * ``P`` — pink;
   * ``G`` — green;
   * ``g`` — light green;
   * ``O`` — orange;
   * ``Y`` — yellow;
   * ``B`` — blue;
   * ``b`` — light blue;
   * ``W`` — white;
   * ``K`` — black;
   * ``N`` — brown;
   * ``U`` — purple;
   * ``V`` — violet; and
   * ``M`` — silver.

   See `an example colour-ring form
   <https://openbiomaps.org/projects/checkitout/upload/?form=939&type=web>`_.

.. TODO: Confirm the current names of all available column types and map
   each form type to its required PostgreSQL data type.

.. TODO: Clarify whether the numeric minimum and maximum settings constrain
   numeric values, character lengths, or both.

.. TODO: Document the accepted input formats, time zones, ranges, and
   storage types for date, date-time, time, and interval fields. PostgreSQL
   has no built-in type named ``datetime`` or ``timeinterval``, so identify
   the exact database types used.

.. TODO: Confirm the exact WKT geometry names accepted for line fields. The
   standard WKT geometry type is ``LINESTRING``, while the source interface
   may use the label ``LINE``.

.. TODO: Document how form geometry types interact with the form SRID,
   destination-column SRID, geometry collections, multipart geometries,
   three-dimensional coordinates, and invalid geometries.

.. TODO: Explain the autocomplete shorthand and JSON formats, database
   connection used for lookups, applicable permissions, result limits,
   matching behaviour, and SQL-injection protections.

.. TODO: Document the storage format and attachment relationship used by
   ``photo id``.

.. TODO: Verify the syntax, storage representation, supported leg sections,
   and complete colour set of the ``colour rings`` type. Clarify whether
   ``purple`` and ``violet`` are intentionally separate values.


Input control
.............

Input controls check values entered into the field. The available options
are:

* no check;
* minimum and maximum;
* regular expression;
* spatial; and
* custom check.

.. TODO: Document the configuration syntax and behaviour of every input
   control, including client-side and server-side validation.

.. TODO: Explain whether minimum and maximum constraints refer to length,
   numeric value, date, or another property depending on the column type.

.. TODO: Document the regular-expression dialect, delimiters, flags,
   escaping rules, and whether the expression must match the complete
   value.

.. TODO: Explain the available spatial and custom checks and add tested
   examples. Identify where custom validation code is stored and who is
   permitted to edit it.


List definition
...............

To use a list during data submission, set the column type to ``list``,
``autocomplete``, or ``autocompletelist``.

List definitions can describe simple or multiple-choice lists, autocomplete
sources, values obtained from other database tables, and rules for filtering
those values.

A short list can be defined directly. In the following example, uploaders
can select ``female`` or ``male`` from a drop-down list. The selected value
is stored in the database.

.. code-block:: json

   {
     "list": {
       "female": [],
       "male": []
     }
   }

Several input labels can be mapped to the same stored value. For example,
``F``, ``f``, and ``female`` can all be interpreted as the stored value
``female``. This is particularly useful during file upload when data from
different contributors or years use different labels for the same concept.

.. code-block:: json

   {
     "list": {
       "female": [
         "F",
         "f",
         "female"
       ],
       "male": [
         "M",
         "m",
         "male"
       ]
     }
   }

A list can also be entered in plain-text format, with one value on each
line. When the form is saved, the application converts the plain-text list
to JSON. The resulting JSON can then be edited directly.

.. TODO: Clarify how list keys, labels, and aliases are displayed and
   matched. Document case sensitivity, whitespace handling, duplicate
   labels, empty values, and translation support.

.. TODO: Explain how multiselect and ``autocompletelist`` values are stored
   in the destination column and which PostgreSQL column types are
   supported.

List values can also come from an SQL table. Specify the schema
(``optionsSchema``), table (``optionsTable``), stored-value column
(``valueColumn``), and, where required, visible-label column
(``labelColumn``).

Values can be filtered using ``preFilterColumn`` and ``preFilterValue``.
The following example applies prefilters:

.. code-block:: json

   {
     "optionsTable": "milvus_taxon",
     "valueColumn": "word",
     "preFilterColumn": [
       "lang",
       "status"
     ],
     "preFilterValue": [
       "obm_taxon",
       [
         "accepted",
         "undefined"
       ]
     ],
     "orderBy": "taxon_db",
     "order": "desc"
   }

The complete list definition uses JSON. It can be assembled with the list
editor in the web interface and is checked for valid syntax by the
application. If the syntax is invalid, the application returns an error
message.

The following example lists the documented properties:

.. code-block:: json

   {
     "list": {
       "val1": [
         "label1",
         "label2"
       ]
     },
     "optionsSchema": "e.g. public",
     "optionsTable": "a table name",
     "valueColumn": "a column from the table",
     "labelColumn": "a column from the table - optional",
     "filterColumn": "",
     "pictures": {
       "an element from the list, e.g. val1": "url-string"
     },
     "triggerTargetColumn": [
       ""
     ],
     "Function": "",
     "disabled": [
       "an element from the list, e.g. val1"
     ],
     "preFilterColumn": [
       ""
     ],
     "preFilterValue": [
       ""
     ],
     "preFilterRelation": [
       ""
     ],
     "multiselect": "true or false, default is false",
     "selected": [
       "an element from the list, e.g. val1"
     ],
     "size": "a numeric value",
     "orderBy": [
       "column or SQL expression"
     ],
     "order": [
       "ASC or DESC"
     ],
     "limit": "numeric value"
   }

.. TODO: Replace the illustrative complete definition with one or more
   valid, executable examples. Placeholder values such as ``e.g. public``
   and type descriptions represented as strings cannot be copied directly
   into a working form.

.. TODO: Provide a reference table for every supported property, including
   its type, default, permitted values, applicable form-column types, and
   supported clients.

.. TODO: Clarify whether ``Function`` is intentionally case-sensitive while
   the other property names begin with lowercase letters.

.. TODO: Explain the behaviour and accepted syntax of ``labelAsValue``,
   ``filterColumn``, ``pictures``, ``disabled``, ``preFilterRelation``,
   ``multiselect``, ``selected``, ``size``, ``orderBy``, ``order``, and
   ``limit``.

.. TODO: Confirm whether ``orderBy`` and ``order`` accept either a string or
   an array. The examples on this page currently demonstrate both forms.

.. TODO: Document how table and column identifiers or SQL expressions are
   validated. In particular, explain the security restrictions applied to
   ``orderBy`` and any other property that may contain an SQL expression.

.. TODO: Explain whether list queries apply project row- and column-level
   access rules and which database user executes them.


Joint lists
...........

A joint list uses the value selected in one column, called the starter
column, to determine the available values in another column. This creates a
dependent or cascading list.

First, create a lookup table containing the relationships between the list
levels. For example, an ``animal_taxons`` table could describe which animal
groups belong to each supergroup. Vertebrates could contain amphibians,
reptiles, birds, and mammals, while invertebrates could contain cnidarians
and insects.

In the list definition of the starter column, specify the target column:

.. code-block:: json

   {
     "triggerTargetColumn": [
       "affected_list_name"
     ],
     "Function": "select_list",
     "optionsSchema": "shared",
     "optionsTable": "animal_taxons",
     "valueColumn": "animal_group_name",
     "labelColumn": "animal_group_name",
     "labelAsValue": true
   }

The properties used in this example are:

``Function``
   Uses the documented value ``select_list``.

``optionsSchema``
   Identifies the schema containing the lookup table. This example uses
   ``shared``.

``optionsTable``
   Identifies the lookup table.

``valueColumn``
   Identifies the column providing the values for the starter list.

``labelColumn``
   Identifies the column providing the visible labels.

``triggerTargetColumn``
   Identifies the form column whose list must be updated.

In the affected column, define which lookup-table column provides its values
and which column is used to filter them:

.. code-block:: json

   {
     "optionsTable": "animal_taxons",
     "valueColumn": "animal_group_name",
     "labelColumn": "animal_group_name",
     "filterColumn": "animal_supergroup",
     "Function": "select_list",
     "optionsSchema": "shared"
   }

Here, ``filterColumn`` identifies the lookup-table column that is matched
against the value selected in the preceding form column.

Joint lists can connect more than two form columns:

.. code-block:: json

   {
     "optionsSchema": "shared",
     "optionsTable": "animal_taxons",
     "filterColumn": "animal_supergroup",
     "Function": "select_list",
     "valueColumn": "animal_group_name",
     "triggerTargetColumn": [
       "species"
     ],
     "labelColumn": "animal_group_name"
   }

In a chain of joint lists, ``triggerTargetColumn`` identifies the next form
column, ``filterColumn`` identifies the lookup-table column used to match
the preceding selection, and ``valueColumn`` and ``labelColumn`` define the
current list.

.. TODO: Verify the descriptions of ``valueColumn`` and ``labelColumn`` in
   starter and affected columns. Add an example lookup table with sample
   rows so that the direction of each relationship is unambiguous.

.. TODO: Explain how the selected value from the starter form column is
   mapped to ``filterColumn`` and whether the form-column name must match a
   lookup-table column name.

.. TODO: Document how joint lists handle empty selections, changed parent
   values, duplicate options, multiple parent values, multiselect fields,
   autocomplete fields, and chains longer than two levels.

.. TODO: Confirm whether ``optionsSchema`` must always be ``shared`` for
   joint lists. The examples later on this page use ``public``, indicating
   that other schemas may be supported.


Joint-list example: buildings within a settlement
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Suppose a project collects data about species breeding in artificial nest
boxes. A lookup table named ``tytoalba_buildings`` records which buildings
occur in each settlement. The settlement field should provide an
autocomplete list, and the building field should show only buildings in the
selected settlement.

First, configure the settlement column as an autocomplete field and identify
the building column as its target:

.. code-block:: json

   {
     "triggerTargetColumn": [
       "building"
     ],
     "Function": "select_list",
     "optionsSchema": "public",
     "optionsTable": "tytoalba_buildings",
     "valueColumn": "settlement"
   }

Next, configure the building column as a list and filter its values using the
selected settlement:

.. code-block:: json

   {
     "optionsTable": "tytoalba_buildings",
     "filterColumn": "settlement",
     "Function": "select_list",
     "valueColumn": "building"
   }

.. TODO: Confirm whether the second definition inherits ``optionsSchema``
   from the starter column or whether ``optionsSchema`` was omitted
   accidentally.

.. TODO: Add example rows from ``tytoalba_buildings`` and show the visible
   result after a settlement is selected.


.. _default-values:

Default values
..............

A predefined value can be assigned to a field. The documented dynamic
default values are:

* ``_autocomplete``;
* ``_input``;
* ``_list``;
* ``_geometry``;
* ``_login_name``;
* ``_email``;
* ``_boolean``;
* ``_attacment``;
* ``_datum``; and
* ``_auto_geometry``.

For example, ``_input`` produces an empty input field, ``_list`` fills a
selection list using the list definition, ``_geometry`` provides geometry
selection, and ``_datum`` provides date selection.

See `an example form
<https://openbiomaps.org/projects/checkitout/upload/?form=421&type=web>`_.

.. TODO: Confirm the complete and current list of dynamic default values and
   describe the result of each one in every supported client.

.. TODO: Verify whether ``_attacment`` is intentionally spelled with one
   ``h`` for compatibility with the implementation or is a typographical
   error that should be changed to ``_attachment``.

.. TODO: Verify whether ``_datum`` is the current documented identifier and
   explain how it differs from a literal date or a current-date default.

.. TODO: Explain how to define literal default values and how values that
   begin with an underscore are escaped.

.. TODO: Clarify when defaults are evaluated, whether users can overwrite
   them, and how they interact with sticky, hidden, read-only, and once-only
   fields.

.. TODO: Document what ``_login_name`` and ``_email`` produce for an
   unauthenticated submission and whether these values should be considered
   trusted identity information.


.. _api-params:

Field display options
.....................

The following display options are documented:

``sticky``
   Primarily used by the mobile application. When selected, the field
   retains its value when a new row is started.

``hidden``
   The field is not displayed.

``read only``
   The field value cannot be modified.

``once``
   In the mobile application, the field is displayed only once for an
   observation list, at the end of the observation.

   This option is intended to allow a field to be moved outside the
   repeating table in the web form. Currently, a similar result can be
   achieved in the web form by using a default value.

``list elements as buttons``
   Displays list elements as buttons. Images can be used on the buttons.
   Images should be defined for all list elements in the list definition.

``unfolding list``
   Provides a species-list workflow for the mobile application. This option
   can be used only with an autocomplete field, typically a scientific-name
   field, when the form also contains a number-of-individuals field assigned
   the corresponding semantic role in the database-table settings.

   The mobile application displays the selected species names and their
   individual counts in a list. Counts can be modified without saving a
   separate record after every change. The option is therefore most useful
   in an observation-event form, where **Save observation** acts as an
   intermediate save and does not clear the accumulated species list.

The following list definition associates images with example button values:

.. code-block:: json

   {
     "pictures": {
       "animals": "http://....png",
       "plants": "http://....png",
       "mushrooms": "http://....png",
       "bats": "http://....png"
     }
   }

.. TODO: Confirm why this section uses the ``api-params`` reference label
   and whether these options are represented as API parameters.

.. TODO: Document which display options are available in web, file-upload,
   API, and mobile clients and how unsupported options are treated.

.. TODO: Explain whether hidden and read-only fields can be changed by a
   direct API request or file upload. Display restrictions must not be
   treated as server-side access controls without validation.

.. TODO: Define the exact scope and lifecycle of a sticky value, including
   new observations, new events, form changes, application restarts, and
   different users on the same device.

.. TODO: Clarify the current implementation and intended web-form behaviour
   of the ``once`` option.

.. TODO: Explain image URL requirements, supported formats, caching,
   authentication, alternative text, and behaviour when an image is
   unavailable. Replace the ``http://....png`` placeholders with safe,
   working examples.

.. TODO: Document how the unfolding list identifies the number-of-
   individuals field and how it stores, updates, and validates the resulting
   observations.


Column relations
................

Column relations check or modify the value of one field according to the
value of another field. For example, a weight field can be restricted to a
numeric range of 20 to 30 when the sex field contains ``female``:

.. code-block:: text

   (sex=female) {minmax(20:30)}

See `an example form
<https://openbiomaps.org/projects/checkitout/upload/?form=938&type=web>`_.

.. TODO: Explain where relations are configured in the administration
   interface and whether a relation belongs to the field being checked or
   the field that triggers it.

.. TODO: Document when relations are evaluated in web forms, file uploads,
   API requests, and mobile applications, and whether validation is repeated
   on the server.

.. TODO: Explain how multiple relations are combined, how conflicts are
   resolved, and whether evaluation order is significant.


Pseudo-columns
..............

Columns from other upload forms can be added using the following format:

.. code-block:: text

   form-name:column1,column2,columnN

The listed columns appear after the column containing this definition.
Values entered in the pseudo-columns are uploaded using the other form's
definition. This allows data to be submitted to two tables in one workflow.

.. TODO: Explain where the pseudo-column definition is entered and add a
   complete example using two forms and two related destination tables.

.. TODO: Document how records written through the two forms are linked,
   ordered, validated, committed, and rolled back. Clarify what happens if
   one insert succeeds and the other fails.

.. TODO: Explain whether pseudo-columns support nested pseudo-forms,
   attachments, geometry, access rules, published form versions, file
   uploads, APIs, and mobile applications.

.. TODO: Clarify how naming conflicts and obligatory fields in the referenced
   form are handled.


The relations language definition
---------------------------------

The documented general syntax of the relations language is:

.. code-block:: text

   (rel_field=rel_statement) {rel_type(rel_value)}, (rel_field=rel_statement) {rel_type(rel_value)}, ...

The intended interpretation is:

.. code-block:: text

   IF another field (rel_field) matches rel_statement,
   THEN apply rel_type with rel_value to the current field.

``rel_type`` is a function associated with the current field type. The
documented functions are:

``year``
   For date fields, extracts the year component from a date string.

``minmax``
   For text or numeric fields, performs a minimum and maximum range check.

``obligatory``
   For any field type, changes whether the current field is obligatory.

``inequality``
   For any field type, compares the related field and the current field
   using a supported comparison operator. A failed comparison produces a
   validation error.

A regular-expression statement begins with ``!!`` followed by a regular
expression, for example:

.. code-block:: text

   !!^(\d{2})$

When ``rel_statement`` is a regular expression, ``rel_value`` can use a
replacement function based on the matched value:

``.``
   Replaces the current field value with the string matched in
   ``rel_field``.

``.+``
   Appends the current field value to the string matched in ``rel_field``.

``+.``
   Appends the string matched in ``rel_field`` to the current field value.

For an ``inequality`` relation, the documented expressions use ``+`` for the
matched value of ``rel_field`` and ``.`` for the current field value:

.. code-block:: text

   +<.
   +<=.
   +>=.
   +=.
   +<>.

For other relation types, ``rel_value`` can contain another value or may be
ignored, depending on the function.

.. TODO: Verify the formal grammar shown above against the current parser.
   The original description used both ``rel_type=rel_value`` and
   ``rel_type(rel_value)`` notation, while all examples use the latter.

.. TODO: Provide a complete list of supported relation functions and the
   field types, arguments, return values, and error behaviour of each one.
   The examples below use ``set``, but it is not included in the documented
   function list.

.. TODO: Document escaping and quoting rules for field names and values that
   contain spaces, commas, parentheses, braces, equals signs, non-ASCII
   characters, or regular-expression metacharacters.

.. TODO: Confirm the supported regular-expression engine and explain capture
   groups, replacement syntax, delimiters, modifiers, Unicode behaviour,
   and invalid-expression handling.

.. TODO: Clarify the meaning of the ``.``, ``.+``, and ``+.`` replacement
   operators and add tested examples showing the resulting values.

.. TODO: Confirm whether ``<>`` means “not equal” and whether ``!=`` is also
   supported.

.. TODO: Explain how dates, numeric strings, null values, and locale-specific
   decimal separators are compared.


Relation examples
.................

Making a field obligatory
~~~~~~~~~~~~~~~~~~~~~~~~~

On the ``tarsus_length`` column:

.. code-block:: text

   (clutch_size=!!^([123])$) {obligatory(1)}

This makes ``tarsus_length`` obligatory when ``clutch_size`` is ``1``,
``2``, or ``3``.

.. TODO: Confirm whether the regular expression intentionally permits only
   one-character values and whether ``clutch_size`` is treated as text or a
   number.


Comparing two dates
~~~~~~~~~~~~~~~~~~~

On the ``end_date`` column:

.. code-block:: text

   (found_date=!!^(.+)$) {inequality(+>=.)}

If ``found_date`` is not empty, the relation checks whether ``end_date`` is
greater than or equal to ``found_date``. A false result produces an upload
error.

.. TODO: Verify the direction of the comparison. According to the
   documented placeholders, ``+>=.`` appears to mean
   ``found_date >= end_date``, which conflicts with the accompanying
   description that ``end_date`` must be greater than or equal to
   ``found_date``. Replace the example only after testing the parser.


Adding a year to a date
~~~~~~~~~~~~~~~~~~~~~~~

On a date field that does not contain a year:

.. code-block:: text

   (year=!!^(d{4})$) {set(.)}

If the ``year`` column is not empty and contains four digits, the date field
is updated with that year.

.. TODO: Verify this example. A regular expression for four digits would
   conventionally use ``\d{4}``, but the documented expression is
   ``d{4}``. Confirm whether the backslash was lost during documentation
   formatting.

.. TODO: Explain how ``set(.)`` combines the year with the existing date
   value. The current example does not specify the input format or resulting
   value clearly.


Requiring a ring number
~~~~~~~~~~~~~~~~~~~~~~~

On the ``ring_number`` field:

.. code-block:: text

   (recapture=1) {obligatory(1)}

If ``recapture`` has the value ``1``, ``ring_number`` becomes obligatory.


Requiring an alternative name
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

On the ``english_name`` column:

.. code-block:: text

   (scientific_name=!!(^$)) {obligatory(1)}

If ``scientific_name`` is empty, ``english_name`` becomes obligatory.

.. TODO: Confirm whether the parentheses around ``^$`` are required or
   merely create a capture group.


Setting a value according to a count
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

On the ``amount_type`` field:

.. code-block:: text

   (number_of_individuals>50) {set(estimated value)},(egyedszam<=50) {set(exact value)}

If the number of individuals is greater than 50, ``amount_type`` is set to
``estimated value``. If it is 50 or less, ``amount_type`` is set to
``exact value``.

.. TODO: Verify the conditional syntax. The general grammar documents
   ``rel_field=rel_statement``, but this example places ``>`` and ``<=``
   between the field and value.

.. TODO: Confirm whether ``egyedszam`` should be
   ``number_of_individuals``. The example currently uses different field
   names for the two branches.

.. TODO: Explain whether values containing spaces, such as
   ``estimated value``, must be quoted or escaped.

.. TODO: Add tested examples for ``minmax``, ``year``, regular-expression
   replacement, several conditions on one field, and relations involving
   empty or null values.
