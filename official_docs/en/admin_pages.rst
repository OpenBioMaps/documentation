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
    - rowid: not used
    - latitude: together with longitude can be used for creating spatial geometry
    - longitude: together with latitude can be used for creating spatial geometry
    - citing: used in summary functions
    - sensitive: 
    - attacment: file attacmnets colum
    - UTM Zone: used in spatial geometry creation

Groups
------
Create and manage groups

Upload forms
------------
:ref:`upload-form-management`


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
