.. _new-project:

Új OpenBioMaps-projekt létrehozása
==================================

Egy meglévő OpenBioMaps-projekt jogosultsággal rendelkező tagja a
**Founding new project** űrlap használatával hozhat létre új
adatbázisprojektet.

Az új projekt független attól a projekttől, amelyből létrehozták. Az alapító
lesz a projekt első tulajdonosa, és más felhasználók meghívásáig az egyetlen
tagja.

.. TODO: Dokumentálni kell, hogy milyen jogosultság szükséges egy projekt
   létrehozásához, és meg kell adni a **Founding new project** űrlap aktuális
   navigációs útvonalát. Meg kell erősíteni, hogy a projektlétrehozás
   letiltható-e szerver szinten.


A projekt létrehozása előtt
---------------------------

Az űrlap kitöltése előtt gondolja át a következőket:

* a projekt célját és hatókörét;
* a projekt által kezelt információkat;
* a szükséges adatbázistáblákat és kapcsolatokat;
* kik tekinthessék meg, küldhessék be és módosíthassák az adatokat;
* kezel-e a projekt személyes vagy érzékeny biodiverzitási adatokat; valamint
* kik felelősek a projekt adminisztrációjáért és az adatkezelésért.

A projekt adatstruktúrájának és irányításának megtervezéséhez tekintse meg
a következőket:

* :doc:`Kezdeti lépések <getting_started>`;
* :doc:`Adatgyűjtés <data_collection>`;
* :doc:`Adatkezelés <data_management>`; valamint
* :doc:`Adatkezelési szabályzat <data_policy>`.


A projektlétrehozási űrlap kitöltése
------------------------------------

Az űrlapon a következő beállításokat kell megadni.


Projektazonosító
................

Adjon meg egy egyedi, rövid azonosítót a projekthez. Ez az azonosító szerepel
a projekt URL-jében, és előtagként vagy azonosítóként is használható a projekt
adatbázis-konfigurációjában.

Használjon kisbetűkből, számokból és aláhúzásjelekből álló rövid nevet.
Kerülje a szóközöket, az ékezetes karaktereket, az írásjeleket és az
idézőjelek közé tett SQL-azonosítókat. Körültekintően válassza ki az
azonosítót, mert a projekt létrehozása utáni módosítása hatással lehet az
URL-ekre, az adatbázis-objektumokra, a konfigurációs fájlokra, az
API-kliensekre és a külső integrációkra, ezért szinte lehetetlen.

.. TODO: Meg kell erősíteni a pontosan engedélyezett karaktereket, a
   minimális és maximális hosszt, az egyediség hatókörét és a fenntartott
   azonosítókat. Dokumentálni kell, hogy a projektazonosító mindig az
   adatbázistáblák neveként vagy előtagjaként szolgál-e.

.. TODO: Dokumentálni kell, hogy támogatott-e a projektek átnevezése. Ha igen,
   ismertetni kell a teljes migrációs eljárást, valamint annak az URL-ekre,
   az adatbázis-objektumokra, a térkép-konfigurációra, a feladatokra, az
   API-kliensekre és a külső integrációkra gyakorolt hatását.


Projektcím
..........

Adjon meg egy rövid, leíró címet a projekthez. Ez a cím a projekt fejlécében
és más, felhasználók számára látható helyeken jelenik meg.

A cím a projekt létrehozása után lefordítható. Legyen tömör; gyakran két vagy
három szó is elegendő, de az egyértelműség érdekében szükség esetén hosszabb
cím is használható.

A projektleírásokkal és a fordításokkal kapcsolatos információkért tekintse
meg a következőket:

* :ref:`Projektleírás <project-description>`; valamint
* :ref:`Helyi fordítások <localisation>`.


Projektleírás
.............

Adja meg a projekt és céljának részletes leírását. A leírásnak segítenie kell
a leendő közreműködőket és adatfelhasználókat a következők megértésében:

* mit gyűjt a projekt;
* mi a földrajzi, időbeli és taxonómiai hatóköre;
* mely szervezetek vagy személyek felelősek érte;
* hogyan kívánják felhasználni az adatokat; valamint
* hol juthatnak a felhasználók további információkhoz.

A leírás a projekt létrehozása után frissíthető.


Alapértelmezett adathozzáférés
..............................

