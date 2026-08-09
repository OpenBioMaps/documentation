Kliensek
********

QGIS
====
A QGIS (korábbi nevén Quantum GIS) egy ingyenes, nyílt forráskódú
térinformatikai rendszer (GIS), amely lehetővé teszi a földrajzi adatok
megjelenítését, szerkesztését és elemzését, valamint professzionális
térképek készítését. Az OSGeo projekt részeként fejlesztett szoftver a világ
egyik legnépszerűbb asztali GIS-alkalmazása, amely teljes körű alternatívát
kínál a drága, licencalapú kereskedelmi megoldásokkal (például az ArcGIS
rendszerrel) szemben.

Az OpenBioMaps QGIS-bővítménye hozzáférést biztosít az OpenBioMaps adataihoz
a QGIS rendszerből.

`OpenBioMaps QGIS-bővítmény <https://plugins.qgis.org/plugins/obm_connect/>`_


Az R használata
===============
Az R egy ingyenes programozási nyelv és szoftverkörnyezet, amelyet
statisztikai számításokhoz, adatelemzéshez és grafikus megjelenítéshez
terveztek. Ross Ihaka és Robert Gentleman hozta létre 1993-ban az Aucklandi
Egyetemen, és széles körben használják kutatók, adatbányászok és
statisztikusok.

Az ``obm`` R-csomag eszközöket biztosít az OpenBioMaps adatainak R-ből
történő eléréséhez és feldolgozásához.

`obm a CRAN-on <https://cran.r-project.org/web/packages/obm/index.html>`_

PostgreSQL-kliensek
===================
Platformfüggetlen, teljes körű adatbázis-kezelés.

`A pgAdmin professzionális PostgreSQL-kliens, amely az OpenBioMaps PostgreSQL-adatbázisainak kezelésére használható <https://www.pgadmin.org/>`_

MapServer-kliensek
==================
A MapServer-kliensek olyan szoftveres felületek, asztali GIS-alkalmazások
vagy webes térképi könyvtárak, amelyek a MapServer által szolgáltatott OGC
webszolgáltatásokat (például WMS, WFS és WCS) használják. Gyakori kliensek
az olyan asztali eszközök, mint a QGIS és az ArcGIS, az olyan webes
könyvtárak, mint az OpenLayers és a Leaflet, valamint a MapServer saját
belső képessége, amellyel távoli szerverek klienseként működhet.

Az OpenBioMaps térképeinek megjelenítése elsősorban a MapServer
használatával történik, ezért a MapServer-kliensprogramok csatlakozhatnak az
OpenBioMaps térképszolgáltatásaihoz, ez azonban nagyrészt a projekt
konfigurációjától függ.

OAuth-kliensek
==============
A JWT (JSON Web Token) egy kompakt, önálló tokenformátum, amely az adatok
biztonságos továbbítására szolgál. Az OAuth 2.0 egy hozzáférés-átruházást
biztosító engedélyezési keretrendszer. Nem egymással versengő megoldások: az
OAuth gyakran aláírt JWT-t használ hozzáférési tokenként vagy
azonosítótokenként a felhasználói állítások állapotmentes továbbításához.

Appsmith
========
Az Appsmith egy nyílt forráskódú, low-code fejlesztési platform, amely
rendkívül gyorsan teszi lehetővé belső üzleti eszközök, adminisztrációs
felületek, irányítópultok és egyéni munkafolyamatok létrehozását. Saját
példányt üzemeltetünk!

`OBM Appsmith <https://appsmith.openbiomaps.org/user/login>`_

Nextcloud
=========
A Nextcloud egy nyílt forráskódú, saját üzemeltetésű
tartalom-együttműködési platform, amely teljes ellenőrzést biztosít a saját
adatok felett. Kiváló, adatvédelem-központú alternatívája az olyan népszerű
felhőszolgáltatásoknak, mint a Google Drive, a Microsoft OneDrive és a
Dropbox. A Nextcloud természetesen integrálható az OpenBioMaps rendszerrel.
Ezt szemlélteti a Camptrap adatbázis, amelyben a felhasználók egy
Nextcloud-fiókba töltenek fel képeket; egy, az OpenBioMaps-projektre épülő
alkalmazás elemzi ezeket a képeket, majd visszatölti őket a
Nextcloud-fiókba.

API-kliensek
============
Az OpenBioMaps programozható felületeket is biztosít külső
kliensalkalmazások számára. Az egyik legnagyobb kliensalkalmazásunk az
ECOLLAB által fejlesztett OpenBioMaps terepi mobilalkalmazás.

:doc:`OpenBioMaps API <../api>`
