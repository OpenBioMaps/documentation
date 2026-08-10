Szerveradminisztráció
*********************

Ez az oldal egy OpenBioMaps-szerver alacsony szintű konfigurációját ismerteti.
A jelenlegi telepítések általában Docker Compose-szolgáltatások gyűjteményeként
futtatják az OpenBioMaps alkalmazást. Az alkalmazás webszerverét és a PHP
futtatókörnyezetét az ``app`` konténer biztosítja, míg a MapServer és a
PostgreSQL külön konténerekben fut.

Az ezen az oldalon szereplő példák az OpenBioMaps alkalmazás-lemezképén és a
referencia Docker Compose-konfiguráción alapulnak. A lemezképek tartalma és a
szolgáltatások definíciói kiadásonként változhatnak. Mindig hasonlítsa össze
ezt a dokumentációt a telepítés alatt álló verzióhoz mellékelt fájlokkal.

Ne tároljon valódi jelszavakat, klienstitkokat, titkosítási kulcsokat vagy más
hitelesítési adatokat dokumentációban vagy forráskód-tárolóban.

Supervisor
==========

A Supervisor az alacsony szintű konfigurációhoz, frissítésekhez és
projektkarbantartáshoz használható önálló webalkalmazás. Egy
OpenBioMaps-szerver telepítésének részeként települ, és általában a következő
URL-ek egyikén érhető el:

* ``https://YOUR_SERVER/supervisor/``
* ``https://YOUR_SERVER/supervisor.php``

A pontos URL a szerver és a fordított proxy konfigurációjától függ.

A Supervisor két üzemmóddal rendelkezik:

Rendszermód
  Rendszerszintű karbantartást és frissítéseket biztosít, beleértve a
  rendszerkonfiguráció kezelését.

Projektmód
  Projektfrissítést, projektlétrehozást és adatbázis-karbantartást, a
  ``local_vars.php.inc`` kezelését, valamint a projekt ``local`` könyvtárához
  fájlkezelőt biztosít.

A projektmód a projektadminisztrátorok számára a projekt adminisztrációs
felületén keresztül is elérhetővé tehető.

A Supervisor elérését korlátozza a megbízható adminisztrátorokra. Használjon
HTTPS-t és erős, egyedi jelszót, továbbá fontolja meg további hálózati szintű
korlátozások alkalmazását.

A Supervisor jelszavának újbóli létrehozása
-------------------------------------------

A Docker-gazdagépen a Supervisor jelszava a telepítés utáni parancsfájllal
hozható létre újra:

.. code-block:: console

   cd /srv/docker/openbiomaps
   ./obm_post_install.sh update supervisor

A telepítési könyvtár pontos helye eltérhet. A parancsot az OpenBioMaps
telepítési parancsfájljait tartalmazó könyvtárból futtassa, és ellenőrizze,
hogy a kimenetben vannak-e hibák.

A jelszó módosítása után ellenőrizze, hogy a Supervisor elérhető-e, az új
hitelesítési adatot pedig tárolja megfelelő jelszókezelőben.

Rendszerváltozó-fájlok
======================

Az OpenBioMaps az egyes projektek ``local_vars.php.inc`` fájljai mellett
rendszerszintű változófájlokat is használ.

Az alkalmazás-lemezkép jelenleg a következő helyen tartalmaz egy alapfájlt:

``/var/www/html/biomaps/root-site/server_vars.php.inc``

A Docker-lemezkép a ``/etc/openbiomaps`` könyvtárat kötetként is deklarálja.
Az adminisztrátor által kezelt rendszerkonfiguráció általában itt található,
például:

``/etc/openbiomaps/system_vars.php.inc``

A ``server_vars.php.inc`` és a ``system_vars.php.inc`` közötti pontos
kapcsolat és betöltési sorrend OpenBioMaps-kiadásonként eltérhet. Ne
feltételezze, hogy a két fájl felcserélhető. Használja a Supervisort és a
telepített kiadáshoz mellékelt sablonokat, frissítés után pedig ellenőrizze az
érvényes konfigurációt.

Mivel a referenciaként szolgáló Compose-konfigurációban a
``/etc/openbiomaps`` könyvtár az ``etc_openbiomaps`` Docker-kötetből van
csatolva, az itt végzett módosítások az ``app`` konténer cseréjekor is
megmaradnak.

A következő szakaszok a korábban a ``system_vars.php.inc`` példájában
bemutatott beállításokat ismertetik. Az értékek példák, és azokat a tényleges
telepítésnek megfelelően felül kell vizsgálni.

Hálózati és URL-beállítások
---------------------------

