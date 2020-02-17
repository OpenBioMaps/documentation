Modulok
*******

Általános modul kezelés:  
========================

A modul oldalon lehet bekapcsolni azokat a plusz funkciókat, amik nincsenek automatikusan hozzárendelve az OpenBioMaps alap keretrendszeréhez.

Modul hozzáadása a saját listánkhoz:
------------------------------------
A modul oldal felkínál nekünk előre behozott modulokat ezekről dönthetünk, hogy bekapcsoljuk vagy töröljük őket a saját listánkból, lásd lentebb. Ezenfelül a saját listánkhoz hozzáadhatunk további modulokat is, ehhez a modul lap aljára kell görgetni. A világos kék sáv első cellájában duplán kattintva felugrik egy legördülő lista a jelneleg aktív modulokkal. Rákattintunk a nekünk szükséges modul nevére, majd a *"hozzáad"* gombra kattintva már hozzá is adtuk a modult a saját listánkhoz.

Modul hozzáférés beállítások:
-----------------------------
Az egyes modulokat akár többször is hozzáadhatjuk a listánkhoz. Ez lehetővé teszi számunkra, hogy az egyes modulokhoz többféle hozzáférést adjunk meg. Ez azoknál a moduloknál lényeges, ahol az egyes felhasználóknak, vagy csoportoknak (ide kell egy link a csoport létrehozás eléréséhez) különböző hozzáférést szeretnénk adni, például: allowed_columns modul. Egy másik példa, hogy ha több adattáblánk van, akkor minden táblára külön megadhatjuk, hogy a lekérdezésnél melyik oszlopok értékei alapján tudjunk szűrni, például: text_filter modul.  
A **"Hozzáférés"** oszlopban kiválaszthatjuk, hogy publikusak-e a beállításaink *(everybody)*, vagy csak az adatbázisunkba bejelentkezett felhasználók *(logined users)* használhatják az adott opciót. A **"Csoport hozzáférés"** oszlopban tovább finomíthatjuk a hozzáférési opciókat, azáltal hogy kiválasztjuk az előre definiált csoportjainkat, vagy akár egyes személyeket is hozzárendelhetünk az adott beállításhoz.

Modul törlés a saját listánkból:
--------------------------------
A nem használt modulokat ki tudjuk törölni a saját listánkból úgy, hogy a **"Module name"** oszlopban kitöröljük az adatbázis nevét és rákattintunk a **"Műveletek"** oszlopban található *"módosít"* gombra.

Modul ki/be kapcsolás:
----------------------
Miután kialakítottuk a saját modul listánkat, az egyes modulokat ki és be tudjuk kapcsolni. Ezt úgy lehet megtenni, hogy az **"Engedélyezett"** fejlécű oszlopban választunk az *"igen"* vagy *"nem"* opcióból. 

Modulok személyre szabása:
--------------------------
A **"Function"** oszlopban kiválaszthatjuk, hogy a modul gyári beállításait szeretnénk használni *"default"* opció választásával, vagy ha egyéni beállításokat szeretnénk használni választhatjuk a *"private"* opciót is. Az utóbbi esetben lehetőség van az egyes modulok forráskódjának a letöltésére, amit az adatbázisunk igényei szerint kiegészíthetünk még további funkciókkal. A modul forráskódját a **"Modul cseréje"** oszlopból tudjuk letölteni az *"export"* gombra kattintva. A módosított modult *"Fájl kiválasztása"* opción keresztül tudjuk visszatölteni és aktiválni az adatbázisunkhoz.

Modulok paraméterezése:
-----------------------
Be tudjuk állítani, hogy a különböző modulok milyen feltételek mellett működjenek, vagy akár azt is, hogy melyik oszlopokra legyen érvényes. Ezt a **"Parameters"** oszlopon keresztül tudjuk megtenni. A modulok paraméterezését modulonkra lebontva megtalálhatod alább a *"Modul leírások"* részben.


Modul leírások:
===============

additional_columns
------------------
Általános leírás:
	* Ha egy adatbázis több adattáblából áll azokat különböző változókkal össze lehet kötni.
	* Lekérdezésnél az egy azonosítóhoz tartozó össze adatot lekérdezésnél. Ezt a funkciót a térképes oldalon az *"ignore table JOINS"* beikszelésével figyelmen kívül lehet hagyni.

