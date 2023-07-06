.. _project_administration:

Administrative pages
********************

Administrative access
---------------------
Administrative functions can be delegated to user groups.


.. _database-columns:

Database tables and columns
---------------------------

[web] -> [profile] -> [project administration] -> [database table management]

We can create a SQL table that OBM registers to our project and creates the default OBM columns in it. The table name should not contain accented characters, spaces or other special characters! Avoid using capital letters! The _ character is allowed. It is strongly recommended that a description of arbitrary length be provided for the table.

Only tables registered here can be used in the OBM interface (map display, form use, text queries)!

Here, you can set which columns from each table should be available for form creation and queries in the web interface. 

Also, here you can specify the columns to be specially handled. This means that columns that are used by certain modules without knowing the exact name of the column or on the same basis are available in meta queries. Such privileged columns are the species name, date, data collector, copy number and location columns. For the location column, the X,Y coordinate column and the Postgres geometry column can be specified separately. For date, multiple date columns can be specified, for data collector, multiple columns can be specified. For species name, the column containing the scientific name and national name can be specified separately if available. All other columns must be set to "data" type.

    - data: for general purpose columns
    - spatial geometry: this column can be used for map creation
    - scientific species name: this column can be used in taxon management
    - alternative names: this column can be used in taxon management
    - date this column can be used in date filters
    - no. of individuals: can be used in summary functions
    - latitude: together with longitude can be used for creating spatial geometry
    - longitude: together with latitude can be used for creating spatial geometry
    - citing: used in summary functions
    - attachment: file attachments column
    - UTM Zone: used in spatial geometry creation

The 'comment field' should contain descriptions of the content of the columns (metadata) and may also have a regulatory role in some cases. In the case of the obm_geometry column, the comment field can be used to specify the geometry column's srid, which will define the stored srid of the uploaded data. The value entered must be in the format `srid:4326` and will be stored in biomaps/header_names/f_srid and used by the application in the global variable SRID_C.

For the obm_id column, you can specify whether the rules table should be used as follows: use_rules:1 This can only be modified with master access.

In both cases, the SET prefix is automatically added in the comment field and must be cleared in order to validate the change. This is done to prevent accidental modification of these parameters.

An SQL console is available at the top of the page, which can only be used with operator status and after separate authentication.

Also available here is a drop-down list of all the tables that start with the name of our project in the SQL database. Of these, the ones marked in red are not handled by the OBM interface because they are not registered as tables accessible to OBM.

Views management is mainly used to serve a specific function, namely to replace one of our data tables with a View. In such a case, the system creates a Schema for our project with the same name as the base table and moves our original tables there, for which it also creates the corresponding INSERT/UPDATE/DELETE Rules. This feature can be useful when we have a large data table and there are some flows or triggers that are too slow to use, or we want to create custom versions of our data table to meet some specific user needs.


Groups
------
Creating and managing groups. These groups can be used for the management of access and usage control of upload forms, data, modules, and administrative functions.
The groups can contain groups.


Upload forms
------------
:doc:`upload_forms`


Functions
---------
Some pre-built triggers can be turned on and off here, and the associated functions can be edited.

You can also view the status of all triggers and SQL Rules associated with the selected table.

Built-in triggers:
    - Taxon list auto update: Add 'scientific name' and 'alternative names' to the taxon table which is used by the taxon filter,
    - Taxon name auto update: updates the data table on taxon table updating,
    - History: create history lines in the "history table" after updating and delete rows,
    - Access rules: create a rule line in the "rules table" after inserting a new row. The rules applied are from the form settings.


Species names
-------------
Taxon table management interface.
Assign species names to the following categories: [accepted name], [synonym name], [common name], [mispelled name]
The species names in the taxon table (species name database) are used by the "taxon-name-repair-background-jobs" and the search interfaces.

.. _data-access:

Access
------
Overview of set access rules and their work statuses.

[web] -> [profile] -> [project administration] -> [data access]

[system] -> [/web-app-path/] -> [/projects/YOURPROJECT/local_vars.php.inc]

View the general access setting of the project per data table. This is not configurable here!

Translations
------------
 
    - Global translations: global translations can be added and improved in our public translator platform: https://translate.openbiomaps.org.
        You can also start a new language on this interface, and translations of the mobile app and other openbiomaps components can be found here.
        Feel free to create, add and improve translations!

    - Local translations:
        Use the 'str_' prefix, followed by some pretty understandable English expressions. Eg: str_observations, the translation of which must be given in the given active language. In this case, observation.

See local translations in action here: 
   https://openbiomaps.org/projects/checkitout/upload/?form=426&type=web

Modules
-------
:doc:`modules <../modules>`.


Interrupted uploads
-------------------
Users' saved and unfinished file or form data uploads can be found here. Once uploaded, they can be resumed or discarded. Most of these interrupted uploads can be deleted!


File manager
------------
List of uploaded attachments. Attachments can be managed here. There is a possibility to export all attachments belonging to a data table into one compressed file using the export functionality. Exporting can take a long time due to it using a "Background-Job". When it is ready a link will appear next to the export button to access the produced file.


