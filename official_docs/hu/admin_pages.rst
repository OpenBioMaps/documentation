Adminisztratív oldalak
**********************

.. _database-columns:

Adatbázis oszlopok
------------------
Itt lehet beállítani, hogy az egyes táblákból melyik oszlopok legyenek elérhetőek az űrlapok készítéséhez és lekérdezéshez a webes felületen. 

Szintén itt lehet megadni a különlegesen kezelet oszlopokat. Ez azt jelenti, hogy olyan oszlopok amiket egyes modulok használnak anélkül, hogy tudnák mi az oszlop pontos neve ill. ugyanilyen alapon metakeresésekben is elérhetőek. Ilyen kitüntetett oszlopok a fajnév, dátum, adatgyüjtő, példányszám és hely oszlopok. A hely oszlopnál külön megadható az X,Y koordináta oszlop és a postgres geometria oszlop is. Dátumnál megadható több dátum oszlop is, adatgyűjtőnél szintén több oszlop is megadható. Fajnévél külön megadható a tudományos és nemzeti nevet tartalmazó oszlop ha van ilyen. Minden egyéb oszlop "adat" típusúra kell beállítani.

A "megjegyzés mező" az oszlopok tartalmára vonatkozó leírásokat kell tartalmazzon (meta adatok), továbbá egyes esetekben szabályzó szerepe is lehet. Az obm_geometry oszlop esetén a megjegyzés mezőbe lehet megadni a geometria oszlop srid-ját, amit a feltöltött adatok tárolt srid-ját fogja meghatározni. Beírt értéket `srid:4326` formátumba kell megadni és a biomaps/header_names/f_srid helyen kerül eltárolásra és az alkalmazás az SRID_C globális változóban használja.

Az obm_id oszlopnál megadható, hogy legyen-e a rules tábla használva így: use_rules:1 Ezt csak master hozzáféréssel lehet módosítani.

Mindkét esetben az megjegyzés mezőben automatikusan odakerül a SET előtag, amit ki kell törölni, hogy érvényesítetni lehessen a módosítást. Ez azért van így, hogy ne lehessen véletlenül módosítani ezeket a paramétereket.

A lap címsávjának jobb oldalán látható >_ SQL gombbal egy SQL konzol nyitható. Ez csak üzemeltetői státusszal és külön authentikáció után használható.

Adat hozzáférés
---------------
A projekt általános hozzáférési beállításának megtekintése adat táblánként. Itt ez nem konfogurálható!

.. _admin-group-access:

Adminisztratív hozzáférések
---------------------------
Felhasználói csoportok hozzárendelése adminisztratív funkciókhoz. Például űrlap készítési vagy fajnév tábla kezelési jogkör kiadása.

.. _groups:

Csoportok
---------
Felhasználói csoportok létrehozása és felhasználók csoportokhoz hozzáadása itt történik. A felhasználói csoportok űrlapok, modulok és adminisztratív funkciókhoz való hozzáférés beállításban van jelentősége.


Faj nevek
---------
Minden projektben be lehet állítani egy fajnév tábla használatát, amely automatikisan gyűjti ki a megadott adattáblából a fajneveket. Tudmányos és nemzeti nyelvi neveket is tud kezeleni. A fajnév táblát használja a fajnév kereső modul. A fajnév tábla lehetőv teszi szinoním nevek használatát. 

A fajnév tábla elnevezése mindig a projektnév_taxon formájú, amelyben legalább a következő oszlopok szerepelnek: meta (szóközök nélküli fajnév), word (fajnév ahogy az adattáblában szerepel), lang (fajnevet tartalmazó oszlop neve), taxon_id (szinoním, nemezti és tudományos fajneveket egy faj összekötő egyedi belső azonosító),	status (elfogadott tudományos [1], szinoním tudományos [2], nemzeti név [3], hibás [4], nem kategorizált [0]),	modifier_id (az utolsó módosítást végző felhasználó azonosítója). További két oszlop kísérletesen szerepelhet: frequency (Lekérdezések száma az adott fajnévre - ez egy),	taxon_db (Az adott fajnév előfordulási gyakorisága az adott adattáblában). Ezen túl bármilyen egyéni kiegészítéssel bővíthető a taxon tábla, például védettség, taxon kategóriák.

Ezen az adminisztratív lapon történik a taxon tábla lekérdezése és karbantartása.


Felfüggesztett adatfeltöltések
------------------------------
A felhasználók elmentett és be nem fejezett feltöltései elérhetők innen. 


Feltöltő űrlapok
----------------
Itt lehet feltöltő űrlapokat létrehozni és módosítani. 

Az űrlapok kezelésének részletes leírása itt található:
:doc:`upload_forms`.


Fájl kezelő
-----------
Csatolt fájlként feltöltött képek és egyéb állományok listája és kezelése.


Függvények
----------
Táblatörténet, adat elérési szabályozás és fajnév táblák trigger függvényei itt megtekinthetőek és ki-be kapcsolhatóak.


Mapserver beállítások
---------------------
A projekthez tartozó mapserver mapfájlok konfigurálhatóak itt.


Modulok
-------
Beépülő modulok hozzáadása, engedélyezése és paraméterezésének felülete.
Az engedélyezett modulok használatát felhasználókhoz/csoportokhoz lehet rendelni.

Paraméterként megadhatunk egyszerű karakterláncot, vagy JSON objektumot.

Az elérhető modulok listája és leírásai itt találhatóak: 
:doc:`modulok <../modules>`


Nyelvi definíciók
-----------------
Meg lehet tekinteni itt az egész projektre globálisan definiált fordításokat. Ezek itt szerkeszthetőek: https://github.com/OpenBioMaps/translations/blob/master/global_project_translations.csv

