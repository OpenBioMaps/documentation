# Module

Modulele sunt extensii configurabile ale aplicației web OpenBioMaps. Acestea
pot adăuga componente ale interfeței cu utilizatorul, funcții de procesare a
datelor, formate de export, instrumente administrative, API-uri sau integrări
cu servicii externe.

Există două domenii principale de aplicare a modulelor:

- **Modulele la nivel de proiect** oferă funcții care se aplică întregului
  proiect, precum gestionarea formelor spațiale, suportul pentru atașamente
  sau crearea utilizatorilor PostgreSQL.
- **Modulele la nivel de tabel** se aplică unui anumit tabel de date, precum
  filtrele paginii hărții, afișarea rezultatelor, transformările datelor sau
  formatele de export.

Modulele sunt conectate la hook-uri din aplicație. Majoritatea hook-urilor
destinate utilizatorilor se află pe pagina hărții și pe pagina profilului,
deși modulele pot adăuga și pagini de administrare, API-uri, activități de
fundal și funcții referitoare la încărcare.

Majoritatea modulelor acceptă parametri în format JSON. Unele module oferă în
schimb o interfață de administrare dedicată, iar altele necesită atât
parametri JSON, cât și configurări suplimentare ale bazei de date sau
MapServer.

> **Compatibilitatea versiunilor:** Modulele disponibile și parametrii
> acestora se pot modifica între versiunile OpenBioMaps. Pagina de
> administrare a modulelor din aplicația instalată reprezintă lista oficială
> a modulelor disponibile pentru un proiect. Verificați sursa modulului și
> notele de versiune înainte de a copia o configurație dintr-o altă
> instalare.

## Administrarea modulelor

Modulele pot fi activate și configurate pe pagina **Administrarea proiectului
→ Module**.

De obicei, un modul poate fi:

- adăugat proiectului;
- atribuit unor utilizatori sau grupuri;
- configurat cu parametri JSON;
- activat sau dezactivat; și
- deschis printr-o pagină de administrare specifică modulului, dacă aceasta
  este disponibilă.

Numele modulelor și cheile JSON sunt sensibile la majuscule și minuscule.
Validați JSON înainte de salvare. JSON nu permite comentarii sau virgule la
sfârșitul listelor.

### Adăugarea unui modul personalizat

Modulele personalizate pot fi încărcate și adăugate unui proiect.
Dezvoltatorii trebuie să utilizeze modulele exemplificative din
`resources/includes/modules/examples/` ca punct de plecare și să compare
implementarea acestora cu modulele incluse în versiunea OpenBioMaps instalată.

Codul unui modul personalizat trebuie verificat înainte de implementare. Un
modul rulează ca parte a aplicației și poate avea acces la datele proiectului,
la sesiunea utilizatorului autentificat și la conexiunile bazei de date.

### Accesul la module

Același modul poate fi adăugat de mai multe ori, cu setări de acces sau
parametri diferiți. Acest lucru permite administratorilor să ofere
configurații diferite unor utilizatori, grupuri sau tabele diferite.

De exemplu:

- `allowed_columns` poate expune coloane diferite unor grupuri diferite; și
- `text_filter` poate furniza coloane de filtrare specifice tabelelor într-un
  proiect care conține mai multe tabele de date.

Coloana **Access** controlează publicul general al unei instanțe de modul.
Opțiunile disponibile includ accesul public și accesul limitat la
utilizatorii autentificați.

Coloana **Group access** limitează suplimentar instanța modulului la anumite
grupuri ale proiectului sau la anumiți utilizatori.

Atunci când mai multe instanțe ale aceluiași modul se aplică unui utilizator,
testați ce configurație este selectată sau combinată de versiunea OpenBioMaps
instalată. Evitați suprapunerea regulilor de acces dacă nu înțelegeți
comportamentul acestora.

### Activarea și dezactivarea modulelor

Fiecare instanță de modul configurată poate fi activată sau dezactivată.
Dezactivarea unui modul îi păstrează configurația, dar împiedică utilizarea
acestuia.

După modificarea stării unui modul, testați pagina relevantă cu utilizatori
din fiecare grup de acces afectat. Unele module creează și obiecte în baza de
date sau păstrează setări specifice modulului atunci când sunt dezactivate.

### Eliminarea modulelor

Interfața de administrare a modulelor nu oferă în prezent o opțiune generală
pentru eliminarea unui modul instalat din aplicație.

O instanță de modul configurată poate fi dezactivată. Nu ștergeți manual
fișierele modulului sau obiectele bazei de date decât dacă este cunoscută
procedura de eliminare a modulului și este disponibilă o copie de siguranță.

### Parametrii modulelor

Majoritatea modulelor acceptă parametri JSON direct pe pagina de administrare
a modulelor. Alte module oferă o filă de administrare dedicată sarcinilor
specifice modulului. `box_load_selection` este un exemplu de modul cu
interfață administrativă proprie.