.. list-table::
   :header-rows: 1
   :widths: 24 28 48

   * - Változó
     - Példaérték
     - Leírás
   * - ``USE_NON_STANDARD_HTTP_PORTS``
     - ``false``
     - Engedélyezi egy olyan helyi telepítés támogatását, amely nem proxy
       mögött található, és nem szabványos HTTP-portokat használ. Nem
       kötelező, és a példában le van tiltva.
   * - ``OB_DOMAIN``
     - ``localhost/biomaps``
     - Az OpenBioMaps által használt nyilvános szervercím és telepítési
       útvonal. Cserélje le a tényleges állomásnévre és útvonalra. Az értéknek
       összhangban kell lennie a fordított proxy és a TLS konfigurációjával.
   * - ``POSTGRES_PORT``
     - ``5432``
     - Az OpenBioMaps által használt PostgreSQL-szolgáltatás portja.
   * - ``GISDB_HOST``
     - ``localhost``
     - Az újonnan létrehozott projektek konfigurációjába beillesztett
       adatbázis-állomás. Docker-telepítésben ez általában a ``localhost``
       helyett egy Docker-hálózati név vagy álnév, például ``gisdata``.
   * - ``MAPSERVER_HOST``
     - ``mapserver``
     - Az újonnan létrehozott projektek konfigurációjába beillesztett
       MapServer-szolgáltatás állomása. A referencia Compose-környezetben a
       ``mapserver`` a Docker Compose-szolgáltatás neve.

Egy konténeren belül a ``localhost`` magára a konténerre hivatkozik. Nem
hivatkozik másik Compose-szolgáltatásra. Az ``app`` konténernek például
általában ``mapserver`` néven kell elérnie a MapServer szolgáltatást, az
adatbázist pedig az adatbázis-szolgáltatás egyik hálózati nevén vagy álnevén
keresztül.

A referencia-adatbázisszolgáltatás neve ``biomaps_db``, álnevei pedig
``biomaps`` és ``gisdata``. A meglévő OpenBioMaps-sablonok ezen álnevek
egyikét várhatják. A ``GISDB_HOST`` módosítása előtt vizsgálja meg egy működő
projekt konfigurációját, és ellenőrizze, hogy a telepített kiadás melyik nevet
várja.

Könyvtárbeállítások
-------------------

.. list-table::
   :header-rows: 1
   :widths: 24 31 45

   * - Változó
     - Példaérték
     - Leírás
   * - ``OB_SYSDIR``
     - ``/var/lib/openbiomaps/``
     - Az OpenBioMaps állandó rendszeradatainak alapkönyvtára. Ez a
       dokumentált alapértelmezés, és a példában nem kötelező.
   * - ``OB_TMP``
     - ``/var/lib/openbiomaps/tmp/``
     - Az OpenBioMaps ideiglenes fájljaihoz használt könyvtár. A referencia
       Compose-konfigurációban az állandó ``var_lib`` köteten belül található.
   * - ``OB_ROOT``
     - ``/var/www/html/biomaps/root-site``
     - Az alkalmazás dokumentumgyökér-könyvtára. A példa nem tartalmaz záró
       perjelet.
   * - ``OB_ROOT_SITE``
     - ``/var/www/html/biomaps/root-site/``
     - Az alkalmazás root-site könyvtára. Az alkalmazáskód egyes részei záró
       perjellel várják ezt az alakot.
   * - ``OB_RESOURCES``
     - ``/var/www/html/biomaps/resources/``
     - A megosztott OpenBioMaps-erőforrásokat tartalmazó könyvtár.

Ne módosítsa az útvonalakat a Docker-lemezkép, az Apache
dokumentumgyökere, a kötetcsatolások, a projektútvonalak és az ezekre
hivatkozó összes parancsfájl ellenőrzése nélkül.

Kapcsolódás a rendszeradatbázishoz
---------------------------------

Ezek a változók az OpenBioMaps rendszeradatbázisához való kapcsolódást
határozzák meg. Elkülönülnek a szervertelepítési útmutatóban dokumentált,
projektspecifikus ``gisdb_*`` beállításoktól.

.. list-table::
   :header-rows: 1
   :widths: 24 26 50

   * - Változó
     - Példaérték
     - Leírás
   * - ``biomapsdb_user``
     - Titkos, telepítésspecifikus érték
     - Az OpenBioMaps rendszeradatbázisának eléréséhez használt
       PostgreSQL-felhasználó.
   * - ``biomapsdb_pass``
     - Titkos, telepítésspecifikus érték
     - A rendszeradatbázis felhasználójának jelszava. Használjon erős,
       véletlenszerű értéket, és ne véglegesítse kódtárolóba.
   * - ``biomapsdb_name``
     - Telepítésspecifikus érték
     - Az OpenBioMaps rendszeradatbázisának neve.
   * - ``biomapsdb_host``
     - ``localhost``
     - A rendszeradatbázist futtató állomás. A referencia
       Docker-környezetben a ``localhost`` helyett használja a megfelelő
       adatbázis-szolgáltatás nevét vagy álnevét, kivéve, ha a PostgreSQL
       valóban az ``app`` konténerben fut.
   * - ``POSTGIS_V``
     - ``2.5``
     - Korábbi PostGIS-verziójelölő. Ezt az értéket általában nem szükséges
       beállítani, és lehet, hogy nem a jelenleg telepített verziót jelöli.

A referencia Compose-fájl az ``openbiomaps/database:pg17-3.5`` lemezképet
használja. A lemezkép neve a korábbi ``POSTGIS_V`` példánál újabb
PostgreSQL/PostGIS-kombinációra utal. Ne használja a ``POSTGIS_V`` értékét a
szerver tényleges verziójának meghatározásához. Ha verzióinformációra van
szükség, kérdezze le az adatbázis-szervert.

