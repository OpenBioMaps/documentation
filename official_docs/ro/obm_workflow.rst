.. _data-flow-database-integration:

Fluxul de date OpenBioMaps și integrarea bazei de date
******************************************************

Această pagină descrie modul în care OpenBioMaps conectează configurația
proiectului, obiectele bazei de date PostgreSQL, metadatele, fluxurile de
încărcare, regulile de acces, interogările și clienții externi.

Este destinată dezvoltatorilor, administratorilor de server și
administratorilor de proiect cu experiență care trebuie să înțeleagă
implementarea tehnică din spatele fluxului de gestionare a datelor disponibil
utilizatorilor. Pentru o introducere generală privind colectarea și
gestionarea datelor, consultați:

* :doc:`Noțiuni introductive <getting_started>`;
* :doc:`Colectarea datelor <data_collection>`;
* :doc:`Gestionarea datelor <data_management>`; și
* :doc:`Accesul la date <data_access>`.

Detaliile de implementare descrise aici pot varia între versiunile
OpenBioMaps și configurațiile proiectelor. Înainte de modificarea directă a
obiectelor bazei de date, examinați metadatele, triggerele, vizualizările,
regulile de acces și codul-sursă actuale ale proiectului. Testați modificările
structurale într-un proiect separat și creați o copie de siguranță adecvată
înainte de aplicarea lor asupra datelor de producție.


Prezentare generală tehnică
===========================

Un flux de date OpenBioMaps obișnuit conține următoarele etape tehnice:

#. Un administrator de proiect definește tabelele, coloanele, relațiile și
   metadatele OpenBioMaps din PostgreSQL.
#. Formularele de încărcare expun coloanele selectate clienților web, pentru
   încărcarea fișierelor, API sau mobili.
#. Un client trimite înregistrări și, acolo unde este cazul, fișiere atașate
   și metadate privind încărcarea.
#. OpenBioMaps validează și transformă valorile trimise conform definiției
   formularului.
#. Aplicația inserează valorile acceptate în tabelul destinație și
   înregistrează informații despre încărcare.
#. Triggerele bazei de date sau activitățile în fundal pot întreține
   istoricul, regulile de acces, datele taxonomice, valorile derivate și alte
   structuri specifice proiectului.
#. Șabloanele de interogare combină tabelele proiectului cu fragmentele pentru
   controlul accesului și module.
#. Datele rezultate pot fi afișate prin aplicația web sau accesate prin
   exporturi, API-uri, clienți SQL și alte integrări.
#. Copiile de siguranță, arhivele și politica proiectului determină modul în
   care datele și configurația asociată sunt păstrate.

Nu fiecare proiect utilizează toate aceste etape. De exemplu, un proiect mic
poate utiliza un singur tabel de observații și un singur formular web, în
timp ce un proiect de monitorizare poate utiliza tabele separate pentru
situri, evenimente, observații, taxoni, fișiere atașate și rezultate ale
validării.


Backend PostgreSQL
==================

OpenBioMaps stochează datele proiectului în PostgreSQL și utilizează în mod
obișnuit PostGIS pentru datele spațiale. Baza de date conține atât obiecte
PostgreSQL obișnuite, cât și metadate OpenBioMaps care descriu modul în care
aplicația trebuie să utilizeze obiectele respective.

Existența unui tabel sau a unei coloane PostgreSQL nu face prin ea însăși ca
obiectul respectiv să fie disponibil în OpenBioMaps. Metadatele
corespunzătoare trebuie să identifice obiectul și să descrie rolul acestuia în
proiect.


Tabelele bazei de date și metadatele
------------------------------------

Tabelele create prin interfața de administrare a proiectului sunt create în
PostgreSQL și înregistrate în metadatele OpenBioMaps. Tabelele înregistrate
pot fi apoi utilizate de formularele de încărcare, șabloanele de interogare,
module, instrumentele administrative și alte componente ale aplicației.

Un tabel sau o vizualizare creată cu un client SQL nu este înregistrată
automat. Aceasta trebuie adăugată în metadatele OpenBioMaps relevante înainte
ca aplicația să o poată utiliza în siguranță și în mod consecvent.

Interfața de administrare trebuie preferată pentru operațiunile acceptate
asupra tabelelor, deoarece poate actualiza atât obiectul PostgreSQL, cât și
metadatele asociate. Modificările SQL directe pot lăsa metadate, formulare,
interogări, triggere sau module care fac trimitere la un obiect care nu mai
există.

Pentru mai multe informații, consultați
:ref:`Tabelele și coloanele bazei de date <database-columns>`.

