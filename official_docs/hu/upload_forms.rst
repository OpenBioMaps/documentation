.. _manage-upload-forms:

Feltöltési űrlapok kezelése
===========================

A feltöltési űrlapok határozzák meg, hogy a felhasználók és külső kliensek
hogyan küldhetnek adatokat egy projektbe. Az űrlap meghatározza a céltáblát,
az elérhetőséget, a hozzáférési beállításokat, a támogatott klienseket, a
mezőket, az érvényesítési szabályokat, az alapértelmezett értékeket és a mezők
közötti kapcsolatokat.

.. TODO: Adjon hozzá egy bevezető munkafolyamatot, amely elmagyarázza a
   feltöltési űrlapok létrehozását, tesztelését, közzétételét, másolását,
   letiltását és kivezetését.

.. TODO: Ismertesse, hogy milyen adminisztrátori jogosultság szükséges a
   feltöltési űrlapok kezeléséhez, és adja meg az oldal jelenlegi navigációs
   útvonalát.

.. TODO: Tisztázza, hogy mely beállítások közösek a webes, fájlfeltöltési,
   API- és mobilkliensekben, és nevezze meg azokat a beállításokat, amelyeket
   csak egy adott kliens támogat.


Az elérhető űrlapok listája
---------------------------

A meglévő űrlapok kiválaszthatók szerkesztésre, törlésre vagy letiltásra.

Letiltott űrlapokkal nem tölthetők fel adatok, és ezek az űrlapok nem láthatók
a kliensek űrlaplistájában. Az offline kliensek nem tölthetnek fel adatokat
törölt űrlapokkal, és a törölt űrlapok nem állíthatók vissza.
Az űrlapok szerkesztésével módosítható a hatókörük (web, API vagy
fájlfeltöltés), az adatbázistábla mezőivel való kapcsolatuk, a leírásuk és a
hozzáférési szabályaik, valamint az, hogy megfigyelési esemény vagy alkalmi
módban működjenek-e.

A letiltott űrlapok szürke háttérrel jelennek meg a listában.

Az űrlapok írásvédettre is állíthatók, amit egy lakat ikon jelez a listában.
(Ehhez állítsa a ``project_forms`` tábla ``active`` mezőjének értékét 3-ra.)


Az űrlap fejlécének meghatározása
---------------------------------

Céltábla
........

Válassza ki azt a projekttáblát, amelybe a feltöltési űrlapon beküldött adatok
kerülnek.

Csak olyan, az OpenBioMaps által a projekten belül regisztrált SQL-táblák
választhatók ki, amelyek tartalmazzák az OpenBioMaps alapmezőit, például az
obm_id, obm_uploading_id stb. mezőket.
A kiválasztott tábla később nem módosítható, mivel az űrlap mezői a
kiválasztott tábla mezőihez kapcsolódnak.

Az űrlapok érzékenyek a táblaszerkezet változásaira. Emiatt erősen ajánlott,
hogy a táblákat ne az OpenBioMaps rendszeren kívüli eszközzel szerkessze, mert
így az űrlap elveszíti kapcsolatát a mezőkkel. Ilyen esetekben az űrlap
módosításainak mentése megoldhatja az inkonzisztenciát, de a kliensek nem
tudják majd feltölteni az offline adatokat!


Az űrlap neve
.............

Adja meg a feltöltési űrlap nevét. A névnek egyedinek kell lennie a projekten
belül, mivel a név az űrlapok egyedi azonosítójának része.

Egy űrlap a nevének módosításával másolható. Ebben az esetben az eredeti űrlap
megtartja eredeti nevét; más szóval egy űrlapot nem lehet átnevezni, csak újat
lehet létrehozni, ami hatással van az offline kliensek működésére!

A név többnyelvű lehet, ha ``str_`` előtaggal rendelkező fordítási kulcsot
használ. További információért lásd:
:ref:`Fordítások <localisation>`.


Hozzáférés az űrlaphoz
......................

Határozza meg, hogy kik láthatják és használhatják az űrlapot:

* nyilvános felhasználók;
* minden bejelentkezett felhasználó; vagy
* csak a megadott csoportok.

Ha a **csak a megadott csoportok** lehetőség van kiválasztva, aktívvá válik a
felhasználó- és csoportválasztó mező, amelyben hozzáférés adható a kiválasztott
felhasználóknak vagy csoportoknak.

.. TODO: Erősítse meg az adminisztrációs felületen jelenleg használt
   feliratokat, valamint azt, hogy a hozzáférés csoportok mellett közvetlenül
   egyéni felhasználókhoz is hozzárendelhető-e.

.. TODO: Magyarázza el, hogy a nyilvános űrlap-hozzáférés engedélyezi-e a
   hitelesítés nélküli adatbeküldést, és ebben az esetben hogyan történik a
   feltöltő, a tulajdonjog, az olvasási és írási hozzáférés, a
   sebességkorlátozás és a visszaélések megelőzésének kezelése.

.. TODO: Tisztázza, hogy a beágyazott csoporttagság hozzáférést biztosít-e az
   űrlaphoz, valamint azt, hogy a csoporttagság változásai hogyan érintik a
   folyamatban lévő vagy mentett feltöltéseket.


Adathozzáférés
..............

Az űrlapon keresztül feltöltött adatok csak az itt megadott csoportok számára
lesznek elérhetők. Alapértelmezés szerint a feltöltő olvashatja és
szerkesztheti a feltöltött adatokat.

.. TODO: Dokumentálja, hogy az űrlap adathozzáférési beállításai hogyan
   kerülnek át a projekt sorszintű hozzáférési szabályaiba, beleértve az
   olvasási és írási hozzárendelések pontos jelentését és formátumát.

.. TODO: Erősítse meg a működést arra az esetre, ha nincs kiválasztva
   csoport, valamint azt, hogy a feltöltő mindig kap-e olvasási és írási
   hozzáférést.

.. TODO: Magyarázza el, hogyan működnek együtt ezek a beállítások az
   ``ACC_LEVEL``, ``MOD_LEVEL`` és érzékenységi beállításokkal, a
   hozzáférésiszabály-triggerrel és az ``allowed_columns`` modullal. Adjon
   példákat nyilvános, bejelentkezéshez kötött és csoportokra korlátozott
   projektekhez.

.. TODO: Dokumentálja, hogy mi történik az űrlap adathozzáférési
   beállításainak módosításakor. Tisztázza, hogy az új beállítások csak a
   későbbi feltöltéseket érintik-e, vagy a meglévő rekordokat is frissítik.


Űrlaptípus
..........

A következő űrlaptípusok közül legalább egyet ki kell választani:

* webes űrlap;
* fájlfeltöltési űrlap; vagy
* API-űrlap külső kliensek, például a mobilalkalmazás általi hozzáféréshez.

