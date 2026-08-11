:author: Miklós Bán
:date: 2026-08-08

.. _user-interfaces:

Interfețe cu utilizatorul
*************************

Proiectele OpenBioMaps pot fi accesate prin intermediul unei aplicații web,
precum și prin mai multe aplicații externe și interfețe programatice. Aplicația
web este interfața principală pentru vizualizarea, colectarea, interogarea și
gestionarea datelor proiectului. În funcție de configurația proiectului și de
permisiunile utilizatorului curent, este posibil ca unele dintre interfețele
descrise mai jos să nu fie disponibile.

Această pagină oferă o prezentare generală a principalelor interfețe cu
utilizatorul. Instrucțiuni detaliate pentru configurarea funcționalităților
individuale sunt disponibile în secțiunile corespunzătoare despre administrare
și integrare din documentație.


Aplicația web
=============

Aplicația web OpenBioMaps oferă acces la datele proiectului și la instrumentele
specifice proiectului. Paginile și funcțiile disponibile depind de configurația
proiectului, de modulele instalate și de permisiunile utilizatorului curent.


Pagina de autentificare
=======================

Pagina de autentificare permite utilizatorilor înregistrați să se autentifice
pe un server OpenBioMaps. În funcție de configurația serverului, aceasta poate
oferi și opțiuni pentru recuperarea parolei, înregistrare și autentificare
printr-un serviciu extern.


Parolă uitată
-------------

Utilizatorii care au înregistrat o adresă de e-mail pot solicita un link
temporar de autentificare. Linkul este trimis la adresa de e-mail asociată
contului lor.


Înregistrarea și alăturarea la un proiect
-----------------------------------------

În fluxul de lucru implicit, un utilizator are nevoie de o invitație din partea
unui utilizator existent înainte de a se alătura unui proiect OpenBioMaps. Dacă
înregistrarea publică sau autentificarea printr-un serviciu extern este
activată pe server, poate fi disponibil un flux de înregistrare diferit.

Acolo unde solicitările de invitație sunt activate, utilizatorii pot solicita
acces urmând linkul de înregistrare de pe pagina de autentificare.
Administratorii de proiect primesc aceste solicitări. În funcție de setările
proiectului, sistemul poate fie să trimită automat o invitație, fie să aștepte
ca un administrator de proiect să aprobe solicitarea și să trimită manual o
invitație.

E-mailul de invitație conține un link pentru alăturarea la proiect. În timpul
acestui proces, utilizatorul trebuie:

* să confirme că dorește să se alăture proiectului;
* să accepte acordul utilizatorului și declarația privind prelucrarea datelor; și
* să stabilească o parolă.

Utilizatorului i se poate solicita și furnizarea unor informații suplimentare
de profil.


Pagina de profil
================

Pagina de profil oferă acces la setările personale și la conținutul specific
utilizatorului, inclusiv invitații, mesaje, stări de încărcare salvate și
istoricul încărcărilor.

Pentru mai multe informații despre setările profilului, consultați
:doc:`Profilul utilizatorului <profile>`.


Invitații
---------

În mod implicit, utilizatorii înregistrați pot invita alte persoane să se
alăture unui proiect. Invitația este trimisă în limba selectată de expeditor,
iar mesajului de invitație generat automat i se poate adăuga un mesaj personal.

O invitație expiră la două săptămâni după trimitere. Dacă destinatarul nu se
alătură proiectului înainte ca invitația să expire, trebuie trimisă o invitație
nouă.

În mod implicit, un utilizator poate avea până la 11 invitații active în cadrul
unui proiect. Un administrator de proiect poate modifica această limită în
``local_vars.php.inc``. Dacă limita este stabilită la ``0``, numai gazdele
proiectului pot trimite invitații.

.. TODO: Confirmați dacă limita invitațiilor se aplică per utilizator, per
   proiect sau la nivelul întregului server. Confirmați, de asemenea, dacă
   „gazdă a proiectului” este denumirea actuală a acestui rol în interfața cu
   utilizatorul.


Mesaje
------

Proiectele OpenBioMaps includ un sistem intern de mesagerie pentru notificări
automate și mesaje schimbate între utilizatori. Utilizatorii pot alege pe
pagina lor de profil dacă mesajele trebuie redirecționate și către adresa lor
de e-mail.

