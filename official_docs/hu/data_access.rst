Adathozzáférés
**************

Az OpenBioMaps többféle lehetőséget biztosít a projektadatok lekérdezésére,
megtekintésére és letöltésére. Az ezeken a felületeken elérhető rekordok és
mezők köre a projekt hozzáférési szabályaitól és az aktuális felhasználó
jogosultságaitól függ.

Ez az oldal áttekintést nyújt az elérhető adatlekérési módszerekről és a
projektadatokhoz való hozzáférés szabályozására szolgáló mechanizmusokról.


Adatok lekérése
===============

Az adatok lekérhetők a webalkalmazáson keresztül, letölthetők a támogatott
fájlformátumokban, vagy külső alkalmazásokból is elérhetők.


Fájlok letöltése
----------------

A lekérdezési eredmények különféle formátumokban tölthetők le. A
projektmodul beállításaitól függően az elérhető formátumok a következők
lehetnek:

* szöveges és strukturált adatok: CSV és JSON;
* táblázatok: ODS, XLS és XLSX;
* szöveges attribútumokkal rendelkező térbeli adatok: ESRI Shapefile, KML,
  GPX és SQLite.

Az ESRI Shapefile-export több kapcsolódó fájlból is állhat, beleértve a
``.shp``, ``.dbf``, ``.cpg``, ``.prj`` és ``.shx`` fájlokat.

A felhasználók egyenként tölthetik le az adatrekordokhoz kapcsolódó képeket,
míg a projektadminisztrátorok az adminisztrációs felületen keresztül
tömegesen is letölthetik azokat.

Az adminisztrátorok az adatbázistáblák kezelési oldalán CSV-formátumban
exportálhatják az adattáblák szöveges mezőit.

Az adatexport az Export modul használatával egyedi engedélykérelmekhez is
köthető.


Webes lekérdezések
------------------

A webalkalmazás eszközöket biztosít a hozzáférhető rekordok szűréséhez és
lekéréséhez. A projekt konfigurációjától függően a felhasználók a
következőket hajthatják végre:

* attribútumalapú lekérdezések szöveges, lista-, dátum- és más konfigurált
  mezők használatával;
* térbeli lekérdezések a térképen kijelölt vagy megrajzolt geometriák
  használatával; vagy
* kombinált térbeli és attribútumalapú lekérdezések.

A lekérdezési felületek áttekintését lásd:
:doc:`Felhasználói felületek <user_interface>`.

.. TODO: Dokumentálni kell, hogyan tekinthetők meg, pontosíthatók,
   menthetők, hivatkozhatók és exportálhatók a lekérdezési eredmények.
   Azt is tisztázni kell, hogy minden projekt támogatja-e a kombinált
   térbeli és attribútumalapú lekérdezéseket.


Külső alkalmazások
------------------

A projektadatok külső alkalmazásokból is elérhetők:

* az OpenBioMaps API parancsfájlokból, az OpenBioMaps R-csomagból és más
  API-kliensekből használható;
* egy engedélyezett SQL-kapcsolat közvetlen adatbázis-hozzáférést
  biztosíthat olyan alkalmazások számára, mint a QGIS; valamint
* a támogatott kliensalkalmazások saját lekérdezési és letöltési
  felületeket biztosíthatnak.

A külső alkalmazásokból történő hozzáférésre a projekt hozzáférési
szabályai, valamint a hitelesített felhasználóhoz vagy kapcsolathoz rendelt
jogosultságok vonatkoznak.

További információért lásd:

* :doc:`OpenBioMaps API <api>`; valamint
* :doc:`Kliensalkalmazások <clients>`.


Az adatokhoz való hozzáférés szabályozása
=========================================

Az OpenBioMaps több szinten képes szabályozni a hozzáférést:

* a projektszintű beállítások határozzák meg az alapértelmezett hozzáférési
  és módosítási szabályzatot;
* a sorszintű szabályok az egyes rekordokhoz való hozzáférést szabályozzák;
  valamint
* az oszlopszintű szabályok határozzák meg, hogy mely mezők tekinthetők meg
  vagy tölthetők le.

