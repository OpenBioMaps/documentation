Adminisztratív oldalak
**********************

Adatbázis oszlopok
------------------
Itt lehet beállítani, hogy az egyes táblákból melyik oszlopok legyenek elérhetőek az űralpok készítéséhez és lekérdezéshez a webes felületen. 

Szintén itt lehet megadni a különlegesen kezelet oszlopokat. Ez azt jelenti, hogy olyan oszlopok amiket egyes modulok használnak anélkül, hogy tudnák mi az oszlop pontos neve ill. ugyanilyen alapon metakeresésekben is elérhetőek. Ilyen kitüntetett oszlopok a fajnév, dátum, adatgyüjtő, példányszám és hely oszlopok. A hely oszlopnál külön megadható az X,Y koordináta oszlop és a postgres geometria oszlop is. Dátumnál megadható több dátum oszlop is, adatgyűjtőnél szintén több oszlop is megadható. Fajnévél külön megadható a tudományos és nemzeti nevet tartalmazó oszlop ha van ilyen. Minden egyéb oszlop "adat" típusúra kell beállítani.

Csoportok
---------
Felhasználói jogosultság kezelés része. Űrlapok, modulok és adatok eléréséhez csoportokat lehet létrehozni. Az egyes felhasználók is lehetnek csoportok.

Feltöltő űrlapok
----------------
Itt lehet feltöltő űrlapokat létrehozni és módosítani. 
Az űrlapok kezelésének részletes leírása itt található:
:ref:`new-upload-form` and :ref:`edit-upload-form`.

Függvények
----------
Táblatörténet, elérési szabályozás és fajnév táblák trigger függvényei itt megtekinthetőek és ki-be kapcsolhatóak.

Faj nevek
---------
Faj nevek karbantartása. Faj nevek összekapcsolása, javítása és státuszának beállítása.

Hozzáférések
------------
A projekt általános hozzáférési beállításának megtekintése. Itt ez nem konfogurálható!

Nyelvi fájlok
-------------
Elavult.

Modulok
-------
Beépülő modulok hozzáadása, engedélyezése és paraméterezésének felülete.
Az engedélyezett modulok használatát felhazsnálókhoz/csoportokhoz lehet rendelni.

Paraméterként megadhatunk egyszerű karakterláncot, vagy JSON objektumot.

Az elérhető modulok listája és leírásai itt találhatóak: 
:doc:`modulok <../modules>`


Elmentett feltöltések
---------------------
A felhasználók elmentett és be nem fejezett feltöltései elérhetők innen. 

Fájl kezelő
-----------
Csatolt fájlként feltöltött képek és egyéb állományok listája és kezelése.

SQL lekérdezés beállítások
--------------------------
Adatlekérdezésekhez az alap SQL lekérdezés beállítása. Mapserver rétgenként lehet egyet létrehozni.

Webes térképi rétegek
---------------------
Az egyes SQL lekérdezésekhez tartozó openlayers beállítások helye.

Tagok
-----
A projektbe regisztrált tagok listája. Státuszokat és csoport tagságokat lehet itt állítgatni

Mapserver beállítások
---------------------
A projekthez tartozó mapserver mapfájlok konfigurálhatóak itt.

Szerver logok
-------------
Hibakeresésre szolgál. A projekt szerver belső üzenetei és a mapserver üzenetei tekinthetők meg itt. 
