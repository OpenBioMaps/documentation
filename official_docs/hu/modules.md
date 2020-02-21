Általános modul kezelés:  
========================

A modul oldalon lehet bekapcsolni azokat a plusz funkciókat, amik nincsenek automatikusan hozzárendelve az OpenBioMaps alap keretrendszeréhez.

Modul hozzáadása a saját listánkhoz
-----------------------------------
A modul oldal felkínál nekünk előre behozott modulokat ezekről dönthetünk, hogy bekapcsoljuk vagy töröljük őket a saját listánkból, lásd lentebb. Ezenfelül a saját listánkhoz hozzáadhatunk további modulokat is, ehhez a modul lap aljára kell görgetni. A világos kék sáv első cellájában duplán kattintva felugrik egy legördülő lista a jelenleg aktív modulokkal. Rákattintunk a nekünk szükséges modul nevére, majd a *"hozzáad"* gombra kattintva már hozzá is adtuk a modult a saját listánkhoz.

Modul hozzáférés beállítások
----------------------------
Az egyes modulokat akár többször is hozzáadhatjuk a listánkhoz. Ez lehetővé teszi számunkra, hogy az egyes modulokhoz többféle hozzáférést adjunk meg. Ez azoknál a moduloknál lényeges, ahol az egyes felhasználóknak, vagy csoportoknak különböző hozzáférést szeretnénk adni, például: allowed_columns modul. Egy másik példa, hogy ha több adattáblánk van, akkor minden táblára külön megadhatjuk, hogy a lekérdezésnél melyik oszlopok értékei alapján tudjunk szűrni, például: text_filter modul.  
A **Hozzáférés** oszlopban kiválaszthatjuk, hogy publikusak-e a beállításaink *(everybody)*, vagy csak az adatbázisunkba bejelentkezett felhasználók *(logined users)* használhatják az adott opciót. A **Csoport hozzáférés** oszlopban tovább finomíthatjuk a hozzáférési opciókat, azáltal hogy kiválasztjuk az előre definiált csoportjainkat, vagy akár egyes személyeket is hozzárendelhetünk az adott beállításhoz.

Modul törlés a saját listánkból
-------------------------------
A nem használt modulokat ki tudjuk törölni a saját listánkból úgy, hogy az **Engedélyezett** oszlopot *"nem"*-re állítjuk és a **Module name** oszlopban kitöröljük az adatbázis nevét, majd rákattintunk a **Műveletek** oszlopban található *"módosít"* gombra.

Modul ki/be kapcsolás
---------------------
Miután kialakítottuk a saját modul listánkat, az egyes modulokat ki és be tudjuk kapcsolni. Ezt úgy lehet megtenni, hogy az **Engedélyezett** fejlécű oszlopban választunk az *"igen"* vagy *"nem"* opcióból. 

Modulok személyre szabása
-------------------------
A **Function** oszlopban kiválaszthatjuk, hogy a modul gyári beállításait szeretnénk használni *"default"* opció választásával, vagy ha egyéni beállításokat szeretnénk használni választhatjuk a *"private"* opciót is. Az utóbbi esetben lehetőség van az egyes modulok forráskódjának a letöltésére, amit az adatbázisunk igényei szerint kiegészíthetünk még további funkciókkal. A modul forráskódját a **Modul cseréje** oszlopból tudjuk letölteni az *"export"* gombra kattintva. A módosított modult *"Fájl kiválasztása"* opción keresztül tudjuk visszatölteni és aktiválni az adatbázisunkhoz.

Modulok paraméterezése
----------------------
Be tudjuk állítani, hogy a különböző modulok milyen feltételek mellett működjenek, vagy akár azt is, hogy melyik oszlopokra legyen érvényes. Ezt a **Parameters** oszlopon keresztül tudjuk megtenni. A modulok paraméterezését modulokra lebontva megtalálhatod alább a *"Modul leírások"* részben.


Modul leírások
==============

additional_columns
------------------
Általános leírás

