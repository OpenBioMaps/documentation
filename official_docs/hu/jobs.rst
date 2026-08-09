:author: Miklós Bán
:date: 2026-08-09

.. _jobs:

Háttérfolyamatok
****************

A háttérfolyamatok önálló programok, amelyek ütemezett vagy manuálisan
indított feladatokat hajtanak végre egy OpenBioMaps-projekt számára. Olyan
műveletekhez használhatók, amelyeket nem szükséges interaktív webes kérés
részeként futtatni, például adatvalidáláshoz, karbantartáshoz,
importáláshoz, exportáláshoz, térbeli feldolgozáshoz és értesítések
küldéséhez.

A háttérfolyamatok általában PHP nyelven készülnek, de egy
OpenBioMaps-szerver a szerveradminisztrátor által telepített és
engedélyezett Python, R, Bash vagy más nyelvet is támogathat.

A projektadminisztrátorok a **Profile > Project administration >
Background jobs** felületen kezelhetik a háttérfolyamatokat.
Jogosultságaiktól és a szerver konfigurációjától függően az
adminisztrátorok:

* előre meghatározott háttérfolyamatokat telepíthetnek a központi
  háttérfolyamat-repository-ból;
* projektspecifikus háttérfolyamatokat tölthetnek fel;
* konfigurálhatják a háttérfolyamatok paramétereit;
* beállíthatják a végrehajtási ütemezéseket;
* engedélyezhetik vagy letilthatják a háttérfolyamatokat;
* manuálisan elindíthatják a háttérfolyamatokat;
* megvizsgálhatják a legutóbbi végrehajtások eredményeit; valamint
* szerkeszthetik a háttérfolyamatok forráskódját.

Az adminisztrációs felület áttekintését és a rendszerszintű ütemezési
példát lásd: :ref:`Háttérfolyamatok <background-jobs>`.


Háttérfolyamat-repository
=========================

Az előre meghatározott OpenBioMaps-háttérfolyamatokat az
`OpenBioMaps web-app-jobs repository
<https://gitlab.com/openbiomaps/web-app-jobs>`_ tartalmazza.

A repository ettől a dokumentációtól függetlenül változhat. Egy
háttérfolyamat telepítése vagy frissítése előtt tekintse át a kiválasztott
verzió forráskódját és konfigurációját.

A repository README fájlja ismerteti a PHP-háttérfolyamatok hagyományos
elrendezését. Egy PHP-háttérfolyamat általában két azonos nevű fájlból áll:

* egy, a ``jobs/run/`` könyvtárban elhelyezett végrehajtható fájlból; és
* egy, a ``jobs/run/lib/`` könyvtárban elhelyezett támogató
  könyvtárfájlból.

A más nyelven írt háttérfolyamatok állhatnak egyetlen, a ``jobs/run/``
könyvtárban található végrehajtható fájlból. A pontos telepítési elrendezés
az OpenBioMaps verziójától és a szerver konfigurációjától függhet.


Háttérfolyamat telepítése és konfigurálása
==========================================

Ahol ez támogatott, egy előre meghatározott háttérfolyamat a központi
repository-ból telepíthető a háttérfolyamatok adminisztrációs felületén. Egy
projektspecifikus háttérfolyamat feltölthető, vagy arra jogosult
szerveradminisztrátor által manuálisan is telepíthető.

Egy háttérfolyamat telepítése után:

#. tekintse át a forráskódját;
#. tekintse át és állítsa be az összes projektspecifikus paramétert;
#. ellenőrizze, hogy a hivatkozott táblák, oszlopok, modulok, sablonok és
   könyvtárak léteznek;
#. a **Run** használatával futtassa manuálisan a háttérfolyamatot;
#. várja meg a végrehajtás befejezését;
#. vizsgálja meg az eredményt és a szervernaplókat;
#. ellenőrizze az adatbázisban vagy a fájlrendszerben végrehajtott
   módosításokat; valamint
#. csak a manuális teszt sikeres befejezése után engedélyezze az ismétlődő
   végrehajtást.

A háttérfolyamatok paraméterei és adatbázisra vonatkozó feltételezései
megvalósításspecifikusak. Egy adott projekthez létrehozott háttérfolyamat
módosítás nélkül nem feltétlenül működik másik projektben.


Ütemezés
========

Az ismétlődő háttérfolyamatok a projekthez konfigurált ütemezőt használják.
A szerver rendszerszintű ütemezőjének rendszeresen meg kell hívnia az
OpenBioMaps projektütemezőjét; ellenkező esetben a konfigurált
háttérfolyamatok nem indulnak el automatikusan.

