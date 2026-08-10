Gyakran ismételt kérdések
*************************

Általános információk
=====================

Mi az OpenBioMaps?
------------------

Az OpenBioMaps egy nyílt forráskódú szoftverplatform és szolgáltatásgyűjtemény
biológiai adatok kezeléséhez. Segítségével adatbázis-alapú projektek hozhatók
létre, amelyeket több felhasználó egyidejűleg, különböző eszközökről és eltérő
jogosultsági szintekkel érhet el.

A szervezetek saját OpenBioMaps-szervert üzemeltethetnek. Egyes intézmények
üzemeltetett OpenBioMaps-szolgáltatásokat is biztosítanak kutatási vagy
közösségi tudományos projektek számára, így a projekteknek nem feltétlenül
kell saját szervert fenntartaniuk. Az elérhetőség, a jogosultsági feltételek
és a támogatás feltételei az üzemeltető intézménytől függnek.

Mi az OpenBioMaps Consortium?
-----------------------------

Az OpenBioMaps Consortium koordinálja a platformmal és annak fejlesztésével
kapcsolatos együttműködést.

További információkért lásd: :doc:`Az OpenBioMaps Consortium <consortium>`.

Hol találhatók meglévő OpenBioMaps-szerverek?
---------------------------------------------

A regisztrált szerverek az
`OpenBioMaps hálózati adatbázisában
<https://openbiomaps.org/projects/openbiomaps_network>`_ találhatók.

Előfordulhat, hogy a lista nem tartalmaz minden önállóan üzemeltetett
OpenBioMaps-szervert.

Projektek és regisztráció
=========================

Hogyan találhatok vagy hozhatok létre adatbázisprojektet?
---------------------------------------------------------

A meglévő projektek az OpenBioMaps-szerver projektlistáján vagy a szervert
üzemeltető szervezet által biztosított információk alapján találhatók meg.

Ha már tagja egy projektnek, a szerver lehetővé teheti, hogy a webes felületen
keresztül új adatbázisprojektet igényeljen vagy hozzon létre. A pontos eljárás
és a szükséges jogosultságok a szerver konfigurációjától függnek. Ha a
projektlétrehozási funkció nem érhető el a fiókjával, forduljon a
szerveradminisztrátorhoz.

Hogyan regisztrálhatok egy OpenBioMaps-projektbe?
-------------------------------------------------

A regisztrációhoz általában meghívó szükséges. A projekt konfigurációjától
függően a meglévő tagok vagy kizárólag az adminisztrátorok kaphatnak
jogosultságot új felhasználók meghívására.

A projektek a bejelentkezési oldalukon meghívásigénylő űrlapot is
biztosíthatnak. Ez lehetővé teszi, hogy a leendő felhasználók hozzáférést
kérjenek a projektadminisztrátoroktól, de az igénylés elküldése nem biztosít
automatikusan tagságot.

Egyes szerverek külső OpenID Connect-szolgáltatón, például a Google
szolgáltatásán keresztüli regisztrációt vagy bejelentkezést is támogatnak. Az
elérhető szolgáltatók és az, hogy létrehozható-e rajtuk keresztül új fiók, a
szerver és a projekt konfigurációjától függ.

Egy adott projekthez való csatlakozással kapcsolatos információkért forduljon
annak létrehozóihoz vagy adminisztrátoraihoz.

Adatfeltöltés és hozzáférés
===========================

Hogyan tölthetek fel adatokat?
------------------------------

A szokásos módszer egy projektspecifikus adatfeltöltési űrlap használata. Az
űrlapok a webes felületen, valamint ha a projekt támogatja, egy OpenBioMaps
mobilalkalmazáson keresztül használhatók.

Az űrlapok konfigurációjáról lásd:
:doc:`Feltöltési űrlapok kezelése <upload_forms>`.

Nagy méretű vagy speciális importálások PostgreSQL-klienssel is
végrehajthatók. Közvetlen adatbázis-importálást csak tapasztalt, megfelelő
jogosultságokkal rendelkező felhasználók végezhetnek, mert ezek a műveletek
megkerülhetik az alkalmazásszintű ellenőrzést és a feltöltési
munkafolyamatokat.

Hogyan férhetek hozzá az adatokhoz?
-----------------------------------

A projekt konfigurációjától és az Ön jogosultságaitól függően az adatok több
módon is elérhetők:

* a webes felületen végzett térképes vagy szöveges lekérdezésekkel;
* a webes felület letöltési és exportálási funkcióival;
* adatmegosztási funkciókkal;
* PostgreSQL-klienssel;
* QGIS vagy más kompatibilis GIS-kliens használatával;
* OpenBioMaps API-n keresztül;
* az OpenBioMaps R-csomaggal; vagy
* a :doc:`PWA térképes lekérdezőalkalmazással <pwa>`.

További információkért lásd: :doc:`Adathozzáférés <data_access>`,
:doc:`API-dokumentáció <api>` és :doc:`Kliensek <clients>`.

Milyen adatletöltési lehetőségek érhetők el?
--------------------------------------------

Az elérhető letöltési módszerek a projektben engedélyezett moduloktól és az
aktuális felhasználó jogosultságaitól függnek. Ezek a következők lehetnek:

* CSV-, JSON-, KML-, GPX-, SHP- és más exportmodulok;
* hozzáférés QGIS vagy más PostgreSQL/PostGIS-kliens használatával;
* könyvjelzők, mentett lekérdezések és állandó hivatkozások;
* API-alapú lekérés; valamint
* az OpenBioMaps R-csomag.

Egyes projektek jóváhagyáshoz kötik a letöltések elérhetővé tételét. Az
exportokra továbbra is érvényesek a projekt rekord- és oszlopszintű
hozzáférési szabályai.

Miért láthatnak más felhasználók olyan adatokat, amelyeket én nem tudok lekérdezni?
-----------------------------------------------------------------------------------

A rekordok valószínűleg meghatározott felhasználókra vagy csoportokra vannak
korlátozva. A projekt feltöltési űrlapjának beállításai meghatározhatják, hogy
az adott űrlappal feltöltött rekordokhoz kik kapnak olvasási vagy módosítási
hozzáférést.

Ha a rekordokat megfelelő hozzáférési beállítások nélkül töltik fel,
előfordulhat, hogy csak a projektadminisztrátorok láthatják őket. A
projektadminisztrátorok később módosíthatják a hozzáférési szabályokat, a
pontos eljárás azonban a projekt adatbázissémájától és szabálykonfigurációjától
függ.

A következő szemléltető SQL-példa hozzáadja a ``295`` numerikus
szerepkör-azonosítót a kiválasztott rekordok olvasási hozzáférési tömbjéhez:

.. code-block:: sql

   UPDATE mydatabase_rules AS rules
   SET read = rules.read || 295
   FROM (
       SELECT data.obm_id AS row_id
       FROM public.mydatabase AS data
       LEFT JOIN mydatabase_rules AS existing_rules
           ON data.obm_id = existing_rules.row_id
       WHERE data.observer ILIKE 'Smith%'
   ) AS selected
   WHERE selected.row_id = rules.row_id;

Cserélje le az összes tábla- és oszlopnevet, feltételt és
szerepkör-azonosítót a projektnek megfelelő értékekre.

Ez a példa csak azokat a rekordokat frissíti, amelyekhez már tartozik
megfelelő szabályrekord. Nem hozza létre a hiányzó szabályokat. Ugyanazt a
szerepkört többször is hozzáfűzheti, ha az már megtalálható a tömbben.

Hozzon létre biztonsági mentést, és vizsgálja meg az érintett rekordokat a
hozzáférési szabályok frissítése előtt. Amikor csak lehetséges, támogatott
adminisztrációs felületen keresztül végezze el a módosítást. A helytelen
SQL-módosítások nem szándékosan hozzáférhetővé tehetik vagy korlátozhatják a
projektadatokat.

Mobilhozzáférés
===============

Hogyan kérhetek le adatokat mobileszközzel?
-------------------------------------------

A :doc:`PWA térképes lekérdezőalkalmazás <pwa>` képes lekérdezni a projekt
rekordjait, és offline is elérhetővé teheti a korábban lekért rekordokat.
Elérhetősége és konfigurációja a projekttől függ.

Az OpenBioMaps terepi adatgyűjtéshez készült mobilalkalmazásokat is biztosít.
Az elérhető lehetőségekről lásd:
:doc:`Mobilalkalmazások <mobile_applications>`.

Hogyan használhatom az OpenBioMaps mobilalkalmazást?
----------------------------------------------------

Az offline mobilalkalmazás Android- és iOS-eszközökhöz készült. A használat
megkezdéséhez:

#. Válassza ki a projektet üzemeltető OpenBioMaps-szervert.
#. Válassza ki a projektet.
#. Jelentkezzen be a projektben használt fiókjával.
#. Online állapotban nyissa meg a szükséges adatgyűjtési űrlapokat, hogy azok
   letöltődjenek az eszközre.