* Ha egy adatbázis több adattáblából áll azokat különböző változókkal össze lehet kötni.
* Lekérdezésnél az egy azonosítóhoz tartozó összes adatot lekérdezi. Ezt a funkciót a térképes oldalon az *"ignore table JOINS"* beikszelésével figyelmen kívül lehet hagyni.
* Például bizonyos odú projektekben külön táblázatban kezeljük az adatokat a szülőkről és a fiókákról, ha az egy odúhoz tartozó össze adatot megszeretnénk kapni, akkor az *"odu_aszonosito"* oszlopot adjuk meg "összekötő" változónak.

Paraméterezés:

Egymás alá írt oszlop nevek, felsorolás jel és vessző nélkül. Például:

		faj
		megfigyelő
		dátum

Fejleszői dokumentáció

	Függvények: return_columns()

	Hívások:

allowed_columns
---------------
Általános leírás:

* Itt lehet beállítani, hogy melyik oszlop legyen látható a különböző hozzáférési szinteken. 
* Akkor lehet használni ha az adattáblához van *"rules"* tábla is rendelve és a projekt alap hozzáférési szintje nem publikus.

Paraméterezés:

	for_sensitive_data: 
		vesszővel elválasztott felsorolása azoknak az oszlopoknak, amiket láthatóvá szeretnénk tenni. Nem mutatja az adathoz tartozó geometriát.
	for_no-geom_data: 
		vesszővel elválasztott felsorolása azoknak az oszlopoknak, amiket láthatóvá szeretnénk tenni
	for_general: 
		vesszővel elválasztott felsorolása azoknak az oszlopoknak, amiket láthatóvá szeretnénk tenni

Fejleszői dokumentáció

	Függvények: return_columns(), return_gcolumns()

	Hívások:

bold_yellow
-----------
Általános leírás:

* Vastag betűvel sárgán írt oszlop nevek az eredmény listákban. Lekérdezés után a *"Kinyitható lista"* táblához csatolt részletes leírásban vastag betűvel, sárgán írt oszlop nevek jelennek meg.
* Ezzel a modullal határozható meg az is, hogy az applikációban a **"Felvett adatok"** menüpontban az adatfelvétel összefoglaló címkéin, milyen adatok jelenjenek meg.

Paraméterezés:
	
	Egymás alá írt oszlop nevek, felsorolás jel és vessző nélkül. Pl.:	
		faj
		megfigyelő
		dátum

Fejleszői dokumentáció

	Függvények:

	Hívások:

box_custom
----------
Általános leírás:

* Egyénileg létrehozott modulok betöltését teszi lehetővé.
* Az egyénileg létrehozott modult a projekt könyvtárban az *includes/modules/private* mappában kell elhelyezni. Amennyiben szükséges, létre kell hozni a könyvtárat. A könyvtár jogosultságait célszerű úgy beállítani, hogy a www-data felhasználónak ne legyen írási jogosultsága. Ezzel elkerülhető, hogy az egyénileg létrehozott moduljaink felülíródjanak egy frissítés során.

Paraméterezés:
A modul(ok) fájlneve kiterjesztés nélkül. Több custom modul esetén a modulneveket sortöréssel kell elválasztani.
Például *hrsz_query*, ahol a *hrsz_query_Class* egy osztály a *hrsz_query.php* fájlban ami a *includes/modules/private* mappába került.

	hrsz_query

Fejleszői dokumentáció

	Az osztálynak legalább a print_box () és a print_js () funkcióknak tartalmazniuk kell.
	
	Függvények:

	Hívások:

box_load_coord
--------------
Általános leírás:

* A térképes oldalon feltűnik a *"pozíció"* blokk a térkép alatt. Ha a kurzort mozgatjuk a térképen, akkor láthatjuk hogy a *"pozíció"* blokkban a koordináta folyamatosan változik, mintegy lekövetve a kurzorunk helyzetét a térképen.
* Szintén a *"pozíció"* blokkban, ha beírjuk a szélességi és hosszúsági fokokat, akkor a kis, fekete *"nyalókára"* kattintva a téképen megjelenik a pontunk.

Paraméterezés:
Különböző koordináta rendszerek vetületeit adhatjuk itt meg, pl.:

	wgs84:4326
	eov=23700

Fejleszői dokumentáció

	Függvények: print_box(), limits(), ajax(), print_js()

	Hívások: 