Levélkézbesítés
---------------

.. list-table::
   :header-rows: 1
   :widths: 24 24 52

   * - Változó
     - Példaérték
     - Leírás
   * - ``SENDMAIL``
     - ``smtp``
     - Az alapértelmezett levélkézbesítési mód. A dokumentált értékek:
       ``sendmail`` és ``smtp``. A projekt felülírhatja ezt a beállítást a
       ``local_vars.php.inc`` fájlban.

Ha az SMTP van kiválasztva, állítsa be a szükséges SMTP-állomást,
hitelesítést, feladót, portot és átviteli biztonsági beállításokat a megfelelő
rendszer- vagy projektszinten. Ne tároljon SMTP-hitelesítési adatokat
nyilvános konfigurációs fájlokban.

Gyorsítótár
-----------

.. list-table::
   :header-rows: 1
   :widths: 24 24 52

   * - Változó
     - Példaérték
     - Leírás
   * - ``CACHE``
     - ``memcache``
     - Kiválasztja az OpenBioMaps által használt gyorsítótár-megvalósítást.

A referencia alkalmazás-lemezkép a következő környezeti alapértelmezéseket is
meghatározza:

.. list-table::
   :header-rows: 1
   :widths: 24 24 52

   * - Környezeti változó
     - Alapértelmezett érték
     - Leírás
   * - ``CACHE_HOST``
     - ``memcached``
     - A Memcached-szolgáltatás állomásneve. Megegyezik a referencia
       Compose-fájlban szereplő szolgáltatásnévvel.
   * - ``CACHE_PORT``
     - ``11211``
     - A Memcached által a Docker-hálózaton belül használt port.

A ``memcached`` szolgáltatás a privát ``obm_back`` hálózathoz kapcsolódik, és
nem szükséges portot közzétennie a Docker-gazdagépen.

Választható R Shiny-szolgáltatások
----------------------------------

.. list-table::
   :header-rows: 1
   :widths: 32 22 46

   * - Változó
     - Példaérték
     - Leírás
   * - ``RSERVER_PORT_someproject``
     - ``7982``
     - Projektspecifikus R Shiny Server-port. Cserélje le a ``someproject``
       részt a megfelelő projektazonosítóra. Csak azokhoz a projektekhez
       állítsa be, amelyek még használják az R Shiny-integrációt.

Az R Shiny támogatása korábbi vagy választható integráció. A beállítása előtt
ellenőrizze, hogy a telepített OpenBioMaps-kiadás támogatja-e.

Támogatott nyelvek
------------------

.. list-table::
   :header-rows: 1
   :widths: 24 25 51

   * - Változó
     - Példaérték
     - Leírás
   * - ``LANGUAGES``
     - ``en, hu, ro``
     - A szerver által támogatott nyelvek vesszővel elválasztott listája. A
       megfelelő nyelvi fájlokat telepíteni kell.

Ez a rendszerszintű érték elkülönül a projektszintű nyelvválasztástól. A
projekt nyelvi beállításainak a szerveren elérhető nyelveket kell használniuk.

Automatikus hibajelentések
--------------------------

.. list-table::
   :header-rows: 1
   :widths: 28 30 42

   * - Változó
     - Példaérték
     - Leírás
   * - ``AUTO_BUGREPORT_ADDRESS``
     - A kódtároló karbantartói által biztosított bejövő hibajegycím
     - Egy bejövő címen keresztül engedélyezi a hibajegykezelővel való
       integrációt. Kérje a megfelelő hibajegykulcsot vagy címet az
       OpenBioMaps kódtárolójának karbantartóitól.

A teljes bejövő címet kezelje titkos adatként, mert bárki, aki megszerzi,
hibajegyeket hozhat létre vagy kéretlen tartalmat küldhet be. Ellenőrizze a
naplókat és a kimenő jelentéseket annak biztosítására, hogy ne tartalmazzanak
érzékeny projekt- vagy felhasználói adatokat.

Webes hitelesítési titok
------------------------

.. list-table::
   :header-rows: 1
   :widths: 28 28 44

   * - Változó
     - Példaérték
     - Leírás
   * - ``WEB_CLIENT_SECRET``
     - Titkos, telepítésspecifikus érték
     - A webes hitelesítés által használt kötelező titkos érték. Ugyanezt az
       értéket kell tárolni a rendszeradatbázis ``web`` OAuth-klienséhez.

A konfigurációs értéknek és a hozzá tartozó adatbázisértéknek szinkronban
kell maradnia. Hozzon létre erős, véletlenszerű titkos értéket, korlátozza a
hozzáférést, és gondosan tervezze meg a titok cseréjét, mert csak az egyik
példány módosítása megszakítja a webes hitelesítést.

A rendszerváltozók módosításainak alkalmazása
---------------------------------------------

Egy rendszerbeállítás módosítása után:

#. Ellenőrizze a módosított konfiguráció szintaxisát.
#. Szükség esetén indítsa újra vagy hozza létre újra az érintett szolgáltatást.
#. Vizsgálja meg a szolgáltatás naplóit.
#. Tesztelje a Supervisort és egy reprezentatív projektet.
#. Tesztelje a hitelesítést, az adatbázis-hozzáférést, a térképeket és a
   háttérfeladatokat, ha a módosított beállítás hatással van ezekre az
   összetevőkre.

Például:

.. code-block:: console

   docker compose config
   docker compose restart app
   docker compose logs --tail=200 app

Régebbi rendszereken a pontos Docker Compose-parancs ``docker-compose`` is
lehet.

Az alkalmazás-lemezkép úgy állítja be a PHP OPcache-t, hogy az időbélyeg
ellenőrzése le legyen tiltva. Emiatt előfordulhat, hogy egy futó folyamat nem
észleli azonnal a módosított PHP-fájlokat. A PHP-konfiguráció vagy az
alkalmazás módosítása után az ``app`` konténer újraindításával elkerülhető az
elavult gyorsítótárazott kód kiszolgálása.

Docker-szolgáltatásarchitektúra
===============================

A referencia Compose-konfiguráció egy ``obm_back`` nevű privát bridge
hálózatot hoz létre. A hálózat szolgáltatásai a Compose-szolgáltatásneveken és
a beállított hálózati álneveken keresztül kommunikálhatnak.

Az alapvető szolgáltatások:

.. list-table::
   :header-rows: 1
   :widths: 21 29 50

   * - Szolgáltatás
     - Lemezkép
     - Rendeltetés
   * - ``app``
     - ``registry.gitlab.com/openbiomaps/web-app:latest``
     - Az Apache HTTP Server, a PHP, az OpenBioMaps webalkalmazás és a
       Supervisor futtatása.
   * - ``mapserver``
     - ``openbiomaps/mapserver``
     - A projekttérképek megjelenítéséhez használt MapServer-szolgáltatás
       futtatása.
   * - ``biomaps_db``
     - ``openbiomaps/database:pg17-3.5``
     - A rendszer- és az alapértelmezett topológiában a projektadatbázisokhoz
       használt PostgreSQL és PostGIS futtatása.
   * - ``memcached``
     - ``memcached:latest``
     - A megosztott alkalmazás-gyorsítótár biztosítása.
   * - ``obm-server-api``
     - ``registry.gitlab.com/openbiomaps/api/obm-server-api:latest``
     - A különálló OpenBioMaps szerver API biztosítása.
   * - ``adminer``
     - ``adminer``
     - Böngészőalapú adatbázis-adminisztrációs felület biztosítása.

A szolgáltatások pontos listája a telepített Compose-fájltól függ. A
választható szolgáltatások letilthatók, eltávolíthatók vagy lecserélhetők.

Éles telepítések esetén fontolja meg, hogy a ``latest`` használata helyett
tesztelt kiadási címkékhez vagy módosíthatatlan kivonatokhoz rögzíti a
lemezképeket. Ez kiszámíthatóvá teszi a frissítéseket, és egyszerűsíti a
visszaállást.

Alkalmazásszolgáltatás: Apache és PHP
====================================

Az ``app`` lemezkép a hivatalos ``php:8.4-apache-trixie`` lemezképen alapul.
Az Apache és a PHP ezért ugyanabban a konténerben fut.

Apache-konfiguráció
-------------------

A lemezkép a következő Apache-konfigurációt végzi el:

* engedélyezi a ``headers``, ``proxy``, ``proxy_http``, ``rewrite`` és ``ssl``
  modulokat;
* az alapértelmezett dokumentumgyökeret a
  ``/var/www/html/biomaps/root-site`` könyvtárra módosítja; valamint
* az OpenBioMaps Apache-konfigurációját
  ``/etc/apache2/conf-enabled/openbiomaps.conf`` néven telepíti.

A referencia Compose-fájl a konténer 80-as és 443-as portját a gazdagép
azonos portjain teszi közzé:

.. code-block:: text

   80:80
   443:443

Ha egy másik fordított proxy végzi a TLS lezárását, szükség lehet a közzétett
portok és az Apache virtuálisgép-konfigurációjának módosítására. Győződjön
meg arról, hogy a nyilvános séma, állomás, útvonal és továbbított fejlécek
összhangban vannak az ``OB_DOMAIN`` értékével és a projekt URL-jeivel.

Az egyéni Apache-konfigurációt karbantartott lemezképpel, bind mount
csatolással vagy más reprodukálható telepítési mechanizmussal kell biztosítani.
Ne szerkesszen közvetlenül egy futó konténert, mert ezek a módosítások
elvesznek a konténer cseréjekor.

A referencia Compose-fájl megjegyzésbe tett példákat tartalmaz a
TLS-tanúsítványok és egyéni SSL virtuális gép csatolásához. A
tanúsítványokat a konténeren kívül hozza létre és újítsa meg, kivéve, ha a
telepítés szándékosan más tanúsítványkezelési megoldást használ.

Az Apache-konfiguráció módosítása után ellenőrizze azt a konténeren belül:

.. code-block:: console

   docker compose exec app apache2ctl configtest
   docker compose restart app
   docker compose logs --tail=200 app

PHP-konfiguráció
----------------

Az alkalmazás-lemezkép telepíti az OpenBioMaps által igényelt
PHP-bővítményeket, beleértve a PostgreSQL, PDO PostgreSQL, nemzetköziesítési,
ZIP, GD, Exif, Memcached, YAML és mcrypt támogatást.

