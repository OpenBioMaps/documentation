:author: Miklós Bán
:date: 2026-08-09

Adatgyűjtés
***********

A biodiverzitási adatgyűjtés az élő szervezetek előfordulását,
egyedszámát, állapotát vagy más jellemzőit rögzíti azzal a környezettel
együtt, amelyben az információt megszerezték. Ez a környezet rendszerint
magában foglalja a gyűjtés helyét és időpontját, a megfigyelőt vagy az
adatforrást, a mintavételi módszert és a mintavételi ráfordítás mértékét.

Az adatgyűjtési folyamat kialakítása határozza meg, hogy az abból származó
adatok milyen tudományos kérdések megválaszolását teszik lehetővé. Egy faj
előfordulását rögzítő rekord dokumentálhatja, hogy a fajt egy adott helyen
és időpontban észlelték, a hiány, az egyedszám, az elterjedés vagy az
időbeli változás becsléséhez azonban általában strukturált mintavételi terv
és a mintavételi ráfordításra vonatkozó információ szükséges
[MacKenzie2002]_ [Isaac2014]_.

Az OpenBioMaps nem ír elő egyetlen adatmodellt vagy mintavételi protokollt.
Ehelyett konfigurálható adatbázistáblákat, adatrögzítési űrlapokat,
validálási szabályokat, térbeli mezőket és hozzáférés-szabályozást biztosít,
amelyek különböző biodiverzitási projektekhez igazíthatók. Ezért a
mintavételi tervet és a rögzített mezők jelentését a projektnek kell
meghatároznia az adatbázis és az űrlapok konfigurálása előtt.

Ez az oldal általános útmutatást nyújt a biodiverzitási adatgyűjtési terv
és egy OpenBioMaps-projekt összekapcsolásához. Az űrlapok konfigurálására
vonatkozó részletes útmutató itt található:
:doc:`Feltöltési űrlapok kezelése <upload_forms>`.


Az adatgyűjtés megtervezése
===========================

Az adatbázistáblák vagy adatrögzítési űrlapok létrehozása előtt meg kell
határozni a gyűjtés célját és azokat a kérdéseket, amelyek megválaszolását
az adatoktól várják. A fontos tervezési döntések közé tartoznak a
következők:

* mely szervezeteket, taxonómiai csoportokat, élőhelyeket vagy környezeti
  változókat rögzítik;
* a megfigyeléseket alkalomszerűen vagy előre meghatározott protokoll
  alapján gyűjtik-e;
* meg kell-e őrizni a sikertelen észlelési vagy nulla megfigyelést
  tartalmazó eseményeket;
* milyen térbeli és időbeli egységeket használnak;
* rögzíteni kell-e a mintavételi ráfordítást, a módszertant és a környezeti
  feltételeket;
* megismétlik-e a mintavételt ugyanazokon a helyszíneken;
* kik gyűjtik, validálják, kezelik és használják az adatokat;
* milyen ellenőrzött szótárakat és taxonómiai referenciákat használnak;
  valamint
* milyen metaadatokat és származási információkat kell megőrizni.

Ezeket a döntéseket az adatbázis műszaki szerkezetének véglegesítése előtt
kell meghozni. Egy hiányzó mező későbbi hozzáadása lehetővé teheti új
információk gyűjtését, de nem képes visszaállítani a korábbi felmérések
során nem rögzített háttér-információkat.

A szélesebb körű biodiverzitási felmérésekhez hozzájárulni kívánó
projekteknek azt is meg kell fontolniuk, hogyan kapcsolódnak
megfigyeléseik a már kialakult fogalmakhoz és szabványokhoz. Az Essential
Biodiversity Variables az egyik olyan keretrendszer, amely összekapcsolja
a helyi megfigyeléseket a szélesebb körű biodiverzitás-monitorozással
[Pereira2013]_. A Darwin Core széles körben használt szókészletet biztosít
a taxonokra, előfordulásokra, eseményekre, helyszínekre és kapcsolódó
biodiverzitási adatokra vonatkozó információk cseréjéhez [Wieczorek2012]_.


A legfontosabb adatgyűjtési megközelítések
==========================================

