:author: Miklós Bán
:date: 2026-08-08


Első lépések
************

Válassza ki, hogyan szeretné használni az OpenBioMaps rendszert
================================================================
OpenBioMaps-projekt létrehozásához hozzáférésre van szüksége egy
OpenBioMaps-szerverhez. Ez lehet saját szerver, bérelt szerver vagy egy más
által már üzemeltetett, OpenBioMaps-projektek tárolására szolgáló szerver.

Csatlakozás egy meglévő szerverhez
----------------------------------
Új projektet – amelyet esetenként adatbázisnak is neveznek – a legegyszerűbben
egy meglévő OpenBioMaps-szerveren hozhat létre. Ellenőrizze az ismert
szerverek listáját, hogy van-e olyan szerver, amelyhez hozzáférhet. Léteznek
olyan nyilvános szerverek, amelyek számos különböző adatbázist tárolnak.

Saját szerver beállítása
------------------------
Ha nagyobb kapacitásra van szüksége, vagy a teljes szerverhez való
hozzáférést ellenőrizni szeretné, telepítheti saját OpenBioMaps-szerverét.

:doc:`Az OpenBioMaps-szerver telepítése <../server_install>`

Docker-alapú telepítéshez lásd:

:doc:`Docker-telepítés <../docker>`


OpenBioMaps-projekt létrehozása
===============================
Egy OpenBioMaps-szerver több adatbázisprojektet is tárolhat. Projekt
létrehozása előtt hozzáféréssel kell rendelkeznie a szerveren található
valamelyik meglévő projekthez. Miután megkapta a hozzáférést, létrehozhatja és
az adatgyűjtési követelményeinek megfelelően konfigurálhatja saját projektjét.

A szükséges lépéseket az alábbi útmutatók ismertetik:
https://openbiomaps.org/documents/en/tutorials.html#new-project és
https://openbiomaps.org/documents/en/new_project.html

A megfigyelési adatmodell megismerése
=====================================
Az adatbázis és az adatgyűjtési űrlapok megtervezése előtt érdemes
megismerni, hogyan ábrázolja az OpenBioMaps a biodiverzitási
megfigyeléseket.

:doc:`Megfigyelési események és alkalmi megfigyelések <../observation_events>`


Az adatok beállítása
====================
A projekt létrehozása után meg kell határoznia az adatok szerkezetét és
gyűjtésük módját.

Az OpenBioMaps lehetővé teszi projektspecifikus adatbázistáblák és mezők
létrehozását és kezelését. Az adatbázis szerkezetének tükröznie kell a
rögzíteni kívánt információkat és a különböző adattípusok közötti
kapcsolatokat.

Az adatbázis szerkezetének meghatározása
----------------------------------------

A projekt táblái és azok oszlopai az adminisztrációs felületen kezelhetők.
Az ott regisztrált táblák és mezők elérhetővé válnak az OpenBioMaps
felületein, és lekérdezésekhez, valamint adatgyűjtéshez használhatók.

Ajánlott leírást megadni a táblákhoz és a mezőkhöz. Ezek a leírások a
projekt metaadatainak részét képezik, és segítenek a felhasználóknak
megérteni az adatok jelentését és tervezett felhasználását.

:doc:`Adminisztrációs beállítások <../admin_settings>`

Adatgyűjtési űrlapok létrehozása
--------------------------------

Az adatbázis szerkezetének meghatározása után létrehozhatja az adatok
rögzítésére és gyűjtésére szolgáló feltöltési űrlapokat.

A feltöltési űrlap határozza meg, hogy mely mezők érhetők el a felhasználók
számára, mely mezők kötelezők, hogyan adhatók meg az értékek, valamint hogyan
történik az adatgyűjtés. Az űrlapok webes adatrögzítéshez,
fájlfeltöltésekhez és API-n keresztüli hozzáféréshez használhatók.

:doc:`Feltöltési űrlapok kezelése <../upload_forms>`

Az adatbázis szerkezete és az adatgyűjtési űrlapok együttesen határozzák meg
az OpenBioMaps-projekt alapvető adatgyűjtési munkafolyamatát.

Adatkezelés és hozzáférés
=========================

Az adatgyűjtés megkezdése előtt gondolja át, hogyan történik majd az adatok
kezelése, és hogyan szabályozza az adatokhoz való hozzáférést.

* :doc:`Adathozzáférés <../data_access>`
* :doc:`Adatkezelési irányelvek <../data_policy>`


Kapcsolódás a projekthez
========================
Az OpenBioMaps-projektek az adatgyűjtés, az adatkezelés vagy az elemzés
módjától függően többféle felületen és eszközzel érhetők el.

Webes felület
-------------
A webes felület az OpenBioMaps-projektek kezelésének központi eszköze.
Eszközöket biztosít az adatkezeléshez, a felhasználók kezeléséhez, a
konfiguráláshoz és az adminisztrációhoz.

:doc:`Felhasználói felület <../user_interface>`

:doc:`Adminisztrációs felület <../admin_settings>`

Az OpenBioMaps programozható felületeket is biztosít külső
kliensalkalmazások számára.

:doc:`OpenBioMaps API <../api>`


QGIS-integráció
---------------
Az OpenBioMaps QGIS-bővítmény hozzáférést biztosít az OpenBioMaps adataihoz
a QGIS rendszerből.

`OpenBioMaps QGIS-bővítmény <https://plugins.qgis.org/plugins/obm_connect/>`_

R-csomag
--------
Az ``obm`` R-csomag eszközöket biztosít az OpenBioMaps adatainak R-ből
történő eléréséhez és feldolgozásához.

`obm a CRAN-on <https://cran.r-project.org/web/packages/obm/index.html>`_

Egyéb integrációk
-----------------
Appsmith, Nextcloud – más eszközre van szüksége?


Az adatgyűjtés és az adatkezelés megkezdése
===========================================
Az OpenBioMaps-projekt most már készen áll az adatgyűjtésre.

A munkafolyamattól függően az adatok rögzíthetők a webes felületen,
feltölthetők fájlokból, gyűjthetők mobilalkalmazásokkal, vagy továbbíthatók
az OpenBioMaps API-n keresztül.

Miután az adatok bekerültek a rendszerbe, a projekt adatkezelési
munkafolyamatának és szabályainak megfelelően validálhatók, kezelhetők,
lekérdezhetők, megjeleníthetők, elemezhetők és megoszthatók.

Az egyes adatgyűjtési munkafolyamatokról további információt az alábbi
oldalon talál:
:doc:`OpenBioMaps-adatgyűjtési példák <../data_collection_examples>`.