A referencia Compose-fájl bemutatja, hogyan lehet felülírni a
PHP-beállításokat egyes INI-fájlok ``/usr/local/etc/php/conf.d`` könyvtárba
csatolásával:

.. code-block:: text

   ./php-date.timezone.ini -> /usr/local/etc/php/conf.d/php-date.timezone.ini
   ./php-upload.ini        -> /usr/local/etc/php/conf.d/php-upload.ini

Ez a megközelítés többek között a következő beállításokhoz használható:

* ``date.timezone``;
* ``upload_max_filesize``;
* ``post_max_size``;
* ``memory_limit``;
* ``max_execution_time``; valamint
* munkamenettel kapcsolatos beállítások.

A feltöltések beállításakor tartsa összhangban az összes vonatkozó korlátot.
A ``post_max_size`` értékének például a teljes kéréshez, nem csak a feltöltött
fájlhoz kell elegendőnek lennie. Egy fordított proxy további
kérésméret-korlátot szabhat meg.

Ellenőrizze az érvényes PHP-konfigurációt a konténeren belül, és ne
feltételezze, hogy a csatolt fájl betöltődött:

.. code-block:: console

   docker compose exec app php --ini
   docker compose exec app php -i
   docker compose logs --tail=200 app

A csatolt INI-fájlok módosítása után indítsa újra az ``app`` szolgáltatást.

Alkalmazásnaplók
----------------

A lemezkép létrehozza a ``/var/log/openbiomaps.log`` fájlt, és a
webszerver-felhasználóhoz rendeli. A referencia Compose-fájl bind mount
csatolással a Docker-gazdagépről csatolja ezt a fájlt:

.. code-block:: text

   ./openbiomaps.log -> /var/log/openbiomaps.log

A gazdagépen található fájlnak léteznie kell, és olyan jogosultságokkal kell
rendelkeznie, amelyek lehetővé teszik, hogy a konténer ``www-data``
felhasználója írja. Vizsgálja meg a konténer szabványos kimenetét és az
Apache-naplókat is:

.. code-block:: console

   docker compose logs --tail=200 app
   docker compose logs -f app

Állítsa be a gazdagépen tárolt naplófájlok rotációját, nehogy azok elfoglalják
az összes rendelkezésre álló lemezterületet. Kerülje a jelszavak, tokenek,
teljes adatbázis-kapcsolati karakterláncok vagy érzékeny megfigyelési adatok
naplózását.

MapServer-szolgáltatás
======================

A MapServer a különálló ``mapserver`` szolgáltatásban fut. Az ``app`` konténer
általában a ``mapserver`` állomásnéven éri el a privát Docker-hálózaton.

A referencia Compose-konfiguráció a következő erőforrásokat osztja meg a
MapServer szolgáltatással:

.. list-table::
   :header-rows: 1
   :widths: 29 31 40

   * - Forrás
     - Konténerbeli útvonal
     - Rendeltetés
   * - ``mapserver_log`` kötet
     - ``/tmp/mapserver``
     - Megosztott MapServer-napló és ideiglenes adatok.
   * - ``var_lib`` kötet
     - ``/var/lib/openbiomaps``
     - Megosztott OpenBioMaps-rendszeradatok.
   * - ``projects`` kötet
     - ``/var/www/html/biomaps/root-site/projects``
     - Projektfájlok és projektspecifikus mapfile-ok.
   * - ``./openbiomaps.conf``
     - ``/etc/apache2/conf-enabled/openbiomaps.conf``
     - A MapServer-konténer Apache-konfigurációja.
   * - ``./00_msencrypt-wrapper.conf``
     - ``/etc/apache2/conf-enabled/00_msencrypt-wrapper.conf``
     - A MapServer titkosítási burkolójának Apache-konfigurációja.
   * - ``./msencrypt-wrapper.pl``
     - ``/usr/local/bin/msencrypt-wrapper.pl``
     - A MapServer-szolgáltatás által használt burkoló.

A gazdagépről csatolt MapServer Apache-konfiguráció vagy burkoló módosításait
ellenőrizni kell, majd újra kell indítani a ``mapserver`` szolgáltatást:

.. code-block:: console

   docker compose exec mapserver apache2ctl configtest
   docker compose restart mapserver
   docker compose logs --tail=200 mapserver

A projektek mapfile-jait általában az OpenBioMaps projektadminisztrációján és
a Supervisoron keresztül kezelik. Mivel a ``projects`` kötet megosztott, az
alkalmazás és a MapServer egyaránt hozzáférhet ugyanazokhoz a
projektfájlokhoz.

A MapServer nem tesz közzé gazdagépportot a referencia Compose-fájlban. Ez
szándékos: a kéréseknek általában az OpenBioMaps alkalmazáson vagy annak
beállított proxyján keresztül kell haladniuk ahelyett, hogy a MapServer
közvetlenül elérhető lenne az internetről.

A MapCache további konfigurációt igényel, és pusztán egy MapCache URL
meghatározásával nem válik elérhetővé. A MapCache bevezetésekor dokumentálja
a tárolását, a gyorsítótár érvénytelenítését, az erőforrás-korlátokat és a
hálózati elérhetőséget.