A biodiverzitási megfigyelések többféle módon gyűjthetők. A következő
kategóriák nem zárják ki egymást: egyetlen OpenBioMaps-projekt több
megközelítéshez is használhat különböző űrlapokat és táblákat.


Alkalmi megfigyelések
---------------------

Az alkalmi, véletlenszerű vagy eseti megfigyelés egy előre meghatározott
mintavételi terv követése nélkül észlelt szervezetet rögzít. Ilyen lehet
például egy séta során észrevett ritka madár, egy ismeretlen növényről
készített fénykép vagy egy lakossági bejelentésben szereplő elütött állat.

Egy jól használható alkalmi megfigyelésnek általában a következőket kell
tartalmaznia:

* a megfigyelt taxont;
* a megfigyelés dátumát és – ha rendelkezésre áll – időpontját;
* a helyszínt;
* a megfigyelőt vagy a rekord forrását;
* az egyedszám vagy az egyedek számára vonatkozó információt, ahol ez
  releváns; valamint
* a rendelkezésre álló alátámasztó bizonyítékot, például fényképet,
  hangfelvételt, példányhivatkozást vagy megjegyzést.

Az alkalmi rekordok dokumentálhatják az előfordulásokat, bővíthetik a faj
észlelési helyeire vonatkozó ismereteket, és további felméréseket
alapozhatnak meg. Elterjedésmodellezéshez vagy trendelemzéshez is
hozzájárulhatnak, ha a mintavételi torzításukat kifejezetten figyelembe
veszik.

A bejelentett előfordulások gyűjteménye azonban rendszerint nem mutatja
meg, hogy a megfigyelők hol keresték, de nem észlelték a fajt. Az
adatokat az egyenetlen adatgyűjtési ráfordítás, a hozzáférhetőség, a
megfigyelők preferenciái és az azonosítási készségek eltérései is
befolyásolhatják. Emiatt a feldolgozatlan alkalmi rekordok önmagukban
általában nem értelmezhetők torzítatlan foglaltsági, egyedszám-, populáció-
méret-, elterjedés- vagy időbeli változásbecslésként [Isaac2014]_.

Egy protokoll javíthatja az alkalmi megfigyelések egységességét azáltal,
hogy meghatározza a kötelező mezőket, az elfogadható bizonyítékokat, a
taxonómiai validálást, valamint a térbeli és időbeli pontosságot. Ezek a
követelmények javítják a rekordok minőségét, de önmagukban nem alakítják
az alkalmi gyűjtést valószínűségi alapú vagy szisztematikus felméréssé.


Mintavételi és megfigyelési események
-------------------------------------

A mintavételi vagy megfigyelési esemény egy meghatározott helyen és
időpontban végzett, körülhatárolt adatgyűjtési tevékenységet jelent. Az
esemény megadhatja a módszert, az időtartamot, a mintavételi területet, a
transzekt hosszát, a csapdák vagy a megfigyelők számát, illetve a
mintavételi ráfordítás más mérőszámát is.

Egy esemény a következőket tartalmazhatja:

* egyetlen szervezetre vonatkozó megfigyelést sem, ha a felmérést
  elvégezték, de egyetlen célszervezetet sem észleltek;
* egy megfigyelést; vagy
* azonos mintavételi tevékenységhez kapcsolódó több megfigyelést.

Az észlelést nem tartalmazó események megőrzése akkor fontos, ha egy rekord
hiányának meghatározott jelentése van. A dokumentált sikertelen észlelés
azt mutatja, hogy meghatározott protokoll alapján történt mintavétel, míg
egy alkalmi rekord hiánya nem igazolja, hogy bárki keresett volna az adott
helyszínen. Az ismételt észlelési és sikertelen észlelési adatok megfelelő
vizsgálati terv és modellfeltételezések esetén alkalmasak lehetnek
foglaltságmodellezésre és a tökéletlen észlelhetőség becslésére
[MacKenzie2002]_.

Az OpenBioMaps rendszerben a közös eseményinformációk egyszer tárolhatók
egy esemény- vagy megfigyelésilista-rekordban, míg az egyes
taxonmegfigyelések közös azonosítón keresztül kapcsolhatók ehhez a
rekordhoz. Ez elkerüli a szükségtelen ismétlést, és lehetővé teszi az
esemény megőrzését akkor is, ha egyetlen szervezetre vonatkozó megfigyelést
sem tartalmaz.