A központi repository a következő hagyományos cron-példát tartalmazza:

.. code-block:: console

   */5 * * * * /usr/bin/php /var/www/html/biomaps/projects/YOUR-PROJECT/jobs.php > /dev/null 2>&1

Előfordulhat, hogy a parancsot a webszerver felhasználójával – általában a
``www-data`` felhasználóval – kell futtatni. Az útvonalak, a végrehajtó
felhasználók, a konténerek és a PHP-parancsok telepítésenként eltérnek.
Docker-telepítésben a projektütemezőt általában az alkalmazáskonténeren
belül hívják meg.

A rendszerszintű meghívás időköze korlátozza az ütemezés tényleges
felbontását. Ha például a projektütemezőt ötpercenként hívják meg, egy
háttérfolyamat nem indítható el megbízhatóan percenként.

Az adminisztrációs áttekintést és a Docker-alapú példát lásd:
:ref:`Háttérfolyamatok ütemezése <background-jobs>`.


Felügyelet és hibaelhárítás
===========================

A háttérfolyamatok adminisztrációs felülete – ahol ez támogatott –
megjeleníti a legutóbbi végrehajtás állapotát és kimenetét. Részletesebb
információk lehetnek elérhetők a **Project administration > Server logs**
felületen.

Egy háttérfolyamat hibájának vizsgálatakor ellenőrizze:

* meghívja-e a rendszerütemező a projektütemezőt;
* engedélyezve van-e a háttérfolyamat;
* esedékes-e az ütemezés szerint;
* fut-e még egy másik végrehajtás;
* a végrehajtó felhasználó képes-e olvasni és írni a szükséges fájlokat;
* telepítve vannak-e a szükséges programok és nyelvi csomagok;
* léteznek-e a konfigurált táblák és oszlopok;
* elegendők-e az adatbázis-jogosultságok;
* van-e elegendő szabad hely az ideiglenes és exportkönyvtárakban; valamint
* tartalmaz-e hibát az alkalmazás, a háttérfolyamatok, a PHP, a konténer
  vagy a rendszer naplója.

Egy háttérfolyamat akkor is befejeződhet anélkül, hogy a kívánt eredményt
létrehozná, ha konfigurációja nem felel meg a projekt sémájának. Ne csak a
sikeres kilépési állapotra hagyatkozzon, hanem ellenőrizze a létrehozott
rekordokat, fájlokat vagy értesítéseket is.


Biztonság
=========

Egy háttérfolyamat telepítése vagy szerkesztése végrehajtható kód szerverre
telepítésével egyenértékű. Ezeket a funkciókat megbízható
adminisztrátorokra kell korlátozni.

Egyéni vagy frissített háttérfolyamat telepítése előtt vizsgálja meg a
következő kockázatokat:

* SQL-injektálás;
* operációsrendszer-parancsok injektálása;
* nem biztonságos fájlútvonalak és fájljogosultságok;
* adatbázis-hitelesítési adatok vagy személyes adatok felfedése;
* korlátlan adatbázis-lekérdezések;
* korlátlan memória-, processzor- vagy lemezhasználat;
* nem biztonságos hálózati kérések;
* hiányzó hozzáférés-ellenőrzések;
* csatolmányok és archívumok nem biztonságos kezelése; valamint
* nem szándékos ismételt végrehajtás.

Adatokat frissítő vagy törlő háttérfolyamatok futtatása előtt készítsen
megfelelő biztonsági mentést. Az exportáló háttérfolyamatoknak alkalmazniuk
kell a projekt adathozzáférési és adatvédelmi követelményeit a létrehozott
fájlokra. A létrehozott archívumokat és jelentéseket védett helyen kell
tárolni, és el kell távolítani, amikor már nincs rájuk szükség.


A központi repository háttérfolyamatai
======================================

A következő háttérfolyamat-könyvtárak találhatók meg a központi
repository-ban. Egyes háttérfolyamatok általános célúak, míg másokat egy
adott projekthez vagy munkafolyamathoz fejlesztettek.

Az alábbi leírások a repository nevei és az elérhető repository-metaadatok
által jelzett célt foglalják össze. A telepítendő verzió forráskódjában
ellenőrizni kell a pontos működést, a konfigurációs paramétereket, az
adatbázis-módosításokat, az értesítések címzettjeit és a hibakezelést.


Általános adat- és fájlfeldolgozás
----------------------------------

``clean_temp``
   Az OpenBioMaps-munkafolyamatok által létrehozott ideiglenes adatokat
   vagy fájlokat törli. Engedélyezése előtt tekintse át a konfigurált
   útvonalakat, táblákat, megőrzési szabályokat és törlési feltételeket. A
   hibás tisztítási konfiguráció még szükséges fájlokat vagy adatokat is
   eltávolíthat.

``export_attachments``
   Exportot készít a projekt csatolmányaiból. Olyan munkafolyamatokban
   használható, amelyek a háttérben készítenek csatolmányarchívumokat.
   Ellenőrizze a rekordok kiválasztásának módját, a hozzáférési szabályok
   alkalmazását, az archívum létrehozási helyét és elérhetőségének
   időtartamát.

``export_data``
   Háttérben futó adatexportot készít. A kiválasztott táblák, oszlopok,
   szűrők, a kimeneti formátum, a hozzáférés-ellenőrzések, a kimenet helye
   és a letöltési mechanizmus a háttérfolyamat konfigurációjától és a
   forráskód verziójától függ.

``intersect_data``
   Térbeli metszési munkafolyamatot hajt végre a konfigurált adatkészletek
   között. Futtatása előtt ellenőrizze a forrás- és céltáblákat,
   geometriaoszlopokat, térbeli referenciarendszereket és a frissítés
   működését.

``valid_list_values``
   A konfigurált listamezőkhöz kapcsolódó értékeket ellenőrzi vagy dolgozza
   fel. A forráskód áttekintésével állapítsa meg, hogy csak jelenti-e az
   érvénytelen értékeket, vagy módosítja is azokat.


Megfigyelési listák feldolgozása
--------------------------------

``observation_lists``
   A szabványos megfigyelésilista-munkafolyamat használatával dolgozza fel
   a megfigyelési listákat. Az adatbázisra vonatkozó feltételezéseit és az
   ideiglenes adatok kezelését össze kell vetni a projekt sémájával.

``observation_lists_without_temp``
   A megfigyelési listák feldolgozásának olyan változata, amelyet a
   szabványos ideiglenesadatszakaszt nem használó munkafolyamatokhoz
   terveztek.

``incomplete_observation_lists``
   A hiányos megfigyelési listákat dolgozza fel. A munkafolyamat az
   ``incomplete_list_processed`` és az ``incomplete_list_unprocessed``
   üzenetsablont használhatja a feldolgozás sikerességének közlésére. A
   telepített forrásverzióban ellenőrizze a sablonok tényleges használatát
   és címzettjeit.


Taxonómiai feldolgozás
----------------------

``species_name_validation``
   A projektadatokban használt tudományos neveket validálja. Tekintse át a
   konfigurált taxontáblát, forrásmezőket, az elfogadott nevekre vonatkozó
   szabályokat, valamint azt, hogy a háttérfolyamat csak jelenti-e a
   problémákat, vagy módosítja is a rekordokat.

``superspecies_autonames``
   Egy superspecies-munkafolyamat által használt neveket hoz létre vagy tart
   karban. Ez a háttérfolyamat projektspecifikus taxonómiai konvencióktól
   függ, ezért nem szabad engedélyezni a konfigurált táblák és névadási
   szabályok felülvizsgálata nélkül.

``linnaeus_job``
   Linnaeushoz kapcsolódó, projektspecifikus feldolgozási munkafolyamatot
   valósít meg. Pontos taxonómiai műveletét és szükséges sémáját a
   repository áttekintése nem ismerteti; ezeket a forráskódból és a
   konfigurációból kell meghatározni.


Importálás és külső integrációk
-------------------------------

``iNatHarvester``
   Megfigyelési adatokat gyűjt az iNaturalist rendszerből OpenBioMaps-
   projektbe történő importáláshoz vagy feldolgozáshoz. Használata előtt
   tekintse át a távoli API beállításait, a taxon- és
   felhasználómegfeleltetést, a duplikátumészlelést, a földrajzi szűrőket,
   a sebességkorlátozást és a céltábla konfigurációját.

``hunviphab_tracklogs``
   A HunVipHab-munkafolyamat útvonalnaplóit dolgozza fel. Ez egy
   specializált háttérfolyamat, amelynek szükséges tábláit,
   útvonalnapló-formátumát és kimeneti mezőit a forráskódból kell
   ellenőrizni.

``chirovox_rename``
   Átnevezési műveletet hajt végre a ChiroVox-munkafolyamathoz. Futtatása
   előtt a forráskód alapján azonosítsa az érintett fájlokat vagy
   rekordokat, a névadási konvenciót és az ütközések kezelését.


Adatbázis-karbantartás és egyéni SQL
-----------------------------------

``sql_daily``
   Konfigurált SQL-t futtat ismétlődő karbantartási vagy feldolgozási
   feladatként. Az SQL-háttérfolyamatok tetszőleges projektadatot
   módosíthatnak vagy törölhetnek, ezért vizsgáljon meg minden utasítást,
   tesztelje őket nem éles környezetben, és szükség esetén készítsen
   biztonsági mentést.

``sql_maintenance``
   PostgreSQL-karbantartást végez az ``ANALYZE`` és/vagy a ``VACUUM``
   használatával. Ezek a műveletek frissítik a lekérdezéstervező
   statisztikáit, és felszabadítják vagy újrafelhasználhatóvá teszik az
   elavult sorverziókhoz kapcsolódó tárhelyet. Tekintse át a kiválasztott
   relációkat és beállításokat, az erőforrás-igényes karbantartást pedig
   egyeztesse a szerveradminisztrátorral.


Projektspecifikus munkafolyamatok
---------------------------------

``kaszalasi_bejelento``
   Projektspecifikus kaszálásbejelentési munkafolyamatot valósít meg. Ez a
   változat értesítésekhez kapcsolódó feldolgozást is tartalmaz. Használata
   előtt a forráskódból ellenőrizze az érintett rekordokat,
   üzenetsablonokat, címzetteket és feltételeket.

``kaszalasi_bejelento_ertesites_nelkul``
   A kaszálásbejelentési munkafolyamat értesítések nélküli változatát
   valósítja meg. Más adatfeldolgozási funkciókat megoszthat a
   ``kaszalasi_bejelento`` háttérfolyamattal; ezeket a forráskódban kell
   ellenőrizni.

``telepules_hozzarendeles``
   Települést rendel a konfigurált rekordokhoz. Valószínűleg térbeli
   adatoktól és projektspecifikus mezőktől függ. Ellenőrizze a
   határadatokat, a geometriaoszlopokat, a térbeli referenciarendszereket,
   az egyeztetési szabályokat, valamint a településen kívüli vagy annak
   határán fekvő rekordok kezelését.


Fejlesztés és tesztelés
-----------------------

``job_teszt``
   A háttérfolyamatok telepítésének vagy végrehajtásának ellenőrzésére
   szolgáló tesztfeladat. Forráskódjának felülvizsgálata nélkül nem szabad
   éles adatfeldolgozási feladatként kezelni.


Háttérfolyamatok frissítése
===========================

Egy háttérfolyamat frissítése megváltoztathatja a szükséges paramétereket,
az adatbázisra vonatkozó feltételezéseket és a mellékhatásokat. A telepített
verzió lecserélése előtt:

#. őrizze meg a jelenlegi forráskódot és konfigurációt;
#. tekintse át a központi repository módosításait;
#. ellenőrizze az adatbázis-sémamigrációkat és az új függőségeket;
#. tiltsa le az ismétlődő ütemezést;
#. ahol lehetséges, telepítse a frissítést egy tesztprojektben;
#. futtassa manuálisan, és vizsgálja meg az eredményt; valamint
#. csak a validálás után állítsa vissza az ütemezést.

A központi repository-ból történő frissítés felülírhatja a helyi
módosításokat. A projektspecifikus változtatásokat tartsa verziókövetés
alatt, vagy külön egyéni háttérfolyamatként tartsa karban.


Egyéni háttérfolyamatok készítése
================================

Egy egyéni háttérfolyamatnak:

* egyértelműen dokumentált céllal kell rendelkeznie;
* minden konfigurációt validálnia kell az adatok módosítása előtt;
* paraméterezett SQL-t kell használnia;
* kerülnie kell a hitelesítési adatok forráskódba ágyazását;
* elegendő információt kell naplóznia a hibák diagnosztizálásához anélkül,
  hogy érzékeny adatokat fedne fel;
* hiba esetén – ahol ez támogatott – nullától eltérő kilépési állapotot
  kell visszaadnia;
* biztonságosan újrapróbálhatónak kell lennie, vagy egyértelműen
  dokumentálnia kell, ha nem az;
* meg kell akadályoznia vagy biztonságosan kell kezelnie az egymást átfedő
  végrehajtásokat;
* korlátozott lekérdezéseket és erőforrás-korlátokat kell használnia;
* sikeres és sikertelen végrehajtás után is törölnie kell az ideiglenes
  fájlokat; valamint
* dokumentálnia kell minden adatbázis-, modul-, végrehajthatóprogram- és
  nyelvicsomag-függőséget.

Ahol lehetséges, az egyéni háttérfolyamatokat éles telepítésük előtt
reprezentatív adatokat tartalmazó külön projektben kell tesztelni.