PostgreSQL- és PostGIS-szolgáltatás
==================================

A ``biomaps_db`` szolgáltatás az ``openbiomaps/database:pg17-3.5`` lemezkép
használatával futtatja a PostgreSQL és PostGIS rendszereket. Adatkönyvtárát
az állandó ``biomaps_data`` kötet tárolja:

``/var/lib/postgresql/data``

A szolgáltatás a következő nevekkel rendelkezik a privát hálózaton:

* Compose-szolgáltatásnév: ``biomaps_db``;
* hálózati álnév: ``biomaps``; valamint
* hálózati álnév: ``gisdata``.

A telepített OpenBioMaps-konfiguráció által elvárt nevet használja. Az
``app`` vagy ``mapserver`` konténerből ne használja a ``localhost`` nevet erre
az adatbázis-szolgáltatásra való hivatkozáshoz.

A referencia-konfiguráció nem teszi közzé az adatbázis portját a
Docker-gazdagépen. Ez csökkenti a kitettséget, és elegendő az ``obm_back``
hálózathoz kapcsolódó alkalmazásszolgáltatások számára. Csak akkor tegye
közzé a PostgreSQL szolgáltatást, ha külső hozzáférés szükséges, és ebben az
esetben korlátozza a hozzáférést tűzfalszabályokkal, PostgreSQL
hozzáférés-vezérléssel, valamint adott esetben TLS használatával.

Adatbázis-hitelesítési adatok
-----------------------------

A referencia Compose-fájl nem állít be közvetlenül rögzített
``POSTGRES_PASSWORD`` értéket. A megjegyzései szerint az adatbázis-lemezkép
véletlenszerű jelszót hoz létre, kivéve, ha kifejezetten megadják a
hitelesítési adatokat.

A hitelesítési adatok kezeléséhez használja a telepítési folyamatot és a
Supervisort. Az adatbázis-szolgáltatás cseréje vagy újbóli létrehozása előtt
ellenőrizze, hol tárolódnak a létrehozott hitelesítési adatok, és győződjön
meg arról, hogy rendelkezésre áll tesztelt biztonsági mentés.

Ne módosítsa egy adatbázis jelszavát anélkül, hogy frissítené az azt használó
összes rendszer- és projektkonfigurációt.

Adatbázis-tárolás és biztonsági mentés
-------------------------------------

A ``biomaps_data`` kötet állandó adatbázisadatokat tartalmaz. A kötet
másolása a PostgreSQL aktív írási műveletei közben önmagában nem garantál
konzisztens adatbázis-biztonsági mentést. Használjon PostgreSQL-kompatibilis
biztonsági mentési eszközöket vagy a támogatott OpenBioMaps archiválási
eljárást.

Rendszeresen tesztelje a visszaállítást elkülönített környezetben. Egy
biztonsági mentés nem tekinthető ellenőrzöttnek, amíg nem állították
sikeresen vissza.

Az adatbázis-szolgáltatás vizsgálata:

.. code-block:: console

   docker compose ps biomaps_db
   docker compose logs --tail=200 biomaps_db

A szolgáltatás újbóli létrehozásakor ne távolítsa el a ``biomaps_data``
kötetet, kivéve, ha szándékosan törli az adatbázist, és rendelkezésre áll
ellenőrzött helyreállítási terv.

Külön projektadatbázis
----------------------

A referencia Compose-fájl megjegyzésbe tett példát tartalmaz egy különálló
``gisdata`` adatbázis-szolgáltatáshoz. Ha a rendszer- és projektadatbázisok
elkülönülnek:

* módosítsa a Docker hálózati álneveit;
* frissítse a rendszer- és projektadatbázisok állomásbeállításait;
* állítson be külön hitelesítési adatokat;
* frissítse a biztonsági mentési és monitorozási eljárásokat; valamint
* ellenőrizze a hozzáférést az ``app`` és a ``mapserver`` szolgáltatásból is.

Ne tegye közzé az adatbázis portját, kivéve, ha a Docker-hálózaton kívüli
klienseknek csatlakozniuk kell.

Memcached-szolgáltatás
======================

A ``memcached`` szolgáltatás biztosítja az alkalmazás gyorsítótárát. Az
``app`` konténerből a ``memcached:11211`` címen érhető el a privát
Docker-hálózaton keresztül.

A Memcached nem biztosít hitelesítést a referencia-konfigurációban. Ne tegye
közzé a portját. Egyéni Docker-hálózat használata esetén győződjön meg arról,
hogy csak megbízható alkalmazásszolgáltatások érhetik el.

A gyorsítótárazott adatok eldobhatók, és nem kezelhetők állandó tárhelyként.
A Memcached újraindítása vagy cseréje törölheti a gyorsítótárazott
bejegyzéseket anélkül, hogy törölné az alapul szolgáló OpenBioMaps-adatokat.

API-szolgáltatás
================

Az ``obm-server-api`` szolgáltatás különálló OpenBioMaps API-lemezképet
futtat. A szolgáltatás:

* írásvédetten csatolja a telepítés ``.env`` fájlját;
* az Apache indítása előtt futtatja az inicializáló parancsfájlját; valamint
* a referencia-konfigurációban a konténer 80-as portját a gazdagép 9001-es
  portjaként teszi közzé.

