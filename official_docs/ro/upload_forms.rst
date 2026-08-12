.. _manage-upload-forms:

Gestionarea formularelor de încărcare
=====================================

Formularele de încărcare definesc modul în care utilizatorii și clienții
externi pot trimite date unui proiect. Un formular specifică tabelul
destinație, disponibilitatea, setările de acces, clienții acceptați,
câmpurile, regulile de validare, valorile implicite și relațiile dintre
câmpuri.

.. TODO: Adăugați un flux introductiv care să explice cum se creează,
   testează, publică, copiază, blochează și retrage un formular de încărcare.

.. TODO: Explicați ce permisiune administrativă este necesară pentru
   gestionarea formularelor de încărcare și indicați calea actuală de
   navigare către această pagină.

.. TODO: Clarificați ce setări sunt comune clienților web, pentru încărcarea
   fișierelor, API și mobili și identificați setările acceptate numai de un
   anumit client.


Lista formularelor disponibile
------------------------------

Formularele existente pot fi selectate pentru editare, ștergere sau blocare.

Datele nu pot fi încărcate folosind formulare blocate, iar aceste formulare
nu sunt vizibile pentru clienți în lista formularelor. Clienții offline nu
pot încărca date folosind formulare șterse, iar formularele șterse nu pot fi
restaurate.
Prin editarea formularelor, puteți modifica domeniul lor de utilizare (web,
API sau încărcare de fișiere), relația cu câmpurile tabelului bazei de date,
descrierea și regulile de acces, precum și modul lor de funcționare: eveniment
de observare sau ad-hoc.

Formularele blocate apar pe un fundal gri în listă.

Formularele pot fi setate și în mod doar în citire, indicat în listă printr-o
pictogramă cu lacăt. (Pentru aceasta, setați valoarea câmpului ``active`` din
tabelul ``project_forms`` la 3.)


Definirea antetului formularului
--------------------------------

Tabel destinație
................

Selectați tabelul proiectului în care vor fi scrise datele trimise prin
formularul de încărcare.

Puteți selecta numai tabele SQL înregistrate de OpenBioMaps în cadrul
proiectului, care conțin câmpurile OpenBioMaps de bază, precum ``obm_id``,
``obm_uploading_id`` etc.
Tabelul selectat nu poate fi modificat ulterior, deoarece câmpurile
formularului sunt legate de câmpurile tabelului selectat.

Formularele sunt sensibile la modificările structurii tabelului. Din acest
motiv, se recomandă insistent să nu editați tabelele cu alt instrument decât
OpenBioMaps, deoarece formularul își va pierde legătura cu câmpurile. În
astfel de cazuri, salvarea modificărilor formularului poate rezolva
inconsecvența, dar clienții nu vor putea încărca datele offline!


Numele formularului
...................

Introduceți un nume pentru formularul de încărcare. Numele trebuie să fie
unic în cadrul proiectului, deoarece face parte din identificatorul unic al
formularelor.

Un formular poate fi copiat prin redenumire. În acest caz, formularul
original își păstrează numele inițial; cu alte cuvinte, un formular nu poate
fi redenumit, ci numai copiat într-un formular nou, ceea ce afectează
funcționarea clienților offline!

Numele poate fi multilingv atunci când se utilizează o cheie de traducere cu
prefixul ``str_``. Pentru mai multe informații, consultați
:ref:`Traduceri <localisation>`.


Accesul la formular
...................

Definiți cine poate vizualiza și utiliza formularul:

* utilizatorii publici;
* toți utilizatorii autentificați; sau
* numai grupurile specificate.

Dacă este selectată opțiunea **numai grupurile specificate**, câmpul de
selectare a utilizatorilor și grupurilor devine activ, permițând acordarea
accesului utilizatorilor sau grupurilor selectate.

.. TODO: Confirmați etichetele actuale utilizate de interfața de administrare
   și dacă accesul poate fi atribuit direct utilizatorilor individuali,
   precum și grupurilor.

.. TODO: Explicați dacă accesul public la formular permite trimiterea datelor
   fără autentificare și cum sunt gestionate în acest caz utilizatorul care
   efectuează încărcarea, proprietatea, accesul de citire, accesul de
   scriere, limitarea ratei și prevenirea abuzurilor.

.. TODO: Clarificați dacă apartenența la grupuri imbricate acordă acces la
   formular și modul în care modificările apartenenței la grup afectează
   încărcările active sau salvate.


Accesul la date
...............

Datele încărcate prin formular vor fi disponibile numai grupurilor
specificate aici. În mod implicit, utilizatorul care efectuează încărcarea
poate citi și edita datele încărcate.

.. TODO: Documentați modul în care setările formularului privind accesul la
   date sunt transferate către regulile de acces la nivel de rând ale
   proiectului, inclusiv semnificația și formatul exacte ale atribuirilor de
   citire și scriere.

.. TODO: Confirmați comportamentul atunci când nu este selectat niciun grup
   și dacă utilizatorului care efectuează încărcarea i se acordă întotdeauna
   acces de citire și scriere.

.. TODO: Explicați modul în care aceste setări interacționează cu
   ``ACC_LEVEL``, ``MOD_LEVEL``, setările de sensibilitate, triggerul
   regulilor de acces și modulul ``allowed_columns``. Includeți exemple
   pentru proiecte publice, autentificate și restricționate la grupuri.

.. TODO: Documentați ce se întâmplă atunci când sunt modificate setările
   formularului privind accesul la date. Clarificați dacă setările noi
   afectează numai încărcările ulterioare sau actualizează și înregistrările
   existente.


Tipul formularului
..................

Trebuie selectat cel puțin unul dintre următoarele tipuri de formular:

* formular web;
* formular pentru încărcarea fișierelor; sau
* formular API, pentru accesul clienților externi, precum aplicația mobilă.

.. TODO: Explicați capacitățile și limitările fiecărui tip de formular,
   inclusiv dacă pot fi activate simultan mai multe tipuri.