A tényleges jogosultságok ezért több beállítástól is függhetnek. A
projektadminisztrátoroknak különböző csoportokhoz tartozó felhasználókkal,
valamint hitelesítés nélkül is tesztelniük kell az így kialakuló
hozzáférést, ha a nyilvános hozzáférés engedélyezett.

.. TODO: Teljes jogosultság-kiértékelési modellt kell készíteni, amely
   bemutatja a projekt-, sor- és oszlopszintű, valamint a felhasználói
   csoportokhoz kapcsolódó szabályok pontos elsőbbségi sorrendjét és
   kölcsönhatását.


Projektszintű hozzáférés
------------------------

Az alapértelmezett projektszintű hozzáférési beállításokat a
``local_vars.php.inc`` konfigurációs fájl határozza meg:

.. code-block:: php

   define('ACC_LEVEL', 'group'); // Can be set to 'public' or 'login'.
   define('MOD_LEVEL', 'group');

Az ``ACC_LEVEL`` azt az alapértelmezett szintet határozza meg, amelyen a
projektadatok elérhetők. A dokumentált értékek a következők:

``public``
   Az adatok nyilvánosan hozzáférhetők, az esetleges részletesebb
   hozzáférési szabályok figyelembevételével.

``login``
   Az adatok a hitelesített felhasználók számára hozzáférhetők, az
   esetleges részletesebb hozzáférési szabályok figyelembevételével.

``group``
   A hozzáférést a projektcsoportok és további hozzáférési szabályok
   szabályozzák.

A ``MOD_LEVEL`` azt az alapértelmezett szintet határozza meg, amelyen az
adatok módosíthatók. Hasonló hozzáférési modellt használ.

Ha a ``MOD_LEVEL`` értéke ``public``, az adatok a felhasználó
bejelentkezése nélkül is módosíthatók. Ez a beállítás kizárólag akkor
használható, ha kifejezetten szükség van hitelesítés nélküli módosításra,
és annak biztonsági következményeit mérlegelték.

.. TODO: Ellenőrizni kell az ``ACC_LEVEL`` és a ``MOD_LEVEL`` összes
   érvényes értékét, és dokumentálni kell pontos működésüket. Különösen
   azt kell tisztázni, hogy miben különbözik a ``login`` a ``group``
   értéktől, és támogatottak-e további értékek.

.. TODO: Ismertetni kell, hogy ezek az állandók a teljes projektre
   vonatkoznak-e, hogyan lépnek életbe a konfigurációs változtatások,
   valamint kezelhetők-e a projektadminisztrációs felületen.


Sorszintű hozzáférés
--------------------

Ha az ``ACC_LEVEL`` vagy a ``MOD_LEVEL`` értéke ``group``, az egyes
rekordokhoz való hozzáférés egy projektspecifikus ``*_rules`` táblával
szabályozható. A ``*`` a projekt által használt nevet vagy előtagot jelöli.

Egy szabálytábla egy adattáblához kapcsolódik. Az adatrekordot az
adattáblában található ``obm_id`` érték és a szabálytáblában található
``row_id`` érték kapcsolja össze a megfelelő szabállyal.

Csoportszintű hozzáférést használó projektben azok a rekordok, amelyekhez
nem tartozik bejegyzés a szabálytáblában, kizárólag a projektgazdák számára
érhetők el.

.. TODO: Ellenőrizni kell, hogy egy adatrekordhoz pontosan egy vagy több
   szabálytáblabeli sor tartozhat-e. Azt is meg kell erősíteni, hogy a
   „projektgazda” annak a szerepkörnek a jelenlegi neve-e, amely hozzáférhet
   a szabállyal nem rendelkező rekordokhoz.

A szabálytábla működése a projektadminisztrációs felületen, a
**Project administration > Functions > Create access rules** menüpontban
konfigurálható. Ezen a felületen létrehozható vagy frissíthető a
triggerfüggvény, valamint engedélyezhető vagy letiltható annak működése.

Ha engedélyezve van, a trigger a rekordok létrehozása, módosítása vagy
törlése után karbantartja a szabálytáblát.