Vizsgálja felül a ``.env`` minden értékét, és korlátozza a fájl
jogosultságait a Docker-gazdagépen. A fájl hitelesítési adatokat vagy más
titkos értékeket tartalmazhat.

A ``9001:80`` közzététele minden gazdagépfelületen elérhetővé teszi az API-t,
kivéve, ha a Docker vagy a tűzfal konfigurációja korlátozza azt. Éles
környezetben lehetőleg a beállított HTTPS fordított proxyn keresztül irányítsa
az API-t, vagy korlátozott felülethez kösse.

Az API inicializálási és futásidejű hibáinak vizsgálata:

.. code-block:: console

   docker compose logs --tail=200 obm-server-api

Adatbázis-adminisztrációs szolgáltatás
======================================

A referencia-konfiguráció tartalmazza az Adminer szolgáltatást, és a gazdagép
9882-es portján teszi közzé.

Az adatbázis-adminisztrációs felület biztonsági szempontból érzékeny. Erős
további hozzáférés-vezérlés nélkül ne tegye elérhetővé a nyilvános
interneten. Részesítse előnyben a következő megközelítések egyikét:

* csak karbantartás végzésekor engedélyezze;
* kösse a loopback interfészhez;
* korlátozza tűzfallal vagy privát hálózattal; vagy
* biztonságos adminisztrációs alagúton keresztül érje el.

A közzétett port localhosthoz kötéséhez például a
``127.0.0.1:9882:8080`` értékkel egyenértékű Compose-portleképezés
használható.

Távolítsa el vagy tiltsa le a szolgáltatást, amikor nincs rá szükség.

Állandó kötetek
===============

A referencia Compose-konfiguráció a következő nevesített köteteket határozza
meg:

.. list-table::
   :header-rows: 1
   :widths: 27 73

   * - Kötet
     - Rendeltetés
   * - ``root-private``
     - Privát alkalmazásfájlok a
       ``/var/www/html/biomaps/root-site/private`` könyvtárban.
   * - ``projects``
     - Az alkalmazás és a MapServer által megosztott projektkönyvtárak.
   * - ``var_lib``
     - Állandó OpenBioMaps-rendszeradatok a
       ``/var/lib/openbiomaps`` könyvtárban.
   * - ``mapserver_log``
     - Megosztott MapServer-napló és ideiglenes fájlok a ``/tmp/mapserver``
       könyvtárban.
   * - ``etc_openbiomaps``
     - Az adminisztrátor által kezelt OpenBioMaps-konfiguráció az
       ``/etc/openbiomaps`` könyvtárban.
   * - ``biomaps_data``
     - PostgreSQL-adatok a ``/var/lib/postgresql/data`` könyvtárban.

A nevesített kötetek túlélik a konténerek szokásos cseréjét, de kifejezett
művelettel továbbra is törölhetők. A biztonsági mentési és
katasztrófa-helyreállítási tervben szerepeljen minden olyan kötet, amely
szükséges adatokat vagy konfigurációt tartalmaz.

A Compose-fájl azt is bemutatja, hogyan cserélhető le egy nevesített kötet
bind mount csatolásra. A bind mount csatolások megkönnyítik a gazdagépbeli
útvonalak vizsgálatát, de helyes abszolút útvonalakat, tulajdonosi
beállításokat, jogosultságokat és biztonsági mentési eljárásokat igényelnek.

Konfigurációs munkafolyamat
===========================

A beállítás típusának megfelelő konfigurációs mechanizmust válassza:

.. list-table::
   :header-rows: 1
   :widths: 34 66

   * - Konfiguráció típusa
     - Ajánlott mechanizmus
   * - OpenBioMaps rendszerváltozók
     - A Supervisor és az állandó ``/etc/openbiomaps`` kötet.
   * - Projektváltozók
     - Projektadminisztráció vagy a Supervisor projektmódja.
   * - Apache-beállítások az ``app`` szolgáltatásban
     - Karbantartott egyéni lemezkép vagy kifejezett konfigurációcsatolás.
   * - PHP-beállítások
     - Az ``/usr/local/etc/php/conf.d`` könyvtárba csatolt INI-fájlok.
   * - MapServer Apache-beállítások
     - A ``mapserver`` konténerbe csatolt gazdagépfájlok.
   * - Projekt-mapfile-ok
     - Projektadminisztráció vagy Supervisor, a megosztott ``projects``
       kötetben tárolva.
   * - Adatbázis-beállítások
     - Compose-környezet, OpenBioMaps-konfiguráció és az adatbázis-lemezkép
       támogatott konfigurációs mechanizmusa.
   * - Titkos értékek
     - Korlátozott hozzáférésű környezeti fájlok vagy külön
       titokkezelési mechanizmus.

Ne végezzen fontos módosításokat kizárólag egy futó konténeren belül. Az ilyen
módosítások nem reprodukálhatók, és a konténer cseréjekor eltűnnek.

A Compose-fájl módosítása után:

.. code-block:: console

   docker compose config
   docker compose pull
   docker compose up -d
   docker compose ps
   docker compose logs --tail=200

