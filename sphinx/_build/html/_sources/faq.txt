Frequently Asked Questions
**************************

What is OpenBioMaps?
--------------------
The OpenBioMaps is a framework for biological data with spatial attributes. In this framework it is allowed to create databases. The biological and spatial data in these databases are available for anyone.

The framework contains several different databases which served by more servers. These applications are the UMN Mapserver (which serve the web maps), the PostgreSQL database server (where cthe framework's and the databases' data stored), the PostGIS library (which handle the spatial queries), the Apache webserver (which handle the web output), the OpenLayers Javascript library (which handle the web map displaying in the browsers) and finally the Debian Linux operating system which serves the backround for the whole system. 

What is OpenBioMaps consortium?
-------------------------------
The OpenBioMaps consortium has been established through cooperation between public institutions and social organizations. Their goal was to develop and operate the OpenBioMap community database framework. The members of the consortium are equal partners and they have all contributed to achievenig this objective in some ways. The partnership can be extended, if the parties wishing to join are willing to accept the system's fundamentals, satisfy the specified conditions set and the partners accept the new member.


Current OpenBioMaps partners:


**University of Debrecen**

contact: Dr. Miklós Bán, banm@vocs.unideb.hu.


**Danube-Ipoly National Park Directorate**

contact: Zsolt Baranyai, baranyaizs@dinpi.hu.


**Eötvös Loránd University**

contact: Dr. Tibor Standovár, standi@caesar.elte.hu


**WWF World Wildlife Fund for Nature Hungary**

contact: Katalin Sipos, katalin.sipos@wwf.hu


**Eszterházy Károly University**

contact: Dr. Erika Pénzesné Kónya, konya.erika@uni-eszterhazy.hu


**Milvus Group Association**
contact: István Kovács, 

**Danube-Dráva National Park Directorate**

contact:


The OpenBioMaps consortium established at September 1, 2015. The OpenBioMaps Consortium Agreement will be available `here <docs/consortium_agreement_2015.pdf>`_.

How can I contact the consortium?
---------------------------------
By email:

management@lists.openbiomaps.org

How can I create a new database?
--------------------------------
Bármilyen biológiai, térbeli információkkal is rendelkező adatok tárolására és kezelésére létre lehet hozni új adatbázist. Ez lehet egy tudományos projekt napi használatban lévő adatbázisa, vagy archív célú adatbázis, lehet tudományos cikk, vagy pályázati adatmegjelenítési kötelezettség kapcsán létrehozott adatbázis is.

Új adatbázis projektet minden regisztrált felhasználó alapíthat, de az adatbázis csak az OpenBioMaps irányító testület jóváhagyása után kaphat végleges státuszt. Új adatbázist a bejelentkezett felhasználók az erre létrehozott webes sablon segítségével hozhatnak létre. Egy új, üres adatbázis létrehozása pár perc.

How can I upload data?
----------------------
Az adatok PostgreSQL/PostGIS adatbázisban vannak tárolva. A létrehozott adatbázisok projekt gazdája tudja meghatározni kik tölthetnek be adatokat az adatbázisba. Az adatok feltöltése közvetlenül is történhet az adatbázisba, vagy történhet egyedileg definiált adatfeltöltő sablonok segítségével pl. gpx, vagy excel fájlokból. Minden adatbázisnak egyedi adatfeltöltő felülete van.

How can I store queries and how can I refere them?
--------------------------------------------------
A webes felületen beállított térképi lekérdezések a bejelentkezett felhasználók számára elmenthetőek. Az elmentett lekérdezések egyedi azonosítóval hivatkozhatók és később bármikor megismételhetőek. A lekérdezések wfs/wms url-je is tárolásra kerül, így egy lekérdezés és ismétlése közötti adatbázis változások is könnyen nyomonkövethetőek.

A hivatkozások formátuma ilyen: http://openbiomaps.org/projects/database/?loadquery=xx@abcd1234

A hivatkozás böngészőben való betöltésére a projekt térkép töltődik be a lekérdezett pontokat kiemelve és a hozzá tartozó adatokat megjelenítve.

How can I sign up for OpenBioMaps?
----------------------------------
A regisztrációhoz meghívó szükséges. Minden regisztrált felhasználó meghívhat tetszőlegesen bárkit.

A bejelentkezési név és jelszó a webes felületen keresztül adható meg vagy asztali alkalmazásokból normál http authentikácóként.

A bejelentkezett felhasználók eltárolhatják a lekérdezéseiket, tölthetnek fel adatokat, megnézhetnek korlátozottan elérhető térképeket. A bejelentkezéshez egyedileg meghatározott jogosultságok rendelhetők, amiket a különböző projektek adatgazdái állítanak be.

A regisztrációval, meghívássokkal kapcsolatban további információkért keresse az adatbázisok létrehozóit, kezelőit vagy tagjait.

Is there any programming interface for developers?
--------------------------------------------------
A Project Data Service (PDS) segítségével a projectek és a felhasználói adatok jogosultságfüggően projektenként lekérdezhetők webes kérésekkel az adatbázisokból.

Példa: http://openbiomaps.org/pds/service.php?project=fishdb

Ebben a példában a Halas adatbázis project információs lapját kérdeztük le.

A PDS JSON formában adja vissza a lekérdezett adatokat.

Szintaktikailag hibás lekérdezés esetén, hibaüzenetet ad vissza.

Érvénytelen adat kérés esetén, üres objektumot kapunk válaszként.

A PDS figyelembe veszi a lekérdező jogosultságát. Ha nincs bejelentkezve a lekérdező, alap jogosultság szerinti lekérdezésekre kap választ.

A PDS még fejlesztés alatt áll, a meglévő funkciók dokumentációja érdekében keresse Bán Miklóst [biomaps 'at' vocs.unideb.hu]

What languages are supported?
-----------------------------
Nincsenek nyelvi korlátok, az oldal jelenleg Magyarul és Angolul és részben Románul elérhető.

Az adatbázisoknak egymástól független egyedi nyelvi fájljai vannak. 

Which operating systems are compatible width OpenBioMaps?
---------------------------------------------------------
A webes portál és a térkép és adatbázis szolgáltatások egyaránt kompatibilisek a legtöbb operációs rendszerrel.

A fejlesztések során viszont ezt nem szoktuk ellenőrizni. 

How can I contribute to OpenBioMaps?
------------------------------------
 *   Adatbázisok létrhozásával
 *   Adatok közlésével
 *   Adatbázis szerverek hostolásával, adományozásával
 *   Nyelvi fordításokkal
 *   Programozással

Shoud I pay for anything?
-------------------------
Az OpenBioMaps minden szolgáltatása teljesen ingyenes!

How and where the OpenBioMaps strore the data?
----------------------------------------------
Jelenleg két szerverünk van Debrecenben a Debreceni Egyetem számítóközpontjában és 1 szerverünk van az ELTE infoparkjában. 1 szerver  Marosvásárhelyen egy a DINPI-nél.

A szerverek között adatbázis szintű szinkronizáció van. Az adatbázisok tartalma naponta le van mentve. 

How can I join to the OpenBioMaps?
----------------------------------
A regisztrációhoz meghívó szükséges. Minden regisztrált felhasználó meghívhat tetszőlegesen bárkit.

A bejelentkezési név és jelszó a webes felületen keresztül adható meg vagy asztali alkalmazásokból normál http authentikácóként.

A bejelentkezett felhasználók eltárolhatják a lekérdezéseiket, tölthetnek fel adatokat, megnézhetnek korlátozottan elérhető térképeket. A bejelentkezéshez egyedileg meghatározott jogosultságok rendelhetők, amiket a különböző projektek adatgazdái állítanak be.

A regisztrációval, meghívássokkal kapcsolatban további információkért keresse az adatbázisok létrehozóit, kezelőit vagy tagjait. 

I lost my password, how can I get a new?
----------------------------------------
Don't worry, It is very easy to get a new password.

Follow the "lost password" link on the login page.

There you can type your login email address. After you sent it the system will send and email for you which contains a link.

Following this link you will be log in temporarily and you can change your password. 

Pink squares appear on the map page
-----------------------------------
It can be related with the layers or the mapfile settings.

How can I control the shared polygons?
--------------------------------------
On the profile page there are two links

    Own polygons
    Shared polygons

Following the first one, you see those polygons that you uploaded or saved (using the save selection option)

Following the second link, you see all the shared polygons including your own polygons.

In the own polygon page there is an option to share polygons with all users in the project or all logined users or anybody.

In both pages you can control, where would you like to see these polygons (as map selection or as uploading area). These options are marked by "eye" and "X" pictograms.

In both pages you can rename polygons. You can delete only your not shared polygons.

What is the RUM?
----------------
RUM is acronym of database openness classes:

Read Upload Modify

All levels can be - 0 +

where

[-] is not public, [0] is partially public and the [+] is public

and the colors are: - black 0 red + green

e.g.

RUM partial public read, public upload and no public modify 

Are there DOI for databases?
----------------------------
Every accepted database can get DOI through the DataCite DOI Service.

The OBM Consortium ask the DOI if the database is accepted and provide all the necessary information for DOI registration.

All databases has a DOI metadata page like:

http://danubedata.org/index.php?metadata

We create an alias of this page as http://danubedata.org/doi/ after the database got its doi.

Our DOI prefix is: 10.18426

The DOI suffixes are automatically generated and they are unique.

In every database it is possible to ask additional DOI-s for data subsets. These DOI-s will be extend the original database DOI after a /
