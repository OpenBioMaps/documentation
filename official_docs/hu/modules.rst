Modulok
*******

specieslist
    specieslist summary above results

summary
    results summary

results_table

results_asList
    Create foldable slides like results
    Called in results_builder()

results_asGPX
    Results as gpx

results_asCSV
    Results as csv

nuttons
    save and other button above results

photo_div
    photo or file uploader toggle div

box_load_selection
    Map Filter Functions
    These functions returns with a html table which displayed beside the map window
    These are optional boxes. Setting are in the biomaps db projects' table.
    
    Load prevously saved spatial queries' polygons

box_load_coord
    Show given coordinates position on the map

box_load_last_data
    Query last data

box_custom
    Custom box - only user defined version exists

text_filter
    Taxon and other text filters
    create boxes
    assemble WHERE part of query string

transform_data
    Transform data
    In result list it can transform data as need
    E.g. geometry to wkt

results_stable
    compact results table Stable

allowed_columns
    columns visible for users in different access level

bold_yellow
    vastag betűvel sárgán írt oszlop nevek az eredmény listákban
    
    Általános leírás:
    
    Paraméterek:
      oszlop nevek

extra_form_input_parameters

additional_columns
    additional columns
    use it together with the join_tables module
    return with an array:
    co [0] columns array
    c  [1] column name assoc array

join_tables
    join table to use additional columns
    use it together with the additional_columns module
    RETURN: join command and column list and visible names list
    [0] column name , separated list
    [1] prefixed column names array: all column which defined in the database columns
    [2] visible names array of array by JOIN

snap_to_grid
    project specified sanp to grid points on the map
    not recommended to use!
    
    Általános leírás:
    
    Paraméterek:

restricted_data
    Rule based data restriction

form_list

identify_point
    A térképi lapon megjelenő adat információ lekérdező eszköz
    
    Általános leírás:
        A modul engedélyezésével egy "i" ikon jelenik meg a térkép alatt funkciók mezőben. Ezzel az eszközzel egy adat pontra kattintava egy buborék ablakot jelenik meg a klikkelés közelében lévő adatokkal.
    
    Paraméterek:
        oszlop nevek amelyeket meg kívánunk jeleníteni az infó ablakban

custom_notify

custom_data_check
    Custom data checks of upload data

custom_filetype
    Custom file preparation. E.g. observado style CSV

create_pg_user
    Behatárolt hozzáférésű POSTGRES felhasználó létrehozása
    
    Általános leírás:
        A modul engedélyezésével (akik kapnak jogot a modul használatára) a felhazsnálók tudnak maguknak saját postgres felhazsnálót készíteni. 
        Ez a felhasználó csak olvasni tud az adatbázisból, módosítani, törölni nem. 
        Minden a projekthez rendelt adattáblát tud olvasni.
        Egyszerre csak egy kliens programból tud az adatbázishoz kapcsolódni.
        Egy év után automatikusan lejár a hozzáférése.
        Bármikor megújíthatja a hozzáférését a felhasználó.
    
    Paraméterek:
