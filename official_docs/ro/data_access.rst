Accesul la date
****************

OpenBioMaps oferă mai multe modalități de interogare, vizualizare și
descărcare a datelor proiectului. Înregistrările și câmpurile disponibile
prin aceste interfețe depind de regulile de acces ale proiectului și de
permisiunile utilizatorului curent.

Această pagină oferă o prezentare generală a metodelor disponibile pentru
preluarea datelor și a mecanismelor utilizate pentru controlul accesului la
datele proiectului.


Preluarea datelor
=================

Datele pot fi preluate prin intermediul aplicației web, descărcate în
formatele de fișiere acceptate sau accesate din aplicații externe.


Descărcarea fișierelor
----------------------

Rezultatele interogărilor pot fi descărcate într-o varietate de formate. În
funcție de setările modulului proiectului, formatele disponibile pot include:

* text și date structurate: CSV și JSON;
* foi de calcul: ODS, XLS și XLSX;
* date spațiale cu atribute text: ESRI Shapefile, KML, GPX și SQLite.

Exportul ESRI Shapefile poate consta din mai multe fișiere asociate, inclusiv
fișiere ``.shp``, ``.dbf``, ``.cpg``, ``.prj`` și ``.shx``.

Utilizatorii pot descărca individual imaginile asociate înregistrărilor de
date, în timp ce administratorii de proiect le pot descărca în bloc prin
interfața de administrare.

Administratorii pot exporta câmpurile text ale tabelelor de date în format
CSV prin pagina de gestionare a tabelelor bazei de date.

Exportul datelor poate fi, de asemenea, condiționat de cereri individuale de
autorizare prin intermediul modulului Export.


Interogări web
--------------

Aplicația web oferă instrumente pentru filtrarea și preluarea înregistrărilor
accesibile. În funcție de configurația proiectului, utilizatorii pot efectua:

* interogări bazate pe atribute, utilizând text, liste, date și alte câmpuri
  configurate;
* interogări spațiale, utilizând geometrii selectate sau desenate pe hartă;
  sau
* interogări combinate, spațiale și bazate pe atribute.

Pentru o prezentare generală a interfețelor de interogare, consultați
:doc:`Interfețe pentru utilizatori <user_interface>`.

.. TODO: Documentați modul în care rezultatele interogărilor pot fi
   vizualizate, rafinate, salvate, citate și exportate. De asemenea, trebuie
   clarificat dacă toate proiectele acceptă interogări combinate, spațiale și
   bazate pe atribute.


Aplicații externe
-----------------

Datele proiectului pot fi accesate și din aplicații externe:

* API-ul OpenBioMaps poate fi utilizat de scripturi, de pachetul OpenBioMaps
  pentru R și de alți clienți API;
* o conexiune SQL autorizată poate oferi acces direct la baza de date pentru
  aplicații precum QGIS; și
* aplicațiile client acceptate pot oferi propriile interfețe de interogare și
  descărcare.

Accesul printr-o aplicație externă este condiționat de regulile de acces ale
proiectului și de permisiunile asociate utilizatorului sau conexiunii
autentificate.

Pentru mai multe informații, consultați:

* :doc:`API-ul OpenBioMaps <api>`; și
* :doc:`Aplicații client <clients>`.


Controlul accesului la date
===========================

OpenBioMaps poate controla accesul la mai multe niveluri:

* setările la nivel de proiect definesc politica implicită de acces și
  modificare;
* regulile la nivel de rând controlează accesul la înregistrări individuale;
  și
* regulile la nivel de coloană controlează câmpurile care pot fi vizualizate
  sau descărcate.

Prin urmare, permisiunile efective pot depinde de mai multe setări.
Administratorii de proiect trebuie să testeze accesul rezultat cu utilizatori
care aparțin unor grupuri diferite, precum și fără autentificare, acolo unde
este activat accesul public.

.. TODO: Furnizați un model complet de evaluare a permisiunilor, care să
   prezinte precedența exactă și interacțiunea dintre regulile la nivel de
   proiect, rând și coloană și regulile grupurilor de utilizatori.


Accesul la nivel de proiect
---------------------------

Setările implicite de acces la nivel de proiect sunt definite în fișierul de
configurare ``local_vars.php.inc``:

.. code-block:: php

   define('ACC_LEVEL', 'group'); // Can be set to 'public' or 'login'.
   define('MOD_LEVEL', 'group');

``ACC_LEVEL`` definește nivelul implicit la care pot fi accesate datele
proiectului. Valorile documentate sunt:

``public``
   Datele sunt accesibile public, sub rezerva oricăror reguli de acces mai
   specifice.

``login``
   Datele sunt accesibile utilizatorilor autentificați, sub rezerva oricăror
   reguli de acces mai specifice.

``group``
   Accesul este controlat prin grupurile proiectului și prin reguli de acces
   suplimentare.

