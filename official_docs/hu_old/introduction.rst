Bevezetés
*********

Az OpenBioMaps projektnek céljai
================================
* A biodiverzitással kapcsolatos adatok kezelésének támogatása azért, hogy azok hatékonyabban legyenk használhatók a természet megőrzésének céljából
* Ingyenes és szabadon hozzáférhető biológiai, térképi adatbázis szolgáltatás fenntartása
* Nyílt forráskódú és szabadon felhasználható biodiverzitási adatkezelő szoftveres eszközök fejlesztése
* A biodiverzitással kapcsolatos oktatás és kutatás támogatása


Az OpenBioMaps fontos tulajdonságai
===================================
* Az OpenBioMaps minden szolgáltatása ingyenesen vehető igénybe.
* Az OpenBioMaps célja élő szervezetekre vonatkozó (természetvédelmi jelentőségű vagy biodiverzitás kutatásban használható) előfordulási és az ahhoz kapcsolódó adatok (biotikai adatok) nyilvántartása.
* Az OpenBioMaps kifejezett célja a felsőfokú oktatás támogatása és a kutatás és természetvédelem kapcsolatának erősítése.
* Az OpenBioMaps nyílt forráskódú alkalmazásokra támaszkodó, decentralizált, minimalizált költségigényű, központi ellenőrzés nélküli részadatbázisokból álló adatbázis és keretrendszer.
* Az OpenBioMaps elsődleges célközönsége a természettudományos és természetvédelmi szakma, valamint a környezetügyet is érintő tervek, stratégiák, döntések előkészítői.
* Tetszőleges struktúrájú és szabályozású adatbázisok létrehozása és kezelése a felhasználók által.
* Egyszerű adat feltöltés különböző fájl formátumokból (ods, xls, xlsx, gpx, shp, csv ...).
* Ismételhető és idézhető lekérdezések.
* Tartós azonosítok használata (DOI) adatbázisokhoz és lekérdezésekhez is.
* Az adatok kölönböző formátumokban letölthetőek (shp, csv, gpx, json, ...)
* Az adatok elérhetőek távoli adatbázisokból vagy asztali alkalmazásokból is (pl.: R, QGIS).
* Integrálható szolgáltatások.
* Adatkapcsolatok más adatbázisokkal.
* Személyre szabható adat feltöltő felületek létrehozása.
* Terepi mobil adatgyűjtő alkalmazás.
* Közösségi szerkesztésű dokumentáció.
* Bármilyen nyelvre fordítható felület (jelenleg Magyar, Angol, Román, Spanyol, Portugál és részben Orosz, Német, Horvát, Francia, Cseh, Lengyel és Görög nyelvekre van fordítás). A fordításokhoz bárki hozzájárulhat a https://translate.openbiomaps.org weblate felületen keresztül
* Közösségi visszajelzéseken alapuló fejlesztés.

Adatkezelési szabályzat
=======================
Az OpenBioMaps megalkotói, úgy mint a szoftverek fejlesztői és az OpenBioMaps közösségi szolgáltatások fenntartói (lényegében az OpenBioMaps Konzorcium tagjai) az adatok kezelését nem szabályozza. A fejlesztők és a közössgéi szolgáltatások fenntartói nem gyűjtenek adatokat a felhasználókról és nem gyűjtik az OpenBioMapssal szoftvereket gyűjtőtt adatokat sem. Nem tartanak fenn semmilyen jogot a gyűjtött adatokkal kapcsolatban. Minden egyes OpenBioMaps szerver példány valamilyen intézmény fenntartásában létezik és így annak az intézménynek a szabályai vonatkoznak rá elsősorban. Mindazonáltal irányadó adatkezelési stratégiákat megfogalmaztunk, amelyet egyéb rendelkezések hiányában bárki alkalmazhat.