Interfața de mesagerie poate fi deschisă din pagina de profil. Aceasta le
permite utilizatorilor să caute în mesaje și să creeze mesaje noi. Mesajele
sunt organizate în următoarele categorii:

* Mesaje personale;
* Mesaje trimise;
* Mesaje de sistem;
* Evaluări și comentarii; și
* Flux de știri.

Administratorii de proiect pot trimite mesaje grupurilor de utilizatori și pot
trimite mesaje și prin e-mail. Ceilalți utilizatori își pot trimite mesaje
individuale.

Aplicațiile client pot accesa și mesajele utilizatorului. De exemplu, o
aplicație mobilă poate notifica utilizatorii despre mesajele primite de la
administratorii de proiect sau de la alți utilizatori, precum și despre
evaluările și comentariile asociate înregistrărilor încărcate de aceștia.


Crearea unui proiect nou
------------------------

Unui utilizator înregistrat i se poate permite să creeze un proiect nou de
bază de date. Creatorul devine proprietarul noului proiect, care este
independent de proiectul din care a fost creat.

Pentru instrucțiuni, consultați
:doc:`Crearea unui proiect OpenBioMaps nou <new_project>`.


Administrarea proiectului
=========================

În mod implicit, paginile de administrare a proiectului sunt disponibile
proprietarului/fondatorului proiectului. Și alți utilizatori administratori pot
avea acces la funcțiile administrative.

Accesul la funcțiile administrative individuale poate fi acordat separat.
De exemplu, unui utilizator i se poate acorda permisiunea de a gestiona
formularele de încărcare și setările hărții.

Pentru o prezentare generală a interfeței de administrare, consultați
:doc:`Administrarea proiectului <admin_pages>`.


Pagina hărții
=============

Pagina hărții afișează datele spațiale ale proiectului și oferă instrumente
pentru interogări spațiale și bazate pe atribute. Aceasta este disponibilă dacă
proiectul conține date spațiale (există un câmp geometric în cel puțin un tabel
PostgreSQL care aparține proiectului) și dacă au fost configurate setările
necesare pentru baza de date și MapServer (a fost definit un șablon de
interogare, a fost configurat stratul din mapfile-ul MapServer și a fost
stabilită conexiunea dintre serverul PostgreSQL și MapServer).

În funcție de configurația proiectului, harta poate afișa toate înregistrările
accesibile sau numai rezultatele interogării curente. Datele de tip punct,
linie și poligon pot fi afișate în straturi suprapuse separate.

Un proiect poate furniza mai multe hărți de bază. OpenStreetMap este harta de
bază implicită, dar pot fi disponibile și grile, imagini aeriene, locații de
eșantionare sau alte straturi specifice proiectului. Administratorii de proiect
pot configura opțional o hartă de bază Google dacă sunt disponibile contul
Google și setările API necesare.


Interogări spațiale
-------------------

Utilizatorii pot iniția o interogare spațială prin:

* desenarea unei geometrii pe hartă;
* selectarea unei locații cu instrumentul de informații al hărții; sau
* selectarea unei geometrii încărcate anterior.

Geometriei selectate sau desenate i se poate aplica o zonă tampon. De exemplu,
o interogare punctuală poate include înregistrările aflate pe o rază de 500 de
metri, în timp ce o interogare liniară poate include înregistrările aflate
într-un coridor de 10 metri.

Instrumentele de desenare, straturile de interogare și opțiunile pentru zona
tampon disponibile depind de configurația proiectului.


Interogări textuale și după atribute
------------------------------------

Proiectele pot furniza câmpuri de interogare personalizate pentru filtrarea
înregistrărilor după valorile atributelor acestora. În funcție de configurația
câmpului, controalele de introducere disponibile pot include:

* câmpuri de text;
* câmpuri cu completare automată;
* liste cu selecție unică sau multiplă;
* câmpuri pentru dată și oră; și
* selectoare de intervale de date.

Condițiile spațiale și cele bazate pe atribute pot fi utilizate împreună
atunci când interfața de interogare a proiectului permite acest lucru.