.. TODO: Documentați cerințele de autentificare, selectare a versiunii și
   compatibilitate pentru clienții API și aplicațiile mobile.


Descrierea formularului
.......................

Introduceți o descriere scurtă sau detaliată a formularului. Descrierea poate
oferi instrucțiuni contribuitorilor.

.. TODO: Explicați unde este afișată descrierea în interfețele web, pentru
   încărcarea fișierelor, API și mobile, dacă acceptă traduceri sau marcaje și
   dacă există o lungime maximă.


SRID-ul formularului
....................

Selectați sistemul de referință spațială utilizat de datele trimise prin
formular. Sistemele de referință spațială pot fi căutate la
https://spatialreference.org/. Valoarea implicită este EPSG:4326 (WGS 84).

Dacă este specificată o listă de sisteme de referință spațială, utilizatorii
care efectuează încărcarea pot selecta numai opțiunile din listă. Definiți
lista sub forma unor identificatori EPSG și etichete vizibile separate prin
virgulă, utilizând următorul format:

.. code-block:: text

   4326:wgs84,23700:eov

.. TODO: Confirmați dacă SRID-ul formularului descrie coordonatele furnizate
   de utilizatorul care efectuează încărcarea, SRID-ul de stocare al coloanei
   de geometrie destinație sau ambele. Explicați când și cum este efectuată
   transformarea coordonatelor.

.. TODO: Documentați modul în care SRID-ul formularului afectează geometria
   WKT, câmpurile de latitudine și longitudine, fișierele spațiale importate,
   desenarea pe harta web și coordonatele aplicației mobile.

.. TODO: Confirmați sintaxa acceptată și validarea listei SRID, inclusiv dacă
   sunt acceptate spațiile, etichetele traduse, autoritățile non-EPSG sau
   etichetele sensibile la scrierea cu majuscule și minuscule.


Gruparea formularelor
.....................

Formularele pot fi organizate în grupuri în interfața web de selectare a
formularelor. Numele grupurilor pot fi definite sau selectate aici.

Această opțiune nu este disponibilă în prezent în aplicația mobilă.

.. TODO: Explicați cum sunt create, ordonate, redenumite, traduse și
   eliminate grupurile de formulare. Clarificați dacă gruparea afectează
   accesul sau numai prezentarea.

.. TODO: Confirmați dacă gruparea formularelor rămâne neacceptată în
   versiunea actuală a aplicației mobile.


Publicarea formularului
.......................

Un formular poate fi blocat prin publicarea sa folosind butonul portocaliu de
publicare din zona antetului formularului. Actualizarea unui formular
publicat creează o versiune nouă. Versiunile anterioare rămân disponibile
clienților API, precum aplicația mobilă.

Dintr-un formular publicat poate fi creată o versiune preliminară pentru
testare utilizând butonul **Creați o versiune preliminară** din partea de jos
a paginii. În mod implicit, versiunea preliminară este disponibilă numai
creatorului său. Ulterior, aceasta poate fi publicată în ramura publicată a
formularului.

.. TODO: Definiți modelul complet de versionare a formularelor, inclusiv
   versiunile preliminare, versiunile publicate, ramurile, identificatorii
   versiunilor și semnificația blocării unui formular.

.. TODO: Explicați dacă publicarea intră în vigoare imediat și cum selectează
   sau stochează în memoria cache o versiune a formularului clienții web,
   pentru încărcarea fișierelor, API și mobili.

.. TODO: Documentați cine poate vizualiza și testa o versiune preliminară,
   cum poate fi modificat accesul la aceasta și dacă pot exista simultan mai
   multe versiuni preliminare ale unui formular.

.. TODO: Explicați cum poate un administrator să compare versiuni, să revină
   la o versiune anterioară, să retragă o versiune publicată sau să
   soluționeze trimiterile efectuate folosind o versiune veche.


Setările evenimentelor de observare
...................................

Pentru o explicație a evenimentelor de observare și a diferenței dintre
observațiile ocazionale și cele bazate pe evenimente, consultați
:doc:`Evenimente de observare și observații ocazionale
<observation_events>`.

Pentru un eveniment de observare poate fi stabilită o limită de timp,
exprimată în minute. Când limita este atinsă, aplicația mobilă avertizează
utilizatorul că timpul a expirat. Avertismentul nu încheie evenimentul, iar
utilizatorul poate continua înregistrarea observațiilor.

Un **eveniment de observare forțat** înseamnă că formularul poate fi lansat
numai în modul eveniment. Dacă suportul pentru evenimente de observare este
activat, dar nu este forțat, utilizatorul poate alege între modul eveniment și
modul de observare ocazională.

.. TODO: Documentați toate setările evenimentelor de observare și explicați
   cum sunt stocate identificatorii evenimentelor, orele de început și
   sfârșit, valorile câmpurilor comune și observațiile individuale.

.. TODO: Explicați dacă limita de timp are doar caracter orientativ în
   fiecare client acceptat și ce se întâmplă atunci când aplicația este
   offline, suspendată sau repornită în timpul unui eveniment.

.. TODO: Confirmați etichetele actuale pentru activarea și forțarea
   evenimentelor de observare și identificați setările acceptate de interfața
   web, API și aplicația mobilă.


.. _tracklog:

Jurnalul traseului
..................

Această opțiune activează înregistrarea automată a jurnalului traseului în
timp ce formularul este utilizat. Înregistrarea jurnalului traseului poate fi
obligatorie sau opțională și este disponibilă numai în modul eveniment.

.. TODO: Explicați frecvența înregistrării locațiilor, permisiunile de
   localizare necesare și modul în care sunt gestionate înregistrarea
   offline, precizia, consumul bateriei și evenimentele întrerupte.

.. TODO: Documentați unde sunt stocate jurnalele traseelor, cine le poate
   accesa, cum sunt legate de evenimente și observații și dacă regulile lor
   de acces diferă de cele ale înregistrărilor trimise.

