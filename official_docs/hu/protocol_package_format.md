# Protokollcsomag-formátum, 1. verzió

Ez a dokumentum határozza meg a protokolltelepítő első csomagformátumának
követelményeit. A csomag deklaratív YAML: a projekt tábláit, oszlopait, listáit
és űrlapjait írja le. Nem tartalmaz végrehajtható kódot vagy SQL-t.

A [terepi megfigyelési példa](https://gitlab.com/openbiomaps/share-your-protocol/-/blob/main/minimal/protocol.yml)
és a [PDS-csomag](https://gitlab.com/openbiomaps/share-your-protocol/-/blob/main/pds-mobile-test/protocol.yml)
a protokolltároló közzétehető csomagjai. A telepítő az ilyen formátumú
csomagokat a beállított GitLab-katalógusból olvassa.

## Csomagfájlok és verziókezelés

A GitLab-katalógus egy `catalog.yml` fájl a tároló beállított útvonalán.
Minden katalógusbejegyzés azonosít egy protokollt, és a tárolóhoz képest
relatív útvonallal hivatkozik annak YAML-csomagjára. A csomag megadja a
következőket:

- `format_version`: a fájlformátum egész számmal jelölt verziója;
- `protocol_id`: stabil, fordított DNS-jelölésű azonosító, amely a kiadások
  között változatlan marad, például `org.openbiomaps.pds-mobile-test`;
- `protocol_version`: a protokoll kiadása, a formátumtól függetlenül.

A katalógus megismétli a protokoll azonosítóját és verzióját, így a kliensek
az összes csomag betöltése nélkül listázhatják őket. A csomag értékeinek
egyezniük kell a katalógusbejegyzéssel. A tároló commitja pontosan azonosítja
a közzétett katalógus és csomag tartalmát; a csomag útvonala nem léphet ki a
tárolóból.

Az első specifikáció az `1` formátumverziót használja. A beolvasónak el kell
utasítania a nem támogatott formátumverziót és az ismeretlen tulajdonságokat;
nem hagyhatja figyelmen kívül észrevétlenül a beállításokat. A protokollverziók
függetlenek a formátumverziótól. A telepítő támogatja a bővítő frissítéseket;
a meglévő definíciók módosítása kézi felülvizsgálatot igényel.

A telepítő a szerver `/etc/openbiomaps/system_vars.php.inc` fájljában
beállított nyilvános GitLab-projektet olvassa. A
`PROTOCOL_INSTALLER_GITLAB_PROJECT` értékét a GitLab-projekt útvonalaként
(`group/project`) adja meg. Az opcionális `PROTOCOL_INSTALLER_GITLAB_REF`
konstans választja ki az ágat (alapértéke `main`), a
`PROTOCOL_INSTALLER_GITLAB_CATALOGUE_PATH` pedig a tárolóhoz képest relatív
katalógusfájlt (alapértéke `catalog.yml`). Ez az első verzió nem használ
tokent, és nem támogat privát tárolókat.

```php
define('PROTOCOL_INSTALLER_GITLAB_PROJECT', 'openbiomaps/share-your-protocol');
define('PROTOCOL_INSTALLER_GITLAB_REF', 'main');
define('PROTOCOL_INSTALLER_GITLAB_CATALOGUE_PATH', 'catalog.yml');
```

## Azonosítók és nevek

A táblák, oszlopok, űrlapok és listák stabil, csomagon belüli azonosítókkal
rendelkeznek. A hivatkozások ezeket használják, soha nem a javasolt
adatbázisneveket. Az azonosítók kisbetűket, számjegyeket és aláhúzásjeleket
tartalmazhatnak, betűvel kezdődnek, és az adott elemtípuson belül egyediek.
A `suggested_name` az újonnan létrehozott objektumok ember számára olvasható
helyi neve; ez javaslat, amely módosítható, illetve az objektum egy kompatibilis
meglévő objektumhoz rendelhető. A csomagok nem adhatnak meg adatbázist, sémát,
projekttáblanevet vagy adatbázis-tulajdonost.

Minden tábla megad egy `target` értéket:

- `project_main`: a projekt meglévő főtáblája, amely bővíthető;
- `create`: új adattábla, amelyet az adminisztrátor kompatibilis meglévő
  táblához rendelhet, vagy létrehozhat.

A formátum nem engedi tetszőleges fizikai cél megadását a csomagban.
A rendszer által kezelt OBM-oszlopokat és a táblák működéséhez szükséges
infrastruktúrát a telepítő biztosítja; ezeket nem szabad protokolloszlopként
megismételni. Az űrlapok a fenntartott `system.geometry` és `system.files`
oszlopazonosítókkal hivatkozhatnak a szabványos geometria- és mellékletmezőkre.
Ezek nem a csomag által definiált oszlopok, és a csomagban nem nevezhetők át.

## Táblák és oszlopok

Minden oszlopnak van stabil `id` azonosítója, `suggested_name` neve és
hordozható `data_type` adattípusa, valamint opcionálisan `description` és
`required` metaadata. Az 1. verzió adattípusai: `text`, `varchar`, `integer`,
`decimal`, `boolean`, `date`, `time`, `datetime`, `interval` és `text_array`.
A típusok a tárolt értékeket írják le, nem az űrlap vezérlőelemeit. A geometria
és a mellékletek a fent leírt fenntartott rendszeroszlopokat használják.
Nyers SQL-típus közvetlen megadására nincs lehetőség.

A `varchar` pozitív egész számú `max_length` értéket igényel, és
`varchar(max_length)` oszlopot hoz létre. Például:

```yaml
- id: species
  suggested_name: species
  data_type: varchar
  max_length: 255
```

A csomag `varchar(n)` oszlopa használhat meglévő `varchar(m)` oszlopot, ha
`m >= n`, illetve korlátlan hosszúságú `varchar` vagy `text` oszlopot.
A csomag korlátlan `text` oszlopa nem használhat korlátozott `varchar(n)`
oszlopot: a cél elutasíthatná a későbbi, `n` karakternél hosszabb értékeket.
Meglévő, korlátozott hosszúságú fajnévoszlop használatához tegyen közzé olyan
protokollverziót, amely `varchar` típust és megfelelő `max_length` értéket
ad meg.

Az oszlopnevek javaslatok, nem azonosítók. A telepítő a kiválasztott meglévő
oszlopokat a típus és kapacitás kompatibilitása alapján hasonlítja össze.
Nem alakíthatja át automatikusan az adatokat, és nem módosíthatja a meglévő
oszlopdefiníciókat.

## Listák

Minden listának van stabil `id` azonosítója és az alábbi `kind` értékek egyike:

- `fixed`: a csomaghoz tartozó, rendezett `{code, label}` értékek. Az űrlap a
  `code` értéket tárolja; a `label` a megjelenített szöveg. A `multiselect`
  opcionális, alapértéke hamis.
- `project`: hely egy projektspecifikus listának. Az adminisztrátor
  telepítéskor adja meg vagy választja ki a helyi forrást; a csomag adhat
  útmutatást, de nem követelhet meg egy adott helyi listát.
- `table`: a csomag egy másik táblájából olvasott lista. A `table`,
  `value_column` és `label_column` stabil logikai hivatkozások a csomag
  azonosítóira, nem SQL-nevek.

A táblából olvasott lista tartalmazhat `filter_column` és `filter_value`
értékeket, amelyeknek egy deklarált oszlopra, illetve egy skalárértékre kell
hivatkozniuk. Ez SQL beágyazása nélkül támogatja a szűrt választási
lehetőségeket. Az űrlapmező a lista stabil azonosítójával hivatkozik rá.
A listák megőrzik a kódokat és címkéket, amikor az adminisztrátor egyenértékű
helyi forrást választ.

## Űrlapok és mezők

Minden űrlap megad egy stabil `id` azonosítót, egy `suggested_name` nevet,
egy `mode` értéket (`web` vagy `api`), egy céltábla-azonosítót, opcionális
leírást, beállításokat és rendezett mezőket. Az 1. verzió beállításai:
`observationlist_mode` (`false`, `true` vagy `force`), `observationlist_time`
(nemnegatív egész számú perc) és `tracklog_mode` (`false`, `force` vagy üres
karakterlánc). A kihagyott beállítások az alkalmazás alapértékét használják.

Minden mező egy deklarált oszlopazonosítóra vagy fenntartott rendszeroszlop
azonosítójára hivatkozik, és megadja a felületi `type` típusát. Az 1. verzió
felületi típusai: `text`, `textarea`, `numeric`, `boolean`, `date`, `time`,
`datetime`, `timetominutes`, `tinterval`, `array`, `list`, `autocomplete`,
`autocompletelist`, `point`, `line`, `polygon`, `wkt` és `file_id`. Opcionális
tulajdonságok: `required` (logikai érték), `default` (skalár vagy null),
`api_params` (támogatott alkalmazásparaméter-karakterláncok listája) és `list`
(listaazonosító). A `list` tulajdonság kötelező a `list`, `autocomplete` és
`autocompletelist` típusoknál; más mezőtípusoknál érvénytelen. Az alapértékek
literális értékek, kivéve a jelenleg támogatott, alkalmazás által feloldott
`_email`, `_login_name` és `_login_email` alapértékeket. Más speciális értékek
csak akkor használhatók a csomagokban, ha a telepítő kifejezetten támogatja
őket.

Az 1. verzió mező- és tárolási típusainak kompatibilitása:

| Űrlapmező típusa | Kompatibilis oszlop |
| --- | --- |
| `text`, `textarea`, `list`, `autocomplete`, `autocompletelist` | `text` vagy `varchar` |
| `numeric` | `integer` vagy `decimal` |
| `boolean` | `boolean` |
| `date` | `date` |
| `time` | `time` |
| `datetime` | `datetime` |
| `timetominutes` | `integer` |
| `tinterval` | `interval` |
| `array` | `text_array` |
| `point`, `line`, `polygon`, `wkt` | `system.geometry` |
| `file_id` | `system.files` |

A feldolgozónak el kell utasítania az ismétlődő azonosítókat, az ismeretlen
tulajdonságokat és felsorolt értékkészleteken kívüli értékeket, a nem deklarált
hivatkozásokat, az inkompatibilis mező–oszlop párokat, az érvénytelen
listaforrásokat és űrlapbeállításokat. Az ellenőrzésnek minden adatbázisírást
meg kell előznie. A kereszthivatkozások és a kompatibilitás ellenőrzése a
YAML/séma feldolgozását kiegészítő szemantikai ellenőrzés.

## A katalógus szerkezete

A katalógus `catalogue_format_version: 1` értéket és egy `protocols` listát
tartalmaz. Minden bejegyzés tartalmazza a `protocol_id`, `protocol_version`,
`title`, `description` és `package` mezőket. A `package` a csomag YAML-fájljának
a tárolóhoz képest relatív útvonala. A bejegyzések a
`(protocol_id, protocol_version)` pár alapján egyediek.

Lásd a [közzétett katalógust](https://gitlab.com/openbiomaps/share-your-protocol/-/blob/main/catalog.yml)
és a :ref:`csomagkészítőknek és adminisztrátoroknak szóló útmutatót <protocol-installer-guide>`.