.. TODO: Magyarázza el az egyes űrlaptípusok képességeit és korlátait,
   beleértve azt is, hogy egyszerre több típus engedélyezhető-e.

.. TODO: Dokumentálja az API-kliensek és mobilalkalmazások hitelesítési,
   verzióválasztási és kompatibilitási követelményeit.


Az űrlap leírása
................

Adja meg az űrlap rövid vagy részletes leírását. A leírás útmutatást
tartalmazhat a közreműködők számára.

.. TODO: Magyarázza el, hol jelenik meg a leírás a webes, fájlfeltöltési,
   API- és mobilfelületeken; támogatja-e a fordításokat vagy a jelölőnyelvet;
   és van-e maximális hossza.


Az űrlap SRID-je
................

Válassza ki az űrlapon beküldött adatok által használt térbeli
referencia-rendszert. A térbeli referencia-rendszerek a
https://spatialreference.org/ webhelyen kereshetők. Az alapértelmezett érték
az EPSG:4326 (WGS 84).

Ha meg van adva a térbeli referencia-rendszerek listája, a feltöltők csak a
felsorolt lehetőségek közül választhatnak. A listát vesszővel elválasztott
EPSG-azonosítókkal és látható címkékkel adja meg a következő formátumban:

.. code-block:: text

   4326:wgs84,23700:eov

.. TODO: Erősítse meg, hogy az űrlap SRID-je a feltöltő által megadott
   koordinátákat, a célgeometria-oszlop tárolási SRID-jét vagy mindkettőt
   leírja-e. Magyarázza el, mikor és hogyan történik a
   koordináta-transzformáció.

.. TODO: Dokumentálja, hogyan befolyásolja az űrlap SRID-je a WKT-geometriát,
   a szélességi és hosszúsági mezőket, az importált térbeli fájlokat, a webes
   térképen történő rajzolást és a mobilalkalmazás koordinátáit.

.. TODO: Erősítse meg az SRID-lista elfogadott szintaxisát és érvényesítését,
   beleértve azt, hogy támogatottak-e a szóközök, a lefordított címkék, a nem
   EPSG hatóságok és a kis- és nagybetűkre érzékeny címkék.


Űrlapok csoportosítása
......................

Az űrlapok csoportokba rendezhetők a webes űrlapválasztó felületen. Itt
határozhatók meg vagy választhatók ki a csoportnevek.

Ez a lehetőség jelenleg nem érhető el a mobilalkalmazásban.

.. TODO: Magyarázza el, hogyan hozhatók létre, rendezhetők, nevezhetők át,
   fordíthatók le és távolíthatók el az űrlapcsoportok. Tisztázza, hogy a
   csoportosítás befolyásolja-e a hozzáférést, vagy csak a megjelenítést.

.. TODO: Erősítse meg, hogy az űrlapok csoportosítása továbbra sem támogatott
   a mobilalkalmazás jelenlegi verziójában.


Az űrlap közzététele
....................

Egy űrlap zárolható az űrlap fejlécében található narancssárga közzétételi
gombbal történő közzététellel. Egy közzétett űrlap frissítése új verziót hoz
létre. A korábbi verziók továbbra is elérhetők maradnak az API-kliensek,
például a mobilalkalmazás számára.

Közzétett űrlapból tesztelési célú piszkozat hozható létre az oldal alján
található **Piszkozatverzió létrehozása** gombbal. Alapértelmezés szerint a
piszkozat csak a létrehozója számára érhető el. A piszkozat ezt követően
közzétehető az űrlap közzétett ágán.

.. TODO: Határozza meg az űrlapok teljes verziókezelési modelljét, beleértve
   a piszkozatokat, a közzétett verziókat, az ágakat, a verzióazonosítókat és
   az űrlap zárolásának jelentését.

.. TODO: Magyarázza el, hogy a közzététel azonnal hatályba lép-e, és a webes,
   fájlfeltöltési, API- és mobilkliensek hogyan választják ki vagy
   gyorsítótárazzák az űrlap verzióját.

.. TODO: Dokumentálja, ki tekinthet meg és tesztelhet egy piszkozatot, hogyan
   módosítható a piszkozathoz való hozzáférés, és létezhet-e egynél több
   piszkozat egy űrlaphoz.

.. TODO: Magyarázza el, hogyan hasonlíthatja össze az adminisztrátor a
   verziókat, hogyan állhat vissza egy korábbi verzióra, hogyan vezethet ki
   egy közzétett verziót, illetve hogyan kezelheti a régi verzióval beküldött
   adatokat.


Megfigyelési esemény beállításai
................................

A megfigyelési események magyarázatáért, valamint az alkalmi és az
eseményalapú megfigyelések közötti különbségekért lásd:
:doc:`Megfigyelési események és alkalmi megfigyelések <observation_events>`.

Egy megfigyelési eseményhez percben kifejezett időkorlát állítható be. A
korlát elérésekor a mobilalkalmazás figyelmezteti a felhasználót, hogy az idő
lejárt. A figyelmeztetés nem fejezi be az eseményt, és a felhasználó
folytathatja a megfigyelések rögzítését.

A **kötelező megfigyelési esemény** azt jelenti, hogy az űrlap csak
eseménymódban indítható el. Ha a megfigyelési események támogatása
engedélyezett, de nem kötelező, a felhasználó választhat az eseménymód és az
alkalmi megfigyelési mód között.

.. TODO: Dokumentálja a megfigyelési események összes beállítását, és
   magyarázza el, hogyan tárolódnak az eseményazonosítók, a kezdési és
   befejezési időpontok, a megosztott mezőértékek és az egyes megfigyelések.

.. TODO: Magyarázza el, hogy az időkorlát minden támogatott kliensben csak
   tájékoztató jellegű-e, és mi történik, ha az alkalmazás egy esemény közben
   offline állapotba kerül, felfüggesztik vagy újraindítják.

.. TODO: Erősítse meg a megfigyelési események engedélyezésére és kötelezővé
   tételére szolgáló beállítások jelenlegi feliratait, és nevezze meg, hogy
   mely beállításokat támogatja a webes felület, az API és a mobilalkalmazás.


.. _tracklog:

Útvonalnapló
............

Ez a lehetőség engedélyezi az útvonalnapló automatikus rögzítését az űrlap
használata közben. Az útvonalnapló rögzítése kötelező vagy választható lehet,
és csak eseménymódban érhető el.

.. TODO: Magyarázza el, milyen gyakran történik a helyadatok rögzítése,
   milyen helyhozzáférési jogosultságok szükségesek, és hogyan működik az
   offline rögzítés, a pontosság, az akkumulátorhasználat és a megszakított
   események kezelése.