.. TODO: Adăugați o notă privind confidențialitatea și securitatea, care să
   explice că jurnalele traseelor pot dezvălui deplasările unui contribuitor
   și pot constitui, prin urmare, date cu caracter personal sau sensibile.


.. _periodic-notification:

Notificare periodică
....................

La intervalul specificat, în minute, aplicația îi reamintește observatorului
să înregistreze o observație nouă. Cronometrul rulează continuu și repornește
de fiecare dată când utilizatorul înregistrează o observație.

.. TODO: Confirmați dacă notificările periodice sunt disponibile numai în
   aplicația mobilă și dacă funcționează atunci când aplicația rulează în
   fundal.

.. TODO: Explicați când începe primul interval, ce se întâmplă atunci când o
   notificare este închisă și dacă înregistrarea sau editarea unei observații
   repornește cronometrul.


Definirea coloanelor formularului
---------------------------------

Secțiunea de definire a coloanelor specifică ce coloane ale tabelului
destinație apar în formular și cum sunt afișate și validate valorile trimise.

.. TODO: Explicați cum determină metadatele și tipurile de date ale
   coloanelor bazei de date setările inițiale ale coloanelor formularului.

.. TODO: Documentați modul în care modificările coloanelor tabelului
   destinație afectează versiunile preliminare și publicate existente ale
   formularului.


Inclusă
.......

Dacă este selectată, coloana apare în formular.

.. TODO: Explicați dacă o coloană neinclusă poate primi totuși o valoare
   implicită, generată sau furnizată prin API.


Ordinea coloanelor
..................

Câmpul mic de introducere de lângă opțiunea **Inclusă** definește ordinea
coloanei în formular. În mod implicit, acesta este gol.

.. TODO: Documentați valorile acceptate, sensul ordonării, tratarea valorilor
   duplicate sau lipsă și dacă ordinea poate fi modificată prin
   glisare și fixare.


Coloană
.......

Sunt afișate două nume: numele vizibil al coloanei, care poate fi editat
pentru formular, și numele original al coloanei bazei de date.

.. TODO: Explicați dacă numele vizibil acceptă chei de traducere ``str_`` și
   cum este prezentat în șabloanele de fișiere, mesajele de validare,
   exporturi, definițiile API și clienții mobili.

.. TODO: Clarificați dacă modificarea numelui vizibil afectează numai
   formularul sau modifică și metadatele bazei de date.


Obligatorie
...........

Sunt disponibile trei opțiuni: **da**, **nu** și **eroare necritică**.

``Da`` (vișiniu)
   Formularul nu poate fi trimis fără o valoare în această coloană.

``Nu`` (gri)
   Formularul poate fi trimis cu o valoare goală în această coloană.

``Eroare necritică`` (roz)
   Valorile goale sau cele care nu respectă o restricție pot fi trimise, dar
   utilizatorul care efectuează încărcarea trebuie să confirme fiecare rând
   afectat.

.. TODO: Explicați cum funcționează confirmarea unei erori necritice în
   formularele web, încărcările de fișiere, clienții API și aplicația mobilă.

.. TODO: Documentați dacă o confirmare a erorii necritice este înregistrată
   în baza de date sau în metadatele încărcării și dacă administratorii pot
   diferenția valorile confirmate de valorile care au trecut validarea.

.. TODO: Clarificați modul în care setările formularului privind caracterul
   obligatoriu interacționează cu restricțiile ``NOT NULL`` ale bazei de
   date, relațiile dintre coloane și câmpurile ascunse sau doar în citire.


Descrierea coloanei
...................

Introduceți o scurtă descriere a câmpului.

.. TODO: Explicați unde sunt afișate descrierile coloanelor, dacă acceptă
   traduceri sau marcaje și dacă sunt moștenite din comentariile coloanelor
   bazei de date.


Tipul coloanei
..............

Sunt disponibile următoarele tipuri de coloane ale formularului:

``text``
   Text arbitrar. Pot fi specificate lungimi minime și maxime.

``numeric``
   O valoare numerică. Pot fi specificate valori sau lungimi minime și
   maxime.

``list``
   O listă derulantă cu un singur element selectabil în mod implicit.

``true-false``
   O valoare booleană fals/adevărat. Ordinea valorilor poate fi controlată în
   câmpul de definire a listei, de exemplu ``false, true``.

``date``
   O dată cu anul, luna și ziua separate printr-un caracter acceptat. Este
   stocată utilizând un tip de dată al bazei de date.

``date and time``
   O dată urmată de un spațiu și o oră în format
   ``hour:minute:second``. Dacă secundele sunt omise, aplicația le consideră
   automat ``00`` și îi solicită utilizatorului care efectuează încărcarea să
   accepte modificarea. Dacă minutele sunt omise, aplicația le consideră
   ``00`` și solicită, de asemenea, confirmarea. Valoarea este stocată
   utilizând un tip dată-oră al bazei de date.

``time (timetominutes)``
   O valoare în format ``hours:minutes``, pe care aplicația o transformă
   într-un număr întreg. Este stocată utilizând un tip întreg al bazei de
   date.

``time``
   O valoare în format ``hours:minutes``, stocată utilizând un tip de oră al
   bazei de date.

``time interval (timeinterval)``
   Un interval de timp, de exemplu
   ``2014-02-25 12:00:00 2014-02-25 13:00:00``. Este stocat utilizând un tip
   de interval de timp al bazei de date.

``autocomplete``
   Generează sugestii de completare automată din coloana tabelului SQL
   specificată în câmpul de definire a listei. Sintaxa prescurtată documentată
   este ``table_name.column``. În mod implicit, tabelul este căutat în schema
   ``public`` a bazei de date ``gisdata``.

``autocompletelist``
   Similar cu ``autocomplete``, dar permite introducerea mai multor valori
   de completare automată într-un singur câmp.

``photo id``
   Dacă modulul pentru fotografii este activat, aplicația stochează în acest
   câmp identificatorii fotografiilor încărcate.

``geometry: point``
   O geometrie punctuală reprezentată ca WKT ``POINT(...)``.