A különbség részletesebb ismertetését lásd:
:doc:`Megfigyelési események és alkalmi megfigyelések <observation_events>`.


Ismételt monitorozás
--------------------

A monitorozás az állapot vagy a változás értékelése érdekében ismételten
gyűjtött megfigyelésekből áll. Rendszerint állandó vagy kiválasztott
mintavételi helyszíneket, dokumentált módszert, meghatározott ütemezést és
összehasonlítható ráfordítási mérőszámokat alkalmaz.

Egy monitorozási tervben szükség lehet a következők rögzítésére:

* a mintavételi helyszín azonosítója és helye;
* az egyes mintavételi események kezdete és vége;
* az alkalmazott protokoll és felszerelés;
* az időtartam, terület, távolság vagy a ráfordítás más mérőszáma;
* az észlelések és a kifejezetten rögzített sikertelen észlelések;
* az egyedszám, borítás, biomassza, állapot vagy más válaszváltozó;
* a környezeti feltételek és az észlelhetőséget befolyásoló tényezők;
* a protokoll vagy a mintavételi helyszín változásai; valamint
* a minőség-ellenőrzési és validálási információk.

Az adatbázisnak meg kell különböztetnie az állandó entitásokat – például a
mintavételi helyszíneket és protokollokat – az ismételt eseményektől és az
ezek során végzett megfigyelésektől. Ehhez általában kapcsolódó táblákra
van szükség egyetlen, minden információtípust tartalmazó tábla helyett.

Az OpenBioMaps ezeket a kapcsolatokat projektspecifikus táblákkal,
azonosítókkal, feltöltési űrlapokkal, lekérdezésekkel és adatfeldolgozási
munkafolyamatokkal képes ábrázolni. A megfelelő szerkezet a monitorozási
tervtől függ, ezért azt a tudományos módszert és a relációs adatmodellezést
egyaránt ismerő szakembereknek kell felülvizsgálniuk.


A biodiverzitási adatok más forrásai
------------------------------------

A projektek példányokból, laboratóriumi elemzésekből, akusztikus
rögzítőkből, kameracsapdákból, nyomkövető eszközökből, távérzékelésből,
külső adatbázisokból vagy más automatizált rendszerekből származó adatokat
is kezelhetnek.

Ezekhez a forrásokhoz további entitásokra és metaadatokra lehet szükség,
például:

* példány-, minta- vagy médiaazonosítókra;
* kihelyezési és begyűjtési eseményekre;
* az eszköz azonosítójára és konfigurációjára;
* kalibrálási és feldolgozási információkra;
* laboratóriumi módszerekre és származtatott mérésekre;
* a forrásanyag és a származtatott rekordok közötti kapcsolatokra;
* automatizált azonosítási eredményekre és megbízhatósági értékekre;
  valamint
* a feldolgozáshoz használt szoftver, modell vagy referencia-adatbázis
  verziójára.

Az OpenBioMaps képes ilyen információk tárolására vagy összekapcsolására,
de a projektnek kell meghatároznia a szükséges adatmodellt, fájltárolási
stratégiát, validálási folyamatot és származáskezelési szabályokat.


Az adatgyűjtés ábrázolása az OpenBioMaps rendszerben
===================================================

Egy OpenBioMaps-megvalósításnak meg kell őriznie az adatgyűjtési tervben
meghatározott fogalmakat és kapcsolatokat. Az adatbázis kényelmes
használata nem írhatja felül a mintavételi tevékenység, a megfigyelés, a
taxon, a helyszín, a személy és a feldolgozási lépés közötti tudományos
különbséget.


Táblák és kapcsolatok
---------------------

Egy egyszerű alkalmi adatgyűjtés egyetlen fő megfigyelési táblával is
ábrázolható. A strukturáltabb gyűjtésekhez külön táblákra lehet szükség a
következőkhöz:

* mintavételi helyszínek;
* mintavételi vagy megfigyelési események;
* egyedi szervezetmegfigyelések;
* taxonok vagy taxonfogalmak;
* protokollok;
* megfigyelők és szervezetek;
* példányok, minták vagy médiafájlok;
* eszközök vagy kihelyezések; valamint
* validálási és feldolgozási eredmények.

