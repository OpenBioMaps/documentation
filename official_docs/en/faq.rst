.. raw:: html

    <style> 
    .red {color:#ff0000;font-weight:bold;}
    .green {color:#00ff00;font-weight:bold;}
    </style>

Frequently Asked Questions
**************************

What is OpenBioMaps?
--------------------
OpenBioMaps is a software and services platform for managing biological data. It can be used on its own or as a service. It can be used to create database-based projects that can be used simultaneously by multiple users with different devices and access privilege levels. If you do not wish to maintain your server, you can use it as a service, as some institutions also operate servers that host research or citizen-science projects for no charge.

What is OpenBioMaps Consortium?
-------------------------------
:doc:`See Consortium <../introduction#OpenBioMaps Consortium>`


How can I create/find a new database-project?
----------------------------------------------
If you are already a member of a project on a server, you can use the web interface to create a new database project on the same server. This is a simple process that can be done by filling in a form.


How can I upload data?
----------------------
Simply answered: using data upload forms.
Or perhaps using any PostgreSQL client, although this solution is only recommended for occasional imports of large amounts of data.


How can I access data?
----------------------
- Via the web interface with map or text queries. 
- Using a PostgreSQL client.
- Using the OpenBioMaps R package.
- Using data sharing via the web interface.
- Data export via the web interface.
- Width the :doc:`PWA application <../pwa>`

How can I retrieve data with my mobile phone?
---------------------------------------------
With the :doc:`PWA application <../pwa>`


How can I sign up for an OpenBioMaps project?
---------------------------------------------
Registration requires an invitation. Any registered member can invite new users. In addition, by default, an invitation request form is available from the login interface, which can be filled in by new hosts to request an invitation to join a project. In addition, there is an OpenID module that allows registration and login with a Google Account.

For more information on registration and invitations, please contact the creators or administrators of the database you wish to join.


Is there a programmable interface for developers?
--------------------------------------------------
Yes. The Project Data Service (PDS) allows you to query projects and user data on a per-project basis through URL requests from databases.

Example: https://openbiomaps.org/pds.php?scope=get_project_list

For more information visit the API documentation.

What language support is available?
-----------------------------------
There are no language restrictions, but OpenBioMaps is currently available in Hungarian, English Romanian, Spanish, and partially in Russian. Additional languages or translations can be added through the https://translate.openbiomaps.org interface.

Each project can have individual language settings and associated translations.


How can I contribute to OpenBioMaps?
------------------------------------
- By creating/establishing a database project
- Uploading data to a database project
- By creating a new OpenBioMaps server
- Hosting database-project on your server
- Adding new languages or improving existing translations
- Software development
- Financial support


Should I pay for anything?
--------------------------
All components and services of OpenBioMaps are completely free of charge, but some of the development is not voluntary work, i.e. we pay the developers, so all support for the development is gratefully accepted!


How and where does the OpenBioMaps store the data?
--------------------------------------------------
Each OpenBioMaps server stores the data in its own database and file system.


Is there any backup solution?
-----------------------------
No centralized backup, as there is no centralized data management in OpenBioMaps. Each server has its own backup solution, but some servers use each other's storage capacity for archiving.


I lost my password, how can I get a new one?
--------------------------------------------
Don't worry, it's very easy to get a new password.

Follow the "lost password" link on the login page.

There you can enter your login email address. Once you submit it, you will receive an email from the system containing a link that you can follow to log in to your account and set a new password.


Pink squares appear on the map page
-----------------------------------
This may be due to some kind of configuration error, which may be related to the map layers or the settings of the data queries.


What is the RUM?
----------------
RUM is an acronym for database openness classes:

Read - Upload - Modify

Each element can have a value of [-] or [0] or [+].

where

[-] is not public, [0] is partially public and the [+] is public

and the colors are: [-] black, [0] red and [+] green

e.g.

<font color="red">R</font><font color="green">U</font>M partial public read, public upload and no public modify 


Is it possible to assign a DOI to databases?
--------------------------------------------
Yes, all databases in a finalized state can receive a DOI using the DataCite DOI Service.

All databases have a DOI metadata page like:

https://dinpi.openbiomaps.org/projects/danubefish/index.php?metadata

Our DOI prefix in DataCite is: 10.18426

The DOI suffixes are automatically generated and they are unique.

In every database, it is possible to assign additional DOI-s for datasets.


Where can I find the list of the existing OpenBioMaps servers?
--------------------------------------------------------------
The servers that have registered can be found in the OpenBioMaps database at https://openbiomaps.org/projects/openbiomaps_network.


How to use the OpenBioMaps mobile app?
--------------------------------------
On iPhone or Android (currently, only the Android version works). Users need to be logged in on their server to access the data upload forms available in their project. After logging in and downloading the forms, the app can be used offline. The current base map is Google-based and only works offline if the target area is downloaded for offline use from the Google Terrain Map application.

The mobile application lists the servers that are registered in the https://openbiomaps.org/projects/openbiomaps_network database.


Where can I find the OpenBioMaps R package?
-------------------------------------------
For now, only available as a developer package here: https://github.com/OpenBioMaps/obm.r

What data download options are there?
-------------------------------------
* Using CSV, KML, JSON, and other modules where available
* Via QGIS
* Using bookmarks and permanent links
* Using the R package

How/where can I access photos taken in the field with the mobile app?
---------------------------------------------------------------------

On the web interface, one by one on the data's data page, or in the administrative interface on the files tab. You can also download all the photos in one operation. The PDS API also supports downloading images in one download. Also via the supervisor interface (located on the administrative functions / system information page).

How can I delete data?
----------------------
The OBM web interface does not include a data deletion function, but there is still the possibility to delete data if it is deemed necessary.
Each upload has an entry in the system.uploadings table. Its ID can be referenced to delete all records of an upload from the SQL client at once. If the uploading table is linked to the data table with a foreign key, it is sufficient to delete the uploading metadata row and it will delete the corresponding rows from the data table, but this linkage is not automatically set. It is usually safer to explicitly delete the required rows with an SQL command. If you want to delete all rows of an upload, it is handy to do it with a single command referring to the upload ID:

.. code-block:: sql

   DELETE FROM your_table WHERE uploading_id=x;


I can't query/see data which is visible to other users
-------------------------------------------------------
The project data is likely restricted access, which is defined as only certain users or groups of users having access to the data. In practice, this setting is enforced by specifying in the data upload form settings which users or user groups will have read or modify access to data uploaded with a particular form. 
If there is data uploaded where no settings have been made, then by default only the project admins will have access to the data uploaded. The data access setting can be changed subsequently by the project admins using SQL commands, e.g: 

.. code-block:: sql

   UPDATE mydatabase_rules d SET read = read || 295 FROM (
   SELECT row_id FROM "public". "mydatabase" LEFT JOIN mydatabase_rules ON (obm_id=row_id) WHERE "observer" ILIKE 'Smith%') AS foo 
   WHERE foo.row_id=d.row_id