``geometry: line``
   O geometrie liniară reprezentată ca WKT ``LINESTRING(...)``.

``geometry: polygon``
   O geometrie poligonală reprezentată ca WKT ``POLYGON(...)``.

``geometry: any``
   O geometrie reprezentată în WKT folosind un tip de geometrie acceptat.
   Consultați `un exemplu de formular
   <https://openbiomaps.org/projects/checkitout/upload/?form=736&type=web>`_.

``colour rings``
   Permite specificarea unei combinații de inele colorate. Secțiunea dintre
   paranteze drepte definește numărul maxim de inele care poate fi specificat
   pentru diferitele secțiuni ale piciorului. Aceasta este urmată de codurile
   individuale și etichetele culorilor disponibile, de exemplu
   ``[XX],Blue:B,red:R,green:G``.

   Codurile culorilor documentate sunt:

   * ``R`` — roșu;
   * ``P`` — roz;
   * ``G`` — verde;
   * ``g`` — verde-deschis;
   * ``O`` — portocaliu;
   * ``Y`` — galben;
   * ``B`` — albastru;
   * ``b`` — albastru-deschis;
   * ``W`` — alb;
   * ``K`` — negru;
   * ``N`` — maro;
   * ``U`` — purpuriu;
   * ``V`` — violet; și
   * ``M`` — argintiu.

   Consultați `un exemplu de formular pentru inele colorate
   <https://openbiomaps.org/projects/checkitout/upload/?form=939&type=web>`_.

.. TODO: Confirmați denumirile actuale ale tuturor tipurilor de coloane
   disponibile și mapați fiecare tip de formular la tipul de date PostgreSQL
   necesar.

.. TODO: Clarificați dacă setările minime și maxime pentru tipul numeric
   limitează valorile numerice, lungimile caracterelor sau ambele.

.. TODO: Documentați formatele de intrare, fusurile orare, intervalele și
   tipurile de stocare acceptate pentru câmpurile de dată, dată-oră, oră și
   interval. PostgreSQL nu are tipuri încorporate denumite ``datetime`` sau
   ``timeinterval``, prin urmare identificați tipurile exacte utilizate în
   baza de date.

.. TODO: Confirmați denumirile exacte ale geometriilor WKT acceptate pentru
   câmpurile liniare. Tipul de geometrie WKT standard este ``LINESTRING``, în
   timp ce interfața-sursă poate utiliza eticheta ``LINE``.

.. TODO: Documentați modul în care tipurile de geometrie ale formularului
   interacționează cu SRID-ul formularului, SRID-ul coloanei destinație,
   colecțiile de geometrii, geometriile multipart, coordonatele
   tridimensionale și geometriile nevalide.

.. TODO: Explicați formatele prescurtate și JSON pentru completarea automată,
   conexiunea la baza de date utilizată pentru căutări, permisiunile
   aplicabile, limitele rezultatelor, comportamentul potrivirii și măsurile
   de protecție împotriva injectării SQL.

.. TODO: Documentați formatul de stocare și relația cu fișierele atașate
   utilizate de ``photo id``.

.. TODO: Verificați sintaxa, reprezentarea stocată, secțiunile de picior
   acceptate și setul complet de culori al tipului ``colour rings``.
   Clarificați dacă ``purple`` și ``violet`` sunt în mod intenționat valori
   separate.


Controlul datelor introduse
...........................

Controalele datelor introduse verifică valorile introduse în câmp. Opțiunile
disponibile sunt:

* fără verificare;
* minim și maxim;
* expresie regulată;
* spațial; și
* verificare personalizată.

.. TODO: Documentați sintaxa de configurare și comportamentul fiecărui
   control al datelor introduse, inclusiv validarea pe client și server.

.. TODO: Explicați dacă restricțiile minime și maxime se referă la lungime,
   valoare numerică, dată sau altă proprietate, în funcție de tipul coloanei.

.. TODO: Documentați dialectul expresiilor regulate, delimitatorii,
   indicatorii, regulile de eludare și dacă expresia trebuie să corespundă
   valorii complete.

.. TODO: Explicați verificările spațiale și personalizate disponibile și
   adăugați exemple testate. Identificați unde este stocat codul de validare
   personalizat și cine are permisiunea de a-l edita.


Definirea listei
................

Pentru a utiliza o listă în timpul trimiterii datelor, setați tipul coloanei
la ``list``, ``autocomplete`` sau ``autocompletelist``.

Definițiile listelor pot descrie liste simple sau cu selecție multiplă, surse
de completare automată, valori obținute din alte tabele ale bazei de date și
reguli pentru filtrarea valorilor respective.

O listă scurtă poate fi definită direct. În exemplul următor, utilizatorii
care efectuează încărcarea pot selecta ``female`` sau ``male`` dintr-o listă
derulantă. Valoarea selectată este stocată în baza de date.

.. code-block:: json

   {
     "list": {
       "female": [],
       "male": []
     }
   }

Mai multe etichete de intrare pot fi mapate la aceeași valoare stocată. De
exemplu, ``F``, ``f`` și ``female`` pot fi interpretate toate drept valoarea
stocată ``female``. Acest lucru este util în special la încărcarea fișierelor
atunci când datele provenite de la contribuitori sau din ani diferiți
utilizează etichete diferite pentru același concept.

.. code-block:: json

   {
     "list": {
       "female": [
         "F",
         "f",
         "female"
       ],
       "male": [
         "M",
         "m",
         "male"
       ]
     }
   }

O listă poate fi introdusă și în format text simplu, cu câte o valoare pe
fiecare rând. Când formularul este salvat, aplicația transformă lista în text
simplu în JSON. JSON-ul rezultat poate fi apoi editat direct.

.. TODO: Clarificați modul în care sunt afișate și potrivite cheile,
   etichetele și aliasurile listelor. Documentați sensibilitatea la scrierea
   cu majuscule și minuscule, tratarea spațiilor albe, etichetele duplicate,
   valorile goale și suportul pentru traduceri.

