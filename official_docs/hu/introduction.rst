:author: Miklós Bán
:date: 2026-08-08

Bevezetés
*********

Miért az OpenBioMaps?
=====================

A biodiverzitás kutatásának és a természetvédelemnek az egyik legnagyobb
kihívása nem a megfigyelések terepi összegyűjtése, hanem az összegyűjtött
adatok megbízható dokumentálása, kezelése és felhasználása. A terepi
megfigyeléseket strukturált módon kell rögzíteni, biztonságosan kell tárolni,
ellenőrizni kell az esetleges hibákat, továbbá hozzáférhetővé kell tenni
azokat a későbbi elemzéshez és felhasználáshoz. Ha ezeket a feladatokat
egymástól elkülönülő eszközökkel és manuális folyamatokkal végzik, az
adatkezelés szükségtelenül bonyolulttá és időigényessé válhat.

Az OpenBioMaps e probléma megoldására jött létre. Egyetlen rugalmas
adatkezelési keretrendszerben kapcsolja össze a terepi adatgyűjtést az
adattárolással, az adatkezeléssel, a validálással, a megjelenítéssel, az
elemzéssel és az adatokhoz való hozzáféréssel.

A terepi munkát végzők számára ez azt jelenti, hogy a megfigyelések
jelentős utófeldolgozás nélkül rögzíthetők és továbbíthatók egy strukturált
adatbázisba. A kutatók és adatkezelők számára pedig azt, hogy az adatok
egységes rendszerben ellenőrizhetők, rendszerezhetők, lekérdezhetők,
elemezhetők és megoszthatók. A cél nem a kutatók által használt eszközök
lecserélése, hanem azok összekapcsolása egy egységes és reprodukálható
munkafolyamatban.

Mi az OpenBioMaps?
==================

Az OpenBioMaps egy nyílt forráskódú biodiverzitásiadat-kezelő rendszer és
keretrendszer, amely természetvédelmi szakemberekkel és kutatókkal
együttműködésben készül. Elsősorban az élőlényekre vonatkozó megfigyelések
és a hozzájuk kapcsolódó adatok kezelésére tervezték, különösen a
biodiverzitás-kutatás és a természetvédelem területén.

Egy OpenBioMaps-telepítés PostgreSQL-alapú adatkezelési környezetet biztosít,
amely az adott projekt követelményeinek megfelelően konfigurálható. Az
adatbázis szerkezete, az adatrögzítési felületek, a hozzáférési szabályok,
a munkafolyamatok és az adatkezelési folyamatok egyaránt a projekt
igényeihez igazíthatók.

Az OpenBioMaps üzemeltethető egy szervezet saját szerverén, vagy használható
egy megbízható partner által fenntartott szerveren. Ez lehetővé teszi olyan
hosszú távú adatkezelési környezet kialakítását, amely nem függ központilag
ellenőrzött adatbázistól vagy egyetlen előre meghatározott adatmodelltől.

Az adatgyűjtés és az adatok felhasználásának összekapcsolása
===========================================================

Az OpenBioMaps egyik központi alapelve, hogy az adatgyűjtés nem választható
el az adatok későbbi kezelésétől és felhasználásától.

Egy jellemző munkafolyamat a következőket foglalhatja magában:

* megfigyelések gyűjtése a terepen;
* megfigyelések feltöltése vagy rögzítése az adatbázisban;
* az adatok validálása és dokumentálása;
* az adatok rendszerezése és kezelése a projekten belül;
* az adatok lekérdezése és szűrése;
* az adatok megjelenítése és elemzése külső eszközökkel, például QGIS vagy R
  használatával;
* kiválasztott adatok közzététele vagy megosztása; valamint
* az adatok újbóli felhasználása kutatási, monitorozási,
  természetvédelmi-tervezési vagy egyéb célokra.

Mivel ezek a tevékenységek közös adatkezelési környezeten keresztül
kapcsolódnak egymáshoz, számos olyan művelet automatizálható, amely egyébként
manuális adatátvitelt vagy ismételt adatfeldolgozást igényelne. Ez csökkenti
a hibák kockázatát, és lehetővé teszi, hogy a terepi munkát végzők és a
kutatók kevesebb időt töltsenek adminisztratív feladatokkal.