akkor legkérdezésnél az összes adattáblából lekérdezi az egy azonosítóhoz kapcsolódó adatot. 
Paraméterezés:
	* Egymás alá írt oszlop nevek, felsorolás jel és vessző nélkül. Pl.:	faj
										megfigyelő
										dátum
Függvények: return_columns()
Hívások:

allowed_columns
---------------
Általános leírás: 
	* Itt lehet beállítani, hogy melyik oszlop legyen látható a különböző hozzáférési szinteken. 
	* Akkor lehet használni ha az adattáblához van *"rules"* tábla is rendelve.
Paraméterezés:
	* for_sensitive_data: vesszővel elválasztott felsorolása azoknak az oszlopoknak, amiket láthatóvá szeretnénk tenni. Nem mutatja az adathoz tartozó geometriát.
	* for_no-geom_data: vesszővel elválasztott felsorolása azoknak az oszlopoknak, amiket láthatóvá szeretnénk tenni
	* for_general: vesszővel elválasztott felsorolása azoknak az oszlopoknak, amiket láthatóvá szeretnénk tenni

Függvények:
	* return_columns() 
	* return_gcolumns()
Hívások:

bold_yellow
-----------
Általános leírás: 
	* Vastag betűvel sárgán írt oszlop nevek az eredmény listákban. Lekérdezés után a *"Kinyitható lista"* táblához csatolt részletes leírásban vastag betűvel, sárgán írt oszlop nevek jelennek meg.
	* Ezzel a modullal határozható meg az is, hogy az aplikációban a **"Felvett adatok"** menüpontban az adatfelvétel összefoglaló címkéin, milyen adatok jelenjenek meg.
Paraméterezés:
	* Egymás alá írt oszlop nevek, felsorolás jel és vessző nélkül. Pl.:	faj
										megfigyelő
										dátum
Függvények:
Hívások:

box_load_selection
------------------
Általános leírás:
	* Lehetővé teszi saját előre definiált koordináták feltöltését a profil oldalon megtalálható **"Megosztott geometriák"** ablakon keresztül. Ezek a koordináták lehetnek pontok, poligonok vagy akár raszterek is.
	* Az előre definiált koordinátáinkat a modul oldalon keresztül tudjuk hozzáadni az adatbázisunkhoz, úgy hogy ráklikkelünk a zöld háttérrel rendelkező fogaskerékre. A megjelenő oldalon nem csak a saját, hanem a mások által definiált "publikusnak" nyilvánított koordináták is megjelennek. Megkeressük a számunkra szükséges koordinátákat, majd a koordináta mellett található áthúzott szemekre kattintva be tudjuk állítani, hogy az adott koordináta látható legyen-e az adatbázisban. Továbbá eldönthetjük, hogy ezeket a koordinátákat egyes személyekhez, csoportokhoz rendeljük.
	* Bekapcsolása után a **Térkép** oldalon megjelenik a **"Térbeli lekérdezés"** ablak. Itt egy legördülő listában láthatóak az előre definiált koordinátáink, amelyek alapján lekérdezhetjük az adatainkat. Raszterek esetén beállítható, hogy csak azokat az adatokat kérdezze le, amik a raszteren belül találhatóak vagy azokat is, amelyek a raszterek élei alá esnek.
	* A webes és fájl feltöltés esetén, ha az *"obm_geometry"* oszlop típust használjuk koordináta felvételre, akkor a megjelenő az oszlop legördülő menüjére kattintva megjelenik egy kis ablak, amin keresztül lehetővé válik a térképről történő koordináta felvétel. Ezen a kis ablakon belül található a *"geometria listából"* opció, aminek a legördülő menüjében megtalálhatóak az előre deifiniált koordinátáink. Emellett lehetőségünk van közvetlenül a térképről felvenni koordinátákat a *"koordináták térképről"* menüpontra kattintva.
	* *"koordináták térképről"*  menüpont: erre az opcióra kattintva megjelenik egy térkép amiről felvhetjük a koordinátáinkat. A térkép jobb alsó sarkában található ceruza ikonra kattintva egy pontot jelölhetünk ki, míg a négyzet ikonra kattinta poligonként, akár egy nagyobb területet is körbe jelölhetünk.
