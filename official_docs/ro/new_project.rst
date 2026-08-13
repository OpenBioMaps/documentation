.. _new-project:

Crearea unui proiect OpenBioMaps nou
====================================

Un membru autorizat al unui proiect OpenBioMaps existent poate crea un
proiect nou de bază de date utilizând formularul **Founding new project**.

Noul proiect este independent de proiectul din care este creat. Fondatorul
devine proprietarul său inițial și, până la invitarea altor utilizatori,
singurul său membru.

.. TODO: Documentați permisiunea necesară pentru crearea unui proiect și
   furnizați calea actuală de navigare către formularul
   **Founding new project**. Confirmați dacă funcția de creare a proiectelor
   poate fi dezactivată la nivelul serverului.


Înainte de crearea unui proiect
-------------------------------

Înainte de a completa formularul, luați în considerare următoarele aspecte:

* scopul și domeniul de aplicare al proiectului;
* informațiile pe care le va gestiona proiectul;
* tabelele bazei de date și relațiile necesare;
* persoanele care trebuie să poată vizualiza, trimite și modifica datele;
* dacă vor fi prelucrate date cu caracter personal sau date sensibile
  privind biodiversitatea; și
* persoanele responsabile de administrarea proiectului și gestionarea
  datelor.

Pentru recomandări privind planificarea structurii datelor și guvernanța
unui proiect, consultați:

* :doc:`Introducere <getting_started>`;
* :doc:`Colectarea datelor <data_collection>`;
* :doc:`Gestionarea datelor <data_management>`; și
* :doc:`Politica privind datele <data_policy>`.


Completarea formularului pentru crearea proiectului
---------------------------------------------------

Formularul solicită următoarele setări.


Identificatorul proiectului
...........................

Introduceți un identificator unic și scurt pentru proiect. Acest
identificator este utilizat în URL-ul proiectului și poate fi utilizat și ca
prefix sau identificator în configurația bazei de date a proiectului.

Utilizați un nume scurt alcătuit din litere mici, cifre și caractere de
subliniere. Evitați spațiile, caracterele cu diacritice, semnele de
punctuație și identificatorii SQL între ghilimele. Alegeți cu atenție
identificatorul, deoarece modificarea acestuia după crearea proiectului poate
afecta URL-urile, obiectele bazei de date, fișierele de configurare, clienții
API și integrările externe, astfel încât schimbarea sa este aproape
imposibilă.

.. TODO: Confirmați caracterele permise exacte, lungimea minimă și maximă,
   domeniul de unicitate și identificatorii rezervați. Documentați dacă
   identificatorul proiectului este utilizat întotdeauna drept nume sau
   prefix pentru tabelele bazei de date.

.. TODO: Documentați dacă redenumirea unui proiect este acceptată. Dacă da,
   descrieți procedura completă de migrare și efectul acesteia asupra
   URL-urilor, obiectelor bazei de date, configurației hărții, activităților,
   clienților API și integrărilor externe.


Titlul proiectului
..................

Introduceți un titlu scurt și descriptiv pentru proiect. Acest titlu apare
în antetul proiectului și în alte locuri vizibile utilizatorilor.

Titlul poate fi tradus după crearea proiectului. Păstrați-l concis; două sau
trei cuvinte sunt adesea suficiente, deși poate fi utilizat un titlu mai
lung atunci când este necesar pentru claritate.

Pentru informații despre descrierile și traducerile proiectelor, consultați:

* :ref:`Descrierea proiectului <project-description>`; și
* :ref:`Traduceri locale <localisation>`.


Descrierea proiectului
......................

Introduceți o descriere detaliată a proiectului și a scopului acestuia.
Descrierea trebuie să ajute potențialii colaboratori și utilizatorii datelor
să înțeleagă:

* ce colectează proiectul;
* domeniul său geografic, temporal și taxonomic;
* organizațiile sau persoanele responsabile de acesta;
* modul în care se intenționează utilizarea datelor; și
* unde pot obține utilizatorii informații suplimentare.

Descrierea poate fi actualizată după crearea proiectului.


Accesul implicit la date
........................

Selectați regulile inițiale pentru vizualizarea și modificarea datelor
proiectului. Aceste setări determină nivelul implicit de acces al
proiectului.

Un proiect închis sau restricționat la anumite grupuri poate defini după
creare reguli mai detaliate de acces la nivel de rând și de coloană.
Setările implicite pot fi modificate și ulterior, dar modificările trebuie
testate cu atenție pentru a vă asigura că acestea nu expun date
restricționate și nu împiedică utilizatorii autorizați să le acceseze.

Pentru descrierea controalelor de acces disponibile, consultați
:doc:`Acces la date <data_access>`.

.. TODO: Documentați opțiunile exacte de acces afișate în formularul pentru
   crearea proiectului și asociați fiecare opțiune cu valorile de
   configurare ``ACC_LEVEL`` și ``MOD_LEVEL`` corespunzătoare.

.. TODO: Confirmați dacă modificarea setărilor implicite la nivel de proiect
   afectează înregistrările existente sau modifică numai modul în care sunt
   evaluate regulile actuale de acces.


Centrul inițial al hărții
.........................

Specificați centrul inițial al hărții proiectului. Această setare determină
zona afișată atunci când utilizatorii deschid pentru prima dată pagina
hărții.

Centrul hărții poate fi modificat ulterior prin interfața administrativă
pentru configurarea hărții.


Sistemul de referință al coordonatelor hărții
.............................................

Specificați identificatorul de referință spațială (SRID) utilizat de harta
de bază a proiectului. Valoarea implicită este EPSG:4326 (WGS 84). Sistemele
de referință spațială pot fi consultate la
https://spatialreference.org/.

Utilizați un SRID diferit numai atunci când proiectul are o cerință tehnică
clară în acest sens și toate componentele relevante îl acceptă. Sistemul de
referință configurat trebuie să fie compatibil cu datele spațiale ale
proiectului, configurația OpenLayers, straturile MapServer, șabloanele de
interogare, exporturile și clienții externi.

Modificarea unui SRID nu transformă neapărat coordonatele existente.
Atribuirea unui SRID incorect poate plasa geometriile într-un loc greșit sau
poate face nevalide interogările spațiale.

Pentru informații de configurare conexe, consultați
:ref:`Setări pentru hartă <map-settings>`.

.. TODO: Confirmați dacă acest câmp definește proiecția hărții de bază,
   SRID-ul geometriei proiectului, proiecția de afișare a hărții web sau o
   combinație a acestora. Documentați locul în care au loc transformările
   coordonatelor.


Crearea proiectului
-------------------

După completarea și trimiterea formularului, OpenBioMaps creează proiectul
cu starea experimentală. Această stare îi informează pe utilizatori că
structura și configurația proiectului sunt încă în curs de dezvoltare; ea nu
împiedică în sine funcționarea proiectului.

.. TODO: Definiți stările de proiect acceptate, semnificația exactă a
   acestora și modul în care un administrator schimbă starea unui proiect
   din experimentală în testare, stabilă, arhivată sau într-o altă stare
   disponibilă. Confirmați dacă starea proiectului afectează vreun
   comportament al aplicației.

În timpul creării proiectului, sistemul creează configurația și obiectele
necesare ale bazei de date. La finalizarea procesului, acesta afișează un
mesaj care conține numele și parola administratorului SQL al proiectului.

Stocați aceste date de autentificare într-un manager de parole aprobat sau
într-un alt loc sigur. Nu le trimiteți prin e-mail necriptat, nu le includeți
în documentație și nu le înregistrați într-un depozit de cod sursă.
Administratorul SQL poate modifica sau șterge datele proiectului și obiectele
bazei de date.

.. TODO: Documentați dacă parola generată pentru administratorul SQL poate fi
   afișată din nou, schimbată prin OpenBioMaps sau recuperată prin
   Supervisor. Adăugați procedura recomandată pentru schimbarea datelor de
   autentificare.

Fondatorul poate accesa proiectul nou utilizând același nume de utilizator
și aceeași parolă OpenBioMaps folosite în proiectul inițial. Datele de
autentificare ale administratorului SQL sunt separate de datele de
autentificare ale fondatorului în aplicația web și trebuie utilizate numai
pentru activitățile de administrare a bazei de date care le necesită.


Structura inițială a bazei de date
----------------------------------

La crearea proiectului, OpenBioMaps creează un tabel inițial de date al
proiectului, care conține coloanele de sistem necesare pentru versiunea
respectivă de OpenBioMaps. Tabelul inițial poate fi apoi extins cu coloane
specifice proiectului, iar alte tabele sau vizualizări pot fi înregistrate
prin interfața de administrare.

Nu ștergeți și nu redenumiți coloanele de sistem doar pentru că par
neutilizate. Procesarea încărcărilor, regulile de acces, istoricul,
atașamentele, modulele sau clienții externi pot depinde de acestea.

Pentru detalii tehnice, consultați:

* :ref:`Tabelele și coloanele bazei de date <database-columns>`; și
* :doc:`Fluxul de date și integrarea bazei de date OpenBioMaps <obm_workflow>`.

.. TODO: Documentați obiectele exacte create pentru un proiect nou,
   inclusiv bazele de date, schemele, tabelele, coloanele de sistem,
   secvențele, tabelele de reguli, rolurile, fișierele de configurare,
   fișierele mapfile, directoarele și modulele implicite.


Configurarea proiectului nou
----------------------------

Un proiect nou creat necesită configurări suplimentare înainte de a începe
colectarea obișnuită a datelor sau utilizarea publică.

Un proces obișnuit de configurare include următorii pași:

#. **Definiți modelul de date.**

   Adăugați coloanele necesare în tabelul inițial de date și creați sau
   înregistrați orice tabele, vizualizări, relații, constrângeri, indecși și
   metadate suplimentare.

   Consultați :ref:`Tabelele și coloanele bazei de date <database-columns>`.

#. **Configurați regulile de acces și grupurile.**

   Creați grupurile de utilizatori necesare și verificați accesul la nivel
   de proiect, de rând și de coloană utilizând conturi de utilizator
   reprezentative.

   Consultați :doc:`Acces la date <data_access>` și
   :ref:`Grupuri <group-settings>`.

#. **Creați formularele de încărcare.**

   Definiți formulare separate pentru fluxurile de lucru necesare prin web,
   încărcare de fișiere, API sau dispozitive mobile. Configurați câmpurile
   obligatorii, validarea, valorile implicite, atribuirile de acces și
   versiunile publicate ale formularelor.

   Consultați
   :doc:`Gestionarea formularelor de încărcare <upload_forms>`.

#. **Configurați șabloanele de interogare SQL.**

   Creați șabloanele de interogare utilizate pentru interogările textuale și
   straturile spațiale ale hărții. Includeți substituenții necesari pentru
   controlul accesului și module.

   Consultați :ref:`Setări pentru interogări SQL <sql-query-settings>`.

#. **Configurați interfața hărții.**

   Definiți vizualizarea inițială a hărții, hărțile de bază, straturile
   suprapuse, configurația MapServer, sistemele de referință ale
   coordonatelor, stilurile și conexiunile dintre straturile hărții și
   șabloanele de interogare.

   Consultați :ref:`Setări pentru hartă <map-settings>`.

#. **Activați și configurați modulele.**

   Instalați sau activați numai modulele necesare proiectului. Modulele
   obișnuite pentru interogare și vizualizare pot include ``text_filter``,
   ``identify_points``, ``results_asStable``, ``results_buttons`` și
   ``results_summary``, în funcție de versiunea OpenBioMaps și cerințele
   proiectului.

   Consultați :doc:`Module <modules>`.

#. **Configurați fluxurile de lucru auxiliare.**

   Acolo unde este necesar, configurați istoricul, triggerele pentru
   regulile de acces și taxonomie, șabloanele de mesaje, activitățile de
   fundal, gestionarea atașamentelor, traducerile și integrările externe.

   Consultați :ref:`Funcții <trigger-functions>` și
   :doc:`Activități de fundal <jobs>`.

#. **Adăugați informațiile despre proiect și documentele de guvernanță.**

   Verificați titlul și descrierea proiectului, organizațiile responsabile,
   informațiile de contact, politica privind datele, informațiile privind
   confidențialitatea, licențele, cerințele de atribuire și condițiile de
   utilizare.

   Consultați :doc:`Politica privind datele <data_policy>`.

#. **Testați întregul flux de lucru.**

   Trimiteți înregistrări reprezentative prin fiecare client acceptat.
   Testați valorile valide și nevalide, atașamentele, geometriile,
   încărcările întrerupte, validarea, istoricul, restricțiile de acces,
   interogările, hărțile, răspunsurile API, exporturile și procedurile de
   ștergere sau corectare.

#. **Pregătiți copiile de siguranță și monitorizarea.**

   Confirmați că baza de date, atașamentele, configurația, modulele,
   activitățile și setările hărții sunt incluse în procedura prevăzută
   pentru copiile de siguranță. Testați restaurarea înainte de a vă asuma
   angajamente privind posibilitatea de recuperare.


Lista de verificare înainte de lansare
--------------------------------------

Înainte de a invita colaboratori obișnuiți sau de a face proiectul public,
verificați dacă:

* modelul de date reprezintă metodologia de colectare prevăzută;
* fiecare tabel și coloană are metadate relevante;
* formularele de încărcare utilizează versiunile publicate prevăzute;
* validarea este impusă pe server acolo unde este necesar;
* accesul public și cel restricționat au fost testate separat;
* locațiile sensibile și datele cu caracter personal beneficiază de
  protecția prevăzută;
* interogările cartografice și textuale returnează înregistrări consecvente;
* descărcările și răspunsurile API conțin numai câmpurile autorizate;
* sunt disponibile informații privind licențele, atribuirea și citarea;
* administratorii și responsabilii cu datele au responsabilități clar
  atribuite;
* activitățile de fundal și notificările au fost testate;
* fișierele generate și încărcările întrerupte au o procedură de curățare;
* jurnalele serverului și ale proiectului pot fi examinate de administratorii
  autorizați;
* copiile de siguranță includ toate datele și fișierele promise; și
* un test de restaurare a fost finalizat cu succes.

Păstrați proiectul în starea experimentală sau de testare până când
structura, modelul de acces, fluxurile de lucru pentru introducerea datelor
și procedura de recuperare au fost validate.
