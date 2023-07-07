.. _user-interfaces:

User interfaces
***************

**Contents:**

.. toctree::
   :maxdepth: 2

   profile.rst
   invitations.rst
   invitations.rst
   new_project.rst
   admin_pages.rst
   modules.rst
   upload_forms.rst
   data_query_interface.rst


Log in
======

Forgotten password
------------------
By entering your registered email address here you can request a temporary login link, which will be sent to you by email.

Profile tab
===========
:doc:`Settings related to our profile <../profile>`.


Invitations
===========
Each member can invite additional members.

:doc:`For more information, visit the invitations page <../invitations>.


Project administration
======================
:doc:`Project level settings <../admin_pages>`. For example, upload forms and map settings, or user administration.


Messages
========
Message types
--------------

Internal messages are read and sent here. Our messaging system distinguishes between four message types:

* A system message can be sent by a project or a server process to an individual user. Such a message could be, for example, a message from a background validation process.
* A personal message can be sent between users. The message editing interface can be accessed by clicking the Write Message button at the bottom left of the Messages page.
* Comment Notification - This message type is sent when someone has commented on your data, uploads or users.
* News - when uploading data, creating a new project, sharing polygons, the system creates a news item for everyone to see.

The messages page is available to all logged in users. Anyone can send messages to project members.

In addition to individual messages, project administrators can also send messages to groups or notify users of messages by email.

User settings
-------------

Users can set up email notifications for different message types. This can be done using the options on the profile page.

Additional plans
----------------

* daily aggregated notification of messages
* reply option for message body and comments 


creation of a new database
==========================

Any registered member can create a new database project, which he/she will own and will be completely independent from the project in which it was created.

:doc:`More information about creating a database<../new_project>`


Map page
========

If you have map data and valid settings (SQL, Mapserver), you can view and query the map data from this subpage. Some map settings may differ significantly, for example, only the queried data may be displayed. There may be different base maps, e.g. grids, or aerial photos, sampling locations on a map. You can display point, line and polygon data (in separate layers). Several base maps can be selected (OSM is the default). In some projects you can set up a google base map if the project owners do so by entering some google account data.

map queries
-----------
Spatial queries can be triggered by drawing on the map, by tapping on the map (info module), or by selecting pre-loaded geometries. When drawing a map, a buffer zone can be specified around the drawing pointer. That is, you can query a point by dropping a point in say a 500m radius circle, or around a line in a 10m zone.

text queries
------------
Arbitrary text query options can be set up in each project to query data, which options can include a number of helper functions such as auto-text completion, list selection, date, time, date interval selection, multiple list item selection, etc..

query storage
-------------
The result of a query can be stored on the server, which can be referenced by a persistent keyword. A DOI identifier can be requested for these identifiers. The query can also be stored, which can be used to repeat the query.



Data upload
===========
Any number of forms can be defined for a data table, with which forms different data can be loaded with different options. For example, some forms may be designed for mobile formatting only or for public data upload, while others may be designed specifically for a certain file type to be imported.
At any time during the upload process, it is possible to save and download the upload status in CSV format.

File upload
-----------
      Supported formats: 
        
        - Plain text files: csv, dsv, tsv, json
        
        - Image files: jpg, tiff (Exif columns are read out)
        
        - Spreadsheet formats: ods (Libreoffice), xls (Excel), xlsx (Excel)
        
        - Spatial formats: esri shape (.shp, .dbf, .cpg, .prj, .shx combined), gpx (GPS data format (xml)), sqlite
        
        - Genetic data files: fasta
        
      Any of the files listed here can be imported by entering a URL (simple GET query)

Web form filling
----------------


Database summary page
=====================
Each database comes with a summary page containing a description of the database and contact details.

Opening page
============
Custom landing pages can be created for projects. There are templates and pre-built functions for this, but in fact this landing page can be anything. Examples:

... figure:: images/nyitolap_1.jpg
   :scale: 50 %
   :alt: map query page
   
   No separate landing page is set

.. figure:: images/nyitolap_2.jpg
   :scale: 50 %
   :alt: boxed landing page
   
   with map on main site

.. figure:: images/nyitolap_3.jpg
   :scale: 50 %
   :alt: boxed landing page
   
   with image gallery in main location

.. figure:: images/nyitolap_4.jpg
   :scale: 50 %
   :alt: boxed landing page
   
   Full screen with slide-in image gallery


.. figure:: images/nyitolap_5.jpg
   :scale: 50 %
   :alt: boxed landing page
   
   More boxed landing pages with upload history in the main location


.. figure:: images/nyitolap_6.jpg
   :scale: 50 %
   :alt: map landing page leaflet with map
   
   Project embedded in a landing page interface


Error submission
================
The bug submission feature is available from the profile page and the upload page. Clicking on the posterized Tinder bug in the bottom right corner of the screen will bring up the bug submission interface.


... figure:: images/fault_1.jpg
   :scale: 100 %
   :alt: hiding beetle
   
   Bug in the bottom right corner

.. figure:: images/fault_2.jpg
   :scale: 100 %
   :alt: Error sending interface
   
   Simple messaging interface
   
The interface sends the errors to the OpenBioMaps developer page (https://gitlab.com/groups/openbiomaps/-/issues), from where the user will automatically receive a response from the system for further events.

The error handler can be made available on a server by specifying the AUTO_BUGREPORT_ADDRESS address in the system_vars.php.inc configuration file. More information about the GitLab Issue handler interface can be found here: https://docs.gitlab.com/ee/user/project/issues/