.. TODO: Documentați tabelele și coloanele exacte ale metadatelor utilizate
   pentru înregistrarea unui tabel sau a unei vizualizări a proiectului în
   versiunea OpenBioMaps actuală.

.. TODO: Adăugați o procedură acceptată pentru înregistrarea unui tabel sau a
   unei vizualizări PostgreSQL existente fără recrearea acesteia.

.. TODO: Verificați ce se întâmplă cu metadatele OpenBioMaps atunci când un
   tabel înregistrat este redenumit sau șters direct prin SQL. Nu vă bazați
   pe curățarea automată a metadatelor înainte ca acest comportament să fie
   testat pentru versiunea actuală.


Descrierile tabelelor
---------------------

Un tabel înregistrat poate avea o descriere inteligibilă pentru utilizatori.
Descrierile tabelelor și coloanelor fac parte din metadatele proiectului și
trebuie să explice semnificația, proveniența, unitățile, valorile așteptate și
utilizarea prevăzută a datelor.

Descrierile sunt recomandate insistent chiar și atunci când nu sunt
obligatorii din punct de vedere tehnic. O structură a bazei de date care
poate fi înțeleasă numai pe baza identificatorilor săi SQL este dificil de
întreținut, schimbat și reutilizat.

Pentru recomandări privind metadatele și proveniența, consultați
:doc:`Gestionarea datelor <data_management>` și
:doc:`Politica privind datele <data_policy>`.


Coloanele bazei de date
-----------------------

Un tabel al proiectului este alcătuit din coloane de date obișnuite și, acolo
unde este necesar, coloane de sistem OpenBioMaps. PostgreSQL determină tipul
fizic al datelor, constrângerile și stocarea fiecărei coloane. Metadatele
OpenBioMaps determină modul în care aplicația interpretează și utilizează
coloana.


Coloane de sistem
.................

Tabelele create de OpenBioMaps conțin în mod obișnuit coloane cu prefixul
``obm_``. În funcție de versiunea OpenBioMaps și de configurația proiectului,
acestea pot include câmpuri pentru:

``obm_id``
   Identificatorul intern al unei înregistrări.

``obm_geometry``
   Geometria spațială asociată înregistrării.

``obm_uploading_id``
   O referință la încărcarea prin care a fost creată înregistrarea.

``obm_validation``
   Informații asociate validării.

``obm_comments``
   Comentarii sau adnotări asociate înregistrării.

``obm_modifier_id``
   Informații care identifică un utilizator sau un proces care a modificat
   înregistrarea.

``obm_files_id``
   O referință sau referințe asociate fișierelor atașate încărcate.

Definiția unui tabel de bază poate semăna cu exemplul următor:

.. code-block:: sql

   CREATE TABLE public.test_table (
       obm_id integer
           DEFAULT nextval(
               'public.test_table_obm_id_seq'::regclass
           )
           NOT NULL,
       obm_geometry public.geometry,
       obm_uploading_id integer,
       obm_validation numeric,
       obm_comments text[],
       obm_modifier_id integer,
       obm_files_id character varying(32),
       CONSTRAINT enforce_dims_obm_geometry
           CHECK (public.st_ndims(obm_geometry) = 2),
       CONSTRAINT enforce_srid_obm_geometry
           CHECK (public.st_srid(obm_geometry) = 4326)
   );

Acest exemplu este ilustrativ și nu trebuie considerat schema autoritară
pentru fiecare instalare. Tipurile coloanelor, constrângerile, gestionarea
fișierelor atașate, definițiile secvențelor și setările sistemelor de
referință spațială pot varia între versiuni și proiecte.

Nu ștergeți sau redenumiți o coloană ``obm_`` doar pentru că pare
neutilizată. Prelucrarea încărcărilor, triggerele, modulele, regulile de
acces, istoricul, interogările sau clienții externi pot depinde de aceasta.

.. TODO: Generați o referință autoritară pentru fiecare coloană de sistem
   creată de interfața de administrare actuală. Pentru fiecare coloană,
   documentați tipul PostgreSQL, posibilitatea de a avea valoarea nulă,
   valoarea implicită, constrângerile, referințele și componentele aplicației
   care o utilizează.

.. TODO: Verificați dacă toate coloanele ``obm_`` enumerate sunt obligatorii
   în fiecare tabel gestionat sau dacă unele sunt opționale și create numai
   pentru fluxurile de lucru selectate.

.. TODO: Documentați modelul actual pentru fișierele atașate și confirmați
   dacă ``obm_files_id`` conține un identificator, mai mulți identificatori
   sau o referință la alt tabel.


