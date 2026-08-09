:author: Miklós Bán
:date: 2026-08-07

.. observation-events:

Megfigyelési események
......................

Fogalomtár: megfigyelési esemény és megfigyelés

A nemzetközi adatmegosztási szabványokkal (Darwin Core / GBIF) összhangban
az OpenBioMaps adatstruktúrája két különálló szintre osztja a terepi
adatgyűjtést: **megfigyelési eseményre** és **megfigyelésre**. Ez a
felosztás biztosítja, hogy mind a strukturált felmérések, mind az alkalmi
megfigyelések pontosan rögzíthetők legyenek.

1. Megfigyelési esemény

A **megfigyelési esemény** egy előre meghatározott térbeli és időbeli
környezet, amely egy adott adatgyűjtési vagy mintavételi tevékenységet
ábrázol.

 **- Lényeges elem:** Maga az esemény a terepi tevékenység, vagyis a
 mintavétel, nem pedig a megtalált szervezet.

**Fő jellemzők:**

Mindig rendelkezik **rögzített helyszínnel** – koordinátákkal vagy állandó
ponttal –, valamint **időponttal** vagy időintervallummal.

Gyakran meghatározott módszertanhoz vagy protokollhoz kapcsolódik, például
ötperces pontszámláláshoz vagy csapdázáshoz.

**A „nulla megfigyelés” (hiány) kezelése:** A megfigyelési esemény akkor is
létrejön és érvényes marad a rendszerben, ha a kutató a felmérés során
egyetlen fajt sem figyelt meg.

 - Ez a „negatív adat” alapvető fontosságú a tudományos elemzésekhez és a
   mintavételi ráfordítás dokumentálásához.

**Hierarchia:** Egy megfigyelési esemény **nulla, egy vagy több** egyedi
megfigyelést tartalmazhat. Az esemény során rögzített megfigyelések közös
azonosítóval rendelkeznek: ``observation_list_id``.

2. Megfigyelés

A **megfigyelés** egy adott taxon – faj, nemzetség stb. – egyedi terepi
észlelését vagy rögzítését jelenti.

 - Lényege: Maga a biológiai adat, vagyis a szervezet jelenlétének
   bizonyítéka.

**Fő jellemzők:**

Tartalmazza a **taxon nevét** – például a faj nevét –, valamint a megszámolt
vagy becsült **egyedszámot**, illetve más mennyiségi mutatót. Mindig
tartalmaz helyszínt, dátumot és időpontot.

**Típusai a rendszerben:**

 **- Eseményhez kapcsolódó megfigyelés:** Strukturált felmérés, vagyis
 megfigyelési esemény részeként rögzített fajadat. Ebben az esetben a
 helyszín- és időadatokat a megfigyelés az eseménytől örökli, vagy az
 eseményen belül adják meg.
 **- Alkalmi megfigyelés:** Olyan egyedi észlelés, amely nem része előre
 megtervezett protokollnak vagy felmérésnek, hanem eseti jelleggel,
 közvetlenül rögzítik, például egy út közben megfigyelt ritka madár
 esetében.

Összefoglaló táblázat fejlesztők és felhasználók számára

+-----------------------------+--------------------------------------------+-----------------------------------------+
| Jellemző                    | Megfigyelés                                | Eseményhez kapcsolódó megfigyelés       |
+=============================+============================================+=========================================+
| **Mit ábrázol?**            | A terepi munka vagy mintavétel környezetét.| Egy adott szervezet észlelését.         |
+-----------------------------+--------------------------------------------+-----------------------------------------+
| **Maradhat üres?**          | **Igen.** Ha a protokoll szerint semmit    | **Nem.** Mindig tartalmaznia kell a     |
|                             | sem találtak, az esemény akkor is létezik. | fajt és az egyedek számát.              |
+-----------------------------+--------------------------------------------+-----------------------------------------+
| **Mennyiségi mutató**       | A mintavételi ráfordítás, például az       | Egyedszám, borítás vagy darabszám.      |
|                             | időtartam vagy a terület nagysága.         |                                         |
+-----------------------------+--------------------------------------------+-----------------------------------------+
| **GBIF / DwC megfelelő**    | Esemény / mintavételi esemény adatai       | Előfordulás / előfordulási adatok       |
+-----------------------------+--------------------------------------------+-----------------------------------------+