* Az egyes szervereken működő projektek egymástől függetlenül szabályozhatóak. A projekt alapítója (magánszemély, vagy jogi személy) a szabályok létrehozója egyúttal.
* A projekt gazdák a projekt létrehozói, vagy az általuk ezzel a feldattal megbízott szakemberek.
* A felhasználók, minden személy, vagy intézmény aki az OpenBioMaps szolgáltatásokat használja.
* A gyűjtött adatok az adatgyűjtők elidegeníthetetlen szellemi tulajdonát képzik, de a projektet létrehozó személynek vagy intézménynek az általa meghatározott felhasználási joga van hozzá. 
* A felhasználók csak a személyes adataikról rendelkezhetnek, a projektben gyűjtött adatok kezelésének megszüntetését nem kérhetik a projekt tulajdonostól. 
* A projekt-ben gyűjtött adatok közzététele a projekt egyéni szabályozása szerint történhet, amelyhez az OBM szerver szoftver eszközöket biztosít. Egy projekt lehet teljesen zárt és teljesen nyitott is, azaz az adatok hozzáférehtősége lehet teljesen kolátozott (még az adatgyűjtő sem fér többé hozzá) és teljesen nyitott is (amikor bárki hozzáfér az adatokhoz és akár módosíthatja is azokat).
* Az OpenBioMaps megfelelő beállítása amely a gyűjtött adatok és személyes adatok kezelésére is vonatkozik a projekt gazdák felelőssége.  Az OpenBioMaps fejlesztői és az OpenBioMaps közösségi szolgáltatások fenntartói nem vállalnak felelősséget a szervereken kezelt adatokért.

OpenBioMaps folyamatok
======================
Az OBM megpróbál támogatást adni a teljes adat életútra, az adatgyűjtéstől a rendszerezésen át a felhasználásig.

.. figure:: images/adat_eletut_infog.png
   :scale: 50 %
   :alt: OpenBioMaps adat életút infógrafika

:doc:`OBM Workflow <../obm_workflow>`

:download:`Lekérdezési séma (pdf) <docs/query_scheme.pdf>` :download:`Lekérdezési séma (odp) <docs/query_scheme.odp>`

Első lépések
============
A saját adatbázis létrehozásához szüksége lesz egy szerverre. Ez lehet saját szerver, bérelt szerver, vagy egy olyan szerver, amelyet valaki más már karbantart az OpenBioMaps kiszolgálására.

A legegyszerűbb egy új adatbázist egy meglévő OpenBioMaps szerveren létrehozni. Nézze meg az ismert szerverek listáját, hogy van-e hozzáférése valamelyikhez. Vannak dedikált nyilvános szerverek, amelyek számos különböző adatbázisnak adnak otthont.

Ha nagyobb kapacitásra van szüksége, vagy szeretné ellenőrizni a hozzáférést a teljes szerverhez, telepíthet dedikált szervert. Ez nem olyan bonyolult. Itt van egy útmutató: https://openbiomaps.org/documents/hu/server_install.html

Ha saját adatbázis-projektet szeretne létrehozni egy meglévő szerveren, akkor hozzáféréssel kell rendelkeznie az adott szerveren lévő adatbázishoz. Ha ez megvan, akkor ott könnyedén létrehozhatja a saját adatbázis-projektjét, amelynek lépéseit itt találja: https://openbiomaps.org/documents/hu/tutorials.html#new-project és
itt: https://openbiomaps.org/documents/hu/new_project.html


OpenBioMaps Konzorcium
======================
Az OpenBioMaps közösség a szoftverek fejlesztésének irányítására és az ingyenes szolgáltatások fenntartására egy konzorciumot hozott létre. A konzorciumi tagság feltétele a a fejlesztéshez, vagy a szolgáltatások fenntartásához történő szignifikáns hozzájárulás.

Az első OpenBioMaps konzorciumot közintézmények és civil szervezetek hozták létre 2015 szeptember elsején.

Jelenlegi OpenBioMaps partnerek:

Debreceni Egyetem

kapcsolat: Dr. Bán Miklós

Duna-Ipoly Nemzeti Park Igazgatóság

kapcsolat: Baranyai Zsolt

Eötvös Loránd Tudományegyetem

kapcsolat: Ritter Dávid

WWF Magyarország

kapcsolat: Sipos Katalin

Eszterházy Károly Egyetem

kapcsolat: Dr. Pénzesné Kónya Erika

Milvus Csoport Egyesület

kapcsolat: Papp Edgár

Duna-Dráva Nemzeti Park Igazgatóság

kapcsolat: Gáborik Ákos

Fertő-Hanság Nemzeti Park Igazgatóság

kapcsolat: Takács Gábor

:download:`OpenBioMaps Konzorcium Szerződés<docs/consortium_2015.pdf>`


Kapcsolat a konzorciummal:

management@lists.openbiomaps.org