A kapcsolódó rekordokat állandó azonosítókkal kell összekötni. A
kapcsolatokat nem szabad kizárólag nevekből, koordinátákból vagy
megjelenítési címkékből kikövetkeztetni, mert ezek az értékek
megváltozhatnak, vagy nem feltétlenül egyediek.

A táblák és mezők leírásainak ismertetniük kell az adatok jelentését,
mértékegységét, szókészletét és elvárt tartalmát. Ezek a leírások a
projekt metaadatainak részét képezik, és segítik a felhasználókat a
gyűjtemény értelmezésében és újrafelhasználásában.


Űrlapok és munkafolyamatok
--------------------------

Egy projekt ugyanahhoz a táblához több feltöltési űrlapot is meghatározhat.
Külön űrlapok lehetnek hasznosak a következőkhöz:

* alkalmi megfigyelések;
* strukturált terepi felmérések;
* mintavételi eseményhez tartozó megfigyelések;
* történeti adatkészletek importálása;
* nyilvános vagy közösségi tudományos adatközlések;
* szakértői validálás; valamint
* mobil adatgyűjtés.

Minden űrlapnak csak az adott munkafolyamathoz tartozó mezőket kell
megjelenítenie. A kötelező mezőknek, ellenőrzött listáknak,
alapértelmezett értékeknek, validálási szabályoknak és súgószövegeknek az
adatgyűjtési protokollt kell tükrözniük.

Az űrlapokhoz és mezőkhöz leírásokat kell megadni. Ezek segíthetnek a
felhasználóknak megérteni, milyen adatot kell megadniuk, és a kompatibilis
mobilkliensek számára is hozzáférhetővé tehetők.

.. TODO: Ellenőrizni kell, hogy mely OpenBioMaps-mobilalkalmazások jelenítik
   meg az űrlapok és mezők leírásait, mely leírásmezőket használják, és a
   leírások offline állapotban is elérhetők-e.


Ajánlott alapinformációk
========================

A projekthez szükséges pontos mezők annak céljától függenek, de a legtöbb
megfigyelési gyűjteménynek érdemes figyelembe vennie a következő
kategóriákat.


Taxoninformációk
----------------

A taxonneveket lehetőleg ellenőrzött és dokumentált taxonómiai listából
kell kiválasztani. Az automatikus kiegészítést használó mező segítheti a
felhasználókat az elfogadott tudományos nevek, valamint – megfelelő
konfiguráció esetén – a köznyelvi vagy nemzeti nevek megtalálásában.

A projektnek rögzítenie kell, mely taxonómiai referenciát vagy ellenőrző
listát használja, és lehetőség szerint meg kell őriznie a taxonfogalom
állandó azonosítóját. Ha csak egy névkarakterláncot rögzítenek, az
bizonytalanságot okozhat a nevek változásakor, vagy amikor ugyanazt a nevet
különböző szaktekintélyek eltérően értelmezik.

A projektek engedélyezhetik olyan nevek beküldését, amelyek még nem
szerepelnek az ellenőrzött listában. Ezeket az értékeket egyértelműen meg
kell jelölni későbbi felülvizsgálatra, nem pedig észrevétlenül elfogadott
taxonnévként kezelni. Az automatikus névvalidálás segítheti ezt a
folyamatot, de a bizonytalan egyezéseknek és javításoknak
visszakövethetőnek kell maradniuk.

Az OpenBioMaps-projektek taxonokhoz kapcsolódó szemantikai
oszlopszerepeket, automatikus kiegészítési forrásokat, bővíthető listákat
és háttérben futó validálási feladatokat használhatnak e munkafolyamatok
támogatására.

További információ a `Superspecies <https://gitlab.com/superspecies/>`_
rendszerről.

.. TODO: Ismertetni kell, hogy a „superspecies” egy adott OpenBioMaps
   taxonadatbázis, modul, tábla vagy automatikus kiegészítési szolgáltatás
   jelenlegi neve-e. Ha megvalósításspecifikus kifejezés, a jelenlegi
   hivatalos nevével kell helyettesíteni, és hivatkozni kell a konfigurációs
   dokumentációjára.

.. TODO: Dokumentálni kell az ``auto_species_name`` oszlop vagy beállítás
   jelenlegi célját és konfigurációját. Tisztázni kell, hogy a beküldött
   nevet, egy validált nevet, egy taxonazonosítót vagy az automatikus
   egyeztetési folyamat eredményét tárolja-e.


Megfigyelői és forrásmegjelölési információk
-------------------------------------------

A megfigyelésért felelős személyt vagy szervezetet rögzíteni kell, ha ez
jogilag és etikailag megfelelő. A hitelesített OpenBioMaps-fiók
segítségével a beküldés összekapcsolható a feltöltővel, de a feltöltő nem
feltétlenül azonos a megfigyelővel, az adat rögzítőjével, a meghatározóval,
az adattulajdonossal vagy a jogtulajdonossal.

Ezeket a szerepköröket külön kell tárolni, ha eltérnek egymástól. A
projekteknek azt is meg kell határozniuk, hogyan jelenítik meg, exportálják,
őrzik meg és osztják meg a személyes adatokat.

Egy űrlap automatikusan kitölthet egy mezőt a bejelentkezett felhasználó
fiókjából, csökkentve az ismételt adatrögzítést.

.. TODO: Ellenőrizni kell a feltöltési űrlap ``login_name`` beállításának
   pontos működését. Dokumentálni kell, mely felhasználói attribútumot
   illeszti be, a felhasználó szerkesztheti-e az értéket, valamint hogyan
   kezeli az API-n keresztül vagy hitelesítés nélkül beküldött rekordokat.


Dátum és idő
------------

Egy megfigyelésnek tartalmaznia kell az előfordulás dátumát és – ahol ez
releváns – időpontját. Egy mintavételi eseményhez kezdő és befejező
időpont is szükséges lehet.

A projekteknek meg kell határozniuk:

* kötelező-e az időpont;
* melyik időzónát használják;
* hogyan ábrázolják a bizonytalan, megközelítő vagy hiányos dátumokat;
* a rögzített érték a megfigyelés, a beküldés, az importálás vagy a
  feldolgozás időpontjára vonatkozik-e; valamint
* hogyan validálják az eszközök által megadott vagy fájlokból importált
  időbélyegeket.

A megfigyelés időpontját nem szabad az adatbázisba történő beillesztés
időbélyegével helyettesíteni. Mindkettő hasznos lehet, de eltérő eseményt
írnak le.


Hely és geometria
-----------------

A hely koordinátákkal, OpenBioMaps-geometriamezővel, mintavételihelyszín-
azonosítóval, helynévvel vagy ezek kombinációjával ábrázolható.

Az ``obm_geometry`` mezőt gyakran használják egy rekord térbeli
geometriájának tárolására. A gyűjteménytől függően pontot, vonalat vagy
poligont tartalmazhat. A projektnek a következőket is dokumentálnia kell:

* a koordináta-referenciarendszert – az alapértelmezett a WGS84;
* a hely meghatározásához használt módszert;
* a koordináták bizonytalanságát vagy térbeli pontosságát;
* átalakították vagy általánosították-e a koordinátákat;
* az érzékeny helyszínekre alkalmazott korlátozásokat; valamint
* hogy a geometria a szervezetet, a megfigyelőt, egy útvonalat, a
  mintavételi területet vagy más térbeli fogalmat jelöl-e.

A mobileszközről származó koordinátákat nem szabad automatikusan pontosnak
tekinteni. A pontosság az eszköztől, a környezettől, a helymeghatározási
módszertől és a helyzet rögzítésére rendelkezésre álló időtől függően
változhat.


Mennyiség és észlelés
---------------------

Ahol ez releváns, a gyűjtésnek rögzítenie kell az egyedek számát, a
százalékos borítást, a biomasszát, a jelenlétet, az észlelési állapotot
vagy más meghatározott mennyiséget. Az érték mértékegységének és
értelmezésének egyértelműnek kell lennie.

Nulla érték csak akkor használható, ha a protokoll megállapítja, hogy a
mintavétel megtörtént, de a célt nem észlelték. Nem használható hiányzó
információ helyettesítésére.


Módszer és mintavételi ráfordítás
---------------------------------

A strukturált felméréseknek elegendő információt kell rögzíteniük a
mintavételi tevékenység értelmezéséhez és – ahol lehetséges –
megismétléséhez. Ide tartozhat a protokoll, az időtartam, a távolság, a
terület, a csapdák száma, a megfigyelői ráfordítás, a felszerelés és a
környezeti feltételek.

A módszerre és a ráfordításra vonatkozó információkat a mintavételi
eseményhez kell kapcsolni, ha az adott esemény minden megfigyelésére
érvényesek.


Bizonyíték, validálás és származás
----------------------------------

Fényképek, hangfelvételek, példányok, megjegyzések és más alátámasztó
anyagok segíthetik egy megfigyelés validálását. A projekteknek meg kell
őrizniük a megfigyelés és bizonyítéka közötti kapcsolatot, valamint a
csatolt anyag eredetére és jogaira vonatkozó információkat.

A validálás során nem szabad észrevétlenül felülírni az eredetileg
beküldött információkat. Ahol ez megvalósítható, a projekteknek meg kell
őrizniük:

* a beküldött értéket;
* az elfogadott vagy javított értéket;
* a validáló személyazonosságát vagy szerepkörét;
* a validálás dátumát;
* a validálás állapotát és a megjegyzéseket; valamint
* a döntéshez használt módszert vagy referenciát.

A származás megőrzése érthetővé teszi a javításokat és támogatja a későbbi
újrafelhasználást. Általánosabban a biodiverzitási adatokat úgy kell
kezelni, hogy megtalálhatók, meghatározott feltételek mellett hozzáférhetők,
interoperábilisak és újrafelhasználhatók legyenek [Wilkinson2016]_.


Mezőelnevezés és interoperabilitás
=================================

Az egyértelmű és állandó mezőnevek megkönnyítik a projekt karbantartását.
A mezőneveket leírásokkal kell kiegészíteni, és nem szabad olyan
rövidítésekre hagyatkozni, amelyek jelentését csak az eredeti projektcsapat
ismeri.

Ha az adatokat külső rendszerekkel is megosztják, a projekteknek érdemes
megfontolniuk mezőik megfeleltetését olyan kialakult szókészleteknek, mint
a Darwin Core [Wieczorek2012]_. A Darwin Core által ihletett nevek
használata megkönnyítheti a megfeleltetést, de egy ismert név mezőhöz
rendelése önmagában nem elegendő. A mező jelentésének, mértékegységének,
számosságának, szókészletének és kapcsolatainak is kompatibilisnek kell
lenniük a megfelelő kifejezéssel.

A projektnek nem kell minden adatot közvetlenül adatcsere-formátumban
tárolnia. Használhat az adatgyűjtési munkafolyamatához illeszkedő
szerkezetet, és létrehozhat egy dokumentált exportot vagy átalakítást,
amely megfelelteti rekordjait a szükséges szabványnak.


Gyakorlati ellenőrzőlista
=========================

Az adatgyűjtési űrlap elérhetővé tétele előtt ellenőrizni kell, hogy:

* meghatározták a tudományos célt és a célpopulációt;
* szükség esetén megkülönböztetik az alkalmi megfigyeléseket a strukturált
  mintavételi eseményektől;
* a protokoll által megkövetelt esetekben megőrizhetők az észlelést nem
  tartalmazó befejezett események;
* a taxonok megfelelő ellenőrzött listához vagy felülvizsgálati
  munkafolyamathoz kapcsolódnak;
* nem keverik össze a megfigyelés és a beküldés időbélyegét;
* a geometriák jelentése és koordináta-referenciarendszere meghatározott;
* ábrázolható a térbeli bizonytalanság és az érzékeny helyszínek;
* szükség esetén megkülönböztetik a megfigyelő, a feltöltő, a meghatározó,
  a tulajdonos és a jogtulajdonos szerepkörét;
* dokumentálták a mennyiségeket és mértékegységeket;
* rögzíthetők a mintavételi módszerek és ráfordítások;
* a kötelező mezők és validálási szabályok tükrözik a protokollt;
* az eredeti értékek és az utólagos javítások visszakövethetők maradnak;
* az űrlapok és mezők leírásai érthetők az adatgyűjtők számára;
* felülvizsgálták a hozzáférési szabályokat és a személyes adatokra
  vonatkozó követelményeket;