Exemplele din acest document utilizează substituenți precum `YOURTABLE`,
`column_name` și `schema.table`. Înlocuiți acești substituenți cu
identificatori din proiect.

## Module la nivel de proiect

### `box_load_selection`

Modulul `box_load_selection` gestionează forme spațiale reutilizabile.

Acesta oferă următoarele funcții:

- Utilizatorii pot încărca puncte, linii și poligoane. ESRI Shapefile este
  utilizat frecvent, dar pot fi acceptate și alte formate spațiale standard.
- Formele încărcate pot fi utilizate pentru definirea extinderii spațiale a
  unei interogări de date.
- O formă poate furniza geometria unei înregistrări în timpul încărcării prin
  web sau fișier.
- Formele pot fi partajate cu alți utilizatori.
- Formele disponibile utilizatorului pot fi descărcate și afișate de
  aplicația mobilă.

Formele încărcate recent nu sunt vizibile implicit altor utilizatori.
Administratorii de proiect pot acorda utilizatorilor permisiunea de a utiliza
fiecare formă pentru interogări sau încărcări de date.

Utilizatorii pot gestiona formele partajate prin blocul modulului
**Shared geometries** de pe pagina profilului. Administratorii de proiect pot
gestiona aceste permisiuni prin fila de administrare
`box_load_selection`.

Atunci când modulul este activat, pe pagina hărții apare o casetă
**Spatial query**. Utilizatorii pot selecta o formă disponibilă și pot
executa o interogare spațială în raport cu aceasta. Pentru geometriile
poligonale, interfața poate permite utilizatorilor să aleagă dacă sunt
incluse înregistrările care intersectează limita poligonului.

Dacă un formular de încărcare utilizează un câmp `obm_geometry`, controlul
hărții acestuia poate oferi opțiunea **Geometry from list**. Selectarea unei
forme denumite inserează geometria WKT a acesteia în câmpul de încărcare.

Aplicația mobilă poate afișa semi-transparent pe hărțile formularelor formele
disponibile pentru încărcare, etichetate cu numele acestora.

**Parametri:** Niciunul. Modulul utilizează interfața sa de administrare
dedicată.

### `photos`

Modulul `photos` activează câmpurile pentru fotografii și alte atașamente în
formularele de încărcare și afișează imaginile atașate pe paginile fișelor de
date ale înregistrărilor.

Limitele dimensiunilor fișierelor, tipurile de fișiere permise, stocarea,
controlul accesului și cerințele privind copiile de siguranță trebuie
configurate și la nivelul aplicației și al serverului.

**Parametri:** Niciunul.

### `create_pg_user`

Modulul `create_pg_user` permite utilizatorilor autorizați să creeze conturi
PostgreSQL personale.

Atunci când modulul este activat:

- pe pagina profilului apare o casetă **Create PostgreSQL user** pentru
  utilizatorii autorizați;
- utilizatorii își pot crea și reînnoi propriul cont pentru baza de date;
- contul generat este atribuit grupului de utilizatori PostgreSQL al
  proiectului; și
- contul poate fi utilizat de clienți pentru baze de date, precum QGIS.

În mod implicit, contul generat:

- are acces de citire la tabelele bazei de date ale proiectului;
- este limitat la o singură conexiune simultană a clientului; și
- expiră după un an.

Contul generat este adăugat grupului PostgreSQL denumit după proiect, de
obicei sub forma `PROJECT_user`. Un administrator al bazei de date poate
acorda permisiuni suplimentare, precum accesul de scriere la anumite tabele,
dar trebuie să respecte principiul privilegiului minim.

Utilizatorii își pot reînnoi accesul înainte sau după expirare, în funcție de
regulile modulului instalat.

Următoarea captură de ecran prezintă un exemplu de conexiune
PostgreSQL/PostGIS în QGIS:

![Adăugarea unei conexiuni PostGIS OpenBioMaps în QGIS](images/qgis_connect.jpg)

Nu expuneți PostgreSQL la internetul public fără setări adecvate pentru
firewall, TLS, autentificare și controlul accesului.

**Parametri:** Niciunul. Versiunile actuale pot oferi o pagină de
administrare dedicată.

### `computation`

Modulul `computation` furnizează funcții de calcul specifice proiectului.

Comportamentul său exact depinde de versiunea instalată a modulului și de
configurația proiectului. Examinați implementarea modulului înainte de a-l
activa într-un proiect aflat în producție.

**Parametri:** Niciunul documentat.

### `custom_filetype`

Modulul `custom_filetype` acceptă pregătirea specifică proiectului a unor
formate personalizate de descărcare, precum un fișier CSV în stil Observado.

Formatul de ieșire și orice implementare personalizată necesară depind de
proiect.

