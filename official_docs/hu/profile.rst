Profil lap
**********

Felhasználói adatok
-------------------
A felhasználói adatok az e-mail cím kivételével szabadon megváltoztathatóak. Az e-mail cím megváltoztatásához rendszergazda szintű megerősítés szükséges. 

Beállítások
-----------
* Itt állítható be, hogy az e-mail címe látható legyen a projekt többi tagjának. 
* Be állíthatja, hogy szeretne-e e-maileket kapni a projektről.
* Megszűntetheti a felhasználói fiókját.
    

ORCID profil
------------
Az ORCID azonosítóval rendelkezők számára lehetőség van a ORCID profil adatok beolvasására.

.. _user-information:

Felhasználói információk
------------------------
Itt ellenőrizhető, hogy milyen státusszal (üzemeltető, normál vagy inaktív) rendelkezik az adott adatbázisban.

Az adatainkra, feltöltéseinkre és felhasználói profilunkra kapott értékelések súlyozott összesítése

.. _other-databases:

Más adatbázisok
---------------
Itt találja azokat az adatbázisokat felsorolva, amelyekben tag az adott szerveren. Az adatbázis nevére kattintva átléphet egy másik adatbázisba. Minden egyes átlépés után újra be kell jelentkeznie.

.. _activity:

Aktivitás
---------
- Adat feltöltéseink száma (mennyi adatfeltöltést végeztünk összesen eddig)
- Adat módosításaink száma
- Feltöltött rekordok száma az összes feltöltésünkben
- Faj statisztika: Mennyi faj volt az eddigi összes feltöltésükben. Fajonként számlált lista
- Térbeli aktivitási terület kiterjedése km2-ben a feltöltéseink alapján. A kiírt szám klikkelhető és térképen megmutatja az adatrekordokat határoló konvex poligont.

.. _interrupted-imports:

Felfüggesztett adatfeltöltések
------------------------------
Az elmentett feltöltéseink listája. A hivatkozásokra kattintva folytathatja a feltöltést ott, ahol félbehagyta.

.. _bookmarks:

Könyvjelzők
-----------
Lehetőség van a lekérdezések elmentésére és megismétlésére a könyvjelző hivatkozások használatával. A könyvjelző hivatkozások nem megoszhatóak, csak bejelentkezve és a létrehozójuk számára működnek. A könyvjelzők magukat a lekérdezéseket tárolják nem annak az eredményét, így az adatbázis tartalmának változása megváltoztatja a könyvjelző használatával kapott eredményeket is.

.. _sharing-data:

Adatok megosztása
-----------------
A lekérdezési eredmények eltárolhatók és megoszthatók. Ebben az esetben nem az adatbázisban tárolt adatokat látják, akivel megosztották a lekérdezést, hanem annak tárolt változatát. Ez a tárolt eredményállapot nem változik, teljesen független az adatbázistól. Bárki, aki rendelkezik a megosztási hivatkozással, hozzáférhet a lekérdezésben tárolt adatokhoz. A megosztási hivatkozás tartós azonosító, amely egy DOI azonosítóhoz is társítható.

.. _Api keys:

Api kulcsok
-----------
Az aktív és frissíthető API kulcsaink listája. Leginkább a fejlesztők számára van jelentősége.

Modulok egyéni felületei
------------------------
Egyes modulok tehetnek ide ki kezelő felületeket. Pl: postgres felhasználó készítő modul, geometria feltöltő modul, letöltés kérő modul, stb...

Egyedi geometriák kezelése
..........................
Ez a funkció csak akkor érhető el, ha a shared_geoms modul lehetővé teszi.

Lehetőség van egyéni geometriák feltöltésére vagy rajzolására a további műveletekhez. Ezek a műveletek lehetnek térbeli lekérdezések vagy geometria hozzárendelése a feltöltött adatokhoz.

Az egyéni geometriákat a profiloldalon két linket követve tudja kezelni: megosztott geometriák és saját geometriák.

A saját geometriák linket követve törölheti vagy megoszthatja, átnevezheti és módosíthatja a geometriák nézeti beállításait. A nézeti beállítások a következők: Nézet a térbeli kiválasztási listában és Nézet az adatok feltöltése - nevesített térbeli formák hozzárendelése listában.

A megosztott geometriák linket követve átnevezheti a geometriákat és módosíthatja a nézeti beállításokat. A megosztott geometriákat nem törölheti!

PostgreSQL felhasználó létrehozása
..................................
Egy évig aktív felhasználó létrehozása, akinek olvasási joga van a projekt adattábláira SQL kliens programokon keresztül. QGIS használathoz szükséges!

Vélemények
----------
Felhasználói véleményezés. Itt olvashatjuk és reagálhatunk a rólunk írt véleményekre. Mások profil oldalán itt véleményezhetjük az adott felhasználót. 

A vélemények pont értéke beleszámít az összpontozási értékbe, amivel az adatvalidálási munkát is lehet támogatni.