box_load_last_data
------------------
Általános leírás:

* Létrehozza a **Gyors lekérdezések** opciót a térképes oldalon a térkép jobb oldalán. Három lehetőség közül lehet választani:
	* utolsó saját feltöltés, 
	* legutolsó feltöltés (bárkié) 
	* utolsó feltöltött sorok.
* A modul oldalon be lehet állítani, hogy mennyi lehet az utolsó feltöltött sorok lekérdezett sor mennyisége. A másik két opció esetében mindig 1 sort ad vissza a modul.

Paraméterezés:
Egy számot adunk meg, pl.: 10

	10

Fejleszői dokumentáció

	Függvények:

	Hívások:

box_load_selection
------------------
Általános leírás:

* Lehetővé teszi saját előre definiált koordináták feltöltését a profil oldalon megtalálható **"Megosztott geometriák"** ablakon keresztül. Ezek a koordináták lehetnek pontok, poligonok vagy akár raszterek is.
* Az előre definiált koordinátáinkat a modul oldalon keresztül tudjuk hozzáadni az adatbázisunkhoz, úgy hogy rákattintunk a zöld háttérrel rendelkező fogaskerékre. A megjelenő oldalon nem csak a saját, hanem a mások által definiált "publikusnak" nyilvánított koordináták is megjelennek. Megkeressük a számunkra szükséges koordinátákat, majd a koordináta mellett található áthúzott szemekre kattintva be tudjuk állítani, hogy az adott koordináta látható legyen-e az adatbázisban. Továbbá eldönthetjük, hogy ezeket a koordinátákat egyes személyekhez vagy csoportokhoz rendeljük.
* Bekapcsolása után a **Térkép** oldalon megjelenik a **"Térbeli lekérdezés"** ablak. Itt egy legördülő listában láthatóak az előre definiált koordinátáink, amelyek alapján lekérdezhetjük az adatainkat. Raszterek esetén beállítható, hogy csak azokat az adatokat kérdezze le, amik a raszteren belül találhatóak vagy azokat is, amelyek a raszterek élei alá esnek.
* A webes és fájl feltöltés esetén, ha az *"obm_geometry"* oszlop típust használjuk koordináta felvételre, akkor a megjelenő az oszlop legördülő menüjére kattintva megjelenik egy kis ablak, amin keresztül lehetővé válik a térképről történő koordináta felvétel. Ezen a kis ablakon belül található a *"geometria listából"* opció, aminek a legördülő menüjében megtalálhatóak az előre definiált koordinátáink. Emellett lehetőségünk van közvetlenül a térképről felvenni koordinátákat a *"koordináták térképről"* menüpontra kattintva.
* *"koordináták térképről"*  menüpont: erre az opcióra kattintva megjelenik egy térkép amiről felvehetjük a koordinátáinkat. A térkép jobb alsó sarkában található ceruza ikonra kattintva egy pontot jelölhetünk ki, míg a négyzet ikonra kattintva poligonként, akár egy nagyobb területet is körbe jelölhetünk.

Paraméterezés:
Beállíthatjuk, hogyan szeretnénk az adatokat lekérdezni, ha ezt nem paraméterezzük akkor az összes mód elérhető.

	contains -
	intersects -
	crosses -
	disjoint -

Fejleszői dokumentáció

	Függvények:

	Hívások:

create_pg_user
--------------
Általános leírás:

* Engedélyezés után a profil oldalon megjelenik a **Postgres felhasználó készítése** opció.
* A modul engedélyezésével azok a felhasználók, akik kapnak jogot a modul használatára, tudnak maguknak saját postgres azonosítót készíteni.
* Behatárolt hozzáférésű POSTGRES felhasználó létrehozása: ez a felhasználó csak olvasni tud az adatbázisból, módosítani, törölni nem. 
	* Minden a projekthez rendelt adattáblát tud olvasni.
	* Egyszerre csak egy kliens programból tud az adatbázishoz kapcsolódni.
	* Egy év után automatikusan lejár a hozzáférése.
	* Bármikor megújíthatja a hozzáférését a felhasználó.

Paraméterezés:

Fejleszői dokumentáció
	
	Függvények: create_pg_user(), show_button()

	Hívások:

custom_admin_pages
------------------
Általános leírás:
	
Paraméterezés:

Fejleszői dokumentáció

	Függvények:

	Hívások:

custom_data_check
-----------------
Általános leírás:

* (Custom data checks of upload data.)?

Paraméterezés:

Fejleszői dokumentáció

	Függvények: list(), check()

	Hívások:

custom_filetype
---------------
Általános leírás:

* Adat fájlok átalakítása, más rendszerek formátumára pl.: observado típusú .CSV

Paraméterezés:

Fejleszői dokumentáció

	Függvények: option_list(), custom_read()

	Hívások:

custom_notify
-------------
Általános leírás:

* (Creates custom postgres based notify events.)???

Paraméterezés:

Fejleszői dokumentáció
	
	Függvények: listen(), unlisten(), notify(), email()

	Hívások:

download_restricted
-------------------
Általános leírás:

* A lekérdezett adatok letöltése az adatbázis adminok jóváhagyásával lehetséges.

Paraméterezés:

Fejleszői dokumentáció

	Függvények:

	Hívások:

ebp
---
Általános leírás:

* Automatikusan tölti fel speciális adatokat speciális felületekre pl: EBirds adatbázis

Paraméterezés:

Függvények:

Hívások:

extra_params
------------
Általános leírás:

* (Extra input paramaters for forms.)?

Paraméterezés:

Fejleszői dokumentáció
	
	Függvények:

	Hívások:

form_choose
-----------
Általános leírás:

Paraméterezés:

Fejleszői dokumentáció
	
	Függvények:

	Hívások:

grid_view
---------
Általános leírás:

* Előre definiált poligonok szerint is lehet adatot lekérdezni.
* SQL-ben kell beállítani a szükséges paramétereket

Paraméterezés:
	
	layer_options

Paraméterezésre példa: 
		layer_options:kef_5 (dinpi_grid), utm_2.5 (dinpi_grid), utm_10 (dinpi_grid), utm_100 (dinpi_grid), original (dinpi_points,dinpi_grid),etrs(dinpi_grid)

Példa trigger funkcióra:

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

Fejleszői dokumentáció
	
	Függvények: print_box(), default_grid_geom(), get_grid_layer()

	Hívások:

identify_point
--------------
Általános leírás:
* Egy vagy több pont azonosítása a térképen.
* Egy kis buborékban láthatóvá tesz az adott adat pontról néhány információt, amit előzőleg már beállítottunk.

Paraméterezés:
Egymás alá írt sorok, felsorolás jel és vessző nélkül pl.:

	faj
	dátum

Fejlesztői dokumentáció

	Függvények: return_data(), print_button()

	Hívások:

list_manager
------------
Általános leírás:
* Az adatbázis oszlopoknál bekapcsol egy plusz funkciót, ami meghatározza a listát. ?

Paraméterezés:

Fejleszői dokumentáció
	
	Függvények:

	Hívások:

massive_edit
------------
Általános leírás:

* Lehetővé teszi a már feltöltött adatok szerkesztését a fájl feltöltés opción keresztül.
* Csak akkor működik, ha az obm_id oszlop engedélyezve van.
* Létre kell hozni egy külön formot a szerkesztéshez.

Paraméterezés:

Fejleszői dokumentáció
	
	Függvények:

	Hívások:

move_project
------------
Általános leírás:

* A projekt költöztetése egyik szerverről a másikra.

Paraméterezés:

Fejleszői dokumentáció
	
	Függvények:

	Hívások:

photos
------
Általános leírás:

* Lehetővé teszi a fájl feltöltés funkciót, azáltal hogy létrehozza a **obm_files_id** oszloptípust, ami az OpenBioMaps saját oszloptípusa.
* Bekapcsolás utáni elérési útvonal: Projekt adminisztráció -> Adatbázis oszlopok. Hozzáadjuk az adattáblánkhoz az **obm_files_id** oszlopot, majd ennek az oszlopnak az *OpenBioMaps* típusát *"csatolmánynak"* állítjuk a legördülő menüből.

