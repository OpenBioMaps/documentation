Modulok
*******

specieslist
    specieslist summary above results

summary
    results summary

results_table
    create a full html table of the results
    
    Hívások:
    
    Általános leírás:
        Nincs használva, mert nagy adatmennyiségeknél nagyon megterhelő a böngészőnek. Pár száz sor adat az még ok.
        Tovább lehet persze fejleszteni lapozós lekérdezőssé, vagy valami eleve kisebb táblázatok megjelenítéséhez.
    
    Paraméterek:

results_asList
    Create foldable slides like results
    Hívások: results_builder()
    
    Általános leírás:
    
    Paraméterek:

results_asGPX
    Eredmények GPX formátumba
    
    Hívások:
    
    Általános leírás:
    
    Paraméterek:
    
results_asCSV
    Results as csv
    
    Hívások:
    
    Általános leírás:
    
    Paraméterek:

results_asJSON
    Results as JSON
    
    Hívások:
    
    Általános leírás:
    
    Paraméterek:

results_asSHP
    Results as csv
    
    Hívások:
    
    Általános leírás:
    
    Paraméterek:
    
nuttons
    save and other button above results section - under map
    
    Hívások:
    
    Általános leírás:
    
    Paraméterek:

photo_div
    photo or file uploader toggle div
    
    Hívások:
    
    Általános leírás:
    
    Paraméterek:
    
box_load_selection
    Map Filter Functions
    These functions returns with a html table which displayed beside the map window
    These are optional boxes. Setting are in the biomaps db projects' table.
    
    Load prevously saved spatial queries' polygons
    
    Hívások:
    
    Általános leírás:
    
    Paraméterek:
    
box_load_coord
    Show given coordinates position on the map
    
    Hívások: print_box, limits, ajax, print_js
    
    Általános leírás:
    
    Paraméterek:
    
box_load_last_data
    Query last data
    
    Hívások:
    
    Általános leírás:
    
    Paraméterek:
    
box_custom
    Custom box - only user defined version exists
    Egyénileg létrehozott modulok betöltését teszi lehetővé.
    Hívások:
    
    Általános leírás: Az egyénileg létrehozott modult a projekt könyvtárban az includes/modules/private mappában kell elhelyezni. Amennyiben szükséges, létre kell hozni a könyvtárat. A könyvtár jogosultságait célszerű úgy beállítani, hogy a www-data felhasználónak ne legyen írási jogosultsága. Ezzel elkerülhető, hogy az egyénileg létrehozott moduljaink felülíródjanak egy frissítés során.
    
    Paraméterek: A modul osztályneve.
    
text_filter
    Taxon and other text filters
    create boxes
    assemble WHERE part of query string
    
    Hívások:
    
    Általános leírás:
    
    Paraméterek:
    
transform_data
    Transform data
    In result list it can transform data as need
    E.g. geometry to wkt
    
    Hívások:
    
    Általános leírás:
    
    Paraméterek:
    
results_stable
    compact results table Stable
    
    Hívások:
    
    Általános leírás:
    
    Paraméterek:
    
allowed_columns
    columns visible for users in different access level
    
    Hívások:
    
    Általános leírás:
    
    Paraméterek:
    
bold_yellow
    vastag betűvel sárgán írt oszlop nevek az eredmény listákban
    
    Hívások:
    
    Általános leírás:
    
    Paraméterek:
      oszlop nevek

extra_form_input_parameters
    
    Hívások:
    
    Általános leírás:
    
    Paraméterek:
    
additional_columns
    additional columns
    use it together with the join_tables module
    return with an array:
    co [0] columns array
    c  [1] column name assoc array
    
    Hívások:
    
    Függvények: return_columns()
    
    Általános leírás:
    
    Paraméterek:
    
join_tables
    join table to use additional columns
    use it together with the additional_columns module
    RETURN: join command and column list and visible names list
    [0] column name , separated list
    [1] prefixed column names array: all column which defined in the database columns
    [2] visible names array of array by JOIN
    
    Hívások:
    
    Függvények: return_joins()
    
    Általános leírás:
    
    Paraméterek:

snap_to_grid
    project specified sanp to grid points on the map
    not recommended to use!
    
    Hívások:
    
    Függvények: geom_column(), geom_column_join(), rules_join()
    
    Általános leírás:
    
    Paraméterek:
    

restricted_data
    Rule based data restriction
    
    Hívások:
    
    Függvények: rule_data()
    
    Általános leírás:
    
    Paraméterek:
    
form_list
    
    Hívások:
    
    Függvények: form_list()
    
    Általános leírás:
    
    Paraméterek:
    
identify_point
    A térképi lapon megjelenő adat információ lekérdező eszköz
    
    Hívások:
    
    Függvények: return_data(), print_button()
    
    Általános leírás:
        A modul engedélyezésével egy "i" ikon jelenik meg a térkép alatt funkciók mezőben. Ezzel az eszközzel egy adat pontra kattintava egy buborék ablakot jelenik meg a klikkelés közelében lévő adatokkal.
    
    Paraméterek:
        oszlop nevek amelyeket meg kívánunk jeleníteni az infó ablakban
        
        json objektum: hiperlink megjelenítésére alkalmas. 
       
            elemei:
                
                type - kötelező, egyelőre csak a "link" érték működik
                
                href - kötelező - hivatkozás címe
                
                label - kötelező - a link/gomb szövege/cimkéje - többnyelvűséget támogatja
                
                class - opcionális - a linkhez rendelt osztályok
                
                id - opcionális - a linkhez rendelt azonosító
                
                target - opcionális - alapértelmezett "_blank"
                
                params - opcionális - a href elem paraméterei 

            A href elemet a modul-paraméterek közt felsorolt oszlopok értékeivel paraméterezhetjük. lásd a példát:

            Példa:
            { "type": "link", "href": "//example.com?nest_id=%1%&species=%2%", "label": "str_add_data", "class": "pure-button button-href", "params": ["obm_id","species"] }

            A fenti példa a következő hiperlinket fogja generálni:

            <a href="//example.com?nest_id=2898&species=Brachyramphus perdix" target="_blank" id="" class="pure-button button-href">Adat hozzáadása</a>

            A json-t egy sorosra kell tömöríteni!

custom_notify
    
    Hívások:
    
    Függvények: listen(), unlisten(), notify(), email()
    
    Általános leírás:
    
    Paraméterek:
  
custom_data_check
    Custom data checks of upload data
    
    Hívások:
    
    Függvények: list(), check()
    
    Általános leírás:
    
    Paraméterek:
  
custom_filetype
    Custom file preparation. E.g. observado style CSV
    
    Hívások:
    
    Függvények: option_list(), custom_read()
    
    Általános leírás:
    
    Paraméterek:
  
create_pg_user
    Behatárolt hozzáférésű POSTGRES felhasználó létrehozása
    
    Hívások:
    
    Függvények: create_pg_user(), show_button()
        
    Általános leírás:
        A modul engedélyezésével (akik kapnak jogot a modul használatára) a felhazsnálók tudnak maguknak saját postgres felhazsnálót készíteni. 
        Ez a felhasználó csak olvasni tud az adatbázisból, módosítani, törölni nem. 
        Minden a projekthez rendelt adattáblát tud olvasni.
        Egyszerre csak egy kliens programból tud az adatbázishoz kapcsolódni.
        Egy év után automatikusan lejár a hozzáférése.
        Bármikor megújíthatja a hozzáférését a felhasználó.
    
    Paraméterek:

custom_admin_pages:
    ...
    
    Hívások:
    
    Függvények: nincsenek föggvények.
    
    Általános leírás:
    
    Paraméterek:
    
grid_view:
    Custom file preparation. E.g. observado style CSV
    
    Hívások: 
    
    Függvények: print_box()
    
    Általános leírás:
    
    Paraméterek:
