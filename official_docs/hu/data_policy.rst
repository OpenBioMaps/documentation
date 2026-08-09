.. _data-policy:

Adatkezelési irányelvek
***********************

Egy OpenBioMaps-projektnek dokumentált adatkezelési irányelvekkel kell
rendelkeznie, amelyek ismertetik az adatok gyűjtésének, kezelésének,
felülvizsgálatának, hozzáférésének, megosztásának és megőrzésének módját,
valamint későbbi archiválásukat vagy törlésüket. Az irányelvek segítenek az
adatközlőknek, a projektadminisztrátoroknak, az adatok felhasználóinak és a
külső partnereknek megérteni, mire számíthatnak a projekttől, és milyen
felelősségeik vannak.

Ez az oldal keretrendszert biztosít a projektspecifikus adatkezelési
irányelvek elkészítéséhez. Önmagában nem tekinthető teljes szabályzatnak, és
nem minősül jogi tanácsadásnak. A megfelelő szabályok a projekt céljától, az
érintett szervezetektől, a kezelt adatok kategóriáitól, a szerver
üzemeltetőjétől és az alkalmazandó jogszabályoktól függenek.

Az OpenBioMaps-projekt műszaki hozzáférési beállításainak a közzétett
irányelveket kell megvalósítaniuk, de nem helyettesítik azokat. Ugyanakkor
az irányelvek nem ígérhetnek olyan korlátozásokat, megőrzési időket,
biztonsági mentéseket vagy szolgáltatásokat, amelyek ténylegesen nincsenek
megvalósítva és rendszeresen ellenőrizve.

A műszaki jogosultságok konfigurálásáról lásd:
:doc:`Adathozzáférés <../data_access>`.


Kapcsolat más dokumentumokkal
=============================

A projekt adatkezelési irányelveit több kapcsolódó dokumentum is
kiegészítheti. Ezek hatókörét egyértelműen meg kell különböztetni.

``Adatkezelési irányelvek``
   A projektadatok irányítását és életciklusát ismertetik, beleértve az
   adatgyűjtést, a minőség-ellenőrzést, a hozzáférést, az újrafelhasználást,
   a megőrzést és a felelősségeket.

``Adatvédelmi tájékoztató``
   Ismerteti a személyes adatok kezelését, azonosítja az érintett
   adatkezelőt vagy adatkezelőket, és tájékoztatja az érintetteket a
   jogaikról.

``Felhasználási feltételek``
   Meghatározzák a szerver, a projekt, az alkalmazás vagy a kapcsolódó
   szolgáltatások használatának szerződéses szabályait.

``Sütitájékoztató``
   Ismerteti a webalkalmazás által használt sütiket vagy hasonló,
   böngészőoldali technológiákat.

``Licenc vagy adatfelhasználási megállapodás``
   Meghatározza, mit tehetnek a címzettek az adatokkal, és milyen
   feltételek vonatkoznak az adatokhoz való hozzáférésre vagy azok
   újrafelhasználására.

``Adatközlői megállapodás``
   Meghatározza, milyen adatokat jogosult beküldeni az adatközlő, és milyen
   engedélyeket ad a projektnek.

Egy dokumentum e témák közül többet is lefedhet, de minden szabálynak
egyértelmű hatókörrel kell rendelkeznie. A szerver egészére vonatkozó
feltételek nem határozzák meg automatikusan a szerveren tárolt minden
projekt irányítási szabályzatát.

A nyilvános OpenBioMaps-szolgáltatás példákat biztosít a
`felhasználási feltételekre <https://openbiomaps.org/terms/>`_,
az `adatvédelmi tájékoztatóra <https://openbiomaps.org/privacy/>`_ és a
`sütitájékoztatóra <https://openbiomaps.org/cookies/>`_. Ezek a
dokumentumok egy adott szolgáltatás példái, és nem másolhatók át másik
szerverre vagy projektbe a szervezetek, az adatkezelési műveletek, a
joghatóság, a dátumok és a kapcsolattartási adatok ellenőrzése nélkül.

.. TODO: Azonosítani kell az egyes OpenBioMaps-szervereken tárolt
   projektekre vonatkozó szerverszintű felhasználási feltételeket,
   adatvédelmi tájékoztatót és sütitájékoztatót. Ismertetni kell, mely
   rendelkezéseket örökli a projekt, és melyeket kell a projekt
   üzemeltetőjének meghatároznia.

.. TODO: Meg kell állapítani, hogy az OpenBioMaps képes-e
   projektspecifikus adatkezelési irányelveket, adatvédelmi tájékoztatót,
   feltételeket és licencet tárolni vagy megjeleníteni az adminisztrációs
   felületen. Dokumentálni kell az alkalmazandó konfigurációs mezőket,
   sablonokat és a tartalékértékek sorrendjét.


A projekt adatkezelési irányelveinek elkészítése
===============================================

Az adatkezelési irányelveket a rendszeres adatgyűjtés megkezdése előtt kell
elkészíteni. Felül kell vizsgálni őket, amikor megváltozik a projekt célja,
az adatbázis szerkezete, a hozzáférési modell, a részt vevő szervezetek
köre, a külső integrációk vagy a jogi követelmények.

Az irányelveket olyan nyelven kell megfogalmazni, amelyet a célközönség
megért. Ha egy projekt több nyelven működik, az irányelveknek meg kell
határozniuk, melyik változat a mérvadó, és hogyan tartják karban a
fordításokat.

Az irányelveknek legalább a következő kérdésekre kell választ adniuk:

* Mi a projekt célja?
* Milyen adatokat gyűjt?
* Ki üzemelteti a projektet, és kihez lehet fordulni?
* Ki jogosult adatok beküldésére, megtekintésére, módosítására,
  validálására, exportálására vagy közzétételére?
* Hogyan értékelik és dokumentálják az adatminőséget?
* Mely rekordok vagy mezők érzékenyek?
* Milyen feltételekkel használhatók fel újra az adatok?
* Hogyan kell hivatkozni a projektre és adatközlőire?
* Mennyi ideig őrzik meg az adatokat, csatolmányokat, naplókat és
  biztonsági mentéseket?
* Hogyan jelenthetők a hibák, a jogokkal kapcsolatos aggályok, a biztonsági
  incidensek vagy a törlési kérelmek?
* Hogyan és mikor módosíthatók az irányelvek?

.. TODO: El kell dönteni, hogy a projektek szabványos szabályzatsablont,
   ellenőrzőlistát vagy mindkettőt kapjanak-e. Szabványos sablon bevezetése
   esetén azonosítani kell a kötelező és az opcionális rendelkezéseket.


Hatókör és cél
==============

Az irányelveknek a projekt azonosításával és céljának meghatározásával kell
kezdődniük. Ez segít eldönteni, mely adatok relevánsak, és megakadályozza,
hogy az egyik célból gyűjtött adatokat észrevétlenül egy azzal
összeegyeztethetetlen célra használják fel.

A hatókörnek a következőket kell tartalmaznia:

* a projekt nyilvános nevét és adatbázis-azonosítóját;
* a tudományos, természetvédelmi, oktatási vagy működési célt;
* a földrajzi, taxonómiai és időbeli hatókört;
* az érintett adattáblákat és főbb adatkategóriákat;
* az érintett webes, mobil-, API- és külsőkliens-felületeket;
* minden kapcsolódó adatbázist vagy szolgáltatást;
* a tervezett felhasználókat és kedvezményezetteket; valamint
* a projekt hatókörén kifejezetten kívül eső tevékenységeket.

Ha a projekt kísérleti, teszt- és éles környezettel rendelkezik, az
irányelveknek tisztázniuk kell, mely környezetek tartalmaznak valós
adatokat, és mely szabályok vonatkoznak az egyes környezetekre.

.. TODO: Meg kell határozni a kísérleti, tesztelési, stabil, archivált és
   megszüntetett projektekre vonatkozó jelenlegi OpenBioMaps-terminológiát.
   Meg kell erősíteni, hogy ezek az alkalmazás által megvalósított formális
   projektállapotok vagy csupán irányítási fogalmak.

.. TODO: Rövid példát kell hozzáadni egy biodiverzitási előfordulási
   projekt, valamint egy ismételt megfigyelési eseményeken alapuló
   monitorozási projekt hatókörének meghatározására.


Fogalommeghatározások
=====================

Az irányelvekben használt kifejezéseket következetesen kell meghatározni. A
projekttől függően a hasznos fogalommeghatározások közé tartozhatnak a
következők:

``Projekt``
   Az OpenBioMaps-adatbázis, annak konfigurált felületei és a kapcsolódó
   adatkezelési munkafolyamat.

``Szerverüzemeltető``
   Az OpenBioMaps-szerver és az alapjául szolgáló infrastruktúra
   üzemeltetéséért felelős szervezet.

``Projektüzemeltető``
   Egy adott projekt irányításáért felelős személy vagy szervezet.

``Adatközlő``
   A projektbe adatokat beküldő személy vagy szervezet.

``Adattulajdonos`` vagy ``jogtulajdonos``
   A beküldött adatok meghatározott jogait birtokló személy vagy szervezet.
   A pontos jelentést meg kell határozni, nem pedig feltételezni.

``Adatgazda``
   A projekt irányelveinek megfelelő adat- és metaadat-karbantartásért
   felelős személy.

``Validáló`` vagy ``kurátor``
   A beküldött adatok felülvizsgálatára, annotálására, elfogadására,
   javítására vagy elutasítására jogosult személy.

``Adatfelhasználó``
   A projektadatokat megtekintő, lekérdező, letöltő vagy más módon
   feldolgozó személy vagy alkalmazás.

``Rekord``
   Egy megfigyelést, eseményt, taxont, helyszínt, mintát vagy más
   projektentitást ábrázoló sor vagy egymással logikailag összekapcsolt
   sorok halmaza.

``Csatolmány``
   Egy rekordhoz kapcsolódó fájl, például fénykép, hangfelvétel, dokumentum
   vagy adatfájl.

``Metaadat``
   A projektet, annak tábláit és oszlopait, egy adatkészletet, egy
   feltöltést vagy egy rekordot leíró információ.

``Személyes adat``
   Az alkalmazandó jog által meghatározott, azonosított vagy azonosítható
   személyre vonatkozó információ.

``Érzékeny biodiverzitási adat``
   Olyan adat, amelynek nyilvánosságra hozatala veszélyt jelenthet egy
   fajra, élőhelyre, védett területre, földtulajdonosra, adatközlőre,
   kutatási tevékenységre vagy természetvédelmi intézkedésre.

A fogalommeghatározások nem sugallhatják azt, hogy egy projekt pusztán az
adatok tárolásával megszerezte azok tulajdonjogát. A szerzői jog, az
adatbázisjogok, a titoktartási kötelezettségek, a munkaszerződések és más
jogok eltérően alkalmazhatók a különböző joghatóságokban.

.. TODO: Egységesíteni kell a ``project owner``, ``project founder``,
   ``project host``, ``operator``, ``administrator``, ``data owner`` és
   ``uploader`` kifejezéseket az OpenBioMaps dokumentációjában és
   felhasználói felületén.

.. TODO: Jogi felülvizsgálatot kell kérni a ``data owner`` és az
   ``ownership of data`` kifejezésekre vonatkozóan. Ahol indokolt,
   pontosabb fogalmakkal – például jogtulajdonos, adatközlő, adatőrző,
   adatkezelő vagy forrás – kell helyettesíteni őket.


Irányítás és felelősségek
=========================

Egy projektben több szervezet és adminisztrációs szint is részt vehet. A
felelősségeket kifejezetten ki kell osztani, nem pedig a műszaki
jogosultságokból kikövetkeztetni.

Az irányelveknek azonosítaniuk kell a következő feladatokért való
felelősséget:

* a szerver üzemeltetése és biztonságossá tétele;
* a projekt irányítása;
* az adatbázis szerkezetének és metaadatainak meghatározása;
* az adatközlők és a csoporttagság jóváhagyása;
* a feltöltési űrlapok létrehozása és karbantartása;
* az adathozzáférési szabályok felülvizsgálata;
* a rekordok validálása és javítása;
* az érintettek és jogtulajdonosok kérelmeinek megválaszolása;
* az exportálási vagy adathozzáférési kérelmek felülvizsgálata;
* a licencek és forrásmegjelölési információk karbantartása;
* a biztonsági mentés, a visszaállítás és a katasztrófa utáni helyreállítás;
* az incidenskezelés;
* az adatok megőrzése vagy törlése;
* a külső integrációk karbantartása; valamint
* az irányelvek módosításainak felülvizsgálata és közzététele.

Az adminisztrációs hozzáférésnek a legkisebb jogosultság elvét kell
követnie. A felhasználókezelőknek például nem szükséges automatikusan
jogosultságot kapniuk SQL végrehajtására, háttérfolyamatok szerkesztésére
vagy minden csatolmány exportálására.

A hozzárendelhető adminisztrációs funkciók áttekintését lásd:
:doc:`Adminisztrációs beállítások <../admin_settings>`.

.. TODO: Felelősségi mátrixot kell készíteni a szerverüzemeltető, a
   projektalapító, a projektüzemeltető, az adminisztrátor, az adatgazda, a
   kurátor, az adatközlő és az adatfelhasználó szerepkörére.

.. TODO: Dokumentálni kell, mely adminisztrációs műveleteket rögzíti az
   auditnapló, és mennyi ideig őrzik meg ezeket az auditinformációkat.

.. TODO: Eljárást kell meghatározni a felelősség átadására arra az esetre,
   ha egy projektalapító vagy projektüzemeltető elhagyja a részt vevő
   szervezetet.


Adatgyűjtés
===========

Az irányelveknek ismertetniük kell, milyen adatokat, kik és milyen
felületeken keresztül küldhetnek be. Az OpenBioMaps-projektek webes
űrlapokon, fájlfeltöltéseken, mobilalkalmazásokon, az API-n, közvetlen
adatbázis-kapcsolatokon vagy automatikus importálásokon keresztül
fogadhatnak adatokat.

Minden adatgyűjtési munkafolyamat esetében dokumentálni kell:

* az adatgyűjtés célját;
* az adatok várt forrását;
* a kötelező és opcionális mezőket;
* az engedélyezett fájl- és csatolmánytípusokat;
* az alkalmazandó validálási szabályokat;
* a szükséges forrásmegjelölést és származási információkat;
* az adatok beküldésének jogi vagy szervezeti felhatalmazását;
* engedélyezett-e a névtelen vagy hitelesítés nélküli adatbeküldés;
* az új rekordok kezdeti hozzáférési besorolását; valamint
* mi történik, ha egy beküldés hiányos vagy elutasításra kerül.

Az adatközlők csak olyan adatokat küldhetnek be, amelyek átadására
jogosultak. Ez magában foglalja a fényképekhez, hangfelvételekhez,
jelentésekhez, más adatbázisból másolt adatokhoz és azonosítható személyekre
vonatkozó információkhoz kapcsolódó jogok és titoktartási kötelezettségek
ellenőrzését.

A feltöltési űrlapokat a :doc:`Feltöltési űrlapok kezelése
<../upload_forms>` ismerteti.

.. TODO: Dokumentálni kell, hogy az OpenBioMaps megkövetelheti-e az
   adatközlőktől projektspecifikus adatközlői megállapodás elfogadását a
   beküldés előtt, és hogy a rendszer rögzíti-e az elfogadott megállapodás
   verzióját a feltöltéssel együtt.

.. TODO: Meg kell határozni a hitelesítés nélkül beküldött adatok
   működését, valamint tulajdonosi vagy adatőrzési szabályait. Meg kell
   erősíteni, hogy minden jelenlegi felület támogatja-e a névtelen
   feltöltést.

.. TODO: Útmutatást kell hozzáadni a külső szolgáltatásokból, például a
   GBIF vagy az iNaturalist rendszeréből történő adatimportáláshoz,
   beleértve a származást, a licencek összeegyeztethetőségét, a
   duplikátumészlelést és a későbbi frissítéseket.


Metaadatok és származás
=======================

Az adatokhoz elegendő metaadatot kell mellékelni ahhoz, hogy jelentésük,
forrásuk, minőségük és engedélyezett felhasználásuk érthető legyen.

A projektszintű metaadatoknak általában a következőket kell tartalmazniuk:

* a projekt címét és leírását;
* a felelős szervezeteket és kapcsolattartókat;
* a földrajzi, időbeli és taxonómiai lefedettséget;
* az adatgyűjtési módszereket;
* a minőség-ellenőrzési folyamatokat;
* a hozzáférési és újrafelhasználási feltételeket;
* a licenceket;
* az előnyben részesített hivatkozásokat; valamint
* a frissítés gyakoriságát.

A tábla- és oszlopszintű metaadatoknak ismertetniük kell az adatok
jelentését, mértékegységeit, megengedett értékeit,
koordináta-referenciarendszereit, taxonómiai konvencióit, a hiányzó értékek
ábrázolását és az adatokon végzett átalakításokat.

A rekord- vagy feltöltésszintű származási információk a következőket
tartalmazhatják:

* az adatközlőt vagy a forrásszervezetet;
* az adatgyűjtőt vagy a megfigyelőt;
* az eredeti rekordazonosítót;
* a beküldés és a megfigyelés dátumát;
* a használt feltöltési űrlapot vagy importálási folyamatot;
* a forrás-adatkészletet és annak verzióját;
* az importálás során végzett átalakításokat;
* a validálási állapotot; valamint
* a származtatott vagy felváltott rekordokra mutató hivatkozásokat.

Az adatbázistáblákhoz és -oszlopokhoz megadott leírások a projekt
metaadatainak részét képezik. Lásd: :ref:`Adatbázistáblák és -oszlopok
<database-columns>`.

.. TODO: Meg kell határozni azokat a minimális metaadatokat, amelyek
   szükségesek ahhoz, hogy egy OpenBioMaps-projekt éles használatra vagy
   közzétételre késznek minősüljön.

.. TODO: Az OpenBioMaps projekt-, tábla-, oszlop-, feltöltés- és
   rekordmetaadatait meg kell feleltetni az olyan releváns szabványoknak,
   mint a Darwin Core, az Ecological Metadata Language, a DataCite és adott
   esetben az ISO 19115.

.. TODO: Dokumentálni kell, mely származási információkat rögzíti
   automatikusan az OpenBioMaps, és mely mezőket kell hozzáadni a projekt
   sémájához.


Adatminőség és validálás
========================

Az irányelveknek ismertetniük kell, hogy egy rekord tárolása nem feltétlenül
igazolja annak helyességét. Meg kell határozniuk az elérhető validálási
állapotokat, valamint azt, hogy ki rendelheti hozzá vagy módosíthatja
ezeket.

A minőség-ellenőrzések a következőket foglalhatják magukban:

* a kötelező mezők és adattípusok validálása;
* ellenőrzött listák és tartományellenőrzések;
* a taxonnevek validálása;
* a dátumok és koordináták konzisztenciájának ellenőrzése;
* a duplikátumok észlelése;
* a koordináta-referenciarendszerek ellenőrzése;
* a csatolmányok vagy alátámasztó bizonyítékok felülvizsgálata;
* szakértői határozás;
* automatikus térbeli vagy időbeli ellenőrzések;
* összehasonlítás külső referenciaadatokkal; valamint
* az adatközlők vagy felülvizsgálók megjegyzései.

A javítások során meg kell őrizni a releváns származási információkat. Ahol
ez megvalósítható, a projektnek meg kell különböztetnie az eredetileg
beküldött értéket a későbbi normalizálástól, értelmezéstől vagy javítástól.

A közzétett adatokhoz megfelelő minősítéseket kell mellékelni. Egy
figyelmeztetés vagy validálási jelző hiánya nem mutatható be a pontosság, a
teljesség, egy adott célra való alkalmasság vagy a jelenlegi taxonómiai
értelmezés garanciájaként.

.. TODO: Dokumentálni kell az OpenBioMaps által megvalósított
   adatértékelési modellt, beleértve a rekordok, feltöltések és
   felhasználók értékelését, valamint minden numerikus pontszám vagy
   validálási állapot pontos jelentését.

.. TODO: Ismertetni kell, hogy a rekordelőzmények tárolják-e a korábbi és
   az új értékeket, a szerkesztők személyazonosságát, az időbélyegeket és
   a módosítások okát. Meg kell határozni, ki tekintheti meg és állíthatja
   vissza a korábbi értékeket.

.. TODO: Ajánlott javítási munkafolyamatot kell hozzáadni, amely kiterjed a
   bejelentett hibákra, a kurátori felülvizsgálatra, az adatközlővel
   folytatott egyeztetésre, a javításra, az elutasításra, a visszavonásra
   és az adatok korábbi címzettjeinek értesítésére.


Hozzáférés és közzététel
========================

Az irányelveknek meg kell határozniuk, mely adatok nyilvánosak, melyekhez
férnek hozzá kizárólag hitelesített felhasználók vagy meghatározott
csoportok, melyek érhetők el csak jóváhagyás után, illetve melyekhez férnek
hozzá kizárólag a projektadminisztrátorok.

Az OpenBioMaps a következőket kombinálhatja:

* projektszintű hozzáférési beállítások;
* sorszintű hozzáférési szabályok;
* oszlopszintű korlátozások;
* csoporttagság;
* adminisztratív szerepkörök; valamint
* exportengedélyezési munkafolyamatok.

A tényleges műszaki konfigurációt minden releváns felhasználói csoportot
képviselő fiókkal, valamint – ha a nyilvános hozzáférés engedélyezett –
hitelesítés nélkül is tesztelni kell.

Az elérhető szabályozási lehetőségekről lásd:
:doc:`Adathozzáférés <../data_access>`.

Az irányelveknek meg kell különböztetniük a következőket:

* annak megismerése, hogy egy rekord létezik;
* egy rekord megtekintése a térképen;
* attribútumainak megtekintése;
* pontos geometriájának megtekintése;
* lekérdezése és szűrése;
* letöltése;
* csatolmányainak megtekintése vagy letöltése;
* módosítása vagy törlése;
* lekérése az API-n keresztül;
* hozzáférés SQL vagy külső alkalmazás használatával; valamint
* hozzáférés jóváhagyott adatigénylésen keresztül.

Ezek a műveletek különböző mennyiségű információt tehetnek hozzáférhetővé,
ezért nem szükséges azonos jogosultságokkal rendelkezniük.

.. TODO: Dokumentálni kell az OpenBioMaps pontos jogosultság-feloldási
   algoritmusát, és annak alapján tesztelt példákat kell készíteni a
   nyilvános, hitelesített, csoport-, kizárólagos tulajdonosi és
   oszlopkorlátozásos adatokra.

.. TODO: Meg kell erősíteni, hogyan alkalmazzák a csatolmányok előnézetei
   és exportjai, az API-eredmények, a térképrétegek, a gyorsítótárazott
   fájlok és a közvetlen SQL-kapcsolatok a sor- és oszlopszintű
   hozzáférési szabályokat.

.. TODO: Rendszeres hozzáférés-felülvizsgálati eljárást kell meghatározni,
   amely kiterjed a csoporttagságra, az adminisztratív jogosultságokra, az
   API hitelesítési adataira, a közvetlen adatbázisfiókokra és a létrehozott
   letöltési hivatkozásokra.


Érzékeny biodiverzitási adatok
==============================

A pontos helyszínek, az adatgyűjtési módszerek, a megfigyelők
személyazonossága vagy más attribútumok kockázatot jelenthetnek a
veszélyeztetett fajokra, élőhelyekre, földtulajdonosokra, adatközlőkre és
természetvédelmi tevékenységekre. A projektnek meg kell határoznia e
kockázatok értékelésének módját és az alkalmazott védelmi intézkedéseket.

A lehetséges védelmi intézkedések a következők:

* kiválasztott mezők visszatartása;
* teljes rekordok hozzáférésének meghatározott csoportokra korlátozása;
* a pontos geometria elrejtése a nyilvános felhasználók elől;
* általánosított koordináták közzététele;
* a közzététel késleltetése;
* egyedi jóváhagyás előírása az exportokhoz;
* a nyilvános és korlátozott csatolmányok elkülönítése; valamint
* a korlátozás okának és felülvizsgálati dátumának rögzítése.

A korlátozásoknak arányosnak és dokumentáltnak kell lenniük, továbbá
rendszeresen felül kell vizsgálni őket. Egy rekord nem maradhat korlátlan
ideig korlátozott pusztán azért, mert állapotát soha nem értékelték újra.

Bizonyos projektkonfigurációkban a szabálytábla támogatja az érzékenységgel
kapcsolatos olyan értékeket, mint a ``sensitive``, ``restricted``,
``no-geom`` és ``only-owner``. Pontos működésüket ellenőrizni kell, mielőtt
a projekt ezekre hagyatkozna.

.. TODO: Meg kell erősíteni a támogatott érzékenységi értékek teljes
   listáját és pontos hatását a webes felületen, a térképeken, a
   lekérdezésekben, a letöltésekben, az API-ban, a csatolmányoknál és az
   írási műveleteknél.

.. TODO: Dokumentálni kell, hogy az OpenBioMaps támogatja-e a koordináták
   általánosítását, vagy csak elrejti a geometriát. Ha az általánosítás
   támogatott, ismertetni kell az algoritmust, a pontosságot, a
   következetességet és a származtatott exportok kezelését.

