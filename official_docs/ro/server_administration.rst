Administrarea serverului
************************

Această pagină descrie configurarea de nivel inferior a unui server
OpenBioMaps. Instalările actuale rulează în mod normal OpenBioMaps ca pe o
colecție de servicii Docker Compose. Serverul web al aplicației și mediul de
execuție PHP sunt furnizate de containerul ``app``, în timp ce MapServer și
PostgreSQL rulează în containere separate.

Exemplele de pe această pagină se bazează pe imaginea aplicației OpenBioMaps
și pe configurația Docker Compose de referință. Conținutul imaginilor și
definițiile serviciilor se pot modifica între versiuni. Comparați întotdeauna
această documentație cu fișierele livrate împreună cu versiunea implementată.

Nu stocați parole reale, secrete ale clienților, chei de criptare sau alte
date de autentificare în documentație sau într-un depozit de cod sursă.

Supervisor
==========

Supervisor este o aplicație web autonomă pentru configurare de nivel
inferior, actualizări și întreținerea proiectelor. Este instalată ca parte a
unei instalări de server OpenBioMaps și este disponibilă în mod normal la
unul dintre următoarele URL-uri:

* ``https://YOUR_SERVER/supervisor/``
* ``https://YOUR_SERVER/supervisor.php``

URL-ul exact depinde de configurația serverului și a proxy-ului invers.

Supervisor are două moduri de funcționare:

Modul sistem
  Oferă întreținere și actualizări la nivel de sistem, inclusiv gestionarea
  configurației sistemului.

Modul proiect
  Oferă actualizări ale proiectelor, crearea proiectelor și întreținerea
  bazei de date, gestionarea fișierului ``local_vars.php.inc`` și un manager
  de fișiere pentru directorul ``local`` al proiectului.

Modul proiect poate fi pus și la dispoziția administratorilor de proiect
prin interfața de administrare a proiectului.

Limitați accesul la Supervisor la administratorii de încredere. Utilizați
HTTPS și o parolă puternică și unică și luați în considerare restricții
suplimentare la nivel de rețea.

Regenerarea parolei Supervisor
------------------------------

Pe gazda Docker, parola Supervisor poate fi regenerată cu scriptul de
post-instalare:

.. code-block:: console

   cd /srv/docker/openbiomaps
   ./obm_post_install.sh update supervisor

Directorul exact de instalare poate fi diferit. Executați comanda din
directorul care conține scripturile de instalare OpenBioMaps și verificați
dacă rezultatul acesteia conține erori.

După schimbarea parolei, verificați dacă Supervisor este accesibil și stocați
noile date de autentificare într-un manager de parole adecvat.

Fișierele variabilelor de sistem
================================

OpenBioMaps utilizează fișiere cu variabile la nivel de sistem pe lângă
fișierul ``local_vars.php.inc`` al fiecărui proiect.

Imaginea aplicației include în prezent un fișier de bază la:

``/var/www/html/biomaps/root-site/server_vars.php.inc``

Imaginea Docker declară, de asemenea, ``/etc/openbiomaps`` ca volum.
Configurația sistemului gestionată de administrator este stocată în mod
normal acolo, de exemplu:

``/etc/openbiomaps/system_vars.php.inc``

Relația exactă și ordinea de încărcare pentru ``server_vars.php.inc`` și
``system_vars.php.inc`` pot varia între versiunile OpenBioMaps. Nu
presupuneți că cele două fișiere sunt interschimbabile. Utilizați Supervisor
și șabloanele furnizate împreună cu versiunea instalată și verificați
configurația efectivă după o actualizare.

Deoarece ``/etc/openbiomaps`` este montat din volumul Docker
``etc_openbiomaps`` în configurația Compose de referință, modificările
efectuate acolo persistă atunci când containerul ``app`` este înlocuit.

Secțiunile următoare descriu setările prezentate anterior în exemplul
``system_vars.php.inc``. Valorile sunt exemple și trebuie verificate pentru
instalarea efectivă.

Setări de rețea și URL
----------------------

.. list-table::
   :header-rows: 1
   :widths: 24 28 48

   * - Variabilă
     - Valoare exemplificativă
     - Descriere
   * - ``USE_NON_STANDARD_HTTP_PORTS``
     - ``false``
     - Activează suportul pentru o instalare locală care nu se află în
       spatele unui proxy și utilizează porturi HTTP nestandard. Este
       opțională și dezactivată în exemplu.
   * - ``OB_DOMAIN``
     - ``localhost/biomaps``
     - Adresa publică a serverului și calea de implementare utilizate de
       OpenBioMaps. Înlocuiți-o cu numele real al gazdei și calea reală.
       Valoarea trebuie să fie în concordanță cu configurația proxy-ului
       invers și TLS.
   * - ``POSTGRES_PORT``
     - ``5432``
     - Portul serviciului PostgreSQL utilizat de OpenBioMaps.
   * - ``GISDB_HOST``
     - ``localhost``
     - Gazda bazei de date introdusă în configurațiile proiectelor nou
       create. Într-o instalare Docker, aceasta trebuie în mod normal să fie
       un nume de rețea sau un alias Docker, precum ``gisdata``, în loc de
       ``localhost``.
   * - ``MAPSERVER_HOST``
     - ``mapserver``
     - Gazda serviciului MapServer introdusă în configurațiile proiectelor
       nou create. În mediul Compose de referință, ``mapserver`` este numele
       serviciului Docker Compose.

În interiorul unui container, ``localhost`` se referă la containerul
respectiv. Nu se referă la un alt serviciu Compose. De exemplu, containerul
``app`` trebuie să acceseze în mod normal MapServer ca ``mapserver``, iar
baza de date prin intermediul unuia dintre numele de rețea sau aliasurile
serviciului bazei de date.

Serviciul bazei de date de referință se numește ``biomaps_db`` și are
aliasurile ``biomaps`` și ``gisdata``. Șabloanele OpenBioMaps existente pot
aștepta unul dintre aceste aliasuri. Înainte de a modifica ``GISDB_HOST``,
inspectați configurația unui proiect funcțional și verificați ce nume este
așteptat de versiunea instalată.

Setări pentru directoare
------------------------

.. list-table::
   :header-rows: 1
   :widths: 24 31 45

   * - Variabilă
     - Valoare exemplificativă
     - Descriere
   * - ``OB_SYSDIR``
     - ``/var/lib/openbiomaps/``
     - Directorul de bază pentru datele persistente ale sistemului
       OpenBioMaps. Aceasta este valoarea implicită documentată și este
       opțională în exemplu.
   * - ``OB_TMP``
     - ``/var/lib/openbiomaps/tmp/``
     - Directorul utilizat pentru fișierele temporare OpenBioMaps. Este
       stocat în volumul persistent ``var_lib`` în configurația Compose de
       referință.
   * - ``OB_ROOT``
     - ``/var/www/html/biomaps/root-site``
     - Directorul rădăcină pentru documentele aplicației. Exemplul nu
       include o bară oblică la sfârșit.
   * - ``OB_ROOT_SITE``
     - ``/var/www/html/biomaps/root-site/``
     - Directorul site-ului rădăcină al aplicației. Unele părți ale codului
       aplicației necesită această formă cu o bară oblică la sfârșit.
   * - ``OB_RESOURCES``
     - ``/var/www/html/biomaps/resources/``
     - Directorul care conține resursele OpenBioMaps partajate.

Nu modificați căile fără a verifica imaginea Docker, rădăcina documentelor
Apache, montările volumelor, căile proiectelor și toate scripturile care fac
referire la acestea.

Conexiunea la baza de date a sistemului
---------------------------------------

Aceste variabile definesc conexiunea la baza de date a sistemului
OpenBioMaps. Ele sunt distincte de setările ``gisdb_*`` specifice
proiectului, documentate în ghidul de instalare a serverului.

.. list-table::
   :header-rows: 1
   :widths: 24 26 50

   * - Variabilă
     - Valoare exemplificativă
     - Descriere
   * - ``biomapsdb_user``
     - Valoare secretă specifică instalării
     - Utilizatorul PostgreSQL folosit pentru accesarea bazei de date a
       sistemului OpenBioMaps.
   * - ``biomapsdb_pass``
     - Valoare secretă specifică instalării
     - Parola utilizatorului bazei de date a sistemului. Utilizați o valoare
       aleatorie puternică și nu o includeți într-un depozit.
   * - ``biomapsdb_name``
     - Valoare specifică instalării
     - Numele bazei de date a sistemului OpenBioMaps.
   * - ``biomapsdb_host``
     - ``localhost``
     - Gazda care rulează baza de date a sistemului. În mediul Docker de
       referință, utilizați numele sau aliasul corespunzător al serviciului
       bazei de date în loc de ``localhost``, cu excepția cazului în care
       PostgreSQL rulează efectiv în containerul ``app``.
   * - ``POSTGIS_V``
     - ``2.5``
     - Marcaj istoric al versiunii PostGIS. În mod normal, nu este necesară
       setarea acestei valori și este posibil ca aceasta să nu reprezinte
       versiunea instalată în prezent.