Salvarea și identificarea interogărilor
---------------------------------------

Rezultatul unei interogări poate fi stocat pe server și i se poate atribui un
identificator persistent. Pentru rezultatele stocate ale interogărilor care
îndeplinesc condițiile poate fi solicitat și un DOI. Interogările pot fi
salvate pentru a putea fi repetate ulterior.

.. TODO: Explicați diferența dintre o interogare salvată, rezultatul stocat al
   unei interogări, un cuvânt-cheie persistent și un DOI. Documentația trebuie
   să precizeze dacă repetarea unei interogări returnează rezultatul original
   stocat sau execută din nou interogarea asupra conținutului curent al bazei
   de date.


Instrumentul de testare a geometriei
====================================

Instrumentul de testare a geometriei este o interfață separată, bazată pe
hartă, pentru inspectarea și editarea geometriilor reprezentate în formate
precum GeoJSON și WKT. Acesta poate fi utilizat și cu geometrii obținute prin
cereri OpenStreetMap.

Această aplicație este disponibilă în fiecare proiect dacă adăugați
/geometest/ la sfârșitul URL-ului principal, cu condiția ca URL-ul principal
să nu fie suprascris de alte setări. De exemplu:

https://openbiomaps.org/projects/checkitout/geomtest/

Interfața web de încărcare utilizează, de asemenea, această aplicație pentru a
selecta locații pe hartă și a verifica utilizatorii.

Pagina de încărcare a datelor
=============================

Pagina de încărcare a datelor este utilizată pentru pregătirea, validarea și
trimiterea înregistrărilor către baza de date a unui proiect.

Un proiect poate defini mai multe formulare de încărcare pentru același tabel
al bazei de date. Fiecare formular poate expune câmpuri, reguli de validare,
controale de introducere și opțiuni de încărcare diferite. De exemplu, un
formular poate fi conceput pentru trimiterea publică a datelor, în timp ce
altul poate fi optimizat pentru o aplicație mobilă sau pentru un anumit format
de import.

Pentru informații despre crearea și configurarea formularelor, consultați
:doc:`Gestionarea formularelor de încărcare <upload_forms>`.


Încărcarea fișierelor
---------------------

Interfața de încărcare acceptă următoarele tipuri de fișiere:

* fișiere text delimitate și structurate: CSV, DSV, TSV și JSON;
* imagini: JPEG și TIFF, inclusiv metadatele Exif acceptate;
* foi de calcul: ODS, XLS și XLSX;
* date spațiale: componente ESRI Shapefile, fișiere GPX și SQLite; și
* date privind secvențele genetice: FASTA.

O încărcare ESRI Shapefile poate fi alcătuită din fișierele asociate ``.shp``,
``.dbf``, ``.cpg``, ``.prj`` și ``.shx``.

Fișierele acceptate pot fi importate și de la un URL utilizând o cerere HTTP
GET.

.. TODO: Documentați structura JSON acceptată, regulile privind delimitatorii
   și codificarea caracterelor pentru fișierele text, câmpurile Exif acceptate
   și structura necesară a fișierelor SQLite. De asemenea, trebuie explicat
   modul în care fișierele Shapefile alcătuite din mai multe fișiere sunt
   selectate sau împachetate pentru încărcare.

.. TODO: Clarificați dacă importurile de la URL acceptă HTTPS, autentificare,
   redirecționări și parametri URL și dacă URL-urilor de la distanță li se
   aplică restricții pe partea de server.


Introducerea datelor prin formularul web
----------------------------------------

Formularele web le permit utilizatorilor să creeze înregistrări direct în
interfața web a proiectului. Tabelul pentru introducerea datelor funcționează
asemănător unei foi de calcul: câmpurile bazei de date sunt afișate sub formă
de coloane, iar înregistrările sunt introduse sub formă de rânduri.

Deși tabelul poate conține un număr arbitrar de rânduri, acesta este destinat
în principal introducerii câtorva zeci sau, cel mult, câtorva sute de
înregistrări. Pentru seturile de date mai mari se recomandă pregătirea unei foi
de calcul și utilizarea interfeței de încărcare a fișierelor.

