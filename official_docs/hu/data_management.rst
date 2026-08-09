:author: Miklós Bán
:date: 2026-08-08


Adatkezelés
***********

Az OpenBioMaps rendszerben az adatkezelés a biodiverzitási adatok teljes
életciklusa során végzett rendszerezési, dokumentálási, validálási,
karbantartási, feldolgozási és újrafelhasználási folyamatokat foglalja
magában.

A cél annak biztosítása, hogy az adatok az eredeti adatgyűjtési
tevékenységet követően is érthetők, megbízhatók, visszakövethetők és
használhatók maradjanak.

Az OpenBioMaps eszközöket biztosít mind az adatok szerkezetének, mind azoknak
a folyamatoknak a kezeléséhez, amelyek során az adatokat gyűjtik,
ellenőrzik, átalakítják, lekérdezik és felhasználják.

Az adatbázis szerkezete és a metaadatok
=======================================

Az OpenBioMaps az adatokat önálló fájlok vagy táblázatok helyett
strukturált adatbázistáblákban tárolja.

Az adatbázis szerkezete határozza meg, milyen típusú információk tárolhatók,
és hogyan kapcsolódnak egymáshoz a különböző információtípusok.

A táblákhoz és mezőkhöz metaadatok kapcsolhatók, amelyek leírják azok
jelentését, tartalmát és tervezett felhasználását. A megfelelő metaadatok
elengedhetetlenek az adatok megértéséhez és újrafelhasználásához, különösen
akkor, ha egy projektet hosszú időn keresztül vagy több személy tart karban.

:ref:`Adminisztrációs beállítások: Adatbázisoszlopok <database-columns>`

Adatminőség és validálás
========================

Az adatminőség javítható az adatok rendszerbe kerüléskor történő
ellenőrzésével, valamint az adatkezelés során alkalmazott validálási
szabályokkal.

A projekt konfigurációjától függően az OpenBioMaps ellenőrizheti az
értékeket, a kötelező mezőket, az adatok közötti kapcsolatokat, a térbeli
információkat és más projektspecifikus korlátozásokat.

A validálás az adatrögzítés vagy adatfeltöltés során, valamint a későbbi
adatfeldolgozás részeként is elvégezhető.

* :doc:`Háttérfolyamatok <../jobs>`
* :doc:`Modulok <../modules>`

Adatfeldolgozás és harmonizáció
===============================

A különböző forrásokból gyűjtött adatok eltérő formátumokat,
terminológiát, taxonómiákat, koordináta-rendszereket vagy más
konvenciókat használhatnak.

Az OpenBioMaps olyan munkafolyamatok részeként használható, amelyek az
eredeti információ megőrzése és a feldolgozási lépések dokumentálása
mellett harmonizálják és átalakítják az adatokat.

Az adatfeldolgozás magában foglalhatja az értékek szabványosítását, a
térbeli adatok átalakítását, a taxonnevek feloldását, adatkészletek
egyesítését, illetve az adatok elemzésre és közzétételre történő
előkészítését.

Az adatok származása és dokumentálása
=====================================

A megbízható biodiverzitási adatokhoz a rögzített megfigyelés önmagában nem
elegendő. Fontos megőrizni azt is, hogy a megfigyelést mikor, hol, hogyan
és ki gyűjtötte, valamint hogyan dolgozták fel később az adatokat.

Az OpenBioMaps strukturált mezők, metaadatok, lekérdezések és
projektspecifikus munkafolyamatok segítségével támogatja az adatgyűjtési és
adatkezelési folyamatok dokumentálását.

Ezen információk adatokkal együtt történő megőrzése javítja a
visszakövethetőséget, és lehetővé teszi a későbbi ellenőrzést és
újrafelhasználást.

Lekérdezések és származtatott adatok
====================================

A lekérdezések az eredeti rekordok módosítása nélkül használhatók adatok
kiválasztására, szűrésére, összekapcsolására és átalakítására.

Ez lehetővé teszi az adatok projektspecifikus nézeteinek létrehozását
különböző célokra, például elemzéshez, jelentéskészítéshez,
megjelenítéshez vagy közzétételhez.

A megismételhető lekérdezések a származtatott adatkészletek előállításának
dokumentált és reprodukálható módját is biztosíthatják.

Adatexport és újrafelhasználás
==============================

Az OpenBioMaps adatai exportálhatók, illetve külső alkalmazásokból is
elérhetők elemzés, megjelenítés, közzététel és más célok érdekében.

A munkafolyamat követelményeitől függően az adatok közvetlenül az
OpenBioMaps rendszerből használhatók, vagy átvihetők olyan eszközökbe, mint
a QGIS és az R.

:doc:`Adathozzáférés <../data_access>`

Adatéletciklus
==============

Az OpenBioMaps a biodiverzitási adatok életciklusának különböző szakaszait
képes támogatni a kezdeti terepi megfigyeléstől a későbbi elemzésen és
közzétételen át az újrafelhasználásig.

Egy jellemző munkafolyamat a következőket foglalhatja magában:

* adatgyűjtés;
* strukturált adatbázisban történő tárolás;
* validálás és minőség-ellenőrzés;
* dokumentálás és metaadatkezelés;
* adatfeldolgozás és harmonizáció;
* elemzés és megjelenítés;
* közzététel vagy szabályozott megosztás; valamint
* további kutatási vagy természetvédelmi tevékenységekhez történő
  újrafelhasználás.

Ezek a szakaszok nem feltétlenül alkotnak szigorúan lineáris folyamatot. Az
adatok visszatérhetnek korábbi szakaszokba, amikor hibákat azonosítanak, új
információk válnak elérhetővé, vagy megváltoznak a projekt követelményei.
