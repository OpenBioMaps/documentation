Modules can be turned on and off for an OpenBioMaps project. The basic functions of the system are supplemented with various functions (such as text search options). Modules can be defined per table and assigned to different users or user groups. The locations of the modules are as follows:
 - map page
 - profile tab

Most modules can be configured with simple parameters, but some modules have a custom configuration interface.

Modul administration:  
=====================

The modules can be enabled and configured on the *project_administration -> modules* page.

Add a module
------------

Module access
-------------

Drop a module
-------------

Turn off a module
-----------------

Custom modules
--------------

Parameters for modules
----------------------


Module descriptions
===================

additional_columns
------------------
    Additional columns

    Calls:

    Functions: return_columns()

    General description:
        use it together with the join_tables module
        return with an array:
        co [0] columns array
        c  [1] column name assoc array

    Parameters: New line separated list of column names

allowed_columns
---------------
    Columns visibility for users in different access levels
    It depends on the existence of _rules table

    Calls:

    Functions:
       return_columns(), return_gcolumns()

    General description:

    Parameters:
       for_sensitive_data: comma separated list of column names
       for_no-geom_data: comma separated list of column names
       for_general: comma separated list of column names

bold_yellow
-----------
    Bold yellow text for some columns in the results lists.

    Calls:

    General description:

    Parameters:
      New line separated list of column names

box_load_selection
------------------
    Map filter functions

    These functions returns with a html table which displayed beside the map window
    These are optional boxes. Setting are in the biomaps db projects' table.

    Load prevously saved spatial queries' polygons

    Calls:

    General description:

    Parameters:

        available spatial relationships (optional, if no parameter is given, all relationships are available)
            contains
            intersects
            crosses
            disjoint

box_load_coord
--------------
    Show given coordinates position on the map

    Calls: print_box, limits, ajax, print_js

    General description:

    Parameters: example:

    {
      "wgs84":"4326",
      "eov":"23700"
     }

box_load_last_data
------------------
    Query last data or last uploads.

    Calls:

    General description:

    Parameters: Number of records in last uploads, default is 10