Paraméterezés:

Fejleszői dokumentáció
	
	Függvények:

	Hívások:

read_table
----------
Általános leírás:

* Görgethető html táblázatot hoz létre, ami egy linken keresztül elérhetővé lehet tenni.

Paraméterezés:
	
	schema.table, vagy
        schema.table:default-order-column

Fejleszői dokumentáció
	
	Függvények:

	Hívások:

restricted_data
---------------
Általános leírás:

* (Rule based data restriction) ??

Paraméterezés:

Fejleszői dokumentáció

	Függvények: rule_data()

	Hívások:

results_buttons
---------------
Általános leírás:

* Lekérdezés után a térképes felületen létrehozza a következő füleket: **Mentési opciók**, **Szerkesztési opciók**, **Megjelenítési opciók**.

Paraméterezés:

Fejleszői dokumentáció
	
	Függvények:

	Hívások:

results_asCSV
-------------
Általános leírás:

* Lekérdezésnél létrehoz egy letölthető .CSV fájlt. 
* A térkép alatt **Mentési opciók** fül lenyitásával találjuk meg ezt a fájlt.
* Be kell hozzá kapcsolni a *"results_button"* modult, hogy láthatóvá váljon a **Mentési opciók** fül.

Paraméterezés:

Fejleszői dokumentáció

	Függvények:

	Hívások:

results_asGPX
-------------
Általános leírás:

* Lekérdezésnél létrehoz egy letölthető .GPX fájlt, amit koordináta kezelő szoftverekkel tudunk alkalmazni pl.: GPS. 
* A térkép alatt **Mentési opciók** fül lenyitásával találjuk meg ezt a fájlt.
* Be kell hozzá kapcsolni a *"results_button"* modult, hogy láthatóvá váljon a **Mentési opciók** fül.

Paraméterezés:

Függvények:

Hívások:

results_asHtmltable
-------------
Általános leírás:

* Lekérdezésnél létrehoz egy .html fájlt. 
* A térkép alatt **Mentési opciók** fül lenyitásával találjuk meg ezt a fájlt.
* Be kell hozzá kapcsolni a *"results_button"* modult, hogy láthatóvá váljon a **Mentési opciók** fül.

Paraméterezés:

Fejleszői dokumentáció

	Függvények:

	Hívások:

results_asJSON
--------------
Általános leírás:

* Lekérdezésnél létrehoz egy letölthető .JSON fájlt. 

Paraméterezés:

Függvények:

Hívások:

results_asList
--------------
Általános leírás:

* Lehetővé teszi a listás lekérdezést.
* Lekérdezés után a térképes oldalon megjelenik a **Megjelenítési opciók** fülben a *"Kinyitható lista"* opció, ami csak feltöltés azonosítóját mutatja. A részletekre kattintva a feltöltéshez tartozó összes adat megjelenik egy külön ablakban.
* Be kell hozzá kapcsolni a *"results_button"* modult, hogy láthatóvá váljon a **Megjelenítési opciók** fül.

Paraméterezés:

Fejleszői dokumentáció

	Függvények: results_builder()

	Hívások:

results_asSHP
-------------
Általános leírás:

* Lekérdezésnél létrehoz egy letölthető .SHP fájlt, amit .zip formátumban lehet letölteni.

Paraméterezés:

Fejleszői dokumentáció

	Függvények:

	Hívások:

results_asStable
----------------
Általános leírás:

* Létrehoz egy kompakt táblázatot, amiben csak az általunk választott oszlopok lesznek benne.
* Be kell hozzá kapcsolni a *"results_button"* modult, hogy láthatóvá váljon a **Megjelenítési opciók** fül.

Paraméterezés:
Egymás alá írt oszlop nevek, felsorolás jel és vessző nélkül. Például:
	
	faj
	megfigyelő
	dátum

Fejleszői dokumentáció

	Függvények:

	Hívások:

results_asTable
-------------
Általános leírás:

* Olyan táblázatot hoz létre, ami az összes lekérdezett adatot tartalmazza.
* Nincs használva, mert nagy adatmennyiségeknél nagyon megterhelő a böngészőnek. Pár száz sor adat az még ok.