Tipuri PostgreSQL și tipuri OpenBioMaps
.......................................

Un tip de date PostgreSQL descrie modul în care este stocată o valoare și
operațiunile bazei de date care pot fi efectuate asupra acesteia. Printre
exemple se numără ``text``, ``integer``, ``date``, ``timestamp``, tablourile
și tipurile de geometrie PostGIS.

Un tip de coloană OpenBioMaps sau un rol semantic descrie modul în care
aplicația utilizează coloana. De exemplu, o coloană poate reprezenta:

* o valoare generală a datelor;
* o denumire științifică;
* o denumire alternativă a unui taxon;
* o dată a observației;
* un număr de indivizi;
* o geometrie;
* o coordonată;
* o citare; sau
* un fișier atașat.

Numai coloanele înregistrate care sunt puse la dispoziție prin metadatele
OpenBioMaps pot fi selectate de componentele aplicației, precum formularele
de încărcare și interfețele de interogare.

Tipul PostgreSQL și rolul semantic OpenBioMaps trebuie să fie compatibile.
Atribuirea unui rol semantic nu transformă tipul fizic al datelor și nu
validează automat valorile existente.

.. TODO: Adăugați un tabel de compatibilitate care să mapeze fiecare tip
   semantic OpenBioMaps la tipurile PostgreSQL acceptate și la funcțiile sau
   modulele de bază care îl utilizează.

.. TODO: Documentați dacă atribuirea sau modificarea unui tip semantic
   afectează formularele de încărcare existente, șabloanele de interogare,
   clienții mobili sau definițiile formularelor stocate în memoria cache.


Identificatorii coloanelor și denumirile vizibile
.................................................

Identificatorii PostgreSQL trebuie să utilizeze litere mici, numere și
caractere de subliniere. Evitați spațiile, caracterele cu diacritice,
identificatorii citați și alte caractere speciale. Metadatele OpenBioMaps pot
asocia unei coloane o denumire vizibilă separată, astfel încât un
identificator adecvat pentru baza de date nu trebuie să fie afișat direct
utilizatorilor.

De exemplu, o coloană a bazei de date poate fi denumită
``observation_date``, în timp ce denumirea sa vizibilă este afișată ca
``Observation date`` sau echivalentul tradus al acesteia.

O denumire vizibilă care începe cu prefixul ``str_`` poate fi utilizată drept
cheie de traducere acolo unde este acceptată localizarea specifică
proiectului. Aplicația client afișează traducerea disponibilă pentru limba sa
curentă, aplicând comportamentul de rezervă configurat atunci când lipsește o
traducere.

Redenumirea numai a denumirii vizibile nu redenumește coloana PostgreSQL.
Redenumirea coloanei PostgreSQL poate întrerupe formularele, interogările,
triggerele, vizualizările, modulele, exporturile și clienții externi.

Pentru mai multe informații despre traducerile locale, consultați
:ref:`Traduceri locale <localisation>`.

.. TODO: Documentați comportamentul de rezervă exact atunci când lipsește o
   cheie de traducere ``str_`` sau o traducere pentru limba activă.

.. TODO: Confirmați ce clienți utilizează denumirile vizibile și care expun
   identificatorii PostgreSQL neprelucrați în formulare, exporturi,
   răspunsurile API sau mesajele de eroare.


Ordinea coloanelor
..................

PostgreSQL păstrează ordinea fizică a coloanelor în definițiile tabelelor,
dar nu oferă o operațiune simplă și acceptată pentru reordonarea coloanelor
existente. Metadatele OpenBioMaps și formularele de încărcare pot defini o
ordine de prezentare independentă de ordinea fizică din baza de date.

Ordinea la nivel de proiect poate fi utilizată în mod implicit de afișările
datelor și de formulare. Un formular individual de încărcare poate suprascrie
ordinea respectivă pentru propriul flux de lucru. Dacă nu este definită nicio
ordine la nivelul aplicației, interfața poate utiliza ordinea bazei de date
sau a metadatelor.

Nu recreați un tabel de producție numai pentru a modifica ordinea vizibilă a
coloanelor sale, cu excepția cazului în care există o cerință tehnică
verificată. Recrearea unui tabel poate afecta:

* secvențele și valorile implicite;
* cheile primare și externe;
* indecșii și constrângerile;
* proprietatea și privilegiile;
* triggerele și regulile;
* comentariile și metadatele;
* vizualizările și vizualizările materializate;
* tabelele regulilor de acces;
* formularele de încărcare și șabloanele de interogare; și
* aplicațiile externe.

Utilizați setările OpenBioMaps pentru ordinea de prezentare acolo unde este
posibil.