.. TODO: Dokumentálja, hol tárolódnak az útvonalnaplók, kik férhetnek hozzájuk,
   hogyan kapcsolódnak az eseményekhez és megfigyelésekhez, valamint azt,
   hogy hozzáférési szabályaik eltérnek-e a beküldött rekordokétól.

.. TODO: Adjon hozzá adatvédelmi és biztonsági megjegyzést, amely elmagyarázza,
   hogy az útvonalnaplók felfedhetik egy közreműködő mozgását, ezért személyes
   vagy érzékeny adatnak minősülhetnek.


.. _periodic-notification:

Időszakos értesítés
...................

A megadott, percben kifejezett időközönként az alkalmazás emlékezteti a
megfigyelőt egy új megfigyelés rögzítésére. Az időzítő folyamatosan működik,
és minden alkalommal újraindul, amikor a felhasználó megfigyelést rögzít.

.. TODO: Erősítse meg, hogy az időszakos értesítések csak a
   mobilalkalmazásban érhetők-e el, és működnek-e, amikor az alkalmazás a
   háttérben fut.

.. TODO: Magyarázza el, mikor kezdődik az első időköz, mi történik az
   értesítés elutasításakor, és egy megfigyelés rögzítése vagy szerkesztése
   újraindítja-e az időzítőt.


Az űrlap oszlopainak meghatározása
----------------------------------

Az oszlopdefiníciós szakasz határozza meg, hogy a céltábla mely oszlopai
jelenjenek meg az űrlapon, valamint a beküldött értékek megjelenítésének és
érvényesítésének módját.

.. TODO: Magyarázza el, hogyan határozzák meg az adatbázisoszlopok metaadatai
   és adattípusai az űrlaposzlopok kezdeti beállításait.

.. TODO: Dokumentálja, hogy a céltábla oszlopainak módosításai hogyan érintik
   a meglévő piszkozat- és közzétett űrlapverziókat.


Tartalmazza
...........

Ha ki van választva, az oszlop megjelenik az űrlapon.

.. TODO: Magyarázza el, hogy egy nem tartalmazott oszlop kaphat-e
   alapértelmezett, generált vagy API-n keresztül megadott értéket.


Oszlopsorrend
.............

A **Tartalmazza** lehetőség melletti kis beviteli mező határozza meg az oszlop
űrlapon elfoglalt helyét. Alapértelmezés szerint üres.

.. TODO: Dokumentálja az elfogadott értékeket, a rendezés irányát, az azonos
   vagy hiányzó értékek kezelését, valamint azt, hogy a sorrend módosítható-e
   fogd és vidd művelettel.


Oszlop
......

Két név jelenik meg: az oszlop látható neve, amely az űrlapon szerkeszthető,
és az adatbázisoszlop eredeti neve.

.. TODO: Magyarázza el, hogy a látható név támogatja-e a ``str_`` fordítási
   kulcsokat, és hogyan jelenik meg a fájlsablonokban, az érvényesítési
   üzenetekben, az exportokban, az API-definíciókban és a mobilkliensekben.

.. TODO: Tisztázza, hogy a látható név módosítása csak az űrlapot érinti-e,
   vagy az adatbázis metaadatait is módosítja.


Kötelező
........

Három lehetőség érhető el: **igen**, **nem** és **enyhe hiba**.

``Igen`` (bordó)
   Az űrlap nem küldhető be érték nélkül ebben az oszlopban.

``Nem`` (szürke)
   Az űrlap akkor is beküldhető, ha ebben az oszlopban nincs érték.

``Enyhe hiba`` (rózsaszín)
   Az üres vagy egy korlátozásnak nem megfelelő értékek beküldhetők, de a
   feltöltőnek minden érintett sort meg kell erősítenie.

.. TODO: Magyarázza el, hogyan működik az enyhe hiba megerősítése a webes
   űrlapokban, fájlfeltöltésekben, API-kliensekben és a mobilalkalmazásban.

.. TODO: Dokumentálja, hogy az enyhe hiba megerősítése rögzül-e az
   adatbázisban vagy a feltöltés metaadataiban, és az adminisztrátorok meg
   tudják-e különböztetni a megerősített értékeket az érvényesítésen
   megfelelő értékektől.

.. TODO: Tisztázza, hogy az űrlapszintű kötelezőségi beállítások hogyan
   működnek együtt az adatbázis ``NOT NULL`` megszorításaival, az
   oszlopkapcsolatokkal és a rejtett vagy írásvédett mezőkkel.


Oszlopleírás
............

Adja meg a mező rövid leírását.

.. TODO: Magyarázza el, hol jelennek meg az oszlopleírások, támogatják-e a
   fordításokat vagy a jelölőnyelvet, és öröklik-e az adatbázisoszlopok
   megjegyzéseit.


Oszloptípus
...........

A következő űrlaposzlop-típusok érhetők el:

``text``
   Tetszőleges szöveg. A minimális és maximális hossz megadható.

``numeric``
   Numerikus érték. Minimális és maximális érték vagy hossz adható meg.

``list``
   Alapértelmezés szerint egyetlen elem kiválasztását lehetővé tevő
   legördülő lista.

``true-false``
   Logikai false/true érték. Az értékek sorrendje a listadefiníciós mezőben
   szabályozható, például ``false, true``.

``date``
   Dátum, amelyben az évet, hónapot és napot egy elfogadott karakter
   választja el. Adatbázisbeli dátumtípusként tárolódik.

``date and time``
   Dátum, amelyet szóköz, majd ``óra:perc:másodperc`` formátumú idő követ.
   Ha a másodperc hiányzik, az alkalmazás automatikusan ``00`` értékként
   kezeli, és kéri a feltöltőt a módosítás elfogadására. Ha a perc hiányzik,
   az alkalmazás szintén ``00`` értékként kezeli, és megerősítést kér. Az
   érték adatbázisbeli dátum-idő típusként tárolódik.

``time (timetominutes)``
   ``óra:perc`` formátumú érték, amelyet az alkalmazás egész számmá alakít.
   Adatbázisbeli egész szám típusként tárolódik.

``time``
   ``óra:perc`` formátumú érték, amely adatbázisbeli időtípusként tárolódik.

``time interval (timeinterval)``
   Időintervallum, például
   ``2014-02-25 12:00:00 2014-02-25 13:00:00``. Adatbázisbeli
   időintervallum-típusként tárolódik.

``autocomplete``
   Automatikus kiegészítési javaslatokat hoz létre a listadefiníciós mezőben
   megadott SQL-tábla oszlopából. A dokumentált rövidített szintaxis:
   ``table_name.column``. Alapértelmezés szerint a tábla keresése a
   ``gisdata`` adatbázis ``public`` sémájában történik.