.. TODO: Érzékenységértékelési eljárást kell kidolgozni, amely azonosítja,
   ki sorolhat be egy rekordot, milyen indokok használhatók, hogyan
   rögzítik a döntéseket, és mikor kell felülvizsgálni a korlátozásokat.

.. TODO: Példákat kell hozzáadni a veszélyeztetett fajok, aktív fészkek,
   magánterületek, régészeti vagy barlangi helyszínek, embargó alatt álló
   kutatások és az adatközlők biztonsága esetére.


Személyes adatok és adatvédelem
===============================

A biodiverzitási adatok akkor is tartalmazhatnak személyes adatokat, ha a
projekt elsődleges célja nem személyekre vonatkozó információk gyűjtése.
Ilyenek lehetnek például:

* az adatközlők, megfigyelők, adatgyűjtők, validálók és fényképészek neve;
* e-mail-címek és felhasználói profiladatok;
* egy személy otthonához vagy mozgásához kapcsolódó pontos helyszínek;
* mobilalkalmazások útvonalnaplói;
* fényképek, hangfelvételek és szabad szöveges megjegyzések;
* IP-címek és alkalmazásnaplók;
* a rekordok tulajdonosi és szerkesztési előzményei; valamint
* a felhasználókhoz kapcsolódó megjegyzések vagy értékelések.

Az alkalmazandó adatvédelmi tájékoztatónak azonosítania kell a releváns
adatkezelőt vagy adatkezelőket, az adatkezelés céljait, jogalapjait, az
adatkategóriákat, a címzetteket, a megőrzési időket, a nemzetközi
adattovábbításokat, a biztonsági intézkedéseket, a kapcsolattartási adatokat
és az érintettek jogait, az alkalmazandó jog követelményeinek megfelelően.

A projekt adatkezelési irányelveinek hivatkozniuk kell az alkalmazandó
adatvédelmi tájékoztatóra, nem pedig megkísérelniük annak helyettesítését. A
jogalapokra és a törvényes jogokra vonatkozó állításokat az adott
joghatóságban megfelelő képesítéssel rendelkező személynek kell
felülvizsgálnia.

Különös gondosság szükséges, ha az adatok gyermekekre, kiszolgáltatott
személyekre, magánlakásokra, munkavállalók megfigyelésére, folyamatos
helymeghatározásra vagy a személyes adatok különleges kategóriáira
vonatkoznak.

.. TODO: Minden adatkezelési munkafolyamat esetében meg kell határozni a
   szerverüzemeltető, a projektüzemeltető, a részt vevő szervezetek, az
   adatközlők és a külső szolgáltatók adatvédelmi szerepkörét és
   felelősségét.

.. TODO: Frissíteni és jogilag felül kell vizsgálni az alapértelmezett
   adatvédelmi tájékoztatót. Az elérhető példa 2022-ből származik, és
   előfordulhat, hogy nem tükrözi a jelenlegi szervezeteket, adatkezelési
   műveleteket, technológiákat, megőrzési időket vagy alkalmazandó
   adatvédelmi követelményeket.

.. TODO: Leltárt kell készíteni a jelenlegi webalkalmazás, a
   mobilalkalmazások, az API, a hitelesítési szolgáltatás, a naplók, a
   háttérfolyamatok, a biztonsági mentések, az e-mail-szolgáltatás és a
   külső integrációk által kezelt összes személyes adatról.

.. TODO: Dokumentálni kell, hogyan fogadják, hitelesítik, osztják ki,
   teljesítik és rögzítik a hozzáférésre, helyesbítésre, korlátozásra,
   hordozhatóságra, tiltakozásra és törlésre irányuló kérelmeket.

.. TODO: Tisztázni kell, hogyan érinti a fiók törlése a feltöltött
   rekordokat, a forrásmegjelölést, az előzményeket, a megjegyzéseket, az
   értékeléseket, az API-tokeneket, az aktív munkameneteket, az ütemezett
   feladatokat, a naplókat, a biztonsági mentéseket és a más felhasználók
   által már exportált másolatokat.


Jogok, licencek és engedélyezett újrafelhasználás
=================================================

Az irányelveknek meg kell határozniuk, milyen jogokkal kell rendelkezniük az
adatközlőknek a beküldött adatok felett, és milyen engedélyeket adnak a
projektnek. Meg kell határozniuk azt a licencet vagy más feltételeket is,
amelyek alapján a címzettek újra felhasználhatják az adatokat.

Eltérő jogok vonatkozhatnak a következőkre:

* egyedi megfigyelések;
* összeállított adatbázisok;
* fényképek és hangfelvételek;
* jelentések és más csatolmányok;
* taxonómiai vagy földrajzi referenciaadatok;
* térképcsempék és alaptérképek;
* metaadatok;
* szoftverek és űrlapdefiníciók; valamint
* külső forrásból importált tartalom.

Egy projekt nem nevezheti nyíltnak az adatokat, ha a címzettek nem
rendelkeznek egyértelmű engedéllyel azok újrafelhasználására. A nyilvános
láthatóság önmagában nem jelent licencet.

Ha több licenc alkalmazandó, az exportoknak elegendő információt kell
megőrizniük ahhoz, hogy minden rekord vagy csatolmány esetében megállapítható
legyen az alkalmazandó licenc és forrásmegjelölés. Egymással
összeegyeztethetetlen forráslicenceket engedély nélkül nem szabad új licenc
alatt egyesíteni.

.. TODO: Meg kell határozni az OpenBioMaps által az adatokhoz,
   metaadatokhoz és médiafájlokhoz támogatott vagy ajánlott licenceket.
   Ismertetni kell a nyilvános hozzáférés, a korlátozott hozzáférés, a CC0,
   a CC BY, a CC BY-NC és az egyéni adatfelhasználási megállapodások közötti
   különbségeket.

.. TODO: Dokumentálni kell, hol tárolhatók a projekt-, tábla-, feltöltés-,
   rekord- és csatolmányszintű licencinformációk, és hogy automatikusan
   bekerülnek-e az exportokba és az API-válaszokba.

.. TODO: Eljárást kell létrehozni az egymással ütköző tulajdonosi,
   szerzőségi, licenc-, titoktartási vagy törlési igények rendezésére.

.. TODO: Jogilag felül kell vizsgálni minden olyan szabályt, amely a
   névtelenül beküldött adatok jogait a projektüzemeltetőre ruházza át.
   Biztosítani kell, hogy a felhasználói felület a beküldés előtt bemutassa
   az alkalmazandó feltételeket.


