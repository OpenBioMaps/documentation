.. _user-interfaces:

User interfaces
***************


Log in page
===========

Forgotten password
------------------
By entering your registered email address here, you can request a temporary login link, which will be sent to you by email.

Registration
------------
To join OpenBioMaps projects on a server, a user must receive an invitation from another user unless public registration with external service authentication is enabled. Invitations can be requested on the login interface by following the registration link. Project administrators receive the invitation requests. Depending on the project settings, the system may automatically send an invitation in response to the registration request, or a project administrator send the invitation. The invitation email contains a link that the user can click to join the project. During the joining process, the user must confirm their intention to join, accept the terms of the user agreement and the data processing declaration, and finally set a password. Optionally, they can also provide additional information about themselves.

Profile page
============
:doc:`Settings related to our profile <../profile>`.

Invitations
-----------
By default, all registered users can invite additional members.

:doc:`For more information, visit the invitations page <../invitations>`.

Messages
--------
Projects have an internal messaging system that can include both automated and personal messages. The system is capable of forwarding messages to the user's email address, which can be set on the profile page. The message sending interface, accessible as a standalone element from the profile page, allows users to search for their messages and create new ones, categorized into five categories: Personal Messages, Sent Messages, System Messages, Ratings and Comments, and News Feed. Administrators can send messages to other users in groups and via email. Regular users can also send messages individually to other users. Client applications can read the user's messages; for example, the mobile application will notify us when project administrators or other users send us messages or when we receive ratings or comments from other users regarding the data we uploaded.

Creation of a new database
--------------------------
Any registered member can create a new database project, which he/she will own and will be completely independent of the project in which it was created.

:doc:`More information about creating a database<../new_project>`


Project administration
======================
:doc:`Project settings <../admin_pages>`. For example, upload forms and map settings, or user administration.


Map page
========

If you have map data and valid settings (SQL, Mapserver), you can view and query the map data from this subpage. Some map settings may differ significantly, for example, only the queried data may be displayed. There may be different base maps, e.g., grids or aerial photos, and sampling locations on a map. You can display point, line, and polygon data (in separate layers). Several base maps can be selected (OSM is the default). In some projects, you can set up a Google base map if the project owners do so by entering some Google account data.

map queries
-----------
Spatial queries can be triggered by drawing on the map, tapping on the map (info module), or selecting pre-loaded geometries. When drawing a map, a buffer zone can be specified around the drawing pointer. That is, you can query a point by dropping a point in say a 500m radius circle, or around a line in a 10m zone.

text queries
------------
Arbitrary text query options can be set up in each project to query data, which options can include several helper functions such as auto-text completion, list selection, date, time, date interval selection, multiple list item selection, etc...

query storage
-------------
The result of a query can be stored on the server and referenced by a persistent keyword. A DOI identifier can be requested for these identifiers. The query can also be stored and used to repeat it.



Data upload page
================
Any number of forms can be defined for a data table, allowing different data to be loaded with different options. For example, some forms may be designed for mobile-only formatting or public data upload, while others may be designed specifically for a particular file type to be imported.
At any time during the upload process, you can save and download the upload status in CSV format.

File upload
-----------
Supported formats: 
        
- Plain text files: CSV, DSV, TSV, JSON
- Image files: jpg, tiff (Exif columns are read out)
- Spreadsheet formats: ods (LibreOffice), xls (Excel), xlsx (Excel)
- Spatial formats: ESRI shape (.shp, .dbf, .cpg, .prj, .shx combined), GPX (GPS data format (XML)), SQLite
- Genetic data files: fasta
        
Any of the files listed here can be imported by entering a URL (simple GET query)

Web form filling
----------------
Web forms are a variant of forms that can only be used on the project's web interface (similar to file uploads), allowing records to be created by filling out a table. By default, the table functions like a spreadsheet application. The field names of our database are in the column headers, and we fill in the rows. A table of arbitrary length can be created, but for very large tables, we recommend using the file upload option, where a table prepared in a spreadsheet application can be uploaded. This interface is typically a tool for preparing and uploading a few dozen, at most a few hundred rows of records. The headers of the required fields are red, while those of the optional fields are gray (the same applies to file uploads). Below the header of each field is a yellow field that serves for bulk filling of the fields. This interface provides several convenience functions for bulk modification of the field contents. It is possible to skip rows or apply various formatting and transformation functions to individual columns.

External applications
---------------------
    
* Use of API interface (e.g. mobile app, R-package)
* Use SQL connection (e.g. QGIS)

Export data from the upload process
-----------------------------------
During the data upload process and from the saved state of interrupted uploads, the data can be exported to a CSV file.

Abort data upload
-----------------
The data upload process can be interrupted at any time from the web interface. A backup is automatically created every 2 minutes, but you can create one at any time by clicking the Save button in the redundant menu bar. 

Uploads that have been suspended can be restored by selecting them from the 'Suspended Uploads' list on the profile page.

Completed uploads are automatically deleted from the list.

Data upload history page
------------------------
The metadata for each data upload is automatically recorded and can be accessed on the user's profile page or in the datasheet.

Datasheet page
==============
Each data record has its data sheet, which contains all the associated metadata and data fields for the record. Depending on the settings, the available data content can be restricted in various ways.

Data history page
-----------------
Each data record has its data history sheet, where you can view the changes to the record. This feature only works if the project host has enabled data change records in the project settings.


Database summary page
=====================
Each database includes a summary page with a description and contact details.


Welcome page
============
:doc:`Variable welcome pages can be set for each project <../welcome_page>`.


Error reporting
===============
The bug submission feature is available from the profile page and the upload page. Clicking the bug in the bottom-right corner of the screen will open the bug submission interface.

.. figure:: images/hiba_1.jpg
   :scale: 100 %
   :alt: hiding beetle
   
   Bug in the bottom right corner

.. figure:: images/hiba_2.jpg
   :scale: 100 %
   :alt: Error sending interface
   
   Simple messaging interface
   
The interface sends errors to the OpenBioMaps developer page (https://gitlab.com/groups/openbiomaps/-/issues), from which the user will automatically receive a system response for subsequent events.

The error handler can be made available on a server by specifying the AUTO_BUGREPORT_ADDRESS address in the system_vars.php.inc configuration file. More information about the GitLab Issue handler interface can be found here: https://docs.gitlab.com/ee/user/project/issues/