``autocompletelist``
   Az ``autocomplete`` típushoz hasonló, de lehetővé teszi több automatikusan
   kiegészített érték megadását egy mezőben.

``photo id``
   Ha a fényképmodul engedélyezve van, az alkalmazás ebben a mezőben tárolja
   a feltöltött fényképek azonosítóit.

``geometry: point``
   WKT ``POINT(...)`` formában megadott pontgeometria.

``geometry: line``
   WKT ``LINESTRING(...)`` formában megadott vonalgeometria.

``geometry: polygon``
   WKT ``POLYGON(...)`` formában megadott poligongeometria.

``geometry: any``
   Támogatott geometriatípussal, WKT formában megadott geometria. Lásd
   `a példaűrlapot
   <https://openbiomaps.org/projects/checkitout/upload/?form=736&type=web>`_.

``colour rings``
   Színesgyűrű-kombináció megadását teszi lehetővé. A szögletes zárójelben
   lévő szakasz határozza meg a különböző lábrészekhez megadható gyűrűk
   maximális számát. Ezt követik az elérhető színek egyedi kódjai és címkéi,
   például ``[XX],Blue:B,red:R,green:G``.

   A dokumentált színkódok:

   * ``R`` — piros;
   * ``P`` — rózsaszín;
   * ``G`` — zöld;
   * ``g`` — világoszöld;
   * ``O`` — narancssárga;
   * ``Y`` — sárga;
   * ``B`` — kék;
   * ``b`` — világoskék;
   * ``W`` — fehér;
   * ``K`` — fekete;
   * ``N`` — barna;
   * ``U`` — bíbor;
   * ``V`` — ibolya; és
   * ``M`` — ezüst.

   Lásd `a színesgyűrű-űrlap példáját
   <https://openbiomaps.org/projects/checkitout/upload/?form=939&type=web>`_.

.. TODO: Erősítse meg az összes elérhető oszloptípus jelenlegi nevét, és
   rendelje hozzá az egyes űrlaptípusokat a szükséges PostgreSQL-adattípushoz.

.. TODO: Tisztázza, hogy a numerikus minimum- és maximumbeállítások a
   numerikus értékeket, a karakterhosszokat vagy mindkettőt korlátozzák-e.

.. TODO: Dokumentálja a dátum-, dátum-idő-, idő- és intervallummezők
   elfogadott beviteli formátumait, időzónáit, tartományait és tárolási
   típusait. A PostgreSQL nem rendelkezik ``datetime`` vagy ``timeinterval``
   nevű beépített típussal, ezért nevezze meg a pontosan használt
   adatbázistípusokat.

.. TODO: Erősítse meg a vonalmezőkben elfogadott pontos WKT-geometrianeveket.
   A szabványos WKT-geometriatípus a ``LINESTRING``, míg a forrásfelület a
   ``LINE`` címkét használhatja.

.. TODO: Dokumentálja, hogyan működnek együtt az űrlap geometriatípusai az
   űrlap SRID-jével, a céloszlop SRID-jével, a geometriagyűjteményekkel, a
   többrészes geometriákkal, a háromdimenziós koordinátákkal és az érvénytelen
   geometriákkal.

.. TODO: Magyarázza el az automatikus kiegészítés rövidített és JSON
   formátumát, a keresésekhez használt adatbázis-kapcsolatot, az alkalmazandó
   jogosultságokat, az eredménykorlátokat, az illesztés működését és az
   SQL-injektálás elleni védelmet.

.. TODO: Dokumentálja a ``photo id`` által használt tárolási formátumot és
   csatolmánykapcsolatot.

.. TODO: Ellenőrizze a ``colour rings`` típus szintaxisát, tárolási
   ábrázolását, a támogatott lábrészeket és a teljes színkészletet. Tisztázza,
   hogy a ``purple`` és a ``violet`` szándékosan különálló értékek-e.


Bevitelvezérlés
...............

A bevitelvezérlők ellenőrzik a mezőbe írt értékeket. A következő lehetőségek
érhetők el:

* nincs ellenőrzés;
* minimum és maximum;
* reguláris kifejezés;
* térbeli; és
* egyéni ellenőrzés.

.. TODO: Dokumentálja minden bevitelvezérlő konfigurációs szintaxisát és
   működését, beleértve a kliens- és kiszolgálóoldali érvényesítést.

.. TODO: Magyarázza el, hogy a minimum- és maximumkorlátozások az oszloptípustól
   függően hosszra, numerikus értékre, dátumra vagy más tulajdonságra
   vonatkoznak-e.

.. TODO: Dokumentálja a reguláris kifejezések dialektusát, határolójeleit,
   jelzőit, escape-szabályait, valamint azt, hogy a kifejezésnek a teljes
   értékre kell-e illeszkednie.

.. TODO: Magyarázza el az elérhető térbeli és egyéni ellenőrzéseket, és adjon
   hozzá tesztelt példákat. Nevezze meg, hol tárolódik az egyéni érvényesítési
   kód, és ki jogosult annak szerkesztésére.


Listadefiníció
..............

Ha listát szeretne használni az adatbeküldés során, állítsa az oszloptípust
``list``, ``autocomplete`` vagy ``autocompletelist`` értékre.

A listadefiníciók egyszerű vagy több választást lehetővé tevő listákat,
automatikus kiegészítési forrásokat, más adatbázistáblákból származó értékeket
és ezen értékek szűrésére szolgáló szabályokat írhatnak le.

Egy rövid lista közvetlenül is meghatározható. A következő példában a
feltöltők a ``female`` vagy ``male`` értéket választhatják ki egy legördülő
listából. A kiválasztott érték kerül az adatbázisba.

.. code-block:: json

   {
     "list": {
       "female": [],
       "male": []
     }
   }

Több beviteli címke is hozzárendelhető ugyanahhoz a tárolt értékhez. A ``F``,
``f`` és ``female`` például egyaránt értelmezhető a tárolt ``female``
értékként. Ez különösen hasznos fájlfeltöltés során, amikor a különböző
közreműködőktől vagy évekből származó adatok ugyanarra a fogalomra eltérő
címkéket használnak.

.. code-block:: json

   {
     "list": {
       "female": [
         "F",
         "f",
         "female"
       ],
       "male": [
         "M",
         "m",
         "male"
       ]
     }
   }

A lista egyszerű szöveges formátumban is megadható, soronként egy értékkel. Az
űrlap mentésekor az alkalmazás JSON formátumúvá alakítja az egyszerű szöveges
listát. Az így létrejött JSON ezután közvetlenül szerkeszthető.

.. TODO: Tisztázza, hogyan jelennek meg és illeszkednek a listakulcsok,
   címkék és álnevek. Dokumentálja a kis- és nagybetűk érzékenységét, a
   szóközök kezelését, az ismétlődő címkéket, az üres értékeket és a
   fordítások támogatását.

