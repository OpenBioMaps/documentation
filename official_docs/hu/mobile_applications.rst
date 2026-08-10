:author: Miklós Bán
:date: 2026-08-10

Mobilalkalmazások
*****************

Számos mobilalkalmazás támogatja az OpenBioMaps funkcióit. Ezek közé tartoznak
az adatok online és offline környezetben történő lekérésére és gyűjtésére
szolgáló eszközök, a Progressive Web Appoktól (PWA-k) a natív
mobilalkalmazásokig.

Offline alkalmazás Android- és iOS-eszközökhöz
==============================================

.. TODO:  További fejlesztések szükségesek még:
   Meg kellene adni az alkalmazás hivatalos nevét, valamint a Google Play és App Store hivatkozásokat.
   Hasznos lenne képernyőképekkel bemutatni a szerver- és projektválasztást, a szinkronizálást, valamint a megfigyelési esemény kezelését.
   Pontosítani kellene, hogyan működik a szerverválasztás, és hozzáadható-e egyedi OpenBioMaps-szerver.
   Dokumentálni kellene a szinkronizálási hibák kezelését és azt, hogy mikor biztonságos törölni a szinkronizált adatokat az eszközről.
   Jó lenne részletesen leírni a biztonsági mentési és exportálási formátumokat, illetve azok visszaállítását.
   Érdemes lenne méréssel alátámasztott ajánlást adni a GPS idő- és távolságszűrőinek akkumulátorhasználatáról.
   Pontosítani kellene, milyen Android- és iOS-verziókat támogat az alkalmazás.
   Az adatvédelmi és jogosultsági információkat — különösen a helyadatok, csatolmányok és hibakeresési mentések kezelését — külön szakaszban is érdemes lenne összefoglalni.



Áttekintés
----------

Az offline mobilalkalmazás terepi adatgyűjtésre készült. Rugalmas felületet
biztosít a projektspecifikus adatgyűjtési feladatokhoz, és a szükséges
projektek és űrlapok letöltése után folyamatos internetkapcsolat nélkül is
használható.

Az OpenBioMaps nem biztosít egyetlen előre meghatározott adatgyűjtési űrlapot
vagy módszert. Minden projekt saját űrlapokat és adatmezőket határoz meg.
Következésképpen a következők a projekt konfigurációjától és az aktuális
felhasználó jogosultságaitól függnek:

* mely projektek érhetők el;
* mely űrlapok érhetők el ezekben a projektekben;
* mely mezők jelennek meg az egyes űrlapokon; valamint
* hogyan viselkednek ezek a mezők.

Csak hitelesített felhasználók gyűjthetnek adatokat az alkalmazással. Az
alkalmazás nem biztosít általános regisztrációs funkciót, bár egyes projektek
az alkalmazáson kívül egyszerű vagy automatikus regisztrációs folyamatot is
támogathatnak.

Fejlesztés
----------

Az alkalmazást az Ecollab Ltd. fejleszti React Native és Expo használatával.

Kezdeti lépések
---------------

A szerver és a projekt kiválasztásához, a bejelentkezéshez, valamint az
űrlapok letöltéséhez internetkapcsolat szükséges. A szükséges űrlapok
letöltése után azok offline is használhatók.

Szerver kiválasztása
^^^^^^^^^^^^^^^^^^^^

Válassza ki a használni kívánt projektet üzemeltető OpenBioMaps-szervert. A
szerverhez való kapcsolódáshoz és az elérhető projektinformációk lekéréséhez
internetkapcsolat szükséges.

Projekt kiválasztása
^^^^^^^^^^^^^^^^^^^^

Válasszon egy projektet a kiválasztott szerveren elérhető projektek közül. A
megjelenített projektek a szerver konfigurációjától és az Ön hozzáférési
jogosultságaitól függnek.

Internetkapcsolat szükséges a projekt első betöltésekor vagy konfigurációjának
frissítésekor.

Bejelentkezés
^^^^^^^^^^^^^

Jelentkezzen be e-mail-címével és jelszavával. A hitelesítéshez
internetkapcsolat szükséges.

Sikeres bejelentkezés után hozzáférhet a fiókja számára elérhető projektekhez
és űrlapokhoz. A nyilvánosan elérhető projektek és űrlapok szintén
megjelenhetnek.

Űrlap kiválasztása
^^^^^^^^^^^^^^^^^^

Online állapotban válasszon ki és nyisson meg egy űrlapot az offline
használathoz szükséges információk letöltéséhez. Az űrlap sikeres betöltése
után offline is elérhető marad mindaddig, amíg el nem távolítják a helyi
adatait, vagy amíg az űrlapot nem szükséges frissíteni.

Űrlap kitűzése a kezdőképernyőre
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A gyakran használt űrlapok a gyorsabb hozzáférés érdekében kitűzhetők a
kezdőképernyőre. Egy űrlap kitűzéséhez vagy a kitűzés megszüntetéséhez
koppintson az űrlap neve melletti rajzszög ikonra.