Az OpenBioMaps ezért nem csupán a megfigyelések tárolására szolgáló
adatbázis. Olyan keretrendszert biztosít, amelyben a biodiverzitási adatok
köré teljes és reprodukálható adatkezelési munkafolyamat építhető.

Az OpenBioMaps megközelítése
============================

Az OpenBioMaps megközelítése több alapelvre épül:

* **Rugalmasság:** a projektek saját adatbázis-struktúrákat, adatmezőket,
  munkafolyamatokat és hozzáférési szabályokat határozhatnak meg.
* **Integráció:** az adatok más rendszerekkel és eszközökkel, többek között
  QGIS, R és távoli adatbázisok használatával is elérhetők és továbbíthatók.
* **Reprodukálhatóság:** a lekérdezések és az adatfeldolgozás dokumentálható,
  megismételhető és hivatkozható.
* **Hosszú távú adatkezelés:** az adatokat strukturált adatbázis tárolja,
  nem pedig egyedi táblázatokhoz vagy elszigetelt fájlokhoz kötődnek.
* **Automatizálás:** a validálás, az adatátvitel és más ismétlődő műveletek
  automatizálhatók a manuális munka és a hibák csökkentése érdekében.
* **Nyitottság:** az OpenBioMaps nyílt forráskódú szoftvereken alapul, és
  szabadon hozzáférhető közösségi szolgáltatásokat biztosít.
* **Decentralizáció:** az adatbázisokat független szervezetek üzemeltethetik
  anélkül, hogy az adatok központi ellenőrzésére lenne szükség.
* **Közösségi fejlesztés:** a rendszer fejlesztése és karbantartása
  kutatókkal, természetvédelmi szakemberekkel és más felhasználókkal
  együttműködésben történik.

Az OpenBioMaps célja, hogy alkalmazkodjon a változó követelményekhez, ne
pedig minden projektre azonos, rögzített munkafolyamatot kényszerítsen. Egy
projekt viszonylag egyszerű adatstruktúrával is elindulhat, majd a
monitorozási program, a kutatási kérdések vagy az adatkezelési követelmények
változásával továbbfejlődhet.


Főbb tulajdonságok
==================
* Ingyenes és nyíltan hozzáférhető OpenBioMaps-szolgáltatások.
* Testreszabható adatbázis-struktúrák, adatrögzítési felületek,
  munkafolyamatok és hozzáférési szabályok.
* Webes adatfeltöltés számos formátumban (ods, xls, xlsx, gpx, shp, csv
  stb.).
* API-hozzáférés az adatok lekérdezéséhez és feltöltéséhez.
* Megismételhető és hivatkozható lekérdezések.
* Állandó azonosítók (DOI-k) adatbázisokhoz és lekérdezésekhez.
* Adatexport különböző formátumokban (shp, csv, gpx, json stb.).
* Integráció R, QGIS, távoli adatbázisok és más külső rendszerek
  használatával.
* Integráció terepi mobil adatgyűjtő alkalmazásokkal.
* Testreszabható adatkezelési felületek.
* Kapcsolódás külső biodiverzitási adatbázisokhoz és platformokhoz, például
  a GBIF és az iNaturalist rendszeréhez.


OpenBioMaps-munkafolyamat
=========================

Az OpenBioMaps-munkafolyamat összekapcsolja a terepi adatgyűjtést, az
adatkezelést, a validálást, az elemzést, a közzétételt és az adatok újbóli
felhasználását.

:doc:`OBM-munkafolyamat <../obm_workflow>`

:download:`Lekérdezési séma (pdf) <docs/query_scheme.pdf>`
:download:`Lekérdezési séma (odp) <docs/query_scheme.odp>`

OpenBioMaps Consortium
======================

Az OpenBioMaps fejlesztését és karbantartását kutatóintézetekből,
természetvédelmi szervezetekből és más partnerekből álló konzorcium végzi. A
konzorcium koordinálja a szoftverfejlesztést, és fenntartja a közösségi
szolgáltatásokat.

:doc:`OpenBioMaps Consortium <consortium>`

:doc:`Első lépések az OpenBioMaps használatával <getting_started>`
