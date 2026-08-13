:author: Miklós Bán
:date: 2026-08-09

.. _jobs:

Activități de fundal
********************

Activitățile de fundal sunt programe autonome care efectuează sarcini
programate sau inițiate manual pentru un proiect OpenBioMaps. Acestea sunt
adecvate pentru operații care nu trebuie să fie executate în cadrul unei
solicitări web interactive, precum validarea datelor, întreținerea,
importurile, exporturile, procesarea spațială și trimiterea notificărilor.

Activitățile sunt scrise de obicei în PHP, deși un server OpenBioMaps poate
accepta și Python, R, Bash sau un alt limbaj instalat și activat de
administratorul serverului.

Administratorii de proiect pot gestiona activitățile prin **Profile >
Project administration > Background jobs**. În funcție de permisiunile lor
și de configurația serverului, administratorii pot:

* instala activități predefinite din depozitul central de activități;
* încărca activități specifice proiectului;
* configura parametrii activităților;
* configura programările execuțiilor;
* activa sau dezactiva activitățile;
* porni manual activitățile;
* examina rezultatele execuțiilor recente; și
* edita codul sursă al activităților.

Pentru o prezentare generală a interfeței de administrare și un exemplu de
programare la nivel de sistem, consultați
:ref:`Activități de fundal <background-jobs>`.


Depozitul de activități
=======================

Activitățile OpenBioMaps predefinite sunt întreținute în
`depozitul OpenBioMaps web-app-jobs
<https://gitlab.com/openbiomaps/web-app-jobs>`_.

Depozitul se poate modifica independent de această documentație. Examinați
codul sursă și configurația versiunii selectate înainte de instalarea sau
actualizarea unei activități.

Fișierul README al depozitului descrie structura tradițională a
activităților PHP. O activitate PHP este alcătuită de obicei din două
fișiere cu același nume:

* un fișier executabil plasat în ``jobs/run/``; și
* un fișier de bibliotecă auxiliar plasat în ``jobs/run/lib/``.

Activitățile scrise în alte limbaje pot consta numai dintr-un fișier
executabil aflat în ``jobs/run/``. Structura exactă de instalare poate
depinde de versiunea OpenBioMaps și de configurația serverului.


Instalarea și configurarea unei activități
==========================================

Acolo unde această funcție este acceptată, o activitate predefinită poate fi
instalată din depozitul central prin interfața de administrare a
activităților de fundal. O activitate specifică proiectului poate fi și
încărcată sau instalată manual de un administrator de server autorizat.

După instalarea unei activități:

#. examinați codul sursă al acesteia;
#. examinați și setați toți parametrii specifici proiectului;
#. confirmați că tabelele, coloanele, modulele, șabloanele și directoarele
   menționate există;
#. utilizați **Run** pentru a executa manual activitatea;
#. așteptați finalizarea execuției;
#. examinați rezultatul și jurnalele serverului;
#. verificați toate modificările efectuate în baza de date sau în sistemul
   de fișiere; și
#. activați execuția recurentă numai după reușita testului manual.

Parametrii activităților și ipotezele privind baza de date sunt specifice
implementării. Este posibil ca o activitate creată pentru un proiect să nu
funcționeze în alt proiect fără modificări.


Programare
==========

Activitățile recurente utilizează planificatorul configurat pentru proiect.
Planificatorul de la nivelul sistemului al serverului trebuie să invoce
periodic planificatorul proiectului; în caz contrar, activitățile configurate
nu vor porni automat.

Depozitul central oferă următorul exemplu cron tradițional:

.. code-block:: console

   */5 * * * * /usr/bin/php /var/www/html/biomaps/projects/YOUR-PROJECT/jobs.php > /dev/null 2>&1

Este posibil ca această comandă să trebuiască executată ca utilizatorul
serverului web, de obicei ``www-data``. Căile, utilizatorii de execuție,
containerele și comenzile PHP diferă între instalări. În mod normal,
instalările Docker invocă planificatorul proiectului din interiorul
containerului aplicației.

Intervalul de invocare de la nivelul sistemului limitează rezoluția efectivă
a programării. De exemplu, dacă planificatorul proiectului este invocat la
fiecare cinci minute, o activitate nu poate porni în mod fiabil la fiecare
minut.

Consultați :ref:`Programarea activităților <background-jobs>` pentru
prezentarea generală a administrării și un exemplu orientat spre Docker.


Monitorizare și depanare
========================

Interfața de administrare a activităților de fundal afișează starea și
rezultatele execuțiilor recente, acolo unde această funcție este acceptată.
Informații mai detaliate pot fi disponibile în **Project administration >
Server logs**.

La diagnosticarea unei activități, verificați:

* dacă planificatorul proiectului este invocat de planificatorul sistemului;
* dacă activitatea este activată;
* dacă a sosit momentul programat pentru execuția acesteia;
* dacă o altă execuție este încă în curs;
* dacă utilizatorul care execută activitatea poate citi și scrie fișierele
  necesare;
