:author: Miklós Bán
:date: 2026-08-08

Bevezetés
*********

Miért az OpenBioMaps?
=====================

A biodiverzitás-kutatás és a természetvédelem egyik legnagyobb kihívása nem a megfigyelések terepi gyűjtése, hanem az összegyűjtött adatok megbízható dokumentálása, kezelése és felhasználása. A terepi megfigyeléseket strukturált módon kell rögzíteni, biztonságosan kell tárolni, ellenőrizni kell a hibáikat, valamint hozzáférhetővé kell tenni őket a későbbi elemzéshez és felhasználáshoz. Ha ezeket a feladatokat egymástól független eszközökkel és manuális folyamatokkal végzik, az adatkezelés szükségtelenül bonyolulttá és időigényessé válhat.

Az OpenBioMaps e probléma megoldására jött létre. Egyetlen rugalmas adatkezelési keretrendszeren belül kapcsolja össze a terepi adatgyűjtést az adatok tárolásával, kezelésével, ellenőrzésével, megjelenítésével, elemzésével és hozzáférhetővé tételével.

A terepi munkát végzők számára ez azt jelenti, hogy a megfigyelések jelentős utófeldolgozás nélkül rögzíthetők és továbbíthatók egy strukturált adatbázisba. A kutatók és adatkezelők számára pedig azt, hogy az adatok egységes rendszer használatával ellenőrizhetők, rendszerezhetők, lekérdezhetők, elemezhetők és megoszthatók. A cél nem a kutatók által használt eszközök lecserélése, hanem azok összekapcsolása egy egységes és reprodukálható munkafolyamatban.

Mi az OpenBioMaps?
==================

Az OpenBioMaps egy nyílt forráskódú biodiverzitás-adatkezelési rendszer és keretrendszer, amelyet természetvédelmi szakemberekkel és kutatókkal együttműködésben fejlesztettek ki. Elsősorban élő szervezetek megfigyeléseinek és a hozzájuk kapcsolódó adatoknak a kezelésére készült, különösen a biodiverzitás-kutatás és a természetvédelem területén.

Egy OpenBioMaps-telepítés PostgreSQL-alapú adatkezelési környezetet biztosít, amely az adott projekt követelményeihez igazítható. Az adatbázis szerkezete, az adatrögzítési felületek, a hozzáférési szabályok, a munkafolyamatok és az adatkezelési folyamatok egyaránt a projekt igényeihez alakíthatók.

Az OpenBioMaps üzemeltethető egy szervezet saját szerverén, vagy használható egy megbízható partner által fenntartott szerveren keresztül. Ez lehetővé teszi hosszú távú adatkezelési környezet kialakítását anélkül, hogy a projekt egy központilag irányított adatbázistól vagy egyetlen előre meghatározott adatmodelltől függne.

Az adatgyűjtés és az adatfelhasználás összekapcsolása
====================================================

Az OpenBioMaps egyik központi alapelve, hogy az adatgyűjtést nem szabad elválasztani az adatok későbbi kezelésétől és felhasználásától.

Egy tipikus munkafolyamat a következőket foglalhatja magában:

* megfigyelések gyűjtése a terepen;
* megfigyelések feltöltése vagy rögzítése az adatbázisban;
* az adatok ellenőrzése és dokumentálása;
* az adatok rendszerezése és kezelése a projekten belül;
* az adatok lekérdezése és szűrése;
* az adatok megjelenítése és elemzése külső eszközök, például QGIS vagy R használatával;
* kiválasztott adatok közzététele vagy megosztása; valamint
* az adatok újbóli felhasználása kutatáshoz, monitorozáshoz, természetvédelmi tervezéshez vagy más célokra.

Mivel ezek a tevékenységek közös adatkezelési környezeten keresztül kapcsolódnak egymáshoz, számos olyan művelet automatizálható, amely egyébként manuális adatátvitelt vagy ismételt adatfeldolgozást igényelne. Ez csökkenti a hibák kockázatát, és lehetővé teszi, hogy a terepi munkát végzők és a kutatók kevesebb időt fordítsanak adminisztratív feladatokra.

