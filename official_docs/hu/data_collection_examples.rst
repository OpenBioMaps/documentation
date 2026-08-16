:szerző: Bán Miklós
:dátum: 2026.08.16

Mintavétel egy madárodú-telepen
*******************************

Ez a példa egy lehetséges adatbázis-szerkezetet és adatbeviteli munkafolyamatot ismertet egy madárodú telepen zajló fészkelési tevékenység nyomon követéséhez. Példánk hasznos keretrendszert nyújt, például ha több éven át szeretnénk nyomon követni a fészkelőhelyen bekövetkező fészkelési siker változásait, vagy ha viselkedéskutatásokat végzünk, és szeretnénk mérni kiválasztott egyedek viselkedési reakcióit vagy fészkelési sikerét más egyedekhez viszonyítva, valamint különböző években és különböző kezelések mentén.

Bemutatja, hogyan tárolhatók a statikus adatok, az időfüggő információk és megfigyelések egymáshoz kapcsolódó táblákban, ahelyett, hogy egyetlen, nagyon széles táblában vagy táblázatkezelő programokban próbálnánk kezelni.

Általános útmutatást az adatgyűjtés tervezéséhez, valamint az
entitások és kapcsolatok ábrázolásához lásd: :doc:`Adatgyűjtés <data_collection>`.
A megfigyelési események és az alkalmi megfigyelések közötti különbség magyarázatát lásd:
:doc:`Megfigyelési események és alkalmi megfigyelések <observation_events>`.


A fő entitások meghatározása
============================

Ahhoz, hogy egy madárház-telephelyen dolgozhassunk, olyan adatbázis-szerkezetre van szükségünk, amely alkalmas
mind a madárházak, mind a bennük zajló fészkelési tevékenység
nyilvántartására. Ha karbantartási munkákat végeznek a madárházakon,
a szerkezetnek ezt is képesnek kell lennie ábrázolni.

A különböző típusú információkat ezért külön
táblákban kell tárolni. Lesz egy táblánk a fészekdobozokhoz, egy másik az
időfüggő állapotukhoz és elhelyezkedésükhöz, egy harmadik a fészkelési eseményekhez, és egy
negyedik a fiókák gondozásához vagy a karbantartási tevékenységekhez. Ezek a táblák
összekapcsolódnak egymással, de nem ajánlott őket egyetlen,
nagyon széles táblában kezelni. Ehelyett több
kisebb, egymással kapcsolódó táblába kell szervezni őket.

.. TODO: Adjunk hozzá egy entitás-kapcsolat diagramot, amely bemutatja a négy javasolt
   táblát, azok elsődleges kulcsait, idegen kulcsait, valamint az egyes
   kapcsolatok kardinalitását.

.. TODO: Tisztázzuk, hogy a fészekdoboz-karbantartás és a fiókák gondozása
   ugyanazt a tevékenységtípust jelenti-e. Ha különálló fogalmakról van szó, használjunk külön
   táblákat, vagy magyarázzuk el, mely műveletek tartoznak az egyes fogalmakhoz.


A madárház-nyilvántartás létrehozása
==============================

Első feladatunk a madárház-nyilvántartás létrehozása. Nyomon kell követnünk az
egyes madárházakra vonatkozóan rögzített információkat, beleértve azt is, hogy a madárházat hogyan azonosítják
a terepen, mikor telepítették, és hogy még mindig ott van-e, vagy már
eltávolították.

Ha véletlenül ugyanazt a terepi azonosító számot rendelnék hozzá
két fészekdobozhoz, be kell vezetnünk egy belső azonosítót is, amely
minden fészekdoboz esetében garantáltan egyedi. Célszerű lenne biztosítani,
hogy egy terepi azonosító, például a 102-es szám, ne jelenjen meg két különálló
fészekdobozon, de ezt nagy fészekdoboz-kolóniában
nehéz lehet garantálni.

Alternatív megoldásként minden fészekdobozhoz csatolhatnánk egy
további azonosítót, amelyet úgy terveznének, hogy csak közelről legyen
olvasható. Ez lehetne például egy egyedi gyártású fémtáblára
vésett szám, amely biztosítja, hogy ne legyen két egyforma
tábla. Ha ilyen rendszert alkalmazunk, mind a terepi azonosítót, mind
az egyedi azonosítót fel kell venni a fészekdoboz-nyilvántartásba.

