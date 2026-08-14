.. |br| raw:: html

    <br>
    

Documentația API
****************

.. _new-api:

OpenAPI
=======
Începând cu API v3.0 -

`<https://gitlab.com/openbiomaps/api/obm-project-api/#openbiomaps-project-api>`_

Exemplu Swagger UI:

`<https://openbiomaps.org/projects/checkitout/api/v3/swagger-ui>`_

.. _old-api:

API PDS
=======
De la API v1.0 la 2.6

Metode HTTP: GET, POST

Instrumente API: autentificare, preluarea datelor, trimiterea datelor, actualizarea setărilor

Acesta este primul API OBM (1.0, 2.0–2.6), care este planificat să fie eliminat treptat începând din septembrie 2026 și înlocuit cu API v3 (swagger-openapi).

Gestionari API:
---------------
Gestionar de autentificare (OAUTH):

/oatuh/token.php: autentificare/autorizare

Interfață bazată pe autentificare (PDS/Oauth):

/projects/*projectname*/*API_VERSION*/pds.php: preluarea datelor, încărcarea datelor, actualizarea setărilor

Solicitări neautentificate (web):

/projects/*projectname*/index.php

Versiunea API PDS:
..................
Exemplu: http://openbiomaps.org/projects/dead_animals/v2.1/pds.php

Versiunea implicită (dacă șirul versiunii lipsește din URL) este 1.1., care este compatibilă cu 2.0 și compatibilă retroactiv cu 1.0.


OAUTH
-----------
O implementare oauth2 bazată pe ttps://bshaffer.github.io/oauth2-server-php-docs/. OAUTH este utilizat atât în interfața web, cât și în PDS.

Variabile
.........
- grant_type:     password
- username:       o adresă de e-mail înregistrată
- password:       șirul parolei
- scope:          lista domeniilor de acces solicitate în sesiunea autentificată

Este necesară autentificarea HTML a clienților

Clienții disponibili sunt mobile, R, web

OAUTH acceptă numai solicitări de tip

- application/x-www-form-urlencoded
- multipart/form-data

Domenii de acces:

- get_form_data
- get_form_list
- put_data
- ...

.. _pds-api:

API PDS
-------
Interfața API principală a OBM. Este concepută în principal pentru clienții R și mobile. Utilizează OAUTH pentru autentificare.
Din cauza procesării OAUTH, aceasta acceptă numai solicitări application/x-www-form-urlencoded și multipart/form-data!

Variabile PDS
.............
- scope:          metode pentru date: consultați mai jos
- value:          majoritatea domeniilor de acces utilizează această variabilă
- header:         (trimiterea datelor) listă JSON cu numele coloanelor tabelului
- ignore_warning: (trimiterea datelor) ignoră avertismentele de încărcare
- form_id:        (put_data) stabilește ID-ul formularului
- data:           (trimiterea datelor) matrice JSON cu datele încărcate


Domenii de acces de tip GET
...........................
**get_project_vars**

Interoghează variabilele generale ale proiectului (disponibile și pentru utilizatorii neautentificați).

Parametri suplimentari:

- project [text]: dacă nu este setat, valoarea implicită este proiectul *template*

Returnează:

- project_url [url string]: adresa web a proiectului
- project_description [text string]: descrierea scurtă a proiectului
- game [on/off]: joc disponibil pentru aplicația mobilă Android
- public_mapserv [url string]: URL-ul serviciului de hărți accesibil public
- rserver_port [numeric]: portul numeric al serverului R-Shiny, accesibil la project_url

**get_project_list**

Obține o listă și informații de bază despre proiectele bazei de date disponibile pe server. Dacă un utilizator este deja autentificat, obține lista proiectelor în care utilizatorul are un cont și în care există interfețe publice pentru interogare sau încărcare. Dacă utilizatorul nu este autentificat, interoghează numai proiectele publice.

Parametri suplimentari:

- only-project [text]: interoghează parametrii numai pentru proiectul selectat; valoarea implicită este interogarea tuturor proiectelor accesibile
- accessible [text]: all/**accessible**. Dacă parametrul *accessible* este furnizat și valoarea sa este „accessible” (implicit)

Returnează:

- project_table [string],
- creation_date [date string],
- Creator [string],
- email [string],
- stage [string] experimental/testing/stable,
- doi [string],
- running_date [date string],
- license [string],
- rum [string],
- collection_dates [date range string],
- subjects [text],

**get_form_list**

Interoghează lista formularelor de încărcare disponibile.

**get_form_data**

Interoghează câmpurile formularului selectat.

Parametri suplimentari:

- value [numeric] ID-ul numeric al unui formular.

Returnează: :ref:`consultați exemplele de mai jos <get_form_data_example>`.

Explicațiile variabilelor:

*default value*: valoare fixă pentru toate observațiile. Aceasta poate fi controlată cu următoarele opțiuni:

- '_input' funcționează ca orice alt câmp cu un indicator sticky.
- '_list' funcționează ca orice alt câmp de tip listă cu un indicator sticky.
- '_geometry' funcționează ca un câmp de tip geometrie
- '_login_name' această valoare este înlocuită cu numele utilizatorului dacă acesta este autentificat sau este returnată ca _input
- '_email' această valoare este înlocuită cu adresa de e-mail a utilizatorului dacă acesta este autentificat sau este returnată ca _input
- '_autocomplete' alias pentru input
- '_boolean' se afișează ca o listă booleană normală
- '_attachment' se afișează ca un câmp normal pentru atașamente
- '_datum' se afișează ca un câmp normal pentru dată
- '_auto_geometry' câmp de geometrie fără opțiuni suplimentare (map, set)
- '_none' nu este utilizat

*column*: numele coloanei din baza de date

*short_name*: numele coloanei afișat utilizatorilor

*list*: matrice JSON pentru elementele meniului de selectare. Poate avea formatul {key:value} sau [value,value]

*control*: comenzi pentru verificarea datelor: custom_check, minmax, spatial, nocheck, NULL

*count*: (matrice JSON) dacă control='minmax', acest câmp conține valorile limită, de exemplu 1:100

*type*: tipul OpenBioMaps al coloanei:

- autocomplete	(matrice JSON)
- autocomplete_list (matrice JSON)
- boolean (listă cu două elemente)
- crings (inele colorate - text)
- date (YYYY-MM-DD sau alt format clar)
- datetime (YYYY-MM-DD HH:mm:ss)
- file_id (numele fișierelor ca ID-uri atribuite de server)
- line (șir de geometrie WKT)
- list (matrice JSON)
- numeric
- point	(șir de geometrie WKT)
- polygon (șir de geometrie WKT)
- text
- time (HH:mm)
- timetominutes (valoare numerică între 0 și 1440)
- tinterval interval de timp (HH:mm - HH:mm)
- wkt (șir WKT)
- array (matrice JSON)

*genlist*: matrice JSON pentru elementele unui meniu de completare automată. Poate avea formatul {key:value} sau [value,value]

*obl*: 1,2,3 (obligatoriu, neobligatoriu, eroare necritică). O eroare necritică poate fi tratată ca neobligatorie.

*api_params*: matrice JSON cu valori de control. Până la API v2.0, numai 'sticky' ca element al matricei.

api_params după API v2.0:

.. code-block:: json

  {
   "sticky":"off",
   "hidden":"off",
   "readonly":"off",
   "list_elements_as_buttons":"off",
   "once":"off",
   "unfolding_list": "off"
  }

*spatial_limit*: șir de poligon WKT pentru limita spațială. Este utilizat dacă tipul Control este spatial.

*list_definition*: matrice JSON cu definiția listei complexe

*custom_function*: null

*custom_label*:

*field_description*:


**get_profile**

Obține datele de profil ale unui utilizator selectat

**get_data**

Obține rânduri de date dintr-un tabel de date selectat (date despre observații).

**get_specieslist**

Obține lista de specii dintr-un proiect.

**get_history**

Obține istoricul unui rând de date selectat.

**get_report**

Execută o interogare predefinită și obține rezultatul.

**get_tables**

Obține lista tabelelor dintr-un proiect

**get_trainings**

Indisponibil începând cu API 2.6

Obține lista instruirilor/formularelor disponibile.

Returnează:

- setul de titluri, ID-uri și descrieri ale instruirilor,...

**get_training_questions**

Obține lista întrebărilor pentru instruirea selectată.

Indisponibil începând cu API 2.6

Parametri suplimentari:

- value [numeric] ID-ul numeric al unei instruiri.

Returnează:

- setul de întrebări, răspunsuri și setări

**training_results**

Lista stărilor instruirilor utilizatorilor pentru fiecare formular. Starea poate fi -1 (netrimis), 0 (nevalidat încă), 1 (finalizat, în regulă).

Indisponibil începând cu API 2.6

**training_toplist**

Clasamentul instruirilor. Valorile Mean, Max și Count pentru fiecare formular.

Indisponibil începând cu API 2.6

Parametri suplimentari:

- value [text] sinteză fără nume (nonames).

**get_mydata_rows**

Matrice JSON cu datele încărcate.

Parametri suplimentari:

- Value [numeric] limita lungimii matricei. Dacă este 0, nu există nicio limită; implicit nu există nicio limită.


Domenii de acces de tip POST
............................
**put_data**

Trimite/încarcă date utilizând un formular selectat

Poate fi

    - tracklog
    - form_id

Parametri obligatorii pentru form_id:

    - header
    - data

Parametri opționali împreună cu form_id:

    - metadata
    - api_warnings
    - srid
    - description
    - upload_table_post
    - default_values

Încărcarea fișierelor


Domenii de acces de tip PATCH
.............................
*set_rules*

Actualizează anumite setări


Exemple PDS
===========
**Exemple de autentificare**
----------------------------
Utilizarea CURL:

``curl -u mobile:123 https://openbiomaps.org/oauth/token.php -d "grant_type=password&username=foo@foobar.hu&password=mysecretpassword&scope=get_form_data+get_form_list+put_data" | jq``

Mesaje de eroare specifice:

.. code-block:: json

  {
    "error": "invalid_grant",
    "error_description": "Invalid username and password combination"
  }

Răspuns reușit:

.. code-block:: json

  {
    "access_token": "2cf59c094cc83498355ee9f520848efab6f71fe02",
    "expires_in": 3600,
    "token_type": "Bearer",
    "scope": "get_form_data get_form_list put_data apiprofile",
    "refresh_token": "e14dd3e0f13dffb17d36b2acfe9d161fd4ec1d4fb"
  }

Utilizarea tokenului de reîmprospătare:

``curl -F 'grant_type=refresh_token' -F 'refresh_token=e14dd3e0f13dffb17d36b2acfe9d161fd4ec1d4f3' -F 'client_id=R' https://openbiomaps.org/oauth/token.php | jq``

Returnează:

.. code-block:: json

  {
    "access_token":"ccc1d3e0f13dffb17d36b2acfe9d161fd4ec1d4de",
    "expires_in":3600,
    "token_type":"Bearer",
    "scope":"get_form_data get_form_list",
    "refresh_token":"a1e1d3e0f13dffb17d36b2acfe9d161fd4ec1d27c"
  }

.. _get_form_data_example:

**Exemple get_form_data**
-------------------------
Utilizarea CURL:

``curl -F 'access_token=c53c9ec690fede4c3' -F 'scope=get_form_data' -F 'value=246' -F 'project=dead_animals' https://openbiomaps.org/projects/dead_animals/v2.3/pds.php | jq``

Mesaje de eroare specifice:

.. code-block:: json

  {
   "status": "error",
   "message": "Form access denied.",
   "data": ""
  }

Răspuns reușit:

.. code-block:: json

  {
   "status": "success",
   "message": "",
   "data": {
     "form_header": {
       "login_name": "Gipsz Jakab",
       "login_email": "jakab.gipsz@openbiomaps.jupyter.ga",
       "boldyellow": [
         "species"
       ],
       "num_ind": "quantity",
       "tracklog_mode": "",
       "observationlist_mode": "false",
       "observationlist_time_length": "0",
       "periodic_notification_time": null
     },
     "form_data": [
       {
        "description": "...",
        "default_value": "...",
        "column": "species",
        "short_name": "Scientific species name",
        "list": ["..."],
        "control": "nocheck",
        "count": "{}",
        "type": "list",
        "genlist": null,
        "obl": "1",
        "api_params": {
          "sticky": "on",
          "hidden": "off",
          "readonly": "off",
          "list_elements_as_buttons": "on",
          "once": "off",
          "unfolding_list": "off"
        },
        "spatial_limit": null,
        "list_definition": {
          "multiselect": false,
          "selected": null,
          "triggerTargetColumn": [],
          "Function": ""
        },
        "custom_function": null,
        "column_label": null,
        "field_description": "..."
       }
    ]
   }
  }


**Exemple get_form_list**
-------------------------
Utilizarea CURL:

``curl https://openbiomaps.org/projects/checkitout/pds.php -d "access_token=d4fba6585303bba8da3e6afc1eb9d2399499ef3eb&scope=get_form_list"``

.. code-block:: json

  {
   "status": "success",
   "message": "",
   "data": [
    {
      "id": "1017",
      "visibility": "Observation list - obligatory / tracklog no",
      "form_id": "1017",
      "published_form_id": "1016",
      "form_name": "Observation list - obligatory / tracklog no",
      "last_mod": "1674809097"
    },
    {
      "id": "938",
      "visibility": "relational columns test",
      "form_id": "938",
      "published_form_id": "937",
      "form_name": "relational columns test",
      "last_mod": "1660679646"
    }]
  }

**Exemple de încărcare a datelor**
----------------------------------
Utilizarea CURL:

  curl -i -X POST \\ |br|
  -H "Content-Type:application/x-www-form-urlencoded" \\ |br|
  -H "Authorization:Bearer ..." \\ |br|
  -d "scope=put_data" \\ |br|
  -d "form_id=128" \\ |br|
  -d "header=[\"obm_geometry\",\"datum\",\"comment\",\"observer\"]" \\ |br|
  -d "data=[{\"obm_geometry\":\"point(48.071187 19.293714)\",\"datum\":\"2018-04-03\",\"comment\":\"asdad\",\"observer\":\"sdsaada\"}]" \\ |br|
  -d "ignore_warning=1" \\ |br|
  'https://openbiomaps.org/projects/checkitout/v2.5/pds.php'

Utilizarea JavaScript:

.. code-block:: javascript

    const xhr = new XMLHttpRequest();
    xhr.open("POST", "https://openbiomaps.org/projects/checkitout/v2.5/pds.php");
    xhr.setRequestHeader("Content-Type", "application/x-www-form-urlencoded; charset=UTF-8");
    const encodedData = Object.keys(data)
        .map(key => encodeURIComponent(key) + '=' + encodeURIComponent(data[key]))
        .join('&');
    xhr.onload = () => {
      if (xhr.readyState == 4 && xhr.status == 201) {
        console.log(JSON.parse(xhr.responseText));
      } else {
        console.log(`Error: ${xhr.status}`);
      }
    };
    xhr.send(encodedData);

Încărcarea datelor cu mai multe atașamente (fișiere):

    curl \\ |br|
    -F "access_token=..." \\ |br|
    -F 'scope=put_data' \\ |br|
    -F 'form_id=58' \\ |br|
    -F 'header=["species","obm_geometry","obm_files_id"]' \\ |br|
    -F 'batch=[\\ |br|
    {"data":[{"species":"Sylvia curruca","obm_geometry":"POINT(22.0 46.3)"}],"attached_files":"file1,file2"},\\ |br|
    {"data":[{"species":"Lanius Collurio","obm_geometry":"POINT(21.5 47.1)"}],"attached_files":"file3"}]' \\ |br|
    -F 'file1=@file1' \\ |br|
    -F 'file2=@file2' \\ |br|
    -F 'file3=@file3' \\ |br|
    http://localhost/biomaps/projects/template/pds.php

Încărcarea datelor împachetate. Linie de date într-o arhivă ZIP. Acesta este formatul vechi de export al aplicației mobile. Arhiva ZIP conține următoarele fișiere: |br|
    geometry.wkt |br|
    PICT01.JPG |br|
    PICT02.JPG |br|
    note.txt |br|

Numele fișierului ZIP este 'Sun May 13 08:52:51 CEST 2018.zip', creat pe baza șirului care reprezintă data și ora observației. Fișierul note.txt conține comentariul observației, care poate fi asociat cu o coloană a formularului. În acest exemplu, coloana este 'species'. Celelalte 3 coloane nu trebuie înlocuite sau omise. Dacă formularul conține coloane obligatorii, acestea pot fi completate prin parametrul default_value. În acest exemplu, coloana 'egyedszam' este un câmp obligatoriu care va fi completat cu '1'. Liniile împachetate pot fi împachetate suplimentar. În acest caz, parametrul 'packed_line' trebuie schimbat în 'multipacked_lines', iar arhiva zip trebuie să conțină fișierele zip descrise mai sus.

    curl \\ |br|
    -F 'scope=put_data' \\ |br|
    -F 'table=dinpi' \\ |br|
    -F 'form_id=58' \\ |br|
    -F 'header=["obm_geometry","obm_files_id","faj","dt_to"]' \\ |br|
    -F 'default_values={"egyedszam":"1"}' \\ |br|
    -F 'packed_line=@Sun May 13 08:52:51 CEST 2018.zip' \\ |br|
    http://localhost/biomaps/pds.php


**Exemplu get_project_list**
----------------------------
Utilizarea CURL:

Aceasta este o solicitare neautentificată către PDS:

``curl https://openbiomaps.org/projects/checkitout/v2.5/pds.php -d "scope=get_project_list&value=" | jq``

Răspuns reușit:

.. code-block:: json

  {
  "status":"success",
  "data": [
    {
      "project_table": "checkitout",
      "creation_date": "2016-03-09",
      "Creator": "",
      "email": "",
      "stage": "sandbox",
      "doi": null,
      "running_date": null,
      "licence": "ODbL",
      "rum": "+++",
      "collection_dates": null,
      "subjects": null,
      "project_hash": "28gmst44rm8g",
      "project_url": "https://openbiomaps.org/projects/checkitout/",
      "project_description": "Checkitout! Sandbox.",
      "public_mapserv": "-",
      "training": "f",
      "rserver": "f",
      "language": "hu",
      "game": "off",
      "rserver_port": 0
    }
  ]
  }

Explicații și exemple pentru instruiri
--------------------------------------
Nu există niciun client începând cu API 2.6.

Utilizarea Curl:

``curl -F 'scope=get_trainings' -F 'access_token=9d45...' -F 'project=dinpi' http://localhost/biomaps/pds.php``

Rezultatul unui apel reușit:

.. code-block:: json

  {"status":"success",
   "data":[
    {"id":"1","form_id":"95","html":"<div>...",,"task_description":"<div>...","enabled":"t","title":"Gyakorlás I.","qorder":"1","project_table":"dinpi"}]}

``curl -F 'scope=get_training_questions' -F 'access_token=9d45...' -F 'project=dinpi' http://localhost/biomaps/pds.php``

Rezultatul unui apel reușit:

.. code-block:: json

  {"status":"success",
   "data":[
    {"qid":"1", "training_id":"1", "caption":"...?", "answers":[{"Answer": "...","isRight": "false" } ],"qtype":"multiselect"}]}

qtype poate fi multi-select sau single select

``curl -F 'scope=training_results' -F 'access_token=9bb4...' -F 'project=dinpi' http://localhost/biomaps/pds.php``

Rezultatul unui apel reușit:

.. code-block:: json

  {"status":"success","data":"{"95":1,"96":0,"97":-1,"98":-1}"}

Semnificația valorilor: formularul 95 este finalizat, formularul 96 este finalizat, dar nu a fost încă validat, iar formularele 97 și 98 nu au fost încă finalizate

``curl -F 'scope=training_toplist' -F 'value=nonames' -F 'access_token=5ac3...' -F 'project=dinpi' http://localhost/biomaps/pds.php``

Rezultatul unui apel reușit:

.. code-block:: json

  {"status":"success",
   "data":{
    "95":{"mean":"0.50000000000000000000","count":"2","max":"0.7"},
    "96":{"mean":"0.70000000000000000000","count":"1","max":"0.7"},
    "97":{"mean":"0.70000000000000000000","count":"1","max":"0.7"},
    "98":{"mean":null,"count":"1","max":null}}}

``curl -F 'scope=training_toplist' -F 'access_token=5ac3...' -F 'project=dinpi' http://localhost/biomaps/pds.php``

.. code-block:: json

  {"status":"success","data":{
        "95":{"Gipsz Jakab":{"mean":"0.30000000000000000000","count":"1","max":"0.3"},
              "Foo Aladár":{"mean":"0.70000000000000000000","count":"1","max":"0.7"}},
        "96":{"Foo Aladár":{"mean":"0.70000000000000000000","count":"1","max":"0.7"}},
        "97":{"Foo Aladár":{"mean":"0.70000000000000000000","count":"1","max":"0.7"}},
        "98":{"Mr. Bean":{"mean":null,"count":"1","max":null}}}}


Răspunsuri generale ale API-ului
--------------------------------
Bazat pe: https://labs.omniti.com/labs/jsend

Este întotdeauna un șir JSON:

.. code-block:: json

  {
   "status":"X",
   "data":"",
   "message":""
  }

X: success, error, fail

Mesaje generale de eroare
-------------------------

.. code-block:: json

  {
    "status": "error",
    "message": "The access token provided is invalid"
  }

.. code-block:: json

  {
    "status": "error",
    "message": "The request requires higher privileges than provided by the access token"
  }



API WEB
-------
index.php este și un serviciu API în anumite cazuri (?query=), numai pentru solicitările _GET și solicitările neautentificate.
Acest API utilizează module text_filter pentru a construi o instrucțiune de interogare SQL.

Variabilele API-ului WEB
........................
query:          (punct final API)

qtable:         (tabel de date pentru preluarea datelor)

report:         (preluarea datelor utilizând interogări stocate)

output:         (JSON, XML, CSV, ... ieșire în fișier; dacă nu este setat, ieșirea este interfața web)

filename:       (numele fișierului de ieșire)

Obține lista serverelor OpenBioMaps active (cunoscute) utilizând API-ul query:

``curl https://openbiomaps.org/projects/openbiomaps_network/index.php -G -d 'query={"available":"up"}&output=json&filename=results.json'``

Obține un tabel filtrat dintr-un tabel care nu este cel implicit:

``curl https://openbiomaps.org/projects/pollimon/index.php -G -d 'query={"q":"2"}&output=json&qtable=pollimon_sample_plots'``

Punct final API LQ:

LQ:             (afișează datele din rezultatul unei interogări stocate)


Exemplu de utilizare:

``wget https://openbiomaps.org/projects/checkitout/?report=2@szamossag&output=csv``
