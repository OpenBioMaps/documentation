Gyakran Ismételt Kérdések
*************************

Mi az OpenBioMaps?
------------------
Az OpenBioMaps (OBM) egy olyan nyílt adatbázis keretrendszer, amely georeferált biológiai adatok tárolását és kezelését teszi lehetővé.

A keretrendszer több különböző ingyenesen hozzáférhető szerverből épül fel:
* UMN Mapserver - az online térképet szolgáltatja
* PostgreSQL adatbázis szerver - tárolja a keretrendszert és a feltöltött adatokat
* PostGIS könyvtár - kezeli a térbeli lekérdezéseket
* Apache webserver - az online kimenetet kezeli
* OpenLayers Javascript könyvtár - az online térkép megjelenítését kezeli a böngészőben
* Debian Linux operációs rendszer - biztosítja a hátteret az egész rendszer számára. 

Mi az OpenBioMaps konzorcium?
-----------------------------
Az OpenBioMaps konzorciumot közintézmények és civil szervezetek hozták létre 2015 szeptember elsején. A konzorcium célja, hogy az OpenBioMaps közösségi adatbázist fejlessze és működtesse. A konzorcium tagjai egyenlő partnerek, akik valamilyen módon hozzájárulnak mind a fejlesztéshez mind a működtetéshez. A konzorciumhoz bárki csatlakozhat, aki elfogadja az OpenBioMaps alaptételeit, eleget tesz annak kitételének és a már jelenlegi konzorciumi partnerek elfogadják a belépését.

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


**Fertő-Hanság Nemzeti Park Igazgatóság**

kapcsolat: Takács Gábor


Az OpenBioMaps konzorcium nyilatkozata `itt <docs/consortium_agreement_2015.pdf>`_ elérhető.

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
Az adatok PostgreSQL/PostGIS adatbázisban vannak tárolva. A létrehozott adatbázisok projekt gazdája tudja meghatározni kik tölthetnek be adatokat az adatbázisba. Az adatok adatbázisba történő feltöltése történhet közvetlenül, vagy egyedileg definiált adatfeltöltő sablonok segítségével pl. gpx, vagy excel fájlokból. Minden adatbázisnak egyedi adatfeltöltő felülete van.

Hogyan tudok eltárolni lekérdezéseket és hivatkozni őket?
---------------------------------------------------------
A webes felületen beállított térképi lekérdezések a bejelentkezett felhasználók számára elmenthetőek. Az elmentett lekérdezések egyedi azonosítóval hivatkozhatóak és később bármikor megismételhetőek. A lekérdezések wfs/wms url-je is tárolásra kerül, így egy lekérdezés és ismétlése közötti adatbázis változások is könnyen nyomonkövethetőek.

A hivatkozások formátuma ilyen: http://openbiomaps.org/projects/database/?loadquery=xx@abcd1234

A hivatkozás böngészőben való betöltésére a projekt térkép töltődik be a lekérdezett pontokat kiemelve és a hozzá tartozó adatokat megjelenítve.

Hogyan tudok regisztrálni az OpenBioMaps-be?
--------------------------------------------
A regisztrációhoz meghívó szükséges. Minden regisztrált felhasználó tetszőlegesen meghívhat bárkit.

A bejelentkezési név és jelszó a webes felületen keresztül adható meg vagy asztali alkalmazásokból normál http authentikácóként.

A bejelentkezett felhasználók eltárolhatják a lekérdezéseiket, tölthetnek fel adatokat, megnézhetnek korlátozottan elérhető térképeket. A bejelentkezéshez egyedileg meghatározott jogosultságok rendelhetőek, amiket a különböző projektek adatgazdái állítanak be.

A regisztrációval, meghívássokkal kapcsolatban további információkért keresse az adatbázisok létrehozóit, kezelőit vagy tagjait.

Van programozható felület fejlesztőknek?
----------------------------------------
A Project Data Service (PDS) segítségével a projectek és a felhasználói adatok az adatbázisokból webes kérésekkel - jogosultságtól függően - projektenként lekérdezhetőek.

Példa: http://openbiomaps.org/pds.php?scope=get_project_list

Ebben a példában az openbiomaps.org-on elérhető projektek listáját kérdeztük le.

A PDS JSON formában adja vissza a lekérdezett adatokat.

Szintaktikailag hibás lekérdezés esetén, hibaüzenetet ad vissza.