Válassza ki a projektadatok megtekintésére és módosítására vonatkozó kezdeti
szabályokat. Ezek a beállítások határozzák meg a projekt alapértelmezett
hozzáférési szintjét.

Egy zárt vagy csoportokra korlátozott projekt a létrehozása után részletesebb
rekord- és oszlopszintű hozzáférési szabályokat határozhat meg. Az
alapértelmezett beállítások később is módosíthatók, de a változtatásokat
gondosan tesztelni kell annak biztosítására, hogy ne tegyenek hozzáférhetővé
korlátozott adatokat, és ne akadályozzák a jogosultsággal rendelkező
felhasználók hozzáférését.

Az elérhető hozzáférés-vezérlési lehetőségek leírását lásd az
:doc:`Adathozzáférés <data_access>` című dokumentumban.

.. TODO: Dokumentálni kell a projektlétrehozási űrlapon megjelenő pontos
   hozzáférési lehetőségeket, és mindegyiket hozzá kell rendelni a megfelelő
   ``ACC_LEVEL`` és ``MOD_LEVEL`` konfigurációs értékhez.

.. TODO: Meg kell erősíteni, hogy a projektszintű alapértelmezések módosítása
   hatással van-e a meglévő rekordokra, vagy csak az aktuális hozzáférési
   szabályok kiértékelésének módját változtatja meg.


A térkép kezdeti középpontja
............................

Adja meg a projekt térképének kezdeti középpontját. Ez a beállítás határozza
meg azt a területet, amelyet a felhasználók a térképoldal első megnyitásakor
látnak.

A térkép középpontja később módosítható a térképpel kapcsolatos
adminisztrációs felületen.


A térkép koordináta-referencia-rendszere
........................................

Adja meg a projekt alaptérképe által használt térbeli referencia-azonosítót
(SRID). Az alapértelmezés az EPSG:4326 (WGS 84). A térbeli
referencia-rendszerek a https://spatialreference.org/ webhelyen kereshetők
meg.

Csak akkor használjon másik SRID-t, ha a projektnek egyértelmű műszaki
követelménye van rá, és minden érintett összetevő támogatja. A beállított
referencia-rendszernek kompatibilisnek kell lennie a projekt térbeli
adataival, az OpenLayers konfigurációjával, a MapServer rétegeivel, a
lekérdezéssablonokkal, az exportokkal és a külső kliensekkel.

Egy SRID módosítása nem feltétlenül alakítja át a meglévő koordinátákat. A
helytelen SRID hozzárendelése rossz helyre teheti a geometriákat, vagy
érvénytelenné teheti a térbeli lekérdezéseket.

A kapcsolódó konfigurációs információkért lásd:
:ref:`Térképbeállítások <map-settings>`.

.. TODO: Meg kell erősíteni, hogy ez a mező az alaptérkép vetületét, a projekt
   geometriájának SRID-jét, a webes térkép megjelenítési vetületét vagy ezek
   valamilyen kombinációját határozza-e meg. Dokumentálni kell, hogy hol
   történnek a koordináta-transzformációk.


A projekt létrehozása
---------------------

A kitöltött űrlap elküldése után az OpenBioMaps kísérleti állapotban hozza
létre a projektet. Ez az állapot arról tájékoztatja a felhasználókat, hogy a
projekt struktúrája és konfigurációja még fejlesztés alatt áll; önmagában nem
akadályozza a projekt működését.

.. TODO: Meg kell határozni a támogatott projektállapotokat, azok pontos
   jelentését, valamint azt, hogyan módosíthatja egy adminisztrátor a projekt
   állapotát kísérletiről tesztelés alatt állóra, stabilra, archiváltra vagy
   más elérhető állapotra. Meg kell erősíteni, hogy a projekt állapota
   befolyásolja-e az alkalmazás működését.

A projekt létrehozása során a rendszer létrehozza a szükséges konfigurációs
és adatbázis-objektumokat. A folyamat befejeződésekor megjelenít egy üzenetet,
amely tartalmazza a projekt SQL-adminisztrátorának nevét és jelszavát.

Tárolja ezeket a hitelesítési adatokat jóváhagyott jelszókezelőben vagy más
biztonságos helyen. Ne küldje el őket titkosítatlan e-mailben, ne foglalja
őket dokumentációba, és ne véglegesítse őket forráskód-tárolóba. Az
SQL-adminisztrátor módosíthatja vagy törölheti a projekt adatait és
adatbázis-objektumait.