* dacă programele și pachetele de limbaj necesare sunt instalate;
* dacă tabelele și coloanele configurate există;
* dacă privilegiile bazei de date sunt suficiente;
* dacă directoarele temporare și de export au suficient spațiu liber; și
* dacă jurnalele aplicației, activităților de fundal, PHP, containerului sau
  sistemului conțin o eroare.

O activitate se poate finaliza fără a produce rezultatul dorit dacă
configurația sa nu corespunde schemei proiectului. Validați înregistrările,
fișierele sau notificările rezultate în loc să vă bazați numai pe o stare de
ieșire care indică reușita.


Securitate
==========

Instalarea sau editarea unei activități este echivalentă cu instalarea de cod
executabil pe server. Aceste funcții trebuie limitate la administratorii de
încredere.

Înainte de instalarea unei activități personalizate sau actualizate,
verificați dacă aceasta prezintă:

* injectare SQL;
* injectarea comenzilor sistemului de operare;
* căi și permisiuni nesigure pentru fișiere;
* divulgarea datelor de autentificare ale bazei de date sau a datelor cu
  caracter personal;
* interogări nelimitate ale bazei de date;
* utilizarea nelimitată a memoriei, procesorului sau spațiului pe disc;
* solicitări de rețea nesigure;
* verificări lipsă pentru controlul accesului;
* gestionarea nesigură a atașamentelor și arhivelor; și
* execuții repetate neintenționate.

Creați o copie de siguranță adecvată înainte de a executa activități care
actualizează sau șterg date. Activitățile de export trebuie să aplice
fișierelor generate cerințele proiectului privind accesul la date și
confidențialitatea. Arhivele și rapoartele generate trebuie stocate într-o
locație protejată și eliminate atunci când nu mai sunt necesare.


Activități din depozitul central
================================

Următoarele directoare de activități sunt prezente în depozitul central.
Unele activități sunt de uz general, în timp ce altele au fost dezvoltate
pentru un anumit proiect sau flux de lucru.

Descrierile de mai jos rezumă scopul indicat de numele din depozit și de
metadatele disponibile în acesta. Comportamentul exact, parametrii de
configurare, modificările bazei de date, destinatarii notificărilor și
gestionarea erorilor trebuie verificate în codul sursă al versiunii
instalate.


Procesarea generală a datelor și fișierelor
-------------------------------------------

``clean_temp``
   Curăță datele sau fișierele temporare create de fluxurile de lucru
   OpenBioMaps. Examinați căile, tabelele, regulile de păstrare și condițiile
   de ștergere configurate înainte de a o activa. O configurație incorectă
   de curățare poate elimina fișiere sau date care sunt încă necesare.

``export_attachments``
   Creează un export din atașamentele proiectului. Această activitate poate
   fi utilizată de fluxurile de lucru care pregătesc arhive de atașamente în
   fundal. Verificați modul în care sunt selectate înregistrările, aplicate
   regulile de acces și scrise arhivele, precum și durata păstrării
   acestora.

``export_data``
   Creează un export de date în fundal. Tabelele, coloanele, filtrele,
   formatul de ieșire, verificările accesului, locația ieșirii și mecanismul
   de descărcare selectate depind de configurația și versiunea sursă a
   activității.

``intersect_data``
   Efectuează un flux de lucru pentru intersecția spațială a seturilor de
   date configurate. Verificați tabelele sursă și țintă, coloanele de
   geometrie, sistemele de referință spațială și comportamentul la
   actualizare înainte de a o executa.

``valid_list_values``
   Verifică sau procesează valorile asociate câmpurilor de tip listă
   configurate. Examinați codul sursă pentru a determina dacă valorile
   nevalide sunt numai raportate sau sunt și modificate.


Procesarea listelor de observații
---------------------------------

``observation_lists``
   Procesează listele de observații utilizând fluxul de lucru standard
   pentru listele de observații. Ipotezele sale privind baza de date și
   modul de tratare a datelor temporare trebuie verificate în raport cu
   schema proiectului.

``observation_lists_without_temp``
   Oferă o variantă de procesare a listelor de observații destinată
   fluxurilor de lucru care nu utilizează etapa standard pentru date
   temporare.

``incomplete_observation_lists``
   Procesează listele de observații incomplete. Fluxul de lucru poate
   utiliza șabloanele de mesaje ``incomplete_list_processed`` și
   ``incomplete_list_unprocessed`` pentru a raporta dacă procesarea a
   reușit. Verificați utilizarea efectivă a șabloanelor și destinatarii în
   codul sursă al versiunii instalate.


Procesare taxonomică
--------------------

``species_name_validation``
   Validează denumirile științifice utilizate de datele proiectului.
   Examinați tabelul de taxoni configurat, câmpurile sursă, regulile privind
   denumirile acceptate și dacă activitatea numai raportează problemele sau
   modifică și înregistrările.

``superspecies_autonames``
   Generează sau întreține denumirile utilizate de un flux de lucru pentru
   superspecii. Această activitate depinde de convențiile taxonomice
   specifice proiectului și nu trebuie activată fără examinarea tabelelor și
   a regulilor de denumire configurate.