Paraméterezés:
	* Beállíthatjuk, hogyan szeretnénk az adatokat lekérdezni, ha ezt nem paraméterezzük akkor az összes mód elérhető.
		* contains -
		* intersects -
		* crosses -
		* disjoint -
Függvények:
Hívások:

box_load_coord
--------------
Általános leírás:
	* A térképes oldalon feltűnik a *"pozició"* blokk a térkép alatt. Ha a kurzort mozgatjuk a térképen, akkor láthatjuk hogy a *"pozició"* blokkban a koordináta folyamatosan változik, mintegy lekövetve a kurzorunk helyzetét a térképen.
Paraméterezés:
	* Különböző koordináta rendszerek vetületeit adhatjuk itt meg, pl.:
				* wgs84:4326
				* eov=23700
Függvények:
Hívások: print_box, limits, ajax, print_js

box_load_last_data
------------------
Általános leírás:
	* Létrehozza a **Gyors lekérdezések** opciót a térképes oldalon a térkép jobb oldalán. Három lehetőség közül lehet választani: utolsó saját feltöltés, legutolsó feltöltés (bárkié) vagy az utolsó feltöltött sorok.
	* A modul oldalon be lehet állítani, hogy mennyi lehet az így lekérdezett sorok száma.
Paraméterezés:
	* Egy számot adunk meg, pl.: 10
Függvények:
Hívások:

box_custom
----------
Általános leírás:
Paraméterezés:
Függvények:
Hívások:
    Custom box - only user defined version exists.

    Calls:

    General description: The custom module has to be in includes/modules/private/ folder (You have to create private folder, if it's not there. It is recomended to add read-only permissions for www-data user to avoid the deletion or modification of the custom module in the course of a system upgrade.

    Parameters: a file's basename in includes/modules/private folder. E.g. hrsz_query

    Where hrsz_query_Class is a class in hrsz_query.php in includes/modules/private/ folder.

    This Class should include at least print_box() and print_js() functions.

    Custom box - only user defined version exists
    Egyénileg létrehozott modulok betöltését teszi lehetővé.
    Hívások:
    
    Általános leírás: Az egyénileg létrehozott modult a projekt könyvtárban az includes/modules/private mappában kell elhelyezni. Amennyiben szükséges, létre kell hozni a könyvtárat. A könyvtár jogosultságait célszerű úgy beállítani, hogy a www-data felhasználónak ne legyen írási jogosultsága. Ezzel elkerülhető, hogy az egyénileg létrehozott moduljaink felülíródjanak egy frissítés során.
    
    Paraméterek: A modul(ok) fájlneve kiterjesztés nélkül. Több custom modul esetén a modulneveket sortöréssel kell elválasztani.
    Pl. hrsz_query, ahol a hrsz_query_Class egy osztály a hrsz_query.php fájlban. Az osztályt legalább a print_box () és a print_js () funkcióknak tartalmazniuk kell.


photos
------
Általános leírás:
Paraméterezés:
Függvények:
Hívások:
    Photo or other attachment box.

    Calls:

    General description:

    Parameters:

read_table
----------
Általános leírás:
Paraméterezés:
Függvények:
Hívások:
    Present a table or an sql view as a rollable html table. This table is available with a unique link.

    Calls:

    General description:
        Add these lines to .htaccess file where  .... should replaced with your project table name
        # read table module
        RewriteRule ^view-table/(.*)/$ /projects/..../includes/modules/results_asTable.php?view&table=$1&%{QUERY_STRING} [NC,L]

    Parameters: schema.table
        or
        schema.table:default-order-column

results_summary
---------------
Általános leírás:
Paraméterezés:
Függvények:
Hívások:
    Summary of results.

results_table
-------------
Általános leírás:
Paraméterezés:
Függvények:
Hívások:
    create a full html table of the results
    
    Hívások:
    
    Általános leírás:
        Nincs használva, mert nagy adatmennyiségeknél nagyon megterhelő a böngészőnek. Pár száz sor adat az még ok.
        Tovább lehet persze fejleszteni lapozós lekérdezőssé, vagy valami eleve kisebb táblázatok megjelenítéséhez.
    
    Paraméterek:

    Create a full html table of the results.

    Calls:

    General description:
        Not used!!

    Parameters:

results_asList
--------------
Általános leírás:
Paraméterezés:
Függvények:
Hívások:
    Create foldable slides like results.

    Calls: results_builder()

    General description:

    Parameters:

results_asGPX
-------------
Általános leírás:
Paraméterezés:
Függvények:
Hívások:
    Save results as a GPX file.

    Calls:

    General description:

    Parameters:

results_asCSV
-------------
Általános leírás:
Paraméterezés:
Függvények:
Hívások:
    Save results as a csv file.

    Hívások:

    Általános leírás:

    Paraméterek:

results_asJSON
--------------
Általános leírás:
Paraméterezés:
Függvények:
Hívások:
    Save results as a JSON file.

    Calls:

    General description:

    Parameters:

results_asSHP
-------------
Általános leírás:
Paraméterezés:
Függvények:
Hívások:
    Save results as a shp file.

    Calls:

    General description:

    Parameters:

results_buttons
---------------
Általános leírás:
Paraméterezés:
Függvények:
Hívások:
    Save and other button above results section, under map.

    Calls:

    General description:

    Parameters:

results_asStable
----------------
Általános leírás:
Paraméterezés:
Függvények:
Hívások:
    Compact results table Stable.

    Calls:

    General description:

    Parameters:

results_specieslist
-----------
Általános leírás:
Paraméterezés:
Függvények:
Hívások:
    Specieslist summary above results.

    Calls:

    General description:

    Parameters:

text_filter
-----------
Általános leírás:
Paraméterezés:
Függvények:
Hívások:
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
Általános leírás:
Paraméterezés:
Függvények:
Hívások:
    Advanced taxon and other text filters.

    Calls:

    General description:
        create boxes
        assemble WHERE part of query string

    Parameters: example:


transform_data
--------------
Általános leírás:
Paraméterezés:
Függvények:
Hívások:
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
Általános leírás:
Paraméterezés:
Függvények:
Hívások:
    Extra input paramaters for forms.

    Calls:

    General description:

    Parameters:

box_load_selection
-----------
Általános leírás:
Paraméterezés:
Függvények:
Hívások:

If this module is enabled "Manage custom geometries" option will appear on your profile page.

It is possible to upload or draw custom geometries for further action. These action can be make spatial queries or assign geometry to uploaded data.

You can manage the custom geometries in the profile page by following two links: shared geometries and own geometries.

Following the own geometries link you can delete or share, rename and modify the view options of your geometries. The view options are the following: View in spatial selection list and View in upload data - assign named spatial forms list.

Following the shared geometries link you can rename the geometries and modify the view options. You cannot delete the shared geometries!

restricted_data
---------------
Általános leírás:
Paraméterezés:
Függvények:
Hívások:
    Rule based data restriction

    alls

    Functions: rule_data()

    General description:

    Parameters:


identify_point
--------------
Általános leírás:
Paraméterezés:
Függvények:
Hívások:
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
Általános leírás:
Paraméterezés:
Függvények:
Hívások:
    Creates custom postgres based notify events.

    Calls:

    Functions: listen(), unlisten(), notify(), email()

    General description:

    Parameters:

custom_data_check
-----------------
Általános leírás:
Paraméterezés:
Függvények:
Hívások:
    Custom data checks of upload data.

    Calls:

    Functions: list(), check()

    General description:

    Parameters:

custom_filetype
---------------
Általános leírás:
Paraméterezés:
Függvények:
Hívások:
    Custom file preparation. E.g. observado style CSV

    Calls:

    Functions: option_list(), custom_read()

    General description:

    Parameters:

create_pg_user
--------------
Általános leírás:
Paraméterezés:
Függvények:
Hívások:
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

grid_view
---------
Általános leírás:
Paraméterezés:
Függvények:
Hívások:
    View data on selected polygon grid

    Calls:

    Functions: print_box(), default_grid_geom(), get_grid_layer()

    General description:

    Parameters: layer_options

    Parameters example: layer_options:kef_5 (dinpi_grid), utm_2.5 (dinpi_grid), utm_10 (dinpi_grid), utm_100 (dinpi_grid), original (dinpi_points,dinpi_grid),etrs(dinpi_grid)

    Example trigger function:

    Trigger on nnn_qgrids:
```sql    
    CREATE TRIGGER self_update BEFORE INSERT OR UPDATE ON dinpi_qgrids FOR EACH ROW EXECUTE PROCEDURE update_qgrids_geometries()
```
    Trigger on nnn table:
```sql
    CREATE TRIGGER update_qgrids AFTER INSERT OR DELETE OR UPDATE ON dinpi FOR EACH ROW EXECUTE PROCEDURE grid_geometries()
```
Function grid_geometries()
```sql
BEGIN
IF tg_op = 'INSERT' THEN

    EXECUTE format('INSERT INTO %I_qgrids (row_id,original) SELECT %L,%L::geometry',TG_TABLE_NAME,NEW.obm_id,NEW.obm_geometry);

RETURN NEW;
END IF;

IF tg_op = 'UPDATE' THEN
    -- create original at first
    --EXECUTE format('INSERT INTO %I_qgrids (row_id,original) SELECT %L,%L::geometry',TG_TABLE_NAME,NEW.obm_id,NEW.obm_geometry);
    EXECUTE format('UPDATE %I_qgrids SET "original"=%L::geometry WHERE row_id=%L', TG_TABLE_NAME,NEW.obm_geometry,NEW.obm_id);

RETURN NEW;
END IF;

IF tg_op = 'DELETE' THEN

    EXECUTE format('DELETE FROM %I_qgrids WHERE row_id=%L',TG_TABLE_NAME,OLD.obm_id);

RETURN OLD;
END IF;

END;
```

Function update_qgrids_geometries()
```sql
BEGIN
-- Available shared grids tables: kef_5, kef_10, utm_2.5, utm_10, etrs
-- Required output grids e.g.: kef_10x10, utm_10x10, etrs, snap

    EXECUTE FORMAT('SELECT st_transform(geometry,4326) FROM shared."kef_5x5"     WHERE st_within(st_setsrid(%L::geometry,4326),st_transform(geometry,4326))',NEW.original) INTO NEW."kef_5";
    EXECUTE FORMAT('SELECT st_transform(geometry,4326) FROM shared."kef_10x10"   WHERE st_within(st_setsrid(%L::geometry,4326),st_transform(geometry,4326))',NEW.original) INTO NEW."kef_10";
    EXECUTE FORMAT('SELECT st_transform(geometry,4326) FROM shared."utm_2.5x2.5" WHERE st_within(st_setsrid(%L::geometry,4326),st_transform(geometry,4326))',NEW.original) INTO NEW."utm_2.5";
    EXECUTE FORMAT('SELECT st_transform(geometry,4326) FROM shared."utm_10x10"   WHERE st_within(st_setsrid(%L::geometry,4326),st_transform(geometry,4326))',NEW.original) INTO NEW."utm_10";
    EXECUTE FORMAT('SELECT st_transform(geometry,4326) FROM shared."utm_100x100" WHERE st_within(st_setsrid(%L::geometry,4326),st_transform(geometry,4326))',NEW.original) INTO NEW."utm_100";
    EXECUTE FORMAT('SELECT st_transform(geometry,4326) FROM shared."etrs"        WHERE st_within(st_setsrid(%L::geometry,4326),st_transform(geometry,4326))',NEW.original) INTO NEW."etrs";
    EXECUTE FORMAT('SELECT st_SnapToGrid(%L::geometry,0.13,0.09)',NEW.original) INTO NEW."snap";

    RETURN NEW;

END;
```

massive_edit
------------
Általános leírás:
Paraméterezés:
Függvények:
Hívások:
   Allows you to edit the selected data massively on the file upload interface

   Calls:

   Functions:

   General description:

   Parameters:

download_restricted
-------------------
Általános leírás:
Paraméterezés:
Függvények:
Hívások:
   Admin-controlled download authorization

   Calls:

   Functions:

   General description:

   Parameters:

list_manager
------------
Általános leírás:
Paraméterezés:
Függvények:
Hívások:
   Calls:

   Functions:

   General description:

   Parameters:

move_project
------------
Általános leírás:
Paraméterezés:
Függvények:
Hívások:
   Calls:

   Functions:

   General description:

   Parameters:
