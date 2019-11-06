Gyakran Ismételt Kérdések
*************************

Mi az OpenBioMaps?
------------------
The OpenBioMaps is a framework for biological data with spatial attributes. In this framework it is allowed to create databases. The biological and spatial data in these databases are available for anyone.

The framework contains several different databases which served by more servers. These applications are the UMN Mapserver (which serve the web maps), the PostgreSQL database server (where cthe framework's and the databases' data stored), the PostGIS library (which handle the spatial queries), the Apache webserver (which handle the web output), the OpenLayers Javascript library (which handle the web map displaying in the browsers) and finally the Debian Linux operating system which serves the backround for the whole system. 

Mi az OpenBioMaps konzorcium?
-----------------------------
The OpenBioMaps consortium has been established through cooperation between public institutions and social organizations. Their goal was to develop and operate the OpenBioMap community database framework. The members of the consortium are equal partners and they have all contributed to achievenig this objective in some ways. The partnership can be extended, if the parties wishing to join are willing to accept the system's fundamentals, satisfy the specified conditions set and the partners accept the new member.

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

kapcsolat: Kovács István, 

**Duna-Dráva Nemzeti Park Igazgatóság**

kapcsolat: Gáborik Ákos

**Fertő-Hnaság Nemzeti Park Igazgatóság**

kapcsolat: Takács Gábor

The OpenBioMaps consortium established at September 1, 2015. The OpenBioMaps Consortium Agreement will be available `here <docs/consortium_agreement_2015.pdf>`_.

Hogyan léphetek kapcsolatba a konzorciummal?
--------------------------------------------
email-en keresztül:

management@lists.openbiomaps.org

Hogyan tudok saját adatbázist készíteni?
----------------------------------------
Bármilyen biológiai, térbeli információkkal is rendelkező adatok tárolására és kezelésére létre lehet hozni új adatbázist. Ez lehet egy tudományos projekt napi használatban lévő adatbázisa, vagy archív célú adatbázis, lehet tudományos cikk, vagy pályázati adatmegjelenítési kötelezettség kapcsán létrehozott adatbázis is.

Új adatbázis projektet minden regisztrált felhasználó alapíthat, de az adatbázis csak az OpenBioMaps irányító testület jóváhagyása után kaphat végleges státuszt. Új adatbázist a bejelentkezett felhasználók az erre létrehozott webes sablon segítségével hozhatnak létre. Egy új, üres adatbázis létrehozása pár perc.

Hogyan tudok adatot feltölteni?
-------------------------------
Az adatok PostgreSQL/PostGIS adatbázisban vannak tárolva. A létrehozott adatbázisok projekt gazdája tudja meghatározni kik tölthetnek be adatokat az adatbázisba. Az adatok feltöltése közvetlenül is történhet az adatbázisba, vagy történhet egyedileg definiált adatfeltöltő sablonok segítségével pl. gpx, vagy excel fájlokból. Minden adatbázisnak egyedi adatfeltöltő felülete van.

Hogyan tudok eltárolni lekérdezéseket és hivatkozni őket?
---------------------------------------------------------
A webes felületen beállított térképi lekérdezések a bejelentkezett felhasználók számára elmenthetőek. Az elmentett lekérdezések egyedi azonosítóval hivatkozhatók és később bármikor megismételhetőek. A lekérdezések wfs/wms url-je is tárolásra kerül, így egy lekérdezés és ismétlése közötti adatbázis változások is könnyen nyomonkövethetőek.

A hivatkozások formátuma ilyen: http://openbiomaps.org/projects/database/?loadquery=xx@abcd1234

A hivatkozás böngészőben való betöltésére a projekt térkép töltődik be a lekérdezett pontokat kiemelve és a hozzá tartozó adatokat megjelenítve.

Hogyan tudok regisztrálni az OpenBioMaps-ba?
--------------------------------------------
A regisztrációhoz meghívó szükséges. Minden regisztrált felhasználó meghívhat tetszőlegesen bárkit.

A bejelentkezési név és jelszó a webes felületen keresztül adható meg vagy asztali alkalmazásokból normál http authentikácóként.

A bejelentkezett felhasználók eltárolhatják a lekérdezéseiket, tölthetnek fel adatokat, megnézhetnek korlátozottan elérhető térképeket. A bejelentkezéshez egyedileg meghatározott jogosultságok rendelhetők, amiket a különböző projektek adatgazdái állítanak be.

A regisztrációval, meghívássokkal kapcsolatban további információkért keresse az adatbázisok létrehozóit, kezelőit vagy tagjait.

Van programozható felület fejlesztőknek?
----------------------------------------
A Project Data Service (PDS) segítségével a projectek és a felhasználói adatok jogosultságfüggően projektenként lekérdezhetők webes kérésekkel az adatbázisokból.

Példa: http://openbiomaps.org/pds.php?scope=get_project_list

