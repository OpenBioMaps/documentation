Projekt adminisztráció
**********************

.. _database-columns:

Adatbázis táblák és oszlopok
----------------------------

[web] -> [profile] -> [Projektadminisztráció] -> [adatbázis tábla kezelés]

Létre tudunk hozni egy SQL táblát, amit az OBM a projektünkhöz regisztrál és az alapértelmezett OBM oszlopokat létrehozza benne. A tábla neve ne tartalmazzon ékezetes karaktereket, szóközt és egyéb speciális karaktereket. Kerüljük a nagybetűk használatát is. A _ karakter megengedett. A táblához tetszőleges hosszúságú leírás megadása nyomatékosan ajánlott.

Az OBM felületen csak a regisztrált táblákat tudjuk használni (térképi megjelenítés, űrlap használat, szöveges lekérdezések)

Itt lehet beállítani, hogy az egyes táblákból melyik oszlopok legyenek elérhetőek az űrlapok készítéséhez és lekérdezéshez a webes felületen. 

Szintén itt lehet megadni a különlegesen kezelet oszlopokat. Ez azt jelenti, hogy olyan oszlopok amiket egyes modulok használnak anélkül, hogy tudnák mi az oszlop pontos neve ill. ugyanilyen alapon metakeresésekben is elérhetőek. Ilyen kitüntetett oszlopok a fajnév, dátum, adatgyüjtő, példányszám és hely oszlopok. A hely oszlopnál külön megadható az X,Y koordináta oszlop és a postgres geometria oszlop is. Dátumnál megadható több dátum oszlop is, adatgyűjtőnél szintén több oszlop is megadható. Fajnévél külön megadható a tudományos és nemzeti nevet tartalmazó oszlop ha van ilyen. Minden egyéb oszlop "adat" típusúra kell beállítani.

A "megjegyzés mező" az oszlopok tartalmára vonatkozó leírásokat kell tartalmazzon (meta adatok), továbbá egyes esetekben szabályzó szerepe is lehet. Az obm_geometry oszlop esetén a megjegyzés mezőbe lehet megadni a geometria oszlop srid-ját, amit a feltöltött adatok tárolt srid-ját fogja meghatározni. Beírt értéket `srid:4326` formátumba kell megadni és a biomaps/header_names/f_srid helyen kerül eltárolásra és az alkalmazás az SRID_C globális változóban használja.

Az obm_id oszlopnál megadható, hogy legyen-e a rules tábla használva így: use_rules:1 Ezt csak master hozzáféréssel lehet módosítani.

Mindkét esetben az megjegyzés mezőben automatikusan odakerül a SET előtag, amit ki kell törölni, hogy érvényesítetni lehessen a módosítást. Ez azért van így, hogy ne lehessen véletlenül módosítani ezeket a paramétereket.

A lap tetején elérhető egy SQL konzol, ami csak üzemeltetői státusszal és külön authentikáció után használható.
Szintén elérhető itt egy kinyitható lista az összes olyan tábla felsorolásával, ami a projektünk nevével kezdődik az SQL adatbázisban. Ezek közül ami pirossal van jelölve, azt nem kezeli az OBM felület, mert nincs beregisztrálva az OBM számára hozzáférhető táblák közé.


.. _access:

Adat hozzáférések
-----------------
A beállított hozzáférési szabályok és azok munkaállapotának áttekintése.

[web] -> [profile] -> [Projektadminisztráció] -> [adat hozzáférés]

[system] -> [/web-app-path/] -> [/projects/YOURPROJECT/local_vars.php.inc]

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

.. _Interrupted uploads:

Felfüggesztett adatfeltöltések
------------------------------
A felhasználók elmentett és be nem fejezett fájl vagy űrlapos adat feltöltései találhatóak meg itt. A feltöltéseket betöltve azok folytathatóak vagy el is lehe vetni őket. Többnyire kitörlhetőek ezek a megszakított feltöltések!

.. _Upload forms:

Feltöltő űrlapok
----------------
Itt lehet feltöltő űrlapokat létrehozni és módosítani. 

Az űrlapok kezelésének részletes leírása itt található:
:doc:`upload_forms`.

.. _File manager:

Fájl kezelő
-----------
Csatolt fájlként feltöltött képek és egyéb állományok listája és kezelése. Ki lehet exportálni egyben az egy táblához tartozó csatományokat, de ez némi időt vehet igénybe, mivel az exportálás egy háttérfolyamatként zajlik. Amikor készen van az export, akkor egy link jelenik meg az export gomb mellett.

.. _Functions:

Függvények
----------
Néhány előre elkészített trigger itt be- és kikapcsolható, és a hozzájuk tartozó funkciók szerkeszthetők.

A kiválasztott táblához kapcsolódó összes trigger és SQL-szabály állapotát is megtekintheti.