Hivatkozás és forrásmegjelölés
==============================

Az irányelveknek meg kell adniuk a projektre vonatkozó előnyben részesített
hivatkozást, és ismertetniük kell, hogyan kell feltüntetni az adatközlőket,
a forrásszervezeteket, az adatkészleteket és az OpenBioMaps rendszert.

Egy hivatkozásnak általában a következőket kell azonosítania:

* az adatok közzétevőjét vagy a felelős szervezetet;
* a projekt vagy az adatkészlet címét;
* az OpenBioMaps-szervert vagy repository-t;
* a verziót, a közzététel vagy a lekérdezés dátumát;
* a hozzáférés dátumát;
* az állandó azonosítót, ha rendelkezésre áll; valamint
* az alkalmazandó licencet.

Ha egy adatkészlet vagy mentett lekérdezés DOI-val vagy más állandó
azonosítóval rendelkezik, ezt kell előnyben részesíteni az esetleg
megváltozó URL-lel szemben.

A rekordszintű forrásmegjelölést meg kell őrizni, ha ezt az alkalmazandó
licenc vagy adatközlői megállapodás megköveteli. A felhasználókat nem szabad
szükségtelenül személyes kapcsolattartási adatok közzétételére utasítani.

.. TODO: Szabványos, géppel olvasható hivatkozási formátumot kell
   meghatározni és megvalósítani az OpenBioMaps-projektekhez, mentett
   lekérdezésekhez és exportokhoz.

.. TODO: Meg kell erősíteni, mely OpenBioMaps-objektumok kaphatnak jelenleg
   DOI-t, hogyan rögzítik a verziókat, és milyen módosítások maradnak
   lehetségesek a közzététel után.

.. TODO: Tesztelt hivatkozási példákat kell hozzáadni egy teljes projektre,
   egy szűrt lekérdezésre, egy API-eredményre, egy letöltött csatolmányra és
   több adatközlőtől összesített adatokra.


Adatigénylések és exportok
==========================

Egyes projektek megkövetelik, hogy a felhasználók engedélyt kérjenek a
korlátozott adatok letöltése előtt. Az irányelveknek ismertetniük kell:

* ki nyújthat be kérelmet;
* milyen információkat kell megadnia a kérelmezőnek;
* milyen szempontok alapján hoznak döntést;
* ki hozza meg a döntést;
* a válaszadás várható idejét;
* az engedélyezett és tiltott felhasználási módokat;
* a szükséges biztonsági intézkedéseket;
* engedélyezett-e az adatok további megosztása;
* a lejárati és törlési követelményeket;
* a jelentési és hivatkozási követelményeket; valamint
* a fellebbezés, módosítás vagy megújítás folyamatát.

A döntéseknek következetesnek és dokumentáltnak kell lenniük. Az exportált
fájlok csak a jóváhagyott rekordokat és mezőket tartalmazhatják, letöltési
hivatkozásaikat pedig védeni kell, és megfelelő idő elteltével le kell
járniuk.

.. TODO: Dokumentálni kell az Export vagy letöltésikérelem-modult,
   beleértve annak munkafolyamatát, szerepköreit, üzenetsablonjait,
   auditbejegyzéseit, létrehozott fájljait, hozzáférés-ellenőrzéseit, a
   hivatkozások lejáratát és a tisztítási eljárást.

.. TODO: Meg kell állapítani, hogy a jóváhagyási feltételek tárolhatók-e a
   kérelemmel együtt, és bemutathatók-e a kérelmezőnek a letöltés előtt.

.. TODO: Meg kell határozni, hogyan értesítheti a projekt a korábbi
   címzetteket, ha az exportált adatokat javítják, visszavonják,
   átsorolják, vagy kiderül róluk, hogy természetvédelmi vagy adatvédelmi
   kockázatot jelentenek.


Megosztás és külső integrációk
==============================

Az adatok letöltéseken, API-kon, közvetlen SQL-kapcsolatokon, QGIS, R,
mobilkliensek, háttérfolyamatok, összekapcsolási szolgáltatások vagy külső
repository-kban történő közzététel révén elhagyhatják az OpenBioMaps webes
felületét.

Az irányelveknek azonosítaniuk kell a rendszeres adatcímzetteket és
integrációkat, az átadott adatokat, a célt, az alkalmazandó
hozzáférés-szabályozást, a frissítés gyakoriságát, a licenceket, valamint a
törlési vagy javítási folyamatot.

Az automatikus közzététel nem tehet hozzáférhetővé olyan mezőket, amelyek
ugyanazon felhasználó elől rejtve lennének a webes felületen. Az
integrációk által használt hitelesítési adatokhoz csak a szükséges
jogosultságokat kell hozzárendelni, és azokat rendszeresen cserélni vagy
visszavonni kell, ha már nincs rájuk szükség.

.. TODO: Leltárt kell készíteni a támogatott külső felületekről, és
   dokumentálni kell, hogy mindegyik következetesen alkalmazza-e a
   projekt-, sor- és oszlopszintű korlátozásokat.

.. TODO: Eljárást kell meghatározni az automatikus adattovábbítások
   jóváhagyására, dokumentálására, felügyeletére és letiltására.

.. TODO: Ismertetni kell, hogyan kerülnek át a javítások és törlések az
   olyan külső szolgáltatásokba, mint a GBIF, az iNaturalist, a
   gyorsítótárazott térképrétegek vagy a replikált adatbázisok.


Megőrzés, törlés és archiválás
==============================

Az irányelveknek megőrzési időket vagy felülvizsgálati szempontokat kell
meghatározniuk minden fő információkategóriához, beleértve a következőket:

* aktív projektrekordok;
* elutasított és visszavont beküldések;
* rekordelőzmények;
* taxonómiai és validálási annotációk;
* felhasználói fiókok és profilok;
* meghívók és csoporttagság;
* megszakított feltöltések és ideiglenes fájlok;
* csatolmányok és létrehozott bélyegképek;
* megjegyzések, értékelések és üzenetek;
* adathozzáférési kérelmek és döntések;
* létrehozott exportok és letöltési hivatkozások;
* alkalmazás- és szervernaplók;
* háttérfolyamat-naplók;
* API-tokenek és munkamenetek;
* biztonsági mentések; valamint
* archivált projektverziók.

Az aktív adatbázisból történő törlés nem feltétlenül távolítja el az
információt a biztonsági mentésekből, külső exportokból, naplókból,
gyorsítótárakból vagy a felhasználók által korábban megszerzett másolatokból.
Az irányelveknek pontosan ismertetniük kell ezeket a korlátokat.