Anteturile câmpurilor obligatorii sunt afișate cu roșu, iar anteturile
câmpurilor opționale sunt afișate cu gri. O zonă galbenă de introducere aflată
sub antetul fiecărui câmp poate fi utilizată pentru a completa mai multe
rânduri cu aceeași valoare.

Interfața oferă și instrumente pentru aplicarea modificărilor în masă,
formatarea sau transformarea valorilor coloanelor și excluderea rândurilor din
încărcare.

.. TODO: Descrieți funcțiile disponibile pentru editarea în masă, formatare
   și transformare. De asemenea, trebuie clarificat dacă un rând exclus rămâne
   în starea de încărcare salvată și poate fi restaurat ulterior.


Validarea și pregătirea datelor
-------------------------------

Înainte ca înregistrările să fie trimise, datele încărcate sau introduse manual
pot fi examinate și corectate în tabelul de încărcare. Instrumentele de
validare și editare disponibile depind de formularul de încărcare și de
câmpurile configurate ale acestuia.

În orice etapă a acestui proces de pregătire, conținutul curent al tabelului de
încărcare poate fi exportat ca fișier CSV.


Salvarea și reluarea unei încărcări
-----------------------------------

Pregătirea unei încărcări mari poate necesita mult timp, iar conexiunea la
server se poate întrerupe înainte ca înregistrările să fie trimise. Pentru a
preveni pierderea datelor pregătite, starea curentă a tabelului de încărcare
poate fi salvată și restaurată ulterior.

Sistemul creează și o copie de rezervă automată aproximativ la fiecare două
minute. Tabelele de încărcare salvate și cele pentru care s-au creat automat
copii de rezervă sunt disponibile din pagina de profil, unde copiile de
rezervă perimate pot fi șterse.

.. TODO: Clarificați diferența dintre o stare de încărcare salvată manual și o
   copie de rezervă automată. De asemenea, trebuie documentate perioada de
   păstrare, limitele de stocare, regulile de acces și condițiile în care sunt
   șterse copiile de rezervă automate.


Istoricul încărcărilor
----------------------

Metadatele despre fiecare încărcare de date finalizată sunt înregistrate
automat. Utilizatorii pot accesa istoricul încărcărilor din pagina lor de
profil și din fișa unei înregistrări încărcate.

.. TODO: Enumerați metadatele stocate pentru o încărcare, explicați cine le
   poate vizualiza și descrieți modul în care o intrare din istoricul
   încărcărilor este asociată înregistrărilor individuale.


Interfețe externe pentru trimiterea datelor
-------------------------------------------

Datele pot fi trimise și din aplicații externe. În funcție de configurația
proiectului și de permisiunile utilizatorului, acestea pot include:

* clienți API;
* aplicații mobile pentru colectarea datelor;
* pachetul R OpenBioMaps; și
* aplicații care utilizează o conexiune SQL autorizată.

Pentru mai multe informații, consultați:

* :doc:`API-ul OpenBioMaps <api>`;
* :doc:`Aplicații client <clients>`; și
* :doc:`Aplicații mobile <mobile_applications>`.


Pagina fișei înregistrării
==========================

Fiecare înregistrare din baza de date are o fișă care conține câmpurile sale
de date și metadatele asociate. Câmpurile și metadatele vizibile unui
utilizator pot fi restricționate prin setările proiectului și regulile de
acces.

.. TODO: Explicați modul în care utilizatorii deschid o fișă, categoriile de
   metadate pe care aceasta le conține și setările proiectului sau regulile de
   acces care controlează conținutul vizibil.


Istoricul datelor
-----------------

Istoricul datelor unei înregistrări prezintă modificările aduse înregistrării
respective. Această pagină este disponibilă numai dacă gazda proiectului a
activat înregistrarea modificărilor în setările proiectului.

.. TODO: Documentați operațiunile care sunt înregistrate, dacă sunt afișate
   valorile anterioare ale câmpurilor și identitatea editorului, cine poate
   accesa istoricul și dacă modificările pot fi anulate.


Pagina cu rezumatul bazei de date
=================================

Fiecare proiect include o pagină cu rezumatul bazei de date, care conține o
descriere a proiectului și datele de contact ale acestuia.