.. TODO: Dokumentálni kell, hogy a létrehozott SQL-adminisztrátori jelszó
   ismét megjeleníthető-e, módosítható-e az OpenBioMaps használatával, vagy
   visszaállítható-e a Supervisor segítségével. Ki kell egészíteni a
   dokumentációt a hitelesítési adatok módosításának ajánlott eljárásával.

Az alapító az eredeti projektben használt OpenBioMaps-felhasználónévvel és
-jelszóval férhet hozzá az új projekthez. Az SQL-adminisztrátor hitelesítési
adatai elkülönülnek az alapító webalkalmazásban használt hitelesítési
adataitól, és csak az ezeket igénylő adatbázis-adminisztrációs feladatokhoz
használhatók.


Kezdeti adatbázis-struktúra
---------------------------

A projekt létrehozásakor az OpenBioMaps létrehoz egy kezdeti projektadattáblát,
amely tartalmazza az adott OpenBioMaps-verzió által megkövetelt
rendszeroszlopokat. A kezdeti tábla ezután projekt-specifikus oszlopokkal
bővíthető, további táblák vagy nézetek pedig az adminisztrációs felületen
regisztrálhatók.

Ne törölje és ne nevezze át a rendszer oszlopait pusztán azért, mert
használaton kívülinek tűnnek. Az adatfeltöltés feldolgozása, a hozzáférési
szabályok, az előzmények, a mellékletek, a modulok vagy a külső kliensek
függhetnek tőlük.

A műszaki részletekért tekintse meg a következőket:

* :ref:`Adatbázistáblák és -oszlopok <database-columns>`; valamint
* :doc:`Az OpenBioMaps adatfolyama és adatbázis-integrációja <obm_workflow>`.

.. TODO: Dokumentálni kell az új projekthez létrehozott objektumok pontos
   körét, beleértve az adatbázisokat, sémákat, táblákat, rendszeroszlopokat,
   szekvenciákat, szabálytáblákat, szerepköröket, konfigurációs fájlokat,
   mapfile-okat, könyvtárakat és alapértelmezett modulokat.


Az új projekt konfigurálása
---------------------------

Egy újonnan létrehozott projekt további konfigurálást igényel a rendszeres
adatgyűjtés vagy nyilvános használat megkezdése előtt.

Egy tipikus beállítási folyamat a következő lépéseket foglalja magában:

#. **Határozza meg az adatmodellt.**

   Adja hozzá a szükséges oszlopokat a kezdeti adattáblához, és hozza létre
   vagy regisztrálja a további táblákat, nézeteket, kapcsolatokat,
   megszorításokat, indexeket és metaadatokat.

   Lásd: :ref:`Adatbázistáblák és -oszlopok <database-columns>`.

#. **Állítsa be a hozzáférési szabályokat és a csoportokat.**

   Hozza létre a szükséges felhasználói csoportokat, és reprezentatív
   felhasználói fiókok használatával ellenőrizze a projekt-, rekord- és
   oszlopszintű hozzáférést.

   Lásd: :doc:`Adathozzáférés <data_access>` és
   :ref:`Csoportok <group-settings>`.

#. **Hozza létre a feltöltési űrlapokat.**

   Határozzon meg külön űrlapokat a szükséges webes, fájlfeltöltési, API- vagy
   mobil munkafolyamatokhoz. Állítsa be a kötelező mezőket, az ellenőrzést,
   az alapértelmezett értékeket, a hozzáférések hozzárendelését és a
   közzétett űrlapverziókat.

   Lásd: :doc:`Feltöltési űrlapok kezelése <upload_forms>`.

#. **Állítsa be az SQL-lekérdezéssablonokat.**

   Hozza létre a szöveges lekérdezések és a térbeli térképrétegek által
   használt lekérdezéssablonokat. Foglalja bele a szükséges
   hozzáférés-vezérlési és modulhelyőrzőket.

   Lásd: :ref:`SQL-lekérdezési beállítások <sql-query-settings>`.

#. **Állítsa be a térképes felületet.**

   Határozza meg a térkép kezdeti nézetét, az alaptérképeket, a fedvényrétegeket,
   a MapServer konfigurációját, a koordináta-referencia-rendszereket, a
   stílusokat, valamint a térképrétegek és a lekérdezéssablonok közötti
   kapcsolatokat.

   Lásd: :ref:`Térképbeállítások <map-settings>`.

