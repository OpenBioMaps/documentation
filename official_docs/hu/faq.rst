.. raw:: html

    <style> 
    .red {color:#ff0000;font-weight:bold;}
    .green {color:#00ff00;font-weight:bold;}
    </style>

Gyakran ismételt kérdések
*************************

Mi az OpenBioMaps?
-----------------
Az OpenBioMaps biológiai adatok kezelésére szolgáló szoftver- és
szolgáltatási platform. Önállóan vagy szolgáltatásként is használható.
Segítségével adatbázis-alapú projektek hozhatók létre, amelyeket több
felhasználó egyidejűleg, különböző eszközökről és eltérő jogosultsági
szintekkel érhet el. Ha nem szeretne saját szervert fenntartani,
szolgáltatásként is használhatja, mivel egyes intézmények olyan szervereket
is üzemeltetnek, amelyek kutatási vagy közösségi tudományos projekteket
ingyenesen fogadnak.

Mi az OpenBioMaps Consortium?
-----------------------------
:doc:`Lásd: Consortium <../consortium>`


Hogyan hozhatok létre új adatbázisprojektet, illetve hogyan találhatok ilyet?
-----------------------------------------------------------------------------
Ha már tagja egy szerveren található projektnek, a webes felületen
létrehozhat egy új adatbázisprojektet ugyanazon a szerveren. Ez egy egyszerű
folyamat, amely egy űrlap kitöltésével végezhető el.


Hogyan tölthetek fel adatokat?
------------------------------
Röviden: adatfeltöltési űrlapok használatával.
PostgreSQL-kliens is használható, ez a megoldás azonban csak nagy
adatmennyiségek alkalmi importálásához ajánlott.


Hogyan férhetek hozzá az adatokhoz?
-----------------------------------
- A webes felületen térképi vagy szöveges lekérdezésekkel.
- PostgreSQL-kliens használatával.
- Az OpenBioMaps R-csomag használatával.
- A webes felületen keresztüli adatmegosztással.
- A webes felületen keresztüli adatexporttal.
- A :doc:`PWA-alkalmazással <../pwa>`.

Hogyan kérhetek le adatokat a mobiltelefonommal?
------------------------------------------------
A :doc:`PWA-alkalmazással <../pwa>`.


Hogyan regisztrálhatok egy OpenBioMaps-projektbe?
-------------------------------------------------
A regisztrációhoz meghívás szükséges. Bármely regisztrált tag meghívhat új
felhasználókat. Emellett alapértelmezés szerint a bejelentkezési felületen
elérhető egy meghívásigénylő űrlap, amelyen az új felhasználók kérhetik,
hogy meghívják őket egy projektbe. Egy OpenID-modul is rendelkezésre áll,
amely Google-fiókkal történő regisztrációt és bejelentkezést tesz lehetővé.

A regisztrációval és a meghívókkal kapcsolatos további információért
forduljon annak az adatbázisnak a létrehozóihoz vagy adminisztrátoraihoz,
amelyhez csatlakozni szeretne.


Van programozható felület a fejlesztők számára?
-----------------------------------------------
Igen. A Project Data Service (PDS) lehetővé teszi a projektek és a
felhasználói adatok projektenkénti lekérdezését adatbázisokból indított
URL-kérésekkel.

Példa: https://openbiomaps.org/pds.php?scope=get_project_list

További információ az API-dokumentációban található.

Milyen nyelveket támogat az OpenBioMaps?
----------------------------------------
Nincsenek nyelvi korlátozások, az OpenBioMaps azonban jelenleg magyar,
angol, román, spanyol és portugál nyelven, valamint korlátozott mértékben
orosz, német és francia nyelven érhető el. További nyelvek és fordítások a
https://translate.openbiomaps.org felületen adhatók hozzá.

Minden projekt saját nyelvi beállításokkal és kapcsolódó fordításokkal
rendelkezhet.


Hogyan járulhatok hozzá az OpenBioMaps fejlesztéséhez?
------------------------------------------------------
- Adatbázisprojekt létrehozásával vagy alapításával.
- Adatok adatbázisprojektbe történő feltöltésével.
- Új OpenBioMaps-szerver létrehozásával.
- Adatbázisprojekt saját szerveren történő elhelyezésével.
- Új nyelvek hozzáadásával vagy a meglévő fordítások javításával.
- Szoftverfejlesztéssel.
- Pénzügyi támogatással.


Kell bármiért fizetnem?
-----------------------
Minden OpenBioMaps-összetevő és -szolgáltatás teljesen ingyenes, a
fejlesztés egy része azonban nem önkéntes munkában történik, vagyis fizetünk
a fejlesztőknek. Ezért hálásan fogadunk minden, a fejlesztéshez nyújtott
támogatást.


Hogyan és hol tárolja az OpenBioMaps az adatokat?
-------------------------------------------------
Minden OpenBioMaps-szerver a saját adatbázisában és fájlrendszerében tárolja
az adatokat.


Van biztonsági mentési megoldás?
--------------------------------
Nincs központosított biztonsági mentés, mivel az OpenBioMaps nem rendelkezik
központosított adatkezeléssel. Minden szerver saját biztonsági mentési
megoldást használ, egyes szerverek pedig egymás tárhelykapacitását is
igénybe veszik archiválásra.


Elfelejtettem a jelszavamat. Hogyan kérhetek újat?
--------------------------------------------------
Ne aggódjon, nagyon egyszerű új jelszót kérni.

Kövesse a bejelentkezési oldalon található „elfelejtett jelszó” hivatkozást.

Itt megadhatja a bejelentkezéshez használt e-mail-címét. Az elküldést
követően a rendszer e-mailben küld egy hivatkozást, amelyet követve
bejelentkezhet a fiókjába, és új jelszót állíthat be.


Rózsaszín négyzetek jelennek meg a térképoldalon
------------------------------------------------
Ezt a térképrétegekhez vagy az adatlekérdezési beállításokhoz kapcsolódó
konfigurációs hiba okozhatja.


Mi az a RUM?
------------

Lásd a RUM FILH modellről szóló publikációt: `RUM/FILH: a standardized operational capability model for biodiversity databases <https://doi.org/10.1093/database/baag044>`_

A RUM az adatbázis nyitottsági osztályainak rövidítése:

Read - Upload - Modify

Mindegyik elem értéke [-], [0] vagy [+] lehet.

ahol

[-] nem nyilvános, [0] részben nyilvános, [+] pedig nyilvános,

a színek pedig a következők: [-] fekete, [0] piros és [+] zöld.

Például:

<font color="red">R</font><font color="green">U</font>M: részben nyilvános
olvasás, nyilvános feltöltés és nem nyilvános módosítás.


Rendelhető DOI az adatbázisokhoz?
---------------------------------
Igen, minden véglegesített állapotú adatbázis kaphat DOI-t a DataCite DOI
Service használatával.

Minden adatbázis rendelkezik DOI-metaadatoldallal, például:

https://dinpi.openbiomaps.org/projects/danubefish/index.php?metadata

A DataCite rendszerben használt DOI-előtagunk: 10.18426

A DOI-utótagok automatikusan jönnek létre, és egyediek.

Minden adatbázisban további DOI-k rendelhetők adatkészletekhez.


Hol találom a meglévő OpenBioMaps-szerverek listáját?
-----------------------------------------------------
A regisztrált szerverek az OpenBioMaps adatbázisában találhatók:
https://openbiomaps.org/projects/openbiomaps_network.


Hogyan használhatom az OpenBioMaps mobilalkalmazást?
----------------------------------------------------
iPhone vagy Android rendszerben – jelenleg csak az androidos verzió működik.
A felhasználóknak be kell jelentkezniük a szerverükön, hogy elérhessék a
projektjükben rendelkezésre álló adatfeltöltési űrlapokat. A bejelentkezés
és az űrlapok letöltése után az alkalmazás offline is használható. A jelenlegi
alaptérkép Google-alapú, és csak akkor működik offline, ha a célterületet
offline használatra letöltötték a Google Terrain Map alkalmazásból.

A mobilalkalmazás a
https://openbiomaps.org/projects/openbiomaps_network adatbázisban
regisztrált szervereket sorolja fel.


Hol találom az OpenBioMaps R-csomagot?
--------------------------------------
Egyelőre csak fejlesztői csomagként érhető el:
https://github.com/OpenBioMaps/obm.r

Milyen adatletöltési lehetőségek állnak rendelkezésre?
------------------------------------------------------
* CSV-, KML-, JSON- és más modulok használatával, ahol elérhetők.
* QGIS használatával.
* Könyvjelzők és állandó hivatkozások használatával.
* Az R-csomag használatával.

Hogyan és hol érhetem el a mobilalkalmazással terepen készített fényképeket?
----------------------------------------------------------------------------

A webes felületen egyenként az adatlapon, vagy az adminisztrációs felület
fájlok lapján. Az összes fénykép egyetlen művelettel is letölthető. A PDS
API szintén támogatja a képek egyetlen letöltésben történő lekérését.
A fényképek a Supervisor felületén is elérhetők, az adminisztrációs
funkciók rendszerinformációs oldalán.

Hogyan törölhetek adatokat?
---------------------------
Az OpenBioMaps webes felülete nem tartalmaz adattörlési funkciót, szükség
esetén azonban az adatok így is törölhetők.

Minden feltöltéshez tartozik egy bejegyzés a ``system.uploadings`` táblában.
Ennek azonosítójára hivatkozva SQL-kliensből egyszerre törölhető egy
feltöltés összes rekordja. Ha a feltöltési tábla idegen kulccsal kapcsolódik
az adattáblához, a feltöltési metaadat sorának törlése automatikusan törli
az adattábla megfelelő sorait, ez a kapcsolat azonban nem jön létre
automatikusan.

Általában biztonságosabb a szükséges sorokat kifejezetten SQL-paranccsal
törölni. Ha egy feltöltés összes sorát törölni szeretné, ezt egyetlen,
a feltöltési azonosítóra hivatkozó paranccsal teheti meg:

.. code-block:: sql

   DELETE FROM your_table WHERE uploading_id=x;


Nem tudok lekérdezni vagy megtekinteni más felhasználók számára látható adatokat
--------------------------------------------------------------------------------
A projektadatok hozzáférése valószínűleg meghatározott felhasználókra vagy
csoportokra korlátozódik, vagyis csak azok a felhasználók és csoportok
férhetnek hozzá az adatokhoz, akik számára ezt engedélyezték. A gyakorlatban
ezt a beállítást az adatfeltöltési űrlapon lehet meghatározni: megadható,
hogy mely felhasználók vagy felhasználói csoportok kapjanak olvasási vagy
módosítási hozzáférést az adott űrlappal feltöltött adatokhoz.

Ha az adatok feltöltése beállítások nélkül történik, alapértelmezés szerint
csak a projektadminisztrátorok férhetnek hozzájuk. Az adathozzáférési
beállítást a projektadminisztrátorok később SQL-parancsokkal módosíthatják,
például:

.. code-block:: sql

   UPDATE mydatabase_rules d SET read = read || 295 FROM (
   SELECT row_id FROM "public". "mydatabase" LEFT JOIN mydatabase_rules ON (obm_id=row_id) WHERE "observer" ILIKE 'Smith%') AS foo 
   WHERE foo.row_id=d.row_id


