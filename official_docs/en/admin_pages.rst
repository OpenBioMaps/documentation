.. _project_administration:

Administrative pages
********************

Administrative access
---------------------
Administrative functions can be delegated to user groups.

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
Create and manage groups

Upload forms
------------
:doc:`upload_forms`

Functions
---------
Manage optional SQL functions and triggers:

    - Taxon list auto update: Add 'scientific name' and 'alternative names' to the taxon table which used by the taxon filter
    - Taxon name auto update: updates the data table on taxon table updating
    - History: creates a history on line in history table on every update and delete
    - Access rules: Custom rules can be defined for the uploaded data user assignments.

Species names
-------------
Taxon table management interface

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
List of uploaded attacments. Attachement can be managed here.

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
Project memeber management interface.

Mapserver settings
------------------
Raw version of mapfile.  See the mapserver documentation for updating this file.

Server logs
-----------
Read logs of mapserver or web app logger.