.. TODO: Explicați cum sunt stocate valorile cu selecție multiplă și
   ``autocompletelist`` în coloana destinație și ce tipuri de coloane
   PostgreSQL sunt acceptate.

Valorile listelor pot proveni și dintr-un tabel SQL. Specificați schema
(``optionsSchema``), tabelul (``optionsTable``), coloana valorii stocate
(``valueColumn``) și, dacă este necesar, coloana etichetei vizibile
(``labelColumn``).

Valorile pot fi filtrate utilizând ``preFilterColumn`` și
``preFilterValue``. Exemplul următor aplică prefiltre:

.. code-block:: json

   {
     "optionsTable": "milvus_taxon",
     "valueColumn": "word",
     "preFilterColumn": [
       "lang",
       "status"
     ],
     "preFilterValue": [
       "obm_taxon",
       [
         "accepted",
         "undefined"
       ]
     ],
     "orderBy": "taxon_db",
     "order": "desc"
   }

Definiția completă a listei utilizează JSON. Aceasta poate fi alcătuită cu
editorul de liste din interfața web, iar aplicația verifică validitatea
sintaxei. Dacă sintaxa nu este validă, aplicația returnează un mesaj de
eroare.

Exemplul următor enumeră proprietățile documentate:

.. code-block:: json

   {
     "list": {
       "val1": [
         "label1",
         "label2"
       ]
     },
     "optionsSchema": "e.g. public",
     "optionsTable": "a table name",
     "valueColumn": "a column from the table",
     "labelColumn": "a column from the table - optional",
     "filterColumn": "",
     "pictures": {
       "an element from the list, e.g. val1": "url-string"
     },
     "triggerTargetColumn": [
       ""
     ],
     "Function": "",
     "disabled": [
       "an element from the list, e.g. val1"
     ],
     "preFilterColumn": [
       ""
     ],
     "preFilterValue": [
       ""
     ],
     "preFilterRelation": [
       ""
     ],
     "multiselect": "true or false, default is false",
     "selected": [
       "an element from the list, e.g. val1"
     ],
     "size": "a numeric value",
     "orderBy": [
       "column or SQL expression"
     ],
     "order": [
       "ASC or DESC"
     ],
     "limit": "numeric value"
   }

.. TODO: Înlocuiți definiția completă ilustrativă cu unul sau mai multe
   exemple valide și executabile. Valorile substituente precum
   ``e.g. public`` și descrierile tipurilor reprezentate ca șiruri nu pot fi
   copiate direct într-un formular funcțional.

.. TODO: Furnizați un tabel de referință pentru fiecare proprietate
   acceptată, inclusiv tipul, valoarea implicită, valorile permise, tipurile
   de coloane ale formularului aplicabile și clienții acceptați.

.. TODO: Clarificați dacă ``Function`` este intenționat sensibil la
   majuscule și minuscule, în timp ce celelalte nume de proprietăți încep cu
   litere mici.

.. TODO: Explicați comportamentul și sintaxa acceptată pentru
   ``labelAsValue``, ``filterColumn``, ``pictures``, ``disabled``,
   ``preFilterRelation``, ``multiselect``, ``selected``, ``size``,
   ``orderBy``, ``order`` și ``limit``.

.. TODO: Confirmați dacă ``orderBy`` și ``order`` acceptă un șir sau un
   tablou. Exemplele de pe această pagină demonstrează în prezent ambele
   forme.

.. TODO: Documentați cum sunt validați identificatorii tabelelor și
   coloanelor sau expresiile SQL. Explicați în special restricțiile de
   securitate aplicate proprietății ``orderBy`` și oricărei alte proprietăți
   care poate conține o expresie SQL.

.. TODO: Explicați dacă interogările listelor aplică regulile de acces la
   nivel de rând și coloană ale proiectului și ce utilizator al bazei de date
   le execută.


Liste corelate
..............

O listă corelată utilizează valoarea selectată într-o coloană, denumită
coloană inițiatoare, pentru a determina valorile disponibile în altă
coloană. Astfel se creează o listă dependentă sau în cascadă.

Mai întâi, creați un tabel de căutare care conține relațiile dintre
nivelurile listei. De exemplu, un tabel ``animal_taxons`` ar putea descrie ce
grupuri de animale aparțin fiecărui supergrup. Vertebratele ar putea conține
amfibieni, reptile, păsări și mamifere, iar nevertebratele ar putea conține
cnidari și insecte.

În definiția listei coloanei inițiatoare, specificați coloana țintă:

.. code-block:: json

   {
     "triggerTargetColumn": [
       "affected_list_name"
     ],
     "Function": "select_list",
     "optionsSchema": "shared",
     "optionsTable": "animal_taxons",
     "valueColumn": "animal_group_name",
     "labelColumn": "animal_group_name",
     "labelAsValue": true
   }

Proprietățile utilizate în acest exemplu sunt:

``Function``
   Utilizează valoarea documentată ``select_list``.

``optionsSchema``
   Identifică schema care conține tabelul de căutare. Acest exemplu
   utilizează ``shared``.

``optionsTable``
   Identifică tabelul de căutare.

``valueColumn``
   Identifică coloana care furnizează valorile pentru lista inițiatoare.

``labelColumn``
   Identifică coloana care furnizează etichetele vizibile.

``triggerTargetColumn``
   Identifică coloana formularului a cărei listă trebuie actualizată.

În coloana afectată, definiți ce coloană a tabelului de căutare furnizează
valorile și ce coloană este utilizată pentru filtrarea lor:

.. code-block:: json

   {
     "optionsTable": "animal_taxons",
     "valueColumn": "animal_group_name",
     "labelColumn": "animal_group_name",
     "filterColumn": "animal_supergroup",
     "Function": "select_list",
     "optionsSchema": "shared"
   }

Aici, ``filterColumn`` identifică acea coloană a tabelului de căutare care
este comparată cu valoarea selectată în coloana precedentă a formularului.

Listele corelate pot conecta mai mult de două coloane ale formularului:

.. code-block:: json

   {
     "optionsSchema": "shared",
     "optionsTable": "animal_taxons",
     "filterColumn": "animal_supergroup",
     "Function": "select_list",
     "valueColumn": "animal_group_name",
     "triggerTargetColumn": [
       "species"
     ],
     "labelColumn": "animal_group_name"
   }

Într-un lanț de liste corelate, ``triggerTargetColumn`` identifică următoarea
coloană a formularului, ``filterColumn`` identifică acea coloană a tabelului
de căutare utilizată pentru potrivirea selecției precedente, iar
``valueColumn`` și ``labelColumn`` definesc lista curentă.

.. TODO: Verificați descrierile proprietăților ``valueColumn`` și
   ``labelColumn`` din coloanele inițiatoare și afectate. Adăugați un exemplu
   de tabel de căutare cu rânduri demonstrative, astfel încât direcția
   fiecărei relații să fie lipsită de ambiguitate.

.. TODO: Explicați modul în care valoarea selectată din coloana inițiatoare a
   formularului este mapată la ``filterColumn`` și dacă numele coloanei
   formularului trebuie să corespundă numelui unei coloane din tabelul de
   căutare.

.. TODO: Documentați modul în care listele corelate gestionează selecțiile
   goale, valorile părinte modificate, opțiunile duplicate, valorile părinte
   multiple, câmpurile cu selecție multiplă, câmpurile de completare automată
   și lanțurile cu mai mult de două niveluri.

.. TODO: Confirmați dacă ``optionsSchema`` trebuie să fie întotdeauna
   ``shared`` pentru listele corelate. Exemplele ulterioare de pe această
   pagină utilizează ``public``, ceea ce indică faptul că pot fi acceptate și
   alte scheme.


Exemplu de listă corelată: clădiri dintr-o localitate
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Să presupunem că un proiect colectează date despre specii care se reproduc în
cuiburi artificiale. Un tabel de căutare denumit ``tytoalba_buildings``
înregistrează clădirile din fiecare localitate. Câmpul localității trebuie să
ofere o listă cu completare automată, iar câmpul clădirii trebuie să afișeze
numai clădirile din localitatea selectată.

Mai întâi, configurați coloana localității ca un câmp cu completare automată
și identificați coloana clădirii drept țintă:

.. code-block:: json

   {
     "triggerTargetColumn": [
       "building"
     ],
     "Function": "select_list",
     "optionsSchema": "public",
     "optionsTable": "tytoalba_buildings",
     "valueColumn": "settlement"
   }

Apoi configurați coloana clădirii ca listă și filtrați-i valorile utilizând
localitatea selectată:

.. code-block:: json

   {
     "optionsTable": "tytoalba_buildings",
     "filterColumn": "settlement",
     "Function": "select_list",
     "valueColumn": "building"
   }

.. TODO: Confirmați dacă a doua definiție moștenește ``optionsSchema`` din
   coloana inițiatoare sau dacă ``optionsSchema`` a fost omis din greșeală.

.. TODO: Adăugați exemple de rânduri din ``tytoalba_buildings`` și arătați
   rezultatul vizibil după selectarea unei localități.


.. _default-values:

Valori implicite
................

Unui câmp i se poate atribui o valoare predefinită. Valorile implicite
dinamice documentate sunt:

* ``_autocomplete``;
* ``_input``;
* ``_list``;
* ``_geometry``;
* ``_login_name``;
* ``_email``;
* ``_boolean``;
* ``_attacment``;
* ``_datum``; și
* ``_auto_geometry``.

De exemplu, ``_input`` generează un câmp de introducere gol, ``_list``
completează o listă de selecție utilizând definiția listei, ``_geometry``
oferă selectarea geometriei, iar ``_datum`` oferă selectarea datei.

Consultați `un exemplu de formular
<https://openbiomaps.org/projects/checkitout/upload/?form=421&type=web>`_.

.. TODO: Confirmați lista completă și actuală a valorilor implicite dinamice
   și descrieți rezultatul fiecăreia în fiecare client acceptat.

.. TODO: Verificați dacă ``_attacment`` este scris intenționat cu un singur
   ``h`` pentru compatibilitate cu implementarea sau este o greșeală de
   tipar care trebuie înlocuită cu ``_attachment``.

.. TODO: Verificați dacă ``_datum`` este identificatorul documentat actual și
   explicați cum diferă acesta de o dată literală sau de o valoare implicită
   reprezentând data curentă.

.. TODO: Explicați cum se definesc valorile implicite literale și cum sunt
   eludate valorile care încep cu o liniuță de subliniere.

.. TODO: Clarificați când sunt evaluate valorile implicite, dacă
   utilizatorii le pot suprascrie și cum interacționează cu câmpurile fixate,
   ascunse, doar în citire și afișate o singură dată.

.. TODO: Documentați ce generează ``_login_name`` și ``_email`` pentru o
   trimitere fără autentificare și dacă aceste valori trebuie considerate
   informații de identitate de încredere.


.. _api-params:

Opțiunile de afișare ale câmpului
.................................

Sunt documentate următoarele opțiuni de afișare:

``sticky``
   Utilizată în principal de aplicația mobilă. Atunci când este selectată,
   câmpul își păstrează valoarea la începerea unui rând nou.

``hidden``
   Câmpul nu este afișat.

``read only``
   Valoarea câmpului nu poate fi modificată.

``once``
   În aplicația mobilă, câmpul este afișat o singură dată pentru o listă de
   observații, la sfârșitul observației.

   Această opțiune este destinată mutării unui câmp în afara tabelului
   repetitiv din formularul web. În prezent, în formularul web se poate
   obține un rezultat similar prin utilizarea unei valori implicite.

``list elements as buttons``
   Afișează elementele listei sub formă de butoane. Pe butoane pot fi
   utilizate imagini. Imaginile trebuie definite pentru toate elementele
   listei în definiția listei.

