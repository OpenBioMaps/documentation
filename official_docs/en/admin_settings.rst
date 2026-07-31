Administrative settings
***********************

.. _administrative-access:

Administrative access
---------------------
The `Administrative access` section allows project administrators to delegate specific administrative functions to user groups. Each function available under the admin_pages can be assigned access rights to different groups created within the project. This enables fine-grained control over who can perform certain administrative tasks.

Key functionalities include:

 - **Function Assignment**: Assign access to specific administrative functions such as database management, data access, and module configuration to user groups.
 - **Access Control**: Ensure that only authorized groups have access to sensitive administrative functions, enhancing project security.

Example of access settings for a project:
 - **User-managers**: User and groups functions.
 - **Data-curators**: Access to species names, files and data manager.
 - **Upload-form-editors**: Access to form management functions.

This section is crucial for maintaining a secure and organized administrative structure within the OpenBioMaps platform.


.. _database-columns:

Database tables and columns
---------------------------
The `Database tables and columns` section allows you to create and manage SQL tables and views. Tables and columns created here are registered in the OBM metadata, making them accessible through the OBM interfaces. Note that tables and fields created via standard SQL clients are not automatically available to OBM.

### Table and Column Naming
 - **Naming Rules**: Avoid accented characters, spaces, or special characters in table names. Use lowercase letters and underscores (_) for separation. Adding a description when creating a table is strongly recommended.

### Column Management
 - **Available Columns**: Specify which columns should be available for form creation and queries in the web interface.
 - **Special Columns**: Define columns for special handling, such as species name, date, data collector, and location. These columns are used by certain modules without knowing the exact name.

### Column Types
 - **Data**: General purpose columns.
 - **Spatial Geometry**: Used for map creation.
 - **Scientific Species Name**: Used in taxon management.
 - **Alternative Names**: Used in taxon management.
 - **Date**: Used in date filters.
 - **Number of Individuals**: Used in summary functions.
 - **Latitude/Longitude**: Used for creating spatial geometry.
 - **Citing**: Used in summary functions.
 - **Attachment**: File attachments column.
 - **UTM Zone**: Used in spatial geometry creation.

### Special Fields
 - **Comment**: Contains descriptions of the column content (metadata). Adding meta descriptions is recommended.
 - **Command**: Define settings or execute actions (e.g., rename or delete columns).

### Column Commands
 - **Set SRID**: For `obm_geometry`, set the SRID using `SET srid:4326`.
 - **Use Rules**: For `obm_id`, specify rule usage with `SET use_rules:1`.
 - **Rename Column**: Use `RENAME:new-name`. Note: Renaming can corrupt upload forms.
 - **Drop Column**: Use `DROP`. Note: Deleting can corrupt upload forms; update related forms accordingly.

### SQL Console
An SQL console is available for operators with separate authentication. It provides a drop-down list of all project-related tables in the SQL database. Tables not registered as accessible to OBM are marked in red.

### Managing Views
Replace data tables with Views to create custom versions or improve performance. The system creates a Schema with the same name as the base table, moving original tables and creating corresponding INSERT/UPDATE/DELETE Rules. This is useful for large data tables with slow flows or triggers.


.. _data-access:

Data access
-----------
The `Data access` section provides an overview of the access rules set for the project and their current statuses. It allows administrators to view access levels for different user groups on the project and all managed data tables.

Key functionalities include:

 - **Access Levels**: Define access levels for reading and modifying data. The available levels are "everybody", "logged-in users", and "specified group members".
 - **Documentation Links**: Provides links to documentation for further information on access settings.
 - **Access Rules by Table**: Displays access rules for each data table, indicating whether restrictions are enabled or disabled.
 - **Restriction Management**: Allows enabling or disabling restrictions based on group access levels and predefined rules.
 - **Trigger Management**: Checks the status of triggers associated with access rules, ensuring they are enabled for proper operation.

Navigation:

 - [web] -> [profile] -> [project administration] -> [data access]
 - [system] -> [/web-app-path/] -> [/projects/YOURPROJECT/local_vars.php.inc]

This section is crucial for checking data security and ensuring that only authorized users have access to sensitive information.



Groups
------
The `Groups` section allows administrators to create and manage user groups within the OpenBioMaps platform. These groups are essential for organizing users and controlling access to various functionalities and data.

Key functionalities include:

- **Group Creation**: Create new groups by specifying a group name. This is the first step in organizing users for access management.
- **User and Group Assignment**: Assign users and other groups to a group, enabling hierarchical group structures. This allows for flexible and scalable access management.
- **Access Management**: Use groups to manage access and usage control for upload forms, data, modules, and administrative functions. Groups can be assigned specific permissions across different sections of the platform.
- **Integration with Other Sections**: Groups created here can be utilized in other administrative interfaces, such as form usage, data access and writing permissions, and module usage.

This section is crucial for maintaining organized and efficient access control within the OpenBioMaps platform.


Upload forms
------------
:doc:`upload_forms`


Functions
---------
The `Functions` section provides tools for managing SQL rules and triggers associated with project tables. It includes two main tables: Rules and Triggers, which list the rules (e.g., instead of) and triggers associated with the project's tables.