``MOD_LEVEL`` definește nivelul implicit la care pot fi modificate datele.
Acesta utilizează un model de acces similar.

Setarea ``MOD_LEVEL`` la ``public`` permite modificarea datelor fără a
solicita utilizatorului să se autentifice. Această setare trebuie utilizată
numai atunci când modificarea fără autentificare este intenționată în mod
explicit și au fost luate în considerare implicațiile sale de securitate.

.. TODO: Confirmați toate valorile valide pentru ``ACC_LEVEL`` și
   ``MOD_LEVEL`` și documentați comportamentul lor exact. Clarificați în
   special modul în care ``login`` diferă de ``group`` și dacă sunt acceptate
   valori suplimentare.

.. TODO: Explicați dacă aceste constante se aplică întregului proiect, cum
   intră în vigoare modificările configurației și dacă pot fi gestionate prin
   interfața de administrare a proiectului.


Accesul la nivel de rând
------------------------

Când ``ACC_LEVEL`` sau ``MOD_LEVEL`` este setat la ``group``, accesul la
înregistrările individuale poate fi controlat printr-un tabel ``*_rules``
specific proiectului. Aici, ``*`` reprezintă numele sau prefixul utilizat de
proiect.

Un tabel de reguli este asociat unui tabel de date. O înregistrare de date
este legată de regula corespunzătoare prin valoarea ``obm_id`` din tabelul de
date și valoarea ``row_id`` din tabelul de reguli.

Într-un proiect care utilizează accesul la nivel de grup, înregistrările fără
o intrare corespunzătoare în tabelul de reguli sunt disponibile numai
gazdelor proiectului.

.. TODO: Confirmați dacă o înregistrare de date poate avea exact un rând
   corespunzător în tabelul de reguli sau mai multe rânduri. Confirmați, de
   asemenea, dacă „gazda proiectului” este denumirea actuală a rolului care
   poate accesa înregistrările fără o regulă.

Funcționalitatea tabelului de reguli poate fi configurată în interfața de
administrare a proiectului, în **Administrarea proiectului > Funcții >
Crearea regulilor de acces**. Această interfață poate fi utilizată pentru
crearea sau actualizarea funcției trigger și pentru activarea sau
dezactivarea acesteia.

Când este activat, triggerul întreține tabelul de reguli după crearea,
modificarea sau ștergerea înregistrărilor.

.. TODO: Confirmați etichetele și amplasarea actuale ale interfeței de
   administrare a regulilor de acces. Documentați ce se întâmplă cu regulile
   existente atunci când triggerul este dezactivat, recreat sau modificat.


Atribuirea grupurilor de citire și scriere
------------------------------------------

Accesul de citire și scriere poate fi atribuit înregistrărilor individuale
prin câmpurile asociate grupurilor din tabelul de reguli.

Aceste valori pot fi completate automat de triggerul tabelului de reguli.
Grupurile atribuite pot fi derivate din setările de acces ale formularului de
încărcare utilizat pentru crearea înregistrării. Informațiile despre
încărcările finalizate și valorile configurate pentru proprietar și grup sunt
stocate în tabelul ``system.uploadings``.

.. TODO: Documentați tipurile de date și valorile acceptate pentru câmpurile
   ``read`` și ``write`` ale tabelului de reguli. Clarificați dacă acestea
   conțin un grup, mai multe grupuri, identificatori de utilizator sau o
   combinație a acestora.

.. TODO: Explicați modul în care setările de acces ale formularului de
   încărcare sunt transferate în ``system.uploadings`` și apoi în tabelul de
   reguli. Trebuie documentat și comportamentul pentru înregistrările create
   în afara unui formular de încărcare, de exemplu prin SQL sau API.


Regenerarea unui tabel de reguli
--------------------------------

Un tabel de reguli poate fi regenerat și manual. Exemplele următoare
utilizează ``abc`` ca tabel de date și ``abc_rules`` ca tabel de reguli al
acestuia.

Următoarele instrucțiuni recreează regulile fără a atribui grupuri de citire
sau scriere:

.. code-block:: sql

   DELETE FROM abc_rules
   WHERE data_table = 'abc';

   INSERT INTO abc_rules (row_id, sensitivity, data_table)
   SELECT obm_id, 'sensitive', 'abc'
   FROM abc;

Următoarele instrucțiuni derivă valorile pentru grup și proprietar din
intrarea corespunzătoare din ``system.uploadings``:

.. code-block:: sql

   DELETE FROM abc_rules
   WHERE data_table = 'abc';

   INSERT INTO abc_rules (row_id, sensitivity, data_table, read, write)
   SELECT a.obm_id, 'sensitive', 'abc', s."group", s.owner
   FROM abc AS a
   LEFT JOIN system.uploadings AS s
       ON s.id = a.obm_uploading_id;