* minden használni kívánt felületen küldtek be tesztrekordokat; valamint
* az így létrejött rekordok dokumentálatlan ismeretek nélkül
  lekérdezhetők, exportálhatók és értelmezhetők.

A szerkezetet valósághű példákkal kell tesztelni, beleértve a hiányzó
értékeket, a bizonytalan meghatározásokat, a várt területen kívüli
megfigyeléseket, az észlelést nem tartalmazó eseményeket, az egy eseményen
belüli több megfigyelést, valamint az összes támogatott webes, mobil- és
API-kliensből beküldött rekordokat.


Példák adatgyűjtésekre
======================

A kidolgozott példák bemutathatják, hogyan ábrázolhatók a különböző
adatgyűjtési tervek OpenBioMaps-táblákkal és -űrlapokkal.

Lásd: :doc:`Példák OpenBioMaps-adatgyűjtésekre <data_collection_examples>`.


Hivatkozások
============

.. [Isaac2014] Isaac, N. J. B., van Strien, A. J., August, T. A.,
   de Zeeuw, M. P., and Roy, D. B. (2014). Statistics for citizen science:
   extracting signals of change from noisy ecological data. *Methods in
   Ecology and Evolution*, 5(10), 1052–1060.
   https://doi.org/10.1111/2041-210X.12254

.. [MacKenzie2002] MacKenzie, D. I., Nichols, J. D., Lachman, G. B.,
   Droege, S., Royle, J. A., and Langtimm, C. A. (2002). Estimating site
   occupancy rates when detection probabilities are less than one.
   *Ecology*, 83(8), 2248–2255.
   https://doi.org/10.1890/0012-9658(2002)083%5B2248:ESORWD%5D2.0.CO;2

.. [Pereira2013] Pereira, H. M., Ferrier, S., Walters, M., Geller, G. N.,
   Jongman, R. H. G., Scholes, R. J., Bruford, M. W., Brummitt, N.,
   Butchart, S. H. M., Cardoso, A. C., Coops, N. C., Dulloo, E.,
   Faith, D. P., Freyhof, J., Gregory, R. D., Heip, C., Höft, R.,
   Hurtt, G., Jetz, W., Karp, D. S., McGeoch, M. A., Obura, D.,
   Onoda, Y., Pettorelli, N., Reyers, B., Sayre, R., Scharlemann,
   J. P. W., Stuart, S. N., Turak, E., Walpole, M., and Wegmann, M.
   (2013). Essential Biodiversity Variables. *Science*, 339(6117),
   277–278. https://doi.org/10.1126/science.1229931

.. [Wieczorek2012] Wieczorek, J., Bloom, D., Guralnick, R., Blum, S.,
   Döring, M., Giovanni, R., Robertson, T., and Vieglais, D. (2012).
   Darwin Core: An evolving community-developed biodiversity data standard.
   *PLOS ONE*, 7(1), e29715.
   https://doi.org/10.1371/journal.pone.0029715

.. [Wilkinson2016] Wilkinson, M. D., Dumontier, M., Aalbersberg, I. J.,
   Appleton, G., Axton, M., Baak, A., Blomberg, N., Boiten, J.-W.,
   da Silva Santos, L. B., Bourne, P. E., Bouwman, J., Brookes, A. J.,
   Clark, T., Crosas, M., Dillo, I., Dumon, O., Edmunds, S., Evelo,
   C. T., Finkers, R., Gonzalez-Beltran, A., Gray, A. J. G.,
   Groth, P., Goble, C., Grethe, J. S., Heringa, J.,
   't Hoen, P. A. C., Hooft, R., Kuhn, T., Kok, R., Kok, J.,
   Lusher, S. J., Martone, M. E., Mons, A., Packer, A. L.,
   Persson, B., Rocca-Serra, P., Roos, M., van Schaik, R.,
   Sansone, S.-A., Schultes, E., Sengstag, T., Slater, T.,
   Strawn, G., Swertz, M. A., Thompson, M., van der Lei, J.,
   van Mulligen, E., Velterop, J., Waagmeester, A., Wittenburg, P.,
   Wolstencroft, K., Zhao, J., and Mons, B. (2016). The FAIR Guiding
   Principles for scientific data management and stewardship.
   *Scientific Data*, 3, 160018.
   https://doi.org/10.1038/sdata.2016.18
