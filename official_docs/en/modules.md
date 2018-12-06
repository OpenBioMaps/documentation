specieslist
-----------
    Specieslist summary above results.
    
    Calls:
    
    General description:

    Parameters:

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
    Save results as a shp file.
    
    Calls:
    
    General description:
    
    Parameters:
    
results_buttons
---------------
    Save and other button above results section, under map.
    
    Calls:
    
    General description:
    
    Parameters:

photos
------
    Photo or other attachment box.
    
    Calls:
    
    General description:
    
    Parameters:
    
box_load_selection
------------------
    Map filter functions

    These functions returns with a html table which displayed beside the map window
    These are optional boxes. Setting are in the biomaps db projects' table.
    
    Load prevously saved spatial queries' polygons
    
    Calls:
    
    General description:
    
    Parameters:
    
box_load_coord
--------------
    Show given coordinates position on the map
    
    Calls: print_box, limits, ajax, print_js
    
    General description:
    
    Parameters:
    
box_load_last_data
------------------
    Query last data or last uploads.
    
    Calls:
    
    General description:
    
    Parameters:
    
box_custom
----------
    Custom box - only user defined version exists.
    
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
    
    Parameters:
    
transform_data
--------------
    Transform data

    Calls:
    
    General description:
        In result list it transform data as need
        E.g. geometry to wkt
    
    Parameters:
    
results_asStable
----------------
    Compact results table Stable.
    
    Calls:
    
    General description:
    
    Parameters:
    
allowed_columns
---------------
    Columns visibility for users in different access levels
    It depends on the existence of _rules table
    
    Calls: 
       
    Functions:
       return_columns(), return_gcolumns()
    
    General description:
    
    Parameters: 
       column names
       *column names
    
bold_yellow
-----------
    Bold yellow text for some columns in the results lists.
    
    Calls:
    
    General description:
    
    Parameters:
      column names

extra_params
------------
    Extra input paramaters for forms.

    Calls:
    
    General description:
    
    Parameters:
    
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
    
    Parameters:

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
    
form_choose
-----------
    List of available forms.

    Calls:
    
    Functions: form_list()
    
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
  
create_postgres_user
--------------------
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

custom_admin_pages
------------------

    
    Calls:
    
    Functions: no functions.
    
    General description:
    
    Parameters:
    
grid_view
---------
    View data on selected polygon grid
    
    Calls: 
    
    Functions: print_box(), default_grid_geom(), get_grid_layer()
    
    General description:
    
    Parameters:
    
    Example trigger function:

```sql
BEGIN

IF tg_op = 'INSERT' THEN

    EXECUTE format('INSERT INTO %I_qgrids (row_id,original) SELECT %L,%L::geometry',TG_TABLE_NAME,NEW.obm_id,NEW.obm_geometry);

    EXECUTE format('UPDATE %I_qgrids SET "kef_5" = foo.geom FROM ( 
        SELECT obm_geometry AS geom
        FROM shared."kef_5x5"
        WHERE st_within(%L::geometry,obm_geometry)
    ) as foo WHERE row_id=%L',TG_TABLE_NAME,NEW.obm_geometry,NEW.obm_id);

    EXECUTE format('UPDATE %I_qgrids SET "kef_10" = st_transform(foo.geom,4326) FROM ( 
        SELECT geom
        FROM shared."kef_10x10"
        WHERE st_within(%L::geometry,st_transform(geom,4326))
    ) as foo WHERE row_id=%L',TG_TABLE_NAME,NEW.obm_geometry,NEW.obm_id);

    EXECUTE format('UPDATE %I_qgrids SET "utm_2.5" = st_transform(foo.geom,4326) FROM ( 
        SELECT geometry as geom
        FROM shared."utm_2.5x2.5"
        WHERE st_within(%L::geometry,st_transform(geometry,4326))
    ) as foo WHERE row_id=%L',TG_TABLE_NAME,NEW.obm_geometry,NEW.obm_id);

    EXECUTE format('UPDATE %I_qgrids SET "utm_10" = st_transform(foo.geom,4326) FROM ( 
        SELECT geom 
        FROM shared."utm_10x10"
        WHERE st_within(%L::geometry,st_transform(geom,4326))
    ) as foo WHERE row_id=%L',TG_TABLE_NAME,NEW.obm_geometry,NEW.obm_id);

    EXECUTE format('UPDATE %I_qgrids SET "utm_100" = st_transform(foo.geom,4326) FROM ( 
        SELECT geom 
        FROM shared."utm_100x100"
        WHERE st_within(%L::geometry,st_transform(geom,4326))
    ) as foo WHERE row_id=%L',TG_TABLE_NAME,NEW.obm_geometry,NEW.obm_id);

RETURN NEW;
END IF;

IF tg_op = 'UPDATE' THEN

    EXECUTE format('UPDATE %I_qgrids SET "original"=%L::geometry WHERE row_id=%L', TG_TABLE_NAME,NEW.obm_geometry,NEW.obm_id);

    EXECUTE format('UPDATE %I_qgrids SET "kef_5" = foo.geom FROM ( 
        SELECT obm_geometry AS geom
        FROM shared."kef_5x5"
        WHERE st_within(%L::geometry,obm_geometry)
    ) as foo WHERE row_id=%L',TG_TABLE_NAME,NEW.obm_geometry,NEW.obm_id);

    EXECUTE format('UPDATE %I_qgrids SET "kef_10" = st_transform(foo.geom,4326) FROM ( 
        SELECT geom
        FROM shared."kef_10x10"
        WHERE st_within(%L::geometry,st_transform(geom,4326))
    ) as foo WHERE row_id=%L',TG_TABLE_NAME,NEW.obm_geometry,NEW.obm_id);

    EXECUTE format('UPDATE %I_qgrids SET "utm_2.5" = st_transform(foo.geom,4326) FROM ( 
        SELECT geometry as geom
        FROM shared."utm_2.5x2.5"
        WHERE st_within(%L::geometry,st_transform(geometry,4326))
    ) as foo WHERE row_id=%L',TG_TABLE_NAME,NEW.obm_geometry,NEW.obm_id);

    EXECUTE format('UPDATE %I_qgrids SET "utm_10" = st_transform(foo.geom,4326) FROM ( 
        SELECT geom 
        FROM shared."utm_10x10"
        WHERE st_within(%L::geometry,st_transform(geom,4326))
    ) as foo WHERE row_id=%L',TG_TABLE_NAME,NEW.obm_geometry,NEW.obm_id);

    EXECUTE format('UPDATE %I_qgrids SET "utm_100" = st_transform(foo.geom,4326) FROM ( 
        SELECT geom 
        FROM shared."utm_100x100"
        WHERE st_within(%L::geometry,st_transform(geom,4326))
    ) as foo WHERE row_id=%L',TG_TABLE_NAME,NEW.obm_geometry,NEW.obm_id);

RETURN NEW;
END IF;

IF tg_op = 'DELETE' THEN
    EXECUTE format('DELETE FROM %I_qgrids WHERE row_id=%L',TG_TABLE_NAME,OLD.obm_id);
RETURN OLD;
END IF;

END;
```
