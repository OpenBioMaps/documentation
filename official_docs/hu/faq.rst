.. raw:: html

    <style> .red {color:#aa0060; font-weight:bold; font-size:16px} </style>
    
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
A webes felületen beállított térképi lekérdezések a bejelentkezett felhasználók számára elmenthetőek. Ennek két lehetséges esete van. egyrészt el lehet magát a lekérdezést tárolni (report-ot készíteni), amely opció az adatlekérdezést mindig az aktuális adatbázis állapot szerint adja meg. Másrészt el lehet tárolni egy lekérdezés ereményét is, amely lekérdezett adatokat egy xml fájlba írja ki és az eltárolt lekérdezés betöltésekor ebből az állományból tölti be az adatokat a rendszer. Mindkét esetben egyedi, tartós azonosítót kap a lekérdezés.

A hivatkozások formátuma ilyen: http://szerver/projects/database/?LQ=xx@a1b2c3d4

Egy példa: `http://openbiomaps.org/projects/checkitout/?LQ=28@WrlMyKLVsjHi7abx <http://openbiomaps.org/projects/checkitout/?LQ=28@WrlMyKLVsjHi7abx>`_

Egy példa egy report (azaz egyedi cimkével megismételhető lekérdzésre) lekérdezésre: `http://openbiomaps.org/projects/checkitout/?report=20@hbh lekérdezés&qtable=checkitout <http://openbiomaps.org/projects/checkitout/?report=20@hbh%20lek%C3%A9rdez%C3%A9s&qtable=checkitout>`_


Hogyan tudok regisztrálni az OpenBioMaps-be?
--------------------------------------------
A regisztrációhoz meghívó szükséges. Minden regisztrált felhasználó tetszőlegesen meghívhat bárkit (bár egyes adatbázisok ezt korlátozhatják).

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

:red:`R` U M: részben nyitott olvasásra, szabadon elérhető feltöltésre és zárt a módosításra.

DOI?
----
Minden stabil adatbázisban tudunk DOI azonosítókat adni. Az OpenBioMaps a DataCite rendszeren keresztül ad DOI-t. A DOI kezelő partnerünk az MTA Könyvtár.

A DataCite DOI kezelő felületén itt található az OpenBioMaps: https://search.datacite.org/repositories/mtakik.obiomap 

DOI igényléshez szükséges a megfelelő metaadatok megadása. A rendszer automatikusan előállítja a metadat lapot amivel a DOI igénylést el lehet indítani egy adatbázishoz, de az igénylés előtt további adatok megadása is szükséges. Egy automatikus nem teljes metaadat lap így nét ki: http://openbiomaps.org/projects/checkitout/?metadata Ezen a lapon már látható, hogy mi lenne a DOI azonosítója ennek az adatbázisnak, ha kérnénk neki.

Itt látható egy példa, ahol már kértünk DOI-t egy adatbázisnak:

http://dinpi.openbiomaps.org/projects/dinpi/10.18426/obm.2e76flbd1abg/

Lehet lekérdezésekhez DOI-t kérni, ami publikációkban megadható. A publikációk DOI-ja és a lekérdezés DOI-ja egymást hivatkozzák és a citáció követést is megoldják. A tartós tárolásra került lekérdezési eredmények DOI azonosítóval megfelelőek egyes lapok által megkövetelt publikus adattárban való elhelyezés követelményének teljesítéséhez. Nemsokára ezt a szolgáltatást könyvtári repozitóriumban elhelyezéssel is ki fogjuk egészíteni.

Egy példa adatlekérdezéshez kért DOI-ra:

http://dinpi.openbiomaps.org/projects/dinpi/10.18426/obm.36vn3g36r3m0/


Az OBM saját DOI elő száma: 10.18426

Az egyéni adatbáziskora mutató DOI utószámok egyediek és automatikusan generálódnak.