.. TODO: Confirmați ordinea de rezervă exactă utilizată de fiecare interfață
   web, API, de export și mobilă atunci când nu este configurată o ordine
   explicită a coloanelor.


Introducerea datelor
====================

Datele proiectului pot intra în PostgreSQL prin fluxurile de încărcare
OpenBioMaps sau prin operațiuni directe asupra bazei de date. Aceste căi nu
sunt echivalente.


Fluxurile de încărcare OpenBioMaps
----------------------------------

Formularele de încărcare definesc tabelul destinație, coloanele expuse,
câmpurile obligatorii, controalele datelor introduse, valorile implicite,
regulile de validare, clienții acceptați și setările de acces.

În funcție de configurație, un formular poate fi utilizat prin:

* o interfață web pentru introducerea datelor;
* un flux pentru încărcarea fișierelor;
* API-ul OpenBioMaps;
* o aplicație mobilă; sau
* alt client compatibil.

O inserare obișnuită bazată pe formular are următoarele etape:

#. Clientul obține sau afișează definiția formularului.
#. Contribuitorul introduce sau încarcă valorile.
#. Aplicația validează structura și valorile trimise.
#. Avertismentele sau erorile necritice de validare sunt prezentate acolo
   unde această funcționalitate este acceptată.
#. Valorile acceptate sunt scrise în tabelul destinație.
#. Sunt înregistrate metadatele privind încărcarea.
#. Fișierele atașate și asocierile acestora sunt stocate acolo unde este
   cazul.
#. Triggerele bazei de date efectuează operațiunile ulterioare configurate.

Pentru configurarea detaliată a formularelor, consultați
:doc:`Gestionarea formularelor de încărcare <upload_forms>`.


Evenimente de încărcare și proveniență
--------------------------------------

Atunci când datele sunt trimise printr-un flux de încărcare OpenBioMaps,
aplicația înregistrează informații despre încărcare în tabelul
``system.uploadings``. Înregistrările scrise într-un tabel de date gestionat
pot face trimitere la încărcarea respectivă prin ``obm_uploading_id``.

Metadatele privind încărcarea pot fi utilizate pentru asocierea
înregistrărilor cu informații precum:

* contribuitorul sau proprietarul;
* tabelul destinație;
* formularul utilizat pentru încărcare;
* momentul trimiterii;
* atribuirile accesului grupurilor;
* fișierul-sursă sau fluxul pentru introducerea datelor; și
* starea prelucrării sau finalizării.

Câmpurile exacte stocate și semnificația acestora sunt specifice versiunii. O
inserare SQL directă nu creează automat un eveniment de încărcare echivalent,
cu excepția cazului în care apelantul implementează explicit fluxul de lucru
necesar.

.. TODO: Documentați schema actuală completă a tabelului
   ``system.uploadings`` și identificați coloanele care reprezintă interfețe
   publice stabile și cele care sunt detalii interne de implementare.

.. TODO: Descrieți limitele tranzacției unei încărcări. Clarificați dacă
   inserarea metadatelor privind încărcarea, a înregistrărilor de date, a
   fișierelor atașate și a regulilor de acces reușește sau eșuează în cadrul
   unei singure tranzacții.

.. TODO: Documentați modul în care sunt reprezentate încărcările întrerupte,
   încărcările preliminare, rândurile respinse, încărcările finalizate și
   încărcările șterse.


Validare și transformare
------------------------

Validarea poate avea loc în mai multe niveluri:

* controalele formularelor pe client;
* prelucrarea încărcărilor pe server;
* tipurile și constrângerile PostgreSQL;
* triggerele bazei de date;
* activitățile în fundal; și
* revizuirea ulterioară de către custode.

Validarea pe client îmbunătățește utilizabilitatea, dar nu trebuie tratată
drept limită de securitate. Valorile primite prin API, încărcări de fișiere
sau conexiuni directe la baza de date necesită o validare adecvată pe server.

Transformările pot normaliza valori, construi geometria, soluționa denumiri
taxonomice, atribui valori implicite sau deriva alte câmpuri. Dacă o
transformare modifică semnificația științifică a datelor trimise, proiectul
trebuie să păstreze valoarea originală sau suficiente informații de
proveniență pentru reconstituirea modificării.

Pentru prelucrarea în fundal, consultați :doc:`Activități în fundal <jobs>`.


Introducerea directă prin SQL
-----------------------------

Utilizatorii autorizați ai bazei de date pot insera sau importa înregistrări
cu ajutorul clienților și instrumentelor PostgreSQL, precum ``COPY``. Acest
lucru poate fi util pentru migrarea în bloc controlată sau pentru repararea
administrativă a datelor.