SQL query settings
------------------
Here you can configure the SQL queries that Mapserver will use to display the map data and the web application will use to display the text results of the queries.
These are mostly not real SQL commands, but templates for SQL query assembly with approximate SQL syntax.

In the Mapserver/map file, WMS layers must contain a DATA definition line with a %query% substitution string to use a dynamically generated SQL command based on the SQL template defined here.

All SQL queries should be connected with one web map layer. In the last column, you can set these connections. In the SQL queries, there are two substitute variables to perform dynamic queries: %qstr% and %morefilters%.

The query may contain magic words. These are delimited by % characters. These will be dynamically replaced by real SQL strings in the OBM SQL interpreter.
Some modules may also generate such magic words!
 
.. code-block:: SQL
 
    SELECT obm_id, %grid_geometry% AS obm_geometry 
        %selected%
    FROM %F%checkitout c%F%
        %uploading_join%
        %rules_join%
        %taxon_join%
        %grid_join%
        %search_join%
        %morefilter%
    WHERE %geometry_type% %envelope% %qstr%

Use %F% and an alias name around the FROM table. It is necessary to split the query template.

If you want to join another table use the %J% around the JOIN statement. E.g.

.. code-block:: SQL

    SELECT n.obm_geometry,n.obm_id,-2 AS date_part,nestbox_type,project_id,beinaction
        %selected%
    FROM %F%public_nestbox_data n%F%
        %J%LEFT JOIN public_nestbox_data_observations o ON o.nestbox_id=n.obm_id%J%
        %taxon_join%
        %morefilter%
    WHERE %envelope% %qstr%

Building more complex queries is possible:

.. code-block:: SQL

    WITH aall AS (
        SELECT o.obm_id,n.obm_geometry,nestbox_type,project_id,beinaction,
        COALESCE(extract(days FROM (CURRENT_DATE-datum)::interval),'-1') as  date_part
            %selected% 
        FROM %F%public_nestbox_data_observations o%F%
        %J%LEFT JOIN public_nestbox_data n ON (nestbox_id=n.obm_id) %J%
        %taxon_join%
        %morefilter% 
        WHERE 1=1 %envelope% %qstr% 
    )
    SELECT * FROM aall ORDER BY date_part DESC


.. _Map settings:

Map settings
------------
Web Map Layers
..............
OpenLayer settings for web-map interface

Mapserver settings
..................
Raw version of mapfile.  See the mapserver documentation for updating this file.


Members
-------
Project member management interface. Here you can see the group memberships of the users as well. The users' system state [admin, user, banned] can be set here. In addition, you can also access the user's profile page from here where you can also change the profile (https://fontawesome.com/v4.7.0/icon/user-secret). 




## Message templates


The messages sent by the system or project must have a template. Global templates are provided for the implemented cases. Please find a list of global templates with short description.

On this page, global templates can be overridden by their local version, by selecting 
a template -> editing -> and saving it. The templates can have variables that 
are substituted with the provided strings, at the moment of sending the message. 
For each template, these variables are defined in the code. 

Variables are marked with %var%. A few global variables are defined, which can 
be used anywhere in the template. 

Including other templates are supported. For example, if you define a footer for 
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

User-related messages:
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

Server info
-----------
There is a lot of basic information available about the project, such as the application version number, storage usage, system load and memory usage, and a link to the Supervisor project administration interface.

Server logs
-----------
Read logs of mapserver or web app logger.

Members
-------
List of members registered in the project. You can change your user status here. These are Normal, Operator, Suspended. Suspended users do not have access to anything in the project, almost equivalent to deleting a profile.
Operators have access to all features and data. The database founder does not have to be an operator to have access to everything. Normal users will by default have access to data upload and data query options according to the project's privilege setting. This default can be modified by creating groups and assigning different permissions to groups. See :ref:`Groups<groups>` and :ref:`Administrative access<admin-group-access>`.

Members' group assignments can also be modified here, but a more convenient interface is Group Manager.

The member name is a reference in this interface. Following this link will take you to the user's profile page. With administrative privileges, a tree-user-secret icon (https://forkaweso.me/Fork-Awesome/icon/user-secret/) will appear in the tab title bar - top right. Clicking on this will take you to another user's profile using your own user login details.

Background jobs
---------------
[web] -> [profile] -> [project administration] -> [background processes]

OBM can perform tasks in the background. You can download background process scripts from the git repo available from the page and modify them or write a completely new one based on the template script. The shell processes have a run and a lib file. The scheduler calls our run file which, in the case of a standard php job, executes the tasks in the lib file.

The scheduler is cron-like, you have to fill in a minute - hour - day fields, which can be * in both cases, i.e. every minute, hour, day has a value. The job will not run if not enabled. You can test it without enabling [run]. With [results] you can see the last results of the job.

In order to run the scheduler, the host must also have a scheduler cron entry for each project job running script. This can be configured by the server administrator. E.g:

```
*/5 * * * * * /usr/local/bin/docker-compose -f /srv/docker/openbiomaps/docker-compose.yml exec -u www-data -T app php /var/www/html/biomaps/root-site/projects/myproject/jobs.php
```