#. Az űrlapok sikeres letöltése után használja őket offline adatgyűjtésre.
#. Kapcsolódjon újra a hálózathoz, és szinkronizálja az összegyűjtött
   rekordokat a szerverrel.

Az alkalmazásban megjelenő szerverek és projektek a regisztrált szerverektől,
a szerver konfigurációjától és a felhasználó hozzáférési jogosultságaitól
függnek.

A korábban megtekintett alaptérképcsempék elérhetők maradhatnak az eszköz
vagy a böngésző gyorsítótárában, de az alaptérképek offline elérhetősége nem
garantált, kivéve, ha az alkalmazás és a térképszolgáltató kifejezetten
támogatja a térképek offline használathoz történő letöltését.

A részletes utasításokért és korlátozásokért lásd:
:doc:`Mobilalkalmazások <mobile_applications>`.

Hogyan férhetek hozzá a mobilalkalmazással készített fényképekhez?
------------------------------------------------------------------

A jogosultságaitól és a projekt konfigurációjától függően a mellékletek a
következő módokon érhetők el:

* egyenként, egy rekord adatlapjáról;
* a projektadminisztrációs felület fájlokat tartalmazó lapjáról;
* az elérhető tömeges letöltési funkcióval;
* mellékletek letöltését támogató API-n keresztül; vagy
* a Supervisorban, a jogosultsággal rendelkező adminisztrátorok számára
  elérhető projektfájl-kezelési funkciókkal.

A pontos lehetőségek az engedélyezett moduloktól és az OpenBioMaps verziójától
függnek. A fényképek érzékeny helyadatokat, projektinformációkat vagy személyes
adatokat tartalmazhatnak, ezért a letöltött fájlokat biztonságosan kell
tárolni és megosztani.

Fejlesztői felületek és kliensek
================================

Van programozható felület a fejlesztők számára?
-----------------------------------------------

Igen. Az OpenBioMaps API-kat biztosít a projekt- és felhasználói adatok
eléréséhez, a hitelesítési és projektjogosultságok figyelembevételével.

A Project Data Service (PDS) URL-alapú kéréseket támogat. A következő kérés
például visszaadja a szerveren elérhető projektlistát:

``https://openbiomaps.org/pds.php?scope=get_project_list``

A támogatott végpontokról, a hitelesítési követelményekről, a paraméterekről
és a válaszformátumokról lásd: :doc:`API-dokumentáció <api>`.

Hol található az OpenBioMaps R-csomag?
--------------------------------------

Az OpenBioMaps R-csomag fejlesztői verziója az
`OpenBioMaps obm.r kódtárolójában
<https://github.com/OpenBioMaps/obm.r>`_ érhető el.

Éles munkafolyamatban történő használat előtt ellenőrizze a kódtároló
dokumentációjában a telepítési utasításokat, az aktuális állapotot és a
kompatibilitási információkat.

Nyelvek és közreműködés
=======================

Milyen nyelveket támogat az OpenBioMaps?
----------------------------------------

Az OpenBioMaps lefordított felhasználói felületek és projektspecifikus
tartalmak támogatására készült. Az egyes fordítások teljessége eltérhet az
alkalmazás összetevői és kiadásai között.

A platform jelenleg több nyelv fordítását tartalmazza, köztük a magyar, angol,
román, spanyol, portugál, orosz, német és francia nyelvét. Egyes fordítások
hiányosak lehetnek.

Az egyes projektek kiválaszthatják saját nyelveiket, és fordításokat
biztosíthatnak a projektspecifikus címkékhez és tartalmakhoz.

Fordításokat az
`OpenBioMaps fordítási platformján
<https://translate.openbiomaps.org>`_ lehet beküldeni.

Hogyan járulhatok hozzá az OpenBioMaps fejlesztéséhez?
------------------------------------------------------

A következő módokon járulhat hozzá:

* OpenBioMaps-adatbázisprojekt létrehozásával vagy karbantartásával;
* adatok gyűjtésével vagy projektbe történő feltöltésével;
* OpenBioMaps-szerver üzemeltetésével;
* projektek saját szerveren történő üzemeltetésével;
* új fordítások hozzáadásával vagy a meglévők javításával;
* a dokumentáció javításával;
* hibák bejelentésével és kivizsgálásával;
* szoftverfejlesztési közreműködéssel; vagy
* pénzügyi támogatással.

Adatok vagy kód beküldése előtt tekintse át az érintett projekt szabályzatait
és a megfelelő forráskód-tároló közreműködési követelményeit.

Kell fizetnem az OpenBioMaps használatáért?
-------------------------------------------

Az OpenBioMaps szoftvere nyílt forráskódú, és szoftverlicencdíj nélkül
használható. A szerverüzemeltetésnek, a projektspecifikus funkciók
fejlesztésének, az adatok tárolásának, a támogatás biztosításának és az
infrastruktúra karbantartásának azonban lehetnek költségei.

Egyes intézmények díjmentesen üzemeltetnek megfelelő projekteket, míg mások
saját feltételeket vagy szolgáltatási díjakat alkalmazhatnak. A részletekért
forduljon az érintett szerver üzemeltetőjéhez.

A fejlesztés és a karbantartás önkéntes és finanszírozott munkát egyaránt
magában foglal. Az OpenBioMaps fejlesztéséhez nyújtott pénzügyi és természetbeni
hozzájárulásokat egyaránt szívesen fogadjuk.

Tárolás, biztonsági mentés és fiók-helyreállítás
================================================

Hol tárolja az OpenBioMaps az adatokat?
---------------------------------------

Minden OpenBioMaps-szerver a saját PostgreSQL-adatbázisaiban és
fájltárhelyén tárolja projektadatait. Ezek közé tartozhatnak az
adatbázisrekordok, a mellékletek, a projektkonfiguráció, a térképfájlok, a
naplók és a létrehozott exportok.

Az OpenBioMaps nem tart fenn egyetlen központi adatbázist, amely minden
szerver összes adatát tartalmazza.

Van biztonsági mentési megoldás?
--------------------------------

Nincs minden OpenBioMaps-telepítésre kiterjedő központi biztonsági mentési
szolgáltatás, mert az adatkezelés decentralizált. Minden szerverüzemeltető
felelős a megfelelő biztonsági mentési eljárás megvalósításáért,
monitorozásáért és teszteléséért.

Egyes szerverüzemeltetők úgy működnek együtt, hogy titkosított vagy
hozzáférés-vezérelt archívumokat tárolnak egymás infrastruktúráján. A
biztonsági mentési megállapodások szerverenként eltérnek.

A projekttulajdonosoknak a következőkről érdemes megkérdezniük
szerverüzemeltetőjüket:

* a biztonsági mentések gyakorisága és megőrzési ideje;
* az adatbázisok, mellékletek és konfigurációs fájlok mentésbe foglalása;
* a külső helyszínen történő tárolás;
* a titkosítás és a hozzáférés-vezérlés; valamint
* a visszaállítás tesztelésének gyakorisága.

A biztonsági mentés nem tekinthető ellenőrzöttnek, amíg nem állították
sikeresen vissza tesztkörnyezetben.

Elvesztettem a jelszavamat. Hogyan állíthatok be újat?
------------------------------------------------------

Használja a bejelentkezési oldalon található **Lost password** hivatkozást.

Adja meg a fiókjához tartozó e-mail-címet, és küldje el az űrlapot. Ha a
szerver képes e-mailt küldeni, és a cím egy fiókhoz tartozik, a rendszer egy
hivatkozást küld, amelynek használatával hozzáférhet a fiókhoz, és új jelszót
állíthat be.

Ha az üzenet nem érkezik meg:

* ellenőrizze a spam vagy levélszemét mappát;
* ellenőrizze, hogy helyesen adta-e meg az e-mail-címet;
* várjon néhány percet, mielőtt újabb üzenetet igényel; valamint
* forduljon a projekt- vagy szerveradminisztrátorhoz.

Biztonsági okokból előfordulhat, hogy a felület nem erősíti meg, hogy az
e-mail-cím regisztrálva van-e.

Hibaelhárítás
=============

Miért jelennek meg rózsaszín négyzetek a térképen?
--------------------------------------------------

A rózsaszín négyzetek általában azt jelzik, hogy egy térképcsempét vagy
réteget nem sikerült megjeleníteni. Lehetséges okok:

* hiba egy MapServer mapfile-ban;
* érvénytelen vagy nem elérhető adatforrás;
* helytelen adatbázis-hitelesítési adatok vagy hálózati beállítások;
* vetületi vagy geometriával kapcsolatos probléma;
* helytelen rétegnév;
* MapServer- vagy MapCache-hiba; vagy
* érvénytelen térképes lekérdezési konfiguráció.

Próbálja meg újratölteni az oldalt, és ellenőrizze, hogy a probléma minden
réteget vagy csak egyetlen réteget érint-e. A projekt- vagy
szerveradminisztrátoroknak meg kell vizsgálniuk az alkalmazás és a MapServer
naplóit, valamint ellenőrizniük kell az érintett mapfile érvényességét.

Adatkezelés
===========

Hogyan törölhetek adatokat?
---------------------------

Előfordulhat, hogy a szabványos OpenBioMaps webes felület nem biztosít
általános célú rekordtörlési funkciót. Ha törlésre van szükség, egy
jogosultsággal rendelkező adatbázis-adminisztrátor SQL vagy más támogatott
adminisztratív munkafolyamat használatával távolíthatja el a rekordokat.

Minden feltöltéshez tartozik egy bejegyzés a rendszer feltöltési
metaadataiban. Egy projekttábla rekordjai egy feltöltési azonosító
használatával hivatkozhatnak erre a feltöltésre. Ha egy megfelelően beállított,
kaszkádolt törlést alkalmazó idegen kulcs összekapcsolja a metaadatokat és az
adattáblákat, a metaadatrekord törlése a kapcsolódó rekordokat is törölheti.
Nem garantált, hogy ez a kapcsolat létezik, ezért az adatbázisséma vizsgálata
nélkül ne hagyatkozzon a kaszkádolt törlésre.

Általában biztonságosabb azonosítani és kifejezetten törölni a szükséges
rekordokat. Például:

.. code-block:: sql

   DELETE FROM your_table
   WHERE uploading_id = x;

Cserélje le a ``your_table``, ``uploading_id`` és ``x`` értékét a projektben
használt tényleges táblára, feltöltési hivatkozási oszlopra és feltöltési
azonosítóra.

Törlés végrehajtása előtt:

#. Hozzon létre és ellenőrizzen egy adatbázis-biztonsági mentést.
#. Futtasson egyenértékű ``SELECT`` lekérdezést, és vizsgáljon meg minden
   érintett rekordot.
#. Ellenőrizze a kapcsolódó táblákat, mellékleteket, szabályokat és
   auditkövetelményeket.
#. Amikor célszerű, hajtsa végre a műveletet tranzakcióban.
#. A tranzakció véglegesítése előtt ellenőrizze az eredményt.
#. Rögzítse, hogy ki és miért végezte el a törlést.

A törlés hatással lehet az auditálási előzményekre, a hozzáférési szabályok
rekordjaira, a mellékletekre, a kapcsolódó rekordokra, az összesítésekre és a
külső másolatokra. Az adatok végleges eltávolítása előtt tekintse át a projekt
adatszabályzatát és megőrzési követelményeit.

RUM nyitottsági modell
======================

Mi a RUM?
---------

A RUM a biodiverzitási adatbázisok működési képességeinek és nyitottságának
leírására szolgáló RUM/FILH-modell része. Lásd a
`RUM/FILH: a biodiverzitási adatbázisok szabványosított működésiképesség-modellje
<https://doi.org/10.1093/database/baag044>`_ című publikációt.

A RUM jelentése:

* **R — Read**
* **U — Upload**
* **M — Modify**

Mindegyik képesség három érték egyikét veheti fel:

.. list-table::
   :header-rows: 1
   :widths: 15 30 55

   * - Érték
     - Jelentés
     - Hagyományos megjelenítési szín
   * - ``-``
     - Nem nyilvános
     - Fekete
   * - ``0``
     - Részben nyilvános
     - Piros
   * - ``+``
     - Nyilvános
     - Zöld

Egy adatbázis például részben nyilvános olvasási hozzáférést, nyilvános
feltöltési hozzáférést és nem nyilvános módosítási hozzáférést biztosíthat. A
három képességet mindig a projekt részletes hozzáférési szabályzatával együtt
kell értelmezni.

DOI-k és hivatkozás
===================

Rendelhető DOI egy adatbázishoz?
--------------------------------

Igen. Egy megfelelően stabil és dokumentált állapotban lévő adatbázishoz vagy
meghatározott adatkészlethez DOI rendelhető a DataCite DOI-szolgáltatáson
keresztül, az OpenBioMaps-szervert üzemeltető szervezet eljárásának
megfelelően.

Az OpenBioMaps-adatbázisok DOI-metaadatoldalt biztosíthatnak. Például:

``https://dinpi.openbiomaps.org/projects/danubefish/index.php?metadata``

Az OpenBioMaps DataCite-előtagja ``10.18426``. A DOI-utótagok egyedileg
jönnek létre.

Egy projekt további DOI-kat is rendelhet az egyes adatkészletekhez. DOI
létrehozása előtt ellenőrizze az adatkészlet verzióját, szerzőit, címét,
kiadási évét, licencét, hozzáférési feltételeit, kiadóját és a céloldal
tartósságát. A DOI-nak olyan állandó céloldalra kell mutatnia, amely elegendő
metaadatot és hozzáférési információt tartalmaz.
