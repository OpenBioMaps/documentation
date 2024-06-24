.. raw:: html

    <style> 
    .red {color:#ff0000;font-weight:bold;}
    .green {color:#00ff00;font-weight:bold;}
    </style>
    
Gyakran Ismételt Kérdések
*************************

Mi az OpenBioMaps?
------------------
Az OpenBioMaps egy szoftver- és szolgáltatási platform a biológiai adatok kezelésére. Önállóan vagy szolgáltatásként is használható. Olyan adatbázis-alapú projektek létrehozására használható, amelyeket egyszerre több, különböző eszközökkel és hozzáférési jogosultsági szintekkel rendelkező felhasználó is használhat. Ha nem kíván saját szervert fenntartani, szolgáltatásként is használhatja, mivel egyes intézmények olyan szervereket is üzemeltetnek, amelyeken kutatási vagy civil tudományos projektek ingyenesen működnek.

Mi az OpenBioMaps konzorcium?
-----------------------------
Az OpenBioMaps konzorciumot közintézmények és civil szervezetek hozták létre 2015 szeptember elsején. A konzorcium célja, hogy az OpenBioMaps szotfevereket fejlessze és arra épülő szabadon hozzáférhető szolgáltatásokat üzemeltessen. A konzorcium tagjai egyenlő partnerek, akik valamilyen módon hozzájárulnak mind a fejlesztéshez mind a működtetéshez. A konzorciumhoz bárki csatlakozhat, aki elfogadja az OpenBioMaps alaptételeit, eleget tesz annak kitételének és a már jelenlegi konzorciumi partnerek elfogadják a belépését.

Jelenlegi OpenBioMaps partnerek:

**Debreceni Egyetem**

kapcsolat: Dr. Bán Miklós


**Duna-Ipoly Nemzeti Park Igazgatóság**

kapcsolat: Baranyai Zsolt


**Eötvös Loránd Tudományegyetem**

kapcsolat: Ritter Dávid


**WWF Magyarország**

kapcsolat: Sipos Katalin


**Eszterházy Károly Egyetem**

kapcsolat: Dr. Pénzesné Kónya Erika


**Milvus Csoport Egyesület**

kapcsolat: Papp Edgár


**Duna-Dráva Nemzeti Park Igazgatóság**

kapcsolat: Gáborik Ákos


**Fertő-Hanság Nemzeti Park Igazgatóság**

kapcsolat: Takács Gábor


Az OpenBioMaps konzorcium nyilatkozata `itt <docs/consortium_agreement_2015.pdf>`_ elérhető.

Hogyan léphetek kapcsolatba a konzorciummal?
--------------------------------------------
email-en keresztül:

management@lists.openbiomaps.org

Hogyan tudok saját adatbázist projektet készíteni/alapítani?
------------------------------------------------------------
Ha már tagja egy szerveren lévő projektnek, akkor a webes felület segítségével új adatbázis-projektet alapíthat ugyanazon a szerveren. Ez egy űrlap kitöltéssel elvégezhető egyszerű folyamat.


Hogyan tudok adatot feltölteni?
-------------------------------
Egyszerű válasz: adatfeltöltési űrlapok használatával.
Vagy esetleg bármilyen PostgreSQL kliens használatával, bár ez a megoldás csak nagy mennyiségű adat alkalmi importálásához ajánlott.


Hogyan férhetek hozzá az adatokhoz?
-----------------------------------
- A webes felületen keresztül térképes vagy szöveges lekérdezésekkel.
- PostgeSQL kliens segítségével.
- Az OpenBioMaps R csomag használatával.
- A webes felületen keresztül történő adatmegosztás használatával.
- Adatexporttal a webes felületen keresztül.


Hogyan tudok regisztrálni egy OpenBioMaps adatbázis proejektbe?
---------------------------------------------------------------
A regisztrációhoz meghívás szükséges. Bármely regisztrált tag meghívhat új felhasználókat. Ezen kívül alapértelmezetten rendelkezésre áll a bejelentkezési felületről egy meghívó igénylő űrlap, aminek a kitöltésével új felhazsnálók igényelhetnek meghívót egy projekthez való csatlakozáshoz. Továbbá létezik egy OpenID modul, amely lehetővé teszi Google fiókkal való regiszráviót és bejelentkezést.

A regisztrációval és a meghívásokkal kapcsolatos további információkért kérjük, forduljon a csatlakozni kívánt adatbázis létrehozóihoz vagy adminisztrátoraihoz.


Van programozható felület fejlesztőknek?
----------------------------------------
Igen. A projektadat-szolgáltatás (PDS) lehetővé teszi a projektek és a felhasználói adatok lekérdezését projektenként, az adatbázisokból érkező URL-kéréseken keresztül.

Példa: https://openbiomaps.org/pds.php?scope=get_project_list

További információkért látogasson el az API dokumentációba.


Milyen nyelvek támogatottak?
----------------------------
Nincsenek nyelvi korlátozások, de az OpenBioMaps jelenleg magyar, angol, román, spanyol és részben orosz nyelven érhető el. További nyelvek vagy fordítások a https://translate.openbiomaps.org felületen keresztül adhatók hozzá.

Minden projektnek egyéni nyelvi beállításai és a hozzá tartozó fordítások lehetnek. 


Hogyan tudok hozzájárulni az OpenBioMaps-hoz?
---------------------------------------------
- Adatbázis-projekt létrehozásával/alapításával
- Adatok feltöltéséval adatbázis-projektbe
- Új OpenBioMaps szerver létrehozásával
- Adatbázisok hosztolásával a szervereden
- Új nyelvek hozzáadásával vagy meglévő fordítások javításával
- Szoftverfejlesztéssel
- Pénzügyi támogatással


Kell fizetni valamiért?
-----------------------
Az OpenBioMaps minden összetevője és szolgáltatása teljesen ingyenes, de a fejlesztések egy része nem önkéntes munka, azaz fizetünk a fejlesztőknek így minden támogatást köszönettel fogadunk a fejlesztéshez!


Hol és hogyan tárolja az OpenBioMaps az adatokat? 
-------------------------------------------------
Minden OpenBioMaps szerver a saját adatbázisában és fájlrendszerében tárolja az adatokat.


Van valamilyen biztonsági mentés megoldás?
------------------------------------------
Nincs központosított biztonsági mentés, mivel az OpenBioMapsban nincs központosított adatkezelés. Minden szerver saját biztonsági mentési megoldással rendelkezik, de néhány szerver egymás tárolókapacitását használja archiválásra.


Elfelejtettem a jelszavamat, most mi lesz?
------------------------------------------
Ne aggódj, nagyon könnyű új jelszót szerezni.

Kövesse a bejelentkezési oldalon található "Elveszett jelszó" linket.

Ott megadhatja a bejelentkezési e-mail címét. Miután elküldte, kap egy e-mailt a rendszertől, amely tartalmaz egy linket, amelyet követve bejelentkezhet a fiókjába, és beállíthat egy új jelszót.

Rózsaszín négyzetek vannak a térkép helyén
------------------------------------------
Ennek az oka valamilyen konfigurációs hiba lehet, amely a térképi rétegekkel vagy az adatkérések beállításaival függhet össze.


Mi az a RUM?
------------
A RUM egy angol nyelvű akroním ami a projekt nyitottságát fejezi ki magyarul OFM lenne.

Read Upload Modify magyarul Olvasás Feltöltés Módosítás

Minden eleme - 0 + értékű lehet.

ahol

[-] zárt, [0] részben nyitott [+] publikus

a hozzá kapcsolódó színek pedig: - fekete 0 piros + zöld

például:

.. role:: red
.. role:: green

:red:`R` :green:`U` **M**: részben nyitott olvasásra, szabadon elérhető feltöltésre és zárt a módosításra.


Lehetséges DOI-t rendelni az adatbázisokhoz?
--------------------------------------------
Igen, minden véglegesített állapotú adatbázis kaphat DOI-t a DataCite DOI szolgáltatás segítségével.

Minden adatbázisnak van egy DOI metaadat oldala, mint például:

https://dinpi.openbiomaps.org/projects/danubefish/index.php?metadata

DOI-előtagunk a DataCite-ban: 10.18426

A DOI utótagok automatikusan generálódnak és egyediek.

Minden adatbázisban lehetőség van további DOI-kat rendelni egyes adatkészletekhez.


Hol találom meg az OpenBioMaps szerverek listáját?
--------------------------------------------------
A regisztrált szerverek egy OpenBioMaps adatbázisában találhatók a https://openbiomaps.org/projects/openbiomaps_network címen.


Hogyan használható az OpenBioMaps mobilalkalmazás?
--------------------------------------------------
Iphone-on vagy Androidon (jelenleg csak az Androidos verzió működik). A felhasználóknak be kell jelentkezniük a saját szerverükön kersztül, hogy érhessék a projektükben rendelkezésre álló adatfeltöltő űrlapokat. A bejelentkezés és az űrlapok letöltése után az alkalmazás offline is használható. A jelenlegi alaptérkép Google alapú, amely csak akkor működik offline, ha a Google terékép alkalmazáson kersztül a célterületet letöltjük offline használatra.

Azokat a szervereket listázza ki a mobil alkalmazás, amelyek regisztrálva vannak az https://openbiomaps.org/projects/openbiomaps_network adatbázisban.


Hol található meg az OpenBioMaps R csomag?
------------------------------------------
Egyelőre csak fejlesztői csomagként érhető el itt: https://github.com/OpenBioMaps/obm.r.

.. _What-data-download-options-are-there:

Milyen adat letöltési lehetőségek vannak?
-----------------------------------------
* Csv, kml, json és egyéb modulok használatával, ha ezek rendelkezésre állnak
* QGIS-en keresztül
* Könyvjelzők és állandó hivatkozások használatával
* Az R csomag használatával

A mobil applikációval terepen készített fotókhoz hogyan/hol lehet hozzáférni?
-----------------------------------------------------------------------------
A webes felületen egyesével az adatok saját adatlapján, vagy az adminisztratív felületen a fájlok lapon. Akár egyben is le lehet tölteni az összes képet. A pds api is támogatja a képek egyben letöltését. A supervisor felületen (az admin oldalakon/rendszerinformáción fülön található) keresztül is.

Hogyan tudok adatokat törölni?
------------------------------
Az OBM webes felület nem tartalmaz adat törlési funkciót, de ettől függetlenül van lehetőség az adatok törlésére, ha ez valóban szükségesnek látszik.

Minden feltöltésnek van egy bejegyzése az system.uploadings  táblában. Annak van egy id-jával hivatkozva egyszerre lehet törölni egy feltöltés összes rekordját SQL kliensből. Amennyiben az  uploading tábla idegen kulcscsal össze van kötve az adattáblával,  akkor elegendő a feltöltési metaadat sort törölni és az törli a hozzá tartozó adatsorokat az adattáblából, de ez az összekapcsolás nincs automatikusan beállítva. Általában biztonságosabb, ha explicit módon töröljük a szükséges sorokat egy SQL paranccsal. Amennyiben egy feltöltés összes sorát szeretnénk törölni praktikusan a feltöltési azonosítóra hivatkozva egyetlen paranccsal megtehető:

```sql
DELETE FROM your_table WHERE uploading_id=x;
```

Nem látom és nem tudom lekérdezni azadatokat, amelyeket más felhasználók látnak
-------------------------------------------------------------------------------
Valószínűleg a projekt adatai korlátozott hozzáférésűek, ami úgy van meghatározva, hogy csak bizonyos felhasználók vagy felhasználó csoportok férhetnek hozzá az adatokhoz. Ez a beállítás a gyakorlatban úgy érvényesül, hogy az adatfeltöltő űrlap beállításai között kell megadni, mely felhasználók vagy felhasználó csoportoknak lesz olvasási, vagy módosítási hozzáférése egy adott űrlappal feltöltött adatokhoz. 
Amennyiben vannak olyan adatok feltöltve, ahol nem volt beállítva semmi, akkor alapértelmezetten csak a projekt gazdák számára lesz elérhető az így feltöltött adat. Az adatok hozzáférésének beállítását a projekt gazdák SQL parancsok segítségével tudják utólag módosítani, pl: 

```sql
UPDATE mydatabase_rules d SET read = read || 295 FROM (
SELECT row_id FROM "public"."mydatabase" LEFT JOIN mydatabase_rules ON (obm_id=row_id) WHERE "observer" ILIKE 'Smith%') AS foo 
WHERE foo.row_id=d.row_id
```