Az alkalmazás felépítése
------------------------

Főképernyő
^^^^^^^^^^

A főképernyőről a következők érhetők el:

* a térkép;
* az űrlapok;
* az összegyűjtött adatok;
* a beállítások;
* a nyomvonalnaplók; valamint
* az eszközök.

A kitűzött űrlapok a gyors hozzáférés érdekében megjelennek a főképernyőn. Ha
éppen fut egy megfigyelési esemény, annak állapota megjelenik a megfelelő
kitűzött űrlap gombján.

Térképképernyő
^^^^^^^^^^^^^^

A térképképernyő a rögzített megfigyelések és az állandó mintavételi helyek
megtekintésére szolgál.

A térképen megjelenő információk a kiválasztott projekttől, a letöltött
adatoktól és a projekt konfigurációjától függnek.

Űrlapok képernyő
^^^^^^^^^^^^^^^^

Az űrlapok képernyő a következőkhöz tartalmazhat űrlapokat:

* alkalmi megfigyelések; valamint
* megfigyelési események.

Az űrlap melletti felkiáltójel azt jelzi, hogy frissítés érhető el. A
szerverről történő kényszerített frissítéshez tartsa nyomva az űrlap nevét.
Az űrlap frissítéséhez internetkapcsolat szükséges.

Az offline használatra letöltött űrlapok jelölést kapnak, hogy
megkülönböztethetők legyenek az offline még nem elérhető űrlapoktól.

A futó megfigyelési eseményeket a megfelelő űrlap neve mellett jelzi az
alkalmazás.

Összegyűjtött adatok képernyő
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Az összegyűjtött adatok képernyő az eszközön rögzített megfigyeléseket sorolja
fel. A szerveroldali konfigurációtól függően a listában kiemelhetők a fontos
értékek, például egy faj neve vagy az egyedek száma. Ez a viselkedés a
``bold_yellow`` modullal állítható be.

Erről a képernyőről a felhasználók:

* áttekinthetik az összegyűjtött rekordokat;
* szinkronizálhatják a rekordokat a szerverrel;
* szerkeszthetik a még nem szinkronizált rekordokat; valamint
* törölhetik a szinkronizált rekordokat az eszközről.

A szinkronizáláshoz internetkapcsolat szükséges. A helyi rekordok törlése
előtt ellenőrizze, hogy a szinkronizálás sikeresen befejeződött-e.

Nyomvonalnaplók képernyő
^^^^^^^^^^^^^^^^^^^^^^^^

A nyomvonalnaplók aktív űrlaptól függetlenül is rögzíthetők. A
szinkronizálás során a rögzített nyomvonalnaplók feltöltődnek a projekt
nyomvonalnapló-táblájába.

Erről a képernyőről a felhasználók:

* megtekinthetik a rögzített nyomvonalnaplókat;
* elindíthatják a nyomvonalnapló rögzítését;
* leállíthatják a nyomvonalnapló rögzítését; valamint
* szinkronizálhatják a nyomvonalnaplókat a szerverrel.

Eszközök képernyő
^^^^^^^^^^^^^^^^^

Az eszközök képernyő a terepmunka során hasznos segédprogramokat biztosít,
többek között:

* véletlenszám-generátort; valamint
* egyéni listagenerátort, amely például gyűrűszámok listájának létrehozására
  használható.

Beállítások
-----------

Nyelv
^^^^^

Az alkalmazás jelenleg az angol, román, magyar, francia, német, kirgiz és
orosz nyelvet támogatja.

A fordításokhoz az
`OpenBioMaps alkalmazás fordítási projektjén
<https://translate.openbiomaps.org/projects/ecollab/expo-app/>`_ keresztül
járulhat hozzá.

Téma
^^^^

Az alkalmazás három témabeállítást biztosít:

* rendszer alapértelmezése;
* sötét; valamint
* világos.

Biztonsági mentés és exportálás
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Biztonsági mentés készíthető az alkalmazás adatainak megőrzéséhez vagy
hibakeresési információk biztosításához.

Az exportálási funkció az alkalmazás által tárolt adatokat más szoftverekkel
is használhatóvá teszi. Az elérhető adatoktól függően az export szabványos
formátumokat, például CSV- és GPX-fájlokat, valamint csatolt JPEG-képeket
tartalmazhat.

A biztonsági mentések és az exportok érzékeny projekt-, hely- vagy
felhasználói adatokat tartalmazhatnak. Ezeket a fájlokat biztonságosan tárolja
és továbbítsa.

Űrlapbeállítások
^^^^^^^^^^^^^^^^

Az alkalmazás több lehetőséget biztosít a kitűzött mezőértékek kezelésére:

Újrainicializálás az űrlap minden megnyitásakor
  A kitűzött értékek az űrlap minden megnyitásakor alaphelyzetbe állnak. Ez
  az alapértelmezett és legbiztonságosabb beállítás. Kényelmetlen lehet, ha
  két űrlapot párhuzamosan használnak, mert a közöttük történő váltás
  alaphelyzetbe állíthatja a kitűzött értékeket.

Mindig a szerverbeállítások használata
  Az alkalmazás a felhasználó által meghatározott kitűzött értékek megőrzése
  helyett a szerver konfigurációját követi. Ez a beállítás azoknak a
  felhasználóknak hasznos, akiknek nincs szükségük kitűzött értékekre, vagy
  hajlamosak véletlenül kitűzni értékeket.

Felhasználói beállítások megtartása a szinkronizálásig
  A felhasználó által meghatározott kitűzött értékek az adatok
  szinkronizálásáig elérhetők maradnak. Ez gyakran praktikus, ha egy
  terepmunka során végig azonos típusú adatokat gyűjtenek, majd a nap végén
  szinkronizálják őket. A szinkronizálás után a kitűzött értékek törlődnek.

Felhasználói beállítások állandó megtartása
  A felhasználó által meghatározott kitűzött értékek mindaddig megmaradnak,
  amíg manuálisan meg nem változtatják őket. Ezt a beállítást körültekintően
  kell használni, mert egy elavult kitűzött érték véletlenül későbbi
  rekordokba is bekerülhet.

Az alkalmazás sikeres vagy sikertelen adatrögzítési kísérlet után
hangjelzést is lejátszhat.

Összegyűjtött adatok beállításai
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Az összegyűjtött adatok beállításai szabályozzák, hogy az alkalmazás:

* megjelenítse-e a csatolt fájlokat;
* automatikusan szinkronizálja-e az összegyűjtött adatokat; valamint
* mindig megjelenítse-e a műveleti gombokat a rekord részletei alatt, az
  összegyűjtött adatok képernyőn.

Az automatikus szinkronizáláshoz hálózati hozzáférés szükséges. A rekordok
vagy az alkalmazásadatok eszközről történő törlése előtt ellenőrizze a
szinkronizálás állapotát.

GPS- és nyomvonalnapló-beállítások
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A GPS használata idő és távolság alapján szűrhető. Ezek a beállítások az
egypontos rögzítésre és a nyomvonalpontok rögzítésére egyaránt hatással
vannak.

A távolságszűrő csökkenti a szükségtelen helyzetfrissítések számát, ha az
eszköz a beállított távolságnál kevesebbet mozdult el. Általános használatra
1 és 5 méter közötti érték ajánlott, de a legmegfelelőbb beállítás az
eszköztől, az elvárt pontosságtól és a terepi körülményektől függ.

Az időintervallum határozza meg, milyen gyakran történjen a nyomvonalpontok
rögzítése. Az alapértelmezett időköz 5 másodperc. A rövidebb időköz
részletesebb nyomvonalat eredményezhet, de növelheti az
akkumulátor-felhasználást és a tárolt adatok mennyiségét is. A terepmunka
előtt tesztelje a kiválasztott időközt a projektben használt eszközökön.

Tárhely
^^^^^^^

A tárhelybeállítások a következőkre használhatók:

* a nem használt fájlok törlése;
* a nem használt munkamenetek eltávolítása;
* a kiválasztások törlése; valamint
* az automatikus kiegészítési listák törlése.

Az adatok törlése előtt körültekintően tekintse át az elérhető lehetőségeket.
A nem szinkronizált megfigyeléseket és nyomvonalnaplókat a helyi
alkalmazásadatok eltávolítása előtt fel kell tölteni vagy biztonsági mentésbe
kell foglalni.

Jogosultságok
^^^^^^^^^^^^^

A jogosultságok képernyő megmutatja, hogy az alkalmazás hozzáfér-e az
operációs rendszer szükséges szolgáltatásaihoz, beleértve a
helymeghatározási szolgáltatásokat. A vonatkozó operációsrendszer-beállítások
is elérhetők innen.

A GPS-alapú adatgyűjtéshez és a nyomvonalnaplók rögzítéséhez helyhozzáférési
jogosultság szükséges. Az elérhető jogosultsági lehetőségek és a háttérben
történő helymeghatározás működése Android és iOS rendszeren eltérhet.

A mobilalkalmazás szerveroldali beállításai
-------------------------------------------

Űrlapok
^^^^^^^

A mobil adatgyűjtési űrlapok az OpenBioMaps feltöltésiűrlap-kezelő felületén
állíthatók be.

További információkért lásd:
:doc:`Feltöltési űrlapok kezelése <upload_forms>`.

Online alkalmazások mobileszközökhöz
====================================

Az OpenBioMaps mobileszközökhöz használható böngészőalapú alkalmazásokat is
biztosít:

* :doc:`Térképalapú adatlekérdező alkalmazás <pwa>`
* :doc:`Mintavételihely-kezelő alkalmazás <mapp>`