**Parametri:** Niciunul documentat.

### `taxon_meta`

Modulul `taxon_meta` furnizează funcții pentru metadatele referitoare la
taxoni.

Interfața sa cu utilizatorul, structura necesară a bazei de date și
configurația trebuie verificate în raport cu versiunea instalată a modulului.

**Parametri:** Niciunul documentat.

## Module la nivel de tabel

### `additional_columns`

Modulul `additional_columns` definește coloanele utilizate pentru asocierea
înregistrărilor din mai multe tabele de date.

Atunci când tabelele sunt conectate printr-un identificator comun,
interogările pot include înregistrările asociate identificatorului respectiv.
Utilizatorii pot evita aceste îmbinări selectând **Ignore table joins** pe
pagina hărții.

De exemplu, un proiect poate stoca înregistrările pentru părinți și urmași în
tabele separate și poate utiliza un identificator comun al vizuinii drept
coloană de îmbinare.

Utilizați acest modul împreună cu `join_tables`.

Modulul returnează:

- o matrice de coloane la indexul `0`; și
- o matrice asociativă de nume de coloane la indexul `1`.

**Parametri:**

```json
[
  "column_name_1",
  "column_name_2"
]
```

### `allowed_columns`

Modulul `allowed_columns` completează regulile de acces la date la nivel de
rând cu restricții la nivel de coloană.

Regulile la nivel de rând determină înregistrările pe care le poate accesa un
utilizator. Acest modul determină coloanele care rămân vizibile atunci când
unei înregistrări i se aplică o regulă `restricted` sau `no-geom` ori atunci
când nu există nicio regulă corespunzătoare.

Modulul este destinat proiectelor al căror nivel de acces de bază nu este
public și ale căror tabele de date utilizează tabelul de reguli
corespunzător.

**Parametri:**

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

Semnificația parametrilor:

- `for_sensitive_data` enumeră coloanele vizibile pentru înregistrările
  sensibile.
- `for_no-geom_data` enumeră coloanele vizibile pentru înregistrările
  `no-geom`. Dacă această cheie este omisă, toate coloanele sunt accesibile
  pentru înregistrările respective.
- `for_general` enumeră coloanele vizibile atunci când nu se potrivește nicio
  regulă. Dacă această cheie este omisă, toate coloanele sunt restricționate
  în acest caz.

Testați permisiunile efective cu conturi publice, autentificate, membre ale
grupurilor și de administrator. Restricțiile coloanelor nu trebuie
considerate un înlocuitor pentru controlul corect al accesului la baza de
date și la API.

### `bold_yellow`

Modulul `bold_yellow` identifică acele câmpuri importante din sintezele
rezultatelor.

Coloanele configurate sunt evidențiate cu galben și caractere aldine în
listele detaliate de rezultate. Aplicația mobilă utilizează și această
configurație pentru a selecta valorile afișate în etichetele de sinteză
**Collected data**.

**Parametri:**

```json
[
  "column_name_1",
  "column_name_2"
]
```

### `box_load_coord`

Modulul `box_load_coord` adaugă un bloc **Position** sub hartă.

Blocul:

- afișează coordonatele poziției actuale a indicatorului; și
- permite unui utilizator să introducă valorile pentru latitudine și
  longitudine și să plaseze punctul corespunzător pe hartă.

Parametrii asociază numele sistemelor de coordonate afișate utilizatorului cu
coduri EPSG.

**Parametri:**

```json
{
  "wgs84": "4326",
  "eov": "23700"
}
```

Configurați numai sisteme de coordonate acceptate de proiect și de
componentele sale cartografice.

### `box_load_last_data`

Modulul `box_load_last_data` adaugă o casetă **Quick queries** pe pagina
hărții.

Aceasta oferă interogări pentru:

- cea mai recentă încărcare a utilizatorului actual;
- cea mai recentă încărcare efectuată de orice utilizator; și
- înregistrările încărcate cel mai recent.

Primele două opțiuni returnează o singură înregistrare. Parametrul controlează
numărul de înregistrări returnate de a treia opțiune. Valoarea implicită
documentată este 10.

**Parametri:**

```json
[
  10
]
```

### `box_custom`

Modulul `box_custom` încarcă pe pagina hărții o casetă personalizată,
specifică proiectului.

Implementarea personalizată trebuie plasată în directorul
`local/includes/modules/` al proiectului. Clasa acesteia trebuie să furnizeze
cel puțin metodele `print_box()` și `print_js()`.

Pentru un modul personalizat stocat în:

`local/includes/modules/hrsz_query.php`

parametrul conține numele de bază al fișierului:

```json
[
  "hrsz_query"
]
```

Clasa corespunzătoare trebuie să fie denumită `hrsz_query_Class`.

Codul modulului personalizat trebuie să valideze datele de intrare, să
escapeze datele de ieșire, să aplice permisiunile și să utilizeze interogări
parametrizate pentru baza de date.

### `identify_point`

Modulul `identify_point` permite utilizatorilor să identifice unul sau mai
multe puncte pe hartă și afișează valorile atributelor selectate într-o
fereastră pop-up pe hartă.

**Parametri:**

```json
[
  "column_name_1",
  "column_name_2"
]
```

Includeți numai coloanele pe care publicul vizat al modulului are permisiunea
să le acceseze.

### `cameratrap_api`

Modulul `cameratrap_api` asigură comunicarea dintre un panou pentru camere
capcană și API-ul Nextcloud.

Funcțiile sale includ:

- gestionarea camerelor și a analizelor;
- încărcarea și descărcarea imaginilor;
- pornirea analizelor; și
- gestionarea datelor de autentificare Nextcloud necesare integrării.

Modulul creează sau utilizează obiecte specifice modulului în baza de date.
Examinați fișierul SQL de instalare și cerințele sale de acces înainte de a-l
activa.

**Parametri:** Niciunul documentat.

### `nextcloud_connect`

Modulul `nextcloud_connect` conectează OpenBioMaps la un server Nextcloud.
Acesta oferă integrarea profilului utilizatorului și emite tokenuri JWT
pentru autentificare.

URL-urile Nextcloud, datele de autentificare, secretele de semnare, duratele
de viață ale tokenurilor și validarea TLS trebuie configurate în siguranță
prin mecanismele preconizate de versiunea instalată.

**Parametri:** Niciunul documentat.

### `validation`

Modulul `validation` oferă un API intern și o interfață de administrare
pentru algoritmii de validare a datelor.

Funcțiile sale includ:

- gestionarea regulilor de validare;
- validarea înregistrărilor; și
- înregistrarea acțiunilor de validare în jurnal.

Implementările de validare specifice proiectului pot efectua verificări
suplimentare asupra datelor încărcate.

**Parametri:** Niciunul documentat. Regulile suplimentare sunt gestionate
prin interfața de administrare a modulului și prin componentele de validare.

### `download_restricted`

Modulul `download_restricted` introduce un flux de lucru pentru autorizarea
descărcărilor, controlat de administrator.

În loc să primească acces imediat la o descărcare, utilizatorii trimit o
solicitare care descrie utilizarea preconizată a datelor. Administratorii pot
aproba sau respinge solicitarea prin interfața de administrare a modulului.

Modulul oferă:

- un formular de solicitare a descărcării;
- un flux de lucru pentru aprobarea de către administrator; și
- integrarea cu `results_buttons`.

Atunci când este utilizat împreună cu `results_buttons`, opțiunile de export
devin disponibile numai utilizatorilor a căror solicitare și ale căror
permisiuni permit descărcarea.

Activarea acestui modul nu elimină necesitatea verificărilor de acces pe
partea serverului. Testați URL-urile directe pentru export și API-urile pentru
a verifica dacă restricțiile privind descărcarea nu pot fi evitate.

**Parametri:** Niciunul. Modulul utilizează interfața sa de administrare
dedicată.

### `extra_params`

Extensia `extra_params` furnizează formularelor parametri de intrare
suplimentari.

Sintaxa exactă și disponibilitatea acestei extensii trebuie verificate în
raport cu versiunea OpenBioMaps instalată, deoarece este posibil ca un modul
independent cu acest nume să nu existe în fiecare versiune.

**Parametri:** Aici nu este documentat niciun format stabil pentru parametri.

### `grid_view`

Modulul `grid_view` afișează date utilizând grile poligonale alternative.
Printre exemple se numără grilele UTM, grilele KEF, punctele ajustate și
poligoanele de grilă generate dinamic.

Atunci când este activă o vizualizare de tip grilă, geometria furnizată de
modul este utilizată în locul geometriei originale a înregistrării pentru
afișarea relevantă.

Implementarea modulului expune metode care includ:

- `print_box()`;
- `default_grid_geom()`; și
- `get_grid_layer()`.

#### Parametri

```json
{
  "layer_options": [
    "kef_5 (layer_data_grid)",
    "original (layer_data_points)"
  ]
}
```

Fiecare intrare `layer_options` asociază o coloană de geometrie cu un strat
MapServer:

- textul dinaintea parantezelor este o coloană din `YOURTABLE_qgrids`; și
- textul din interiorul parantezelor este numele stratului MapServer
  corespunzător.

În exemplu:

- `kef_5` este o coloană de geometrie din `YOURTABLE_qgrids`;
- `layer_data_grid` este stratul poligonal MapServer utilizat pentru
  afișarea acesteia;
- `original` stochează geometria sursă; și
- `layer_data_points` afișează punctele originale.

O geometrie de grilă necesită un strat MapServer compatibil. De exemplu,
`layer_data_grid` trebuie să fie un strat poligonal dacă afișează grile
poligonale.

#### Tabelul grilei

Modulul creează `YOURTABLE_qgrids` dacă acesta nu există deja. Tabelul poate
fi apoi extins cu acele coloane de geometrie necesare proiectului.

Modulul poate crea și un trigger `update_grid_geoms` și comentarii inițiale
pentru coloane. Aceste obiecte generate necesită în mod normal verificări și
modificări specifice proiectului.

Stabiliți numele afișate utilizatorului pentru opțiunile grilei sub forma
comentariilor coloanelor:

```sql
COMMENT ON COLUMN public.YOURTABLE_qgrids.original IS 'Original';
COMMENT ON COLUMN public.YOURTABLE_qgrids.kef_5 IS 'KEF 5×5';
```

Păstrați consecvența identificatorilor SQL. De exemplu, nu configurați
`kef_5` în modul și nu creați o coloană denumită `kef5`.

#### Triggerul tabelului grilei

Următorul exemplu apelează o funcție specifică proiectului pentru actualizarea
grilei:

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

> **Important:** Numărul și ordinea argumentelor triggerului trebuie să
> corespundă exact definiției instalate a funcției
> `update_qgrid_geoms_arg()`. Exemplul istoric de funcție de mai jos citește
> argumente până la indexul `TG_ARGV[8]`, în timp ce exemplul de trigger de
> mai sus furnizează numai șapte argumente. Nu implementați aceste exemple
> fără modificări. Examinați fișierul `grid_view.sql` instalat și funcția
> bazei de date, apoi furnizați toate argumentele necesare.

#### Triggerul tabelului sursă

Tabelul sursă necesită un trigger pentru copierea modificărilor în tabelul
grilei:

```sql
CREATE TRIGGER qgrids
BEFORE INSERT OR DELETE OR UPDATE ON public.YOURTABLE
FOR EACH ROW
EXECUTE PROCEDURE insert_originalgeom_into_qgrids();
```

Un exemplu pentru corpul funcției este:

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

Acesta este numai corpul unei funcții trigger, nu o instrucțiune
`CREATE FUNCTION` completă.

#### Funcția de actualizare a grilei

Următorul exemplu istoric demonstrează operațiile preconizate:

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

Și acesta este numai corpul unei funcții. Variabila `utm10` este declarată,
dar nu este utilizată de implementarea prezentată. Examinați și completați
funcția pentru tipurile de grilă necesare proiectului.

#### Popularea inițială

După ce tabelul grilei și triggerele sunt pregătite, geometriile sursă
existente pot fi copiate într-un tabel de grilă gol:

```sql
INSERT INTO YOURTABLE_qgrids (row_id, original)
SELECT obm_id, obm_geometry
FROM YOURTABLE;
```

Exemplu de actualizare pentru o geometrie ajustată:

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

Exemplu de actualizare utilizând poligoane dintr-un tabel de grilă partajat:

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

În acest exemplu, `shared.kef_5x5` conține poligoanele de grilă predefinite.
O altă geometrie, precum `snap`, poate fi generată dinamic.

Executați mai întâi modificările schemei și actualizările în bloc într-un
mediu de testare. Creați o copie de siguranță a bazei de date, verificați
indecșii spațiali și verificați comportamentul pentru geometrii nule,
nevalide, de frontieră și care nu sunt puncte.

### Activități de validare `job_manager`

Managerul activităților de validare configurează procesele de fundal pentru
un proiect.

Pe pagina sa de administrare, administratorii pot configura:

- o programare simplificată care conține valori pentru minute, ore și zile;
  și
- parametri specifici activității în format JSON.

Adăugarea unei activități o înregistrează în tabelul de activități al
proiectului și poate crea fișiere șablon în directoarele modulului de
validare și ale activităților.

Disponibilitatea și numele exact al acestei componente pot depinde de modulul
de validare instalat. Activitățile de fundal rulează numai dacă executorul
`jobs.php` al proiectului este programat pe server.

**Parametri:** O listă de nume ale activităților de fundal.

#### `observation_lists`

Activitatea `observation_lists` procesează listele de observații încărcate
de aplicația mobilă.

Observațiile încărcate ajung inițial într-un tabel temporar. Activitatea:

- completează `obm_observation_list_id`;
- calculează sau copiază valorile pentru începutul, sfârșitul și durata
  listei; și
- copiază listele complete în tabelul țintă al acestora.

Listele incomplete sunt omise pentru a fi procesate ulterior.

Parametrii activității:

- `list_start_column`: coloana care stochează începutul listei;
- `list_end_column`: coloana care stochează sfârșitul listei;
- `list_duration_column`: coloana care stochează durata;
- `only_time`: dacă se stochează numai ora în locul marcajului temporal
  complet;
- `time_as_int`: dacă ora sau durata se convertește în minute.

Exemplu:

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

Activitatea `incomplete_observation_lists` gestionează listele care rămân
incomplete.

Dacă diferența dintre observațiile așteptate și cele primite se încadrează în
toleranța configurată, lista poate fi procesată la următoarea execuție
`observation_lists` și este trimis un mesaj de sistem.

Dacă diferența depășește toleranța, activitatea trimite un mesaj de sistem,
dar păstrează lista pentru procesare manuală.

Parametrii activității:

- `mail_to`: ID-ul numeric al rolului ai cărui membri primesc mesajul;
- `diff_tolerance`: diferența permisă înainte de a fi necesară procesarea
  manuală;
- `days_offset`: numărul de zile de așteptare înainte de procesarea listei
  incomplete.

Exemplu:

```json
{
  "YOURTABLE": {
    "mail_to": 1265,
    "diff_tolerance": 2,
    "days_offset": 2
  }
}
```

Testați destinatarii notificărilor și programarea activității înainte de a
utiliza acest flux de lucru în producție.

### `join_tables`

Modulul `join_tables` afișează înregistrările asociate pe pagina fișei de
date.

Implementarea documentată în prezent acceptă operații `LEFT JOIN` simple, cu
o singură condiție de egalitate pentru fiecare tabel îmbinat.

**Parametri:**

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

Pentru fiecare tabel îmbinat:

- `table` este tabelul care trebuie îmbinat;
- `ref_field` este câmpul din înregistrarea actuală; și
- `join_field` este câmpul corespunzător din tabelul îmbinat.

Utilizați acest modul împreună cu `additional_columns` acolo unde este
necesar. Asigurați-vă că acele câmpuri utilizate pentru îmbinare sunt
indexate și că utilizatorii sunt autorizați să acceseze datele din fiecare
tabel îmbinat.

### `list_manager`

Modulul `list_manager` gestionează liste de termeni reutilizabile pentru
încărcările și interogările de date.

Acesta oferă:

- crearea și editarea listelor;
- asocierea listelor cu tabelele și coloanele bazei de date;
- generarea conținutului listelor din datele existente;
- stocarea datelor listelor în baza de date; și
- feedback pentru utilizator atunci când o operație asupra unei liste
  eșuează.

Modulul utilizează o fereastră de dialog modală pentru editarea valorilor
listei. Accesul la funcțiile sale administrative trebuie limitat la
utilizatorii care au permisiunea de a modifica vocabularele pentru încărcări
și interogări.

**Parametri:** Niciunul. Modulul utilizează propria interfață cu utilizatorul
și obiecte specifice modulului în baza de date.

### `massive_edit`

Modulul `massive_edit` permite utilizatorilor autorizați să editeze mai multe
înregistrări selectate de pe pagina hărții prin intermediul interfeței pentru
încărcarea fișierelor.

Modificările în bloc pot afecta numeroase înregistrări. Verificați
permisiunile, creați o copie de siguranță și testați fișierul editat pe o
selecție mică înainte de a aplica o actualizare de mari dimensiuni.

**Parametri:** Niciunul.

### `move_project`

Modulul `move_project` mută un proiect pe un alt server OpenBioMaps.

Acesta este un modul experimental. Înainte de utilizare, creați și verificați
copiile de siguranță și verificați compatibilitatea versiunilor aplicației,
extensiilor bazei de date, fișierelor proiectului, utilizatorilor, modulelor,
configurației MapServer și secretelor de pe serverul destinație.

**Parametri:** Niciunul documentat.

### `read_table`

Modulul `read_table` expune un tabel sau o vizualizare SQL sub forma unui
tabel HTML derulabil, accesibil printr-o legătură unică.

**Parametri:**

```json
[
  {
    "table": "schema.table_name",
    "label": "Displayed table name",
    "orderby": "column_name"
  }
]
```

Fiecare intrare conține:

- `table`: numele tabelului sau vizualizării, calificat cu schema;
- `label`: eticheta afișată utilizatorului; și
- `orderby`: coloana utilizată pentru ordonarea implicită.

O legătură unică sau dificil de ghicit nu reprezintă un control suficient al
accesului. Verificați dacă modulul aplică permisiunile preconizate la nivel de
proiect, grup și înregistrare.

### `results_asList`

Modulul `results_asList` afișează rezultatele interogării sub forma unor
intrări pliabile, asemănătoare diapozitivelor.

**Parametri:** Niciunul.

### `results_asGPX`

Modulul `results_asGPX` exportă rezultatele interogării într-un fișier GPX.

**Parametri:**

```json
{
  "name": "name_column",
  "description": [
    "description_column_1",
    "description_column_2"
  ]
}
```

Coloana `name` furnizează numele obiectului spațial GPX. Valorile din
coloanele `description` sunt incluse în descrierea obiectului spațial.

Pot fi exportate numai geometriile compatibile cu exportatorul GPX instalat.

### `results_asCSV`

Modulul `results_asCSV` exportă rezultatele interogării într-un fișier CSV.

**Parametri:**

```json
{
  "sep": ",",
  "quote": "\""
}
```

- `sep` definește separatorul câmpurilor.
- `quote` definește caracterul de încadrare a câmpurilor.

Alegeți setări compatibile cu software-ul utilizat pentru deschiderea
exportului. Exportul trebuie să aplice în continuare toate regulile de acces
aplicabile la nivel de rând și de coloană.

### `results_asJSON`

Modulul `results_asJSON` exportă rezultatele interogării în format JSON.

**Parametri:** Niciunul.

### `results_asTable`

Modulul `results_asTable` afișează rezultatele interogării sub forma unui
tabel HTML pe ecran complet, care conține toate câmpurile disponibile.

Acesta oferă:

- afișarea completă a înregistrării;
- coloane care pot fi sortate; și
- legături pentru vizualizarea sau editarea înregistrărilor atunci când
  utilizatorul are permisiunile necesare.

Afișarea tuturor câmpurilor disponibile poate necesita multe resurse în cazul
seturilor mari de rezultate și poate expune câmpuri care ar trebui
restricționate. Configurați modulele pentru controlul accesului și testați
rezultatul pentru fiecare grup de utilizatori.

**Parametri:** Niciunul.

### `results_asKML`

Modulul `results_asKML` exportă rezultatele interogării într-un fișier KML.

**Parametri:**

```json
{
  "name": "name_column",
  "description": [
    "description_column_1",
    "description_column_2"
  ]
}
```

Coloana `name` furnizează numele obiectului spațial KML. Valorile din
coloanele `description` sunt incluse în descrierea obiectului spațial.

### `results_buttons`

Modulul `results_buttons` adaugă pe pagina hărții controale pentru
descărcarea, salvarea, partajarea și marcarea rezultatelor interogării.

Formatele de descărcare disponibile depind de modulele de export
corespunzătoare care sunt activate. Acestea pot include CSV, GPX, KML, SHP și
JSON.

Modulul poate oferi:

- butoane pentru descărcare;
- interogări și rezultate salvate;
- selecții spațiale salvate;
- semne de carte;
- partajarea cu utilizatori sau alte proiecte OpenBioMaps; și
- integrarea cu `download_restricted`.

Exemplu de configurație:

```json
{
  "bookmarks": "off",
  "sharing": "off",
  "server_share": "on"
}
```

Cheile configurației:

- `bookmarks` activează sau dezactivează semnele de carte pentru interogări;
- `sharing` activează sau dezactivează partajarea generală; și
- `server_share` activează sau dezactivează partajarea cu un alt server sau
  proiect.

Valorile implicite documentate activează semnele de carte și dezactivează
partajarea și partajarea cu serverul. Butoanele pentru descărcare apar atunci
când sunt activate modulele de export corespunzătoare.

Atunci când `download_restricted` este activ, disponibilitatea descărcării
depinde și de fluxul de lucru pentru solicitare și aprobare.

### `results_asStable`

Modulul `results_asStable` afișează pe pagina hărții un tabel de rezultate
compact, care poate fi sortat.

Spre deosebire de un tabel complet de rezultate, acesta afișează numai
coloanele configurate. Poate include și legături pentru vizualizarea sau
editarea înregistrărilor atunci când utilizatorul are permisiunile necesare.

**Parametri:**

```json
[
  "column_name_1",
  "column_name_2"
]
```

Numele modulului utilizează forma istorică `results_asStable`; nu îl
redenumiți în configurație.

### `results_specieslist`

Modulul `results_specieslist` sintetizează speciile prezente în rezultatul
interogării actuale.

Acesta poate afișa:

- numele speciilor;
- numărul de înregistrări pentru fiecare specie;
- numărul de indivizi înregistrați; și
- opțiuni pentru sortare alfabetică sau taxonomică.

Coloanele utilizate pentru numele speciilor și numărul indivizilor depind de
schema proiectului și de implementarea modulului.

**Parametri:** Niciunul documentat.

### `results_summary`

Modulul `results_summary` afișează numărul total de înregistrări distincte
returnate de interogarea actuală.

Acesta se integrează cu regulile de acces, astfel încât înregistrările
restricționate sunt numărate numai atunci când utilizatorul are permisiunea
de a le accesa.

Chiar și o valoare de sinteză poate divulga informații sensibile. Testați
modulul cu înregistrări restricționate și cu fiecare nivel relevant de acces.

**Parametri:** Niciunul.

### `results_table`

Extensia `results_table` creează un tabel HTML complet din rezultatele
interogării.

În funcție de versiunea OpenBioMaps, această funcționalitate poate fi
furnizată de un modul cu un alt nume de implementare, precum
`results_asTable` sau `results_asHtmlTable`. Utilizați numele exact al
modulului afișat pe pagina de administrare a modulelor instalate.

**Parametri:** Niciunul documentat.

### `restricted_data`

Modulul `restricted_data` aplică datelor proiectului restricții bazate pe
reguli.

Proiectul trebuie să aibă reguli de acces și obiecte asociate ale bazei de
date configurate corect. Testați restricțiile prin pagina hărții, pagina
fișei de date, exporturi, API-uri și legături directe către module.

**Parametri:** Niciunul.

### `spa_integration`

Modulul `spa_integration` integrează o aplicație cu o singură pagină într-un
proiect OpenBioMaps.

Acesta necesită setări administrative specifice modulului. Rutarea,
autentificarea, autorizarea, căile resurselor statice și navigarea directă în
browser trebuie testate după configurare.

**Parametri:** Gestionați prin interfața de administrare a modulului.

### `text_filter`

Modulul `text_filter` adaugă filtre de text pe pagina hărții și în API-ul de
interogare. Acesta construiește partea de filtrare a interogării SQL din
coloanele și operatorii de filtrare configurați.

Exemplu:

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

Intrările pot conține o referință la o coloană, urmată de modificatori
specifici modulului, precum:

- `autocomplete`;
- `values()`;
- `nested(...)`; sau
- o etichetă sau un câmp secundar separat prin `::`.

Sintaxa este compactă și dependentă de versiune. Copiați cu atenție
expresiile funcționale cunoscute, utilizați numai identificatori de încredere
ai bazei de date și testați fiecare filtru atât prin pagina hărții, cât și
prin API-ul de interogare.

### `text_filter2`

Modulul `text_filter2` oferă filtre taxonomice și generale de text avansate.
La fel ca `text_filter`, acesta adaugă condiții interogării SQL.

**Parametri:**

```json
{}
```

Setările suplimentare pot fi gestionate prin interfața cu utilizatorul a
modulului sau prin configurația specifică proiectului.

### `transform_data`

Modulul `transform_data` transformă valorile înregistrărilor înainte ca
acestea să fie afișate în zonele de rezultate sau incluse în exporturile
acceptate.

Transformările disponibile includ:

- `geom`: creează o legătură pe care se poate face clic pentru geometrie și
  care deschide locația pe hartă;
- `geom_nolink`: afișează WKT simplificat, fără legătură;
- `geom_wkt`: afișează reprezentarea WKT obișnuită;
- `date_yearonly`: extrage anul dintr-o dată;
- `translate`: traduce constantele text predefinite în text afișat
  utilizatorului;
- `obslistlink`: creează o legătură din identificatorul unei liste de
  observații; și
- `uplid`: aplică transformarea identificatorului de încărcare acceptată de
  modul.

Exemplu:

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

Fiecare cheie este o coloană a bazei de date, iar fiecare valoare este
transformarea aplicată coloanei respective.

Transformările afectează prezentarea, nu valoarea stocată subiacentă.
Verificați dacă legăturile și valorile transformate nu divulgă date
restricționate.

## Module care necesită documentație suplimentară

Depozitul OpenBioMaps actual conține module care nu sunt încă descrise în
detaliu pe această pagină. În funcție de versiunea instalată, acestea pot
include:

- `custom_data_check`;
- `ebp`;
- `fill_stable_with_column`;
- `ioc_bird_list`;
- `natura2000`;
- `results_asHtmlTable`;
- `results_asPDF`;
- `results_asSHP`;
- `service_envimap`;
- `snap_to_grid`; și
- `turnstile`.

Nu deduceți comportamentul sau formatul parametrilor unui modul numai din
numele fișierului acestuia. Examinați sursa, metadatele modulului, fișierul
SQL de instalare, verificările accesului și interfața de administrare înainte
de a-l activa.

## Lista de verificare pentru implementare

Înainte de activarea unui modul în producție:

1. Confirmați că modulul este inclus în versiunea OpenBioMaps instalată.
2. Validați parametrii JSON ai acestuia.
3. Identificați toate modulele, obiectele bazei de date, straturile
   MapServer, activitățile, serviciile externe sau extensiile PHP necesare.
4. Verificați accesul la modul și accesul grupurilor.
5. Testați cu conturi publice, autentificate, membre ale grupurilor și de
   administrator.
6. Testați URL-urile directe, exporturile și API-urile pentru evitarea
   controlului accesului.
7. Verificați jurnalele aplicației, PHP, PostgreSQL și ale activităților de
   fundal.
8. Creați o copie de siguranță a proiectului înainte de activarea modulelor
   care modifică obiectele bazei de date sau efectuează actualizări în bloc.
9. Documentați configurația și procedura pentru dezactivarea modulului sau
   revenirea la starea anterioară.
10. Repetați testele după o actualizare OpenBioMaps.