### Rules and Triggers Tables
- **Rules Table**: Displays SQL rules associated with each project table, allowing administrators to manage and review rule configurations.
- **Triggers Table**: Lists triggers for each table, providing an overview of active and inactive triggers.

### Trigger Functions
The section allows for the creation, editing, and toggling of three types of trigger functions based on templates:

- **Taxon List Trigger**: Automatically inserts species names from the species name field into the taxon table. This is useful for projects with continuously expanding species lists, ensuring that new species are added to the taxon table for maintenance and use in forms and search interfaces.

- **History Trigger**: When enabled, this trigger logs every record-level modification in the target table, including the modification timestamp and the number of changes. This is essential for tracking changes and maintaining a history of data modifications.

- **Access Rules Trigger**: Manages row-level access rules for records in project tables. This trigger can automatically restrict access to records based on a sensitive data field value or assign access rights specified in the upload form to groups. It is particularly useful for projects with restricted data access, allowing for differentiated access control for logged-in users.

These triggers are crucial for maintaining data integrity, security, and usability within the OpenBioMaps platform.


Species names
-------------
Taxon table management interface.

Assign species names to the following categories: [accepted name], [synonym name], [common name], [mispelled name].

The species names in the taxon table (species name database) are used by the "taxon-name-repair-background-jobs" and the search interfaces.



Translations
------------
- Global translations: global translations can be added and improved in our public translator platform: https://translate.openbiomaps.org.
        You can also start a new language on this interface, and translations of the mobile app and other OpenBioMaps components can be found here.
        Feel free to create, add and improve translations!

- Local translations:
        Use the ``str_`` prefix, followed by some pretty understandable English expressions. E.g.: str_observations, the translation of which must be given in the given active language. In this case, observation.

See local translations in action here: 
   https://openbiomaps.org/projects/checkitout/upload/?form=426&type=web

Modules
-------
:doc:`modules <../modules>`.


Interrupted uploads
-------------------
Users' saved and unfinished files or form data uploads can be found here. Once uploaded, they can be resumed or discarded. Most of these interrupted uploads can be deleted!


File manager
------------
The `File manager` section provides a comprehensive interface for managing uploaded attachments within the OpenBioMaps platform. It allows users to view, organize, and export attachments associated with data tables.

Key functionalities include:

- **Attachment Listing**: Displays a list of all uploaded attachments, allowing users to browse and manage files efficiently.
- **Export Functionality**: Users can export all attachments related to a specific data table into a single compressed file. This process is handled as a "Background-Job", and a download link is provided once the export is complete.
- **Filtering and Sorting**: Offers options to filter and sort attachments based on various criteria, such as upload date, file type, and associated data records.
- **Access Control**: Ensures that only authorized users can manage and export attachments, maintaining data security and integrity.
- **Interactive Interface**: Provides an intuitive interface for editing file comments, linking files to data records, and managing file associations.

These features facilitate efficient management of attachments, ensuring that users can easily access and organize their data files.


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

A typical simple SQL query looks like this:

.. code-block:: SQL
 
    SELECT obm_id, obm_geometry %selected%
    FROM %F%checkitout c%F%
        %uploading_join%
        %rules_join%
        %taxon_join%
        %morefilter%
    WHERE %geometry_type% %envelope% %qstr%

.. _Map settings:

Map settings
------------
The `Map settings` section provides comprehensive tools for configuring and managing map layers and spatial data within the OpenBioMaps platform. It includes settings for both the web map interface and the MapServer configuration.

Web Map Layers
..............
- **OpenLayers Settings**: Configure the web map interface using OpenLayers. This includes setting the map center, zoom levels, and available layers. Users can define which layers are visible by default and customize the map's appearance and behavior.

- **Layer Management**: Manage the layers displayed on the map, including adding, removing, and configuring layers. Each layer can be associated with specific data tables and queries, allowing for dynamic data visualization.

MapServer settings
..................
- **Mapfile Configuration**: The raw version of the mapfile is available for advanced users who need to update the MapServer configuration. This includes defining data sources, styling, and rendering options for map layers.

- **Spatial Reference Systems**: Configure the spatial reference systems (SRIDs) used by the map layers. This ensures that spatial data is accurately represented and aligned across different datasets.

- **Extent and Projection**: Define the map's extent and projection settings to control how spatial data is displayed. This includes setting the default projection and ensuring compatibility with various spatial data formats.

These settings are crucial for ensuring that spatial data is accurately represented and easily accessible within the OpenBioMaps platform.


Members
-------
List of members registered in the project. You can change your user status here. These are Normal, Operator, and Suspended. Suspended users do not have access to anything in the project, almost equivalent to deleting a profile.
Operators have access to all features and data. The database founder does not have to be an operator to have access to everything. Normal users will by default have access to data upload and data query options according to the project's privilege setting. This default can be modified by creating groups and assigning different permissions to groups. See :ref:`Groups<groups>` and :ref:`Administrative access<administrative-access>`.