.. TODO: Magyarázza el, hogyan tárolódnak a többszörös kiválasztás és az
   ``autocompletelist`` értékei a céloszlopban, és mely
   PostgreSQL-oszloptípusok támogatottak.

A listaértékek SQL-táblából is származhatnak. Adja meg a sémát
(``optionsSchema``), a táblát (``optionsTable``), a tárolt értéket biztosító
oszlopot (``valueColumn``), valamint szükség esetén a látható címkét biztosító
oszlopot (``labelColumn``).

Az értékek a ``preFilterColumn`` és ``preFilterValue`` használatával
szűrhetők. A következő példa előszűrőket alkalmaz:

.. code-block:: json

   {
     "optionsTable": "milvus_taxon",
     "valueColumn": "word",
     "preFilterColumn": [
       "lang",
       "status"
     ],
     "preFilterValue": [
       "obm_taxon",
       [
         "accepted",
         "undefined"
       ]
     ],
     "orderBy": "taxon_db",
     "order": "desc"
   }

A teljes listadefiníció JSON formátumot használ. A webes felület
listaszerkesztőjével állítható össze, és az alkalmazás ellenőrzi a szintaxis
érvényességét. Ha a szintaxis érvénytelen, az alkalmazás hibaüzenetet ad
vissza.

A következő példa felsorolja a dokumentált tulajdonságokat:

.. code-block:: json

   {
     "list": {
       "val1": [
         "label1",
         "label2"
       ]
     },
     "optionsSchema": "e.g. public",
     "optionsTable": "a table name",
     "valueColumn": "a column from the table",
     "labelColumn": "a column from the table - optional",
     "filterColumn": "",
     "pictures": {
       "an element from the list, e.g. val1": "url-string"
     },
     "triggerTargetColumn": [
       ""
     ],
     "Function": "",
     "disabled": [
       "an element from the list, e.g. val1"
     ],
     "preFilterColumn": [
       ""
     ],
     "preFilterValue": [
       ""
     ],
     "preFilterRelation": [
       ""
     ],
     "multiselect": "true or false, default is false",
     "selected": [
       "an element from the list, e.g. val1"
     ],
     "size": "a numeric value",
     "orderBy": [
       "column or SQL expression"
     ],
     "order": [
       "ASC or DESC"
     ],
     "limit": "numeric value"
   }

.. TODO: Cserélje le a szemléltető teljes definíciót egy vagy több érvényes,
   végrehajtható példára. Az olyan helyőrző értékek, mint az ``e.g. public``
   és a karakterláncként megadott típusleírások nem másolhatók közvetlenül
   működő űrlapba.

.. TODO: Adjon meg referenciatáblázatot minden támogatott tulajdonsághoz,
   beleértve annak típusát, alapértelmezett értékét, engedélyezett értékeit,
   alkalmazható űrlaposzlop-típusait és támogatott klienseit.

.. TODO: Tisztázza, hogy a ``Function`` szándékosan megkülönbözteti-e a kis-
   és nagybetűket, miközben a többi tulajdonságnév kisbetűvel kezdődik.

.. TODO: Magyarázza el a ``labelAsValue``, ``filterColumn``, ``pictures``,
   ``disabled``, ``preFilterRelation``, ``multiselect``, ``selected``,
   ``size``, ``orderBy``, ``order`` és ``limit`` működését és elfogadott
   szintaxisát.

.. TODO: Erősítse meg, hogy az ``orderBy`` és az ``order`` karakterláncot és
   tömböt egyaránt elfogad-e. Az oldalon szereplő példák jelenleg mindkét
   formát bemutatják.

.. TODO: Dokumentálja, hogyan történik a tábla- és oszlopazonosítók, illetve
   az SQL-kifejezések érvényesítése. Különösen az ``orderBy`` és minden más,
   SQL-kifejezést tartalmazó tulajdonság biztonsági korlátozásait ismertesse.

.. TODO: Magyarázza el, hogy a listalekérdezések alkalmazzák-e a projekt sor-
   és oszlopszintű hozzáférési szabályait, és melyik adatbázis-felhasználó
   hajtja végre őket.


Kapcsolt listák
...............

Egy kapcsolt lista az egyik, indítóoszlopnak nevezett oszlopban kiválasztott
érték alapján határozza meg egy másik oszlop elérhető értékeit. Ez függő vagy
kaszkádlistát hoz létre.

Először hozzon létre egy keresőtáblát, amely tartalmazza a listaszintek
közötti kapcsolatokat. Egy ``animal_taxons`` tábla például leírhatná, hogy
mely állatcsoportok tartoznak az egyes főcsoportokhoz. A gerincesek közé
tartozhatnának a kétéltűek, hüllők, madarak és emlősök, míg a gerinctelenek
közé a csalánozók és rovarok.

Az indítóoszlop listadefiníciójában adja meg a céloszlopot:

.. code-block:: json

   {
     "triggerTargetColumn": [
       "affected_list_name"
     ],
     "Function": "select_list",
     "optionsSchema": "shared",
     "optionsTable": "animal_taxons",
     "valueColumn": "animal_group_name",
     "labelColumn": "animal_group_name",
     "labelAsValue": true
   }

A példában használt tulajdonságok:

``Function``
   A dokumentált ``select_list`` értéket használja.

``optionsSchema``
   Azonosítja a keresőtáblát tartalmazó sémát. Ez a példa a ``shared`` sémát
   használja.

``optionsTable``
   Azonosítja a keresőtáblát.

``valueColumn``
   Azonosítja az indítólista értékeit biztosító oszlopot.

``labelColumn``
   Azonosítja a látható címkéket biztosító oszlopot.

``triggerTargetColumn``
   Azonosítja azt az űrlaposzlopot, amelynek listáját frissíteni kell.

Az érintett oszlopban határozza meg, hogy a keresőtábla melyik oszlopa
biztosítja az értékeket, és melyik oszlop szolgál a szűrésükre:

.. code-block:: json

   {
     "optionsTable": "animal_taxons",
     "valueColumn": "animal_group_name",
     "labelColumn": "animal_group_name",
     "filterColumn": "animal_supergroup",
     "Function": "select_list",
     "optionsSchema": "shared"
   }

Itt a ``filterColumn`` azt a keresőtábla-oszlopot azonosítja, amelyet az előző
űrlaposzlopban kiválasztott értékkel kell összevetni.

A kapcsolt listák kettőnél több űrlaposzlopot is összekapcsolhatnak:

.. code-block:: json

   {
     "optionsSchema": "shared",
     "optionsTable": "animal_taxons",
     "filterColumn": "animal_supergroup",
     "Function": "select_list",
     "valueColumn": "animal_group_name",
     "triggerTargetColumn": [
       "species"
     ],
     "labelColumn": "animal_group_name"
   }