.. TODO: Ellenőrizni kell a hozzáférési szabályok adminisztrációs
   felületének aktuális elnevezéseit és helyét. Dokumentálni kell, mi
   történik a meglévő szabályokkal a trigger letiltásakor, újbóli
   létrehozásakor vagy módosításakor.


Olvasási és írási csoportok hozzárendelése
------------------------------------------

Az egyes rekordok olvasási és írási jogosultságai a szabálytábla
csoportokhoz kapcsolódó mezőivel rendelhetők hozzá.

Ezeket az értékeket a szabálytábla triggere automatikusan is kitöltheti. A
hozzárendelt csoportok származhatnak a rekord létrehozásához használt
feltöltési űrlap hozzáférési beállításaiból. A befejezett feltöltésekre,
valamint azok konfigurált tulajdonosi és csoportértékeire vonatkozó
információkat a ``system.uploadings`` tábla tárolja.

.. TODO: Dokumentálni kell a szabálytábla ``read`` és ``write`` mezőinek
   adattípusait és elfogadott értékeit. Tisztázni kell, hogy egyetlen
   csoportot, több csoportot, felhasználói azonosítókat vagy ezek
   kombinációját tartalmazzák-e.

.. TODO: Ismertetni kell, hogyan kerülnek át a feltöltési űrlap hozzáférési
   beállításai a ``system.uploadings`` táblába, majd onnan a
   szabálytáblába. Dokumentálni kell a nem feltöltési űrlapon, hanem például
   SQL vagy az API használatával létrehozott rekordok kezelését is.


Szabálytábla újragenerálása
---------------------------

A szabálytábla manuálisan is újragenerálható. A következő példákban az
``abc`` az adattábla, az ``abc_rules`` pedig annak szabálytáblája.

A következő utasítások olvasási vagy írási csoportok hozzárendelése nélkül
hozzák létre újból a szabályokat:

.. code-block:: sql

   DELETE FROM abc_rules
   WHERE data_table = 'abc';

   INSERT INTO abc_rules (row_id, sensitivity, data_table)
   SELECT obm_id, 'sensitive', 'abc'
   FROM abc;

A következő utasítások a ``system.uploadings`` tábla megfelelő
bejegyzéséből származtatják a csoport- és tulajdonosértékeket:

.. code-block:: sql

   DELETE FROM abc_rules
   WHERE data_table = 'abc';

   INSERT INTO abc_rules (row_id, sensitivity, data_table, read, write)
   SELECT a.obm_id, 'sensitive', 'abc', s."group", s.owner
   FROM abc AS a
   LEFT JOIN system.uploadings AS s
       ON s.id = a.obm_uploading_id;

Ezeket a példákat a projekt tényleges táblaneveihez, sémájához,
oszloptípusaihoz és hozzáférési szabályzatához kell igazítani. Az
adminisztrátoroknak éles adatbázisban történő használat előtt biztonsági
másolatot kell készíteniük a meglévő szabálytábláról, és ellenőrizniük kell
a létrehozott jogosultságokat.

.. TODO: Ellenőrizni kell, hogy a példákban szereplő oszlopnevek és
   értéktípusok megfelelnek-e a jelenlegi sémának. Különösen a
   ``sensitivity``, ``read``, ``write``, ``system.uploadings.group`` és
   ``system.uploadings.owner`` típusát kell ellenőrizni.

.. TODO: Ismertetni kell, hogy a szabálytábla törlése és újraépítése
   átmenetileg hozzáférhetővé vagy elérhetetlenné teheti-e az adatokat,
   a műveletet tranzakción belül kell-e végrehajtani, valamint létezik-e
   olyan adminisztrációs parancs, amely biztonságosan elvégzi ugyanezt a
   feladatot.


Érzékenységi beállítások
------------------------

A szabálytábla ``sensitivity`` mezője befolyásolja egy rekord nyilvános
elérhetőségét a csoportszintű hozzáférést használó projektekben.

A dokumentált értékek a következők:

``sensitive``
   A rekordot kizárólag a vonatkozó hozzáférési szabályokban megadott
   csoportok tagjai olvashatják vagy módosíthatják.