A PDS figyelembe veszi a lekérdező jogosultságát. Ha nincs bejelentkezve a lekérdező, alap jogosultság szerinti lekérdezésekre kap választ.


Milyen nyelvek támogatottak?
----------------------------
Nincsenek nyelvi korlátok, az oldal jelenleg magyarul,angolul, románul és részben oroszul elérhető. További nyelvek vagy javítások hozzáadhatóak a rendszerhez https://github.com/OpenBioMaps/translations/blob/master/global_project_translations.csv fájl szerkesztésével.

Az adatbázisoknak egymástól független egyedi nyelvi fájljai is vannak. 

Milyen operációs rendszerekkel kompatibilis az OpenBioMaps?
-----------------------------------------------------------
A webes portál, a térkép és adatbázis szolgáltatások egyaránt kompatibilisek a legtöbb operációs rendszerrel.

A fejlesztések során viszont ezt nem szoktuk ellenőrizni. 

Hogyan tudok hozzájárulni az OpenBioMaps-hoz?
---------------------------------------------
 *   Adatbázisok létrhozásával
 *   Adatok közlésével
 *   Adatbázis szerverek létrehozásával
 *   Nyelvi fordításokkal
 *   Programozással
 *   Adományozással

Kell fizetni valamiért?
-----------------------
Az OpenBioMaps minden szolgáltatása teljesen ingyenes!

Hol és hogyan tárolja az OpenBioMaps az adatokat? 
-------------------------------------------------
Jelenleg négy szerverünk van. Egy szerverünk van Debrecenben a Debreceni Egyetem informatikai központjában, egy az Eötvös Lóránd Tudományegyetem infoparkjában, egy Marosvásárhelyen a MILVUS csoport és egy a Duna-Ipoly Nemzeti Park Igazgatóság kezelésében.

A szerverek között adatbázis szintű szinkronizáció van. Az adatbázisok tartalma naponta mentésre kerül. 

Hogyan tudok az OpenBioMaps-hoz csatlakozni?
--------------------------------------------
A regisztrációhoz meghívó szükséges. Minden regisztrált felhasználó meghívhat tetszőlegesen bárkit.

A bejelentkezési név és jelszó a webes felületen keresztül adható meg vagy asztali alkalmazásokból normál http authentikácóként.

A regisztrációval, meghívássokkal kapcsolatban további információkért keresse az adatbázisok létrehozóit, kezelőit vagy tagjait. 

Elfelejtettem a jelszavamat, most mi lesz?
------------------------------------------
Nem kell aggódni, új jelszót könnyű beállítani!

Kattintson az "elfelejtett jelszó" mezőre a bejelentkezési oldalon. Adja meg a regisztrált e-mail címét, és a rendszer küldeni fog egy linket, amint keresztül új jelszót állíthat be.

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
A RUM egy angol nyelvű akroním ami a projekt nyitottságát fejezi ki magyarul OFM lenne.

Read Upload Modify magyarul Olvasás Feltöltés Módosítás

Minden eleme - 0 + értékű lehet.

ahol

[-] zárt, [0] részben nyitott [+] publikus

a hozzá kapcsolódó színek pedig: - fekete 0 piros + zöld

például:

<font color="red">R</font><font color="green">U</font>M : részben nyitott olvasásra, szabadon elérhető feltöltésre és zárt a módosításra.

DOI?
----
Minden stabil adatbázis kaphat DOI-t. Továbbá lekérdezések vagy egyes adatok is kaphatnak DOI-t.

The OBM konzorcium megkéri a DOI számot, ha az adatbázis elfogadott és biztosítja a szükséges információkat a DOI szám igényléshez.

Az összes adatbázis DOI metaadat oldala ilyen:

http://danubedata.org/index.php?metadata

Az adatbázishoz készítünk egy alternatív elérési útvonalat, ahol a "/"-jel után az adatbázis saját DOI száma található. Pl.: http://danubedata.org/doi/xxxxx.

Az OBM saját DOI elő száma: 10.18426

Az egyéni adatbáziskora mutató DOI utószámok egyediek és automatikusan generálódnak.

Minden adatbázis számára elérhető, hogy DOI számot igényeljen a specifikus lekérdezései számára. Ez azt jelenti, hogy az adatbázis DOI számát kibővítik egy "/"-jel után.