Ha a hosszú távú tudományos reprodukálhatóság megőrzést követel meg, a
törlést esetleg korlátozással, álnevesítéssel, visszavonással vagy
sírkőrekord közzétételével kell helyettesíteni. Az ilyen döntéseket
dokumentált jogi és tudományos értékelés alapján kell meghozni.

.. TODO: Megőrzési ütemtervet kell készíteni az alapértelmezett
   OpenBioMaps-telepítéshez, és azonosítani kell, mely időtartamok
   konfigurálhatók szerver- és projektszinten.

.. TODO: Dokumentálni kell egy rekord, feltöltés, csatolmány, felhasználói
   fiók, csoport, projekt és létrehozott export törlésének pontos hatását.

.. TODO: Támogatott projektlezárási munkafolyamatot kell meghatározni,
   amely kiterjed a végső exportra, a metaadatok közzétételére, az új
   üzemeltetőnek történő átadásra, a csak olvasható archiválásra, a
   törlésre, a felhasználók értesítésére és a hitelesítési adatok
   eltávolítására.


Biztonsági mentések és visszaállítás
===================================

Az adatkezelési irányelveknek meg kell különböztetniük a biztonsági
mentéseket az archívumoktól.

A biztonsági mentés elsődleges célja a rendszer visszaállítása véletlen
adatvesztés, sérülés vagy műszaki hiba után. Az archívumot az adatok hosszú
távú megőrzése és folyamatos értelmezhetősége érdekében tartják fenn. A
biztonsági mentés nem helyettesíti a dokumentált archívumot, és egy
biztonsági mentési feladat sikeres végrehajtása nem bizonyítja, hogy a
visszaállítás működni fog.

Az irányelveknek meg kell határozniuk:

* mely adatbázis-objektumokról és fájlokról készül biztonsági mentés;
* szerepelnek-e benne a csatolmányok;
* a biztonsági mentés gyakoriságát;
* a megőrzési időt;
* a tárolás helyét és földrajzi joghatóságát;
* a titkosítást és a hozzáférés-szabályozást;
* a biztonsági mentések sikerességének felügyeletéért való felelősséget;
* a visszaállítási prioritásokat és várható időtartamokat;
* a visszaállítási tesztek gyakoriságát; valamint
* mi történik a törölt vagy korlátozott adatokkal a megőrzött biztonsági
  mentésekben.

Az elérhető felhasználásifeltétel-példa szerint bizonyos
OpenBioMaps-szolgáltatások SQL-projekttábláiról naponta készül biztonsági
mentés, amelyeket két hétig őriznek meg, a csatolmányok azonban nem
szerepelnek a mentésben. Ezt az adott szerver ellenőrzése nélkül nem szabad
általános OpenBioMaps-garanciaként bemutatni.

.. TODO: Minden támogatott OpenBioMaps-szervertípus esetében külön meg kell
   erősíteni és dokumentálni a jelenlegi biztonsági mentési megoldásokat,
   beleértve a Docker-telepítéseket és a függetlenül üzemeltetett
   szervereket.

.. TODO: Tesztelt biztonságimentési és visszaállítási eljárást kell
   hozzáadni, amely kiterjed a PostgreSQL-adatbázisra, a
   projektkonfigurációra, a feltöltött csatolmányokra, a létrehozott
   fájlokra, az üzenetsablonokra, a modulokra, a háttérfolyamatokra és a
   térkép-konfigurációra.

.. TODO: Meg kell határozni a helyreállítási ponttal és a helyreállítási
   idővel kapcsolatos célkitűzéseket, valamint ütemtervet kell létrehozni a
   dokumentált visszaállítási tesztekhez.


Biztonság és incidenskezelés
============================

Az irányelveknek össze kell foglalniuk az adatok védelmére alkalmazott
szervezeti és műszaki intézkedéseket anélkül, hogy olyan információkat
tennének közzé, amelyek önmagukban gyengítenék a biztonságot.

A releváns szabályozási intézkedések a következők lehetnek:

* titkosított hálózati kapcsolatok;
* biztonságos hitelesítés és munkamenet-kezelés;
* a legkisebb jogosultság elvét követő csoport- és adminisztratív
  hozzáférés;
* védett adatbázis- és API-hitelesítési adatok;
* szerver- és függőségfrissítések;
* naplózás és felügyelet;
* a biztonsági mentések védelme;
* a végrehajtható háttérfolyamatokra vonatkozó korlátozások;
* fájltípus- és csatolmánykezelési szabályok;
* rendszeres hozzáférés-felülvizsgálatok; valamint
* sérülékenység- és incidenskezelés.

Egy dokumentált incidenseljárásnak meg kell határoznia, hogyan jelentik és
kezelik a feltételezett jogosulatlan hozzáférést, véletlen közzétételt,
adatvesztést, rosszindulatú feltöltéseket, kompromittált hitelesítési
adatokat vagy hibás hozzáférési szabályokat.

.. TODO: Meg kell határozni a szerverüzemeltető és a projektüzemeltető
   biztonsági felelősségeit, beleértve a javításokat, a felügyeletet, a
   hitelesítési adatok kezelését, a hozzáférés felülvizsgálatát és az
   incidensekkel kapcsolatos kommunikációt.

.. TODO: Incidenskezelési folyamatot kell hozzáadni, amely kiterjed az
   észlelésre, a korlátozásra, a bizonyítékok megőrzésére, a
   kockázatértékelésre, a javításra, az értesítésre, a helyreállításra és
   az incidens utáni felülvizsgálatra.

.. TODO: Dokumentálni kell, hogyan jelenthetnek a projektadminisztrátorok
   biztonságosan egy sérülékenységet anélkül, hogy nyilvános
   hibajelentési csatornán tennék közzé.


Az irányelvek módosítása
========================

Az irányelveknek tartalmazniuk kell a verziószámot, a közzététel és a
hatálybalépés dátumát, a felelős szerkesztőt és a változási előzményeket. A
lényeges módosításokat szükség esetén hatálybalépésük előtt közölni kell.

A projektnek meg kell határoznia:

* ki hagyhatja jóvá az irányelvek módosítását;
* hogyan értesítik az érintett felhasználókat;
* szükséges-e az ismételt elfogadás;
* hogyan rögzítik az elfogadást;
* hogyan maradnak hozzáférhetők a korábbi verziók; valamint
* mi történik, ha egy adatközlő vagy felhasználó elutasítja az új
  feltételeket.

