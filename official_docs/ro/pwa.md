Aplicația PWA de interogare pe hartă
====================================

Ce este aplicația OpenBioMaps de interogare pe hartă?
-----------------------------------------------------

Aplicația OpenBioMaps de interogare pe hartă este o aplicație hibridă
online/offline, cunoscută și ca aplicație web progresivă (PWA), concepută
pentru a sprijini activitatea pe teren. Aceasta oferă acces la o bază de date
OpenBioMaps online, permite utilizatorilor să interogheze înregistrări și
afișează locațiile spațiale ale acestora.

Aplicația rulează într-un motor de browser și este concepută în principal
pentru dispozitive mobile. Majoritatea operațiunilor necesită o conexiune la
rețea, însă datele preluate anterior pot fi accesate și offline.

Pentru a afla mai multe despre aplicațiile web progresive, consultați:

[Aplicații web progresive pe web.dev](https://web.dev/progressive-web-apps/)

Cum funcționează?
-----------------

În timp ce sunteți online, puteți afișa datele proiectului ca strat deasupra
hărții de bază. Datele sunt afișate ca un strat de puncte grupate, în care
eticheta din interiorul fiecărui simbol de grup indică numărul de entități
din grupul respectiv.

Harta oferă instrumente de filtrare și interogare pentru preluarea datelor
din baza de date online. În mod implicit, aplicația utilizează zona vizibilă
curentă a hărții drept zonă de interogare. Aplicarea acestui filtru preia
toate înregistrările corespunzătoare vizibile în extinderea curentă.

Evitați interogarea unei zone inutil de mari. Preluarea și afișarea unui număr
mare de înregistrări pot încetini aplicația sau o pot face să nu mai răspundă.

După descărcarea datelor solicitate, aspectul stratului de grupuri se modifică
ușor pentru a indica faptul că entitățile sunt disponibile pe dispozitiv.
Entitățile descărcate rămân grupate, deoarece randarea unui număr mare de
puncte individuale ar putea reduce semnificativ performanța aplicației.

Selectarea unui grup deschide o fereastră de dialog modală derulabilă care
conține atributele entităților din grupul respectiv.

Aplicația rulează într-un browser, dar poate fi instalată și lansată fără
interfața obișnuită a browserului, comportându-se astfel în mod similar unei
aplicații mobile independente. Datele proiectului preluate sunt stocate în
spațiul de stocare offline. Hărțile de bază nu sunt descărcate automat pentru
utilizare offline, deși dalele hărții vizualizate anterior pot rămâne
disponibile în memoria cache a browserului.

Browserele compatibile pot oferi o opțiune pentru instalarea aplicației pe
dispozitiv. În Chrome și în alte browsere bazate pe Chromium, această opțiune
poate apărea în bara de adrese sau în meniul browserului. Instalarea PWA oferă
o interfață mai asemănătoare unei aplicații și facilitează accesul la
funcționalitățile sale offline.

Funcționalități
---------------

- Afișarea locației curente a utilizatorului sub forma unui punct galben.
- Afișarea preciziei GPS sub forma unui cerc gri în jurul marcatorului de
  locație.
- Afișarea unui jurnal al traseului.
- Pornirea și oprirea înregistrării jurnalului traseului.
- Mărirea hărții la locația curentă a utilizatorului.
- Interogarea entităților punctuale din baza de date online prin desenarea
  unui cerc sau poligon ori prin utilizarea zonei vizibile curente a hărții.
- Stocarea înregistrărilor preluate pentru acces offline.
- Afișarea atributelor înregistrărilor preluate.

Limitări
--------

- Sunt acceptate numai entitățile punctuale.
- Hărțile de bază nu pot fi descărcate în mod explicit pentru utilizare
  offline.
- Preluarea unui număr mare de înregistrări, de exemplu mai mult de 50.000,
  poate cauza probleme de performanță sau de stocare offline.
- Disponibilitatea offline a dalelor hărții de bază vizualizate anterior
  depinde de stocarea în memoria cache a browserului și nu este garantată.
- Instalarea PWA și comportamentul offline pot varia în funcție de browser și
  de sistemul de operare.

URL-ul aplicației
-----------------

Aplicația este disponibilă la următorul URL specific proiectului:

`https://YOUR_SERVER/projects/YOUR_PROJECT/pwa-map/`

Înlocuiți:

- `YOUR_SERVER` cu numele gazdei serverului OpenBioMaps;
- `YOUR_PROJECT` cu identificatorul proiectului sau numele directorului
  proiectului.

Setări de configurare pentru aplicația PWA
------------------------------------------

Un număr redus de setări trebuie configurat prin intermediul interfeței de
administrare a proiectului.

### Stratul MapServer

Pe pagina **Setările hărților**, adăugați un nou strat MapServer în fișierul
*hărții private* al proiectului:

```
LAYER
    NAME "my_cluster"
    TYPE point
    STATUS on

    CONNECTIONTYPE postgis
    CONNECTION "host=localhost dbname=gisdata password={xxxxx} user=YOUR_PROJECT_admin options='--client_encoding=UTF8'"

    PROJECTION
        "init=epsg:4326"
    END

    METADATA
        "wms_title" "YOUR_PROJECT Cluster layer"
        "wms_srs"   "epsg:4326 epsg:900913"
    END

    DATA "obm_geometry FROM (SELECT * FROM YOUR_PROJECT WHERE ST_GeometryType(obm_geometry)='ST_Point') as new_table USING UNIQUE obm_geometry USING srid=4326"

    CLUSTER
        MAXDISTANCE 50
        REGION "ellipse"
    END

    LABELITEM "Cluster_FeatureCount"
    CLASSITEM "Cluster_FeatureCount"

    CLASS
        NAME "Clustered points"
        MAXSCALEDENOM 100000
        EXPRESSION ("[Cluster_FeatureCount]" != "1")
        STYLE
            SYMBOL "circle"
            SIZE 30
            COLOR 51 153 204
            OUTLINECOLOR 30 30 30
            OUTLINEWIDTH 1
        END
        LABEL
            #FONT arial
            #TYPE TRUETYPE
            SIZE 8
            COLOR 255 255 255
            ALIGN CENTER
            PRIORITY 10
            BUFFER 1
            PARTIALS TRUE
            POSITION cc
        END
    END

    CLASS
        NAME "Single point"
        MAXSCALEDENOM 100000
        EXPRESSION "1"
        STYLE
            SIZE 12
            SYMBOL "circle"
            COLOR 000 130 255
            OUTLINECOLOR 30 30 30
            OUTLINEWIDTH 1
        END
        TEXT "[NAME_OF_YOUR_LABELING_COLUMN]"
        LABEL
            #FONT arial
            #TYPE TRUETYPE
            SIZE 8
            COLOR 0 0 0
            OUTLINECOLOR 255 255 255
            ALIGN CENTER
            PRIORITY 9
            BUFFER 1
            PARTIALS FALSE
            POSITION ur
        END
    END

    TOLERANCE 50
    UNITS PIXELS
END # WMS cluster layer
```

Înlocuiți următorii substituenți:

- `NAME_OF_YOUR_LABELING_COLUMN` este numele coloanei utilizate pentru
  etichetarea punctelor individuale. O coloană cu numele speciei este o
  alegere obișnuită.
- `YOUR_PROJECT` este numele tabelului bazei de date interogat de strat.
  Acesta este în mod normal tabelul de bază al proiectului.
- `YOUR_PROJECT_admin` este utilizatorul PostgreSQL utilizat de proiect.
- `{xxxxx}` trebuie înlocuit cu parola corectă a bazei de date.

`MAXSCALEDENOM 100000` împiedică afișarea entităților atunci când harta este
micșorată dincolo de scara 1:100.000. Acest lucru ajută la împiedicarea
MapServer să calculeze un număr foarte mare de grupuri.

Șirul de conectare la baza de date trebuie să corespundă mediului serverului.
Nu copiați parola din exemplu și nu înregistrați acreditările reale ale bazei
de date în documentație sau într-un depozit de cod sursă. Cea mai sigură
abordare este copierea setărilor conexiunii dintr-un alt strat funcțional al
aceluiași proiect și verificarea fiecărei valori.

Șirul de conectare din exemplu este:

`CONNECTION "host=localhost dbname=gisdata password={xxxxx} user=YOUR_PROJECT_admin options='--client_encoding=UTF8'"`

Gazda corectă a bazei de date depinde de implementare. Într-o instalare
bazată pe containere, aceasta poate fi numele serviciului PostgreSQL în loc
de `localhost`.

### Interogarea SQL

Pe pagina **Setările interogărilor SQL**, creați o interogare pentru aplicația
PWA:

```
SELECT obm_id, obm_geometry, NAME_OF_YOUR_LABELING_COLUMN %selected%
FROM YOUR_PROJECT
%morefilter%
WHERE ST_GeometryType(obm_geometry)='ST_Point' AND %qstr%
```

Înlocuiți `NAME_OF_YOUR_LABELING_COLUMN` și `YOUR_PROJECT` cu aceleași valori
utilizate în stratul MapServer.

Nu eliminați următorii substituenți ai interogărilor OpenBioMaps:

- `%selected%`
- `%morefilter%`
- `%qstr%`

Filtrul de geometrie predefinit restricționează rezultatul la geometrii
punctuale. Acest lucru este necesar deoarece stratul de grupare nu poate
combina entități de tip linie și poligon.

Înainte de activarea aplicației pentru utilizatori, testați interogarea cu o
zonă vizibilă redusă și verificați dacă:

- sunt returnate numai înregistrările accesibile utilizatorului curent;
- fiecare înregistrare returnată are un `obm_id` valid;
- fiecare geometrie returnată este o geometrie punctuală;
- coloana de etichetare selectată este inclusă în rezultat; și
- interogarea se finalizează într-un interval de timp acceptabil.

Instalare
---------

După finalizarea configurării MapServer și a interogării SQL, deschideți o
singură dată următorul URL pentru inițializarea aplicației:

`https://YOUR_SERVER/projects/YOUR_PROJECT/pwa-map/setup.php`

Înlocuiți `YOUR_SERVER` și `YOUR_PROJECT` cu valorile utilizate în URL-ul
aplicației.

După finalizarea configurării, deschideți aplicația la:

`https://YOUR_SERVER/projects/YOUR_PROJECT/pwa-map/`

Utilizați întotdeauna HTTPS. Este necesar un context securizat pentru
funcționalitățile PWA importante, inclusiv service workers, instalarea,
accesul la locație și funcționarea offline fiabilă.

După deschiderea aplicației:

1. verificați dacă harta se încarcă;
2. acordați permisiunea de localizare dacă sunt necesare funcționalitățile de
   localizare și de jurnal al traseului;
3. efectuați o interogare pe o zonă redusă;
4. verificați dacă sunt afișate grupurile și atributele înregistrărilor;
5. instalați PWA utilizând opțiunea de instalare a browserului, dacă este
   disponibilă; și
6. testați accesul la înregistrările preluate anterior după deconectarea de la
   rețea.