Frissítés előtt tekintse át a kiadási megjegyzéseket, és készítsen
ellenőrzött biztonsági mentést. Éles rendszeren ne töltse le és telepítse
vakon a ``latest`` lemezképeket.

Ajánlott ütemezett feladatok
===========================

Az ütemezett feladatok a Docker-gazdagépről cron vagy ezzel egyenértékű
systemd-időzítő használatával futtathatók. Használjon abszolút útvonalakat,
rögzítse a naplókat, és gondoskodjon arról, hogy az egymást átfedő futások ne
tehessenek kárt az adatokban.

Az alábbi példákat hozzá kell igazítani a telepítéshez. Ütemezés előtt minden
parancsot teszteljen kézzel.

Docker-frissítések
------------------

Az OpenBioMaps parancsfájlokat tartalmazó kódtárolója automatikus frissítési
parancsfájlt tartalmaz:

https://github.com/OpenBioMaps/scripts/tree/master/docker-auto-update

Példa cron-bejegyzés:

.. code-block:: cron

   # m h  dom mon dow   command
   0 4,16 * * * /srv/docker/openbiomaps/auto_update.sh > /srv/docker/openbiomaps/system_update_job.log 2>&1

Az automatikus éles frissítések üzemeltetési kockázattal járnak.
Engedélyezésük előtt határozza meg:

* hogyan készülnek és hogyan ellenőrzik a biztonsági mentéseket;
* hogyan kezelik az adatbázis-migrációkat;
* hogyan észlelik a sikertelen frissítéseket;
* hogyan rögzítik a lemezképek verzióit;
* hogyan történik a visszaállás; valamint
* ki kap értesítést a hibákról.

Archiválási feladatok
---------------------

Az archiválási parancsfájl itt érhető el:

https://github.com/OpenBioMaps/scripts/blob/master/obm_archive.sh

A parancsfájl a ``.archive_list.txt`` és az ``obm_archive_settings.sh``
fájlokat használja. Példaütemezés:

.. code-block:: cron

   # m h  dom mon dow   command
   0 2 * * *  /path_to/obm_archive.sh normal
   15 2 * * * /path_to/obm_archive.sh system
   15 3 1 * * /path_to/obm_archive.sh full
   0 5 * * *  /path_to/obm_archive.sh clean
   # Synchronise archives to a remote server
   0 4 * * *  /path_to/obm_archive.sh sync remote_user@remote-server.example /remote_path_to_archives

Docker-telepítés esetén kövesse az ``obm_archive_settings.sh`` végén
található utasításokat.

Legalább egy biztonsági mentést az OpenBioMaps-gazdagépen kívül tároljon.
Védje a távoli biztonsági mentés hitelesítési adatait, és rendszeresen
tesztelje a visszaállítást.

Háttérfeladat-futtató
---------------------

A háttérfeladatokat használó projektek ``jobs.php`` futtatóját rendszeresen
végre kell hajtani.

Példa:

.. code-block:: cron

   # m h  dom mon dow   command
   */5 * * * * /usr/bin/docker compose -f /srv/docker/openbiomaps/docker-compose.yml exec -u www-data -T app php /var/www/html/biomaps/root-site/projects/PROJECTTABLE/jobs.php

Cserélje le a ``PROJECTTABLE`` értékét a projekt könyvtárára vagy
azonosítójára, és ellenőrizze a telepített kiadás által használt útvonalat.

A cron korlátozott környezettel fut. Használja a Docker abszolút útvonalát,
és szükség esetén kifejezetten adja meg a Compose projektkönyvtárát. A korábbi
parancsot használó rendszereken a végrehajtható fájl ehelyett
``/usr/local/bin/docker-compose`` lehet.

Minden háttérfeldolgozást igénylő projekthez hozzon létre külön bejegyzést.
Figyelje a kilépési állapotot és a naplókat, és akadályozza meg az egyidejű
végrehajtást, ha egy feladat a két futás közötti időnél tovább tarthat.

Üzemeltetési ellenőrzések
========================

Telepítés vagy konfigurációmódosítás után ellenőrizze a szolgáltatások
állapotát:

.. code-block:: console

   docker compose config
   docker compose ps
   docker compose logs --tail=200 app
   docker compose logs --tail=200 mapserver
   docker compose logs --tail=200 biomaps_db
   docker compose logs --tail=200 memcached

Ezután ellenőrizze az alkalmazásban a következőket:

#. Működik a Supervisorba való bejelentkezés.
#. Egy nyilvános projektoldal betöltődik HTTPS-en keresztül.
#. Egy hitelesített felhasználó be- és ki tud jelentkezni.
#. Az alkalmazás képes olvasni és írni az engedélyezett adatbázisrekordokat.
#. A nyilvános és privát térképek megfelelően jelennek meg.
#. A fájlfeltöltések betartják a beállított korlátokat.
#. A levélkézbesítés működik, ha be van állítva.
#. A háttérfeladatok feldolgozása megtörténik.
#. A biztonsági mentések befejeződnek és visszaállíthatók.
#. Az adminisztrációs szolgáltatások nem érhetők el a tervezettnél szélesebb
   körben.

Minden éles telepítéshez rögzítse a lemezképek verzióit, a
konfigurációmódosításokat, a teszteredményeket és a visszaállási eljárást.