A stabil azonosítókat nem szabad kizárólag címkékből, koordinátákból
vagy más, változásnak kitett értékekből levezetni. Az azonosítókról és
a táblázatok közötti kapcsolatokról további információkért lásd
:ref:`Táblázatok és kapcsolatok <data-collection-tables-and-relationships>`.

.. TODO: Adja hozzá a ``data-collection-tables-and-relationships`` hivatkozási
   címkét a ``data_collection.rst`` fájl „Táblák és kapcsolatok” szakaszához,
   ha az a szakasz még nem tartalmaz stabil Sphinx-célt.
   Alternatív megoldásként cserélje ki a fenti hivatkozást egy dokumentumszintű linkre.

.. TODO: Adja meg, hogy a belső fészekdoboz-azonosítót a
   PostgreSQL generálja-e, vagy a projekt biztosítja-e. Adjon meg példaértékeket, és magyarázza el,
   melyik azonosító jelenik meg a terepen dolgozók számára, és melyiket
   használják a külső kulcs kapcsolatokban.


A stabil és az időfüggő információk elkülönítése
================================================

Előfordulhat, hogy egy fészekdoboz nem mindig aktív, vagy akár nem is található meg a helyszínen. Előfordulhat, hogy
felújítás céljából eltávolítják, és egy egész szezonra kint hagyják. Állapotát
ezért nem mindig lehet egyetlen logikai értékkel kifejezni. Ehelyett
az állapotot egy dátumhoz vagy időintervallumhoz kell társítani, és több
állapotrögzítésre is szükség lehet ahhoz, hogy utólag meg lehessen állapítani, mikor volt aktív
a fészekdoboz, és mikor nem.

Emiatt a fészekdoboz-nyilvántartásunk két egymással összefüggő táblából áll:

* egy *fészekalap* táblázat, amely minden egyes fizikai fészekdobozra
  vonatkozó állandó információkat tartalmaz; és
* egy *fészeknyilvántartás* táblázat, amely a dobozra vonatkozó
  időfüggő információkat tartalmaz, például a felszerelést, az állapotot és a helyszínt.

A *fészekalap* táblának nem kell állapotinformációkat tárolnia. Ez a táblázat a
fészekdoboz egyedi azonosítóját tárolja, és tartalmazhatja a
gyártás dátumát, valamint olyan tulajdonságokat is, mint például az anyagát, amelyből készült.

A fészekdoboz egyedi azonosítójára „UNIQUE” korlátozást kell alkalmazni.
A PostgreSQL egyedi korlátozásairól további információt a
`Egyedi korlátozások a PostgreSQL dokumentációjában
<https://www.postgresql.org/docs/current/ddl-constraints.html#DDL-CONSTRAINTS-UNIQUE-CONSTRAINTS>`_ című részben talál.

Ugyanez az egyedi fészekdoboz-azonosító megjelenik a *nest register*
táblában is. Ebben a táblában nem kell egyedinek lennie, mivel egy fészekdobozhoz
több állapotrekord is tartozhat. Az adatbázis azonban nem engedheti meg, hogy egy rekord
olyan fészekdobozra hivatkozzon, amely nem létezik a *nest base* táblában. Ezt a
kapcsolatot külső kulccsal érvényesítik. További információkért lásd
`Külső kulcs-korlátozások a PostgreSQL dokumentációjában
<https://www.postgresql.org/docs/current/ddl-constraints.html#DDL-CONSTRAINTS-FK>`_.

A *fészeknyilvántartás* táblázat a fészekdobozok telepítésére vonatkozó rekordokat és
egyéb, idővel változó információkat tartalmaz. Például minden évben hozzáadható
egy új sor minden fészekdobozhoz. Ennek a táblázatnak legalább egy
dátummezőt kell tartalmaznia, és általában tartalmaz egy mezőt is, amely a fészekdoboz
állapotát jelzi. Fontos továbbá egy térbeli helymeghatározó mező felvétele is, például egy
OpenBioMaps geometriai oszlop, amely a rögzített GPS-helyszínt tartalmazza.