Kapcsolt listák láncában a ``triggerTargetColumn`` azonosítja a következő
űrlaposzlopot, a ``filterColumn`` az előző kiválasztással való összevetéshez
használt keresőtábla-oszlopot, a ``valueColumn`` és a ``labelColumn`` pedig az
aktuális listát határozza meg.

.. TODO: Ellenőrizze a ``valueColumn`` és ``labelColumn`` leírását az indító-
   és az érintett oszlopokban. Adjon hozzá példát egy keresőtáblára
   mintaadatokkal, hogy minden kapcsolat iránya egyértelmű legyen.

.. TODO: Magyarázza el, hogyan rendelődik hozzá az indító űrlaposzlop
   kiválasztott értéke a ``filterColumn`` oszlophoz, és az űrlaposzlop nevének
   meg kell-e egyeznie egy keresőtábla-oszlop nevével.

.. TODO: Dokumentálja, hogyan kezelik a kapcsolt listák az üres
   kiválasztásokat, a szülőérték módosítását, az ismétlődő lehetőségeket, a
   több szülőértéket, a többszörös kiválasztású mezőket, az automatikus
   kiegészítési mezőket és a két szintnél hosszabb láncokat.

.. TODO: Erősítse meg, hogy kapcsolt listák esetében az ``optionsSchema``
   értékének mindig ``shared``-nek kell-e lennie. Az oldalon később szereplő
   példák a ``public`` értéket használják, ami azt jelzi, hogy más sémák is
   támogatottak lehetnek.


Példa kapcsolt listára: épületek egy településen
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Tegyük fel, hogy egy projekt mesterséges költőládákban szaporodó fajokról
gyűjt adatokat. Egy ``tytoalba_buildings`` nevű keresőtábla rögzíti, hogy
melyik településen mely épületek találhatók. A településmezőnek automatikus
kiegészítési listát kell biztosítania, az épületmezőnek pedig csak a
kiválasztott település épületeit kell megjelenítenie.

Először állítsa be a településoszlopot automatikus kiegészítési mezőként, és
adja meg célként az épületoszlopot:

.. code-block:: json

   {
     "triggerTargetColumn": [
       "building"
     ],
     "Function": "select_list",
     "optionsSchema": "public",
     "optionsTable": "tytoalba_buildings",
     "valueColumn": "settlement"
   }

Ezután állítsa be az épületoszlopot listaként, és szűrje az értékeit a
kiválasztott település alapján:

.. code-block:: json

   {
     "optionsTable": "tytoalba_buildings",
     "filterColumn": "settlement",
     "Function": "select_list",
     "valueColumn": "building"
   }

.. TODO: Erősítse meg, hogy a második definíció örökli-e az
   ``optionsSchema`` értékét az indítóoszloptól, vagy az ``optionsSchema``
   véletlenül maradt ki.

.. TODO: Adjon hozzá példasorokat a ``tytoalba_buildings`` táblából, és
   mutassa meg a település kiválasztása után látható eredményt.


.. _default-values:

Alapértelmezett értékek
.......................

Egy mezőhöz előre meghatározott érték rendelhető. A dokumentált dinamikus
alapértelmezett értékek:

* ``_autocomplete``;
* ``_input``;
* ``_list``;
* ``_geometry``;
* ``_login_name``;
* ``_email``;
* ``_boolean``;
* ``_attacment``;
* ``_datum``; és
* ``_auto_geometry``.

Az ``_input`` például üres beviteli mezőt hoz létre, az ``_list`` a
listadefinícióval tölti ki a kiválasztási listát, az ``_geometry`` lehetővé
teszi a geometria kiválasztását, az ``_datum`` pedig dátumválasztást biztosít.

Lásd `a példaűrlapot
<https://openbiomaps.org/projects/checkitout/upload/?form=421&type=web>`_.

.. TODO: Erősítse meg a dinamikus alapértelmezett értékek teljes és aktuális
   listáját, és írja le mindegyik eredményét minden támogatott kliensben.

.. TODO: Ellenőrizze, hogy az ``_attacment`` kompatibilitási okokból
   szándékosan szerepel-e egy ``h`` betűvel, vagy elírásról van szó, amelyet
   ``_attachment`` értékre kell módosítani.

.. TODO: Ellenőrizze, hogy az ``_datum`` a jelenleg dokumentált azonosító-e,
   és magyarázza el, miben különbözik egy literális dátumtól vagy az aktuális
   dátumot megadó alapértelmezett értéktől.

.. TODO: Magyarázza el, hogyan határozhatók meg literális alapértelmezett
   értékek, és hogyan escape-elhetők az aláhúzásjellel kezdődő értékek.

.. TODO: Tisztázza, mikor történik az alapértelmezett értékek kiértékelése, a
   felhasználók felülírhatják-e őket, és hogyan működnek együtt a ragadós,
   rejtett, írásvédett és csak egyszer megjelenő mezőkkel.

.. TODO: Dokumentálja, hogy az ``_login_name`` és az ``_email`` mit ad
   hitelesítés nélküli beküldés esetén, és hogy ezek az értékek megbízható
   személyazonossági információnak tekinthetők-e.


.. _api-params:

Mezőmegjelenítési lehetőségek
.............................

A következő megjelenítési lehetőségek dokumentáltak:

``sticky``
   Elsősorban a mobilalkalmazás használja. Kiválasztásakor a mező megőrzi az
   értékét egy új sor megkezdésekor.

``hidden``
   A mező nem jelenik meg.

``read only``
   A mező értéke nem módosítható.

``once``
   A mobilalkalmazásban a mező csak egyszer jelenik meg egy megfigyelési
   listában, a megfigyelés végén.

   Ez a lehetőség arra szolgál, hogy egy mezőt a webes űrlap ismétlődő
   tábláján kívülre lehessen helyezni. Jelenleg a webes űrlapon hasonló
   eredmény érhető el egy alapértelmezett érték használatával.

``list elements as buttons``
   A lista elemeit gombokként jeleníti meg. A gombokon képek használhatók.
   A listadefinícióban minden listaelemhez meg kell adni képet.

``unfolding list``
   Fajlistás munkafolyamatot biztosít a mobilalkalmazásban. Ez a lehetőség
   csak automatikus kiegészítési mezővel – jellemzően tudományos nevet
   tartalmazó mezővel – használható, ha az űrlap tartalmaz egy egyedszámmezőt
   is, amelyhez az adatbázistábla beállításaiban hozzá van rendelve a
   megfelelő szemantikai szerep.

   A mobilalkalmazás listában jeleníti meg a kiválasztott fajneveket és
   egyedszámukat. Az egyedszámok módosíthatók anélkül, hogy minden módosítás
   után külön rekordot kellene menteni. A lehetőség ezért megfigyelési
   eseményhez tartozó űrlapon a leghasznosabb, ahol a **Megfigyelés mentése**
   köztes mentésként működik, és nem törli az összegyűjtött fajlistát.