``unfolding list``
   Oferă un flux de lucru cu listă de specii pentru aplicația mobilă. Această
   opțiune poate fi utilizată numai cu un câmp de completare automată, de
   regulă un câmp pentru denumirea științifică, atunci când formularul
   conține și un câmp pentru numărul de indivizi căruia i-a fost atribuit
   rolul semantic corespunzător în setările tabelului bazei de date.

   Aplicația mobilă afișează într-o listă denumirile speciilor selectate și
   numărul indivizilor acestora. Numerele pot fi modificate fără salvarea
   unei înregistrări separate după fiecare modificare. Prin urmare, opțiunea
   este cea mai utilă într-un formular pentru evenimente de observare, în
   care **Salvați observația** funcționează ca o salvare intermediară și nu
   golește lista de specii acumulată.

Următoarea definiție de listă asociază imagini valorilor demonstrative ale
butoanelor:

.. code-block:: json

   {
     "pictures": {
       "animals": "http://....png",
       "plants": "http://....png",
       "mushrooms": "http://....png",
       "bats": "http://....png"
     }
   }

.. TODO: Confirmați motivul pentru care această secțiune utilizează eticheta
   de referință ``api-params`` și dacă aceste opțiuni sunt reprezentate ca
   parametri API.

.. TODO: Documentați opțiunile de afișare disponibile în clienții web,
   pentru încărcarea fișierelor, API și mobili și modul în care sunt tratate
   opțiunile neacceptate.

.. TODO: Explicați dacă valorile câmpurilor ascunse și doar în citire pot fi
   modificate printr-o solicitare API directă sau prin încărcarea unui
   fișier. Restricțiile de afișare nu trebuie tratate drept controale de
   acces pe server fără validare.

.. TODO: Definiți domeniul de aplicare și ciclul de viață exacte ale unei
   valori fixate, inclusiv observațiile noi, evenimentele noi, modificările
   formularului, repornirile aplicației și utilizatorii diferiți de pe
   același dispozitiv.

.. TODO: Clarificați implementarea actuală și comportamentul prevăzut în
   formularul web al opțiunii ``once``.

.. TODO: Explicați cerințele privind URL-urile imaginilor, formatele
   acceptate, stocarea în memoria cache, autentificarea, textul alternativ și
   comportamentul atunci când o imagine nu este disponibilă. Înlocuiți
   substituenții ``http://....png`` cu exemple sigure și funcționale.

.. TODO: Documentați modul în care lista extinsă identifică acel câmp pentru
   numărul de indivizi și cum stochează, actualizează și validează
   observațiile rezultate.


Relațiile dintre coloane
........................

Relațiile dintre coloane verifică sau modifică valoarea unui câmp în funcție
de valoarea altui câmp. De exemplu, un câmp pentru greutate poate fi
restricționat la un interval numeric de la 20 la 30 atunci când câmpul pentru
sex conține ``female``:

.. code-block:: text

   (sex=female) {minmax(20:30)}

Consultați `un exemplu de formular
<https://openbiomaps.org/projects/checkitout/upload/?form=938&type=web>`_.

.. TODO: Explicați unde sunt configurate relațiile în interfața de
   administrare și dacă o relație aparține câmpului verificat sau câmpului
   care o declanșează.

.. TODO: Documentați când sunt evaluate relațiile în formularele web,
   încărcările de fișiere, solicitările API și aplicațiile mobile și dacă
   validarea este repetată pe server.

.. TODO: Explicați cum sunt combinate relațiile multiple, cum sunt
   soluționate conflictele și dacă ordinea evaluării este semnificativă.


Pseudocoloane
.............

Coloanele din alte formulare de încărcare pot fi adăugate utilizând următorul
format:

.. code-block:: text

   form-name:column1,column2,columnN

Coloanele enumerate apar după coloana care conține această definiție.
Valorile introduse în pseudocoloane sunt încărcate utilizând definiția
celuilalt formular. Astfel, datele pot fi trimise în două tabele într-un
singur flux.

.. TODO: Explicați unde este introdusă definiția pseudocoloanelor și
   adăugați un exemplu complet care utilizează două formulare și două tabele
   destinație corelate.

.. TODO: Documentați cum sunt legate, ordonate, validate, confirmate și
   anulate înregistrările scrise prin cele două formulare. Clarificați ce se
   întâmplă dacă o inserare reușește, iar cealaltă eșuează.

.. TODO: Explicați dacă pseudocoloanele acceptă pseudoformulare imbricate,
   fișiere atașate, geometrie, reguli de acces, versiuni publicate ale
   formularelor, încărcări de fișiere, API-uri și aplicații mobile.

.. TODO: Clarificați modul în care sunt gestionate conflictele de denumire și
   câmpurile obligatorii din formularul referit.


Definirea limbajului relațiilor
-------------------------------

Sintaxa generală documentată a limbajului relațiilor este:

.. code-block:: text

   (rel_field=rel_statement) {rel_type(rel_value)}, (rel_field=rel_statement) {rel_type(rel_value)}, ...

Interpretarea prevăzută este:

.. code-block:: text

   IF another field (rel_field) matches rel_statement,
   THEN apply rel_type with rel_value to the current field.

``rel_type`` este o funcție asociată tipului câmpului curent. Funcțiile
documentate sunt:

``year``
   Pentru câmpurile de dată, extrage componenta anului dintr-un șir de dată.

``minmax``
   Pentru câmpurile text sau numerice, efectuează o verificare a intervalului
   minim și maxim.

``obligatory``
   Pentru orice tip de câmp, modifică dacă respectivul câmp curent este
   obligatoriu.

``inequality``
   Pentru orice tip de câmp, compară câmpul corelat și câmpul curent folosind
   un operator de comparație acceptat. O comparație nereușită produce o
   eroare de validare.

O instrucțiune cu expresie regulată începe cu ``!!``, urmat de o expresie
regulată, de exemplu:

.. code-block:: text

   !!^(\d{2})$

Atunci când ``rel_statement`` este o expresie regulată, ``rel_value`` poate
utiliza o funcție de înlocuire bazată pe valoarea potrivită:

``.``
   Înlocuiește valoarea câmpului curent cu șirul care a corespuns în
   ``rel_field``.

``.+``
   Adaugă valoarea câmpului curent la sfârșitul șirului care a corespuns în
   ``rel_field``.

``+.``
   Adaugă șirul care a corespuns în ``rel_field`` la sfârșitul valorii
   câmpului curent.

Pentru o relație ``inequality``, expresiile documentate utilizează ``+``
pentru valoarea potrivită din ``rel_field`` și ``.`` pentru valoarea câmpului
curent:

.. code-block:: text

   +<.
   +<=.
   +>=.
   +=.
   +<>.

Pentru alte tipuri de relații, ``rel_value`` poate conține altă valoare sau
poate fi ignorată, în funcție de funcție.

.. TODO: Verificați gramatica formală prezentată mai sus în raport cu
   analizorul actual. Descrierea originală utiliza atât notația
   ``rel_type=rel_value``, cât și ``rel_type(rel_value)``, în timp ce toate
   exemplele utilizează ultima variantă.

.. TODO: Furnizați o listă completă a funcțiilor de relație acceptate și a
   tipurilor de câmp, argumentelor, valorilor returnate și comportamentului
   la eroare pentru fiecare. Exemplele de mai jos utilizează ``set``, dar
   aceasta nu este inclusă în lista funcțiilor documentate.

.. TODO: Documentați regulile de eludare și citare pentru numele câmpurilor
   și valorile care conțin spații, virgule, paranteze, acolade, semne egal,
   caractere non-ASCII sau metacaractere ale expresiilor regulate.

.. TODO: Confirmați motorul de expresii regulate acceptat și explicați
   grupurile de capturare, sintaxa de înlocuire, delimitatorii,
   modificatorii, comportamentul Unicode și tratarea expresiilor nevalide.

.. TODO: Clarificați semnificația operatorilor de înlocuire ``.``, ``.+`` și
   ``+.`` și adăugați exemple testate care să arate valorile rezultate.

.. TODO: Confirmați dacă ``<>`` înseamnă „diferit” și dacă este acceptat și
   ``!=``.

.. TODO: Explicați cum sunt comparate datele, șirurile numerice, valorile
   nule și separatorii zecimali specifici setărilor regionale.


Exemple de relații
..................

Transformarea unui câmp în câmp obligatoriu
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Pe coloana ``tarsus_length``:

.. code-block:: text

   (clutch_size=!!^([123])$) {obligatory(1)}

Aceasta face ca ``tarsus_length`` să fie obligatorie atunci când
``clutch_size`` este ``1``, ``2`` sau ``3``.

.. TODO: Confirmați dacă expresia regulată permite în mod intenționat numai
   valori formate dintr-un singur caracter și dacă ``clutch_size`` este
   tratată ca text sau număr.


Compararea a două date
~~~~~~~~~~~~~~~~~~~~~~

Pe coloana ``end_date``:

.. code-block:: text

   (found_date=!!^(.+)$) {inequality(+>=.)}

Dacă ``found_date`` nu este goală, relația verifică dacă ``end_date`` este
mai mare sau egală cu ``found_date``. Un rezultat fals produce o eroare de
încărcare.

.. TODO: Verificați direcția comparației. Conform substituenților
   documentați, ``+>=.`` pare să însemne
   ``found_date >= end_date``, ceea ce intră în conflict cu descrierea
   însoțitoare, conform căreia ``end_date`` trebuie să fie mai mare sau egală
   cu ``found_date``. Înlocuiți exemplul numai după testarea analizorului.


Adăugarea unui an la o dată
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Pe un câmp de dată care nu conține un an:

.. code-block:: text

   (year=!!^(d{4})$) {set(.)}

Dacă coloana ``year`` nu este goală și conține patru cifre, câmpul de dată
este actualizat cu anul respectiv.

.. TODO: Verificați acest exemplu. O expresie regulată pentru patru cifre ar
   utiliza în mod obișnuit ``\d{4}``, dar expresia documentată este
   ``d{4}``. Confirmați dacă bara oblică inversă s-a pierdut în timpul
   formatării documentației.

.. TODO: Explicați cum combină ``set(.)`` anul cu valoarea existentă a datei.
   Exemplul actual nu specifică în mod clar formatul de intrare sau valoarea
   rezultată.


Solicitarea unui număr de inel
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Pe câmpul ``ring_number``:

.. code-block:: text

   (recapture=1) {obligatory(1)}

Dacă ``recapture`` are valoarea ``1``, ``ring_number`` devine obligatoriu.


Solicitarea unei denumiri alternative
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Pe coloana ``english_name``:

.. code-block:: text

   (scientific_name=!!(^$)) {obligatory(1)}

Dacă ``scientific_name`` este goală, ``english_name`` devine obligatorie.

.. TODO: Confirmați dacă parantezele din jurul ``^$`` sunt obligatorii sau
   doar creează un grup de capturare.


Setarea unei valori în funcție de un număr
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Pe câmpul ``amount_type``:

.. code-block:: text

   (number_of_individuals>50) {set(estimated value)},(egyedszam<=50) {set(exact value)}

Dacă numărul de indivizi este mai mare de 50, ``amount_type`` este setat la
``estimated value``. Dacă este cel mult 50, ``amount_type`` este setat la
``exact value``.

.. TODO: Verificați sintaxa condițională. Gramatica generală documentează
   ``rel_field=rel_statement``, dar acest exemplu plasează ``>`` și ``<=``
   între câmp și valoare.

.. TODO: Confirmați dacă ``egyedszam`` trebuie să fie
   ``number_of_individuals``. Exemplul utilizează în prezent nume de câmp
   diferite pentru cele două ramuri.

.. TODO: Explicați dacă valorile care conțin spații, precum
   ``estimated value``, trebuie citate sau eludate.

.. TODO: Adăugați exemple testate pentru ``minmax``, ``year``, înlocuirea
   prin expresii regulate, mai multe condiții aplicate unui singur câmp și
   relațiile care implică valori goale sau nule.