``linnaeus_job``
   Implementează un flux de procesare specific proiectului, referitor la
   Linnaeus. Operația taxonomică exactă și schema necesară nu sunt descrise
   în prezentarea generală a depozitului și trebuie determinate din codul
   sursă și configurația activității.


Importuri și integrări externe
------------------------------

``iNatHarvester``
   Preia date despre observații din iNaturalist pentru importarea sau
   procesarea acestora într-un proiect OpenBioMaps. Examinați setările
   API-ului extern, asocierile taxonilor și utilizatorilor, detectarea
   duplicatelor, filtrele geografice, limitarea ratei solicitărilor și
   configurația tabelului destinație înainte de utilizare.

``hunviphab_tracklogs``
   Procesează traseele GPS pentru fluxul de lucru HunVipHab. Aceasta este o
   activitate specializată, ale cărei tabele necesare, format al traseelor
   GPS și câmpuri de ieșire trebuie confirmate din codul sursă.

``chirovox_rename``
   Efectuează o operație de redenumire pentru fluxul de lucru ChiroVox.
   Examinați codul sursă pentru a identifica fișierele sau înregistrările
   afectate, convenția de denumire și modul de gestionare a coliziunilor
   înainte de a o executa.


Întreținerea bazei de date și SQL personalizat
----------------------------------------------

``sql_daily``
   Execută instrucțiuni SQL configurate ca sarcină recurentă de întreținere
   sau procesare. Activitățile SQL pot modifica sau șterge orice date ale
   proiectului, prin urmare examinați fiecare instrucțiune, testați-o într-un
   mediu care nu este de producție și creați o copie de siguranță atunci
   când este cazul.

``sql_maintenance``
   Efectuează întreținerea PostgreSQL utilizând ``ANALYZE`` și/sau
   ``VACUUM``. Aceste operații actualizează statisticile planificatorului și
   recuperează sau fac reutilizabil spațiul de stocare asociat versiunilor
   învechite ale rândurilor. Examinați relațiile și opțiunile selectate și
   coordonați operațiile de întreținere care utilizează multe resurse cu
   administratorul serverului.


Fluxuri de lucru specifice proiectelor
--------------------------------------

``kaszalasi_bejelento``
   Implementează un flux de lucru specific proiectului pentru raportarea
   cosirii. Această variantă include procesarea notificărilor. Confirmați din
   codul sursă înregistrările afectate, șabloanele de mesaje, destinatarii și
   condițiile înainte de utilizare.

``kaszalasi_bejelento_ertesites_nelkul``
   Implementează o variantă fără notificări a fluxului de lucru pentru
   raportarea cosirii. Alte comportamente de procesare a datelor pot fi
   comune cu ``kaszalasi_bejelento`` și trebuie verificate în codul sursă.

``telepules_hozzarendeles``
   Atribuie o municipalitate sau o localitate înregistrărilor configurate.
   Este probabil ca această activitate să depindă de date spațiale și de
   câmpuri specifice proiectului. Verificați datele privind limitele,
   coloanele de geometrie, sistemele de referință spațială, regulile de
   asociere și gestionarea înregistrărilor din afara sau de pe limita unei
   municipalități.


Dezvoltare și testare
---------------------

``job_teszt``
   O activitate de testare destinată verificării instalării sau execuției
   activităților. Aceasta nu trebuie tratată drept activitate de procesare a
   datelor de producție fără examinarea codului său sursă.


Actualizarea activităților
==========================

Actualizarea unei activități poate modifica parametrii necesari, ipotezele
privind baza de date și efectele secundare ale acesteia. Înainte de a înlocui
o versiune instalată:

#. păstrați codul sursă și configurația actuală;
#. examinați modificările din depozitul central;
#. verificați dacă există migrări ale schemei sau dependențe noi;
#. dezactivați programarea recurentă;
#. instalați actualizarea într-un proiect de testare, acolo unde este
   posibil;
#. executați-o manual și examinați rezultatul; și
#. restaurați programarea numai după validare.

Modificările locale pot fi suprascrise de o actualizare din depozitul
central. Păstrați modificările specifice proiectului sub controlul
versiunilor sau întrețineți-le ca activitate personalizată separată.


Scrierea activităților personalizate
====================================

O activitate personalizată trebuie:

* să aibă un scop documentat clar;
* să valideze întreaga configurație înainte de a modifica datele;
* să utilizeze SQL parametrizat;
* să evite includerea datelor de autentificare în codul sursă;
* să înregistreze suficiente informații pentru diagnosticarea erorilor fără
  a expune date sensibile;
* să returneze o stare de ieșire diferită de zero la eșec, acolo unde această
  funcție este acceptată;
* să poată fi reexecutată în siguranță sau să documenteze clar cazurile în
  care acest lucru nu este posibil;
* să împiedice sau să gestioneze în siguranță execuțiile suprapuse;
* să utilizeze interogări limitate și limite pentru resurse;
* să curețe fișierele temporare după execuțiile reușite și nereușite; și
* să documenteze toate dependențele privind baza de date, modulele,
  executabilele și pachetele de limbaj.

Acolo unde este posibil, testați activitățile personalizate într-un proiect
separat, cu date reprezentative, înainte de a le instala în producție.