box_custom
----------
    Custom box - only user defined version exists.

    Calls:

    General description: The custom module has to be in includes/modules/private/ folder (You have to create private folder, if it's not there. It is recomended to add read-only permissions for www-data user to avoid the deletion or modification of the custom module in the course of a system upgrade.

    Parameters: a file's basename in includes/modules/private folder. E.g. hrsz_query

    Where hrsz_query_Class is a class in hrsz_query.php in includes/modules/private/ folder.

    This Class should include at least print_box() and print_js() functions.

photos
------
    Photo or other attachment box.

    Calls:

    General description:

    Parameters:

read_table
----------
    Present a table or an sql view as a rollable html table. This table is available with a unique link.

    Calls:

    General description:
        Add these lines to .htaccess file where  .... should replaced with your project table name
        # read table module
        RewriteRule ^view-table/(.*)/$ /projects/..../includes/modules/results_asTable.php?view&table=$1&%{QUERY_STRING} [NC,L]
        
        ! This revrite rule thing is a bad idea!!!

    Parameters: 
     [{"table":"schema.table",
       "label":"somesthing",
       "orderby":"column"}, ... ]

results_summary
---------------
    Summary of results.

results_table
-------------
    Create a full html table of the results.

    Calls:

    General description:
        Not used!!

    Parameters:

results_asList
--------------
    Create foldable slides like results.

    Calls: results_builder()

    General description:

    Parameters:

results_asGPX
-------------
    Save results as a GPX file.

    Calls:

    General description:

    Parameters:

results_asCSV
-------------
    Save results as a csv file.

    Hívások:

    Általános leírás:

    Paraméterek:

results_asJSON
--------------
    Save results as a JSON file.

    Calls:

    General description:

    Parameters:

results_asSHP
-------------
    Results can be saved as SHP files. Separate files are created for the different geometry types. These can be downloaded in a zip archive.

    Calls:

    General description:

    Parameters:

results_asKML
-------------
    Save results as a KML file.

    Calls:

    General description:

    Parameters:

results_buttons
---------------
    Save and other button above results section, under map.

    Calls:

    General description:

    Parameters:

results_asStable
----------------
    Compact results table Stable.

    Calls:

    General description:

    Parameters:

specieslist
-----------
    Specieslist summary above results.

    Calls:

    General description:

    Parameters:

text_filter
-----------
    Taxon and other text filters.

    Calls:

    General description:
        create boxes
        assemble WHERE part of query string

    Parameters: complex example:

    magyar
    obm_taxon
    megj::colour_rings
    obm_datum
    obm_uploading_date
    obm_uploader_user
    d.szamossag:nested(d.egyedszam):autocomplete
    d.egyedszam:values():
    obm_files_id
    faj::autocomplete

text_filter2
-----------
    Advanced taxon and other text filters.

    Calls:

    General description:
        create boxes
        assemble WHERE part of query string

    Parameters: example:


transform_data
--------------
    Transform data

    Calls:

    General description:
        In result list it transform data as need
        E.g. geometry to wkt

    Parameters: example:

    obm_geometry:geom
    obm_uploading_id:uplid
    tema:mmm

extra_params
------------
    Extra input paramaters for forms.

    Calls:

    General description:

    Parameters:

join_tables
-----------
    Join table to use additional columns

    Calls:

    Functions: return_joins()

    General description:
        use it together with the additional_columns module
        RETURN: join command and column list and visible names list
        [0] column name , separated list
        [1] prefixed column names array: all column which defined in the database columns
        [2] visible names array of array by JOIN

    Parameters: example:

    LEFT JOIN:dinpi_mirror:dinpi_mirror.objectid=p.obm_id&dinpi_mirror.objectid>1:1

shared_geom
-----------
If this module is enabled "Manage custom geometries" option will appear on your profile page.

It is possible to upload or draw custom geometries for further action. These action can be make spatial queries or assign geometry to uploaded data.

You can manage the custom geometries in the profile page by following two links: shared geometries and own geometries.

Following the own geometries link you can delete or share, rename and modify the view options of your geometries. The view options are the following: View in spatial selection list and View in upload data - assign named spatial forms list.

Following the shared geometries link you can rename the geometries and modify the view options. You cannot delete the shared geometries!


snap_to_grid
------------
    Project specified sanp to grid points on the map

    Calls:

    Functions: geom_column(), geom_column_join(), rules_join()

    General description:
        not recommended to use!

    Parameters:

restricted_data
---------------
    Rule based data restriction

    alls

    Functions: rule_data()

    General description:

    Parameters:


identify_point
--------------
    A tool for identify one or more data elements on the map

    Calls:

    Functions: return_data(), print_button()

    General description:

    Parameters:
        column names

        json object: shows a hyperlink.

            elements:

                type - obligatory, egyelőre csak a "link" érték működik

                href - obligatory - hivatkozás címe

                label - obligatory - a link/gomb szövege/cimkéje - többnyelvűséget támogatja

                class - optional - a linkhez rendelt osztályok

                id - optional - a linkhez rendelt azonosító

                target - optional - alapértelmezett "_blank"

                params - optional - a href elem paraméterei

            A href elemet a modul-paraméterek közt felsorolt oszlopok értékeivel paraméterezhetjük. lásd a példát:

            Példa:
            { "type": "link", "href": "//example.com?nest_id=%1%&species=%2%", "label": "str_add_data", "class": "pure-button button-href", "params": ["obm_id","species"] }

            A fenti példa a következő hiperlinket fogja generálni:

            <a href="//example.com?nest_id=2898&species=Brachyramphus perdix" target="_blank" id="" class="pure-button button-href">Adat hozzáadása</a>

            A json-t egy sorosra kell tömöríteni!

        obm_files_id: Displays a photo icon on the popup if the record has an attachment.

notify
------
    Creates custom postgres based notify events.

    Calls:

    Functions: listen(), unlisten(), notify(), email()

    General description:

    Parameters:

custom_data_check
-----------------
    Custom data checks of upload data.

    Calls:

    Functions: list(), check()

    General description:

    Parameters:

custom_filetype
---------------
    Custom file preparation. E.g. observado style CSV

    Calls:

    Functions: option_list(), custom_read()

    General description:

    Parameters:

create_pg_user
--------------
If this module is enabled "Create postgres user" option will appear on your profile page.

   Create a restricted access postgres user

    Calls:

    Functions: create_pg_user(), show_button()

    General description:

        By enabling the module (who has the right to use the module), users can create their own postgres user. This user can only read from the database.
        It can read all the data tables assigned to the project.
        It can only connect to a database from one client program at a time.
        After one year, Its access expires automatically.
        Users can renew their access at any time.

    Parameters:

grid_view
---------
    View data on custom polygon grid. E.g UTM 2.5km, UTM 10KM, KEF grid, snap to grid, ...

    Calls:

    Functions: print_box(), default_grid_geom(), get_grid_layer()

    General description:

    Parameters: layer_options

    Parameters example: layer_options:kef_5 (dinpi_grid), utm_2.5 (dinpi_grid), utm_10 (dinpi_grid), utm_100 (dinpi_grid), original (dinpi_points,dinpi_grid),etrs(dinpi_grid)
    
    
    On the nnn_grid table on the comment field the layers visible names should be set:
```sql 
    COMMENT ON COLUMN public.nnn_qgrids.original IS 'original';
    COMMENT ON COLUMN public.nnn_qgrids.snap IS 'snap';
    COMMENT ON COLUMN public.nnn_qgrids.snap_polygon IS 'snap_polygon';
```

    Example trigger functions:

    Trigger on nnn_qgrids. Arguments are in the function:
```sql    
    CREATE TRIGGER update_grid_geoms BEFORE INSERT OR UPDATE ON public.tytoalba_qgrids FOR EACH ROW EXECUTE PROCEDURE public.update_qgrid_geoms_arg('0.1', '0.1', 'f', 'f', 'f', 'f', 't', 't', '0.05');
```
    Trigger on nnn table:
```sql
    CREATE TRIGGER qgrids BEFORE INSERT OR DELETE OR UPDATE ON public.debrecen_dnabank FOR EACH ROW EXECUTE PROCEDURE insert_originalgeom_into_qgrids()
```
Function insert_originalgeom_into_qgrids()
```sql
BEGIN
  IF tg_op = 'INSERT' THEN
    EXECUTE format('INSERT INTO %I_qgrids (row_id,original) SELECT %L,%L::geometry',TG_TABLE_NAME,NEW.obm_id,NEW.obm_geometry);
    RETURN NEW;
END IF;

  IF tg_op = 'UPDATE' THEN
    EXECUTE format('UPDATE %I_qgrids SET "original"=%L::geometry WHERE row_id=%L', TG_TABLE_NAME,NEW.obm_geometry,NEW.obm_id);
    RETURN NEW;
END IF;

IF tg_op = 'DELETE' THEN
    EXECUTE format('DELETE FROM %I_qgrids WHERE row_id=%L',TG_TABLE_NAME,OLD.obm_id);
    RETURN OLD;
END IF;
END;
```

Function update_qgrid_geoms_arg()
```sql
DECLARE
    snap_x numeric := TG_ARGV[0];
    snap_y numeric := TG_ARGV[1];
    kef5 boolean := TG_ARGV[2];
    kef10 boolean := TG_ARGV[3];
    utm25 boolean := TG_ARGV[4];
    utm10 boolean := TG_ARGV[5];
    snap boolean := TG_ARGV[6];
    snap_polygon boolean := TG_ARGV[7];
    snap_polygon_size numeric := TG_ARGV[8];
BEGIN

IF tg_op = 'UPDATE' THEN
    IF kef5 THEN
        EXECUTE FORMAT('SELECT geometry FROM shared."kef_5x5" WHERE st_within(%L::geometry,geometry)',NEW.original) INTO NEW."kef_5";
    END IF;
    IF kef10 THEN
        EXECUTE FORMAT('SELECT geometry FROM shared."kef_10x10" WHERE st_within(%L::geometry,geometry)',NEW.original) INTO NEW."kef_10";
    END IF;
    IF utm25 THEN
        EXECUTE FORMAT('SELECT st_transform(geometry,4326) as geom FROM shared."utm_2.5x2.5" WHERE st_within(%L::geometry,st_transform(geometry,4326))',NEW.original) INTO 
NEW."utm_2.5";
    END IF;
    IF utm10 THEN
        EXECUTE FORMAT('SELECT st_transform(geometry,4326) FROM shared."utm_10x10" WHERE st_within(%L::geometry,st_transform(geometry,4326))',NEW.original) INTO NEW."utm_10";
    END IF;
    IF snap THEN
        EXECUTE FORMAT('SELECT st_SnapToGrid(%L::geometry,%L,%L)',NEW.original,snap_x,snap_y) INTO NEW."snap";
    END IF;
    IF snap_polygon THEN
        EXECUTE FORMAT('SELECT st_expand(st_SnapToGrid(%L::geometry,%L,%L),%L)',NEW.original,snap_x,snap_y,snap_polygon_size) INTO NEW."snap_polygon";
    END IF;

    RETURN NEW;
END IF;
IF tg_op = 'INSERT' THEN

    IF kef5 THEN
        EXECUTE FORMAT('SELECT geometry FROM shared."kef_5x5" WHERE st_within(%L::geometry,geometry)',NEW.original) INTO NEW."kef_5";
    END IF;
    IF kef10 THEN
        EXECUTE FORMAT('SELECT geometry FROM shared."kef_10x10" WHERE st_within(%L::geometry,geometry)',NEW.original) INTO NEW."kef_10";
    END IF;
    IF utm25 THEN
        EXECUTE FORMAT('SELECT st_transform(geometry,4326) as geom FROM shared."utm_2.5x2.5" WHERE st_within(%L::geometry,st_transform(geometry,4326))',NEW.original) INTO 
NEW."utm_2.5";
    END IF;
    IF utm10 THEN
        EXECUTE FORMAT('SELECT st_transform(geometry,4326) FROM shared."utm_10x10" WHERE st_within(%L::geometry,st_transform(geometry,4326))',NEW.original) INTO NEW."utm_10";
    END IF;
    IF snap THEN
        EXECUTE FORMAT('SELECT st_SnapToGrid(%L::geometry,%L,%L)',NEW.original,snap_x,snap_y) INTO NEW."snap";
    END IF;
    IF snap_polygon THEN
        EXECUTE FORMAT('SELECT st_expand(st_SnapToGrid(%L::geometry,%L,%L),%L)',NEW.original,snap_x,snap_y,snap_polygon_size) INTO NEW."snap_polygon";
    END IF;

    RETURN NEW;
END IF;

END;
```

massive_edit
------------

   Allows you to edit the selected data massively on the file upload interface

   Calls:

   Functions:

   General description:

   Parameters:

download_restricted
-------------------

   Admin-controlled download authorization

   Calls:

   Functions:

   General description:

   Parameters:

job_manager (validation)
------------------------
    
    General description:
    	
    	* The job_manager (validation) module is used for managing the background processes of the project. It's parameters are the names of the jobs.
        * On the admin page you can set the time of running (simplified cron style: minute hour day), and the job parameters as json
    	* Adding a new parameter will register the job in the jobs database table, and create the necessary template files in the modules/validation_modules, jobs folders.

    Parameters:

    	* The names of the background processes
    	
    Published jobs:
    	
        observation_lists
            description: 
                This job processes and copies the observation lists collected and uploaded by the mobile app. The observations land in a temporary table, where this job completes the obm_obsevation_list_id column, the columns of start, end and duration of list. If the uploaded list is not complete the list is skipped.

            parameters:
                * list_start_column (string): column name of list start
                * list_end_column (string): column name of list end
                * list_duration_column (string): column name of list duration
                * only_time (boolean): store whole timestamp or just time
                * time_as_int (boolean): convert time to minutes
                
                {
                    "tablename": {
                        "list_start_column": "time_of_start",
                        "list_end_column": "time_of_end",
                        "list_duration_column": "duration",
                        "only_time": true,
                        "time_as_int": true
                        }
                    }
                }

    	incomplete_observation_lists
            description:
                If the uploaded list is incomplete, this module processes it. If the difference is smaller than the tolerance value, then the list will be uploaded by the next observation_list process, but a system message is sent. In other case, when the difference is larger than the tolerance only a system message is sent, the rest has to be processed manually. 
                
            paraméterezés:
                * mail_to (int): role_id - who will get the messages
                * diff_tolerance (int): tolerance of difference
                * days_offset (int): number of days to wait until the list is processed
                
                {
                    "tablename": {
                        "mail_to": 1265,
                        "diff_tolerance": 2,
                        "days_offset": 2
                    }
                }



   Calls:

   Functions:

list_manager
------------

   Calls:

   Functions:

   General description:

   Parameters:

move_project
------------

   Calls:

   Functions:

   General description:

   Parameters:
