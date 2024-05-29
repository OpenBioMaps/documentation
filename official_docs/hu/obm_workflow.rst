OpenBioMaps folyamatok
**********************

.. _PostgreSQL-Backend
  
Postgres háttér
===============

.. _Database-tables

Adatbázis háttér
----------------

.. _Tables

Táblák
......
Az OpenBioMaps csak azokat Postgres táblákat kezeli, amelyeket az OBM admin felületen keresztül hozunk létre. A tábla létrehozásakkor azokat 
beregisztrálja a projektben kezelt táblák közé. Amennyiben egy SQL kliensen keresztül átnevezzük a táblánkat, akkor az OBM elveszíti a kapcsolatot a táblával. Amennyiben SQL kliensből 
kitörlünk egy táblánkat, akkor az OBM automatikusan kitörli a hozzá kapocslódó metaadatokat is. Üres táblát ki lehet törölni az OBM admin felületen keresztül is.
  
.. _metadata

Meta adatok
...........
Az adatbázis táblákhoz megadható egy leíró metaadat, amely kitöltése ugyan nem kötelező, de nagyon ajánlott. 
Alapvetően jó gyakorlat leíró információkkal ellátni a tábláinkat és a mezőinket!

.. _database-columns
  
Adatbázis oszlopok
------------------

.. _default-columns

Alapértelmezett mezők
.....................

Az OpenBioMaps minden általa létrehozott táblában létrehoz több alapértelmezett mezőt, amelynek a megléte kötelező ahhoz, hogy az OBM tudja kezelni a táblát.
Ezeket a mezőket soha ne töröljük ki a tábláinkból!

Ezek a mezők a következőek:

.. code-block:: SQL
  
  CREATE TABLE public.test_table (
    obm_id integer DEFAULT nextval('public.test_table_obm_id_seq'::regclass) NOT NULL,
    obm_geometry public.geometry,
    obm_uploading_id integer,
    obm_validation numeric,
    obm_comments text[],
    obm_modifier_id integer,
    obm_files_id character varying(32),
    CONSTRAINT enforce_dims_obm_geometry CHECK ((public.st_ndims(obm_geometry) = 2)),
    CONSTRAINT enforce_srid_obm_geometry CHECK ((public.st_srid(obm_geometry) = 4326))
  );
  
.. _SQL-columns-vs-OpenBioMaps-columns

SQL mezők vs. OpenBioMaps mezők
...............................
Az SQL-adatbázis mezőit az OpenBioMaps kezeli az összes táblában, viszont csak azokat a mezőket, amelyeknek a használatát az OBM jóváhagyja. 
A jóváhagyás a mező OBM típusának megadásával történik az adminisztrációs felületen.
Az OBM típus, a postgres típustól eltérően, nem a mező tartalmára, hanem a használat módjára vonatkozik.

.. _column-names:

Mező nevek
..........
A mezők elnevezése korlátozott az OBM-ben a Postgres-hez képest. Az OBM nem engedélyezi a nagybetűket és a különleges karaktereket a mezőnevekben, csak az aláhúzásokat. 
Ugyanakkor minden mezőhöz hozzárendel egy megjelenítendő név metaadatot, amely lehet egy automatikusan lefordítható karakterlánc, így minden mezőt a nevével együtt lehet 
megjeleníteni az űrlapokon vagy az adatlekérdezések során. A felhasználó csak a nyers adatok lekérdezésekor látja az eredeti mezőneveket, egyébként a mező létrehozásakor 
megadott karakterláncot vagy annak automatikus fordítását látja.

.. _column-order:

Mező sorrend
............
A Postgres-ben nem adhatja meg a mezők sorrendjét, de az OBM-ben igen. Egyrészt megadható egy alapértelmezett sorrend, amelyet az OBM mind az adatok megjelenítésénél, mind az 
űrlapokon használ, másrészt ez a sorrend felülírható minden egyes űrlapon. Ha nem ad meg semmilyen sorrendet, akkor a mezők a Postgres alapértelmezett mezősorrendjét követik.
Ha meg akarjuk változtatni a mezőink sorrendjét a Postgresben, az egyik megoldás egy nézet használata, vagy a táblázatunk újradefiniálása a megfelelő mezősorrenddel. Az utóbbi 
esetben használhatunk egy CREATE TABLE ... SELECT FROM lekérdezést, hogy a régiből új táblát hozzunk létre, majd töröljük a régit, és az újat nevezzük át a régire, de figyeljünk 
oda a triggerekre, szekvenciákra és kulcsokra is, hogy átvezessük őket!

A Postgres-ben nem adhatja meg a mezők sorrendjét, de az OBM-ben igen. Egyrészt megadható egy alapértelmezett sorrend, amelyet az OBM mind az adatok megjelenítésénél, mind 
az űrlapokon használ, másrészt ez a sorrend felülírható minden egyes űrlapon. Ha nem ad meg semmilyen sorrendet, akkor a mezők a Postgres alapértelmezett mezősorrendjét követik.
Ha meg akarjuk változtatni a mezőink sorrendjét a Postgresben, az egyik megoldás egy nézet használata, vagy a táblázatunk újradefiniálása a megfelelő mezősorrenddel. 
Az utóbbi esetben használhatunk egy CREATE TABLE ... SELECT FROM lekérdezést, hogy a régiből új táblát hozzunk létre, majd töröljük a régit, és az újat nevezzük át a régire, 
de figyeljünk oda a triggerekre, szekvenciákra és kulcsokra is, hogy átvezessük őket!

.. _visible-names:

Megjelenített nevek
...................
Az OpenBioMaps a mezők SQL-ben látható nevei helyett egy metaadatban tárolt úgynevezett megjelenítendő nevet használ a mezők nevének a megjelenítésére, 
amelyet a mezőket létrehozó adminisztrátor ad meg. Alapesetben ez azonos a mező Postgres nevével. Amennyiben a mező neve str_ előtaggal kezdődik, akkor ezek a 
sztringek a kliens alkalmazás nyelvi beállításai szerinti fordítással jelennek meg, amennyiben adtunk meg fordításokat a sztringjeinkhez. 

.. _data-input

Adat bevitel
============

.. _openbiomaps-way

OpenBioMaps út
--------------
Adatok az adattáblákba a feltöltő űrlapokon keresztül tölthetőek be, vagy bármilyen SQL kliensen keresztül is. 
A feltöltő űrlapokkal történt adatbevitel során az adat feltöltési esemény rögzítésére kerül a system.uploading táblában és a feltöltés metaadatai elérhetőek lesznek az adatokkal együtt.

.. _sql-ways

SQL megoldások
--------------
Nagy adatmennyiségek beolvasása történhet a COPY FROM Postgres eszközzel is!


.. _Data-output

Adat kimenet
============

.. _OpenBioMaps-output

OpenBioMaps kimenet
------------------_
Az adatok lekérdezhetőek a webes felületen vagy API-n keresztül. Lehetőség van teljes táblák letöltésére, exportálására vagy az adatok szűrésére, megjelenítésére és exportálására is.

.. _Other-outputs

Egyéb kimenetek
---------------
Az OpenBioMaps az adatokat alapvetően egyszerű strktúrákba tárolja, ilyen módon SQL klienseken keresztül az adatok egyszerűen lekérdezhetőek és ábrázolhatóak, pl. QGIS-ben.

.. _Users

Felhasználók
============