Itt lehet a projektre érvényes fordításokat megadni. A fordítások mindig a projektre beállított nyelvre vontakoznak. Minden fordítható stringet str_somesthing_special_text formában kell megadni ahol az str_ előtag kötelező elem. Fordítások használhatók űrlap nevekben, oszlop nevekben, listákban, űrlap leírásokban, mező leírásokban.


Rshinyserver
------------
A projekthez lehet R-shiny szervert beállítani és így online felületen dinamikus statisztikai ábrákat megjeleníteni. Ez egy kísérleti állapotban lévő funkció, a konfigurálása sok munkát és az R/R-shiny alapos ismeretét igényli. További információ az R-shiny-ról itt: https://shiny.rstudio.com/


SQL lekérdezés beállítások
--------------------------
Adatlekérdezésekhez és térképi megjelenítések SQL lekérdezésekkel valósulnak meg. Az SQL lekérdezések dinamikusan készülnek minden egyes felhasználói kérésre (például a térkép navigálás során). Ezen a felületen lehet a projektünkhoz tartozó SQL lekérdezés sablonokat beállítani. Amennyiben több adattáblához is szeretnénk független térképi felületet megjeleníteni akkor több lekérdezést kell megadnunk. Egy lekérdezést letilthatunk. Ha kiürítjük a lekérdezést és úgy mentjük el, akkor az kitörlődik.
A lekérdezés vontakozhat csak térképre (alaptérképre vonatkozó lekérdezés). Ilyenkor a lekérdezés típusa "base", egyébként "query & base"


Szerver infó
------------
Jelenleg még csak az utolsó módosítás ideje és a módosított fájlok listája látható itt.


Szerver logok
-------------
Hibakeresésre szolgál. A projekt szerver belső üzenetei és a mapserver üzenetei tekinthetők meg itt. 


Tagok
-----
A projektbe regisztrált tagok listája. Felhasználói státuszt lehet itt megani. Ezek a következők: Normál, Üzemeltető, Felfüggesztett. A felfüggesztett felhasználók semmihez nem férnek hozzá a projektben, majdnem egyenértékű a profil törlésével.
Az üzemeltetőknak minden funkcióhoz és adathoz van hozzáférésük. Az adatbázis alapítónak nem muszály üzemeltetőnek lennie ahhoz, hogy mindenhez hozzáférjen. A normál felhasználók alap esetben a projekt jogosultság beállítása szerint férnek hozzá adatfeltöltési és adatlekérdezéi lehetőségekhez. Ez az alapeset módosítható csoportok létrehozásával és különféle jogosítványok csoportokhoz rendelésével. Lásd :ref:`Csoportok<groups>` és :ref:`Adminisztratív hozzáférések<admin-group-access>`.

A tagok csoport hozzárendelései is módosíthatók itt, de erre kényelmesebb felület a Csoportkezelő.

A tagok neve egy hivatkozás ezen a felületen. Ezt a hivatkozást követve a felhasználó profil lapjára léphetünk. Adminisztratív jogkörrel ilyenkor a lap cím sávban - jobboldalt, felül megjelenik egy fa-user-secret ikon (https://fontawesome.com/v4.7.0/icon/user-secret). Erre kattitva a saját felhasználói bejelentkezési adatainkkal át tudunk lépni egy másik felhasználó profiljába.


Tábla létrehozása
-----------------
Létre tudunk hozni egy SQL táblát, amit az OBM a projektünkhöz regsiztál és az alap OBM oszlopokat létrehozza benne. A tábla neve nem tartalmazhat ékezetes karaktereket, szóközt és egyéb speciális karaktereket. Keüljük a nagybetűk használatát is. A _ karakter megengedett. A táblához tetszőleges hosszúságú leírás megadása nyomatékosan ajánlott.

A tábla létrehozása után a felület automatikusan átvált az oszlop kezelő felületre, ahol a frissen létrehozott táblánkhoz oszlopkat tudunk hozzáadni. 

Az OBM felületen csak regisztrált táblákat tudunk használni (térképi megjelenítés, űrlap használat, szöveges lekérdezések)


Webes térképi rétegek
---------------------
A webes térképi megjelenítést egy JavaScript függvénykönyvtár az OenLayers valósítja meg, amely számára meg kell adni, hogy mely mapserver rétegünket milyen sql lekérdezéssel szólítson meg. 

A táblázat első oszlopában az SQL lekérdezéseknél megadott SQL lekérdezés nevekből tudunk választani. 

A második oszlopban a Mapserver számára küldött lekérdezés típusát lehet beállítani. Jelenleg csak a WMS támogatott. 

A harmadik oszlopban a mapserver map konfigurációs fájlunkban szereplő réteg nevét kell megadnunk.  

A negyedik oszlopban beállításokat adhatunk meg az OpenLayers számára. Itt a layers:'...' névnek meg kell egyeznie az előző oszlopban megadott réteg névvel. A következő oszlopban az SQL hozzárendelés státusza látható. 

Az URL oszlopban a "proxy" a legtöbb esetben jó választás, de egyéb speciális  beállítások is lehetségesek, pl Mapcache használata vagy Raster topotérképek esetén. A map proxy oszlopban  a default vagy proxy szónka kell szerepelnie. Ezek jelenleg egyenértékűek. Mapcache használata esetén másképp kell beállítani. 

Az OpenLaers név kötelető, de bármi lehet. Ez fog megjelenni a réteg választó felületen a felhasználóknak.

A sorrend oszlop kitöltésével tudjuk az OpenLayers rétegek kirajzolási sorrendjét megadni.

"OpenLayers réteg definíció" mező kiürítésével és a sor mentésével törölhető egy definíció.

