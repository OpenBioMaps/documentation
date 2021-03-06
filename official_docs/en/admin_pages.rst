.. _project_administration:

Administrative pages
********************

Administrative access
---------------------
Administrative functions can be delegated to user groups.


.. _database-columns:

Database columns
----------------
Add new columns to a table and manage tables: assign OBM meanings to the columns.

    - data: general
    - spatial geometry: this column can be used for map creation
    - scientific species name: this column can be used in taxon management
    - alternative names: this column can be used in taxon management
    - date this column can be used in date filters
    - no. of individuals: can be used in summary functions
    - latitude: together with longitude can be used for creating spatial geometry
    - longitude: together with latitude can be used for creating spatial geometry
    - citing: used in summary functions
    - attacment: file attacmnets colum
    - UTM Zone: used in spatial geometry creation
    
The "comment field" should contain descriptions of the contents of the columns (metadata) and in some cases may have a regulatory role. For the obm_geometry column, you can specify the srid of the geometry column in the comment field, which will determine the stored srid of the uploaded data. The value entered must be in the format `srid: 4326` and stored in biomaps / header_names / f_srid and used by the application in the global variable SRID_C.

In the obm_id column, you can specify whether the rules table should be used like this: use_rules: 1 This can only be changed with master access.

In both cases, the SET prefix is automatically added to the comment field, which must be deleted for the change to take effect. This is so that these parameters cannot be accidentally changed.


Groups
------
Creating and managing groups. These groups can be used for the management of access and usage control of upload forms, data, modules and administrative functions.
The groups can contains groups.

Upload forms
------------
:doc:`upload_forms`


Functions
---------
Manage optional SQL functions and triggers:

    - Taxon list auto update: Add 'scientific name' and 'alternative names' to the taxon table which used by the taxon filter,
    - Taxon name auto update: updates the data table on taxon table updatin,
    - History: create history lines in the "history table" after update and delete rows,
    - Access rules: create a rule line in the "rules table" after inserting new row. The rules applied are from the form settings.


Species names
-------------
Taxon table management interface.
Assign species names to the following categories: [accepted name], [synonym name], [common name], [mispelled name]
The species names in the taxon table (species name database) is used by the "taxon-name-repair-background-jobs" and the search interfaces.


Access
------
Overview of set access rules and their work statuses.

Translations
------------
 
    - Global translations: global translations are periodically updated from this github repository: 
        https://github.com/OpenBioMaps/translations
        Feel free to improve translations!

    - Local translations:
        Use the 'str_' prefix, followed by some pretty understandable English expression. Eg: str_observations, the translation of which must be given in the given active language. In this case, observation.

When you change the language of a web page, you can set other translations for the same terms.

Modules
-------
:doc:`modules <../modules>`.


Interrupted uploads
-------------------
List of interrupted/saved imports of the whole project. Admins can load these imports.


File manager
------------
List of uploaded attachments. Attachments can be managed here. There is a possibility to export all attachments belonging to a data table into one compressed file using the export functionality. Exporting can take a long time due to it is using a "Background-Job". When it is ready a link will appear next to the export button to access the produced file.


SQL query settings
------------------
SQL setting for map and text quieries.

The query can contain magic-words. Some magic-word used my modules. The magic-words marked with % characters and replaced by the query creator with something valid SQL string.
 
.. code-block:: SQL
 
    SELECT obm_id, %grid_geometry% AS obm_geometry %selected%
    FROM %F%checkitout c%F%
        %uploading_join%
        %rules_join%
        %taxon_join%
        %grid_join%
        %search_join%
        %morefilter%
    WHERE %geometry_type% %envelope% %qstr%

Web Map Layers
--------------
OpenLayer settings for web-map interface


Members
-------
Project member management interface. Here you can see the group memberships of the users as well. The users' system state [admin, user, banned] can be set here. In addition, you can also access the user's profile page from here where you can also change the profile (https://fontawesome.com/v4.7.0/icon/user-secret). 


Mapserver settings
------------------
Raw version of mapfile.  See the mapserver documentation for updating this file.


## Message templates


The messages sent by the system or project must have a template. Global templates are provided for the implemented cases. Please find a list of global templates with short description.

On this page global templates can be overridden by their local version, by selecting 
a template -> editing -> and saving it. The templates can have variables which 
are substituted with the provided strings, at the moment of sending the message. 
For each template these variables are defined in the code. 

Variables are marked with %var%. A few global variables are defined, which can 
be used anywhere in the template. 

Including other templates are supported. For example if you define a footer for 
your project, this can be included by appending the @footer@ string to the end 
of the template.

New templates for custom modules or jobs can also be defined here.

### Global variables

* `%PROJECT_TABLE%` - the name of the project
* `%PROJECT_TITLE%` - the short description of the project
* `%PROJECT_DESCRIPTION%` - the long description of the project
* `%USER_NAME%` - the name of the user
* `%URL%`
* `%OB_DOMAIN%`
* `%DOMAIN%` - the domain name defined in the "projects" table
* `%PROTOCOL%` - the protocol defined in the "projects" table 

### Predefined templates

User related messages:
* `welcome_to` - welcome to the project
* `change_email_address` - a confirmation link, for changing the user's email address
* `dropmyaccount` - Confirmation email of dropping the account
* `create_new_project` - confirmation message of creating a new project
* `invitation` - invitation email
* `invitation_accomplished` - notification about the accomplished invitation
* `invitation_request` - message to admins about the invitation request
* `lostpw` - lost password

Miscellaneous:
* `new_gitlab_issue` - a copy of a submitted bug report
* `new_shared_polygon` - Project or system news about a new shared polygon
* `new_upload_news` - Project news about a new upload
* `new_upload_report` - Notification for the admins about a new upload
* `footer` - A general mail footer 
* `interconnect_request` - 

Evaluation notifications:
* `data_evaluation_commenters` - This message is sent when a record, previously commented by the user, gets a new comment.
* `data_evaluation_owner` - This message is sent to the owner if a record uploaded by him gets a comment.
* `upload_evaluation_commenters` - This message is sent when an upload, previously commented by the user, gets a new comment.
* `upload_evaluation_owner` - This message is sent when an upload of the user gets a comment.
* `user_evaluation_commenters` - This message is sent when a user, previously commented by the user, gets a new comment.
* `user_evaluation_owner` - This message is sent when the user itself get the comment.

Messages sent by modules:
* `dlr_new_request` - Notification for project admins about a new download request. - ['username', 'requestid', 'request_message']
* `dlr_request_registered` - Notification for the user that his download request was registered.
* `incomplete_list_processed` - 
* `incomplete_list_unprocessed` - 

Server logs
-----------
Read logs of mapserver or web app logger.