Members' group assignments can also be modified here, but a more convenient interface is Group Manager.

The member name is a reference in this interface. Following this link will take you to the user's profile page. With administrative privileges, a tree-user-secret icon (https://forkaweso.me/Fork-Awesome/icon/user-secret/) will appear in the tab title bar - top right. Clicking on this will take you to another user's profile using your own user login details. 


Message templates
-----------------
The messages sent by the system or project must have a template. Global templates are provided for the implemented cases. Please find a list of global templates with short descriptions.

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

Global variables
................
* `%PROJECT_TABLE%` - the name of the project
* `%PROJECT_TITLE%` - the short description of the project
* `%PROJECT_DESCRIPTION%` - the long description of the project
* `%USER_NAME%` - the name of the user
* `%URL%`
* `%OB_DOMAIN%`
* `%DOMAIN%` - the domain name defined in the "projects" table
* `%PROTOCOL%` - the protocol defined in the "projects" table 

Predefined templates
....................
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
* `user_evaluation_owner` - This message is sent when the user itself gets the comment.

Messages sent by modules:
* `dlr_new_request` - Notification for project admins about a new download request. - ['username', 'requestid', 'request_message']
* `dlr_request_registered` - Notification for the user that his download request was registered.
* `incomplete_list_processed` - 
* `incomplete_list_unprocessed` - 

Server info
-----------
The `Server info` section provides comprehensive details about the server's current status and configuration. It includes:

- **Application Version**: Displays the current version of the OpenBioMaps application.
- **Storage Usage**: Shows the disk usage of project files, including attachments and uploads.
- **System Load**: Provides the server load averages over 1, 5, and 15 minutes, normalized by the number of CPU cores.
- **Memory Usage**: Displays the amount of free memory available on the server.
- **Supervisor Link**: Offers a direct link to the Supervisor project administration interface for further server management.

This information is crucial for administrators to monitor server performance and ensure optimal operation.

Server logs
-----------
The `Server logs` section allows administrators to view and manage logs generated by the system. It includes:

- **Log Sources**: Administrators can select from different log sources such as system logs, mapserver logs, job events, and job errors.
- **Filtering and Searching**: Provides options to filter logs by specific criteria and search for particular entries.
- **Access Control**: Ensures that only authorized users can view logs, maintaining security and privacy.
- **Real-time Updates**: Supports real-time log updates for continuous monitoring of server activities.

These features help in diagnosing issues, tracking system activities, and maintaining security compliance.

Members
-------
List of members registered in the project. You can change your user status here. These are Normal, Operator, and Suspended. Suspended users do not have access to anything in the project, almost equivalent to deleting a profile.
Operators have access to all features and data. The database founder does not have to be an operator to have access to everything. Normal users will by default have access to data upload and data query options according to the project's privilege setting. This default can be modified by creating groups and assigning different permissions to groups. See :ref:`Groups<groups>` and :ref:`Administrative access<administrative-access>`.

Members' group assignments can also be modified here, but a more convenient interface is Group Manager.

The member name is a reference in this interface. Following this link will take you to the user's profile page. With administrative privileges, a tree-user-secret icon (https://forkaweso.me/Fork-Awesome/icon/user-secret/) will appear in the tab title bar - top right. Clicking on this will take you to another user's profile using your own user login details.

Background jobs
---------------
[web] -> [profile] -> [project administration] -> [background processes]

OBM can perform tasks in the background. You can download background process scripts from the git repo available on the page and modify them or write a completely new one based on the template script. The shell processes have a run and a lib file. The scheduler calls our run file which, in the case of a standard php job, executes the tasks in the lib file.

The scheduler is cron-like, you have to fill in minute - hour - day fields, which can be * in both cases, i.e. every minute, hour, and day has a value. The job will not run if not enabled. You can test it without enabling [run]. With [results] you can see the last results of the job.

To run the scheduler, the host must also have a scheduler cron entry for each project job running script. This can be configured by the server administrator. E.g:

```
*/5 * * * * * /usr/local/bin/docker-compose -f /srv/docker/openbiomaps/docker-compose.yml exec -u www-data -T app php /var/www/html/biomaps/root-site/projects/myproject/jobs.php
```

Project description
-------------------
Here you can set the project name displayed in the header of the project page (short description) and the long description of the project for each language.


Data management
---------------
The Data Management section provides tools for managing and summarizing data uploads and observation lists. It includes features for viewing observation lists by uploader, date, and tracklog, as well as summarizing data uploads by user and table.

Key functionalities include:

- **Observation Lists**: View observation lists filtered by uploader, date, or tracklog. This allows administrators to quickly access and review data submissions.
- **Data Upload Summary**: Provides a summary of data uploads, showing the number of records uploaded by each user for each table. This is useful for monitoring data contributions and identifying active contributors.
- **User Activity**: Lists observation lists submitted by users in the last 90 days, helping to track recent activity and engagement.
- **Tracklogs**: Displays tracklogs submitted in the last 30 days, including details such as start and end times, track names, and associated observation lists.

The interface also includes interactive tables for exploring data, with options for filtering and sorting to facilitate data analysis and review.