A következő listadefiníció képeket társít a példában szereplő gombértékekhez:

.. code-block:: json

   {
     "pictures": {
       "animals": "http://....png",
       "plants": "http://....png",
       "mushrooms": "http://....png",
       "bats": "http://....png"
     }
   }

.. TODO: Erősítse meg, hogy ez a szakasz miért használja az ``api-params``
   hivatkozási címkét, és hogy ezek a lehetőségek API-paraméterekként vannak-e
   ábrázolva.

.. TODO: Dokumentálja, mely megjelenítési lehetőségek érhetők el a webes,
   fájlfeltöltési, API- és mobilkliensekben, és hogyan kezelik a nem támogatott
   lehetőségeket.

.. TODO: Magyarázza el, hogy a rejtett és írásvédett mezők módosíthatók-e
   közvetlen API-kéréssel vagy fájlfeltöltéssel. A megjelenítési korlátozások
   érvényesítés nélkül nem tekinthetők kiszolgálóoldali hozzáférés-vezérlésnek.

.. TODO: Határozza meg pontosan a ragadós érték hatókörét és életciklusát,
   beleértve az új megfigyeléseket, új eseményeket, űrlapmódosításokat, az
   alkalmazás újraindítását és az ugyanazt az eszközt használó különböző
   felhasználókat.

.. TODO: Tisztázza az ``once`` lehetőség jelenlegi megvalósítását és
   tervezett webesűrlap-működését.

.. TODO: Magyarázza el a képek URL-jeire vonatkozó követelményeket, a
   támogatott formátumokat, a gyorsítótárazást, a hitelesítést, a helyettesítő
   szöveget és a kép elérhetetlensége esetén tapasztalható működést. Cserélje
   le a ``http://....png`` helyőrzőket biztonságos, működő példákra.

.. TODO: Dokumentálja, hogyan azonosítja az unfolding list az egyedszámmezőt,
   és hogyan tárolja, frissíti és érvényesíti az így létrejövő
   megfigyeléseket.


Oszlopkapcsolatok
.................

Az oszlopkapcsolatok az egyik mező értéke alapján ellenőrzik vagy módosítják
egy másik mező értékét. Egy tömegmező például 20 és 30 közötti numerikus
tartományra korlátozható, amikor a nem mező értéke ``female``:

.. code-block:: text

   (sex=female) {minmax(20:30)}

Lásd `a példaűrlapot
<https://openbiomaps.org/projects/checkitout/upload/?form=938&type=web>`_.

.. TODO: Magyarázza el, hol konfigurálhatók a kapcsolatok az adminisztrációs
   felületen, és hogy egy kapcsolat az ellenőrzött vagy az azt kiváltó mezőhöz
   tartozik-e.

.. TODO: Dokumentálja, mikor történik a kapcsolatok kiértékelése webes
   űrlapokban, fájlfeltöltésekben, API-kérésekben és mobilalkalmazásokban,
   valamint azt, hogy az érvényesítés megismétlődik-e a kiszolgálón.

.. TODO: Magyarázza el, hogyan kapcsolódik össze több kapcsolat, hogyan
   oldódnak fel az ütközések, és számít-e a kiértékelés sorrendje.


Pszeudooszlopok
...............

Más feltöltési űrlapok oszlopai a következő formátumban adhatók hozzá:

.. code-block:: text

   form-name:column1,column2,columnN

A felsorolt oszlopok az ezt a definíciót tartalmazó oszlop után jelennek meg.
A pszeudooszlopokba írt értékek feltöltése a másik űrlap definíciójával
történik. Ez lehetővé teszi, hogy egyetlen munkafolyamatban két táblába
kerüljenek adatok.

.. TODO: Magyarázza el, hol kell megadni a pszeudooszlop definícióját, és
   adjon teljes példát két űrlappal és két kapcsolódó céltáblával.

.. TODO: Dokumentálja, hogyan kapcsolódnak, rendeződnek, érvényesítődnek,
   véglegesítődnek és vonódnak vissza a két űrlapon keresztül írt rekordok.
   Tisztázza, mi történik, ha az egyik beszúrás sikeres, a másik pedig
   sikertelen.

.. TODO: Magyarázza el, hogy a pszeudooszlopok támogatják-e a beágyazott
   pszeudoűrlapokat, csatolmányokat, geometriát, hozzáférési szabályokat,
   közzétett űrlapverziókat, fájlfeltöltéseket, API-kat és
   mobilalkalmazásokat.

.. TODO: Tisztázza, hogyan történik a névütközések és a hivatkozott űrlap
   kötelező mezőinek kezelése.


A kapcsolatok nyelvének meghatározása
-------------------------------------

A kapcsolatok nyelvének dokumentált általános szintaxisa:

.. code-block:: text

   (rel_field=rel_statement) {rel_type(rel_value)}, (rel_field=rel_statement) {rel_type(rel_value)}, ...

A tervezett értelmezés:

.. code-block:: text

   IF another field (rel_field) matches rel_statement,
   THEN apply rel_type with rel_value to the current field.

A ``rel_type`` az aktuális mezőtípushoz kapcsolódó függvény. A dokumentált
függvények:

``year``
   Dátummezők esetében kinyeri az évet egy dátum-karakterláncból.

``minmax``
   Szöveges vagy numerikus mezők esetében minimum- és maximumtartományt
   ellenőriz.

``obligatory``
   Bármely mezőtípus esetében módosítja, hogy az aktuális mező kötelező-e.

``inequality``
   Bármely mezőtípus esetében egy támogatott összehasonlító operátorral
   összehasonlítja a kapcsolódó mezőt az aktuális mezővel. A sikertelen
   összehasonlítás érvényesítési hibát eredményez.

A reguláris kifejezésből álló utasítás ``!!`` karakterekkel kezdődik, amelyet
reguláris kifejezés követ, például:

.. code-block:: text

   !!^(\d{2})$

Ha a ``rel_statement`` reguláris kifejezés, a ``rel_value`` az illeszkedő
értéken alapuló helyettesítő függvényt használhat:

``.``
   Az aktuális mező értékét a ``rel_field`` mezőben illeszkedő karakterláncra
   cseréli.

``.+``
   Az aktuális mező értékét a ``rel_field`` mezőben illeszkedő
   karakterlánchoz fűzi.

``+.``
   A ``rel_field`` mezőben illeszkedő karakterláncot az aktuális mező
   értékéhez fűzi.