Fișierul Compose de referință utilizează imaginea
``openbiomaps/database:pg17-3.5``. Numele imaginii indică o combinație
PostgreSQL/PostGIS mai nouă decât exemplul istoric ``POSTGIS_V``. Nu
utilizați ``POSTGIS_V`` pentru a determina versiunea reală a serverului.
Interogați serverul bazei de date atunci când sunt necesare informații despre
versiune.

Livrarea e-mailurilor
---------------------

.. list-table::
   :header-rows: 1
   :widths: 24 24 52

   * - Variabilă
     - Valoare exemplificativă
     - Descriere
   * - ``SENDMAIL``
     - ``smtp``
     - Metoda implicită de livrare a e-mailurilor. Valorile documentate sunt
       ``sendmail`` și ``smtp``. Un proiect poate suprascrie această setare
       în ``local_vars.php.inc``.

Atunci când este selectat SMTP, configurați gazda SMTP, autentificarea,
expeditorul, portul și setările de securitate a transportului necesare la
nivelul corespunzător al sistemului sau proiectului. Nu stocați datele de
autentificare SMTP în fișiere de configurare publice.

Cache
-----

.. list-table::
   :header-rows: 1
   :widths: 24 24 52

   * - Variabilă
     - Valoare exemplificativă
     - Descriere
   * - ``CACHE``
     - ``memcache``
     - Selectează implementarea cache utilizată de OpenBioMaps.

Imaginea aplicației de referință definește și următoarele valori implicite
ale mediului:

.. list-table::
   :header-rows: 1
   :widths: 24 24 52

   * - Variabilă de mediu
     - Valoare implicită
     - Descriere
   * - ``CACHE_HOST``
     - ``memcached``
     - Numele gazdei serviciului Memcached. Acesta corespunde numelui
       serviciului din fișierul Compose de referință.
   * - ``CACHE_PORT``
     - ``11211``
     - Portul utilizat de Memcached în rețeaua Docker.

Serviciul ``memcached`` este atașat la rețeaua privată ``obm_back`` și nu
trebuie să publice un port pe gazda Docker.

Servicii R Shiny opționale
--------------------------

.. list-table::
   :header-rows: 1
   :widths: 32 22 46

   * - Variabilă
     - Valoare exemplificativă
     - Descriere
   * - ``RSERVER_PORT_someproject``
     - ``7982``
     - Port R Shiny Server specific proiectului. Înlocuiți ``someproject``
       cu identificatorul relevant al proiectului. Configurați această
       setare numai pentru proiectele care încă utilizează integrarea R
       Shiny.

Suportul R Shiny este o integrare învechită sau opțională. Confirmați că
aceasta este acceptată de versiunea OpenBioMaps instalată înainte de a o
configura.

Limbi acceptate
---------------

.. list-table::
   :header-rows: 1
   :widths: 24 25 51

   * - Variabilă
     - Valoare exemplificativă
     - Descriere
   * - ``LANGUAGES``
     - ``en, hu, ro``
     - Lista limbilor acceptate de server, separate prin virgulă. Trebuie
       instalate fișierele relevante pentru limbi.

Această valoare la nivel de sistem este separată de selectarea limbilor la
nivel de proiect. Setările de limbă ale proiectului trebuie să utilizeze
limbi disponibile pe server.

Rapoarte automate de erori
--------------------------

.. list-table::
   :header-rows: 1
   :widths: 28 30 42

   * - Variabilă
     - Valoare exemplificativă
     - Descriere
   * - ``AUTO_BUGREPORT_ADDRESS``
     - O adresă de primire a problemelor furnizată de responsabilii
       depozitului
     - Activează integrarea cu un sistem de urmărire a problemelor printr-o
       adresă de primire. Solicitați cheia sau adresa corespunzătoare a
       problemei de la responsabilii depozitului OpenBioMaps.

Tratați adresa completă de primire ca pe un secret, deoarece orice persoană
care o obține poate crea probleme sau trimite conținut nedorit. Verificați
jurnalele și rapoartele trimise pentru a vă asigura că nu sunt incluse date
sensibile despre proiect sau utilizatori.

Secretul autentificării web
---------------------------

.. list-table::
   :header-rows: 1
   :widths: 28 28 44

   * - Variabilă
     - Valoare exemplificativă
     - Descriere
   * - ``WEB_CLIENT_SECRET``
     - Valoare secretă specifică instalării
     - Secret obligatoriu utilizat de autentificarea web. Aceeași valoare
       trebuie stocată pentru clientul OAuth ``web`` în baza de date a
       sistemului.

Valoarea configurației și valoarea corespunzătoare din baza de date trebuie
să rămână sincronizate. Generați un secret aleatoriu puternic, restricționați
accesul la acesta și planificați cu atenție rotația secretului, deoarece
modificarea unei singure copii va întrerupe autentificarea web.

Aplicarea modificărilor variabilelor de sistem
----------------------------------------------

După modificarea unei setări de sistem:

#. Verificați sintaxa configurației modificate.
#. Reporniți sau recreați serviciul afectat, dacă este necesar.
#. Inspectați jurnalele serviciului.
#. Testați Supervisor și un proiect reprezentativ.
#. Testați autentificarea, accesul la baza de date, hărțile și activitățile
   de fundal atunci când setarea modificată afectează aceste componente.

De exemplu:

.. code-block:: console

   docker compose config
   docker compose restart app
   docker compose logs --tail=200 app

Comanda Docker Compose exactă poate fi ``docker-compose`` pe sistemele mai
vechi.

Imaginea aplicației configurează PHP OPcache cu validarea marcajelor
temporale dezactivată. În consecință, este posibil ca fișierele PHP
modificate să nu fie detectate imediat de un proces care rulează. Repornirea
containerului ``app`` după modificarea configurației PHP sau a aplicației
evită furnizarea codului învechit din cache.

Arhitectura serviciilor Docker
==============================

Configurația Compose de referință creează o rețea bridge privată denumită
``obm_back``. Serviciile din această rețea pot comunica prin numele
serviciilor Compose și aliasurile de rețea configurate.

Serviciile de bază sunt:

.. list-table::
   :header-rows: 1
   :widths: 21 29 50

   * - Serviciu
     - Imagine
     - Scop
   * - ``app``
     - ``registry.gitlab.com/openbiomaps/web-app:latest``
     - Rulează Apache HTTP Server, PHP, aplicația web OpenBioMaps și
       Supervisor.
   * - ``mapserver``
     - ``openbiomaps/mapserver``
     - Rulează serviciul MapServer utilizat pentru randarea hărților
       proiectului.
   * - ``biomaps_db``
     - ``openbiomaps/database:pg17-3.5``
     - Rulează PostgreSQL și PostGIS pentru baza de date a sistemului și, în
       topologia implicită, pentru bazele de date ale proiectelor.
   * - ``memcached``
     - ``memcached:latest``
     - Furnizează cache-ul partajat al aplicației.
   * - ``obm-server-api``
     - ``registry.gitlab.com/openbiomaps/api/obm-server-api:latest``
     - Furnizează API-ul separat al serverului OpenBioMaps.
   * - ``adminer``
     - ``adminer``
     - Furnizează o interfață de administrare a bazei de date bazată pe
       browser.

Lista exactă a serviciilor depinde de fișierul Compose instalat. Serviciile
opționale pot fi dezactivate, eliminate sau înlocuite.

Pentru implementările de producție, luați în considerare fixarea imaginilor
la etichete de versiune testate sau la valori digest imuabile, în loc să
utilizați ``latest``. Astfel, actualizările devin previzibile, iar revenirea
la o versiune anterioară este simplificată.

Serviciul aplicației: Apache și PHP
==================================

Imaginea ``app`` se bazează pe imaginea oficială
``php:8.4-apache-trixie``. Prin urmare, Apache și PHP rulează în același
container.

Configurația Apache
-------------------

Imaginea efectuează următoarele configurări Apache:

* activează modulele ``headers``, ``proxy``, ``proxy_http``, ``rewrite`` și
  ``ssl``;
* schimbă rădăcina implicită a documentelor în
  ``/var/www/html/biomaps/root-site``; și
* instalează configurația Apache OpenBioMaps ca
  ``/etc/apache2/conf-enabled/openbiomaps.conf``.

Fișierul Compose de referință publică porturile 80 și 443 ale containerului
pe aceleași porturi ale gazdei:

.. code-block:: text

   80:80
   443:443

Atunci când un alt proxy invers termină TLS, este posibil să fie necesară
ajustarea porturilor publicate și a configurației gazdei virtuale Apache.
Asigurați-vă că schema, gazda și calea publică, precum și anteturile
redirecționate, corespund setării ``OB_DOMAIN`` și URL-urilor proiectului.

Configurația Apache personalizată trebuie furnizată prin intermediul unei
imagini întreținute, al unei montări bind sau al unui alt mecanism de
implementare reproductibil. Evitați editarea directă a unui container care
rulează, deoarece modificările respective se pierd atunci când containerul
este înlocuit.

Fișierul Compose de referință include exemple comentate pentru montarea
certificatelor TLS și a unei gazde virtuale SSL personalizate. Generați și
reînnoiți certificatele în afara containerului, cu excepția cazului în care
implementarea utilizează în mod intenționat un alt model de gestionare a
certificatelor.

După modificarea configurației Apache, validați-o în interiorul
containerului:

.. code-block:: console

   docker compose exec app apache2ctl configtest
   docker compose restart app
   docker compose logs --tail=200 app

Configurația PHP
----------------

Imaginea aplicației instalează extensiile PHP necesare pentru OpenBioMaps,
inclusiv suport pentru PostgreSQL, PDO PostgreSQL, internaționalizare, ZIP,
GD, Exif, Memcached, YAML și mcrypt.

Fișierul Compose de referință demonstrează cum pot fi suprascrise setările
PHP prin montarea unor fișiere INI individuale în
``/usr/local/etc/php/conf.d``:

.. code-block:: text

   ./php-date.timezone.ini -> /usr/local/etc/php/conf.d/php-date.timezone.ini
   ./php-upload.ini        -> /usr/local/etc/php/conf.d/php-upload.ini

Această abordare poate fi utilizată pentru setări precum:

* ``date.timezone``;
* ``upload_max_filesize``;
* ``post_max_size``;
* ``memory_limit``;
* ``max_execution_time``; și
* setări referitoare la sesiuni.

Atunci când configurați încărcările, păstrați consecvente toate limitele
relevante. De exemplu, ``post_max_size`` trebuie să fie suficient de mare
pentru întreaga solicitare, nu doar pentru fișierul încărcat. Un proxy invers
poate impune o limită suplimentară pentru dimensiunea solicitării.

Inspectați configurația PHP efectivă în interiorul containerului în loc să
presupuneți că a fost încărcat un fișier montat:

.. code-block:: console

   docker compose exec app php --ini
   docker compose exec app php -i
   docker compose logs --tail=200 app

Reporniți serviciul ``app`` după modificarea fișierelor INI montate.

Jurnalele aplicației
--------------------

Imaginea creează ``/var/log/openbiomaps.log`` și îl atribuie utilizatorului
serverului web. Fișierul Compose de referință montează acest fișier de pe
gazda Docker printr-o montare bind:

.. code-block:: text

   ./openbiomaps.log -> /var/log/openbiomaps.log

Fișierul gazdă trebuie să existe și să aibă permisiuni care îi permit
utilizatorului ``www-data`` din container să scrie în el. Inspectați și
ieșirea standard a containerului și jurnalele Apache:

.. code-block:: console

   docker compose logs --tail=200 app
   docker compose logs -f app

Configurați rotația fișierelor jurnal de pe gazdă pentru a împiedica
ocuparea întregului spațiu disponibil pe disc. Evitați înregistrarea
parolelor, tokenurilor, șirurilor complete de conexiune la baza de date sau a
datelor sensibile despre observații.

Serviciul MapServer
===================

MapServer rulează în serviciul separat ``mapserver``. Containerul ``app`` îl
accesează în mod normal prin numele de gazdă ``mapserver`` în rețeaua Docker
privată.

Configurația Compose de referință partajează următoarele resurse cu
MapServer:

.. list-table::
   :header-rows: 1
   :widths: 29 31 40

   * - Sursă
     - Calea din container
     - Scop
   * - Volumul ``mapserver_log``
     - ``/tmp/mapserver``
     - Jurnal și date temporare MapServer partajate.
   * - Volumul ``var_lib``
     - ``/var/lib/openbiomaps``
     - Date persistente partajate ale sistemului OpenBioMaps.
   * - Volumul ``projects``
     - ``/var/www/html/biomaps/root-site/projects``
     - Fișierele proiectelor și fișierele mapfile specifice proiectelor.
   * - ``./openbiomaps.conf``
     - ``/etc/apache2/conf-enabled/openbiomaps.conf``
     - Configurația Apache a containerului MapServer.
   * - ``./00_msencrypt-wrapper.conf``
     - ``/etc/apache2/conf-enabled/00_msencrypt-wrapper.conf``
     - Configurația Apache pentru wrapperul de criptare MapServer.
   * - ``./msencrypt-wrapper.pl``
     - ``/usr/local/bin/msencrypt-wrapper.pl``
     - Wrapperul utilizat de serviciul MapServer.

Modificările configurației Apache MapServer sau ale wrapperului montat de pe
gazdă trebuie validate și urmate de repornirea serviciului ``mapserver``:

.. code-block:: console

   docker compose exec mapserver apache2ctl configtest
   docker compose restart mapserver
   docker compose logs --tail=200 mapserver

Fișierele mapfile ale proiectului sunt gestionate în mod normal prin
administrarea proiectului OpenBioMaps și Supervisor. Deoarece volumul
``projects`` este partajat, atât aplicația, cât și MapServer pot accesa
aceleași fișiere ale proiectului.

MapServer nu publică un port al gazdei în fișierul Compose de referință.
Acest lucru este intenționat: în mod normal, solicitările trebuie să treacă
prin aplicația OpenBioMaps sau prin proxy-ul configurat al acesteia, în loc
ca MapServer să fie expus direct la internet.

MapCache necesită o configurație suplimentară și nu este activat doar prin
definirea unui URL MapCache. Dacă este introdus MapCache, documentați
stocarea, invalidarea cache-ului, limitele de resurse și expunerea sa în
rețea.

Serviciul PostgreSQL și PostGIS
==============================

Serviciul ``biomaps_db`` rulează PostgreSQL și PostGIS utilizând imaginea
``openbiomaps/database:pg17-3.5``. Directorul său de date este stocat în
volumul persistent ``biomaps_data``:

``/var/lib/postgresql/data``

Serviciul are următoarele nume în rețeaua privată:

* numele serviciului Compose: ``biomaps_db``;
* alias de rețea: ``biomaps``; și
* alias de rețea: ``gisdata``.

Utilizați numele așteptat de configurația OpenBioMaps instalată. Nu utilizați
``localhost`` din containerul ``app`` sau ``mapserver`` pentru a face
referire la acest serviciu al bazei de date.

Portul bazei de date nu este publicat pe gazda Docker în configurația de
referință. Acest lucru reduce expunerea și este suficient pentru serviciile
aplicației atașate la ``obm_back``. Publicați PostgreSQL numai atunci când
este necesar accesul extern, iar în acest caz restricționați accesul prin
reguli de firewall, controale de acces PostgreSQL și TLS, după caz.

Datele de autentificare ale bazei de date
-----------------------------------------

Fișierul Compose de referință nu setează direct o valoare fixă pentru
``POSTGRES_PASSWORD``. Comentariile sale indică faptul că imaginea bazei de
date creează o parolă aleatorie, cu excepția cazului în care datele de
autentificare sunt furnizate explicit.

Utilizați fluxul de lucru pentru instalare și Supervisor pentru a gestiona
datele de autentificare. Înainte de înlocuirea sau recrearea serviciului
bazei de date, confirmați unde sunt stocate datele de autentificare generate
și asigurați-vă că este disponibilă o copie de siguranță testată.

Nu modificați o parolă a bazei de date fără a actualiza toate configurațiile
sistemului și proiectelor care o utilizează.

Stocarea și copierea de siguranță a bazei de date
-------------------------------------------------

Volumul ``biomaps_data`` conține date persistente ale bazei de date. Simpla
copiere a volumului în timp ce PostgreSQL scrie în mod activ nu garantează,
în sine, o copie de siguranță consecventă a bazei de date. Utilizați
instrumente de copiere de siguranță adaptate pentru PostgreSQL sau procedura
de arhivare OpenBioMaps acceptată.

Testați în mod regulat restaurarea într-un mediu izolat. O copie de siguranță
care nu a fost restaurată cu succes nu trebuie considerată verificată.

Pentru a inspecta serviciul bazei de date:

.. code-block:: console

   docker compose ps biomaps_db
   docker compose logs --tail=200 biomaps_db

Nu eliminați volumul ``biomaps_data`` atunci când recreați serviciul, cu
excepția cazului în care baza de date este ștearsă intenționat și există un
plan de recuperare verificat.

Bază de date separată pentru proiect
------------------------------------

Fișierul Compose de referință conține un exemplu comentat pentru un serviciu
separat al bazei de date ``gisdata``. Dacă bazele de date ale sistemului și
proiectelor sunt separate:

* ajustați aliasurile rețelei Docker;
* actualizați setările gazdei bazei de date pentru sistem și proiecte;
* configurați date de autentificare separate;
* actualizați procedurile de copiere de siguranță și monitorizare; și
* verificați accesul atât din ``app``, cât și din ``mapserver``.

Evitați publicarea portului bazei de date, cu excepția cazului în care
trebuie să se conecteze clienți din afara rețelei Docker.

Serviciul Memcached
===================

Serviciul ``memcached`` furnizează cache-ul aplicației. Acesta este accesat
ca ``memcached:11211`` din containerul ``app`` prin rețeaua Docker privată.

Memcached nu oferă autentificare în configurația de referință. Nu expuneți
portul acestuia public. Dacă utilizați o rețea Docker personalizată,
asigurați-vă că numai serviciile de încredere ale aplicației îl pot accesa.

Datele din cache sunt dispensabile și nu trebuie tratate drept stocare
persistentă. Repornirea sau înlocuirea Memcached poate elimina intrările din
cache fără a șterge datele OpenBioMaps subiacente.

Serviciul API
=============

Serviciul ``obm-server-api`` rulează o imagine API OpenBioMaps separată.
Acesta:

* montează fișierul ``.env`` al implementării numai pentru citire;
* rulează scriptul de inițializare înainte de a porni Apache; și
* publică portul 80 al containerului ca portul 9001 al gazdei în configurația
  de referință.

Verificați fiecare valoare din ``.env`` și restricționați permisiunile
fișierului pe gazda Docker. Fișierul poate conține date de autentificare sau
alte secrete.

Publicarea ``9001:80`` face ca API-ul să fie accesibil pe toate interfețele
gazdei, cu excepția cazului în care configurația Docker sau firewall-ul
limitează accesul. În producție, este preferabil să direcționați API-ul prin
proxy-ul invers HTTPS configurat sau să îl asociați cu o interfață
restricționată.

Inspectați erorile de inițializare și de execuție ale API-ului cu:

.. code-block:: console

   docker compose logs --tail=200 obm-server-api

Serviciul de administrare a bazei de date
=========================================

Configurația de referință include Adminer și îl publică pe portul 9882 al
gazdei.

O interfață de administrare a bazei de date este sensibilă din punct de
vedere al securității. Nu o expuneți la internetul public fără controale
suplimentare puternice de acces. Preferați una dintre următoarele abordări:

* activați-o numai în timpul lucrărilor de întreținere;
* asociați-o numai cu interfața loopback;
* restricționați-o printr-un firewall sau o rețea privată; sau
* accesați-o printr-un tunel administrativ securizat.

De exemplu, asocierea portului publicat cu localhost ar utiliza o mapare a
portului Compose echivalentă cu ``127.0.0.1:9882:8080``.

Eliminați sau dezactivați serviciul atunci când nu este necesar.

Volume persistente
==================

Configurația Compose de referință definește următoarele volume denumite:

.. list-table::
   :header-rows: 1
   :widths: 27 73

   * - Volum
     - Scop
   * - ``root-private``
     - Fișiere private ale aplicației în
       ``/var/www/html/biomaps/root-site/private``.
   * - ``projects``
     - Directoare ale proiectelor partajate de aplicație și MapServer.
   * - ``var_lib``
     - Date persistente ale sistemului OpenBioMaps în
       ``/var/lib/openbiomaps``.
   * - ``mapserver_log``
     - Jurnal MapServer și fișiere temporare partajate în
       ``/tmp/mapserver``.
   * - ``etc_openbiomaps``
     - Configurație OpenBioMaps gestionată de administrator în
       ``/etc/openbiomaps``.
   * - ``biomaps_data``
     - Date PostgreSQL în ``/var/lib/postgresql/data``.

Volumele denumite supraviețuiesc înlocuirii normale a containerelor, dar pot
fi totuși șterse explicit. Includeți toate volumele care conțin date sau
configurații necesare în planul de copiere de siguranță și recuperare în caz
de dezastru.

Fișierul Compose arată și modul în care un volum denumit poate fi înlocuit cu
o montare bind. Montările bind fac căile gazdei mai ușor de inspectat, dar
necesită căi absolute, proprietari, permisiuni și proceduri de copiere de
siguranță corecte.

Fluxul de lucru pentru configurare
==================================

Alegeți mecanismul de configurare în funcție de tipul setării:

.. list-table::
   :header-rows: 1
   :widths: 34 66

   * - Tipul configurației
     - Mecanism recomandat
   * - Variabilele sistemului OpenBioMaps
     - Supervisor și volumul persistent ``/etc/openbiomaps``.
   * - Variabilele proiectului
     - Administrarea proiectului sau modul proiect din Supervisor.
   * - Setările Apache din ``app``
     - O imagine personalizată întreținută sau o montare explicită a
       configurației.
   * - Setările PHP
     - Fișiere INI montate în ``/usr/local/etc/php/conf.d``.
   * - Setările Apache MapServer
     - Fișiere de pe gazdă montate în containerul ``mapserver``.
   * - Fișierele mapfile ale proiectului
     - Administrarea proiectului sau Supervisor, stocate în volumul
       ``projects`` partajat.
   * - Setările bazei de date
     - Mediul Compose, configurația OpenBioMaps și mecanismul de configurare
       acceptat de imaginea bazei de date.
   * - Secrete
     - Fișiere de mediu restricționate sau un mecanism dedicat de gestionare
       a secretelor.

Nu efectuați modificări importante numai în interiorul unui container care
rulează. Astfel de modificări nu sunt reproductibile și dispar atunci când
containerul este înlocuit.

După modificarea fișierului Compose:

.. code-block:: console

   docker compose config
   docker compose pull
   docker compose up -d
   docker compose ps
   docker compose logs --tail=200