``restricted``
   Ez az érték a jelenlegi dokumentáció szerint ugyanazt jelenti, mint a
   ``sensitive``.

``no-geom``
   A rekord nyilvánosan hozzáférhető lehet, de a geometriája nyilvánosan
   nem jelenik meg.

``only-owner``
   A rekordhoz kizárólag a projekt tulajdonosa férhet hozzá.

.. TODO: Ellenőrizni kell az elfogadott ``sensitivity`` értékek teljes
   listáját, és meg kell határozni a rekordok megtekintésére,
   lekérdezésére, letöltésére és módosítására gyakorolt pontos hatásukat.

.. TODO: Tisztázni kell, hogy a ``restricted`` és a ``sensitive`` valóban
   egymás megfelelői-e, vagy egyes felületeken eltérően működnek. A
   ``no-geom`` esetében ismertetni kell, hogy a geometria eltávolításra,
   általánosításra vagy helyettesítésre kerül-e, vagy csupán nem jelenik
   meg a térképen. Azt is meg kell határozni, mely felhasználó tekintendő
   az ``only-owner`` rekordok tulajdonosának.


Oszlopszintű hozzáférés
-----------------------

Az egyes adatbázismezőkhöz való hozzáférés tovább szabályozható az
``allowed_columns`` modul használatával. Ez a modul határozza meg, hogy a
nyilvános felhasználók vagy a megadott felhasználói csoportok mely
oszlopokat tekinthetik meg vagy tölthetik le.

Olyan projektben, amelyben az ``ACC_LEVEL`` értéke ``group``, a modul
segítségével kiválasztott mezők akkor is hozzáférhetővé tehetők, ha a
projekt egyébként nem biztosít általános hozzáférést minden mezőhöz. A
sorszintű szabályok alapján hozzáférhető rekordok látható mezőit is
korlátozhatja.

Ez lehetővé teszi például annak közlését a felhasználókkal, hogy egy rekord
létezik, miközben csak annak jóváhagyott mezői válnak hozzáférhetővé.

.. TODO: Dokumentálni kell, hogyan engedélyezhető és konfigurálható az
   ``allowed_columns`` modul, szabályozza-e a lekérdezéseket is a
   megjelenített és letöltött eredmények mellett, valamint hogyan kezeli a
   geometriaoszlopokat.

.. TODO: Ellenőrizni kell, hogy az ``allowed_columns`` hozzáférhetővé
   tehet-e nyilvánosan mezőket akkor, ha a rekordhoz nem tartozik
   szabálytáblabeli bejegyzés. Ez biztonsági szempontból érzékeny
   kölcsönhatás, ezért konkrét példákkal kell ismertetni.


A hozzáférési szabályok kölcsönhatása
-------------------------------------

Ha kizárólag csoportszintű projekthozzáférés van beállítva, és ennél
részletesebb szabályok nem biztosítanak hozzáférést, a projektadatok
kizárólag az ilyen korlátozások megkerülésére jogosult adminisztratív
szerepkör számára érhetők el.

A szabálytábla sorszintű szabályozást biztosít, így különböző rekordok
különböző csoportok számára tehetők hozzáférhetővé. Az
``allowed_columns`` modul oszlopszintű szabályozást biztosít, így egy
hozzáférhető rekordnak csak a kiválasztott mezői tekinthetők meg vagy
tölthetők le.

Ha több szabály is alkalmazandó, a tényleges jogosultságokat a projekt-,
sor- és oszlopszintű korlátozások együttesen határozzák meg. Az
adminisztrátoroknak nem szabad abból kiindulniuk, hogy egy általánosabb
szabály automatikusan felülír egy részletesebb korlátozást.

.. TODO: Ezt az általános leírást az OpenBioMaps által megvalósított pontos
   hozzáférés-feloldási algoritmussal kell helyettesíteni. Példákat kell
   adni a nyilvános, hitelesített, csoport-, tulajdonosi, sor- és
   oszlopszintű hozzáférésre, valamint az egymással ütköző olvasási és írási
   jogosultságokra.