#. **Engedélyezze és állítsa be a modulokat.**

   Csak a projekthez szükséges modulokat telepítse vagy engedélyezze. A
   gyakori lekérdezési és megjelenítési modulok közé tartozhat a
   ``text_filter``, az ``identify_points``, a ``results_asStable``, a
   ``results_buttons`` és a ``results_summary``, az OpenBioMaps verziójától
   és a projekt követelményeitől függően.

   Lásd: :doc:`Modulok <modules>`.

#. **Állítsa be a támogató munkafolyamatokat.**

   Szükség esetén állítsa be az előzményeket, a hozzáférési szabályokhoz és a
   taxonómiához tartozó triggereket, az üzenetsablonokat, a háttérfeladatokat,
   a mellékletek kezelését, a fordításokat és a külső integrációkat.

   Lásd: :ref:`Függvények <trigger-functions>` és
   :doc:`Háttérfeladatok <jobs>`.

#. **Adja hozzá a projektinformációkat és az irányítási dokumentumokat.**

   Tekintse át a projekt címét és leírását, a felelős szervezeteket, a
   kapcsolattartási adatokat, az adatkezelési szabályzatot, az adatvédelmi
   információkat, a licenceket, a forrásmegjelölési követelményeket és a
   felhasználási feltételeket.

   Lásd: :doc:`Adatkezelési szabályzat <data_policy>`.

#. **Tesztelje a teljes munkafolyamatot.**

   Küldjön be reprezentatív rekordokat minden támogatott kliensen keresztül.
   Tesztelje az érvényes és érvénytelen értékeket, a mellékleteket, a
   geometriákat, a megszakított feltöltéseket, az ellenőrzést, az
   előzményeket, a hozzáférési korlátozásokat, a lekérdezéseket, a térképeket,
   az API-válaszokat, az exportokat, valamint a törlési és javítási
   eljárásokat.

#. **Készítse elő a biztonsági mentéseket és a monitorozást.**

   Győződjön meg arról, hogy az adatbázisra, a mellékletekre, a
   konfigurációra, a modulokra, a feladatokra és a térképbeállításokra
   kiterjed a tervezett biztonsági mentési eljárás. A helyreállíthatóságra
   vonatkozó vállalások megtétele előtt tesztelje a visszaállítást.


Kiadás előtti ellenőrzőlista
----------------------------

Mielőtt rendszeres közreműködőket hívna meg, vagy nyilvánossá tenné a
projektet, ellenőrizze, hogy:

* az adatmodell megfelelően reprezentálja-e a tervezett adatgyűjtési
  módszertant;
* minden táblához és oszlophoz tartoznak-e érdemi metaadatok;
* a feltöltési űrlapok a tervezett közzétett verziókat használják-e;
* a szükséges esetekben a szerver kikényszeríti-e az ellenőrzést;
* a nyilvános és a korlátozott hozzáférést egymástól függetlenül
  tesztelték-e;
* az érzékeny helyadatok és a személyes adatok megkapják-e a tervezett
  védelmet;
* a térképes és a szöveges lekérdezések konzisztens rekordokat adnak-e
  vissza;
* a letöltések és az API-válaszok csak az engedélyezett mezőket
  tartalmazzák-e;
* elérhetők-e a licencek, a forrásmegjelölési és a hivatkozási útmutatók;
* az adminisztrátorok és az adatgazdák felelősségi körei egyértelműen
  kijelöltek-e;
* tesztelték-e a háttérfeladatokat és az értesítéseket;
* létezik-e tisztítási eljárás a létrehozott fájlokhoz és a megszakított
  feltöltésekhez;
* a szerver- és projektnaplókat megtekinthetik-e a jogosultsággal rendelkező
  adminisztrátorok;
* a biztonsági mentések tartalmaznak-e minden olyan adatot és fájlt, amelynek
  megőrzését vállalták; valamint
* sikeresen elvégeztek-e egy visszaállítási tesztet.

Tartsa a projektet kísérleti vagy tesztelési állapotban mindaddig, amíg nem
ellenőrizték a struktúrát, a hozzáférési modellt, az adatrögzítési
munkafolyamatokat és a helyreállítási eljárást.
