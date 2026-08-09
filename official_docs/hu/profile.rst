.. _profile:

Profiloldal
***********

Felhasználói adatok
-------------------

Beállítások
-----------
    Látható e-mail-cím a projekttagok számára:
    E-mailek fogadása a projekttől:
    Profil törlése


ORCID-profil
------------
   ORCID-profilazonosító hozzáadása, ORCID-profiladatok betöltése, ha az
   azonosítót helyesen adták meg.


Felhasználói információk
------------------------
állapot: normál vagy kiemelt

értékelés: 0 és 1 közötti érték; ez az érték az adatértékelésekből és a
ránk vonatkozó felhasználói értékelésekből származik.

Más adatbázisok
---------------
Az Ön által kezelt összes adatbázis listája.


Tevékenység
-----------
Ez a rész az Ön által végzett feltöltések és feltöltött adatok számát
mutatja. A módosított rekordok számát is megjeleníti.

Fajstatisztika: Az Ön feltöltéseiben szereplő fajok listája és e lista
értékelése.


Megszakított importálások
-------------------------
Új adatok webes űrlapokkal vagy fájlfeltöltéssel történő feltöltésekor
lehetőség van az előkészített adatok aktuális állapotának mentésére.

A feltöltési folyamat mentésekor az adatok és a beállítások az
OpenBioMaps-szerveren tárolódnak. A mentett állapot az azonosítójával
állítható vissza.

Az azonosítók automatikusan jönnek létre. Egy munkamenetben és egy űrlapon
belül csak egy azonosító létezik. Ezért nincs növekményes biztonsági mentés!

A mentett importálásokat a profiloldalon, a „megszakított importálások”
hivatkozásra kattintva követheti nyomon.


Adatok megosztása
-----------------
A lekérdezési eredmények eltárolhatók és megoszthatók. Ebben az esetben
azok, akikkel megosztotta a lekérdezést, nem az adatbázisban tárolt
adatokat látják, hanem azok eltárolt változatát. Az eltárolt eredmény
állapota a létrehozása után nem változik, és teljesen független az
adatbázistól. A megosztási hivatkozás birtokában bárki hozzáférhet a
lekérdezésben tárolt adatokhoz. A megosztási hivatkozás olyan állandó
azonosító, amelyhez DOI-azonosító is rendelhető.


Könyvjelzők
-----------
A lekérdezések könyvjelző-hivatkozások használatával elmenthetők és
megismételhetők. A könyvjelző-hivatkozások nem oszthatók meg; kizárólag
bejelentkezés után, a létrehozójuk számára működnek. A könyvjelzők magát a
lekérdezést, nem pedig annak eredményét tárolják, ezért az adatbázis
tartalmának változásai módosítják a könyvjelző használatával kapott
eredményeket.


API-kulcsok
-----------
Aktív API-kulcsok. Ez egy hitelesítéshez kapcsolódó funkció. Nyomon
követheti a kapcsolatait, és manuálisan bezárhatja őket. Elsősorban
fejlesztők használják.

A következő oldalelemek opcionálisak, és a projektben engedélyezett
meghatározott modulokhoz kapcsolódnak.

Modulspecifikus beállítások
---------------------------
Egyes modulok kezelési felületeket jeleníthetnek meg ezen az oldalon.
Ilyen például a PostgreSQL-felhasználók létrehozására szolgáló modul, a
geometriafeltöltő modul és a letöltésikérelem-modul.

Egyéni geometriák kezelése
..........................
Ez a funkció csak akkor érhető el, ha a ``shared_geoms`` modul
engedélyezett.

Egyéni geometriák tölthetők fel vagy rajzolhatók további műveletekhez.
Ezek a műveletek lehetnek térbeli lekérdezések, vagy geometria
hozzárendelése feltöltött adatokhoz.

Az egyéni geometriák a profiloldal két hivatkozásán keresztül kezelhetők:
megosztott geometriák és saját geometriák.

A saját geometriák hivatkozását követve törölheti, megoszthatja,
átnevezheti geometriáit, valamint módosíthatja megjelenítési beállításaikat.
A következő megjelenítési beállítások érhetők el: megjelenítés a térbeli
kiválasztási listában, valamint megjelenítés az adatfeltöltési felületen a
nevesített térbeli alakzatok hozzárendelési listájában.

A megosztott geometriák hivatkozását követve átnevezheti a geometriákat, és
módosíthatja megjelenítési beállításaikat. A megosztott geometriák nem
törölhetők!

PostgreSQL-felhasználó létrehozása
..................................
Egy évig aktív, a projekt adattábláihoz SQL-kliensprogramokon keresztül
olvasási hozzáférést biztosító felhasználó létrehozása. A QGIS
használatához szükséges!


Vélemények
----------
Más felhasználók véleményei az Ön tevékenységeiről.