Consultați notele de versiune și creați o copie de siguranță verificată
înainte de actualizări. Evitați preluarea și implementarea automată a
imaginilor ``latest`` în sistemele de producție.

Activități programate recomandate
=================================

Activitățile programate pot fi rulate de pe gazda Docker prin cron sau
printr-un cronometru systemd echivalent. Utilizați căi absolute, capturați
jurnalele și asigurați-vă că execuțiile suprapuse nu pot deteriora datele.

Exemplele de mai jos trebuie adaptate instalării. Testați manual fiecare
comandă înainte de a o programa.

Actualizări Docker
------------------

Depozitul de scripturi OpenBioMaps conține un script de actualizare
automată:

https://github.com/OpenBioMaps/scripts/tree/master/docker-auto-update

Exemplu de intrare cron:

.. code-block:: cron

   # m h  dom mon dow   command
   0 4,16 * * * /srv/docker/openbiomaps/auto_update.sh > /srv/docker/openbiomaps/system_update_job.log 2>&1

Actualizările automate în producție implică riscuri operaționale. Înainte de
a le activa, definiți:

* cum sunt create și verificate copiile de siguranță;
* cum sunt gestionate migrările bazei de date;
* cum sunt detectate actualizările nereușite;
* cum sunt înregistrate versiunile imaginilor;
* cum se efectuează revenirea la o versiune anterioară; și
* cine primește notificările de eroare.

Activități de arhivare
----------------------

Scriptul de arhivare este disponibil la:

https://github.com/OpenBioMaps/scripts/blob/master/obm_archive.sh

Acesta utilizează ``.archive_list.txt`` și ``obm_archive_settings.sh``.
Exemplu de programare:

.. code-block:: cron

   # m h  dom mon dow   command
   0 2 * * *  /path_to/obm_archive.sh normal
   15 2 * * * /path_to/obm_archive.sh system
   15 3 1 * * /path_to/obm_archive.sh full
   0 5 * * *  /path_to/obm_archive.sh clean
   # Synchronise archives to a remote server
   0 4 * * *  /path_to/obm_archive.sh sync remote_user@remote-server.example /remote_path_to_archives

Pentru instalările Docker, urmați instrucțiunile de la sfârșitul fișierului
``obm_archive_settings.sh``.

Stocați cel puțin o copie de siguranță în afara gazdei OpenBioMaps.
Protejați datele de autentificare pentru copiile de siguranță la distanță și
testați periodic restaurarea.

Executorul activităților de fundal
----------------------------------

Proiectele care utilizează activități de fundal necesită executarea regulată
a executorului ``jobs.php``.

Exemplu:

.. code-block:: cron

   # m h  dom mon dow   command
   */5 * * * * /usr/bin/docker compose -f /srv/docker/openbiomaps/docker-compose.yml exec -u www-data -T app php /var/www/html/biomaps/root-site/projects/PROJECTTABLE/jobs.php

Înlocuiți ``PROJECTTABLE`` cu directorul sau identificatorul proiectului și
verificați calea utilizată de versiunea instalată.

Cron rulează cu un mediu restricționat. Utilizați calea absolută către
Docker și, dacă este necesar, specificați explicit directorul proiectului
Compose. Pe sistemele care utilizează comanda învechită, executabilul poate
fi în schimb ``/usr/local/bin/docker-compose``.

Creați o intrare separată pentru fiecare proiect care necesită procesare în
fundal. Monitorizați starea de ieșire și jurnalele și împiedicați execuțiile
concurente dacă o activitate poate rula mai mult decât intervalul de
programare.

Verificări operaționale
=======================

După instalare sau modificări ale configurației, verificați starea
serviciilor:

.. code-block:: console

   docker compose config
   docker compose ps
   docker compose logs --tail=200 app
   docker compose logs --tail=200 mapserver
   docker compose logs --tail=200 biomaps_db
   docker compose logs --tail=200 memcached

Apoi verificați în aplicație:

#. Autentificarea în Supervisor funcționează.
#. O pagină publică a proiectului se încarcă prin HTTPS.
#. Un utilizator autentificat se poate conecta și deconecta.
#. Aplicația poate citi și scrie înregistrările permise din baza de date.
#. Hărțile publice și private sunt randate corect.
#. Încărcările fișierelor respectă limitele configurate.
#. Livrarea e-mailurilor funcționează, dacă este configurată.
#. Activitățile de fundal sunt procesate.
#. Copiile de siguranță se finalizează și pot fi restaurate.
#. Serviciile administrative nu sunt expuse mai larg decât s-a intenționat.

Înregistrați versiunile imaginilor, modificările configurației, rezultatele
testelor și procedura de revenire pentru fiecare implementare în producție.