Beépített triggerek:

    - A taxonlista automatikus frissítése: A taxonszűrő által használt taxon-táblához hozzáadjuk a "tudományos nevet" és az "alternatív neveket",
    - Taxonnév automatikus frissítése: frissíti az adattáblát a taxontábla frissítésekor,
    - Előzmények: előzménysorok létrehozása az "előzménytáblában" a sorok frissítése és törlése után,
    - Hozzáférési szabályok: új sor beszúrása után szabálysor létrehozása a "szabályok táblában". Az alkalmazott szabályok az űrlap beállításaiból származnak.

.. _Map settings:

Térkép beállítások
------------------
[web] -> [profile] -> [Projektadminisztráció] -> [térkép beállítások]

A térképi megjelenítés beállításának három része van:

  - mapszerver konfiguráció
  - sql lekérdezés a mapszerver számára
  - openlayers beállítások a mapszerver számára

Mapserver
.........

Egy új projektnél be kell állítani a térkép kiterjedését. Ezt a legkönnyebb úgy megtenni, ha töltünk fel pár sor teszt adatot a várható kiterjedés sarkairól és a kalkulált kiterjedést beírjuk a private.map fájlba, amit ezen az adminisztratív oldalon tudunk szerkeszteni.

A publikus mapfájl használata további beállításokat igényel, jelenleg nem javasolt a használata.

OpenLayers
..........

Az OpenLayers definícióknál tudunk összekötni egy SQL lekérdezést egy MapServer réteggel. Erre azért van szükség, mert a mapserverben alap esetben nem statikus lekérdezések vannak, hanem a webes felületen végrehajotott lekérdezéseket kapja meg a MapServer. Válasszuk ki, hogy melyik SQL lekérdezést melyik MapServer réteghez szeretnénk kapcsolni, adjunk egy tetszőleges nevet az OpenLayers rétegnek és többi változót hagyjuk az alapértelmezett értéken.

"OpenLayers réteg definíció" mező kiürítésével és a sor mentésével törölhető egy definíció.

.. _Modules:

Modulok
-------
A beépülő modulokkal számos extra funkció válik elérhetővé a rendszerünkben, de ezek többnyire további beállításokat igényelnek. 
A modulokat lehet saját igények szerint módosítani, habár ezek karbantartásáról ez után nekünk kell gondokodni. A módosított modulokat meg lehet osztani a közösséggel!

Az engedélyezett modulok használatát felhasználókhoz/csoportokhoz lehet rendelni.

A paramétereket JSON objektumként tudjuk megadni a moduloknak.

Az elérhető modulok listája és leírásai itt találhatóak: 
:doc:`modulok <../modules>`

.. _Translations:

Nyelvi definíciók
-----------------
Meg lehet tekinteni itt az egész projektre globálisan definiált fordításokat. Ezek itt szerkeszthetőek: https://github.com/OpenBioMaps/translations/blob/master/global_project_translations.csv

Itt lehet a projektre érvényes fordításokat megadni. A fordítások mindig a projektre beállított nyelvre vontakoznak. Minden fordítható stringet str_somesthing_special_text formában kell megadni ahol az "str\_" előtag kötelező elem. Fordítások használhatók űrlap nevekben, oszlop nevekben, listákban, űrlap leírásokban, mező leírásokban.

.. _SQL query settings:

SQL lekérdezés beállítások szöveges és térképi lekérdezésekhez
--------------------------------------------------------------
Itt konfigurálhatja azokat az SQL-lekérdezéseket, amelyeket a Mapserver a térképadatok megjelenítéséhez, a webalkalmazás pedig a lekérdezések szöveges eredményeinek megjelenítéséhez használ.
Ezek többnyire nem valódi SQL-parancsok, hanem az SQL-lekérdezések összeállítására szolgáló sablonok, közelítő SQL-szintaxissal.

A Mapserver/térkép fájlban a WMS rétegeknek tartalmazniuk kell egy DATA definíciós sort egy %query% helyettesítő karakterlánccal, hogy az itt definiált SQL sablon alapján dinamikusan generált SQL parancsot használhasson.

Minden SQL-lekérdezést egy webtérkép-réteghez kell kapcsolni. Az utolsó oszlopban állíthatja be ezeket a kapcsolatokat. Az SQL-lekérdezésekben két helyettesítő változó van a dinamikus lekérdezések végrehajtásához: %qstr% és %morefilters%.

A lekérdezés tartalmazhat varázsszavakat. Ezek % karakterekkel vannak elválasztva. Ezeket dinamikusan valódi SQL karakterláncokkal helyettesíti az OBM SQL-értelmező.
Egyes modulok is generálhatnak ilyen varázsszavakat!
 
.. code-block:: SQL
 
    SELECT obm_id, %grid_geometry% AS obm_geometry 
        %selected%
    FROM %F%nestbox c%F%
        %uploading_join%
        %rules_join%
        %taxon_join%
        %grid_join%
        %search_join%
        %morefilter%
    WHERE %geometry_type% %envelope% %qstr%
    
A %grid_geometry% AS obm_geometry helyett használd csak az obm_geometry kifejezést, ha nincs beállítva grid modul! Szintén ne tedd be a %grid_join% se a lekérdezésbe, ha nincs beállítva a grid modul. A %search_join% is modul specifikus.

Használd %F% és egy alias nevet is a FROM tábla megadásánál. Ez feltétlenül szükséges a lekérdezés feldolgozásához
Ha egy másik táblát is szeretnél JOIN-olni akkor használd a  %J% határolót a JOIN kifejezés körül. Például:

.. code-block:: SQL

    SELECT n.obm_geometry,n.obm_id,-2 AS date_part,nestbox_type,project_id,beinaction
        %selected%
    FROM %F%nestbox n%F%
        %J%LEFT JOIN nestbox_observations o ON o.nestbox_id=n.obm_id%J%
        %taxon_join%
        %morefilter%
    WHERE %envelope% %qstr%

Lehetséges még komplexeb lekérdezés összerekasára is:

.. code-block:: SQL

    WITH aall AS (
        SELECT o.obm_id,n.obm_geometry,nestbox_type,project_id,beinaction,
        COALESCE(extract(days FROM (CURRENT_DATE-datum)::interval),'-1') as  date_part
            %selected% 
        FROM %F%nestbox_observations o%F%
        %J%LEFT JOIN nestbox n ON (nestbox_id=n.obm_id) %J%
        %taxon_join%
        %morefilter% 
        WHERE 1=1 %envelope% %qstr% 
    )
    SELECT * FROM aall ORDER BY date_part DESC


.. _Server info:

Szerver infó
------------
Számos alap info elérhető a projektről, mint az alkalmazás verzió száma, tárhely használati adatok, rendszer terhelé és memória használat, továbbá a Supervisor projekt adminisztrációs felület linkje.

.. _Server logs:

Szerver logok
-------------
Hibakeresésre szolgál. A projekt szerver belső üzenetei és a mapserver üzenetei tekinthetők meg itt. 

.. _Members:

Tagok
-----
A projektbe regisztrált tagok listája. Felhasználói státuszt lehet itt megani. Ezek a következők: Normál, Üzemeltető, Felfüggesztett. A felfüggesztett felhasználók semmihez nem férnek hozzá a projektben, majdnem egyenértékű a profil törlésével.
Az üzemeltetőknak minden funkcióhoz és adathoz van hozzáférésük. Az adatbázis alapítónak nem muszáj üzemeltetőnek lennie ahhoz, hogy mindenhez hozzáférjen. A normál felhasználók alap esetben a projekt jogosultság beállítása szerint férnek hozzá adatfeltöltési és adatlekérdezéi lehetőségekhez. Ez az alapeset módosítható csoportok létrehozásával és különféle jogosítványok csoportokhoz rendelésével. Lásd :ref:`Csoportok<groups>` és :ref:`Adminisztratív hozzáférések<admin-group-access>`.

A tagok csoport hozzárendelései is módosíthatók itt, de erre kényelmesebb felület a Csoportkezelő.

A tagok neve egy hivatkozás ezen a felületen. Ezt a hivatkozást követve a felhasználó profil lapjára léphetünk. Adminisztratív jogkörrel ilyenkor a lap cím sávban - jobboldalt, felül megjelenik egy fa-user-secret ikon (https://forkaweso.me/Fork-Awesome/icon/user-secret/). Erre kattitva a saját felhasználói bejelentkezési adatainkkal át tudunk lépni egy másik felhasználó profiljába.

.. _Background jobs:

Háttérfolyamatok kezelése
-------------------------

[web] -> [profile] -> [Projektadminisztráció] -> [háttérfolyamatok]

Az OBM képes háttérben feladatokat elvégezni. Háttérfolyamat szkripteket le tudunk tölteni a lapról elérhető git repo-ból és ezeket is módosíthatjuk, vagy a sablon szkript alapján teljesen újat írhatunk. A héttérfolyamatoknak van egy run és egy lib állománya. Az ütemező a run állományunkat hívja meg, ami sztenderd php job esetén a lib állományban lévő feladatokat hajtja végre.

Az ütemezés  cron-szerű, perc - óra - nap mezőket kell kitölteni hozzá, amely miden esetben lehet * is, azaz minden perc, óra, nap értékű. A jobot, ha nem engedélyezzük nem fut le. Engedélyezés nélkül is tudjuk tesztelni [run]. A [results]-al pedig az adott job utolsó eredményeit tudjuk megnézni.

Ahhoz, hogy az ütemező fusson, a gazdagépnek is kell egy ütemező Cron bejegyzés minden projekt job futtató scriptjéhez lennie. Ezt a szerver rendszergazdája tudja beállítani. Pl:

```
*/5 * * * * /usr/local/bin/docker-compose -f /srv/docker/openbiomaps/docker-compose.yml exec -u www-data -T app php /var/www/html/biomaps/root-site/projects/myproject/jobs.php
```