De exemplu, PostgreSQL permite importarea datelor prin ``COPY FROM``.
Consultați `documentația PostgreSQL pentru COPY
<https://www.postgresql.org/docs/current/sql-copy.html>`_.

Operațiunile SQL directe pot eluda comportamentul la nivelul aplicației,
inclusiv:

* validarea prin formularul de încărcare;
* crearea automată a metadatelor privind încărcarea;
* prelucrarea fișierelor atașate;
* atribuirea regulilor de acces;
* informațiile privind istoricul sau auditul;
* transformările specifice proiectului;
* notificările; și
* gestionarea erorilor la nivelul aplicației.

Triggerele bazei de date sunt executate în continuare, cu excepția cazului în
care sunt dezactivate, dar comportamentul lor poate depinde de valori
furnizate în mod normal de aplicație. Prin urmare, o înregistrare inserată
fără ``obm_uploading_id`` sau alt câmp așteptat poate produce metadate sau
reguli de acces incomplete.

La importarea directă a datelor, cea mai bună practică este crearea unei
încărcări goale, atribuirea ulterioară a identificatorului încărcării
(``obm_uploading_id``) datelor încărcate și specificarea metodei de încărcare
directă și a sursei în metadatele încărcării.

Înaintea unui import direct:

#. examinați tabelul destinație, constrângerile, triggerele și regulile;
#. determinați dacă este necesară o înregistrare de încărcare
   corespunzătoare;
#. validați și transformați explicit datele-sursă;
#. utilizați o tranzacție acolo unde este cazul;
#. testați importul într-un proiect care nu este de producție;
#. verificați accesul la nivel de rând și coloană după inserare;
#. verificați fluxurile pentru istoric, fișiere atașate și date taxonomice;
   și
#. înregistrați sursa și transformarea datelor importate.

Nu dezactivați triggerele doar pentru a permite reușita unui import fără a le
înțelege mai întâi scopul. Triggerele pentru controlul accesului, istoric sau
integritate pot fi esențiale pentru securitate.

.. TODO: Furnizați o procedură acceptată de import în bloc care creează
   metadate și reguli de acces compatibile privind încărcarea, păstrând în
   același timp avantajele de performanță ale comenzii PostgreSQL ``COPY``.

.. TODO: Documentați serviciul aplicației sau API-ul care trebuie preferat în
   locul SQL direct pentru integrările automatizate.


Triggere, reguli și prelucrarea derivată
=======================================

Proiectele OpenBioMaps pot utiliza triggere și reguli PostgreSQL pentru
întreținerea unui comportament specific proiectului atunci când
înregistrările sunt inserate, actualizate sau șterse.

Fluxurile documentate bazate pe triggere includ:

* întreținerea listelor de taxoni;
* istoricul înregistrărilor;
* regulile de acces la nivel de rând; și
* validarea sau valorile derivate specifice proiectului.

Un trigger funcționează în cadrul unei tranzacții a bazei de date și poate
respinge sau modifica o schimbare. O activitate în fundal rulează în mod
normal separat și este mai adecvată pentru prelucrări de lungă durată,
programate, reîncercabile sau care necesită multe resurse.

Distincția este importantă:

``Constrângere``
   Impune un invariant al bazei de date și respinge valorile care nu îl
   respectă.

``Trigger``
   Se execută automat ca parte a unei modificări a bazei de date.

``Regulă``
   Rescrie sau redirecționează operațiunile PostgreSQL selectate, inclusiv
   operațiunile asupra vizualizărilor configurate.

``Activitate în fundal``
   Se execută separat, conform unui program sau după inițierea manuală.

``Validarea aplicației``
   Verifică sau transformă valorile în fluxul aplicației OpenBioMaps.

Aceeași cerință nu trebuie implementată în mod inconsecvent în mai multe
niveluri. Dacă sunt necesare mai multe niveluri, responsabilitățile și
comportamentul lor în caz de eroare trebuie documentate.

Pentru administrarea triggerelor, consultați
:ref:`Funcții <trigger-functions>`.

.. TODO: Documentați ordinea de execuție și dependențele triggerelor standard
   OpenBioMaps.

.. TODO: Identificați triggerele standard create automat pentru un tabel nou
   al proiectului și pe cele care necesită o acțiune explicită a
   administratorului.

.. TODO: Definiți o metodă acceptată pentru testarea triggerelor și
   examinarea efectelor acestora înainte de activarea lor în mediul de
   producție.


Integrarea regulilor de acces
=============================

