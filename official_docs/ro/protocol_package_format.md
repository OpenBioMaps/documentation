# Formatul pachetelor de protocol, versiunea 1

Acest document definește cerințele primului format de pachet pentru programul
de instalare a protocoalelor. Pachetul este YAML declarativ: descrie tabelele,
coloanele, listele și formularele proiectului. Nu conține cod executabil sau SQL.

[Exemplul de observații pe teren](https://gitlab.com/openbiomaps/share-your-protocol/-/blob/main/minimal/protocol.yml)
și [pachetul PDS](https://gitlab.com/openbiomaps/share-your-protocol/-/blob/main/pds-mobile-test/protocol.yml)
sunt pachete publicabile din repository-ul de protocoale. Programul de
instalare citește pachete cu acest format din catalogul GitLab configurat.

## Fișierele pachetului și gestionarea versiunilor

Un catalog GitLab este un fișier `catalog.yml` aflat la o cale configurată în
repository. Fiecare intrare din catalog identifică un protocol și indică
fișierul YAML al pachetului printr-o cale relativă la repository. Un pachet
declară:

- `format_version`: versiunea acestui format de fișier, ca număr întreg;
- `protocol_id`: un identificator stabil în notație DNS inversă, care rămâne
  același între versiuni, de exemplu `org.openbiomaps.pds-mobile-test`;
- `protocol_version`: versiunea protocolului, independentă de format.

Catalogul repetă identificatorul și versiunea protocolului, astfel încât
clienții să poată lista pachetele fără a le încărca pe toate. Valorile
pachetului trebuie să corespundă intrării din catalog. Commitul din repository
identifică exact conținutul publicat al catalogului și al pachetului; calea
pachetului trebuie să rămână în interiorul repository-ului.

Specificația inițială utilizează versiunea de format `1`. Programul care
citește pachetul trebuie să respingă versiunile de format neacceptate și
proprietățile necunoscute, fără a ignora implicit setările. Versiunile
protocoalelor sunt independente de versiunea formatului. Programul de
instalare acceptă actualizări prin adăugare; modificările definițiilor
existente necesită examinare manuală.

Programul de instalare citește un proiect GitLab public configurat în fișierul
`/etc/openbiomaps/system_vars.php.inc` al serverului. Definiți
`PROTOCOL_INSTALLER_GITLAB_PROJECT` drept calea proiectului GitLab
(`group/project`). Constanta opțională `PROTOCOL_INSTALLER_GITLAB_REF`
selectează o ramură (implicit `main`), iar
`PROTOCOL_INSTALLER_GITLAB_CATALOGUE_PATH` selectează fișierul catalogului
relativ la repository (implicit `catalog.yml`). Această primă versiune nu
utilizează un token și nu acceptă repository-uri private.

```php
define('PROTOCOL_INSTALLER_GITLAB_PROJECT', 'openbiomaps/share-your-protocol');
define('PROTOCOL_INSTALLER_GITLAB_REF', 'main');
define('PROTOCOL_INSTALLER_GITLAB_CATALOGUE_PATH', 'catalog.yml');
```

## Identificatoare și nume

Tabelele, coloanele, formularele și listele au identificatoare stabile, locale
pachetului. Referințele utilizează aceste identificatoare, niciodată numele
sugerate pentru baza de date. Identificatoarele utilizează litere mici, cifre
și caractere de subliniere, încep cu o literă și sunt unice în cadrul tipului
de element respectiv. `suggested_name` este un nume local lizibil pentru
obiectele nou create; este o sugestie care poate fi modificată, iar obiectul
poate fi asociat cu unul existent compatibil. Pachetele nu trebuie să specifice
o bază de date, o schemă, un nume de tabel al proiectului sau un proprietar al
bazei de date.

Fiecare tabel declară un `target`:

- `project_main` înseamnă tabelul principal existent al proiectului, care poate
  fi extins;
- `create` înseamnă un tabel de date nou pe care administratorul îl poate
  asocia cu un tabel existent compatibil sau îl poate crea.

Formatul nu permite unui pachet să declare o destinație fizică arbitrară.
Coloanele OBM gestionate de sistem și infrastructura tabelelor sunt furnizate
de programul de instalare și nu trebuie repetate drept coloane ale
protocolului. Formularele pot utiliza identificatoarele de coloană rezervate
`system.geometry` și `system.files` pentru câmpurile standard de geometrie
și atașamente. Aceste identificatoare nu reprezintă coloane definite de
pachet și nu pot fi redenumite într-un pachet.

## Tabele și coloane

Fiecare coloană are un `id` stabil, un `suggested_name`, un `data_type` portabil
și metadate opționale `description` și `required`. Tipurile de date din
versiunea 1 sunt: `text`, `varchar`, `integer`, `decimal`, `boolean`, `date`,
`time`, `datetime`, `interval` și `text_array`. Tipurile descriu valorile
stocate, nu controalele formularului. Geometria și atașamentele utilizează
coloanele de sistem rezervate descrise mai sus. Nu există posibilitatea de a
specifica direct un tip SQL arbitrar.

`varchar` necesită un `max_length` întreg pozitiv și creează o coloană
`varchar(max_length)`. De exemplu:

```yaml
- id: species
  suggested_name: species
  data_type: varchar
  max_length: 255
```

O coloană `varchar(n)` din pachet poate reutiliza `varchar(m)` când `m >= n`
sau o coloană `varchar` fără limită de lungime ori `text`. O coloană `text`
fără limită de lungime din pachet nu poate reutiliza `varchar(n)` limitat:
destinația ar putea respinge valori viitoare mai lungi de `n`. Pentru a
reutiliza o coloană existentă de specii cu lungime limitată, publicați o
versiune de protocol care declară `varchar` și un `max_length` adecvat.

Numele coloanelor sunt sugestii, nu identificatoare. Programul de instalare
compară coloanele existente selectate după compatibilitatea tipului și a
capacității. Nu trebuie să convertească implicit datele sau să modifice
definițiile coloanelor existente.

## Liste

Fiecare listă are un `id` stabil și una dintre următoarele valori `kind`:

- `fixed`: valori ordonate `{code, label}` care aparțin pachetului. Un formular
  stochează `code`; `label` este textul afișat. `multiselect` este opțional și
  implicit fals.
- `project`: un loc rezervat pentru o listă specifică proiectului.
  Administratorul furnizează sau selectează sursa locală în timpul instalării;
  pachetul poate oferi un mesaj de îndrumare, dar nu poate impune o anumită
  listă locală.
- `table`: o listă citită dintr-un alt tabel al pachetului. `table`,
  `value_column` și `label_column` sunt referințe logice stabile către
  identificatoarele pachetului, nu nume SQL.

O listă bazată pe tabel poate include `filter_column` și `filter_value`, care
trebuie să indice o coloană declarată, respectiv o valoare scalară. Acest lucru
permite opțiuni filtrate fără a încorpora SQL. Un câmp de formular face
referire la o listă prin identificatorul ei stabil. Listele păstrează codurile
și etichetele când administratorul alege o sursă locală echivalentă.

## Formulare și câmpuri

Fiecare formular declară un `id` stabil, un `suggested_name`, un `mode`
(`web` sau `api`), identificatorul tabelului destinație, o descriere opțională,
setări și câmpuri ordonate. Setările din versiunea 1 sunt
`observationlist_mode` (`false`, `true` sau `force`), `observationlist_time`
(minute ca număr întreg nenegativ) și `tracklog_mode` (`false`, `force` sau
șir gol). Setările omise utilizează valoarea implicită a aplicației.

Fiecare câmp face referire la un identificator de coloană declarat sau la un
identificator de coloană de sistem rezervat și declară un `type` pentru
interfață. Tipurile de interfață din versiunea 1 sunt `text`, `textarea`,
`numeric`, `boolean`, `date`, `time`, `datetime`, `timetominutes`, `tinterval`,
`array`, `list`, `autocomplete`, `autocompletelist`, `point`, `line`, `polygon`,
`wkt` și `file_id`. Proprietățile opționale sunt `required` (valoare booleană),
`default` (scalar sau null), `api_params` (o listă de șiruri reprezentând
parametri acceptați ai aplicației) și `list` (un identificator de listă).
Proprietatea `list` este obligatorie pentru `list`, `autocomplete` și
`autocompletelist`; este invalidă pentru celelalte tipuri de câmp. Valorile
implicite sunt literale, cu excepția valorilor rezolvate de aplicație acceptate
în prezent: `_email`, `_login_name` și `_login_email`. Alte valori speciale
necesită suport explicit în programul de instalare înainte de a putea fi
utilizate de pachete.

Compatibilitatea dintre tipurile câmpurilor și cele de stocare în versiunea 1:

| Tip de câmp în formular | Coloană compatibilă |
| --- | --- |
| `text`, `textarea`, `list`, `autocomplete`, `autocompletelist` | `text` sau `varchar` |
| `numeric` | `integer` sau `decimal` |
| `boolean` | `boolean` |
| `date` | `date` |
| `time` | `time` |
| `datetime` | `datetime` |
| `timetominutes` | `integer` |
| `tinterval` | `interval` |
| `array` | `text_array` |
| `point`, `line`, `polygon`, `wkt` | `system.geometry` |
| `file_id` | `system.files` |

Parserul trebuie să respingă identificatoarele duplicate, proprietățile și
valorile enumerate necunoscute, referințele nedeclarate, combinațiile
incompatibile câmp/coloană, sursele de liste invalide și setările de formular
invalide. Validarea trebuie efectuată înaintea oricărei scrieri în baza de
date. Verificările referințelor încrucișate și ale compatibilității sunt
verificări semantice suplimentare față de parsarea YAML/schemei.

## Structura catalogului

Catalogul conține `catalogue_format_version: 1` și o listă `protocols`.
Fiecare intrare conține `protocol_id`, `protocol_version`, `title`,
`description` și `package`. `package` este calea relativă la repository a
fișierului YAML al pachetului. Intrările sunt unice după perechea
`(protocol_id, protocol_version)`.

Consultați [catalogul publicat](https://gitlab.com/openbiomaps/share-your-protocol/-/blob/main/catalog.yml)
și :ref:`ghidul pentru autorii de pachete și administratori <protocol-installer-guide>`.