Paraméterezés:

Fejleszői dokumentáció

	Függvények:

	Hívások:

results_specieslist
-------------------
Általános leírás:

* Lekérdezés után a térképes felületen a térkép alatt az **Összefoglaló** fülben létrehozza *"Lekérdezésben előforduló fajok listáját"*.
* Be kell hozzá kapcsolni a *"results_summary"* modult, hogy láthatóvá váljon az **Összefoglaló** fül.

Paraméterezés:

Fejleszői dokumentáció

	Függvények:

	Hívások:

results_summary
---------------
Általános leírás:

* A térképes oldalon lekérdezés után létrehozza az **Összefoglaló** fület a térkép alatt.
* Kiírja a találatok számát.

Paraméterezés:

Fejleszői dokumentáció

	Függvények:

	Hívások:

simple_search
-------------

Általános leírás:

* Google-szerű automatikus kereső motor, több mezőben keres egyszerre, például, megfigyelő és fajnév

Paraméterezés:

Fejleszői dokumentáció

	Függvények:

	Hívások:

text_filter
-----------
Általános leírás:

* Lehetővé teszi bizonyos oszlopok alapján szűrjük a meglévő adatokat pl.: év, helyszín, feltöltő.
* A térképes oldalon létrehozza a **Szöveges szűrők** ablakot a térképes oldal jobb felén.
* Ha be van kapcsolva a *"text_filter2"* modul nem használható.

Paraméterezés:
Egymás alá írt oszlop nevek, felsorolás jel és vessző nélkül. Pl.:
	
	obm_datum
    	obm_uploading_date
    	obm_uploader_userfaj
    	obm_taxon
	
	Létre lehet hozni egymásba épített szűrőket 
			pl.: faj::colour_rings <- csak az adott fajon belül feltett színes gyűrű kombinációkat mutatja
	Létre lehet hozni legördülő (autocomplete) listákat 
			pl.: faj::autocomplete <- legördülő menüből választhatunk, hogy melyik fajra szeretnénk szűrni
	Kombinálhatjuk az egymásba épített és a legördülő menüt
			pl.: faj:nested(colour_rings):autocomplete
    	Akár egyedszám/populáció méeret szerint is lehet szűrni
			pl.: d.egyedszam:values(): 

Fejleszői dokumentáció

	Függvények:

	Hívások:

text_filter2
-----------
Általános leírás:

* Lehetővé teszi bizonyos oszlopok alapján szűrjük a meglévő adatokat pl.: év, helyszín, feltöltő.
* A térképes oldalon létrehozza a **Szöveges szűrők** ablakot a térképes oldal jobb felén.
* Ha be van kapcsolva a *"text_filter"* modul nem használható.
* Fejlesztés alatt!

Paraméterezés:
Egymás alá írt oszlop nevek, felsorolás jel és vessző nélkül. Pl.:	
	
	obm_datum
    	obm_uploading_date
	obm_uploader_userfaj
	obm_taxon

	Létre lehet hozni egymásba épített szűrőket 
			pl.: faj::colour_rings <- csak az adott fajon belül feltett színes gyűrű kombinációkat mutatja
	Létre lehet hozni legördülő (autocomplete) listákat 
			pl.: faj::autocomplete <- legördülő menüből választhatunk, hogy melyik fajra szeretnénk szűrni
	Kombinálhatjuk az egymásba épített és a legördülő menüt
			pl.: faj:nested(colour_rings):autocomplete
    	Akár egyedszám/populáció méret szerint is lehet szűrni
			pl.: d.egyedszam:values(): 

Fejleszői dokumentáció

	Függvények:

	Hívások:

transform_data
--------------
Általános leírás:

	* Lekérdezésnél átalakítja a kimeneti adatot pl.: geometria -> wkt

Paraméterezés:
Egymás alá írt sorok, felsorolás jel és vessző nélkül pl.:

	obm_geometry:geom
	obm_uploading_id:uplid
	tema:mmm

Fejleszői dokumentáció

	Függvények:

	Hívások:

validation
----------
Általános leírás:

Paraméterezés:

Fejleszői dokumentáció

	Függvények:

	Hívások:

