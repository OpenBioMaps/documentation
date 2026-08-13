Întrebări frecvente
********************

Informații generale
===================

Ce este OpenBioMaps?
--------------------

OpenBioMaps este o platformă software open source și o colecție de servicii
pentru gestionarea datelor biologice. Aceasta poate fi utilizată pentru a
crea proiecte susținute de baze de date, pe care mai mulți utilizatori le pot
accesa simultan de pe dispozitive diferite și cu niveluri diferite de
permisiuni.

Organizațiile își pot opera propriul server OpenBioMaps. Unele instituții
oferă și servicii OpenBioMaps găzduite pentru proiecte de cercetare sau de
știință participativă, astfel încât proiectele nu trebuie neapărat să își
întrețină propriul server. Disponibilitatea, eligibilitatea și condițiile de
asistență depind de instituția care furnizează găzduirea.

Ce este Consorțiul OpenBioMaps?
-------------------------------

Consorțiul OpenBioMaps coordonează cooperarea privind platforma și
dezvoltarea acesteia.

Consultați :doc:`Consorțiul OpenBioMaps <consortium>` pentru mai multe
informații.

Unde pot găsi servere OpenBioMaps existente?
--------------------------------------------

Serverele înregistrate sunt enumerate în
`baza de date a rețelei OpenBioMaps
<https://openbiomaps.org/projects/openbiomaps_network>`_.

Este posibil ca lista să nu includă toate serverele OpenBioMaps operate
independent.

Proiecte și înregistrare
========================

Cum pot găsi sau crea un proiect de bază de date?
-------------------------------------------------

Proiectele existente pot fi găsite prin lista de proiecte a unui server
OpenBioMaps sau prin informațiile furnizate de organizația care operează
serverul respectiv.

Dacă sunteți deja membru al unui proiect, serverul vă poate permite să
solicitați sau să creați un alt proiect de bază de date prin interfața web.
Procedura exactă și permisiunile necesare depind de configurația serverului.
Contactați administratorul serverului dacă funcția de creare a proiectelor
nu este disponibilă pentru contul dumneavoastră.

Cum mă pot înregistra într-un proiect OpenBioMaps?
--------------------------------------------------

Înregistrarea necesită în mod normal o invitație. În funcție de configurația
proiectului, membrii existenți sau numai administratorii pot avea
permisiunea de a invita utilizatori noi.

Un proiect poate oferi și un formular de solicitare a invitației pe pagina
sa de autentificare. Acesta permite viitorilor utilizatori să solicite
administratorilor proiectului accesul, dar trimiterea unei solicitări nu
acordă automat calitatea de membru.

Unele servere acceptă înregistrarea sau autentificarea prin intermediul unui
furnizor extern OpenID Connect, precum Google. Furnizorii disponibili și
posibilitatea de a crea un cont nou prin intermediul acestora depind de
configurația serverului și a proiectului.

Pentru informații despre aderarea la un anumit proiect, contactați creatorii
sau administratorii acestuia.

Încărcarea și accesarea datelor
===============================

Cum pot încărca date?
---------------------

Metoda standard este utilizarea unui formular de încărcare specific
proiectului. Formularele pot fi utilizate prin interfața web și, atunci când
proiectul acceptă această funcție, printr-o aplicație mobilă OpenBioMaps.

Consultați :doc:`Gestionarea formularelor de încărcare <upload_forms>`
pentru informații despre configurarea formularelor.

Importurile de mari dimensiuni sau specializate pot fi efectuate și cu un
client PostgreSQL. Importurile directe în baza de date trebuie efectuate
numai de utilizatori cu experiență și cu permisiunile necesare, deoarece
acestea pot ocoli validarea și fluxurile de încărcare de la nivelul
aplicației.

Cum pot accesa datele?
----------------------

În funcție de configurația proiectului și de permisiunile dumneavoastră,
datele pot fi accesate în mai multe moduri:

* prin interogări cartografice sau textuale în interfața web;
* prin descărcări și exporturi în interfața web;
* prin funcțiile de partajare a datelor;
* cu un client PostgreSQL;
* cu QGIS sau cu un alt client GIS compatibil;
* printr-un API OpenBioMaps;
* cu pachetul R OpenBioMaps; sau
* cu :doc:`aplicația PWA pentru interogarea hărții <pwa>`.

Consultați :doc:`Acces la date <data_access>`,
:doc:`Documentația API <api>` și :doc:`Clienți <clients>` pentru mai multe
informații.

Ce opțiuni sunt disponibile pentru descărcarea datelor?
-------------------------------------------------------

Metodele de descărcare disponibile depind de modulele activate pentru
proiect și de permisiunile utilizatorului actual. Acestea pot include:

* module de export CSV, JSON, KML, GPX, SHP și în alte formate;
* acces prin QGIS sau printr-un alt client PostgreSQL/PostGIS;
* semne de carte, interogări salvate și legături permanente;
* preluarea prin API; și
* pachetul R OpenBioMaps.

Unele proiecte necesită aprobare înainte ca o descărcare să fie pusă la
dispoziție. Exporturile continuă să fie supuse regulilor proiectului privind
accesul la nivel de rând și de coloană.

De ce pot alți utilizatori să vadă date pe care eu nu le pot interoga?
----------------------------------------------------------------------

Înregistrările sunt probabil restricționate la anumiți utilizatori sau
anumite grupuri. Setările formularelor de încărcare ale unui proiect pot
defini cine primește acces de citire sau de modificare la înregistrările
încărcate prin formularul respectiv.

Dacă înregistrările sunt încărcate fără setări adecvate de acces, este
posibil ca acestea să fie vizibile numai administratorilor proiectului.
Administratorii proiectului pot modifica ulterior regulile de acces, dar
procedura exactă depinde de schema bazei de date și de configurația regulilor
proiectului.

Următorul exemplu SQL ilustrativ adaugă ID-ul numeric de rol ``295`` în
matricea de acces pentru citire a înregistrărilor selectate:

.. code-block:: sql

   UPDATE mydatabase_rules AS rules
   SET read = rules.read || 295
   FROM (
       SELECT data.obm_id AS row_id
       FROM public.mydatabase AS data
       LEFT JOIN mydatabase_rules AS existing_rules
           ON data.obm_id = existing_rules.row_id
       WHERE data.observer ILIKE 'Smith%'
   ) AS selected
   WHERE selected.row_id = rules.row_id;

Înlocuiți toate denumirile tabelelor, denumirile coloanelor, condițiile și
ID-urile de rol cu valori adecvate proiectului.

Acest exemplu actualizează numai înregistrările care au deja un rând
corespunzător în tabelul de reguli. Acesta nu creează regulile care lipsesc.
De asemenea, poate adăuga același rol de mai multe ori dacă rolul respectiv
este deja prezent.

Creați o copie de siguranță și examinați rândurile afectate înainte de a
executa o actualizare a regulilor de acces. Ori de câte ori este posibil,
efectuați modificarea printr-o interfață de administrare acceptată.
Modificările SQL incorecte pot divulga sau restricționa neintenționat datele
proiectului.

Acces mobil
===========

Cum pot prelua date cu un dispozitiv mobil?
-------------------------------------------

:doc:`Aplicația PWA pentru interogarea hărții <pwa>` poate interoga
înregistrările proiectului și poate pune la dispoziție offline înregistrările
preluate anterior. Disponibilitatea și configurația acesteia depind de
proiect.

OpenBioMaps oferă și aplicații mobile pentru colectarea datelor pe teren.
Consultați :doc:`Aplicații mobile <mobile_applications>` pentru opțiunile
disponibile.

Cum utilizez aplicația mobilă OpenBioMaps?
------------------------------------------

Aplicația mobilă offline este concepută pentru dispozitive Android și iOS.
Pentru a începe să o utilizați:

#. Selectați serverul OpenBioMaps care găzduiește proiectul dumneavoastră.
#. Selectați proiectul.
#. Autentificați-vă cu contul dumneavoastră din proiect.
#. Deschideți formularele necesare pentru colectarea datelor în timp ce
   sunteți online, astfel încât acestea să fie descărcate pe dispozitiv.
#. După ce formularele au fost descărcate cu succes, utilizați-le pentru
   colectarea offline a datelor.
#. Reconectați-vă la rețea și sincronizați înregistrările colectate cu
   serverul.

Serverele și proiectele afișate de aplicație depind de serverele
înregistrate, de configurația serverului și de permisiunile de acces ale
utilizatorului.

Este posibil ca dalele hărții de bază vizualizate anterior să rămână
disponibile în memoria cache a dispozitivului sau a browserului, dar
disponibilitatea offline a hărții de bază nu este garantată decât dacă
aplicația și furnizorul hărții acceptă în mod explicit descărcarea hărților
pentru utilizare offline.

Consultați :doc:`Aplicații mobile <mobile_applications>` pentru instrucțiuni
detaliate și limitări.

Cum pot accesa fotografiile realizate cu aplicația mobilă?
----------------------------------------------------------

În funcție de permisiunile dumneavoastră și de configurația proiectului,
atașamentele pot fi accesate:

* individual, de pe pagina fișei de date a unei înregistrări;
* din fila pentru fișiere a interfeței de administrare a proiectului;
* prin funcția disponibilă pentru descărcarea în bloc;
* printr-un API care acceptă descărcarea atașamentelor; sau
* prin funcțiile de gestionare a fișierelor proiectului disponibile
  administratorilor autorizați în Supervisor.

Opțiunile exacte depind de modulele activate și de versiunea OpenBioMaps.
Fotografiile pot conține informații sensibile despre locație, proiect sau
persoane, astfel încât fișierele descărcate trebuie stocate și partajate în
siguranță.

Interfețe și clienți pentru dezvoltatori
========================================

Există o interfață programabilă pentru dezvoltatori?
----------------------------------------------------

Da. OpenBioMaps oferă API-uri pentru accesarea datelor proiectelor și
utilizatorilor, sub rezerva autentificării și a permisiunilor proiectului.

Project Data Service (PDS) acceptă solicitări bazate pe URL-uri. De exemplu,
următoarea solicitare returnează lista proiectelor disponibile pe un server:

``https://openbiomaps.org/pds.php?scope=get_project_list``

Consultați :doc:`Documentația API <api>` pentru punctele finale acceptate,
cerințele de autentificare, parametrii și formatele răspunsurilor.

Unde pot găsi pachetul R OpenBioMaps?
------------------------------------

Versiunea de dezvoltare a pachetului R OpenBioMaps este disponibilă în
`depozitul obm.r al OpenBioMaps <https://github.com/OpenBioMaps/obm.r>`_.

Consultați documentația depozitului pentru instrucțiunile de instalare,
starea actuală și informațiile privind compatibilitatea înainte de a utiliza
pachetul într-un flux de lucru de producție.

Limbi și contribuții
====================

Ce limbi acceptă OpenBioMaps?
-----------------------------

OpenBioMaps este conceput pentru a accepta interfețe de utilizator traduse
și conținut specific proiectelor. Gradul de finalizare a fiecărei traduceri
poate diferi între componentele aplicației și versiuni.

Platforma include în prezent traduceri pentru mai multe limbi, inclusiv
maghiară, engleză, română, spaniolă, portugheză, rusă, germană și franceză.
Unele traduceri pot fi incomplete.

Proiectele individuale își pot selecta propriile limbi și pot furniza
traduceri pentru etichetele și conținutul specific proiectului.

Traducerile pot fi adăugate prin
`platforma de traducere OpenBioMaps
<https://translate.openbiomaps.org>`_.

Cum pot contribui la OpenBioMaps?
---------------------------------

Puteți contribui prin:

* crearea sau întreținerea unui proiect de bază de date OpenBioMaps;
* colectarea sau încărcarea datelor într-un proiect;
* operarea unui server OpenBioMaps;
* găzduirea proiectelor pe serverul dumneavoastră;
* adăugarea unor traduceri noi sau îmbunătățirea celor existente;
* îmbunătățirea documentației;
* raportarea și investigarea problemelor;
* contribuții la dezvoltarea software-ului; sau
* oferirea de sprijin financiar.

Înainte de a contribui cu date sau cod, consultați politicile proiectului
relevant și cerințele privind contribuțiile ale depozitului de cod sursă
corespunzător.

Trebuie să plătesc pentru a utiliza OpenBioMaps?
-----------------------------------------------

Software-ul OpenBioMaps este open source și poate fi utilizat fără o taxă de
licență software. Totuși, operarea unui server, dezvoltarea funcțiilor
specifice proiectului, găzduirea datelor, furnizarea asistenței și
întreținerea infrastructurii pot implica anumite costuri.

Unele instituții găzduiesc gratuit proiectele eligibile, în timp ce altele
pot aplica propriile condiții sau taxe pentru servicii. Contactați operatorul
serverului relevant pentru detalii.

Dezvoltarea și întreținerea includ atât activități voluntare, cât și
activități finanțate. Contribuțiile financiare și în natură la dezvoltarea
OpenBioMaps sunt binevenite.

Stocare, copii de siguranță și recuperarea contului
===================================================

Unde stochează OpenBioMaps datele?
----------------------------------

Fiecare server OpenBioMaps stochează datele proiectelor sale în propriile
baze de date PostgreSQL și în propriul spațiu de stocare a fișierelor.
Acestea pot include înregistrări ale bazei de date, atașamente, configurația
proiectului, fișiere de hartă, jurnale și exporturi generate.

OpenBioMaps nu întreține o singură bază de date centrală care să conțină
toate datele de pe fiecare server.

Există o soluție pentru copiile de siguranță?
---------------------------------------------

Nu există un serviciu centralizat de copiere de siguranță pentru toate
instalările OpenBioMaps, deoarece gestionarea datelor este descentralizată.
Fiecare operator de server este responsabil de implementarea, monitorizarea
și testarea unei proceduri adecvate de copiere de siguranță.

Unii operatori de servere cooperează prin stocarea unor arhive criptate sau
cu acces controlat în infrastructura celorlalți. Aranjamentele privind
copiile de siguranță diferă între servere.

Proprietarii proiectelor trebuie să solicite operatorului serverului
informații despre:

* frecvența și perioada de păstrare a copiilor de siguranță;
* includerea bazelor de date, a atașamentelor și a fișierelor de
  configurare;
* stocarea în afara locației;
* criptare și controlul accesului; și
* frecvența testării restaurării.

O copie de siguranță nu trebuie considerată verificată până când nu a fost
restaurată cu succes într-un mediu de testare.

Mi-am pierdut parola. Cum pot seta una nouă?
--------------------------------------------

Utilizați legătura **Lost password** de pe pagina de autentificare.

Introduceți adresa de e-mail asociată contului dumneavoastră și trimiteți
formularul. Dacă serverul poate trimite e-mailuri, iar adresa aparține unui
cont, sistemul va trimite o legătură care poate fi utilizată pentru accesarea
contului și setarea unei parole noi.

Dacă mesajul nu sosește:

* verificați dosarul de spam sau de mesaje nedorite;
* verificați dacă ați introdus adresa de e-mail corectă;
* așteptați câteva minute înainte de a solicita un alt mesaj; și
* contactați administratorul proiectului sau al serverului.

Din motive de securitate, este posibil ca interfața să nu confirme dacă o
adresă de e-mail este înregistrată.

Depanare
========

De ce apar pătrate roz pe hartă?
--------------------------------

Pătratele roz indică de obicei faptul că o dală sau un strat al hărții nu a
putut fi randat. Cauzele posibile includ:

* o eroare într-un fișier mapfile MapServer;
* o sursă de date nevalidă sau indisponibilă;
* date de autentificare incorecte pentru baza de date sau setări de rețea
  incorecte;
* o problemă de proiecție sau geometrie;
* o denumire incorectă a stratului;
* o eroare MapServer sau MapCache; sau
* o configurație nevalidă pentru interogarea hărții.

Încercați să reîncărcați pagina și verificați dacă problema afectează toate
straturile sau numai unul dintre ele. Administratorii proiectului sau ai
serverului trebuie să examineze jurnalele aplicației și ale MapServer și să
valideze fișierul mapfile afectat.

Gestionarea datelor
===================

Cum pot șterge date?
--------------------

Este posibil ca interfața web standard OpenBioMaps să nu ofere o funcție
generală pentru ștergerea înregistrărilor. Atunci când ștergerea este
necesară, un administrator autorizat al bazei de date poate elimina
înregistrările prin SQL sau printr-un alt flux administrativ acceptat.

Fiecare încărcare are o intrare corespunzătoare în metadatele de sistem ale
încărcărilor. Înregistrările dintr-un tabel al proiectului pot face referire
la încărcarea respectivă printr-un identificator de încărcare. Dacă o cheie
externă configurată corect, cu ștergere în cascadă, conectează metadatele și
tabelele de date, ștergerea rândului de metadate poate șterge și
înregistrările asociate. Existența acestei relații nu este garantată, prin
urmare nu vă bazați pe ștergerea în cascadă fără a examina schema bazei de
date.

De obicei, este mai sigur să identificați și să ștergeți în mod explicit
înregistrările necesare. De exemplu:

.. code-block:: sql

   DELETE FROM your_table
   WHERE uploading_id = x;

Înlocuiți ``your_table``, ``uploading_id`` și ``x`` cu tabelul, coloana de
referință a încărcării și ID-ul încărcării utilizate efectiv de proiect.

Înainte de a executa o ștergere:

#. Creați și verificați o copie de siguranță a bazei de date.
#. Executați o interogare ``SELECT`` echivalentă și examinați fiecare rând
   care ar fi afectat.
#. Verificați tabelele, atașamentele și regulile asociate, precum și
   cerințele de audit.
#. Executați operația într-o tranzacție, acolo unde este posibil.
#. Verificați rezultatul înainte de a confirma tranzacția.
#. Înregistrați cine a efectuat ștergerea și motivul acesteia.

Ștergerea poate afecta istoricul de audit, rândurile cu reguli de acces,
atașamentele, înregistrările legate, sintezele și copiile externe. Consultați
politica proiectului privind datele și cerințele de păstrare înainte de a
elimina definitiv datele.

Modelul de deschidere RUM
=========================

Ce este RUM?
------------

RUM face parte din modelul RUM/FILH pentru descrierea capacităților
operaționale și a gradului de deschidere al bazelor de date privind
biodiversitatea. Consultați publicația
`RUM/FILH: a standardized operational capability model for biodiversity
databases <https://doi.org/10.1093/database/baag044>`_.

RUM înseamnă:

* **R — Read**
* **U — Upload**
* **M — Modify**

Fiecare capacitate poate avea una dintre cele trei valori:

.. list-table::
   :header-rows: 1
   :widths: 15 30 55

   * - Valoare
     - Semnificație
     - Culoarea tradițională de afișare
   * - ``-``
     - Nu este publică
     - Negru
   * - ``0``
     - Parțial publică
     - Roșu
   * - ``+``
     - Publică
     - Verde

De exemplu, o bază de date poate oferi acces de citire parțial public, acces
public pentru încărcare și niciun acces public pentru modificare. Cele trei
capacități trebuie interpretate întotdeauna împreună cu politica detaliată de
acces a proiectului.

DOI-uri și citare
=================

Se poate atribui un DOI unei baze de date?
------------------------------------------

Da. Unei baze de date sau unui set de date definit, aflat într-o stare
suficient de stabilă și documentată, i se poate atribui un DOI prin serviciul
DataCite DOI, sub rezerva procedurii organizației care operează serverul
OpenBioMaps.

Bazele de date OpenBioMaps pot furniza o pagină cu metadatele DOI. De
exemplu:

``https://dinpi.openbiomaps.org/projects/danubefish/index.php?metadata``

Prefixul DataCite al OpenBioMaps este ``10.18426``. Sufixele DOI sunt
generate în mod unic.

Un proiect poate atribui DOI-uri suplimentare și seturilor de date
individuale. Înainte de emiterea unui DOI, verificați versiunea setului de
date, autorii, titlul, anul publicării, licența, condițiile de acces,
editorul și persistența paginii de destinație. Un DOI trebuie să conducă la
o pagină de destinație stabilă, care conține suficiente metadate și
informații privind accesul.