Accesul la datele proiectului poate fi controlat prin valori implicite la
nivel de proiect, reguli la nivel de rând, restricții la nivel de coloană,
apartenența la grupuri și roluri administrative.

Un flux de acces la nivel de rând conectează în mod obișnuit:

* valoarea ``obm_id`` a înregistrării;
* o valoare ``row_id`` corespunzătoare dintr-un tabel de reguli al
  proiectului;
* numele tabelului destinație;
* atribuirile pentru citire și scriere;
* o valoare a sensibilității; și
* metadatele privind încărcarea sau proprietarul.

Un trigger pentru regulile de acces poate deriva atribuirile din formularul
de încărcare și din intrarea asociată din ``system.uploadings``.
Înregistrările create direct prin SQL nu dețin neapărat metadatele necesare
acestei derivări.

Un șablon de interogare trebuie să includă și fragmentele corespunzătoare
pentru controlul accesului. Regulile corecte din baza de date nu protejează
datele dacă o interogare a aplicației sau o conexiune externă le eludează.

Pentru modelul de acces, consultați :doc:`Accesul la date <data_access>`.
Pentru configurarea șabloanelor de interogare, consultați
:ref:`Setările interogărilor SQL <sql-query-settings>`.

.. TODO: Documentați algoritmul autoritar de soluționare a permisiunilor, de
   la setările proiectului până la asocierile cu tabelul de reguli și
   restricțiile coloanelor.

.. TODO: Verificați dacă, pentru fiecare interfață acceptată, controlul
   accesului este aplicat în PostgreSQL, în interogările generate de
   aplicație sau în ambele locuri.

.. TODO: Adăugați exemple testate care compară o inserare bazată pe formular
   cu o inserare SQL directă într-un proiect restricționat la grupuri.


Ieșirea datelor
===============

OpenBioMaps poate expune datele proiectului prin interfața sa web, hărți,
API-uri, exporturi, rezultate salvate și clienți externi ai bazei de date.
Fiecare cale trebuie evaluată separat din punctul de vedere al controlului
accesului, metadatelor, denumirii câmpurilor și formatului de ieșire.


Interogări web și hărți
-----------------------

Aplicația web utilizează șabloane de interogare SQL configurate pentru
alcătuirea rezultatelor textuale și spațiale ale interogărilor. Șabloanele
pot include substituenți pentru:

* câmpurile selectate;
* filtrarea geometrică;
* filtre suplimentare ale modulelor;
* asocieri taxonomice;
* metadatele privind încărcarea;
* asocieri cu regulile de acces; și
* alte fragmente SQL specifice proiectului.

Straturile MapServer pot utiliza interogări generate dinamic pentru a reda pe
o hartă aceleași date ale proiectului. Interogarea PostgreSQL, fișierul
MapServer mapfile, stratul hărții web și configurația interogării OpenBioMaps
trebuie să rămână consecvente.

O interogare configurată incorect poate omite înregistrări, duplica rânduri,
expune câmpuri restricționate sau eluda o asociere prevăzută cu regulile de
acces. Fiecare configurație de interogare trebuie testată ca:

* vizitator neautentificat;
* utilizator autentificat obișnuit;
* membru al fiecărui grup relevant;
* proprietar sau contribuitor al înregistrării; și
* administrator.

Pentru detalii, consultați
:ref:`Setările interogărilor SQL <sql-query-settings>` și
:ref:`Setările hărților <map-settings>`.


Exporturi
---------

Rezultatele interogărilor sau tabelele complete pot fi exportate în
formatele acceptate. Exporturile mici pot fi generate în timpul unei
solicitări interactive, în timp ce exporturile mai mari pot fi delegate unei
activități în fundal.

Un flux de export trebuie să păstreze sau să includă:

* înregistrările și câmpurile selectate;
* filtrele aplicate;
* momentul interogării sau exportului;
* metadatele proiectului și setului de date;
* informațiile privind licența și atribuirea;
* informațiile aplicabile despre sistemul de referință al coordonatelor;
* proveniența; și
* orice condiții privind sensibilitatea sau reutilizarea pe care destinatarii
  trebuie să le înțeleagă.

Fișierele generate pot rămâne accesibile după încheierea sesiunii inițiale a
utilizatorului. Prin urmare, locația lor de stocare, permisiunile de
descărcare, expirarea și curățarea fac parte din modelul de securitate.

.. TODO: Documentați căile de export care aplică aceleași restricții la nivel
   de rând și coloană ca interfața de interogare web.

.. TODO: Documentați stocarea, denumirea, controlul accesului, expirarea și
   ștergerea fișierelor de export generate.