Aceste exemple trebuie adaptate la numele reale ale tabelelor, schema,
tipurile coloanelor și politica de acces a proiectului. Administratorii
trebuie să creeze o copie de siguranță a tabelului de reguli existent și să
verifice permisiunile generate înainte de a utiliza instrucțiunile într-o
bază de date de producție.

.. TODO: Confirmați că numele coloanelor și tipurile valorilor din exemple
   corespund schemei actuale. Verificați în special tipurile pentru
   ``sensitivity``, ``read``, ``write``, ``system.uploadings.group`` și
   ``system.uploadings.owner``.

.. TODO: Explicați dacă ștergerea și reconstruirea unui tabel de reguli poate
   expune sau ascunde temporar datele, dacă operațiunea trebuie executată
   într-o tranzacție și dacă există o comandă de administrare care efectuează
   aceeași operațiune în siguranță.


Setările de sensibilitate
-------------------------

Câmpul ``sensitivity`` din tabelul de reguli afectează disponibilitatea
publică a unei înregistrări într-un proiect care utilizează accesul la nivel
de grup.

Valorile documentate includ:

``sensitive``
   Înregistrarea poate fi citită sau modificată numai de membrii grupurilor
   specificate prin regulile de acces aplicabile.

``restricted``
   În prezent, această valoare are aceeași semnificație documentată ca
   ``sensitive``.

``no-geom``
   Înregistrarea poate fi accesibilă la nivel public, dar geometria sa nu
   este afișată public.

``only-owner``
   Numai proprietarul proiectului poate accesa înregistrarea.

.. TODO: Confirmați lista completă a valorilor acceptate pentru
   ``sensitivity`` și definiți efectele lor exacte asupra vizualizării,
   interogării, descărcării și modificării înregistrărilor.

.. TODO: Clarificați dacă ``restricted`` și ``sensitive`` sunt într-adevăr
   aliasuri sau dacă diferă în anumite interfețe. Pentru ``no-geom``,
   explicați dacă geometria este eliminată, generalizată, înlocuită sau doar
   ascunsă pe hartă. De asemenea, definiți care utilizator este considerat
   proprietar pentru înregistrările ``only-owner``.


Accesul la nivel de coloană
---------------------------

Accesul poate fi controlat suplimentar pentru câmpurile individuale ale bazei
de date prin utilizarea modulului ``allowed_columns``. Acest modul stabilește
coloanele care pot fi vizualizate sau descărcate de utilizatorii publici ori
de grupurile de utilizatori specificate.

Într-un proiect în care ``ACC_LEVEL`` este setat la ``group``, modulul poate
fi utilizat pentru a face accesibile anumite câmpuri chiar și atunci când
proiectul nu oferă în rest acces general la fiecare câmp. De asemenea, acesta
poate restricționa câmpurile vizibile ale înregistrărilor accesibile prin
reguli la nivel de rând.

Acest lucru permite, de exemplu, ca utilizatorii să poată descoperi existența
unei înregistrări, fiind expus numai un subset aprobat al câmpurilor sale.

.. TODO: Documentați modul în care este activat și configurat modulul
   ``allowed_columns``, dacă acesta controlează interogările, precum și
   rezultatele afișate și descărcate, și modul în care tratează coloanele de
   geometrie.

.. TODO: Confirmați dacă ``allowed_columns`` poate face câmpurile accesibile
   public atunci când o înregistrare nu are o intrare corespunzătoare în
   tabelul de reguli. Această interacțiune este relevantă pentru securitate
   și trebuie descrisă prin exemple concrete.


Modul în care interacționează regulile de acces
-----------------------------------------------

Dacă este configurat numai accesul la nivel de grup pentru proiect și nicio
regulă mai specifică nu acordă acces, datele proiectului sunt disponibile
numai rolului administrativ căruia îi este permis să eludeze restricțiile
respective.

Un tabel de reguli adaugă control la nivel de rând, permițând ca înregistrări
diferite să fie puse la dispoziția unor grupuri diferite. Modulul
``allowed_columns`` adaugă control la nivel de coloană, permițând
vizualizarea sau descărcarea numai a câmpurilor selectate ale unei
înregistrări accesibile.

Atunci când se aplică mai multe reguli, permisiunile efective sunt
determinate de restricțiile lor combinate la nivel de proiect, rând și
coloană. Administratorii nu trebuie să presupună că o regulă mai largă
suprascrie automat o restricție mai specifică.

.. TODO: Înlocuiți această descriere generală cu algoritmul exact de
   soluționare a accesului implementat de OpenBioMaps. Includeți exemple
   privind accesul public, autentificat, de grup, al proprietarului, la nivel
   de rând și la nivel de coloană, precum și permisiunile de citire și
   scriere aflate în conflict.