.. TODO: Descrieți locul din care poate fi accesată pagina cu rezumatul bazei
   de date și identificați setările administrative din care este obținut
   conținutul acesteia. De asemenea, trebuie clarificat dacă pagina conține
   metadate suplimentare, condiții de acces sau informații pentru citare.


Pagina de bun venit
===================

Fiecare proiect poate furniza o pagină de bun venit configurabilă. Aceasta
poate fi utilizată pentru prezentarea proiectului și pentru îndrumarea
utilizatorilor către cele mai importante instrumente și informații ale
acestuia.

Pentru mai multe informații, consultați
:doc:`Configurarea paginii de bun venit <welcome_page>`.


Alte interfețe cu utilizatorul
==============================

Pe lângă aplicația web, datele și serviciile OpenBioMaps pot fi accesate prin
aplicații mobile, software GIS pentru desktop, software statistic și clienți
API personalizați. Interfețele disponibile pentru un anumit proiect depind de
configurația și regulile de acces ale acestuia.


Aplicații mobile
----------------

Aplicațiile mobile pot sprijini colectarea datelor pe teren și comunicarea cu
proiectele OpenBioMaps. Funcționalitățile disponibile depind de aplicație,
precum și de formularele de încărcare și permisiunile proiectului.

Pentru mai multe informații, consultați
:doc:`Aplicații mobile <mobile_applications>`.


QGIS
----

Pluginul OpenBioMaps pentru QGIS oferă acces la datele OpenBioMaps din QGIS.
Proiectele pot furniza și conexiuni SQL autorizate pentru fluxurile de lucru
care necesită acces direct la baza de date.

Pentru mai multe informații despre integrările client acceptate, consultați
:doc:`Aplicații client <clients>`.


R
-

Pachetul R ``obm`` oferă instrumente pentru interogarea și prelucrarea datelor
OpenBioMaps în R.

`obm pe CRAN <https://cran.r-project.org/web/packages/obm/index.html>`_


Clienți API
-----------

API-ul OpenBioMaps permite aplicațiilor și scripturilor autorizate să
interogheze sau să trimită datele proiectului. Operațiunile disponibile depind
de endpoint-ul API, de configurația proiectului și de permisiunile
utilizatorului autentificat.

Pentru mai multe informații, consultați
:doc:`API-ul OpenBioMaps <api>`.


Raportarea erorilor
===================

Acolo unde raportarea erorilor a fost configurată pe server, interfața de
raportare a erorilor este disponibilă din pagina de profil și din pagina de
încărcare a datelor. Selectarea pictogramei pentru erori din colțul din dreapta
jos al ecranului deschide un formular simplu de raportare.

.. figure:: images/hiba_1.jpg
   :scale: 100 %
   :alt: Pictograma de raportare a erorilor din colțul din dreapta jos

   Pictograma de raportare a erorilor din colțul din dreapta jos al paginii

.. figure:: images/hiba_2.jpg
   :scale: 100 %
   :alt: Formular pentru raportarea erorilor

   Formular pentru raportarea erorilor

Rapoartele provenite de la serviciile OpenBioMaps oficiale pot fi
redirecționate către
`sistemul OpenBioMaps de urmărire a problemelor
<https://gitlab.com/groups/openbiomaps/-/issues>`_. Utilizatorul poate primi
mesaje automate de sistem atunci când au loc evenimente ulterioare legate de
raport.

Un administrator de server poate activa un serviciu de raportare a erorilor
prin configurarea variabilei ``AUTO_BUGREPORT_ADDRESS`` în
``system_vars.php.inc``. Serverele întreținute de Consorțiul OpenBioMaps pot
utiliza o valoare furnizată de Consorțiu. Administratorii altor servere trebuie
să furnizeze și să configureze propriul sistem compatibil de urmărire a
problemelor.

.. TODO: Confirmați comportamentul exact și valoarea așteptată pentru
   ``AUTO_BUGREPORT_ADDRESS``. Trebuie documentat dacă rapoartele sunt trimise
   întotdeauna către GitLab, ce informații sunt incluse automat, modul în care
   este gestionată autentificarea și modul în care utilizatorii primesc
   actualizări despre rapoartele lor.