A projekt táblák létrehozásával, az oszlopok regisztrálásával és a
szemantikai szerepek hozzárendelésével kapcsolatos útmutatást lásd
:ref:`Adatbázis-táblák és oszlopok <database-columns>`. Általános térbeli
adatokkal kapcsolatos útmutatást lásd az
:ref:`Hely és geometria <data-collection-location-and-geometry>`
szakaszt az adatgyűjtési dokumentációban.

.. TODO: Adja hozzá a ``data-collection-location-and-geometry`` hivatkozási címkét
   a ``data_collection.rst`` fájl „Hely és geometria” szakaszához, ha még
   nincs elérhető stabil cél. Alternatívaként használjon
   dokumentumszintű hivatkozást.

.. TODO: Határozza meg a javasolt állapotszókincset, például „telepítve”,
   „aktív”, „ideiglenesen eltávolítva”, „sérült”, „kicserélve” és
   „véglegesen eltávolítva”. Magyarázza el, mely átmenetek érvényesek, és hogy
   a lista bővíthető-e.

.. TODO: Döntse el, hogy az egyes állapotrekordok egy adott időpontban
   végzett megfigyelést, egy adott dátummal kezdődő állapotot, vagy egy kifejezett időtartamot
   jelentenek-e, kezdő és záró dátummal. Dokumentálja, hogyan kerül kiválasztásra a jelenlegi állapot,
   ha egy madárházhoz több rekord is létezik.

.. TEVENDŐ: Magyarázza el, hogy egy fészekdoboz áthelyezése új „nest-register”
   rekordot hoz-e létre ugyanarra a fizikai dobozra, vagy egy új „nest-base” rekordot. Magyarázza el továbbá,
   hogyan ábrázolják egy fizikai doboz másikra történő cseréjét ugyanazon a
   helyszínen.

Ha a kolónia 200 fészekdobozt tartalmaz, a *nest base* táblázat mérete
az évek során változatlan marad, feltéve, hogy nem kerülnek hozzá új fizikai dobozok. A *fészek-nyilvántartás* táblázat azonban évente 200 sorral
vagy akár ennél is többel növekedhet. Ez a növekedés várható, és nem jelent problémát. A táblázat
a kolónia történetét tartalmazza, és az egyes egyedi azonosítókhoz tartozó legfrissebb
rekord lekérdezése adja meg az aktuális állapotot.

.. TODO: Adjunk hozzá egy futtatható PostgreSQL-példát, amely visszaadja az egyes
   fészekdobozok aktuális állapotrekordját. A példának meg kell határoznia, hogyan kezelje az azonos értékeket,
   a hiányzó dátumokat, a jövőbeli dátumokat és az ugyanazon a napon történt többszörös változásokat.
   .


A fészkelési események rögzítése
=========================

A következő táblázat a *szaporodási események* táblája. Hasonlóan működik, mint egy
eseménynapló, és tartalmaz egy külső kulcsot, amely minden szaporodási eseményt összekapcsol a
vonatkozó fészekdoboz egyedi azonosítójával. Legalább egy
megfigyelési dátumot vagy dátum-idő mezőt kell tartalmaznia, a szaporodási esemény leírásához és elemzéséhez
szükséges további mezők mellett.

A mezőket annak megfelelően kell definiálni, hogy értékeiket hogyan fogják feldolgozni.
A számként kezelendő adatokat numerikus adatbázis-
oszlopokban kell tárolni. Például, ha az elemzéshez szükség van a tojások számára, azt
egész szám mezőben kell tárolni. Olyan értékeket, mint „körülbelül 8
tojás” vagy „tojások”, nem szabad elfogadni ebben a mezőben.

Ha az adatbázis-oszlop egész számként van definiálva, a terepmunka utáni
adatbevitel során csak érvényes egész számértékek fogadhatók el. Ha egy terepi jegyzet nem egyértelmű,
az adatgyűjtőnek vagy az adatbeviteli operátornak megfelelő
döntést kell hoznia és dokumentálnia, amíg a szükséges kontextus még rendelkezésre áll. Fél
évvel vagy több évvel később a kétértelműség már nem oldható meg,
és előfordulhat, hogy az értéket ki kell hagyni az elemzésből.

A mennyiségekről, mértékegységekről, kifejezett nem észlelésekről és
a mintavételi erőfeszítésről további információkért lásd: :doc:`Adatgyűjtés <data_collection>`.

.. TODO: Adjon meg egy javasolt minimális mezőkészletet a fészkelési eseményekhez, beleértve
   az esemény azonosítóját, a fészekdoboz azonosítóját, a megfigyelés dátumát és időpontját,
   a megfigyelőt, a taxont, a fészkelési állapotot, a tojásszámot, a fiókásszámot, a bizonyítékot,
   a megjegyzéseket és az érvényesítési állapotot.

.. TODO: Magyarázza el, hogyan kell ábrázolni a bizonytalan számlálási eredményeket. Például
   fontolja meg a numerikus számlálási eredmény tárolását a számlálási típustól vagy
   a bizonytalansági mezőtől elkülönítve, ahelyett, hogy hozzávetőleges szöveget engedélyezne a numerikus
   mezőben.

.. TODO: Pontosítsa, hogy egy sor egy fészekdobozhoz tett teljes látogatást,
   egy látogatás során egy taxon megfigyelését, vagy egy fészkelési állapotra
   vonatkozó megfigyelést jelöl-e. Ha egy látogatás több megfigyelést is tartalmazhat, fontolja meg
   a mintavételi esemény és az egyes megfigyelések szétválasztását,
   a :doc:`Megfigyelési események és alkalmi megfigyelések
   <observation_events>` című részben leírtak szerint.

.. TODO: Magyarázza el, hogyan kerülnek rögzítésre azok a befejezett látogatások, amelyek során nem történt fészkelési tevékenység, vagy nem
   észleltek állatot. Az ilyen rekordokat nem szabad kizárólag
   a fészkelési esemény sorának hiányából következtetni.


A fészekgondozási és karbantartási tevékenységek rögzítése
=====================================================

A negyedik táblázat a fészekkezelési vagy karbantartási tevékenységeket rögzíti.
Kapcsolatai eltérhetnek a többi tábláétól. Egyes műveletek
közvetlenül egy fizikai fészekdobozhoz kapcsolódhatnak, míg mások egy
konkrét szaporodási eseményhez. A táblázatnak ezért valószínűleg szüksége lesz egy
idegen kulcsra a *fészekalap* táblához, és szükség lehet egy idegen kulcsra a
*szaporodási események* táblához is.

Ezt a táblázatot itt *fészekgondozás* táblázatnak nevezzük.

.. TODO: Határozza meg a *fészekgondozás* táblában tárolt tevékenységeket, például
   a takarítást, javítást, cserét, tojáseltávolítást, gyűrűzést, mérést vagy
   áthelyezést. Különbséget kell tenni a fészekdobozok rutin karbantartása és az
   egy adott fészekaljra hatással lévő beavatkozások között.

.. TEVENDŐ: Döntsük el, mely kapcsolatok kötelezőek. Például minden
   karbantartási bejegyzéshez szükség lehet egy fészekdoboz-azonosítóra, míg csak
   a fészekaljra vonatkozó beavatkozásokhoz szükséges fészkelési esemény-azonosító.

.. TEVENDŐ: Vegye fel azokat a mezőket, amelyek szükségesek a beavatkozás okának,
   a felelős személynek, a dátumnak és időpontnak, az engedélyeknek vagy jóváhagyásoknak,
   az elvégzett műveletnek, annak eredményének és az esetleges alátámasztó bizonyítékoknak a dokumentálásához.


A struktúra megvalósítása az OpenBioMaps-ban
=========================================

A PostgreSQL-korlátozások segítik a konzisztencia biztosítását, ami elengedhetetlen a
komplex projektek hosszú távú adatkezeléséhez. Az OpenBioMaps biztosítja a
szükséges eszközöket a PostgreSQL-struktúra konfigurálásához és használatához a projekt
felületein keresztül.

A projekt tábláit és oszlopait az
OpenBioMaps adminisztrációs felületén keresztül kell létrehozni és regisztrálni. Az utasítások és a vonatkozó
figyelmeztetésekért lásd: :ref:`Adatbázis-táblák és oszlopok <database-columns>`.

.. TODO: Adjunk hozzá példatábladefiníciókat, amelyek felsorolják az egyes javasolt oszlopokat, azok
   PostgreSQL adattípusát, hogy nullázhatók-e, valamint az elsődleges kulcs,
   egyedi kulcs vagy külső kulcs korlátozásait.

.. TODO: Adjon hozzá útmutatást ezeknek a tábláknak az OpenBioMaps
   adminisztrációs felületén történő létrehozásához, ahelyett, hogy csak nyers SQL-kódot mutatna.

.. TODO: Ismertesse minden külső kulcs törlési és frissítési viselkedését.
   Kerülje a korábbi megfigyelések kaszkádszerű törlését, kivéve, ha ez egy
   kifejezett és gondosan átvizsgált projektkövetelmény.


Az aktív madárházak megjelenítése a tereptérképen
===========================================

A terepen a megfigyelőknek először meg kell találniuk a madárházakat. A *nest register* táblából
térkép állítható elő. Az OpenBioMaps képes megjeleníteni ezeket az adatokat,
miután a megfelelő táblára vonatkozó lekérdezést konfigurálták, és azt egy
térképréteghez kapcsolták.

Az SQL-lekérdezési sablonok és a térképkonfiguráció áttekintéséhez lásd
:ref:`SQL-lekérdezési beállítások <sql-query-settings>` és
:ref:`Térképbeállítások <map-settings>`.

A kapott térkép kompatibilis OpenBioMaps-kliensekkel jeleníthető meg. A
terepmunkához az OpenBioMaps progresszív webalkalmazás használható, és
a támogatott mobil kliensek is biztosíthatnak adatbázis-lekérdezési és térkép-megjelenítési
funkciókat. A kliensek aktuális
képességeiről lásd :doc:`Progresszív webalkalmazás <pwa>` és
:doc:`Mobilalkalmazások <mobile_applications>`.

Normál esetben csak a jelenleg aktív fészekdobozok jelenjenek meg az operatív
terepképen. Egy lehetséges megvalósítás egy olyan PostgreSQL-nézet létrehozása, amely
minden fészekdoboz esetében csak az aktuálisan aktív rekordot adja vissza. Ez létrehoz egy
virtuális táblát, amely tartalmazza a megjelenítendő fészekdobozokat. Például
a nézet neve lehetne ``current_nest_boxes``.

A nézetek kezelésével kapcsolatos információkért lásd
:ref:`Nézetek kezelése <managing-views>`.

.. TODO: Adja hozzá a ``current_nest_boxes`` nézet teljes definícióját, és
   magyarázza el, hogyan választja ki a legfrissebb érvényes állapotra vonatkozó rekordot. Használjon hordozható,
   kisbetűs SQL-azonosítót, amely kizárólag betűket és aláhúzásjeleket tartalmaz.

.. TODO: Magyarázza el, hogyan alkalmazzák a hozzáférési szabályokat a nézetre és annak térképrétegére.
   Ellenőrizze, hogy a lekérdezési sablon tartalmazza-e az összes helyőrzőt, amely a
   projekt-, sor- és oszlopszintű hozzáférési korlátozások érvényesítéséhez szükséges. Lásd
   :doc:`Adat-hozzáférés <data_access>`.

.. TODO: Dokumentálja az ajánlott mezőkliens offline viselkedését,
   beleértve azt is, hogy mikor szinkronizálódik a térkép és a madárház-lista, és hogyan
   észlelik az elavult adatokat.


A feltöltési űrlapok létrehozása
=========================

Legalább négyféle rekordot kell bevinni a négy táblába:

* állandó fészekdoboz-adatok a *nest base* táblába;
* időfüggő fészekdoboz-adatok a *nest register* táblába;
* megfigyelések a *breeding events* táblába; és
* beavatkozások a *brood-management* táblába.

Ezért legalább négy feltöltési űrlapra van szükségünk. Egy projekt
további űrlapokat is létrehozhat, ha ugyanarra a táblára különböző munkafolyamatok, kliensek, felhasználói csoportok vagy
érvényesítési követelmények vonatkoznak.

Az űrlapok konfigurálásával és közzétételével kapcsolatos részletes utasításokat lásd
:doc:`Feltöltési űrlapok kezelése <upload_forms>`.

.. TODO: Adjon hozzá egy táblázatot, amely felsorolja az egyes javasolt űrlapokat, azok cél tábláját,
   a célközönséget, a támogatott klienseket, az űrlap típusát, a hozzáférési beállításokat, valamint
   azt, hogy azok alkalmi megfigyelési vagy megfigyelési esemény módban kerülnek-e használatra.

.. TODO: Ismertesse, hogyan kell tesztelni az űrlapok tervezetét és közzétett verzióit
   a terepi bevezetés előtt, különösen akkor, ha az offline mobil kliensek
   továbbra is egy régebbi, közzétett verziót használhatnak.


A megfelelő fészekdoboz kiválasztása
==============================

A fészkelési esemény rögzítéséhez a megfigyelőnek ki kell választania a megfelelő fészekdobozt.
Előfordulhat, hogy a festett mezőazonosító nem azonosítja egyértelműen a fizikai fészekdobozt,
és előfordulhat, hogy elírják is. Az űrlapnak ezért tartalmaznia kell a
jelenleg aktív fészekdobozok listáját, amelyből a megfigyelő kiválaszthatja a megfelelőt.

Ideális esetben a megfigyelőnek lehetőséget kell biztosítani arra, hogy ugyanazokat a fészekdobozokat térképen is megtekintse a
kiválasztás megerősítése érdekében. A fent leírt ``current_nest_boxes`` nézet
szolgálhat a lista forrásaként. Az űrlap tárolhatja a fészekdoboz stabil,
egyedi azonosítóját, miközben a megszokottabb, festett terepi
azonosítóját jeleníti meg.

Az OpenBioMaps űrlapszerkesztő támogatja az adatbázis-táblákból
származó listaértékeket. Lásd a :ref:`Lista definíciója <list-definition>` és a közös lista
szakaszokat a :doc:`Feltöltési űrlapok kezelése <upload_forms>` című dokumentumban.


.. TODO: Adja meg a fészekdoboz
   mező által használt teljes JSON-listadefiníciót, beleértve az ``optionsSchema``, ``optionsTable``, ``valueColumn``,
   ``labelColumn`` elemeket, a sorrendet és az esetleges szükséges szűrőket.

.. TODO: Gondoskodjon arról, hogy a látható címke egyértelmű legyen. Ha a színezett mezőazonosítók
   duplikálódhatnak, jelenítse meg további kontextusadatokat, például a
   helyszín nevét, a rekeszt, az aktuális állapotot vagy a rövidített istállóazonosítót
  .

.. TODO: Magyarázza el, hogyan kapcsolódik össze a térkép- és az űrlapválasztás
   az egyes támogatott kliensekben. Ne sugallja, hogy ez az interakció elérhető,
   hacsak azt nem tesztelték a vonatkozó webes, PWA és mobil verziókban.


Faj kiválasztása
===================

Egy szaporodási esemény űrlapjának általában szüksége van egy taxon- vagy fajnév mezőre. A
mezőnek ellenőrzött és dokumentált taxonómiai listát kell használnia. Rövid,
projektspecifikus lista esetén az űrlap
listaszerkesztőjében soronként egy fajnév adható meg, amely az értékeket az űrlap által használt JSON-listává alakítja át.

Egy nagyobb vagy karbantartott taxonómiai referencia esetén az automatikus kiegészítés forrása
általában megfelelőbb, mint egy statikus lista. Lásd a taxon-információkra
vonatkozó útmutatást a :doc:`Adatgyűjtés <data_collection>` részben, valamint az automatikus kiegészítés
és a lista-meghatározás szakaszokat a
:doc:`Feltöltési űrlapkezelés <upload_forms>` részben.

.. TODO: Azonosítsa a példában használt taxonómiai hivatkozást, és
   amennyiben lehetséges, a megjelenített név mellett tároljon egy
   stabil taxon-azonosítót is.

.. TODO: Magyarázza el, hogyan kezelik és érvényesítik az ismeretlen, bizonytalan vagy újonnan beküldött taxonneveket
   anélkül, hogy csendben kicserélnék az eredetileg
   beküldött értéket.


Koordináták, megfigyelők és dátumok rögzítése
===========================================

Hasznos rögzíteni minden fészkelési esemény koordinátáit, még akkor is, ha a
fészekdoboznak már van regisztrált helyzete. A függetlenül rögzített
helyszín segíthet a helytelenül kiválasztott fészekdoboz azonosításában azáltal, hogy összehasonlítja az
esemény helyszínét a regisztrált helyszínnel.

A geometria mező elrejthető a felhasználó elől, vagy csak olvashatóként jeleníthető meg,
de a megjelenítési beállításokat önmagukban nem szabad biztonsági vagy integritási
ellenőrzésként kezelni. A beküldött értéket a szerveren is ellenőrizni kell, és
megfelelően kell feldolgozni.

A megfigyelő mező automatikusan kitölthető a bejelentkezett felhasználó számára.
További megfigyelő mezőkra lehet szükség, ha több ember dolgozik
együtt. Többszörös kiválasztású lista használható, ha egy mezőben több
további megfigyelőt kell kiválasztani.

A megfigyelés dátuma is automatikusan kitölthető és
csak olvashatóvá tehető. A megfigyelés idejét azonban meg kell különböztetni az
adatbázisba való beillesztés vagy feltöltés idejétől. A projekteknek emellett kifejezett
munkafolyamatot is biztosítaniuk kell a jogos visszamenőleges adatbevitelhez.

További információkért lásd a megfigyelő, a dátum és idő, valamint a helyszín szakaszokat
a :doc:`Adatgyűjtés <data_collection>` című dokumentumban. Az űrlap alapértelmezett értékei és megjelenítési
beállításai tekintetében lásd a :ref:`Alapértelmezett értékek <default-values>` és
a :ref:`Mezőmegjelenítési beállítások <api-params>` című szakaszokat.

.. TODO: Pontosítani kell, hogy az automatikusan kitöltött felhasználó a
   megfigyelőt, a rögzítőt, a feltöltőt vagy egy másik szerepkört jelenti-e. Ha ezek a szerepkörök
   eltérnek egymástól, tárolja őket külön.

.. TODO: Határozza meg, hogyan tárolják a több megfigyelőt. Egy kapcsolódó
   esemény-megfigyelő táblázat alkalmasabb lehet, mint egy elválasztójelekkel elválasztott lista, ha
   az egyes megfigyelőket lekérdezni, attribútumokkal ellátni vagy szerepkörökhöz rendelni kell.

.. TODO: Határozza meg, hogy a koordináták a madárházat, a megfigyelőt,
   vagy a tényleges megfigyelést jelölik-e. Rögzítse továbbá a koordináták pontosságát, a felvétel
   módszerét, az SRID-t, valamint a
   beküldött geometriára alkalmazott bármilyen transzformációt vagy általánosítást.

.. TODO: Kerülje az írásvédett megfigyelési dátum használatát pusztán a
   visszamenőleges adatbevitel azonosítására. Tárolja a megfigyelés időbélyegét és a beküldés
   időbélyegét külön, és kifejezetten hasonlítsa össze őket, ha ez a megkülönböztetés
   fontos.


Kapcsolódó mezők használata
====================

Külön mezőket kell létrehozni azoknak a megfigyeléseknek, amelyeket
függetlenül kell lekérdezni vagy elemezni. Ezeknek a mezőknek a közötti kapcsolatok
ezután felhasználhatók az érvényesítés ellenőrzésére.

Például:

* „Vannak tojások a fészekben?” — kötelező logikai mező;
* „Tojások száma” — opcionális egész szám mező, amely kötelezővé válik, ha
  tojások vannak jelen;
* „Vannak fiókák a fészekben?” — kötelező logikai mező; és
* „Fiókák száma” — opcionális egész szám mező, amely kötelezővé válik,
  ha fiókák vannak jelen.

Az OpenBioMaps egy másik
mező értékétől függően megváltoztathatja a mezők viselkedését. Például, ha tojások vannak a fészekben, a tojások száma mező
kötelezővé válhat. Az ilyen kapcsolatok kliensoldali támogatása eltérő lehet, ezért a viselkedést
minden tervezett felületen tesztelni kell, és az érvényesítést a szerveren is
el kell végezni.

A relációs szintaxis részleteiről lásd a
:doc:`Feltöltési űrlapok kezelése <upload_forms>` című dokumentum „oszlop-relációk” című szakaszát.

.. TODO: Adja hozzá a tojás és a csibe mezők tesztelt relációs definícióit.
   Dokumentálja, hogyan különböztetik meg a nulla, hiányzó, ismeretlen és
   nem számított értékeket.

.. TODO: Ellenőrizze, hogy mely relációkat támogatja jelenleg a webes űrlap,
   a fájlfeltöltés, az API, a PWA és a mobilalkalmazás. Ha egy kliens nem
   támogat egy relációt, magyarázza el a szerveroldali érvényesítést vagy az alternatív
   űrlaptervezést, amelyet az adatok konzisztenciájának megőrzésére használnak.


Függő listák használata
=====================

A támogatott kliensek a kiválasztható opciókat az előző listában
kiválasztott érték szerint rendezhetik. Például egy űrlap először megkérdezheti, hogy a
fészek aktív-e:

* ha a válasz „igen”, a következő mezőben a „tojások” vagy
  „csibék” lehetőségek jelenhetnek meg; és
* ha a válasz „nem”, a következő mezőben a „elhagyott”,
  „ragadozók által elpusztított”, „üres”, „egyéb tartalom” vagy „fészekdoboz nem található” lehetőségek jelenhetnek meg.

Ez közös vagy függő listával valósítható meg. A konfiguráció
részleteiről és példáiról lásd a
:doc:`Feltöltési űrlapok kezelése <upload_forms>` című dokumentum „közös lista” című szakaszát.

.. TODO: Adja hozzá a keresőtábla sorait és a teljes JSON-definíciókat mindkét
   mezőhöz, hogy a példa reprodukálható legyen.

.. TODO: Tekintse át a javasolt szókincset. Egyes értékek a fészekdoboz
  állapotát, mások a fészkelés állapotát, míg megint mások a megfigyelés
  sikertelenségét írják le. Fontolja meg, hogy ezeket a fogalmakat külön mezőkben tárolja, ahelyett, hogy
  egy listába egyesítené őket.

.. TEVENDŐ: Határozza meg, mi történik, ha a megfigyelő megváltoztatja az első választ
   egy függő érték kiválasztása után. Az előző értéket törölni kell, vagy
   újra kell érvényesíteni, hogy elkerülhető legyen az inkonzisztens kombináció.


A munkafolyamat tesztelése
====================

Mielőtt az űrlapokat a tényleges terepmunkához használná, küldjön el reális teszt
rekordokat minden tervezett kliensen keresztül. A teszteknek tartalmazniuk kell új és meglévő
fészekdobozokat, duplikált terepi címkéket, áthelyezett vagy ideiglenesen eltávolított dobozokat,
üres fészkeket, bizonytalan számlálási eredményeket, több megfigyelőt, nem elérhető GPS
pozíciókat, visszamenőleges adatbevitelt, valamint megszakított vagy offline beküldéseket.

Ellenőrizze, hogy a kapott rekordok lekérdezhetők és összekapcsolhatók-e anélkül, hogy
nem dokumentált feltételezésekre kellene támaszkodni. Ellenőrizze továbbá, hogy a nyilvános, hitelesített és
csoport-specifikus felhasználók megkapják-e a kívánt űrlapot és adathozzáférést.

A közzététel előtti ellenőrzőlista bővebb változatát lásd a gyakorlati ellenőrzőlistában a
:doc:`Adatgyűjtés <data_collection>` című részben. Az űrlapok közzétételével és
verziókezelésével kapcsolatban lásd a :doc:`Feltöltési űrlapok kezelése <upload_forms>` című részt, a
projekt jogosultságokkal kapcsolatban pedig a :doc:`Adathozzáférés <data_access>` című részt.

.. TODO: Adjon hozzá egy kis, reprodukálható tesztadatkészletet, és sorolja fel az egyes
   érvényesítési, lekérdezési, térképészeti és hozzáférés-vezérlési tesztek várható eredményét.


Mintavétel rögzített mintavételi helyszíneken rögzített transzektek mentén
******************************************************

.. TEVÉKENYSÉG: Adjon hozzá egy kidolgozott példát a rögzített transzektek mentén,
   rögzített mintavételi helyszíneken végzett ismételt mintavételre. Tegyen különbséget a stabil helyszínek és transzektek, valamint a mintavételi
   események, az egyedi megfigyelések, a kifejezett nem észlelések, a nyomvonalak és
   a mintavételi erőfeszítés mérései között.