Accesul prin API
----------------

API-ul OpenBioMaps oferă acces programatic la operațiunile acceptate ale
proiectului. Clienții API pot prelua definițiile formularelor, trimite date,
interoga înregistrări sau efectua alte operațiuni autorizate, în funcție de
versiunea API și de domeniul de aplicare acordat.

O trimitere API care utilizează un formular de încărcare publicat trebuie să
urmeze fluxul formularului pe server. O integrare directă cu baza de date nu
este echivalentă cu o trimitere API și poate produce metadate și un
comportament al triggerelor diferite.

Pentru detalii, consultați :doc:`Documentația API <api>`.


Clienți SQL și aplicații externe
--------------------------------

Clienții SQL externi, precum QGIS, se pot conecta direct la PostgreSQL atunci
când operatorul serverului și al proiectului furnizează explicit acreditări
și acces la rețea.

Accesul direct la baza de date poate expune mai multe informații decât
interfața web dacă privilegiile, vizualizările și securitatea la nivel de
rând PostgreSQL nu reproduc modelul de acces al aplicației. Nu trebuie
presupus că apartenența la grupuri și restricțiile coloanelor la nivelul
aplicației se aplică automat conexiunilor SQL arbitrare.

Preferați roluri dedicate doar pentru citire ale bazei de date, vizualizări
restricționate sau un API în locul partajării unui cont administrativ al
proiectului.

Pentru integrările acceptate, consultați :doc:`Clienți <clients>`.

.. TODO: Documentați privilegiile acordate utilizatorilor PostgreSQL creați
   prin profilul OpenBioMaps sau prin interfața de administrare.

.. TODO: Clarificați dacă, în implementarea actuală, clienții SQL direcți
   sunt restricționați prin securitatea la nivel de rând PostgreSQL,
   vizualizări filtrate, drepturi obișnuite sau alt mecanism.


Utilizatori, roluri și identitățile bazei de date
=================================================

Utilizatorii aplicației OpenBioMaps, rolurile proiectului, grupurile, clienții
OAuth și rolurile PostgreSQL sunt concepte conexe, dar nu sunt
interschimbabile.

``Utilizator al aplicației``
   O persoană sau un serviciu reprezentat de un cont OpenBioMaps.

``Apartenență la proiect``
   Asociază un utilizator al aplicației cu un anumit proiect și o anumită
   stare.

``Grup al proiectului``
   Grupează utilizatorii aplicației pentru accesul la formulare, date, module
   sau funcții administrative.

``Rol administrativ``
   Acordă acces la funcțiile selectate pentru administrarea proiectului.

``Client sau token OAuth``
   Autorizează o aplicație client să acționeze în domeniile de aplicare
   acordate.

``Rol PostgreSQL``
   Controlează autentificarea directă la baza de date și privilegiile SQL.

Un utilizator care poate interoga o înregistrare prin aplicația web nu deține
automat acces direct la PostgreSQL. În schimb, un rol PostgreSQL cu
privilegii extinse asupra tabelelor poate eluda restricțiile implementate
numai în aplicație.

Conturile de serviciu și integrările automatizate trebuie să utilizeze
acreditări dedicate, având numai privilegiile necesare funcției lor.
Tokenurile și parolele bazei de date nu trebuie încorporate în codul-sursă
sau partajate între aplicații fără legătură între ele.

.. TODO: Mapați utilizatorii aplicației, apartenența la proiecte, grupurile,
   permisiunile administrative, identitățile OAuth și rolurile PostgreSQL la
   tabelele și serviciile de autentificare actuale ale bazei de date.

.. TODO: Documentați crearea conturilor, schimbarea acreditărilor, revocarea,
   expirarea și comportamentul auditului pentru fiecare tip de integrare
   acceptat.


Modificări sigure ale schemei
=============================

Modificările unui tabel gestionat pot afecta atât PostgreSQL, cât și
configurația OpenBioMaps. Înainte de redenumirea, înlocuirea sau ștergerea
unui tabel sau a unei coloane:

#. identificați formularele de încărcare care utilizează obiectul;
#. căutați în șabloanele de interogare și fișierele MapServer mapfile;
#. examinați triggerele, regulile, vizualizările, indecșii, constrângerile și
   cheile externe;
#. examinați rolurile semantice ale coloanelor și metadatele proiectului;
#. examinați configurația regulilor de acces și a istoricului;
#. identificați modulele și activitățile în fundal care fac trimitere la
   obiect;
#. identificați clienții API, mobili, QGIS, R și SQL direcți;
#. creați și verificați o copie de siguranță adecvată;
#. testați migrarea într-un proiect separat;
#. definiți o procedură de revenire; și
#. validați toate interfețele acceptate după migrare.

Utilizați interfața de administrare pentru operațiunile pe care le acceptă.
Dacă este necesar SQL direct, actualizați metadatele OpenBioMaps și
configurația dependentă corespunzătoare în cadrul aceleiași migrări
controlate.

Redenumirea unui obiect nu este neapărat mai sigură decât ștergerea și
recrearea sa: ambele pot întrerupe dependențele care stochează identificatorul
original sub formă de text.

.. TODO: Creați proceduri acceptate pentru migrarea care adaugă,
   redenumește, modifică tipul sau șterge o coloană gestionată.

.. TODO: Creați o procedură acceptată pentru înlocuirea unui tabel gestionat
   cu o vizualizare și pentru anularea modificării.

.. TODO: Adăugați un raport administrativ privind dependențele, care să
   enumere formularele, șabloanele de interogare, modulele, activitățile,
   triggerele, regulile, straturile hărții și metadatele care fac trimitere la
   un tabel sau o coloană selectată.


Copii de siguranță, arhive și reproductibilitate
================================================

Un proiect OpenBioMaps complet este alcătuit din mai mult decât tabelele sale
principale de date. În funcție de instalare, restaurarea poate necesita:

* tabelele de proiect și de sistem ale bazei de date;
* secvențele, constrângerile, indecșii, triggerele și regulile;
* metadatele OpenBioMaps;
* fișierele de configurare ale proiectului;
* formularele de încărcare și versiunile acestora;
* fișierele atașate și derivatele generate;
* configurația MapServer și a hărții web;
* modulele și fișierele-sursă locale;
* activitățile în fundal și programele acestora;
* traducerile și șabloanele de mesaje; și
* acreditările sau secretele restaurate printr-un proces securizat separat.

O copie a unui singur tabel PostgreSQL poate păstra înregistrările
observațiilor, pierzând în același timp configurația necesară pentru
interpretarea, editarea, interogarea sau protejarea acestora.

Copiile de siguranță trebuie testate prin restaurare. Arhivele destinate
reutilizării pe termen lung trebuie să păstreze și documentația, licențele,
proveniența, versiunile software și suficiente informații despre schemă
pentru interpretarea datelor în afara serverului original.

Pentru considerații privind guvernanța și păstrarea, consultați
:doc:`Politica privind datele <data_policy>`.

.. TODO: Definiți setul minim de resurse ale bazei de date și sistemului de
   fișiere necesar pentru crearea și restaurarea unei copii de siguranță
   complete a proiectului.

.. TODO: Adăugați un format versionat pentru exportul proiectului, adecvat
   migrării între servere OpenBioMaps compatibile.


Lista de verificare tehnică
===========================

După crearea sau modificarea unui flux de date al proiectului, verificați
dacă:

* fiecare obiect PostgreSQL gestionat are metadatele OpenBioMaps necesare;
* coloanele de sistem au tipurile, constrângerile și valorile implicite
  așteptate;
* secvențele, cheile, indecșii, triggerele și regulile sunt valide;
* definițiile formularelor fac trimitere la coloane destinație existente;
* validarea formularului este aplicată în mod adecvat și pe server;
* metadatele privind încărcarea sunt create și asociate înregistrărilor
  inserate;
* fișierele atașate sunt asociate înregistrărilor prevăzute;
* importurile directe primesc proveniența și regulile de acces adecvate;
* triggerele pentru istoric și date taxonomice produc rezultatele așteptate;
* interogările publice și specifice grupurilor aplică restricțiile la nivel
  de rând;
* coloanele restricționate lipsesc din fiecare rezultat neautorizat;
* straturile hărții și interogările textuale returnează înregistrări
  consecvente;
* trimiterile API și mobile utilizează versiunea publicată prevăzută a
  formularului;
* rolurile SQL nu pot citi sau modifica mai multe date decât este prevăzut;
* exporturile generate sunt protejate și eliminate conform politicii;
* activitățile în fundal rulează cu dependențele necesare și cu privilegii
  minime;
* copiile de siguranță includ datele bazei de date, configurația și fișierele
  atașate acolo unde acest lucru este promis; și
* un test de restaurare reproduce un proiect funcțional și cu acces
  controlat.

Documentați versiunea OpenBioMaps testată, configurația proiectului,
utilizatorii de test, interogările și rezultatele așteptate. Repetați
verificările după actualizările aplicației, migrările schemei sau modificările
semnificative ale politicii de acces.
