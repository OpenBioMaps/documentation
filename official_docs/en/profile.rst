.. _profile:

Profile page
************

User data
---------

Settings
--------
    Visible email address for project members: 
    Receiv e-mails from the project:
    Drop profile
    

ORCID profile
-------------
   Add ORCID profile ID, Load ORCID profile data (if filled correctly)


User information
----------------
state: normal or master
evaluation: A value between 0 and 1; this value comes from data evaluation and user evaluations that apply to us.

Other databases
---------------
List of all databases manage by yourself.


Activity
--------
This part shows the number of uploads and data by yourself. Number of modified records as well.
Species statistics: This is a list of species from your uploads and an evaluation of this list.


Interrupted imports
-------------------
While uploading new data using the web forms or file uploads there is an option to save the actual state of the prepared data.

When you save the uploading process your data and settings will be stored in the OBM server. You can restore the saved state by loading its identifier.

The identifiers are generating automatically. In one SESSION and one form there is only one identifier. So, there is no incremental backup!

You can follow your saved imports in the profile page, by click on the "interrupted imports" link. 


Stored queries
--------------
It is possible to save a permanent copy of the queried data in the OBM servers. These saved queries are repeatable later using its query identifier.

The query identifiers are generated automatically when you save a query on the main map window. Also you can give a name for the saved queries.

On the administrative pages you can follow your saved queries by clicking on the "stored queries" link. 


Saved results
-------------
It is possible to save queries and repeat them by using these ID-s.


Api keys
--------
Active API keys. It is an authentication related function. You can follow your connections and manually close them. Mostly the developers use it.

The following page items are optional and related to specific modules allowed in your project.

Modul specific settings
-----------------------
Some modules can expose management interfaces here. For example: postgres user creation module, geometry upload module, download request module, etc...

Manage custom geometries
........................
This function is only available when the shared_geoms modul allows.

It is possible to upload or draw custom geometries for further action. These action can be make spatial queries or assign geometry to uploaded data.

You can manage the custom geometries in the profile page by following two links: shared geometries and own geometries.

Following the own geometries link you can delete or share, rename and modify the view options of your geometries. The view options are the following: View in spatial selection list and View in upload data - assign named spatial forms list.

Following the shared geometries link you can rename the geometries and modify the view options. You cannot delete the shared geometries!

Create PostgreSQL user
......................
Create an active user for one year with read access to the project's data tables via SQL client programs. Required to use QGIS!



Opinions
--------
User opinions about your activities.