Ebben a példában az openbiomaps.org-on elérhető projektek listáját kérdeztük le.

A PDS JSON formában adja vissza a lekérdezett adatokat.

Szintaktikailag hibás lekérdezés esetén, hibaüzenetet ad vissza.


A PDS figyelembe veszi a lekérdező jogosultságát. Ha nincs bejelentkezve a lekérdező, alap jogosultság szerinti lekérdezésekre kap választ.


Milyen nyelvek támogatottak?
----------------------------
Nincsenek nyelvi korlátok, az oldal jelenleg Magyarul és Angolul Románul és részben Oroszul elérhető. További nyelvek vagy javítások hozzáadhatóak a rendszerhez https://github.com/OpenBioMaps/translations/blob/master/global_project_translations.csv fájl szerkesztésével.

Az adatbázisoknak egymástól független egyedi nyelvi fájljai is vannak. 

Milyen operációs rendszerekkel kompatibilis az OpenBioMaps?
-----------------------------------------------------------
A webes portál és a térkép és adatbázis szolgáltatások egyaránt kompatibilisek a legtöbb operációs rendszerrel.

A fejlesztések során viszont ezt nem szoktuk ellenőrizni. 

Hogyan tudok hozzájárulni az OpenBioMaps-hoz?
---------------------------------------------
 *   Adatbázisok létrhozásával
 *   Adatok közlésével
 *   Adatbázis szerverek létrehozásával
 *   Nyelvi fordításokkal
 *   Programozással
 *   Adományozásával

Kell fizetni valamiért?
-----------------------
Az OpenBioMaps minden szolgáltatása teljesen ingyenes!

Hol és hogyan tárolja az OpenBioMaps az adatokat? 
-------------------------------------------------
Jelenleg két szerverünk van Debrecenben a Debreceni Egyetem számítóközpontjában és 1 szerverünk van az ELTE infoparkjában. 1 szerver  Marosvásárhelyen egy a DINPI-nél.

A szerverek között adatbázis szintű szinkronizáció van. Az adatbázisok tartalma naponta le van mentve. 

Hogyan tudok az OpenBioMaps-hoz csatlakozni?
--------------------------------------------
A regisztrációhoz meghívó szükséges. Minden regisztrált felhasználó meghívhat tetszőlegesen bárkit.

A bejelentkezési név és jelszó a webes felületen keresztül adható meg vagy asztali alkalmazásokból normál http authentikácóként.

A regisztrációval, meghívássokkal kapcsolatban további információkért keresse az adatbázisok létrehozóit, kezelőit vagy tagjait. 

Elfelejtettem a jelszavamat, most mi lesz?
------------------------------------------
Nem kell aggódni, új jelszót könnyű beállítani!

Follow the "lost password" link on the login page.

A bejelentkezési lapon van egy "elfelejtett jelszó" link, azt követve meg kell adni a regisztrált email címed és a rendszer küldeni fog egy linket amit követve meg lehet újítani a jelszót.

Rózsaszín négyzetek vannak a térkép helyén
------------------------------------------
Bármilyen rendszer beállítási hiba rózsaszín négyzetekhez vezethet.

Megosztott polygonok hogyan?
----------------------------
On the profile page there are two links

    Own polygons
    Shared polygons

Following the first one, you see those polygons that you uploaded or saved (using the save selection option)

Following the second link, you see all the shared polygons including your own polygons.

In the own polygon page there is an option to share polygons with all users in the project or all logined users or anybody.

In both pages you can control, where would you like to see these polygons (as map selection or as uploading area). These options are marked by "eye" and "X" pictograms.

In both pages you can rename polygons. You can delete only your not shared polygons.

Mi az a RUM?
------------
A RUM egy angol nyelvű akroním ami a projekt nyitottságát fejezi ki. Magyarul OFM lenne.

Read Upload Modify az Olvasás Feltöltés Módosítás

Minden eleme - 0 + értékű lehet.

ahol

[-] zárt, [0] részben nyitott [+] publikus

a hozzá kapcsolódó színek pedig: - fekete 0 piros + zöld

például:

<font color="red">R</font><font color="green">U</font>M : részben nyitott olvasásra, szabadon elérhető feltöltésre és zárt a módosításra.

DOI?
----
Minden stabil adatbázis kaphat DOI-t. Továbbá lekérdezések vagy egyes adatok is kaphatnak DOI-t.

The OBM Consortium ask the DOI if the database is accepted and provide all the necessary information for DOI registration.

All databases has a DOI metadata page like:

http://danubedata.org/index.php?metadata

We create an alias of this page as http://danubedata.org/doi/ after the database got its doi.

Our DOI prefix is: 10.18426

The DOI suffixes are automatically generated and they are unique.

In every database it is possible to ask additional DOI-s for data subsets. These DOI-s will be extend the original database DOI after a /
