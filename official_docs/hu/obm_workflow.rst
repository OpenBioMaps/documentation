.. _data-flow-database-integration:

Az OpenBioMaps adatfolyama és adatbázis-integrációja
****************************************************

Ez az oldal azt ismerteti, hogyan kapcsolja össze az OpenBioMaps a
projektkonfigurációt, a PostgreSQL adatbázis-objektumokat, a metaadatokat, a
feltöltési munkafolyamatokat, a hozzáférési szabályokat, a lekérdezéseket és
a külső klienseket.

Az oldal azoknak a fejlesztőknek, szerveradminisztrátoroknak és tapasztalt
projektadminisztrátoroknak szól, akiknek meg kell érteniük a felhasználók
számára elérhető adatkezelési munkafolyamat műszaki megvalósítását. Az
adatgyűjtés és az adatkezelés általános bemutatását lásd a következő
dokumentumokban:

* :doc:`Kezdeti lépések <getting_started>`;
* :doc:`Adatgyűjtés <data_collection>`;
* :doc:`Adatkezelés <data_management>`; valamint
* :doc:`Adathozzáférés <data_access>`.

Az itt ismertetett megvalósítási részletek az OpenBioMaps verziójától és a
projekt konfigurációjától függően eltérhetnek. Mielőtt közvetlenül módosítaná
az adatbázis-objektumokat, vizsgálja meg az aktuális projektmetaadatokat,
triggereket, nézeteket, hozzáférési szabályokat és az alkalmazás forráskódját.
A strukturális módosításokat külön projektben tesztelje, és készítsen
megfelelő biztonsági mentést, mielőtt éles adatokon alkalmazná őket.


Műszaki áttekintés
==================

Egy tipikus OpenBioMaps-adatfolyam a következő műszaki szakaszokból áll:

#. A projektadminisztrátor meghatározza a PostgreSQL-táblákat, -oszlopokat,
   -kapcsolatokat és az OpenBioMaps-metaadatokat.
#. A feltöltési űrlapok elérhetővé teszik a kiválasztott oszlopokat a webes,
   fájlfeltöltési, API- vagy mobilkliensek számára.
#. Egy kliens beküldi a rekordokat, valamint adott esetben a mellékleteket és
   a feltöltési metaadatokat.
#. Az OpenBioMaps az űrlap definíciójának megfelelően ellenőrzi és átalakítja
   a beküldött értékeket.
#. Az alkalmazás beilleszti az elfogadott értékeket a céltáblába, és rögzíti
   a feltöltés adatait.
#. Az adatbázis-triggerek vagy a háttérfeladatok karbantarthatják az
   előzményeket, a hozzáférési szabályokat, a taxonómiai adatokat, a
   származtatott értékeket és más projektspecifikus struktúrákat.
#. A lekérdezéssablonok egyesítik a projekttáblákat a hozzáférés-vezérlési és
   modulrészletekkel.
#. Az eredményül kapott adatok megjeleníthetők a webalkalmazásban, vagy
   elérhetők exportokon, API-kon, SQL-klienseken és más integrációkon
   keresztül.
#. A biztonsági mentések, az archívumok és a projektszabályzat határozzák meg,
   hogyan őrzik meg az adatokat és a hozzájuk tartozó konfigurációt.

Nem minden projekt használja az összes szakaszt. Egy kis projekt például
használhat egyetlen megfigyelési táblát és egy webes űrlapot, míg egy
monitorozási projekt külön táblákat használhat a helyszínekhez, eseményekhez,
megfigyelésekhez, taxonokhoz, mellékletekhez és ellenőrzési eredményekhez.


PostgreSQL-háttérrendszer
=========================

Az OpenBioMaps PostgreSQL-ben tárolja a projektadatokat, és a térbeli adatok
kezeléséhez általában PostGIS-t használ. Az adatbázis hagyományos
PostgreSQL-objektumokat és olyan OpenBioMaps-metaadatokat egyaránt tartalmaz,
amelyek leírják, hogyan használja az alkalmazás ezeket az objektumokat.

Egy PostgreSQL-tábla vagy -oszlop megléte önmagában nem teszi elérhetővé az
objektumot az OpenBioMapsban. A megfelelő metaadatoknak is azonosítaniuk kell
az objektumot, és le kell írniuk a projektben betöltött szerepét.


Adatbázistáblák és metaadatok
-----------------------------

A projektadminisztrációs felületen létrehozott táblák a PostgreSQL-ben jönnek
létre, és bekerülnek az OpenBioMaps metaadataiba. A regisztrált táblákat ezt
követően feltöltési űrlapok, lekérdezéssablonok, modulok, adminisztrációs
eszközök és más alkalmazáskomponensek használhatják.

Az SQL-klienssel létrehozott táblák és nézetek regisztrációja nem történik
meg automatikusan. Ezeket hozzá kell adni a megfelelő
OpenBioMaps-metaadatokhoz, mielőtt az alkalmazás biztonságosan és
következetesen használhatná őket.

A támogatott táblaműveletekhez előnyben kell részesíteni az adminisztrációs
felületet, mert az a PostgreSQL-objektumot és a hozzá tartozó metaadatokat is
frissítheti. A közvetlen SQL-módosítások következtében előfordulhat, hogy a
metaadatok, űrlapok, lekérdezések, triggerek vagy modulok továbbra is egy már
nem létező objektumra hivatkoznak.

További információkért lásd:
:ref:`Adatbázistáblák és -oszlopok <database-columns>`.

.. TODO: Dokumentálni kell a projekt tábláinak vagy nézeteinek
   regisztrálásához használt pontos metaadattáblákat és -oszlopokat az
   OpenBioMaps aktuális verziójában.

.. TODO: Ki kell egészíteni a dokumentációt a már meglévő PostgreSQL-táblák
   vagy -nézetek újbóli létrehozás nélküli regisztrálásának támogatott
   eljárásával.

.. TODO: Ellenőrizni kell, mi történik az OpenBioMaps-metaadatokkal, ha egy
   regisztrált táblát közvetlenül SQL használatával neveznek át vagy törölnek.
   Ne hagyatkozzon a metaadatok automatikus tisztítására mindaddig, amíg ezt a
   működést nem tesztelték az aktuális verzióban.


Táblaleírások
-------------

Egy regisztrált táblához ember által olvasható leírás tartozhat. A tábla- és
oszlopleírások a projekt metaadatainak részét képezik, és ismertetniük kell
az adatok jelentését, eredetét, mértékegységeit, elvárt értékeit és tervezett
felhasználását.

A leírások használata akkor is kifejezetten ajánlott, ha műszakilag nem
kötelezők. Nehéz karbantartani, cserélni és újrafelhasználni egy olyan
adatbázis-struktúrát, amely csak az SQL-azonosítói alapján érthető meg.

A metaadatokra és a származásra vonatkozó ajánlásokért lásd:
:doc:`Adatkezelés <data_management>` és
:doc:`Adatkezelési szabályzat <data_policy>`.


Adatbázisoszlopok
-----------------

Egy projekttábla hagyományos adatoszlopokból és szükség esetén
OpenBioMaps-rendszeroszlopokból áll. Az egyes oszlopok fizikai adattípusát,
megszorításait és tárolási módját a PostgreSQL határozza meg. Az
OpenBioMaps-metaadatok határozzák meg, hogyan értelmezi és használja az
alkalmazás az oszlopot.


Rendszeroszlopok
................

Az OpenBioMaps által létrehozott táblák általában tartalmaznak ``obm_``
előtaggal rendelkező oszlopokat. Az OpenBioMaps verziójától és a projekt
konfigurációjától függően ezek a következő mezőket foglalhatják magukban:

``obm_id``
   Egy rekord belső azonosítója.

``obm_geometry``
   A rekordhoz társított térbeli geometria.

``obm_uploading_id``
   Hivatkozás arra a feltöltésre, amelyen keresztül a rekord létrejött.

``obm_validation``
   Ellenőrzéssel kapcsolatos információ.

``obm_comments``
   A rekordhoz társított megjegyzések vagy annotációk.

``obm_modifier_id``
   A rekordot módosító felhasználót vagy folyamatot azonosító információ.

``obm_files_id``
   A feltöltött mellékletekhez kapcsolódó hivatkozás vagy hivatkozások.

Egy egyszerű tábladefiníció a következő példához hasonló lehet:

.. code-block:: sql

   CREATE TABLE public.test_table (
       obm_id integer
           DEFAULT nextval(
               'public.test_table_obm_id_seq'::regclass
           )
           NOT NULL,
       obm_geometry public.geometry,
       obm_uploading_id integer,
       obm_validation numeric,
       obm_comments text[],
       obm_modifier_id integer,
       obm_files_id character varying(32),
       CONSTRAINT enforce_dims_obm_geometry
           CHECK (public.st_ndims(obm_geometry) = 2),
       CONSTRAINT enforce_srid_obm_geometry
           CHECK (public.st_srid(obm_geometry) = 4326)
   );

Ez a példa csak szemléltetési célokat szolgál, és nem tekinthető minden
telepítés mérvadó sémájának. Az oszloptípusok, megszorítások,
mellékletkezelés, szekvenciadefiníciók és térbeli referenciabeállítások
verziónként és projektenként eltérhetnek.

Ne töröljön vagy nevezzen át egy ``obm_`` oszlopot pusztán azért, mert
használaton kívülinek tűnik. A feltöltésfeldolgozás, a triggerek, a modulok, a
hozzáférési szabályok, az előzmények, a lekérdezések vagy a külső kliensek
függhetnek tőle.

.. TODO: El kell készíteni az aktuális adminisztrációs felület által
   létrehozott összes rendszeroszlop mérvadó referenciáját. Minden oszlop
   esetében dokumentálni kell annak PostgreSQL-típusát, nullázhatóságát,
   alapértelmezett értékét, megszorításait, hivatkozásait és az azt használó
   alkalmazáskomponenseket.

.. TODO: Ellenőrizni kell, hogy az összes felsorolt ``obm_`` oszlop kötelező-e
   minden kezelt táblában, vagy egyes oszlopok választhatók, és csak bizonyos
   munkafolyamatokhoz jönnek létre.

.. TODO: Dokumentálni kell a jelenlegi mellékletmodellt, és meg kell
   erősíteni, hogy az ``obm_files_id`` egyetlen azonosítót, több azonosítót
   vagy egy másik táblára mutató hivatkozást tartalmaz-e.


PostgreSQL-típusok és OpenBioMaps-típusok
........................................

A PostgreSQL-adattípus azt írja le, hogyan történik egy érték tárolása, és
milyen adatbázis-műveletek végezhetők el rajta. Ilyen például a ``text``, az
``integer``, a ``date``, a ``timestamp``, a tömbök és a PostGIS
geometriatípusai.

Egy OpenBioMaps-oszloptípus vagy szemantikai szerep azt írja le, hogyan
használja az alkalmazás az oszlopot. Egy oszlop például a következőket
reprezentálhatja:

* általános adatérték;
* tudományos név;
* alternatív taxonnév;
* megfigyelési dátum;
* egyedek száma;
* geometria;
* koordináta;
* hivatkozás; vagy
* melléklet.

Csak azok a regisztrált oszlopok választhatók ki az alkalmazáskomponensekben,
például a feltöltési űrlapokon és a lekérdezési felületeken, amelyeket az
OpenBioMaps-metaadatok elérhetővé tesznek.

A PostgreSQL-típusnak és az OpenBioMaps szemantikai szerepének kompatibilisnek
kell lennie egymással. Egy szemantikai szerep hozzárendelése nem alakítja át
automatikusan a fizikai adattípust, és nem ellenőrzi automatikusan a meglévő
értékeket.

.. TODO: Hozzá kell adni egy kompatibilitási táblázatot, amely minden
   OpenBioMaps szemantikai típust hozzárendel a támogatott
   PostgreSQL-típusokhoz, valamint az azokat használó alapvető függvényekhez
   vagy modulokhoz.

.. TODO: Dokumentálni kell, hogy egy szemantikai típus hozzárendelése vagy
   módosítása hatással van-e a meglévő feltöltési űrlapokra,
   lekérdezéssablonokra, mobilkliensekre vagy a gyorsítótárazott
   űrlapdefiníciókra.


Oszlopazonosítók és látható nevek
................................

A PostgreSQL-azonosítókhoz kisbetűket, számokat és aláhúzásjeleket kell
használni. Kerülje a szóközöket, ékezetes karaktereket, idézőjelek közé tett
azonosítókat és más speciális karaktereket. Az OpenBioMaps-metaadatok külön
látható nevet társíthatnak egy oszlophoz, így az adatbázisban biztonságosan
használható azonosítót nem szükséges közvetlenül megjeleníteni a
felhasználóknak.

Egy adatbázisoszlop neve lehet például ``observation_date``, miközben a
látható neve ``Observation date`` vagy annak lefordított megfelelője.

A ``str_`` előtaggal kezdődő látható nevek fordítási kulcsként használhatók
ott, ahol támogatott a projektspecifikus lokalizáció. A kliensalkalmazás az
aktuális nyelvéhez elérhető fordítást jeleníti meg, hiányzó fordítás esetén
pedig a beállított tartalék viselkedést alkalmazza.

Csak a látható név átnevezése nem nevezi át a PostgreSQL-oszlopot. A
PostgreSQL-oszlop átnevezése működésképtelenné teheti az űrlapokat,
lekérdezéseket, triggereket, nézeteket, modulokat, exportokat és külső
klienseket.

A helyi fordításokkal kapcsolatos további információkért lásd:
:ref:`Helyi fordítások <localisation>`.

.. TODO: Dokumentálni kell a pontos tartalék viselkedést arra az esetre, ha
   egy ``str_`` fordítási kulcs vagy az aktív nyelvhez tartozó fordítás
   hiányzik.

.. TODO: Meg kell erősíteni, hogy mely kliensek használják a látható neveket,
   és melyek teszik elérhetővé a nyers PostgreSQL-azonosítókat az űrlapokon,
   exportokban, API-válaszokban vagy hibaüzenetekben.


Oszlopsorrend
.............

A PostgreSQL megőrzi az oszlopok fizikai sorrendjét a tábladefiníciókban, de
nem biztosít egyszerű, támogatott műveletet a meglévő oszlopok átrendezésére.
Az OpenBioMaps-metaadatok és a feltöltési űrlapok a fizikai adatbázisbeli
sorrendtől függetlenül határozhatják meg a megjelenítési sorrendet.

A projektszintű sorrend alapértelmezésként használható az adatmegjelenítések
és az űrlapok számára. Egy adott feltöltési űrlap a saját munkafolyamatához
felülírhatja ezt a sorrendet. Ha nincs meghatározva alkalmazásszintű sorrend,
a felület az adatbázisban vagy a metaadatokban megadott sorrendet használhatja
tartalék megoldásként.

Ne hozzon létre újra egy éles táblát kizárólag az oszlopok látható
sorrendjének módosítása érdekében, kivéve, ha annak igazolt műszaki oka van.
Egy tábla újbóli létrehozása hatással lehet a következőkre:

* szekvenciák és alapértelmezett értékek;
* elsődleges és idegen kulcsok;
* indexek és megszorítások;
* tulajdonjog és jogosultságok;
* triggerek és szabályok;
* megjegyzések és metaadatok;
* nézetek és materializált nézetek;
* hozzáférésiszabály-táblák;
* feltöltési űrlapok és lekérdezéssablonok; valamint
* külső alkalmazások.

Amikor lehetséges, használja az OpenBioMaps megjelenítésisorrend-beállításait.

.. TODO: Meg kell erősíteni az egyes webes, API-, export- és mobilfelületek
   által használt pontos tartalék sorrendet arra az esetre, ha nincs
   beállítva kifejezett oszlopsorrend.


Adatbevitel
===========

A projektadatok OpenBioMaps-feltöltési munkafolyamatokon vagy közvetlen
adatbázis-műveleteken keresztül kerülhetnek be a PostgreSQL-be. Ezek az
útvonalak nem egyenértékűek.


OpenBioMaps-feltöltési munkafolyamatok
-------------------------------------

A feltöltési űrlapok határozzák meg a céltáblát, az elérhető oszlopokat, a
kötelező mezőket, a beviteli vezérlőket, az alapértelmezett értékeket, az
ellenőrzési szabályokat, a támogatott klienseket és a hozzáférési
beállításokat.

A konfigurációjától függően egy űrlapot a következők használhatnak:

* webes adatrögzítési felület;
* fájlfeltöltési munkafolyamat;
* az OpenBioMaps API;
* mobilalkalmazás; vagy
* más kompatibilis kliens.

Egy tipikus, űrlapon keresztüli beillesztés a következő szakaszokból áll:

#. A kliens lekéri vagy megjeleníti az űrlap definícióját.
#. A közreműködő megadja vagy feltölti az értékeket.
#. Az alkalmazás ellenőrzi a beküldött struktúrát és értékeket.
#. A támogatott esetekben megjelennek a figyelmeztetések vagy az enyhe
   ellenőrzési hibák.
#. Az elfogadott értékek bekerülnek a céltáblába.
#. Az alkalmazás rögzíti a feltöltési metaadatokat.
#. Adott esetben tárolja a mellékleteket és azok társításait.
#. Az adatbázis-triggerek végrehajtják a beállított utófeldolgozó műveleteket.

Az űrlapok részletes konfigurációját lásd:
:doc:`Feltöltési űrlapok kezelése <upload_forms>`.


Feltöltési események és származás
---------------------------------

Amikor az adatokat OpenBioMaps-feltöltési munkafolyamaton keresztül küldik
be, az alkalmazás a ``system.uploadings`` táblában rögzíti a feltöltéssel
kapcsolatos információkat. A kezelt adattáblába írt rekordok az
``obm_uploading_id`` használatával hivatkozhatnak erre a feltöltésre.

A feltöltési metaadatok használatával a rekordok többek között a következő
információkhoz társíthatók:

* a közreműködő vagy a tulajdonos;
* a céltábla;
* a feltöltéshez használt űrlap;
* a beküldés időpontja;
* a csoportos hozzáférés hozzárendelései;
* a forrásfájl vagy az adatrögzítési munkafolyamat; valamint
* a feldolgozás vagy a befejezés állapota.

A tárolt mezők pontos köre és jelentése verzióspecifikus. Egy közvetlen
SQL-beillesztés nem hoz létre automatikusan egyenértékű feltöltési eseményt,
kivéve, ha a hívó kifejezetten megvalósítja a szükséges munkafolyamatot.

.. TODO: Dokumentálni kell a ``system.uploadings`` teljes jelenlegi sémáját,
   és azonosítani kell, mely oszlopok számítanak stabil, nyilvános
   interfésznek, és melyek belső megvalósítási részletek.

.. TODO: Ismertetni kell a feltöltés tranzakciós határait. Egyértelművé kell
   tenni, hogy a feltöltési metaadatok, adatrekordok, mellékletek és
   hozzáférési szabályok beillesztése egyetlen tranzakcióként lesz-e sikeres,
   vagy egyetlen tranzakcióként vall-e kudarcot.

.. TODO: Dokumentálni kell, hogyan jelennek meg a megszakított feltöltések, a
   piszkozatfeltöltések, az elutasított sorok, a befejezett feltöltések és a
   törölt feltöltések.


Ellenőrzés és átalakítás
------------------------

Az ellenőrzés több rétegben is történhet:

* kliensoldali űrlapvezérlők;
* szerveroldali feltöltésfeldolgozás;
* PostgreSQL-típusok és -megszorítások;
* adatbázis-triggerek;
* háttérfeladatok; valamint
* későbbi kurátori felülvizsgálat.

A kliensoldali ellenőrzés javítja a használhatóságot, de nem tekinthető
biztonsági határnak. Az API-n, fájlfeltöltéseken vagy közvetlen
adatbázis-kapcsolatokon keresztül érkező értékeket megfelelő szerveroldali
ellenőrzésnek kell alávetni.

Az átalakítások normalizálhatják az értékeket, létrehozhatják a geometriát,
feloldhatják a taxonómiai neveket, alapértelmezett értékeket rendelhetnek
hozzá, vagy más mezőket származtathatnak. Ha egy átalakítás megváltoztatja a
beküldött adatok tudományos jelentését, a projektnek meg kell őriznie az
eredeti értéket vagy az átalakítás rekonstruálásához elegendő származási
információt.

A háttérfeldolgozásról lásd: :doc:`Háttérfeladatok <jobs>`.


Közvetlen SQL-adatbevitel
-------------------------

A jogosultsággal rendelkező adatbázis-felhasználók PostgreSQL-kliensek és
olyan eszközök használatával illeszthetnek vagy importálhatnak be rekordokat,
mint a ``COPY``. Ez ellenőrzött tömeges migráció vagy adminisztratív
adatjavítás során lehet hasznos.

A PostgreSQL például támogatja az adatok importálását a ``COPY FROM``
használatával. Lásd a `PostgreSQL COPY dokumentációját
<https://www.postgresql.org/docs/current/sql-copy.html>`_.

A közvetlen SQL-műveletek megkerülhetik az alkalmazásszintű viselkedést,
beleértve a következőket:

* a feltöltési űrlap ellenőrzése;
* a feltöltési metaadatok automatikus létrehozása;
* a mellékletek feldolgozása;
* a hozzáférési szabályok hozzárendelése;
* az előzmény- vagy auditinformációk;
* a projektspecifikus átalakítások;
* az értesítések; valamint
* az alkalmazásszintű hibakezelés.

Az adatbázis-triggerek továbbra is lefutnak, kivéve, ha letiltották őket,
viselkedésük azonban függhet azoktól az értékektől, amelyeket általában az
alkalmazás ad meg. Az ``obm_uploading_id`` vagy más elvárt mező nélkül
beillesztett rekord ezért hiányos metaadatokat vagy hozzáférési szabályokat
eredményezhet.

Adatok közvetlen importálásakor bevált gyakorlat egy üres feltöltés
létrehozása, a feltöltés azonosítójának (``obm_uploading_id``) utólagos
hozzárendelése a feltöltött adatokhoz, valamint a közvetlen feltöltési mód és
a forrás megadása a feltöltés metaadataiban.

Közvetlen importálás előtt:

#. tekintse át a céltáblát, a megszorításokat, a triggereket és a szabályokat;
#. állapítsa meg, hogy szükség van-e megfelelő feltöltési rekordra;
#. kifejezetten ellenőrizze és alakítsa át a forrásadatokat;
#. szükség esetén használjon tranzakciót;
#. tesztelje az importálást nem éles projektben;
#. a beillesztés után ellenőrizze a rekord- és oszlopszintű hozzáférést;
#. ellenőrizze az előzmény-, melléklet- és taxonómiai munkafolyamatokat;
   valamint
#. rögzítse az importált adatok forrását és átalakítását.

Ne tiltsa le a triggereket pusztán azért, hogy az importálás sikeres legyen,
anélkül, hogy először megértené a céljukat. A hozzáférés-vezérlési,
előzmény- vagy integritási triggerek biztonsági szempontból kritikusak
lehetnek.

.. TODO: Ki kell egészíteni a dokumentációt egy támogatott tömeges
   importálási eljárással, amely kompatibilis feltöltési metaadatokat és
   hozzáférési szabályokat hoz létre, miközben megőrzi a PostgreSQL ``COPY``
   teljesítménybeli előnyeit.

.. TODO: Dokumentálni kell, hogy automatizált integrációkhoz melyik
   alkalmazásszolgáltatást vagy API-t kell előnyben részesíteni a közvetlen
   SQL-lel szemben.


Triggerek, szabályok és származtatott feldolgozás
=================================================

Az OpenBioMaps-projektek PostgreSQL-triggereket és -szabályokat használhatnak
a projektspecifikus viselkedés fenntartására rekordok beillesztése,
frissítése vagy törlése során.

A dokumentált triggermunkafolyamatok közé tartoznak a következők:

* taxonlisták karbantartása;
* rekordelőzmények;
* rekordszintű hozzáférési szabályok; valamint
* projektspecifikus ellenőrzés vagy származtatott értékek.

A trigger adatbázis-tranzakción belül működik, és elutasíthat vagy módosíthat
egy változtatást. Egy háttérfeladat általában ettől függetlenül fut, ezért
jobban megfelel a hosszú ideig futó, ütemezett, újrapróbálható vagy
erőforrás-igényes feldolgozáshoz.

A megkülönböztetés fontos:

``Constraint``
   Adatbázis-invariánst kényszerít ki, és elutasítja az annak nem megfelelő
   értékeket.

``Trigger``
   Automatikusan végrehajtódik egy adatbázis-módosítás részeként.

``Rule``
   Átírja vagy átirányítja a kiválasztott PostgreSQL-műveleteket, beleértve a
   beállított nézeteken végzett műveleteket.

``Background job``
   Külön, ütemezetten vagy kézi indítás után fut le.

``Application validation``
   Ellenőrzi vagy átalakítja az értékeket az OpenBioMaps alkalmazási
   munkafolyamatában.

Ugyanazt a követelményt nem szabad több rétegben, egymással inkonzisztens
módon megvalósítani. Ha több rétegre van szükség, dokumentálni kell azok
felelősségi köreit és hibakezelési viselkedését.

A triggerek adminisztrációjáról lásd:
:ref:`Függvények <trigger-functions>`.

.. TODO: Dokumentálni kell a szabványos OpenBioMaps-triggerek végrehajtási
   sorrendjét és függőségeit.

.. TODO: Azonosítani kell, hogy mely szabványos triggerek jönnek létre
   automatikusan egy új projekttáblához, és melyek igényelnek kifejezett
   adminisztrátori műveletet.

.. TODO: Meg kell határozni a triggerek tesztelésének és hatásaik éles
   használat előtti vizsgálatának támogatott módját.


Hozzáférésiszabály-integráció
=============================

A projektadatokhoz való hozzáférés a projekt alapértelmezett beállításaival,
rekordszintű szabályokkal, oszlopszintű korlátozásokkal, csoporttagsággal és
adminisztratív szerepkörökkel szabályozható.

Egy rekordszintű hozzáférési munkafolyamat általában a következőket kapcsolja
össze:

* a rekord ``obm_id`` értéke;
* a megfelelő ``row_id`` egy projektszabályokat tartalmazó táblában;
* a céltábla neve;
* az olvasási és írási hozzárendelések;
* egy érzékenységi érték; valamint
* a feltöltési vagy tulajdonosi metaadatok.

Egy hozzáférésiszabály-trigger a feltöltési űrlapból és a
``system.uploadings`` táblában található kapcsolódó bejegyzésből
származtathatja a hozzárendeléseket. A közvetlen SQL használatával létrehozott
rekordok nem feltétlenül rendelkeznek a származtatáshoz szükséges
metaadatokkal.

A lekérdezéssablonnak a megfelelő hozzáférés-vezérlési részleteket is
tartalmaznia kell. Az adatbázisban megfelelően beállított szabályok nem védik
meg az adatokat, ha egy alkalmazáslekérdezés vagy külső kapcsolat megkerüli
őket.

A hozzáférési modellről lásd: :doc:`Adathozzáférés <data_access>`.
A lekérdezéssablonok konfigurációjáról lásd:
:ref:`SQL-lekérdezési beállítások <sql-query-settings>`.

.. TODO: Dokumentálni kell a mérvadó jogosultságfeloldási algoritmust a
   projektbeállításoktól kezdve a szabálytáblák összekapcsolásain át az
   oszlopkorlátozásokig.

.. TODO: Minden támogatott felület esetében ellenőrizni kell, hogy a
   hozzáférés-vezérlés a PostgreSQL-ben, a létrehozott
   alkalmazáslekérdezésekben vagy mindkettőben érvényesül-e.

.. TODO: Tesztelt példákat kell hozzáadni, amelyek összehasonlítják az
   űrlapalapú beillesztést a közvetlen SQL-beillesztéssel egy csoportokra
   korlátozott projektben.


Adatkimenet
===========

Az OpenBioMaps a webes felületén, térképeken, API-kon, exportokon, mentett
eredményeken és külső adatbázis-klienseken keresztül teheti elérhetővé a
projektadatokat. Minden útvonalat külön kell értékelni a hozzáférés-vezérlés,
a metaadatok, a mezőnevek és a kimeneti formátum szempontjából.


Webes lekérdezések és térképek
------------------------------

A webalkalmazás beállított SQL-lekérdezéssablonok használatával állítja össze
a szöveges és térbeli lekérdezések eredményeit. A sablonok a következőkhöz
tartalmazhatnak helyőrzőket:

* kiválasztott mezők;
* geometriai szűrés;
* további modulszűrők;
* taxonómiai összekapcsolások;
* feltöltési metaadatok;
* hozzáférésiszabály-összekapcsolások; valamint
* más projektspecifikus SQL-részletek.

A MapServer rétegei dinamikusan létrehozott lekérdezések használatával
jeleníthetik meg ugyanazokat a projektadatokat egy térképen. A
PostgreSQL-lekérdezésnek, a MapServer mapfile-nak, a webes térképrétegnek és
az OpenBioMaps lekérdezési konfigurációjának összhangban kell maradnia.

Egy helytelenül beállított lekérdezés kihagyhat rekordokat, többszörözheti a
sorokat, hozzáférhetővé tehet korlátozott mezőket, vagy megkerülhet egy elvárt
hozzáférésiszabály-összekapcsolást. Minden lekérdezési konfigurációt tesztelni
kell a következő szerepkörökben:

* nem hitelesített látogató;
* normál hitelesített felhasználó;
* minden érintett csoport tagja;
* rekordtulajdonos vagy közreműködő; valamint
* adminisztrátor.

A részletekért lásd:
:ref:`SQL-lekérdezési beállítások <sql-query-settings>` és
:ref:`Térképbeállítások <map-settings>`.


Exportok
--------

A lekérdezési eredmények vagy teljes táblák támogatott formátumokba
exportálhatók. A kis exportok interaktív kérés során is létrehozhatók, míg a
nagyobb exportok háttérfeladatnak adhatók át.

Egy exportálási munkafolyamatnak meg kell őriznie vagy tartalmaznia kell a
következőket:

* a kiválasztott rekordok és mezők;
* az alkalmazott szűrők;
* a lekérdezés vagy exportálás időpontja;
* projekt- és adatkészlet-metaadatok;
* licenc- és forrásmegjelölési információk;
* a vonatkozó koordináta-referencia-információk;
* származás; valamint
* minden olyan érzékenységi vagy újrafelhasználási feltétel, amelyet a
  címzetteknek ismerniük kell.

A létrehozott fájlok az eredeti felhasználói munkamenet befejeződése után is
elérhetők maradhatnak. Tárolási helyük, letöltési jogosultságaik, lejáratuk és
tisztításuk ezért a biztonsági modell részét képezi.

.. TODO: Dokumentálni kell, hogy mely exportálási útvonalak alkalmazzák
   ugyanazokat a rekord- és oszlopszintű korlátozásokat, mint a webes
   lekérdezési felület.

.. TODO: Dokumentálni kell a létrehozott exportfájlok tárolását, elnevezését,
   hozzáférés-vezérlését, lejáratát és törlését.


API-hozzáférés
--------------

Az OpenBioMaps API programozott hozzáférést biztosít a támogatott
projektműveletekhez. Az API-kliensek az API verziójától és a megadott
hatókörtől függően lekérhetik az űrlapdefiníciókat, adatokat küldhetnek be,
rekordokat kérdezhetnek le, vagy más engedélyezett műveleteket hajthatnak
végre.

Egy közzétett feltöltési űrlapot használó API-beküldésnek a szerveroldali
űrlap-munkafolyamatot kell követnie. Egy közvetlen adatbázis-integráció nem
egyenértékű egy API-beküldéssel, és eltérő metaadatokat vagy
triggerviselkedést eredményezhet.

A részletekért lásd: :doc:`API-dokumentáció <api>`.


SQL-kliensek és külső alkalmazások
----------------------------------

A külső SQL-kliensek, például a QGIS, közvetlenül csatlakozhatnak a
PostgreSQL-hez, ha a szerver és a projekt üzemeltetője kifejezetten biztosít
hitelesítési adatokat és hálózati hozzáférést.

A közvetlen adatbázis-hozzáférés több információt tehet elérhetővé, mint a
webes felület, ha a PostgreSQL-jogosultságok, -nézetek és a rekordszintű
biztonság nem képezik le az alkalmazás hozzáférési modelljét. Nem szabad azt
feltételezni, hogy az alkalmazásszintű csoporttagság és oszlopkorlátozások
automatikusan érvényesek tetszőleges SQL-kapcsolatokra.

Adminisztratív projektfiók megosztása helyett részesítse előnyben a külön
írásvédett adatbázis-szerepköröket, a korlátozott nézeteket vagy egy API-t.

A támogatott integrációkért lásd: :doc:`Kliensek <clients>`.

.. TODO: Dokumentálni kell az OpenBioMaps profil- vagy adminisztrációs
   felületén létrehozott PostgreSQL-felhasználóknak megadott jogosultságokat.

.. TODO: Egyértelművé kell tenni, hogy a közvetlen SQL-klienseket az aktuális
   megvalósításban PostgreSQL rekordszintű biztonság, szűrt nézetek,
   hagyományos jogosultságok vagy más mechanizmus korlátozza-e.


Felhasználók, szerepkörök és adatbázis-identitások
==================================================

Az OpenBioMaps alkalmazásfelhasználói, projektszerepkörei, csoportjai,
OAuth-kliensei és PostgreSQL-szerepkörei egymáshoz kapcsolódó, de nem
felcserélhető fogalmak.

``Application user``
   Egy OpenBioMaps-fiókkal reprezentált személy vagy szolgáltatás.

``Project membership``
   Egy alkalmazásfelhasználót egy adott projekthez és állapothoz társít.

``Project group``
   Alkalmazásfelhasználókat csoportosít az űrlapokhoz, adatokhoz, modulokhoz
   vagy adminisztrációs funkciókhoz való hozzáférés céljából.

``Administrative role``
   Hozzáférést biztosít a kiválasztott projektadminisztrációs funkciókhoz.

``OAuth client or token``
   Engedélyezi, hogy egy kliensalkalmazás a megadott hatókörökön belül
   műveleteket hajtson végre.

``PostgreSQL role``
   A közvetlen adatbázis-hitelesítést és az SQL-jogosultságokat szabályozza.

Az a felhasználó, aki a webalkalmazáson keresztül lekérdezhet egy rekordot,
nem kap automatikusan közvetlen PostgreSQL-hozzáférést. Ezzel szemben egy
széles körű táblajogosultságokkal rendelkező PostgreSQL-szerepkör
megkerülheti a csak az alkalmazásban megvalósított korlátozásokat.

A szolgáltatásfiókoknak és az automatizált integrációknak külön, kizárólag a
feladatukhoz szükséges jogosultságokkal rendelkező hitelesítési adatokat kell
használniuk. A tokeneket és adatbázisjelszavakat nem szabad forráskódba
ágyazni vagy egymástól független alkalmazások között megosztani.

.. TODO: Hozzá kell rendelni az alkalmazásfelhasználókat,
   projekttagságokat, csoportokat, adminisztratív jogosultságokat,
   OAuth-identitásokat és PostgreSQL-szerepköröket az aktuális
   adatbázistáblákhoz és hitelesítési szolgáltatásokhoz.

.. TODO: Dokumentálni kell a fiókok létrehozását, a hitelesítési adatok
   módosítását, visszavonását, lejáratát és auditálási viselkedését minden
   támogatott integrációtípus esetében.


Biztonságos sémamódosítások
===========================

Egy kezelt tábla módosításai a PostgreSQL-re és az OpenBioMaps
konfigurációjára egyaránt hatással lehetnek. Egy tábla vagy oszlop
átnevezése, lecserélése vagy törlése előtt:

#. azonosítsa az objektumot használó feltöltési űrlapokat;
#. keressen a lekérdezéssablonokban és a MapServer mapfile-okban;
#. vizsgálja meg a triggereket, szabályokat, nézeteket, indexeket,
   megszorításokat és idegen kulcsokat;
#. vizsgálja meg a szemantikai oszlopszerepeket és a projektmetaadatokat;
#. vizsgálja meg a hozzáférési szabályok és az előzmények konfigurációját;
#. azonosítsa az objektumra hivatkozó modulokat és háttérfeladatokat;
#. azonosítsa az API-, mobil-, QGIS-, R- és közvetlen SQL-klienseket;
#. készítsen és ellenőrizzen megfelelő biztonsági mentést;
#. tesztelje a migrációt külön projektben;
#. határozzon meg visszaállítási eljárást; valamint
#. a migráció után ellenőrizze az összes támogatott felületet.

Az általa támogatott műveletekhez használja az adminisztrációs felületet. Ha
közvetlen SQL-re van szükség, ugyanannak az ellenőrzött migrációnak a
részeként frissítse a hozzá tartozó OpenBioMaps-metaadatokat és a függő
konfigurációt is.

Egy objektum átnevezése nem feltétlenül biztonságosabb annak törlésénél és
újbóli létrehozásánál: mindkettő működésképtelenné teheti az eredeti
azonosítót szövegként tároló függőségeket.

.. TODO: Támogatott migrációs eljárásokat kell létrehozni egy kezelt oszlop
   hozzáadásához, átnevezéséhez, típusának módosításához és törléséhez.

.. TODO: Támogatott eljárást kell létrehozni egy kezelt tábla nézettel való
   helyettesítéséhez és a módosítás visszavonásához.

.. TODO: Hozzá kell adni egy adminisztratív függőségi jelentést, amely
   felsorolja a kiválasztott táblára vagy oszlopra hivatkozó űrlapokat,
   lekérdezéssablonokat, modulokat, feladatokat, triggereket, szabályokat,
   térképrétegeket és metaadatokat.


Biztonsági mentések, archívumok és reprodukálhatóság
====================================================

Egy teljes OpenBioMaps-projekt nem csupán az elsődleges adattáblákból áll. A
telepítéstől függően a helyreállításhoz a következők lehetnek szükségesek:

* projekt- és rendszer-adatbázistáblák;
* szekvenciák, megszorítások, indexek, triggerek és szabályok;
* OpenBioMaps-metaadatok;
* projektkonfigurációs fájlok;
* feltöltési űrlapok és azok verziói;
* mellékletek és létrehozott származékos fájlok;
* MapServer- és webestérkép-konfiguráció;
* modulok és helyi forrásfájlok;
* háttérfeladatok és ütemezések;
* fordítások és üzenetsablonok; valamint
* különálló, biztonságos folyamaton keresztül visszaállított hitelesítési
  adatok vagy titkos értékek.

Egyetlen PostgreSQL-tábla mentése megőrizheti a megfigyelési rekordokat,
miközben elveszhet az értelmezésükhöz, szerkesztésükhöz, lekérdezésükhöz vagy
védelmükhöz szükséges konfiguráció.

A biztonsági mentéseket visszaállítással kell tesztelni. A hosszú távú
újrafelhasználásra szánt archívumoknak a dokumentációt, licenceket,
származást, szoftververziókat és az adatok eredeti szerveren kívüli
értelmezéséhez elegendő sémainformációt is meg kell őrizniük.

Az irányítási és megőrzési szempontokról lásd:
:doc:`Adatkezelési szabályzat <data_policy>`.

.. TODO: Meg kell határozni a projekt teljes körű biztonsági mentéséhez és
   helyreállításához szükséges adatbázis- és fájlrendszer-erőforrások
   minimális körét.

.. TODO: Hozzá kell adni egy verziózott projektexport-formátumot, amely
   alkalmas a kompatibilis OpenBioMaps-szerverek közötti migrációra.


Műszaki ellenőrzőlista
======================

Egy projektadat-munkafolyamat létrehozása vagy módosítása után ellenőrizze,
hogy:

* minden kezelt PostgreSQL-objektum rendelkezik-e a szükséges
  OpenBioMaps-metaadatokkal;
* a rendszeroszlopok a várt típusokkal, megszorításokkal és alapértelmezett
  értékekkel rendelkeznek-e;
* a szekvenciák, kulcsok, indexek, triggerek és szabályok érvényesek-e;
* az űrlapdefiníciók meglévő céloszlopokra hivatkoznak-e;
* az űrlap-ellenőrzés megfelelő módon a szerveren is érvényesül-e;
* létrejönnek-e a feltöltési metaadatok, és kapcsolódnak-e a beillesztett
  rekordokhoz;
* a mellékletek a kívánt rekordokhoz kapcsolódnak-e;
* a közvetlen importálások megfelelő származási információkat és hozzáférési
  szabályokat kapnak-e;
* az előzmény- és taxonómiai triggerek a várt eredményeket hozzák-e létre;
* a nyilvános és csoportspecifikus lekérdezések kikényszerítik-e a
  rekordkorlátozásokat;
* a korlátozott oszlopok hiányoznak-e minden jogosulatlan kimenetből;
* a térképrétegek és a szöveges lekérdezések konzisztens rekordokat adnak-e
  vissza;
* az API- és mobilbeküldések a kívánt közzétett űrlapverziót használják-e;
* az SQL-szerepkörök nem olvashatnak vagy módosíthatnak-e a tervezettnél több
  adatot;
* a létrehozott exportok védettek-e, és eltávolításuk a szabályzatnak
  megfelelően történik-e;
* a háttérfeladatok a szükséges függőségekkel és a legkisebb szükséges
  jogosultsággal futnak-e;
* a biztonsági mentések ígéret szerint tartalmazzák-e az adatbázis adatait, a
  konfigurációt és a mellékleteket; valamint
* egy helyreállítási teszt működő és hozzáférés-vezérelt projektet hoz-e
  létre.

Dokumentálja a tesztelt OpenBioMaps-verziót, a projekt konfigurációját, a
tesztfelhasználókat, a lekérdezéseket és az elvárt eredményeket. Ismételje
meg az ellenőrzéseket az alkalmazás frissítései, sémamigrációk vagy a
hozzáférési szabályzat lényeges módosításai után.
