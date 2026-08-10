# Modulok

A modulok az OpenBioMaps webalkalmazás konfigurálható bővítményei. Hozzáadhatnak felhasználói felületi elemeket, adatfeldolgozási funkciókat, exportformátumokat, adminisztrációs eszközöket, API-kat vagy külső szolgáltatásokkal való integrációkat.

A moduloknak két fő hatóköre van:

- A **projektszintű modulok** a teljes projektre vonatkozó funkciókat biztosítanak, például térbeli alakzatok kezelését, csatolmányok támogatását vagy PostgreSQL-felhasználók létrehozását.
- A **táblaszintű modulok** egy adott adattáblára vonatkoznak, például a térképoldal szűrőire, az eredmények megjelenítésére, adatátalakításokra vagy exportformátumokra.

A modulok az alkalmazás hookjaihoz kapcsolódnak. A legtöbb felhasználói hook a térképoldalon és a profiloldalon található, de a modulok adminisztrációs oldalakat, API-kat, háttérfeladatokat és feltöltéshez kapcsolódó funkciókat is hozzáadhatnak.

A legtöbb modul JSON formátumú paramétereket fogad. Egyes modulok ehelyett külön adminisztrációs felületet biztosítanak, mások pedig JSON-paramétereket és további adatbázis- vagy MapServer-konfigurációt egyaránt igényelnek.

> **Verziókompatibilitás:** Az elérhető modulok és paramétereik változhatnak az OpenBioMaps kiadásai között. A telepített alkalmazás moduladminisztrációs oldala tartalmazza a projekt számára elérhető modulok irányadó listáját. Mielőtt egy másik telepítésből konfigurációt másolna át, ellenőrizze a modul forrását és a kiadási megjegyzéseket.

## Moduladminisztráció

A modulok a **Projektadminisztráció → Modulok** oldalon engedélyezhetők és konfigurálhatók.

Egy modul általában:

- hozzáadható a projekthez;
- felhasználókhoz vagy csoportokhoz rendelhető;
- JSON-paraméterekkel konfigurálható;
- engedélyezhető vagy letiltható; valamint
- megnyitható egy modulspecifikus adminisztrációs oldalon, ha van ilyen.

A modulnevek és a JSON-kulcsok megkülönböztetik a kis- és nagybetűket. Mentés előtt ellenőrizze a JSON érvényességét. A JSON nem engedélyez megjegyzéseket vagy záró vesszőket.

### Egyéni modul hozzáadása

Egyéni modulok tölthetők fel és adhatók hozzá a projekthez. A fejlesztőknek a `resources/includes/modules/examples/` könyvtárban található példamodulokat kell kiindulási alapként használniuk, és össze kell hasonlítaniuk azok megvalósítását a telepített OpenBioMaps-kiadásban szereplő modulokkal.

Az egyéni modulok kódját üzembe helyezés előtt felül kell vizsgálni. A modul az alkalmazás részeként fut, és hozzáférhet a projekt adataihoz, a hitelesített felhasználó munkamenetéhez és az adatbázis-kapcsolatokhoz.

### Modul-hozzáférés

Ugyanaz a modul többször is hozzáadható eltérő hozzáférési beállításokkal vagy paraméterekkel. Ez lehetővé teszi az adminisztrátorok számára, hogy különböző konfigurációkat biztosítsanak különböző felhasználókhoz, csoportokhoz vagy táblákhoz.

Például:

- az `allowed_columns` különböző oszlopokat tehet elérhetővé különböző csoportok számára; és
- a `text_filter` táblaspecifikus szűrőoszlopokat biztosíthat egy több adattáblát tartalmazó projektben.

Az **Access** oszlop határozza meg egy modulpéldány általános célközönségét. Az elérhető lehetőségek közé tartozik a nyilvános hozzáférés és a bejelentkezett felhasználókra korlátozott hozzáférés.

A **Group access** oszlop tovább korlátozza a modulpéldányt a kiválasztott projektcsoportokra vagy egyéni felhasználókra.

Ha ugyanannak a modulnak több példánya is vonatkozik egy felhasználóra, tesztelje, hogy a telepített OpenBioMaps-verzió melyik konfigurációt választja ki, illetve mely konfigurációkat egyesíti. Kerülje az egymást átfedő hozzáférési szabályokat, hacsak nem ismert a működésük.

### Modulok engedélyezése és letiltása

Minden konfigurált modulpéldány engedélyezhető vagy letiltható. Egy modul letiltása megőrzi annak konfigurációját, de megakadályozza a használatát.

Egy modul állapotának módosítása után tesztelje az érintett oldalt minden érintett hozzáférési csoport felhasználóival. Egyes modulok adatbázis-objektumokat is létrehoznak, vagy letiltásuk után is megőrzik modulspecifikus beállításaikat.

### Modulok eltávolítása

A moduladminisztrációs felület jelenleg nem biztosít általános lehetőséget egy telepített modul alkalmazásból való eltávolítására.

Egy konfigurált modulpéldány letiltható. Ne törölje kézzel a modul fájljait vagy adatbázis-objektumait, kivéve, ha ismert a modul eltávolítási eljárása, és rendelkezésre áll biztonsági mentés.

### Modulparaméterek

A legtöbb modul közvetlenül a moduladminisztrációs oldalon fogad JSON-paramétereket. Más modulok külön adminisztrációs lapot biztosítanak a modulspecifikus feladatokhoz. A `box_load_selection` példa egy saját adminisztrációs felülettel rendelkező modulra.

A dokumentumban szereplő példák olyan helyőrzőket használnak, mint a `YOURTABLE`, a `column_name` és a `schema.table`. Cserélje le ezeket a helyőrzőket a projekt azonosítóira.

## Projektszintű modulok

### `box_load_selection`

A `box_load_selection` modul újrafelhasználható térbeli alakzatokat kezel.

A következő funkciókat biztosítja:

- A felhasználók pontokat, vonalakat és poligonokat tölthetnek fel. Az ESRI Shapefile általánosan használt formátum, de más szabványos térbeli formátumok is támogatottak lehetnek.
- A feltöltött alakzatok felhasználhatók egy adatlekérdezés térbeli kiterjedésének meghatározására.
- Egy alakzat megadhatja egy rekord geometriáját webes vagy fájlból történő feltöltés során.
- Az alakzatok megoszthatók más felhasználókkal.
- A felhasználó számára elérhető alakzatokat a mobilalkalmazás letöltheti és megjelenítheti.

Az újonnan feltöltött alakzatok alapértelmezés szerint nem láthatók más felhasználók számára. A projektadminisztrátorok minden alakzat esetében jogosultságot adhatnak a felhasználóknak annak lekérdezésekhez vagy adatfeltöltésekhez való használatára.

A felhasználók a profiloldaluk **Megosztott geometriák** modulblokkjában kezelhetik a megosztott alakzatokat. A projektadminisztrátorok a `box_load_selection` adminisztrációs lapján kezelhetik ezeket a jogosultságokat.

A modul engedélyezésekor egy **Térbeli lekérdezés** mező jelenik meg a térképoldalon. A felhasználók kiválaszthatnak egy elérhető alakzatot, és térbeli lekérdezést futtathatnak rajta. Poligongeometriák esetén a felület lehetővé teheti annak kiválasztását, hogy a poligon határát metsző rekordok szerepeljenek-e a lekérdezésben.

Ha egy feltöltési űrlap `obm_geometry` mezőt használ, annak térképvezérlője felkínálhatja a **Geometria listából** lehetőséget. Egy elnevezett alakzat kiválasztása beilleszti annak WKT-geometriáját a feltöltési mezőbe.

A mobilalkalmazás a feltöltéshez elérhető alakzatokat félig átlátszóan, a nevükkel feliratozva jelenítheti meg az űrlapok térképein.

**Paraméterek:** Nincsenek. A modul a saját adminisztrációs felületét használja.

### `photos`

A `photos` modul engedélyezi a fénykép- és egyéb csatolmán mezőket a feltöltési űrlapokon, és megjeleníti a csatolt képeket a rekordok adatlapjain.

A fájlméretkorlátokat, az engedélyezett fájltípusokat, a tárolást, a hozzáférés-vezérlést és a biztonsági mentési követelményeket az alkalmazás és a kiszolgáló szintjén is konfigurálni kell.

**Paraméterek:** Nincsenek.

### `create_pg_user`

A `create_pg_user` modul lehetővé teszi a jogosult felhasználók számára személyes PostgreSQL-fiókok létrehozását.

A modul engedélyezésekor:

- egy **PostgreSQL-felhasználó létrehozása** mező jelenik meg a jogosult felhasználók profiloldalán;
- a felhasználók létrehozhatják és megújíthatják saját adatbázis-fiókjukat;
- a létrehozott fiók hozzá lesz rendelve a projekt PostgreSQL-felhasználói csoportjához; valamint
- a fiók adatbázis-kliensekkel, például QGIS-szel használható.

Alapértelmezés szerint a létrehozott fiók:

- olvasási hozzáféréssel rendelkezik a projekt adatbázistábláihoz;
- egyidejűleg egy klienskapcsolatra korlátozott; és
- egy év után lejár.

A létrehozott fiók hozzá lesz adva a projektről elnevezett PostgreSQL-csoporthoz, amelynek formája általában `PROJECT_user`. Egy adatbázis-adminisztrátor további jogosultságokat adhat, például írási hozzáférést bizonyos táblákhoz, de a legkisebb jogosultság elvét kell követnie.

A felhasználók a lejárat előtt vagy után megújíthatják hozzáférésüket, a telepített modul szabályainak megfelelően.

A következő képernyőkép egy példa PostgreSQL/PostGIS-kapcsolatot mutat be QGIS-ben:

![OpenBioMaps PostGIS-kapcsolat hozzáadása QGIS-ben](images/qgis_connect.jpg)

Ne tegye elérhetővé a PostgreSQL-t a nyilvános interneten megfelelő tűzfal-, TLS-, hitelesítési és hozzáférés-vezérlési beállítások nélkül.

**Paraméterek:** Nincsenek. A jelenlegi kiadások külön adminisztrációs oldalt biztosíthatnak.

### `computation`

A `computation` modul projektspecifikus számítási funkciókat biztosít.

Pontos működése a telepített modulverziótól és a projekt konfigurációjától függ. Éles projektben való engedélyezés előtt vizsgálja felül a modul megvalósítását.

**Paraméterek:** Nincsenek dokumentálva.

### `custom_filetype`

A `custom_filetype` modul támogatja projektspecifikus egyéni letöltési formátumok, például Observado-stílusú CSV-fájlok előállítását.

A kimeneti formátum és minden szükséges egyéni megvalósítás a projekttől függ.

**Paraméterek:** Nincsenek dokumentálva.

### `taxon_meta`

A `taxon_meta` modul taxonokkal kapcsolatos metaadat-funkciókat biztosít.

Felhasználói felületét, szükséges adatbázis-struktúráját és konfigurációját a telepített modulverzió alapján kell ellenőrizni.

**Paraméterek:** Nincsenek dokumentálva.

## Táblaszintű modulok

### `additional_columns`

Az `additional_columns` modul több adattáblában található rekordok összekapcsolásához használt oszlopokat határoz meg.

Ha a táblák közös azonosítóval kapcsolódnak egymáshoz, a lekérdezések az adott azonosítóhoz tartozó kapcsolódó rekordokat is tartalmazhatják. A felhasználók a térképoldalon található **Táblakapcsolások figyelmen kívül hagyása** lehetőség kiválasztásával megkerülhetik ezeket a kapcsolásokat.

Egy projekt például külön táblákban tárolhatja a szülő- és utódrekordokat, és közös kotorékazonosítót használhat kapcsolóoszlopként.

Ezt a modult a `join_tables` modullal együtt használja.

A modul a következőket adja vissza:

- oszlopok tömbjét a `0` indexen; és
- oszlopnevek asszociatív tömbjét az `1` indexen.

**Paraméterek:**

```json
[
  "column_name_1",
  "column_name_2"
]
```

### `allowed_columns`

Az `allowed_columns` modul oszlopszintű korlátozásokkal egészíti ki a sorszintű adathozzáférési szabályokat.

A sorszintű szabályok határozzák meg, hogy a felhasználó mely rekordokhoz férhet hozzá. Ez a modul határozza meg, hogy mely oszlopok maradnak láthatók, amikor egy rekord `restricted` vagy `no-geom` szabály hatálya alá esik, illetve amikor nincs egyező szabály.

A modul olyan projektekhez készült, amelyek alapszintű hozzáférése nem nyilvános, és amelyek adattáblái a megfelelő szabálytáblát használják.

**Paraméterek:**

```json
{
  "for_sensitive_data": [
    "column_visible_for_sensitive_records"
  ],
  "for_no-geom_data": [
    "column_visible_for_records_without_geometry_access"
  ],
  "for_general": [
    "column_visible_when_no_rule_matches"
  ]
}
```

A paraméterek jelentése:

- A `for_sensitive_data` az érzékeny rekordok esetében látható oszlopokat sorolja fel.
- A `for_no-geom_data` a `no-geom` rekordok esetében látható oszlopokat sorolja fel. Ha ez a kulcs hiányzik, azoknál a rekordoknál minden oszlop hozzáférhető.
- A `for_general` azokat az oszlopokat sorolja fel, amelyek akkor láthatók, ha egyetlen szabály sem illeszkedik. Ha ez a kulcs hiányzik, ebben az esetben minden oszlop korlátozott.

Tesztelje a tényleges jogosultságokat nyilvános, hitelesített, csoporttag és adminisztrátori fiókokkal. Az oszlopkorlátozások nem helyettesítik a megfelelő adatbázis- és API-hozzáférés-vezérlést.

### `bold_yellow`

A `bold_yellow` modul azonosítja az eredmény-összefoglalók fontos mezőit.

A konfigurált oszlopok félkövér sárga kiemeléssel jelennek meg a részletes eredménylistákban. A mobilalkalmazás ezt a konfigurációt használja az **Összegyűjtött adatok** összefoglaló címkéiben megjelenő értékek kiválasztására is.

**Paraméterek:**

```json
[
  "column_name_1",
  "column_name_2"
]
```

### `box_load_coord`

A `box_load_coord` modul egy **Pozíció** blokkot ad a térkép alá.

A blokk:

- megjeleníti a mutató aktuális helyének koordinátáit; és
- lehetővé teszi a felhasználó számára szélességi és hosszúsági értékek megadását, valamint a megfelelő pont térképen való elhelyezését.

A paraméterek a koordináta-rendszerek felhasználóknak megjelenő neveit EPSG-kódokhoz rendelik.

**Paraméterek:**

```json
{
  "wgs84": "4326",
  "eov": "23700"
}
```

Csak a projekt és térképi összetevői által támogatott koordináta-rendszereket konfiguráljon.

### `box_load_last_data`

A `box_load_last_data` modul egy **Gyors lekérdezések** mezőt ad a térképoldalhoz.

A következő lekérdezéseket biztosítja:

- az aktuális felhasználó legutóbbi feltöltése;
- bármely felhasználó legutóbbi feltöltése; és
- a legutóbb feltöltött rekordok.

Az első két lehetőség egy rekordot ad vissza. A paraméter a harmadik lehetőség által visszaadott rekordok számát szabályozza. A dokumentált alapértelmezett érték 10.

**Paraméterek:**

```json
[
  10
]
```

### `box_custom`

A `box_custom` modul egy projektspecifikus egyéni mezőt tölt be a térképoldalon.

Az egyéni megvalósítást a projekt `local/includes/modules/` könyvtárában kell elhelyezni. Az osztályának legalább a `print_box()` és `print_js()` metódusokat biztosítania kell.

A következő helyen tárolt egyéni modul esetében:

`local/includes/modules/hrsz_query.php`

a paraméter a fájl alapnevét tartalmazza:

```json
[
  "hrsz_query"
]
```

A megfelelő osztály elvárt neve `hrsz_query_Class`.

Az egyéni modulkódnak ellenőriznie kell a bemeneteket, escape-elnie kell a kimenetet, érvényesítenie kell a jogosultságokat, és paraméterezett adatbázis-lekérdezéseket kell használnia.

### `identify_point`

Az `identify_point` modul lehetővé teszi a felhasználók számára egy vagy több pont azonosítását a térképen, és megjeleníti a kiválasztott attribútumértékeket egy térképi felugró ablakban.

**Paraméterek:**

```json
[
  "column_name_1",
  "column_name_2"
]
```

Csak olyan oszlopokat adjon meg, amelyekhez a modul célközönsége jogosult hozzáférni.

### `cameratrap_api`

A `cameratrap_api` modul kommunikációt biztosít egy kameracsapda-irányítópult és a Nextcloud API között.

Funkciói a következők:

- kamerák és elemzések kezelése;
- képek fel- és letöltése;
- elemzések indítása; és
- az integrációhoz szükséges Nextcloud-hitelesítő adatok kezelése.

A modul modulspecifikus adatbázis-objektumokat hoz létre vagy használ. Engedélyezése előtt vizsgálja felül az SQL-telepítőfájlját és hozzáférési követelményeit.

**Paraméterek:** Nincsenek dokumentálva.

### `nextcloud_connect`

A `nextcloud_connect` modul összekapcsolja az OpenBioMaps rendszert egy Nextcloud-kiszolgálóval. Felhasználóiprofil-integrációt biztosít, és JWT-tokeneket bocsát ki hitelesítéshez.

A Nextcloud URL-jeit, hitelesítő adatait, aláírási titkait, tokenjeinek élettartamát és TLS-ellenőrzését biztonságosan, a telepített kiadás által elvárt mechanizmusokon keresztül kell konfigurálni.

**Paraméterek:** Nincsenek dokumentálva.

### `validation`

