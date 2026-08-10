PWA térképi lekérdező alkalmazás
================================

Mi az OBM térképi lekérdező alkalmazás?
---------------------------------------

Az OBM térképi lekérdező alkalmazás egy terepi munkát támogató online/offline
hibrid alkalmazás, más néven progresszív webalkalmazás (Progressive Web App,
PWA). Hozzáférést biztosít egy online OpenBioMaps-adatbázishoz, lehetővé teszi
a felhasználók számára rekordok lekérdezését, és megjeleníti azok térbeli
helyét.

Az alkalmazás böngészőmotorban fut, és elsősorban mobileszközökhöz készült.
A legtöbb művelethez hálózati kapcsolat szükséges, de a korábban lekért adatok
offline is elérhetők.

A progresszív webalkalmazásokról további információt itt talál:

[Progresszív webalkalmazások a web.dev webhelyen](https://web.dev/progressive-web-apps/)

Hogyan működik?
---------------

Online állapotban a projekt adatai rétegként jeleníthetők meg az alaptérkép
felett. Az adatok klaszterezett pontrétegként jelennek meg, ahol az egyes
klaszterszimbólumokban látható címke a klaszterben található elemek számát
jelzi.

A térkép szűrő- és lekérdezőeszközöket biztosít az online adatbázis adatainak
lekéréséhez. Alapértelmezés szerint az alkalmazás az aktuális térképnézetet
használja lekérdezési területként. A szűrő alkalmazása lekéri az aktuális
kiterjedésen belül látható összes egyező rekordot.

Kerülje a szükségtelenül nagy terület lekérdezését. Nagyszámú rekord lekérése
és megjelenítése lelassíthatja az alkalmazást, vagy az alkalmazás
válaszképtelenné válhat.

A kért adatok letöltése után a klaszterréteg megjelenése kissé megváltozik,
jelezve, hogy az elemek elérhetők az eszközön. A letöltött elemek továbbra is
klaszterezve maradnak, mert sok különálló pont megjelenítése jelentősen
csökkenthetné az alkalmazás teljesítményét.

Egy klaszter kiválasztásakor görgethető modális párbeszédablak nyílik meg,
amely a klaszterben található elemek attribútumait tartalmazza.

Az alkalmazás böngészőben fut, de telepíthető és a szokásos böngészőfelület
nélkül is elindítható, így egy önálló mobilalkalmazáshoz hasonlóan viselkedik.
A lekért projektadatokat az alkalmazás offline tárhelyen tárolja. Az
alaptérképek nem töltődnek le automatikusan offline használatra, bár a
korábban megtekintett térképcsempék a böngésző gyorsítótárában maradhatnak.

A támogatott böngészők lehetőséget kínálhatnak az alkalmazás eszközre történő
telepítésére. A Chrome-ban és más Chromium-alapú böngészőkben ez a lehetőség a
címsorban vagy a böngésző menüjében jelenhet meg. A PWA telepítése
alkalmazásszerűbb felületet biztosít, és könnyebben elérhetővé teszi az offline
funkciókat.

Funkciók
--------

- A felhasználó aktuális helyének megjelenítése sárga ponttal.
- A GPS pontosságának megjelenítése a helyzetjelző körüli szürke körrel.
- Útvonalnapló megjelenítése.
- Az útvonalnaplózás elindítása és leállítása.
- Nagyítás a felhasználó aktuális helyére.
- Pontszerű elemek lekérdezése az online adatbázisból kör vagy poligon
  rajzolásával, illetve az aktuális térképnézet használatával.
- A lekért rekordok tárolása offline hozzáféréshez.
- A lekért rekordok attribútumainak megjelenítése.

Korlátozások
------------

- Csak pontszerű elemek támogatottak.
- Az alaptérképek nem tölthetők le kifejezetten offline használatra.
- Nagyszámú, például több mint 50 000 rekord lekérése teljesítmény- vagy
  offline tárhellyel kapcsolatos problémákat okozhat.
- A korábban megtekintett alaptérképcsempék offline elérhetősége a böngésző
  gyorsítótárazásától függ, és nem garantált.
- A PWA telepítése és offline működése böngészőnként és operációs
  rendszerenként eltérhet.

Az alkalmazás URL-je
--------------------

Az alkalmazás a következő projektspecifikus URL-en érhető el:

`https://YOUR_SERVER/projects/YOUR_PROJECT/pwa-map/`

Helyettesítse:

- a `YOUR_SERVER` értékét az OpenBioMaps-kiszolgáló állomásnevével;
- a `YOUR_PROJECT` értékét a projekt azonosítójával vagy könyvtárnevével.

A PWA-alkalmazás konfigurációs beállításai
-----------------------------------------

Néhány beállítást a projekt adminisztrációs felületén kell konfigurálni.

### MapServer-réteg

A **Térképbeállítások** oldalon adjon hozzá egy új MapServer-réteget a projekt
*privát térképfájljához*:

```
LAYER
    NAME "my_cluster"
    TYPE point
    STATUS on

    CONNECTIONTYPE postgis
    CONNECTION "host=localhost dbname=gisdata password={xxxxx} user=YOUR_PROJECT_admin options='--client_encoding=UTF8'"

    PROJECTION
        "init=epsg:4326"
    END

    METADATA
        "wms_title" "YOUR_PROJECT Cluster layer"
        "wms_srs"   "epsg:4326 epsg:900913"
    END

    DATA "obm_geometry FROM (SELECT * FROM YOUR_PROJECT WHERE ST_GeometryType(obm_geometry)='ST_Point') as new_table USING UNIQUE obm_geometry USING srid=4326"

    CLUSTER
        MAXDISTANCE 50
        REGION "ellipse"
    END

    LABELITEM "Cluster_FeatureCount"
    CLASSITEM "Cluster_FeatureCount"

    CLASS
        NAME "Clustered points"
        MAXSCALEDENOM 100000
        EXPRESSION ("[Cluster_FeatureCount]" != "1")
        STYLE
            SYMBOL "circle"
            SIZE 30
            COLOR 51 153 204
            OUTLINECOLOR 30 30 30
            OUTLINEWIDTH 1
        END
        LABEL
            #FONT arial
            #TYPE TRUETYPE
            SIZE 8
            COLOR 255 255 255
            ALIGN CENTER
            PRIORITY 10
            BUFFER 1
            PARTIALS TRUE
            POSITION cc
        END
    END

    CLASS
        NAME "Single point"
        MAXSCALEDENOM 100000
        EXPRESSION "1"
        STYLE
            SIZE 12
            SYMBOL "circle"
            COLOR 000 130 255
            OUTLINECOLOR 30 30 30
            OUTLINEWIDTH 1
        END
        TEXT "[NAME_OF_YOUR_LABELING_COLUMN]"
        LABEL
            #FONT arial
            #TYPE TRUETYPE
            SIZE 8
            COLOR 0 0 0
            OUTLINECOLOR 255 255 255
            ALIGN CENTER
            PRIORITY 9
            BUFFER 1
            PARTIALS FALSE
            POSITION ur
        END
    END

    TOLERANCE 50
    UNITS PIXELS
END # WMS cluster layer
```

Helyettesítse a következő helyőrzőket:

- A `NAME_OF_YOUR_LABELING_COLUMN` az egyes pontok feliratozására használt
  oszlop neve. Erre gyakran egy fajnevet tartalmazó oszlopot használnak.
- A `YOUR_PROJECT` a réteg által lekérdezett adatbázistábla neve. Ez általában
  a projekt alaptáblája.
- A `YOUR_PROJECT_admin` a projekt által használt PostgreSQL-felhasználó.
- Az `{xxxxx}` helyére a megfelelő adatbázisjelszót kell írni.

A `MAXSCALEDENOM 100000` megakadályozza az elemek megjelenítését, amikor a
térkép méretaránya 1:100 000-nél kisebb. Ez segít megelőzni, hogy a
MapServernek nagyon sok klasztert kelljen kiszámítania.

Az adatbázis-kapcsolati karakterláncnak meg kell felelnie a
kiszolgálókörnyezetnek. Ne másolja át a példában szereplő jelszót, és ne
rögzítsen valódi adatbázis-hitelesítő adatokat dokumentációban vagy
forráskód-tárolóban. A legbiztonságosabb megoldás, ha ugyanazon projekt egy
másik, működő rétegének kapcsolati beállításait másolja át, és minden értéket
ellenőriz.

A példában szereplő kapcsolati karakterlánc:

`CONNECTION "host=localhost dbname=gisdata password={xxxxx} user=YOUR_PROJECT_admin options='--client_encoding=UTF8'"`

A megfelelő adatbázis-állomásnév a telepítési környezettől függ.
Konténeralapú telepítésben ez a PostgreSQL-szolgáltatás neve is lehet a
`localhost` helyett.

### SQL-lekérdezés

Az **SQL-lekérdezés beállításai** oldalon hozzon létre egy lekérdezést a
PWA-alkalmazáshoz:

```
SELECT obm_id, obm_geometry, NAME_OF_YOUR_LABELING_COLUMN %selected%
FROM YOUR_PROJECT
%morefilter%
WHERE ST_GeometryType(obm_geometry)='ST_Point' AND %qstr%
```

A `NAME_OF_YOUR_LABELING_COLUMN` és a `YOUR_PROJECT` helyére ugyanazokat az
értékeket írja, amelyeket a MapServer-rétegben használt.

Ne távolítsa el a következő OpenBioMaps-lekérdezési helyőrzőket:

- `%selected%`
- `%morefilter%`
- `%qstr%`

Az előre meghatározott geometriai szűrő pontgeometriákra korlátozza az
eredményt. Erre azért van szükség, mert a klaszterező réteg nem tudja a vonal-
és poligonelemeket egyesíteni.

Mielőtt engedélyezi az alkalmazást a felhasználók számára, tesztelje a
lekérdezést egy kis térképnézettel, és ellenőrizze, hogy:

- csak az aktuális felhasználó számára hozzáférhető rekordok jelennek meg;
- minden visszaadott rekord érvényes `obm_id` értékkel rendelkezik;
- minden visszaadott geometria pontgeometria;
- a kiválasztott feliratoszlop szerepel az eredményben; és
- a lekérdezés elfogadható időn belül befejeződik.

Telepítés
---------

A MapServer- és SQL-lekérdezési beállítások elvégzése után az alkalmazás
inicializálásához nyissa meg egyszer a következő URL-t:

`https://YOUR_SERVER/projects/YOUR_PROJECT/pwa-map/setup.php`

A `YOUR_SERVER` és a `YOUR_PROJECT` helyére az alkalmazás URL-jében használt
értékeket írja.

A beállítás befejezése után nyissa meg az alkalmazást a következő címen:

`https://YOUR_SERVER/projects/YOUR_PROJECT/pwa-map/`

Mindig HTTPS-t használjon. A PWA fontos funkcióihoz – beleértve a service
workereket, a telepítést, a helyadatokhoz való hozzáférést és a megbízható
offline működést – biztonságos környezet szükséges.

Az alkalmazás megnyitása után:

1. ellenőrizze, hogy a térkép betöltődik;
2. adja meg a helyhozzáférési jogosultságot, ha szükség van a helymeghatározási
   és útvonalnapló-funkciókra;
3. futtasson egy lekérdezést egy kis területen;
4. ellenőrizze, hogy a klaszterek és a rekordok attribútumai megjelennek;
5. telepítse a PWA-t a böngésző telepítési lehetőségével, ha az elérhető; és
6. a hálózati kapcsolat megszakítása után tesztelje a korábban lekért
   rekordokhoz való hozzáférést.
