:author: Miklós Bán
:date: 2026-08-10

Mobile applications
*******************

Several mobile applications support OpenBioMaps features. They include tools
for retrieving and collecting data in online and offline environments, and
range from Progressive Web Apps (PWAs) to native mobile applications.

Offline application for Android and iOS devices
================================================

Overview
--------

The offline mobile application is designed for field data collection. It
provides a flexible interface for project-specific data collection tasks and
can be used without a continuous internet connection after the required
projects and forms have been downloaded.

OpenBioMaps does not provide a single predefined data collection form or
method. Each project defines its own forms and data fields. Consequently, the
following depend on the project's configuration and the current user's
permissions:

* which projects are available;
* which forms are available within those projects;
* which fields appear on each form; and
* how those fields behave.

Only authenticated users can collect data with the application. The
application does not provide a general registration function, although some
projects may support a simple or automatic registration process outside the
application.

Development
-----------

The application is developed by Ecollab Ltd. using React Native and Expo.

Getting started
---------------

An internet connection is required to select a server and project, log in,
and download forms. After the required forms have been downloaded, they can
also be used offline.

Selecting a server
^^^^^^^^^^^^^^^^^^

Select the OpenBioMaps server hosting the project you want to use. An internet
connection is required to connect to the server and retrieve the available
project information.

Selecting a project
^^^^^^^^^^^^^^^^^^^

Select a project from the projects available on the chosen server. The
projects displayed depend on the server configuration and your access
permissions.

An internet connection is required when loading a project for the first time
or refreshing its configuration.

Logging in
^^^^^^^^^^

Log in using your email address and password. An internet connection is
required for authentication.

After a successful login, the projects and forms available to your account
can be accessed. Publicly available projects and forms may also be displayed.

Selecting a form
^^^^^^^^^^^^^^^^

Select and open a form while online to download the information required for
offline use. Once the form has been loaded successfully, it remains available
offline until its local data is removed or the form needs to be updated.

Pinning a form to the home screen
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Frequently used forms can be pinned to the home screen for quicker access.
Tap the thumbtack icon next to a form's name to pin or unpin it.

Application structure
---------------------

Main screen
^^^^^^^^^^^

The main screen provides access to:

* the map;
* forms;
* collected data;
* settings;
* track logs; and
* tools.

Pinned forms are displayed on the main screen for quick access. If an
observation event is currently running, its status is shown on the relevant
pinned form button.

Map screen
^^^^^^^^^^

The map screen is used to view recorded observations and permanent sampling
locations.

The information displayed on the map depends on the selected project, the
downloaded data, and the project's configuration.

Forms screen
^^^^^^^^^^^^

The forms screen can contain forms for:

* occasional observations; and
* observation events.

An exclamation mark next to a form indicates that an update is available.
Press and hold the form name to force an update from the server. Updating a
form requires an internet connection.

Forms downloaded for offline use are marked so that they can be distinguished
from forms that are not yet available offline.

Running observation events are indicated next to the corresponding form
name.

Collected data screen
^^^^^^^^^^^^^^^^^^^^^

The collected data screen lists observations recorded on the device. Depending
on the server-side configuration, important values such as a species name or
the number of individuals may be highlighted in the list. This behaviour can
be configured with the ``bold_yellow`` module.

From this screen, users can:

* review collected records;
* synchronise records with the server;
* edit records that have not yet been synchronised; and
* delete synchronised records from the device.

Synchronisation requires an internet connection. Before deleting local
records, verify that synchronisation has completed successfully.

Track logs screen
^^^^^^^^^^^^^^^^^

Track logs can be recorded independently of an active form. During
synchronisation, recorded track logs are uploaded to the project's track-log
table.

From this screen, users can:

* view recorded track logs;
* start track-log recording;
* stop track-log recording; and
* synchronise track logs with the server.

Tools screen
^^^^^^^^^^^^

The tools screen provides utilities that may be useful during fieldwork,
including:

* a random number generator; and
* a custom list generator, which can be used, for example, to create a list
  of ring numbers.

Settings
--------

Language
^^^^^^^^

The application currently supports English, Romanian, Hungarian, French,
German, Kyrgyz, and Russian.

You can contribute translations through the
`OpenBioMaps application translation project
<https://translate.openbiomaps.org/projects/ecollab/expo-app/>`_.

Theme
^^^^^

The application provides three theme options:

* system default;
* dark; and
* light.

Backup and export
^^^^^^^^^^^^^^^^^

A backup can be created to preserve application data or provide information
for debugging.

The export function makes data stored by the application available for use
with other software. Depending on the available data, the export can contain
standard formats such as CSV and GPX, together with attached JPEG images.

Backups and exports may contain sensitive project, location, or user data.
Store and transfer these files securely.

Form settings
^^^^^^^^^^^^^

The application provides several options for managing pinned field values:

Reinitialise whenever a form is opened
  Pinned values are reset whenever the form is opened. This is the default
  and safest option. It may be inconvenient when two forms are used in
  parallel because switching between them can reset pinned values.

Always use server settings
  The application follows the server configuration instead of preserving
  user-defined pinned values. This option is useful for users who do not need
  pinned values or tend to pin values accidentally.

Keep user settings until synchronisation
  User-defined pinned values remain available until data is synchronised.
  This is often practical when collecting the same type of data throughout a
  fieldwork session and synchronising it at the end of the day. After
  synchronisation, the pinned values are cleared.

Always keep user settings
  User-defined pinned values remain in place until they are changed manually.
  This option should be used with care because an outdated pinned value can
  accidentally be included in later records.

The application can also play a sound notification after a successful or
failed recording attempt.

Collected data settings
^^^^^^^^^^^^^^^^^^^^^^^

The collected data settings control whether the application:

* displays attached files;
* automatically synchronises collected data; and
* always displays action buttons below record details on the collected data
  screen.

Automatic synchronisation requires network access. Check the synchronisation
status before deleting records or application data from the device.

GPS and track-log settings
^^^^^^^^^^^^^^^^^^^^^^^^^^

GPS use can be filtered by time and distance. These settings affect both
single-point recording and track-log point recording.

The distance filter reduces unnecessary position updates when the device has
moved less than the configured distance. A value between 1 and 5 metres is
recommended for typical use, but the most appropriate setting depends on the
device, required accuracy, and field conditions.

The time interval determines how frequently track-log points are recorded.
The default interval is 5 seconds. Shorter intervals can produce a more
detailed track, but they can also increase battery usage and the amount of
stored data. Test the selected interval on the devices used by the project
before fieldwork.

Storage
^^^^^^^

The storage settings can be used to:

* delete unused files;
* remove unused sessions;
* clear selections; and
* clear autocomplete lists.

Review the available options carefully before deleting data. Unsynchronised
observations and track logs should be uploaded or backed up before local
application data is removed.

Permissions
^^^^^^^^^^^

The permissions screen shows whether the application has access to required
operating-system services, including location services. It also provides
access to the relevant operating-system settings.

Location permission is required for GPS-based data collection and track-log
recording. Available permission options and background-location behaviour may
differ between Android and iOS.

Server-side mobile application settings
---------------------------------------

Forms
^^^^^

Mobile data collection forms are configured through the OpenBioMaps upload
form management interface.

See :doc:`Upload form management <upload_forms>` for more information.

Online applications for mobile devices
======================================

OpenBioMaps also provides browser-based applications suitable for mobile
devices:

* :doc:`Map-based data query application <pwa>`
* :doc:`Sampling-site manager application <mapp>`