A `validation` modul belső API-t és adminisztrációs felületet biztosít az adatérvényesítési algoritmusokhoz.

Funkciói a következők:

- érvényesítési szabályok kezelése;
- rekordok érvényesítése; és
- érvényesítési műveletek naplózása.

A projektspecifikus érvényesítési megvalósítások további ellenőrzéseket végezhetnek a feltöltött adatokon.

**Paraméterek:** Nincsenek dokumentálva. A további szabályok a modul adminisztrációs felületén és az érvényesítési összetevőkön keresztül kezelhetők.

### `download_restricted`

A `download_restricted` modul adminisztrátor által felügyelt letöltés-engedélyezési munkafolyamatot vezet be.

Az azonnali letöltési hozzáférés helyett a felhasználók kérelmet nyújtanak be, amelyben leírják az adatok tervezett felhasználását. Az adminisztrátorok a modul adminisztrációs felületén jóváhagyhatják vagy elutasíthatják a kérelmet.

A modul a következőket biztosítja:

- letöltési kérelem űrlapja;
- adminisztrátori jóváhagyási munkafolyamat; és
- integráció a `results_buttons` modullal.

A `results_buttons` modullal együtt használva az exportálási lehetőségek csak azoknak a felhasználóknak érhetők el, akiknek kérelme és jogosultságai engedélyezik a letöltést.

A modul engedélyezése nem szünteti meg a kiszolgálóoldali hozzáférés-ellenőrzések szükségességét. Tesztelje a közvetlen exportálási URL-eket és API-kat annak ellenőrzésére, hogy a letöltési korlátozások nem kerülhetők-e meg.

**Paraméterek:** Nincsenek. A modul a saját adminisztrációs felületét használja.

### `extra_params`

Az `extra_params` bővítmény további bemeneti paramétereket biztosít az űrlapokhoz.

A bővítmény pontos szintaxisát és elérhetőségét a telepített OpenBioMaps-kiadás alapján kell ellenőrizni, mivel nem minden verzióban található meg ilyen nevű önálló modul.

**Paraméterek:** Itt nincs dokumentálva stabil paraméterformátum.

### `grid_view`

A `grid_view` modul alternatív poligonrácsok használatával jeleníti meg az adatokat. Ilyenek például az UTM-rácsok, a KEF-rácsok, az illesztett pontok és a dinamikusan létrehozott rácspoligonok.

Amikor egy rácsnézet aktív, a modul által szolgáltatott geometria helyettesíti a rekord eredeti geometriáját az adott megjelenítésben.

A modul megvalósítása többek között a következő metódusokat teszi elérhetővé:

- `print_box()`;
- `default_grid_geom()`; és
- `get_grid_layer()`.

#### Paraméterek

```json
{
  "layer_options": [
    "kef_5 (layer_data_grid)",
    "original (layer_data_points)"
  ]
}
```

Minden `layer_options` bejegyzés egy geometriaoszlopot társít egy MapServer-réteghez:

- a zárójel előtti szöveg a `YOURTABLE_qgrids` egyik oszlopa; és
- a zárójelen belüli szöveg a megfelelő MapServer-réteg neve.

A példában:

- a `kef_5` a `YOURTABLE_qgrids` geometriaoszlopa;
- a `layer_data_grid` a megjelenítéséhez használt MapServer-poligonréteg;
- az `original` a forrásgeometriát tárolja; és
- a `layer_data_points` az eredeti pontokat jeleníti meg.

Egy rácsgeometriához kompatibilis MapServer-réteg szükséges. A `layer_data_grid` rétegnek például poligonrétegnek kell lennie, ha poligonrácsokat jelenít meg.

#### Rácstábla

A modul létrehozza a `YOURTABLE_qgrids` táblát, ha még nem létezik. A tábla ezután kibővíthető a projekthez szükséges geometriaoszlopokkal.

A modul létrehozhat egy `update_grid_geoms` triggert és kezdeti oszlopmegjegyzéseket is. Ezek a létrehozott objektumok általában projektspecifikus felülvizsgálatot és módosítást igényelnek.

Állítsa be a rácsbeállítások felhasználóknak megjelenő neveit oszlopmegjegyzésként:

```sql
COMMENT ON COLUMN public.YOURTABLE_qgrids.original IS 'Original';
COMMENT ON COLUMN public.YOURTABLE_qgrids.kef_5 IS 'KEF 5×5';
```

Az SQL-azonosítókat következetesen használja. Ne konfiguráljon például `kef_5` értéket a modulban, ha az oszlopot `kef5` néven hozza létre.

#### Trigger a rácstáblán

A következő példa egy projektspecifikus rácsfrissítő függvényt hív meg:

```sql
CREATE TRIGGER update_grid_geoms
BEFORE INSERT OR UPDATE ON public.YOURTABLE_qgrids
FOR EACH ROW
EXECUTE PROCEDURE public.update_qgrid_geoms_arg(
  '0.1',
  '0.1',
  't',
  't',
  't',
  't',
  '0.05'
);
```

> **Fontos:** A trigger argumentumainak száma és sorrendje pontosan meg kell, hogy egyezzen az `update_qgrid_geoms_arg()` telepített definíciójával. Az alábbi korábbi példafüggvény a `TG_ARGV[8]` indexig olvas argumentumokat, míg a fenti példatrigger csak hét argumentumot ad át. Ne telepítse ezeket a példákat változtatás nélkül. Vizsgálja meg a telepített `grid_view.sql` fájlt és az adatbázis-függvényt, majd adjon meg minden szükséges argumentumot.

#### Trigger a forrástáblán

A forrástáblához olyan trigger szükséges, amely átmásolja a változásokat a rácstáblába:

```sql
CREATE TRIGGER qgrids
BEFORE INSERT OR DELETE OR UPDATE ON public.YOURTABLE
FOR EACH ROW
EXECUTE PROCEDURE insert_originalgeom_into_qgrids();
```

Egy példafüggvény törzse:

```sql
BEGIN
  IF TG_OP = 'INSERT' THEN
    EXECUTE format(
      'INSERT INTO %I_qgrids (row_id, original) SELECT %L, %L::geometry',
      TG_TABLE_NAME,
      NEW.obm_id,
      NEW.obm_geometry
    );
    RETURN NEW;
  END IF;

  IF TG_OP = 'UPDATE' THEN
    EXECUTE format(
      'UPDATE %I_qgrids SET original = %L::geometry WHERE row_id = %L',
      TG_TABLE_NAME,
      NEW.obm_geometry,
      NEW.obm_id
    );
    RETURN NEW;
  END IF;

  IF TG_OP = 'DELETE' THEN
    EXECUTE format(
      'DELETE FROM %I_qgrids WHERE row_id = %L',
      TG_TABLE_NAME,
      OLD.obm_id
    );
    RETURN OLD;
  END IF;

  RETURN NULL;
END;
```

Ez csak egy triggerfüggvény törzse, nem teljes `CREATE FUNCTION` utasítás.

#### Rácsfrissítő függvény

A következő korábbi példa a tervezett műveleteket szemlélteti:

```sql
DECLARE
  snap_x numeric := TG_ARGV[0];
  snap_y numeric := TG_ARGV[1];
  kef5 boolean := TG_ARGV[2];
  utm10 boolean := TG_ARGV[5];
  snap boolean := TG_ARGV[6];
  snap_polygon boolean := TG_ARGV[7];
  snap_polygon_size numeric := TG_ARGV[8];
BEGIN
  IF TG_OP = 'UPDATE' THEN
    IF kef5 THEN
      EXECUTE format(
        'SELECT geometry FROM shared."kef_5x5" WHERE ST_Within(%L::geometry, geometry)',
        NEW.original
      )
      INTO NEW.kef_5;
    END IF;

    IF snap THEN
      EXECUTE format(
        'SELECT ST_SnapToGrid(%L::geometry, %L, %L)',
        NEW.original,
        snap_x,
        snap_y
      )
      INTO NEW.snap;
    END IF;

    IF snap_polygon THEN
      EXECUTE format(
        'SELECT ST_Expand(ST_SnapToGrid(%L::geometry, %L, %L), %L)',
        NEW.original,
        snap_x,
        snap_y,
        snap_polygon_size
      )
      INTO NEW.snap_polygon;
    END IF;

    RETURN NEW;
  END IF;

  IF TG_OP = 'INSERT' THEN
    IF kef5 THEN
      EXECUTE format(
        'SELECT geometry FROM shared."kef_5x5" WHERE ST_Within(%L::geometry, geometry)',
        NEW.original
      )
      INTO NEW.kef_5;
    END IF;

    IF snap THEN
      EXECUTE format(
        'SELECT ST_SnapToGrid(%L::geometry, %L, %L)',
        NEW.original,
        snap_x,
        snap_y
      )
      INTO NEW.snap;
    END IF;

    IF snap_polygon THEN
      EXECUTE format(
        'SELECT ST_Expand(ST_SnapToGrid(%L::geometry, %L, %L), %L)',
        NEW.original,
        snap_x,
        snap_y,
        snap_polygon_size
      )
      INTO NEW.snap_polygon;
    END IF;

    RETURN NEW;
  END IF;

  RETURN NEW;
END;
```

Ez szintén csak egy függvénytörzs. Az `utm10` változó deklarálva van, de a bemutatott megvalósítás nem használja. Vizsgálja felül és egészítse ki a függvényt a projekt által igényelt rácstípusokhoz.

#### Kezdeti feltöltés

Miután a rácstábla és a triggerek elkészültek, a meglévő forrásgeometriák átmásolhatók egy üres rácstáblába:

```sql
INSERT INTO YOURTABLE_qgrids (row_id, original)
SELECT obm_id, obm_geometry
FROM YOURTABLE;
```

Példa egy illesztett geometria frissítésére:

```sql
UPDATE YOURTABLE_qgrids AS q
SET snap = source.snapped_geometry
FROM (
  SELECT
    obm_id,
    ST_SnapToGrid(obm_geometry, 0.13, 0.09) AS snapped_geometry
  FROM YOURTABLE
) AS source
WHERE q.row_id = source.obm_id;
```

Példa egy megosztott rácstáblából származó poligonok használatával végzett frissítésre:

```sql
UPDATE YOURTABLE_qgrids AS q
SET kef_5 = source.grid_geometry
FROM (
  SELECT
    data.obm_id,
    grid.obm_geometry AS grid_geometry
  FROM YOURTABLE AS data
  LEFT JOIN shared.kef_5x5 AS grid
    ON ST_Within(data.obm_geometry, grid.obm_geometry)
) AS source
WHERE q.row_id = source.obm_id;
```

Ebben a példában a `shared.kef_5x5` tartalmazza az előre meghatározott rácspoligonokat. Más geometria, például a `snap`, dinamikusan is létrehozható.

A sémamódosításokat és tömeges frissítéseket először tesztkörnyezetben futtassa. Készítsen biztonsági mentést az adatbázisról, ellenőrizze a térbeli indexeket, valamint a null, érvénytelen, határvonalon fekvő és nem pont típusú geometriák kezelését.

### `job_manager` érvényesítési feladatok

Az érvényesítési feladatkezelő háttérfolyamatokat konfigurál egy projekthez.

Adminisztrációs oldalán az adminisztrátorok a következőket konfigurálhatják:

- egyszerűsített ütemezés perc-, óra- és napértékekkel; valamint
- feladatspecifikus paraméterek JSON formátumban.

Egy feladat hozzáadása regisztrálja azt a projekt feladattáblájában, és sablonfájlokat hozhat létre az érvényesítési modul és a feladatok könyvtáraiban.

Ennek az összetevőnek az elérhetősége és pontos neve a telepített érvényesítési modultól függhet. A háttérfeladatok csak akkor futnak, ha a projekt `jobs.php` futtatója ütemezve van a kiszolgálón.

**Paraméterek:** Háttérfeladat-nevek listája.

#### `observation_lists`

Az `observation_lists` feladat a mobilalkalmazás által feltöltött megfigyelési listákat dolgozza fel.

A feltöltött megfigyelések kezdetben egy ideiglenes táblába kerülnek. A feladat:

- kitölti az `obm_observation_list_id` értékét;
- kiszámítja vagy átmásolja a lista kezdetének, végének és időtartamának értékeit; valamint
- a teljes listákat átmásolja a céltáblájukba.

A hiányos listákat kihagyja, hogy később dolgozza fel őket.

Feladatparaméterek:

- `list_start_column`: a lista kezdetét tároló oszlop;
- `list_end_column`: a lista végét tároló oszlop;
- `list_duration_column`: az időtartamot tároló oszlop;
- `only_time`: csak az időt tárolja-e a teljes időbélyeg helyett;
- `time_as_int`: percekre alakítsa-e az időt vagy az időtartamot.

Példa:

```json
{
  "YOURTABLE": {
    "list_start_column": "time_of_start",
    "list_end_column": "time_of_end",
    "list_duration_column": "duration",
    "only_time": true,
    "time_as_int": true
  }
}
```

#### `incomplete_observation_lists`

Az `incomplete_observation_lists` feladat a hiányosan maradó listákat kezeli.

Ha a várt és a beérkezett megfigyelések száma közötti különbség a beállított tűréshatáron belül van, a listát a következő `observation_lists` futás feldolgozhatja, és a rendszer üzenetet küld.

Ha a különbség meghaladja a tűréshatárt, a feladat rendszerüzenetet küld, de a listát kézi feldolgozásra hagyja.

Feladatparaméterek:

- `mail_to`: annak a szerepkörnek a numerikus azonosítója, amelynek tagjai megkapják az üzenetet;
- `diff_tolerance`: a megengedett különbség, amely felett kézi feldolgozás szükséges;
- `days_offset`: ennyi napot kell várni a hiányos lista feldolgozása előtt.

Példa:

```json
{
  "YOURTABLE": {
    "mail_to": 1265,
    "diff_tolerance": 2,
    "days_offset": 2
  }
}
```

Tesztelje az értesítések címzettjeit és a feladatok ütemezését, mielőtt éles környezetben erre a munkafolyamatra támaszkodna.

### `join_tables`

A `join_tables` modul kapcsolódó rekordokat jelenít meg egy adatlapon.

A jelenleg dokumentált megvalósítás egyszerű `LEFT JOIN` műveleteket támogat, kapcsolt táblánként egy egyenlőségi feltétellel.

**Paraméterek:**

```json
[
  {
    "table": "events",
    "join_on": [
      {
        "ref_field": "obm_id",
        "join_field": "patient_id"
      }
    ]
  },
  {
    "table": "measurements",
    "join_on": [
      {
        "ref_field": "obm_id",
        "join_field": "record_id"
      }
    ]
  }
]
```

Minden kapcsolt tábla esetében:

- a `table` a kapcsolandó tábla;
- a `ref_field` az aktuális rekord mezője; és
- a `join_field` a kapcsolt tábla egyező mezője.

Ahol szükséges, ezt a modult az `additional_columns` modullal együtt használja. Gondoskodjon a kapcsolómezők indexeléséről, és arról, hogy a felhasználók jogosultak legyenek minden kapcsolt tábla adataihoz hozzáférni.

### `list_manager`

A `list_manager` modul az adatfeltöltésekhez és lekérdezésekhez használható újrafelhasználható kifejezéslistákat kezeli.

A következőket biztosítja:

- listák létrehozása és szerkesztése;
- listák adatbázistáblákhoz és -oszlopokhoz rendelése;
- listatartalmak előállítása meglévő adatokból;
- listaadatok tárolása az adatbázisban; és
- felhasználói visszajelzés sikertelen listaművelet esetén.

A modul modális párbeszédpanelt használ a listaértékek szerkesztéséhez. Adminisztrációs funkcióihoz csak azok a felhasználók férjenek hozzá, akik jogosultak módosítani a feltöltési és lekérdezési szókészleteket.

**Paraméterek:** Nincsenek. A modul saját felhasználói felületét és modulspecifikus adatbázis-objektumait használja.

### `massive_edit`

A `massive_edit` modul lehetővé teszi a jogosult felhasználóknak, hogy a térképoldalon kiválasztott több rekordot a fájlfeltöltési felületen keresztül szerkesszenek.

A tömeges módosítások sok rekordot érinthetnek. Ellenőrizze a jogosultságokat, készítsen biztonsági mentést, és tesztelje a szerkesztett fájlt egy kis kijelölésen, mielőtt nagyobb frissítést alkalmazna.

**Paraméterek:** Nincsenek.

### `move_project`

A `move_project` modul egy másik OpenBioMaps-kiszolgálóra költöztet egy projektet.

Ez egy kísérleti modul. Használata előtt készítsen és ellenőrizzen biztonsági mentéseket, és ellenőrizze az alkalmazásverziók, adatbázis-bővítmények, projektfájlok, felhasználók, modulok, MapServer-konfigurációk és titkos adatok kompatibilitását a célkiszolgálón.

**Paraméterek:** Nincsenek dokumentálva.

### `read_table`

A `read_table` modul egyedi hivatkozáson keresztül görgethető HTML-táblaként tesz elérhetővé egy SQL-táblát vagy -nézetet.

**Paraméterek:**

```json
[
  {
    "table": "schema.table_name",
    "label": "Displayed table name",
    "orderby": "column_name"
  }
]
```

Minden bejegyzés a következőket tartalmazza:

- `table`: séma szerinti minősítéssel ellátott tábla- vagy nézetnév;
- `label`: a felhasználóknak megjelenő címke; és
- `orderby`: az alapértelmezett rendezéshez használt oszlop.

Egy egyedi vagy nehezen kitalálható hivatkozás önmagában nem elegendő hozzáférés-vezérlés. Ellenőrizze, hogy a modul érvényesíti-e a kívánt projekt-, csoport- és rekordszintű jogosultságokat.

### `results_asList`

A `results_asList` modul összecsukható, diákhoz hasonló bejegyzésekként jeleníti meg a lekérdezési eredményeket.

**Paraméterek:** Nincsenek.

### `results_asGPX`

A `results_asGPX` modul GPX-fájlként exportálja a lekérdezési eredményeket.

**Paraméterek:**

```json
{
  "name": "name_column",
  "description": [
    "description_column_1",
    "description_column_2"
  ]
}
```

A `name` oszlop adja a GPX-elem nevét. A `description` oszlopok értékei szerepelnek az elem leírásában.

Csak a telepített GPX-exportálóval kompatibilis geometriák exportálhatók.

### `results_asCSV`

A `results_asCSV` modul CSV-fájlként exportálja a lekérdezési eredményeket.

**Paraméterek:**

```json
{
  "sep": ",",
  "quote": "\""
}
```

- A `sep` határozza meg a mezők elválasztójelét.
- A `quote` határozza meg a mezőket közrefogó karaktert.

Olyan beállításokat válasszon, amelyek kompatibilisek az export megnyitására használt szoftverrel. Az exportnak továbbra is érvényesítenie kell minden alkalmazandó sor- és oszlopszintű hozzáférési szabályt.

### `results_asJSON`

A `results_asJSON` modul JSON formátumban exportálja a lekérdezési eredményeket.

**Paraméterek:** Nincsenek.

### `results_asTable`

A `results_asTable` modul teljes képernyős, minden elérhető mezőt tartalmazó HTML-táblaként jeleníti meg a lekérdezési eredményeket.

A következőket biztosítja:

- teljes rekordmegjelenítés;
- rendezhető oszlopok; és
- rekordok megtekintésére vagy szerkesztésére szolgáló hivatkozások, ha a felhasználó rendelkezik a szükséges jogosultságokkal.

Minden elérhető mező megjelenítése nagy eredményhalmazok esetén erőforrás-igényes lehet, és olyan mezőket tehet hozzáférhetővé, amelyeket korlátozni kellene. Konfigurálja a hozzáférés-vezérlési modulokat, és minden felhasználói csoport esetében tesztelje a kimenetet.

**Paraméterek:** Nincsenek.

### `results_asKML`

A `results_asKML` modul KML-fájlként exportálja a lekérdezési eredményeket.

**Paraméterek:**

```json
{
  "name": "name_column",
  "description": [
    "description_column_1",
    "description_column_2"
  ]
}
```

A `name` oszlop adja a KML-elem nevét. A `description` oszlopok értékei szerepelnek az elem leírásában.

### `results_buttons`

A `results_buttons` modul vezérlőelemeket ad a térképoldalhoz a lekérdezési eredmények letöltéséhez, mentéséhez, megosztásához és könyvjelzőzéséhez.

Az elérhető letöltési formátumok a megfelelő engedélyezett exportmoduloktól függnek. Ezek között szerepelhet CSV, GPX, KML, SHP és JSON.

A modul a következőket biztosíthatja:

- letöltési gombok;
- mentett lekérdezések és eredmények;
- mentett térbeli kijelölések;
- könyvjelzők;
- megosztás felhasználókkal vagy más OpenBioMaps-projektekkel; és
- integráció a `download_restricted` modullal.

Példakonfiguráció:

```json
{
  "bookmarks": "off",
  "sharing": "off",
  "server_share": "on"
}
```

Konfigurációs kulcsok:

- a `bookmarks` engedélyezi vagy letiltja a lekérdezési könyvjelzőket;
- a `sharing` engedélyezi vagy letiltja az általános megosztást; és
- a `server_share` engedélyezi vagy letiltja a másik kiszolgálóval vagy projekttel való megosztást.

A dokumentált alapértelmezések engedélyezik a könyvjelzőket, és letiltják a megosztást, valamint a kiszolgálók közötti megosztást. A letöltési gombok akkor jelennek meg, ha a hozzájuk tartozó exportmodulok engedélyezve vannak.

Ha a `download_restricted` aktív, a letöltések elérhetősége a kérelmezési és jóváhagyási munkafolyamattól is függ.

### `results_asStable`

A `results_asStable` modul kompakt, rendezhető eredménytáblát jelenít meg a térképoldalon.

A teljes eredménytáblával ellentétben csak a konfigurált oszlopokat jeleníti meg. A rekordok megtekintésére vagy szerkesztésére szolgáló hivatkozásokat is tartalmazhat, ha a felhasználó rendelkezik a szükséges jogosultságokkal.

**Paraméterek:**

```json
[
  "column_name_1",
  "column_name_2"
]
```

A modulnév a korábbi `results_asStable` írásmódot használja; ne nevezze át a konfigurációban.

### `results_specieslist`

A `results_specieslist` modul összesíti az aktuális lekérdezési eredményben előforduló fajokat.

A következőket jelenítheti meg:

- fajnevek;
- az egyes fajokhoz tartozó rekordok száma;
- a rögzített egyedek száma; és
- betűrendes vagy taxonómiai rendezési lehetőségek.

A fajnevekhez és egyedszámokhoz használt oszlopok a projekt sémájától és a modul megvalósításától függenek.

**Paraméterek:** Nincsenek dokumentálva.

### `results_summary`

A `results_summary` modul megjeleníti az aktuális lekérdezés által visszaadott különálló rekordok teljes számát.

Együttműködik a hozzáférési szabályokkal, így a korlátozott rekordokat csak akkor számolja, ha a felhasználó jogosult hozzáférni azokhoz.

Már egy összesített darabszám is érzékeny információt fedhet fel. Tesztelje a modult korlátozott rekordokkal és minden releváns hozzáférési szinten.

**Paraméterek:** Nincsenek.

### `results_table`

A `results_table` bővítmény teljes HTML-táblát hoz létre a lekérdezési eredményekből.

Az OpenBioMaps kiadásától függően ezt a funkciót más megvalósítási nevű modul, például a `results_asTable` vagy a `results_asHtmlTable` biztosíthatja. Pontosan azt a modulnevet használja, amely a telepített rendszer moduladminisztrációs oldalán szerepel.

**Paraméterek:** Nincsenek dokumentálva.

### `restricted_data`

A `restricted_data` modul szabályalapú korlátozásokat alkalmaz a projekt adataira.

A projektnek megfelelően konfigurált hozzáférési szabályokkal és kapcsolódó adatbázis-objektumokkal kell rendelkeznie. Tesztelje a korlátozásokat a térképoldalon, az adatlapoldalon, az exportokban, az API-kon és a közvetlen modulhivatkozásokon keresztül.

**Paraméterek:** Nincsenek.

### `spa_integration`

A `spa_integration` modul egy egyoldalas alkalmazást integrál egy OpenBioMaps-projekttel.

Modulspecifikus adminisztrációs beállításokat igényel. A konfiguráció után tesztelni kell az útválasztást, a hitelesítést, a jogosultságkezelést, a statikus erőforrások útvonalait és a közvetlen böngészőnavigációt.

**Paraméterek:** A modul adminisztrációs felületén kezelhetők.

### `text_filter`

A `text_filter` modul szöveges szűrőket ad a térképoldalhoz és a lekérdezési API-hoz. A konfigurált oszlopok és szűrőoperátorok alapján állítja össze az SQL-lekérdezés szűrési részét.

Példa:

```json
[
  "common_name",
  "obm_taxon",
  "notes::colour_rings",
  "obm_datum",
  "obm_uploading_date",
  "obm_uploader_user",
  "data.abundance:nested(data.count):autocomplete",
  "data.count:values():",
  "obm_files_id",
  "species::autocomplete"
]
```

A bejegyzések egy oszlophivatkozást és azt követő modulspecifikus módosítókat tartalmazhatnak, például:

- `autocomplete`;
- `values()`;
- `nested(...)`; vagy
- `::` karakterekkel elválasztott címke vagy másodlagos mező.

A szintaxis tömör és verziófüggő. Gondosan másolja át az ismerten működő kifejezéseket, kizárólag megbízható adatbázis-azonosítókat használjon, és minden szűrőt teszteljen a térképoldalon és a lekérdezési API-n keresztül is.

### `text_filter2`

A `text_filter2` modul fejlett taxonómiai és általános szöveges szűrőket biztosít. A `text_filter` modulhoz hasonlóan feltételeket ad az SQL-lekérdezéshez.

**Paraméterek:**

```json
{}
```

A további beállítások a modul felhasználói felületén vagy projektspecifikus konfigurációban kezelhetők.

### `transform_data`

A `transform_data` modul átalakítja a rekordértékeket, mielőtt azok megjelennének az eredményterületeken vagy bekerülnének a támogatott exportokba.

Az elérhető átalakítások a következők:

- `geom`: kattintható geometriahivatkozást hoz létre, amely megnyitja a helyet a térképen;
- `geom_nolink`: hivatkozás nélkül jeleníti meg az egyszerűsített WKT-t;
- `geom_wkt`: a szokásos WKT-ábrázolást jeleníti meg;
- `date_yearonly`: kinyeri az évet egy dátumból;
- `translate`: előre meghatározott szöveges állandókat fordít le a felhasználóknak megjelenő szövegre;
- `obslistlink`: hivatkozást hoz létre egy megfigyelésilista-azonosítóból; és
- `uplid`: a modul által támogatott feltöltésazonosító-átalakítást alkalmazza.

Példa:

```json
{
  "obm_geometry": "geom",
  "other_geometry": "geom_nolink",
  "obm_uploading_id": "uplid",
  "date_time_field": "date_yearonly",
  "method": "translate",
  "obm_observation_list_id": "obslistlink"
}
```

Minden kulcs egy adatbázis-oszlop, minden érték pedig az adott oszlopon alkalmazott átalakítás.

Az átalakítások a megjelenítést befolyásolják, az alapul szolgáló tárolt értéket nem. Ellenőrizze, hogy az átalakított hivatkozások és értékek nem fednek-e fel korlátozott adatokat.

## További dokumentációt igénylő modulok

A jelenlegi OpenBioMaps-adattár olyan modulokat is tartalmaz, amelyek még nincsenek részletesen ismertetve ezen az oldalon. A telepített verziótól függően ezek a következők lehetnek:

- `custom_data_check`;
- `ebp`;
- `fill_stable_with_column`;
- `ioc_bird_list`;
- `natura2000`;
- `results_asHtmlTable`;
- `results_asPDF`;
- `results_asSHP`;
- `service_envimap`;
- `snap_to_grid`; és
- `turnstile`.

Ne következtessen egy modul működésére vagy paraméterformátumára kizárólag a fájlnevéből. Engedélyezés előtt vizsgálja felül a forrását, modulmetaadatait, SQL-telepítőfájlját, hozzáférés-ellenőrzéseit és adminisztrációs felületét.

## Üzembe helyezési ellenőrzőlista

Mielőtt egy modult éles környezetben engedélyezne:

1. Ellenőrizze, hogy a modul szerepel-e a telepített OpenBioMaps-verzióban.
2. Ellenőrizze a JSON-paraméterek érvényességét.
3. Azonosítsa a szükséges modulokat, adatbázis-objektumokat, MapServer-rétegeket, feladatokat, külső szolgáltatásokat és PHP-bővítményeket.
4. Vizsgálja felül a modulhozzáférést és a csoporthozzáférést.
5. Tesztelje nyilvános, hitelesített, csoporttag és adminisztrátori fiókokkal.
6. Tesztelje a közvetlen URL-eket, exportokat és API-kat a hozzáférés-vezérlés megkerülhetőségének ellenőrzésére.
7. Ellenőrizze az alkalmazás, a PHP, a PostgreSQL és a háttérfeladatok naplóit.
8. Készítsen biztonsági mentést a projektről, mielőtt adatbázis-objektumokat módosító vagy tömeges frissítéseket végző modulokat engedélyezne.
9. Dokumentálja a konfigurációt, valamint a modul letiltásának vagy visszaállításának eljárását.
10. Ismételje meg a teszteket az OpenBioMaps frissítése után.