``inequality`` kapcsolat esetében a dokumentált kifejezések ``+`` karakterrel
jelölik a ``rel_field`` illeszkedő értékét, és ``.`` karakterrel az aktuális
mező értékét:

.. code-block:: text

   +<.
   +<=.
   +>=.
   +=.
   +<>.

Más kapcsolattípusok esetében a ``rel_value`` más értéket tartalmazhat, vagy a
függvénytől függően figyelmen kívül maradhat.

.. TODO: Ellenőrizze a fent bemutatott formális nyelvtant a jelenlegi
   elemzővel. Az eredeti leírás a ``rel_type=rel_value`` és a
   ``rel_type(rel_value)`` jelölést egyaránt használta, miközben minden példa
   az utóbbit használja.

.. TODO: Adja meg a támogatott kapcsolati függvények teljes listáját, valamint
   mindegyik mezőtípusait, argumentumait, visszatérési értékeit és
   hibakezelését. Az alábbi példák használják a ``set`` függvényt, de az nem
   szerepel a dokumentált függvények listájában.

.. TODO: Dokumentálja az escape-elési és idézési szabályokat a szóközt,
   vesszőt, zárójelet, kapcsos zárójelet, egyenlőségjelet, nem ASCII
   karaktereket vagy reguláriskifejezés-meta-karaktereket tartalmazó
   mezőnevekhez és értékekhez.

.. TODO: Erősítse meg a támogatott reguláriskifejezés-motort, és magyarázza
   el a rögzítőcsoportokat, a helyettesítési szintaxist, a határolójeleket, a
   módosítókat, a Unicode-kezelést és az érvénytelen kifejezések kezelését.

.. TODO: Tisztázza a ``.``, ``.+`` és ``+.`` helyettesítő operátorok
   jelentését, és adjon tesztelt példákat az eredményül kapott értékekkel.

.. TODO: Erősítse meg, hogy a ``<>`` jelentése „nem egyenlő”-e, és hogy a
   ``!=`` is támogatott-e.

.. TODO: Magyarázza el, hogyan történik a dátumok, numerikus karakterláncok,
   null értékek és területi beállítástól függő tizedeselválasztók
   összehasonlítása.


Kapcsolati példák
.................

Mező kötelezővé tétele
~~~~~~~~~~~~~~~~~~~~~~

A ``tarsus_length`` oszlopon:

.. code-block:: text

   (clutch_size=!!^([123])$) {obligatory(1)}

Ez kötelezővé teszi a ``tarsus_length`` mezőt, ha a ``clutch_size`` értéke
``1``, ``2`` vagy ``3``.

.. TODO: Erősítse meg, hogy a reguláris kifejezés szándékosan csak egy
   karakterből álló értékeket engedélyez-e, és hogy a ``clutch_size`` szövegként
   vagy számként van-e kezelve.


Két dátum összehasonlítása
~~~~~~~~~~~~~~~~~~~~~~~~~~

Az ``end_date`` oszlopon:

.. code-block:: text

   (found_date=!!^(.+)$) {inequality(+>=.)}

Ha a ``found_date`` nem üres, a kapcsolat ellenőrzi, hogy az ``end_date``
nagyobb vagy egyenlő-e a ``found_date`` értékénél. A hamis eredmény
feltöltési hibát okoz.

.. TODO: Ellenőrizze az összehasonlítás irányát. A dokumentált helyőrzők
   szerint a ``+>=.`` látszólag azt jelenti, hogy
   ``found_date >= end_date``, ami ellentmond a kapcsolódó leírásnak, amely
   szerint az ``end_date`` értékének nagyobbnak vagy egyenlőnek kell lennie a
   ``found_date`` értékénél. A példát csak az elemző tesztelése után cserélje
   le.


Év hozzáadása egy dátumhoz
~~~~~~~~~~~~~~~~~~~~~~~~~~

Egy évet nem tartalmazó dátummezőn:

.. code-block:: text

   (year=!!^(d{4})$) {set(.)}

Ha a ``year`` oszlop nem üres, és négy számjegyet tartalmaz, a dátummező ezzel
az évvel frissül.

.. TODO: Ellenőrizze ezt a példát. A négy számjegyre illeszkedő reguláris
   kifejezés hagyományosan ``\d{4}`` lenne, a dokumentált kifejezés azonban
   ``d{4}``. Erősítse meg, hogy a fordított perjel nem a dokumentáció
   formázása során veszett-e el.

.. TODO: Magyarázza el, hogyan egyesíti a ``set(.)`` az évet a meglévő
   dátumértékkel. A jelenlegi példa nem adja meg egyértelműen a bemeneti
   formátumot vagy az eredményül kapott értéket.


Gyűrűszám megkövetelése
~~~~~~~~~~~~~~~~~~~~~~~

A ``ring_number`` mezőn:

.. code-block:: text

   (recapture=1) {obligatory(1)}

Ha a ``recapture`` értéke ``1``, a ``ring_number`` kötelezővé válik.


Alternatív név megkövetelése
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Az ``english_name`` oszlopon:

.. code-block:: text

   (scientific_name=!!(^$)) {obligatory(1)}

Ha a ``scientific_name`` üres, az ``english_name`` kötelezővé válik.

.. TODO: Erősítse meg, hogy a ``^$`` körüli zárójelek kötelezők-e, vagy csak
   rögzítőcsoportot hoznak létre.


Érték beállítása egy darabszám alapján
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Az ``amount_type`` mezőn:

.. code-block:: text

   (number_of_individuals>50) {set(estimated value)},(egyedszam<=50) {set(exact value)}

Ha az egyedek száma nagyobb 50-nél, az ``amount_type`` értéke ``estimated
value`` lesz. Ha az érték legfeljebb 50, az ``amount_type`` értéke ``exact
value`` lesz.

.. TODO: Ellenőrizze a feltételes szintaxist. Az általános nyelvtan a
   ``rel_field=rel_statement`` formát dokumentálja, ez a példa azonban ``>``
   és ``<=`` jelet helyez a mező és az érték közé.

.. TODO: Erősítse meg, hogy az ``egyedszam`` helyett
   ``number_of_individuals`` értéknek kellene-e szerepelnie. A példa jelenleg
   eltérő mezőneveket használ a két ágban.

.. TODO: Magyarázza el, hogy a szóközt tartalmazó értékeket, például az
   ``estimated value`` értéket idézőjelek közé kell-e tenni vagy escape-elni
   kell-e.

.. TODO: Adjon tesztelt példákat a ``minmax`` és ``year`` használatára, a
   reguláriskifejezés-helyettesítésre, egy mező több feltételére, valamint
   üres vagy null értékeket tartalmazó kapcsolatokra.