Az OpenBioMaps ezért nem pusztán a megfigyelések tárolására szolgáló adatbázis. Keretrendszert biztosít a biodiverzitási adatok köré épülő teljes és reprodukálható adatkezelési munkafolyamat kialakításához.

Az OpenBioMaps megközelítése
============================

Az OpenBioMaps megközelítése több alapelvre épül:

* **Rugalmasság:** a projektek saját adatbázis-struktúrákat, adatmezőket, munkafolyamatokat és hozzáférési szabályokat határozhatnak meg.
* **Integráció:** az adatokhoz más rendszerek és eszközök is hozzáférhetnek, illetve az adatok továbbíthatók ezekbe, beleértve a QGIS, az R és a külső adatbázisok használatát.
* **Reprodukálhatóság:** a lekérdezések és az adatfeldolgozás dokumentálhatók, megismételhetők és hivatkozhatók.
* **Hosszú távú adatkezelés:** az adatokat strukturált adatbázis tárolja, így azok nem kötődnek egyedi táblázatokhoz vagy elszigetelt fájlokhoz.
* **Automatizálás:** az ellenőrzés, az adatátvitel és más ismétlődő műveletek automatizálhatók a manuális munka és a hibák csökkentése érdekében.
* **Nyitottság:** az OpenBioMaps nyílt forráskódú szoftvereken alapul, és szabadon hozzáférhető közösségi szolgáltatásokat biztosít.
* **Decentralizáció:** az adatbázisokat független szervezetek üzemeltethetik anélkül, hogy szükség lenne az adatok központi irányítására.
* **Közösségi fejlesztés:** a rendszer fejlesztése és karbantartása kutatókkal, természetvédelmi szakemberekkel és más felhasználókkal együttműködésben történik.

Az OpenBioMaps célja, hogy alkalmazkodjon a változó követelményekhez, ne pedig minden projektre egyetlen rögzített munkafolyamatot kényszerítsen. Egy projekt viszonylag egyszerű adatstruktúrával is elindulhat, majd a monitorozási program, a kutatási kérdések vagy az adatkezelési követelmények fejlődésével együtt bővülhet.


Főbb tulajdonságok
==================
* Ingyenes és nyíltan hozzáférhető OpenBioMaps-szolgáltatások.
* Testreszabható adatbázis-struktúrák, adatrögzítési felületek, munkafolyamatok és hozzáférési szabályok.
* Webalapú adatfeltöltés különféle formátumokban (ods, xls, xlsx, gpx, shp, csv stb.).
* API-hozzáférés az adatok lekérdezéséhez és feltöltéséhez.
* Megismételhető és hivatkozható lekérdezések.
* Állandó azonosítók (DOI-k) adatbázisokhoz és lekérdezésekhez.
* Adatexportálás különféle formátumokban (shp, csv, gpx, json stb.).
* Integráció R, QGIS, távoli adatbázisok és más külső rendszerek használatával.
* Integráció terepi mobil adatgyűjtő alkalmazásokkal.
* Testreszabható adatkezelési felületek.
* Kapcsolatok külső biodiverzitási adatbázisokhoz és platformokhoz, például a GBIF és az iNaturalist szolgáltatáshoz.


Műszaki megvalósítás
====================

Az OpenBioMaps projektkonfigurációt, PostgreSQL adatbázis-objektumokat,
metaadatokat, feltöltési munkafolyamatokat, hozzáférési szabályokat,
lekérdezéseket és külső klienseket összekapcsoló működésének műszaki
leírását lásd itt:

:doc:`Az OpenBioMaps adatfolyama és adatbázis-integrációja <obm_workflow>`

A következő ábrák a lekérdezési séma áttekintését mutatják be:

:download:`Lekérdezési séma (PDF) <docs/query_scheme.pdf>` |
:download:`Lekérdezési séma (ODP) <docs/query_scheme.odp>`

OpenBioMaps Consortium
======================

Az OpenBioMaps fejlesztését és karbantartását kutatóintézetekből, természetvédelmi szervezetekből és más partnerekből álló konzorcium végzi. A konzorcium koordinálja a szoftverfejlesztést és fenntartja a közösségi szolgáltatásokat.

:doc:`OpenBioMaps Consortium <consortium>`

:doc:`Kezdeti lépések az OpenBioMaps használatához <getting_started>`