A műszaki hozzáférési beállítások, licencek, megőrzési idők, célok vagy
felelős szervezetek megváltozása esetén felül kell vizsgálni az
irányelveket.

.. TODO: Dokumentálni kell, hogy az OpenBioMaps képes-e rögzíteni a
   feltételek vagy irányelvek egyes felhasználók által elfogadott verzióját,
   és lényeges módosítás után új elfogadást kérni.

.. TODO: Verziókezelési és közzétételi folyamatot kell meghatározni a
   szerver egészére vonatkozó és a projektspecifikus irányelvekhez.


A projektszabályzat javasolt szerkezete
=======================================

Egy projektspecifikus szabályzat a következő szerkezetet használhatja:

#. **Dokumentuminformációk** — cím, verzió, tulajdonos, jóváhagyás dátuma,
   hatálybalépés dátuma és felülvizsgálat dátuma.
#. **A projekt azonosítása és célja** — projektnév, szerver, hatókör és
   tervezett felhasználás.
#. **Kapcsolattartók és felelősségek** — szerverüzemeltető,
   projektüzemeltető, adatgazda és a kérelmek kapcsolattartói.
#. **Fogalommeghatározások** — projektspecifikus terminológia.
#. **Gyűjtött adatok** — rekordok, metaadatok, csatolmányok, származás és
   személyes adatok.
#. **Beküldési szabályok** — jogosult adatközlők, elfogadott források és az
   adatközlők felelősségei.
#. **Minőségkezelés** — validálás, javítás, előzmények és minősítések.
#. **Hozzáférési besorolás** — nyilvános, hitelesített,
   csoportkorlátozásos, érzékeny és embargó alatt álló adatok.
#. **Jogok és licencek** — az adatközlők által adott engedélyek és a
   címzettek általi újrafelhasználás.
#. **Hivatkozás és forrásmegjelölés** — előnyben részesített hivatkozások és
   állandó azonosítók.
#. **Kérelmek és külső megosztás** — exportok, integrációk és jóváhagyási
   munkafolyamatok.
#. **Megőrzés és archiválás** — aktív megőrzés, törlés, biztonsági mentések
   és projektlezárás.
#. **Adatvédelem és biztonság** — hivatkozások az adatvédelmi tájékoztatóra
   és az incidenskezelési folyamatra.
#. **Panaszok és kérelmek** — kapcsolattartók és válaszadási eljárás.
#. **Az irányelvek módosítása** — jóváhagyás, értesítés, elfogadás és
   verzióelőzmények.

.. TODO: Ezt a szerkezetet külön letölthető szabályzatsablonná kell
   alakítani, egyértelműen megjelölt kötelező és opcionális
   rendelkezésekkel.

.. TODO: Példaszöveget csak azután szabad hozzáadni, hogy minden példát
   ellenőriztek a jelenlegi OpenBioMaps-funkciókkal, és felülvizsgáltak
   azokban a joghatóságokban, amelyekben használni kívánják.


Megvalósítási ellenőrzőlista
============================

A projekt adatkezelési irányelveinek közzététele előtt a
projektüzemeltetőnek ellenőriznie kell, hogy:

* a projekt célja és hatóköre pontos;
* a felelős szervezetek és kapcsolattartók adatai naprakészek;
* a műszaki szerepkörök megfelelnek a meghatározott felelősségeknek;
* a feltöltési űrlapok csak a kívánt adatokat gyűjtik;
* a szükséges metaadatokat és származási információkat rögzítik;
* a validálási állapotok és minőségi nyilatkozatok érthetők;
* tesztelték a nyilvános, hitelesített és csoportos hozzáférést;
* a térkép-, lekérdezés-, API-, export-, csatolmány- és SQL-hozzáférés
  következetesen működik;
* az érzékeny rekordok és mezők megkapják a kívánt védelmet;
* a licencek és a forrásmegjelölés szerepelnek az exportokban;
* a személyes adatok kezelése megfelel az adatvédelmi tájékoztatónak;
* a megőrzési és törlési állítások megfelelnek a rendszer tényleges
  működésének;
* a biztonsági mentések tartalmazzák a megígért adatbázis-objektumokat és
  fájlokat;
* elvégeztek egy visszaállítási tesztet;
* dokumentálták a külső integrációkat;
* figyelemmel kísérik az incidensekhez és kérelmekhez megadott
  kapcsolattartási csatornákat;
* az irányelvek hatályos verziója elérhető a felhasználók számára; valamint
* meghatározták a következő felülvizsgálat dátumát.

Az irányelveket valós munkafolyamatokon kell tesztelni, nem elegendő
kizárólag szövegként felülvizsgálni őket. Az adminisztrátoroknak különösen
reprezentatív fiókok használatával kell tesztelniük a feltöltési,
lekérdezési, térképi, letöltési, API-, csatolmány-, javítási és törlési
műveleteket.

.. TODO: Automatikus vagy adminisztrátor által támogatott auditjelentést
   kell kidolgozni, amely összehasonlítja a közzétett projektirányelveket a
   hozzáférési beállításokkal, az engedélyezett modulokkal, az
   exportútvonalakkal, a megőrzési beállításokkal és a külső
   integrációkkal.


Nyitott kérdések
================

Több területet is tisztázni kell az OpenBioMaps alkalmazás- és irányítási
modelljében, mielőtt ez az oldal teljesnek tekinthető:

* a szerverüzemeltetők és a projektüzemeltetők közötti pontos kapcsolat;
* a projekt- és adatkezelési szerepkörök mérvadó meghatározásai;
* a teljes hozzáférés-feloldási algoritmus;
* a licencek és szabályzatverziók tárolása és megjelenítése;
* az audit- és előzményinformációk hatóköre és megőrzése;
* a biodiverzitási rekordokban szereplő személyes adatok kezelése;
* az egyes felületek pontos törlési működése;
* a biztonsági mentések tartalma és a visszaállítási garanciák;
* a javítások és törlések továbbítása külső rendszerekbe; valamint
* egy projekt lezárásának vagy átadásának támogatott életciklusa.

.. TODO: Ezeket a kérdéseket az OpenBioMaps karbantartóival,
   szerverüzemeltetőivel, reprezentatív projektadminisztrátorokkal és
   megfelelő jogi vagy adatirányítási szakértőkkel kell tisztázni. A
   megoldott TODO blokkokat tesztelt, verzióspecifikus dokumentációval kell
   helyettesíteni.
