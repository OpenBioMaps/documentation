:author: Miklós Bán
:date: 2026-08-08

Setări administrative
**********************

Interfața de administrare a proiectului oferă instrumente pentru configurarea
unui proiect OpenBioMaps, gestionarea utilizatorilor și a structurilor sale de
date și monitorizarea serviciilor asociate proiectului. Paginile disponibile
unui administrator depind de permisiunile administratorului, configurația
proiectului, modulele instalate și mediul serverului.

Această pagină oferă o prezentare generală a setărilor și instrumentelor
administrative. Unele setări afectează accesul la datele proiectului sau
modifică baza de date subiacentă. Prin urmare, administratorii trebuie să
analizeze cu atenție modificările și să le testeze înainte de a le aplica unui
proiect aflat în producție.

Pentru o prezentare generală a documentației privind administrarea
proiectului, consultați
:doc:`Administrarea proiectului <../admin_pages>`.


.. _administrative-access:

Acces administrativ
===================

Secțiunea **Acces administrativ** permite administratorilor de proiect să
delege grupurilor de utilizatori funcții administrative individuale. Fiecare
funcție disponibilă prin interfața de administrare a proiectului poate fi
atribuită unuia sau mai multor grupuri.

Aceasta oferă un control detaliat asupra persoanelor care pot efectua sarcini
administrative. De exemplu, un proiect ar putea defini următoarele grupuri:

* **Manageri de utilizatori**, cu acces la gestionarea utilizatorilor și a
  grupurilor;
* **Administratori de date**, cu acces la denumirile speciilor, atașamente și
  instrumentele de gestionare a datelor; și
* **Editori ai formularelor de încărcare**, cu acces la gestionarea
  formularelor de încărcare.

Acordați numai permisiunile necesare pentru fiecare rol administrativ.
Funcțiile care modifică structurile bazei de date, execută SQL, gestionează
reguli de acces sau editează cod executabil trebuie să fie limitate la
administratori de încredere.

.. TODO: Documentați fiecare funcție administrativă care poate fi atribuită
   și permisiunile pe care le acordă. De asemenea, trebuie clarificat dacă
   permisiunile moștenite prin grupuri imbricate sunt evaluate recursiv și
   dacă un utilizator trebuie să se autentifice din nou după modificarea
   permisiunilor sale administrative.


.. _database-columns:

Tabelele și coloanele bazei de date
===================================

Secțiunea **Tabelele și coloanele bazei de date** este utilizată pentru
crearea și gestionarea tabelelor, vizualizărilor și coloanelor SQL asociate
unui proiect. Obiectele înregistrate prin această interfață sunt adăugate la
metadatele OpenBioMaps și, prin urmare, pot deveni disponibile pentru
formulare de încărcare, interogări, module și alte interfețe OpenBioMaps.

Tabelele și coloanele create direct printr-un client SQL standard nu sunt
înregistrate automat. Acestea trebuie adăugate și la metadatele OpenBioMaps
corespunzătoare înainte de a putea fi utilizate prin aplicația web.

.. TODO: Explicați cum poate fi înregistrat un tabel sau o vizualizare SQL
   existentă fără a fi recreată. Documentați ce tabele de metadate sunt
   modificate de această interfață și dacă obiectele bazei de date create în
   afara interfeței pot fi importate în siguranță.


Denumirea tabelelor și coloanelor
---------------------------------

Utilizați litere mici, cifre și caractere de subliniere pentru denumirile
tabelelor și coloanelor. Evitați spațiile, caracterele cu diacritice,
identificatorii între ghilimele și alte caractere speciale. Denumirile
trebuie să fie descriptive și să rămână stabile după ce formularele,
interogările sau modulele încep să le utilizeze.

La crearea unui tabel sau a unei coloane trebuie furnizată o descriere.
Aceste descrieri fac parte din metadatele proiectului și ajută utilizatorii
să înțeleagă semnificația și utilizarea preconizată a datelor.

.. TODO: Documentați toate regulile de denumire impuse de interfață,
   inclusiv lungimile maxime, denumirile rezervate, gestionarea schemelor și
   dacă o denumire poate începe cu o cifră.


Înregistrarea coloanelor disponibile
------------------------------------

Administratorii pot selecta coloanele disponibile la crearea formularelor
de încărcare și a interfețelor de interogare. O coloană care există în
PostgreSQL, dar care nu este înregistrată ca fiind disponibilă, nu va apărea
automat în aceste interfețe.

Coloanelor li se pot atribui și roluri semantice. Aceste roluri permit
OpenBioMaps și modulelor sale să identifice câmpuri importante fără a se
baza pe o denumire de coloană specifică proiectului. În funcție de proiect
și de modulele instalate, rolurile pot identifica câmpuri care conțin:

* o denumire științifică;
* o denumire alternativă a taxonului;
* data unei observații;
* un colector de date;
* o locație sau o geometrie;
* un număr de indivizi;
* valori pentru latitudine și longitudine;
* o citare; sau
* un atașament.

.. TODO: Furnizați o listă completă a rolurilor semantice și identificați
   funcțiile de bază sau modulele care utilizează fiecare rol. Clarificați
   dacă mai multe coloane pot avea același rol și dacă o coloană poate avea
   mai multe roluri.


Tipuri de coloane
-----------------

Interfața administrativă oferă următoarele tipuri de coloane sau roluri
semantice documentate:

``Data``
   O coloană de date de uz general.

``Spatial Geometry``
   O coloană de geometrie utilizată pentru hărți și operații spațiale.

``Scientific Species Name``
   O coloană pentru denumirea științifică, utilizată de funcțiile de
   gestionare a taxonilor.

``Alternative Names``
   O coloană pentru denumiri alternative, utilizată de funcțiile de
   gestionare a taxonilor.

``Date``
   O coloană de tip dată sau dată și oră, utilizată de filtrele de dată.

``Number of Individuals``
   O coloană numerică utilizată de funcțiile de sintetizare.

``Latitude/Longitude``
   O coloană de coordonate utilizată pentru crearea geometriei spațiale.

``Citing``
   O coloană referitoare la citări, utilizată de funcțiile de sintetizare.

``Attachment``
   O coloană care face referire la atașamentele încărcate.

``UTM Zone``
   O coloană pentru zona UTM, utilizată atunci când geometria spațială este
   creată din coordonate.

.. TODO: Confirmați că aceste denumiri corespund etichetelor actuale din
   interfața de administrare. Explicați relația dintre aceste tipuri
   semantice și tipurile de date PostgreSQL și documentați orice tip
   PostgreSQL necesar pentru fiecare opțiune.

.. TODO: Clarificați cum sunt asociate coloanele de latitudine și longitudine
   și cum sunt determinate zona UTM, sistemul de referință al coordonatelor
   și emisfera în timpul creării geometriei.


Descrierile și comenzile coloanelor
-----------------------------------

Câmpul **Comment** conține o descriere a conținutului coloanei. Se recomandă
adăugarea unei descrieri relevante, deoarece aceasta contribuie la
metadatele proiectului.

Câmpul **Command** poate fi utilizat pentru a efectua anumite operații sau
pentru a atribui setări unei coloane. Comenzile documentate includ:

``SET srid:4326``
   Atribuie SRID 4326 coloanei ``obm_geometry``. Înlocuiți ``4326`` cu
   identificatorul de referință spațială necesar proiectului.

``SET use_rules:1``
   Activează gestionarea regulilor de acces pentru coloana ``obm_id``.

``RENAME:new_name``
   Redenumește o coloană în ``new_name``.

``DROP``
   Șterge coloana.

Redenumirea sau ștergerea unei coloane poate invalida formulare de
încărcare, șabloane de interogare, module, vizualizări, triggere și aplicații
externe care fac referire la aceasta. Actualizați toate configurațiile
dependente înainte de a efectua oricare dintre aceste operații și creați o
copie de siguranță a bazei de date atunci când este cazul.

.. TODO: Confirmați sintaxa exactă, sensibilitatea la majuscule și minuscule
   și țintele acceptate pentru fiecare comandă. Explicați dacă aceste comenzi
   sunt executate imediat și dacă interfața verifică dependențele bazei de
   date înainte de redenumirea sau ștergerea unei coloane.

.. TODO: Clarificați dacă ``SET srid`` modifică numai metadatele sau
   transformă coordonatele existente. Modificarea unui SRID fără
   transformarea valorilor coordonatelor poate duce la date spațiale
   nevalide.

.. TODO: Explicați ce modifică ``SET use_rules:1`` și dacă această comandă
   creează, activează sau doar înregistrează regulile de acces la nivel de
   rând ale proiectului.


Consolă SQL
-----------

O consolă SQL este disponibilă și administratorilor de sistem. Consola SQL
poate fi utilizată pentru a modifica sau șterge datele proiectului și
structurile bazei de date. Din acest motiv, accesul (la interfața tabelelor
bazei de date) trebuie acordat numai utilizatorilor de încredere care au
suficientă experiență cu PostgreSQL și cu sarcinile de administrare a
sistemului OpenBioMaps.

Interogările executate în consola SQL pot fi salvate și executate din nou.

Consola afișează rezultatele interogării într-un tabel dinamic. Rezultatele
tabelului de interogare pot fi exportate ca fișier CSV. Dacă rezultatele
interogării conțin mai mult de 1.000 de rânduri, tabelul nu mai este afișat;
în schimb, este generat automat un export CSV.


Gestionarea vizualizărilor
--------------------------

Un tabel de date poate fi înlocuit cu o vizualizare pentru a furniza o
reprezentare personalizată a datelor sale sau pentru a îmbunătăți un anumit
flux de lucru. Procesul documentat creează o schemă cu aceeași denumire ca
tabelul original, mută tabelul original în schema respectivă și creează o
vizualizare în locul său anterior. Regulile corespunzătoare ``INSERT``,
``UPDATE`` și ``DELETE`` asigură operațiile de scriere acolo unde sunt
configurate.

Această abordare poate fi utilă pentru tabele mari afectate de fluxuri de
lucru sau triggere costisitoare. Ea modifică în mod semnificativ structura
bazei de date și poate afecta formulare, interogări, module, chei externe,
triggere, copii de siguranță și clienți externi.

.. TODO: Documentați transformarea exactă efectuată atunci când un tabel
   este înlocuit cu o vizualizare, inclusiv denumirile obiectelor,
   proprietatea, privilegiile, secvențele, indecșii, constrângerile, cheile
   externe și regulile de scriere generate. De asemenea, trebuie furnizată o
   procedură acceptată de revenire la starea anterioară.

.. TODO: Explicați ce probleme de performanță este destinată să rezolve
   această funcție. Înlocuirea unui tabel cu o vizualizare nu îmbunătățește
   în sine performanța, astfel încât trebuie descrise definiția preconizată a
   vizualizării și strategia de optimizare.


.. _data-access-check:

Acces la date
=============

Secțiunea **Acces la date** sintetizează configurația de acces a proiectului
și starea actuală a regulilor de acces la nivel de rând. Administratorii pot
inspecta nivelurile de citire și modificare aplicate proiectului și
tabelelor sale de date gestionate.

Interfața include:

* nivelurile configurate pentru citirea și modificarea datelor;
* starea restricțiilor de acces pentru tabelele de date individuale;
* controale pentru activarea sau dezactivarea restricțiilor configurate;
* starea triggerelor utilizate pentru menținerea regulilor de acces; și
* legături către documentația aferentă.

Nivelurile de acces documentate sunt:

``everybody``
   Accesul nu este limitat la utilizatorii autentificați.

``logged-in users``
   Accesul necesită autentificare.

``specified group members``
   Accesul este controlat prin grupurile proiectului și reguli mai
   specifice.

Accesul efectiv la o înregistrare poate fi afectat de reguli la nivel de
proiect, de rând și de coloană. Pentru o prezentare generală detaliată,
consultați :doc:`Acces la date <../data_access>`.

Interfața este disponibilă prin **Profile > Project administration >
Data access**. Unele valori implicite subiacente pot fi definite și în
fișierul de configurare ``local_vars.php.inc`` al proiectului.

.. TODO: Confirmați etichetele actuale de navigare și asociați etichetele
   interfeței ``everybody``, ``logged-in users`` și
   ``specified group members`` cu valorile de configurare corespunzătoare.

.. TODO: Documentați modificările care pot fi efectuate direct prin această
   pagină și pe cele care necesită în continuare editarea
   ``local_vars.php.inc``. Explicați cum sunt soluționate conflictele dintre
   setările interfeței și valorile fișierului de configurare.


.. _group-settings:

Grupuri
=======

Secțiunea **Grupuri** permite administratorilor să creeze și să gestioneze
grupuri de utilizatori ai proiectului. Grupurile sunt utilizate pentru a
atribui acces la date, formulare de încărcare, module și funcții
administrative.

Administratorii pot:

* crea un grup;
* adăuga utilizatori într-un grup sau elimina utilizatori dintr-un grup;
* adăuga grupuri în alte grupuri acolo unde sunt acceptate grupurile
  imbricate; și
* utiliza grupurile rezultate în alte interfețe de gestionare a accesului.

Grupurile imbricate pot asigura o structură de permisiuni reutilizabilă și
scalabilă. Totuși, acestea trebuie păstrate suficient de simple pentru ca
administratorii să poată determina permisiunile efective ale unui anumit
utilizator.

.. TODO: Explicați comportamentul exact al grupurilor imbricate, inclusiv
   apartenența recursivă, prevenirea referințelor circulare și prioritatea
   permisiunilor. Documentați dacă ștergerea unui grup elimină referințele
   sale din formularele de încărcare, regulile de acces, module și
   permisiunile administrative.

.. TODO: Clarificați dacă denumirile grupurilor pot fi modificate după ce un
   grup este utilizat în reguli de acces și dacă regulile de acces stochează
   identificatorul sau denumirea grupului.


.. _upload-forms:

Formulare de încărcare
======================

Formularele de încărcare determină modul în care datele pot fi introduse sau
importate în tabelele proiectului. Acestea definesc câmpurile disponibile,
controalele de introducere, regulile de validare și setările de acces pentru
un flux de lucru de colectare a datelor.

Pentru instrucțiuni detaliate, consultați
:doc:`Gestionarea formularelor de încărcare <../upload_forms>`.


.. _trigger-functions:

Funcții
=======

Secțiunea **Funcții** oferă instrumente pentru examinarea regulilor și
triggerelor SQL asociate tabelelor și vizualizărilor proiectului. Aceasta
include liste separate cu regulile și triggerele înregistrate pentru fiecare
tabel și furnizează șabloane pentru anumite funcții de trigger.

Interfața poate crea, edita, activa sau dezactiva următoarele tipuri de
triggere documentate:

* triggere pentru lista de taxoni;
* triggere pentru istoric; și
* triggere pentru reguli de acces.

În plus, aici pot fi create și configurate și triggere și reguli
personalizate.

Triggerele bazei de date se execută automat atunci când datele se modifică.
Un trigger incorect poate respinge modificări valide, poate modifica datele
în mod neașteptat sau poate slăbi controlul accesului. Testați funcțiile de
trigger personalizate înainte de a le activa într-un proiect aflat în
producție.


Trigger pentru lista de taxoni
------------------------------

Triggerul pentru lista de taxoni inserează denumirile științifice necunoscute
anterior dintr-un câmp configurat pentru denumirea speciei în tabelul de
taxoni al proiectului. Acesta poate ajuta la întreținerea unui proiect a
cărui listă de specii se extinde pe măsură ce sunt adăugate observații.

Denumirile speciilor adăugate în tabelul de taxoni pot fi acum gestionate
prin interfața de gestionare a denumirilor taxonilor.

:ref:`Setări administrative: denumirile speciilor <species-names>`


Trigger pentru istoric
----------------------

Triggerul pentru istoric înregistrează modificările aduse înregistrărilor
din tabelul țintă. Istoricul rezultat poate fi afișat prin interfața
istoricului datelor înregistrării.

.. TODO: Documentați operațiile și valorile înregistrate de triggerul pentru
   istoric. Clarificați dacă acesta stochează valorile anterioare și noi ale
   câmpurilor, marcajele temporale, identitățile editorilor, identificatorii
   tranzacțiilor sau numai un număr de modificări. De asemenea, trebuie
   descrise cerințele privind păstrarea, accesul, restaurarea și stocarea.


Trigger pentru reguli de acces
------------------------------

Triggerul pentru reguli de acces menține regulile de acces la nivel de rând
pentru înregistrările dintr-un tabel al proiectului. Acesta poate deriva
restricții dintr-un câmp configurat pentru sensibilitate și poate transfera
permisiunile de citire și scriere din formularul de încărcare utilizat
pentru crearea unei înregistrări.

De exemplu, dacă un formular de încărcare acordă acces de citire grupurilor
A și B și acces de scriere grupului C, triggerul poate adăuga aceste
atribuiri în intrarea din tabelul de reguli asociată fiecărei înregistrări
create prin formularul respectiv.

Acest trigger este relevant pentru proiectele care utilizează restricții de
acces la nivel de grup sau de rând. Configurația sa trebuie să fie
consecventă cu setările generale de acces ale proiectului și cu schema
tabelului de reguli.

Pentru mai multe informații, consultați
:doc:`Acces la date <../data_access>`.

.. TODO: Explicați modul în care triggerul gestionează înregistrările create
   prin SQL, API sau un alt proces care nu are asociat niciun formular de
   încărcare. Documentați comportamentul său atunci când o înregistrare este
   actualizată, mutată între încărcări sau ștearsă.

.. TODO: Clarificați dacă activarea triggerului creează reguli pentru
   înregistrările existente sau numai pentru modificările ulterioare.
   Trebuie documentată o procedură acceptată pentru regenerarea și validarea
   tuturor regulilor.


.. _species-names:

Denumirile speciilor
====================

Secțiunea **Denumirile speciilor** gestionează tabelul de taxoni al
proiectului. Denumirile speciilor pot fi atribuite următoarelor categorii
documentate:

* denumire acceptată;
* sinonim;
* denumire comună; și
* denumire scrisă greșit.

Denumirile stocate în tabelul de taxoni sunt utilizate de interfețele de
căutare asociate taxonilor și de activitățile de fundal care detectează sau
corectează denumirile taxonilor.

.. TODO: Confirmați denumirile actuale ale categoriilor și corectați, dacă
   este necesar, ortografia lui ``misspelled`` în interfața sursă.
   Documentați relațiile permise între denumirile acceptate, sinonime,
   denumirile comune și variantele scrise greșit.

.. TODO: Explicați ce câmpuri taxonomice sunt stocate, cum pot fi importate
   sau exportate denumirile și cum previne interfața relațiile duplicate sau
   circulare între sinonime.

.. TODO: Identificați denumirea și comportamentul actual al funcționalității
   ``taxon-name-repair-background-jobs`` și adăugați o legătură către
   instrucțiunile sale de configurare.


.. _localisation:

Traduceri
=========

OpenBioMaps utilizează traduceri globale și specifice proiectului.


Traduceri globale
-----------------

Traducerile globale pot fi adăugate și îmbunătățite prin
`platforma de traducere OpenBioMaps
<https://translate.openbiomaps.org/>`_. Platforma conține traduceri pentru
aplicația web, aplicațiile mobile și alte componente OpenBioMaps.
Colaboratorii pot propune și o limbă nouă.

.. TODO: Documentați fluxul de lucru al platformei de traducere pentru
   conturi, verificare și lansare. Explicați când devine disponibilă pe un
   server OpenBioMaps o traducere globală acceptată.


Traduceri locale
----------------

Traducerile locale permit unui proiect să definească texte de interfață
specifice proiectului. Cheile de traducere utilizează prefixul ``str_``
urmat de un identificator descriptiv în limba engleză. De exemplu, un
proiect ar putea defini ``str_observations`` și ar putea furniza traducerea
acestuia în fiecare limbă activă.

Un exemplu public este disponibil la:

https://openbiomaps.org/projects/checkitout/upload/?form=426&type=web

.. TODO: Documentați unde sunt create traducerile locale, cum sunt selectate
   limbile active, ce componente recunosc cheile locale și ce se întâmplă
   atunci când lipsește o traducere. Clarificați dacă traducerile locale
   înlocuiesc șirurile globale care utilizează aceeași cheie.

.. TODO: Înlocuiți sau completați exemplul public cu o captură de ecran
   stabilă sau cu o descriere, deoarece proiectul și identificatorul
   formularului din legătură se pot modifica.


.. _module-settings:

Module
======

Modulele extind funcționalitatea disponibilă într-un proiect OpenBioMaps.
Configurația și cerințele lor de acces depind de fiecare modul în parte.

Modulele extind funcționalitatea disponibilă într-un proiect OpenBioMaps.
Configurația și cerințele lor de acces depind de fiecare modul în parte.
Modulele oferă adesea funcții de bază, precum interfețe de căutare textuală
pe pagina hărții; în alte cazuri, acestea oferă instrumente specifice
anumitor sarcini. Comportamentul modulelor poate fi adesea personalizat.

Pentru mai multe informații, consultați :doc:`Module <../modules>`.


.. _interrupted-uploads:

Încărcări întrerupte
====================

Secțiunea **Încărcări întrerupte** enumeră încărcările de fișiere salvate
sau nefinalizate și sesiunile de introducere a datelor prin formulare web.
În funcție de starea sa, o încărcare întreruptă poate fi restaurată sau
eliminată.

Administratorii trebuie să verifice că o încărcare nu mai este necesară
înainte de a o șterge. O încărcare întreruptă poate conține activități pe
care proprietarul său intenționează să le reia.

.. TODO: Documentați cine poate vizualiza, relua sau șterge încărcarea
   întreruptă a altui utilizator. Explicați diferența dintre o încărcare
   salvată manual, o copie de siguranță automată și o încărcare întreruptă.

.. TODO: Specificați perioadele de păstrare, limitele de stocare, regulile de
   curățare automată și dacă ștergerea unei încărcări întrerupte șterge și
   fișierele temporare încărcate ale acesteia.


.. _file-manager:

Manager de fișiere
==================

Secțiunea **Manager de fișiere** oferă instrumente pentru gestionarea
atașamentelor încărcate în proiect. Aceasta poate fi utilizată pentru a
răsfoi atașamentele, a examina asocierile acestora cu înregistrările bazei
de date și a crea exporturi.

Funcțiile documentate includ:

* enumerarea atașamentelor încărcate;
* filtrarea și sortarea atașamentelor;
* editarea comentariilor fișierelor;
* asocierea atașamentelor cu înregistrări de date;
* gestionarea asocierilor de fișiere existente; și
* exportarea atașamentelor asociate unui tabel de date.

Un export în bloc este procesat ca activitate de fundal. După finalizarea
procesării, sistemul furnizează o legătură pentru descărcarea arhivei
rezultate.

Accesul la funcțiile de gestionare și exportare a atașamentelor trebuie
limitat la utilizatorii autorizați. Fișierele exportate rămân supuse
cerințelor proiectului privind accesul la date și confidențialitatea.

.. TODO: Confirmați filtrele disponibile și metadatele editabile.
   Documentați formatele de atașamente care pot fi previzualizate și dacă
   modificarea asocierii unui fișier actualizează și înregistrarea
   corespunzătoare.

.. TODO: Explicați modul în care exporturile de atașamente aplică regulile de
   acces la nivel de rând și de coloană, unde sunt stocate arhivele
   generate, cât timp rămân valabile legăturile de descărcare și cine le
   poate utiliza.

.. TODO: Clarificați dacă este acceptată ștergerea unui fișier prin această
   interfață și ce se întâmplă cu înregistrările, metadatele, miniaturile și
   copiile de siguranță care fac referire la fișierul șters.


.. _sql-query-settings:

Setări pentru interogări SQL
============================

Secțiunea **Setări pentru interogări SQL** definește șabloanele utilizate
pentru alcătuirea interogărilor pentru straturile MapServer și pentru
rezultatele interogărilor textuale din aplicația web. Aceste șabloane
seamănă cu SQL, dar includ substituenți OpenBioMaps care sunt înlocuiți
dinamic de interpretorul de interogări.

Fiecare șablon de interogare trebuie conectat la un strat al hărții web.
Într-un mapfile MapServer, un strat WMS care utilizează o interogare generată
dinamic trebuie să conțină o definiție ``DATA`` cu substituentul ``%query%``.

Șabloanele de interogare pot conține substituenți delimitați de semne de
procent. Funcțiile de bază și modulele instalate pot înlocui acești
substituenți cu fragmente SQL în timpul execuției.

.. TODO: Furnizați o referință completă pentru toți substituenții acceptați,
   inclusiv pozițiile valide, valorile de înlocuire, dependențele și
   constrângerile de securitate ale acestora. Textul sursă face referire atât
   la ``%morefilter%``, cât și la ``%morefilters%``; confirmați care formă
   este validă.


Șablon de interogare de bază
----------------------------

Un șablon de interogare poate utiliza substituenți precum ``%qstr%`` pentru
condițiile interogării și ``%morefilter%`` pentru filtre suplimentare:

.. code-block:: sql

   SELECT obm_id, %grid_geometry% AS obm_geometry
       %selected%
   FROM %F%checkitout c%F%
       %uploading_join%
       %rules_join%
       %taxon_join%
       %grid_join%
       %search_join%
       %morefilter%
   WHERE %geometry_type% %envelope% %qstr%

Marcajele ``%F%`` identifică relația principală ``FROM`` și aliasul acesteia,
astfel încât interpretorul să poată diviza și extinde șablonul.

.. TODO: Explicați de ce relația principală trebuie încadrată de marcaje
   ``%F%``, dacă sunt acceptate denumirile calificate cu schema și cele între
   ghilimele și ce aliasuri sunt disponibile fragmentelor generate.


Adăugarea îmbinărilor
---------------------

Îmbinările suplimentare pot fi încadrate de marcaje ``%J%``:

.. code-block:: sql

   SELECT
       n.obm_geometry,
       n.obm_id,
       -2 AS date_part,
       nestbox_type,
       project_id,
       beinaction
       %selected%
   FROM %F%public_nestbox_data n%F%
       %J%LEFT JOIN public_nestbox_data_observations o
           ON o.nestbox_id = n.obm_id%J%
       %taxon_join%
       %morefilter%
   WHERE %envelope% %qstr%

.. TODO: Explicați cum sunt procesate mai multe blocuri ``%J%`` și dacă
   interpretorul poate elimina o îmbinare atunci când niciunul dintre
   câmpurile sau filtrele selectate nu o necesită.


Șabloane de interogare complexe
-------------------------------

Șabloanele pot utiliza și expresii comune de tabel și alte construcții SQL:

.. code-block:: sql

   WITH aall AS (
       SELECT
           o.obm_id,
           n.obm_geometry,
           nestbox_type,
           project_id,
           beinaction,
           COALESCE(
               EXTRACT(DAY FROM (CURRENT_DATE - datum)::interval),
               '-1'
           ) AS date_part
           %selected%
       FROM %F%public_nestbox_data_observations o%F%
           %J%LEFT JOIN public_nestbox_data n
               ON nestbox_id = n.obm_id%J%
           %taxon_join%
           %morefilter%
       WHERE 1 = 1 %envelope% %qstr%
   )
   SELECT *
   FROM aall
   ORDER BY date_part DESC

Un șablon simplu obișnuit are următoarea formă:

.. code-block:: sql

   SELECT obm_id, obm_geometry %selected%
   FROM %F%checkitout c%F%
       %uploading_join%
       %rules_join%
       %taxon_join%
       %morefilter%
   WHERE %geometry_type% %envelope% %qstr%

Șabloanele de interogare afectează atât corectitudinea, cât și accesul la
date. O îmbinare incorectă sau un substituent lipsă pentru regulile de acces
poate expune înregistrări sau câmpuri care ar trebui restricționate. Testați
fiecare interogare ca utilizator public, autentificat și specific unui grup
înainte de a o face disponibilă.

.. TODO: Documentați substituenții de control al accesului care sunt
   obligatorii și dacă aplicația respinge șabloanele care îi omit.
   Explicați cum sunt escapate sau asociate valorile parametrilor pentru a
   preveni injectarea SQL.

.. TODO: Adăugați o procedură pentru testarea unui șablon, inspectarea
   codului SQL generat, diagnosticarea erorilor substituenților și
   restaurarea versiunii anterioare.


.. _map-settings:

Setări pentru hartă
===================

Secțiunea **Setări pentru hartă** configurează straturile spațiale din harta
web și definițiile MapServer corespunzătoare. Setările hărții web și ale
MapServer trebuie să rămână consecvente, astfel încât straturile să utilizeze
sursa de date, proiecția, extinderea și stilul preconizate.


Straturile hărții web
---------------------

Setările hărții web configurează interfața de hartă bazată pe OpenLayers.
Administratorii pot defini setări precum:

* centrul inițial al hărții și nivelul de zoom;
* hărțile de bază și straturile suprapuse disponibile;
* straturile vizibile în mod implicit;
* asocierea dintre straturi, tabelele proiectului și șabloanele de
  interogare; și
* anumite aspecte ale aspectului și comportamentului straturilor.

.. TODO: Documentați fiecare setare OpenLayers editabilă, formatul
   preconizat, valoarea implicită și sistemul de referință al coordonatelor
   acceptat. Explicați cum sunt configurate ordinea straturilor, intervalele
   de vizibilitate, opacitatea, legendele și posibilitatea de interogare.


Setări MapServer
----------------

Administratorii avansați pot edita direct fișierul mapfile MapServer al
proiectului. Fișierul mapfile definește sursele de date ale straturilor,
sistemele de referință spațială, extinderile, stilurile și opțiunile de
randare.

Modificările unui fișier mapfile pot face indisponibile straturile
proiectului sau pot expune o sursă de date neintenționată. Păstrați o
versiune funcțională și validați fișierul mapfile editat înainte de a
implementa modificările.

.. TODO: Documentați unde este stocat fișierul mapfile, dacă editările sunt
   versionate, cum poate fi validată sintaxa acestuia și cum poate fi
   restaurată o configurație anterioară.

.. TODO: Explicați ce părți ale fișierului mapfile sunt generate de
   OpenBioMaps și care pot fi editate în siguranță fără a fi suprascrise.


Sisteme de referință spațială
-----------------------------

Straturile hărții trebuie să utilizeze sisteme de referință spațială
definite corect. SRID configurat determină modul în care coordonatele sunt
interpretate și transformate atunci când datele din surse diferite sunt
afișate împreună.

Setările privind extinderea și proiecția hărții controlează zona și sistemul
de coordonate afișate de harta web. Acestea trebuie să fie compatibile cu
datele straturilor, configurația MapServer și setările OpenLayers.

.. TODO: Identificați proiecția necesară pentru harta web, proiecțiile sursă
   acceptate și locul în care au loc transformările. Includeți recomandări
   pentru alegerea unei extinderi și diagnosticarea straturilor afișate
   într-o locație greșită.


.. _member-settings:

Membri
======

Secțiunea **Membri** enumeră utilizatorii înregistrați în proiect.
Administratorii pot gestiona apartenența la proiect, starea și atribuirile
de grupuri.

Stările documentate ale membrilor sunt:

``Normal``
   Utilizatorul primește permisiunile standard de încărcare și interogare
   ale proiectului. Atribuirile mai specifice de grupuri și regulile de acces
   pot modifica aceste permisiuni.

``Operator``
   Utilizatorul are acces la toate funcțiile și datele proiectului.

``Suspended``
   Utilizatorul nu poate accesa funcțiile sau datele proiectului. Suspendarea
   unui utilizator este similară cu dezactivarea apartenenței sale la
   proiect, dar nu îi șterge profilul.

Fondatorul proiectului are acces complet la proiect și nu trebuie să
primească starea de operator. Atribuirile de grupuri pot fi modificate pe
această pagină, deși interfața **Grupuri** poate fi mai potrivită pentru
gestionarea mai multor utilizatori.

Pentru setări conexe, consultați :ref:`Grupuri <groups>` și
:ref:`Acces administrativ <administrative-access>`.

.. TODO: Confirmați denumirile actuale ale stărilor și definiți permisiunile
   exacte ale fondatorilor, proprietarilor, gazdelor, operatorilor și
   utilizatorilor obișnuiți. Aceste denumiri de roluri trebuie armonizate în
   întreaga documentație.

.. TODO: Explicați dacă suspendarea afectează numai proiectul curent sau
   contul utilizatorului de la nivelul întregului server. Documentați
   efectul acesteia asupra tokenurilor API, sesiunilor active, activităților
   programate, proprietății înregistrărilor, invitațiilor și mesajelor.


Vizualizarea profilului altui utilizator
----------------------------------------

Numele unui membru trimite la pagina sa de profil. Administratorii cu
permisiunea necesară pot vedea o pictogramă de utilizator secret în zona din
dreapta sus a paginii. Această funcție deschide profilul altui utilizator,
în timp ce administratorul rămâne autentificat cu propriul cont.

Pictograma utilizată de interfață este documentată de
`Fork Awesome
<https://forkaweso.me/Fork-Awesome/icon/user-secret/>`_.

Această funcție poate expune informații cu caracter personal și conținut
specific utilizatorului. Accesul trebuie restricționat, iar utilizarea sa
trebuie să respecte politicile proiectului privind confidențialitatea și
auditarea.

.. TODO: Clarificați dacă această funcție uzurpă identitatea utilizatorului
   sau permite numai o vizualizare administrativă a profilului. Documentați
   acțiunile permise, dacă utilizatorul afectat este notificat și dacă
   accesul este înregistrat într-un jurnal de audit.


.. _message-templates:

Șabloane de mesaje
==================

Editorul de șabloane de mesaje este momentan indisponibil.

Mesajele trimise automat de sistem sau de un proiect sunt generate pe baza
unor șabloane. OpenBioMaps furnizează șabloane globale pentru tipurile de
mesaje implementate, iar un proiect poate crea versiuni locale care le
înlocuiesc.

Pentru a personaliza un șablon global, selectați-l, editați-i conținutul și
salvați-l ca versiune locală. Șabloanele pot conține variabile care sunt
înlocuite la trimiterea mesajului. Variabilele acceptate de un anumit șablon
sunt definite de funcția, modulul sau activitatea de fundal care îl trimite.

Pot fi create șabloane noi și pentru module și activități de fundal
personalizate.

.. TODO: Documentați câmpurile șablonului, formatele de mesaje acceptate,
   gestionarea limbilor, ordinea de rezervă și procedura de revenire de la o
   versiune locală la versiunea globală.

.. TODO: Explicați dacă este escapat conținutul șablonului și ce elemente
   HTML sau marcaje sunt permise. Editarea șabloanelor trebuie evaluată
   pentru riscuri precum legături nesigure, injectarea HTML și divulgarea
   neintenționată a variabilelor.


Variabile și șabloane incluse
-----------------------------

Variabilele sunt scrise între semne de procent, de exemplu
``%USER_NAME%``. Sunt documentate următoarele variabile globale:

``%PROJECT_TABLE%``
   Identificatorul bazei de date sau denumirea tabelului proiectului.

``%PROJECT_TITLE%``
   Descrierea scurtă a proiectului.

``%PROJECT_DESCRIPTION%``
   Descrierea detaliată a proiectului.

``%USER_NAME%``
   Numele destinatarului sau al utilizatorului relevant.

``%URL%``
   Un URL asociat mesajului.

``%OB_DOMAIN%``
   Domeniul OpenBioMaps asociat mesajului.

``%DOMAIN%``
   Numele de domeniu definit în tabelul ``projects``.

``%PROTOCOL%``
   Protocolul definit în tabelul ``projects``.

Un șablon poate include un alt șablon. De exemplu, adăugarea ``@footer@``
include șablonul denumit ``footer``.

.. TODO: Confirmați semnificația și disponibilitatea exactă a fiecărei
   variabile globale. În special, diferențiați ``%PROJECT_TABLE%``,
   ``%OB_DOMAIN%``, ``%DOMAIN%`` și ``%URL%``.

.. TODO: Documentați dacă șabloanele incluse pot include la rândul lor alte
   șabloane, cum sunt gestionate variabilele sau șabloanele lipsă și dacă
   este împiedicată includerea recursivă.


Șabloane predefinite
--------------------

Șabloanele documentate referitoare la utilizatori sunt:

``welcome_to``
   Îi urează bun venit unui utilizator în proiect.

``change_email_address``
   Trimite o legătură de confirmare pentru modificarea adresei de e-mail a
   unui utilizator.

``dropmyaccount``
   Confirmă o solicitare de ștergere a unui cont.

``create_new_project``
   Confirmă crearea unui proiect.

``invitation``
   Trimite o invitație de alăturare la un proiect.

``invitation_accomplished``
   Raportează că o invitație a fost acceptată.

``invitation_request``
   Notifică administratorii cu privire la o solicitare de invitație.

``lostpw``
   Asigură recuperarea parolei.

Șabloanele de uz general documentate sunt:

``new_gitlab_issue``
   Conține o copie a unui raport de eroare trimis.

``new_shared_polygon``
   Anunță un poligon partajat recent.

``new_upload_news``
   Anunță o încărcare nouă în știrile proiectului.

``new_upload_report``
   Notifică administratorii cu privire la o încărcare nouă.

``footer``
   Furnizează un subsol general pentru mesaje.

``interconnect_request``
   Asigură procesarea unei solicitări de interconectare.

Șabloanele documentate pentru notificările de evaluare sunt:

``data_evaluation_commenters``
   Notifică persoanele care au comentat anterior atunci când o înregistrare
   primește un comentariu nou.

``data_evaluation_owner``
   Notifică proprietarul atunci când o înregistrare încărcată de acesta
   primește un comentariu.

``upload_evaluation_commenters``
   Notifică persoanele care au comentat anterior atunci când o încărcare
   primește un comentariu nou.

``upload_evaluation_owner``
   Notifică proprietarul atunci când încărcarea sa primește un comentariu.

``user_evaluation_commenters``
   Notifică persoanele care au comentat anterior atunci când un utilizator
   primește un comentariu nou.

``user_evaluation_owner``
   Notifică un utilizator atunci când acesta primește un comentariu.

Șabloanele documentate referitoare la module sunt:

``dlr_new_request``
   Notifică administratorii proiectului cu privire la o nouă solicitare de
   descărcare. Variabilele documentate sunt ``username``, ``requestid`` și
   ``request_message``.

``dlr_request_registered``
   Confirmă unui utilizator că solicitarea sa de descărcare a fost
   înregistrată.

``incomplete_list_processed``
   Raportează că o listă incompletă a fost procesată.

``incomplete_list_unprocessed``
   Raportează că o listă incompletă nu a putut fi procesată.

.. TODO: Verificați dacă toți identificatorii șabloanelor sunt actuali și
   adăugați variabilele disponibile pentru fiecare șablon. Scopurile
   ``interconnect_request``, ``incomplete_list_processed`` și
   ``incomplete_list_unprocessed`` necesită explicații suplimentare.

.. TODO: Clarificați dacă ``dropmyaccount`` șterge un cont de la nivelul
   întregului server sau numai apartenența la proiect și dacă
   ``create_new_project`` este o solicitare de confirmare sau o notificare
   trimisă după creare.


.. _server-info:

Informații despre server
========================

Secțiunea **Informații despre server** afișează anumite informații despre
serverul OpenBioMaps și resursele utilizate de proiect. În funcție de
configurația serverului, aceasta poate include:

* versiunea instalată a aplicației OpenBioMaps;
* spațiul pe disc utilizat de fișierele, atașamentele și încărcările
  proiectului;
* mediile de încărcare din ultimele 1, 5 și 15 minute;
* încărcarea serverului normalizată în funcție de numărul de nuclee CPU;
* memoria disponibilă; și
* o legătură către interfața de administrare Supervisor.

Aceste valori îi pot ajuta pe administratori să identifice limitările
resurselor și să furnizeze informații de diagnosticare operatorilor
serverului. Accesul la informații detaliate despre server trebuie
restricționat, deoarece detaliile privind versiunea și infrastructura pot fi
sensibile din punct de vedere al securității.

.. TODO: Confirmați valorile disponibile administratorilor de proiect și pe
   cele care necesită privilegii la nivel de server. Documentați unitățile,
   intervalul de actualizare, sursa datelor, pragurile de avertizare și
   interpretarea fiecărei valori.

.. TODO: Clarificați dacă legătura Supervisor este disponibilă întotdeauna,
   la ce produs Supervisor se referă și cum este autentificat accesul la
   interfața externă respectivă.


.. _server-logs:

Jurnalele serverului
====================

Secțiunea **Jurnalele serverului** oferă acces la jurnalele puse la
dispoziție de configurația serverului. Sursele documentate includ:

* jurnale ale aplicației sau ale sistemului;
* jurnale MapServer;
* evenimente ale activităților de fundal; și
* erori ale activităților de fundal.

Interfața poate permite filtrarea și căutarea. Jurnalele pot conține nume de
utilizatori, identificatori de înregistrări, detalii ale interogărilor, căi
de fișiere, parametri ai solicitărilor sau alte informații sensibile.
Accesul și păstrarea trebuie să respecte politicile de securitate și
confidențialitate ale serverului.

.. TODO: Confirmați sursele de jurnal disponibile și dacă sunt acceptate în
   prezent actualizările în timp real. Documentați locația, formatul, fusul
   orar, rotația, păstrarea și dimensiunea maximă a rezultatelor pentru
   fiecare jurnal.

.. TODO: Explicați ce date personale sau confidențiale pot apărea în jurnale
   și cum pot administratorii să descarce, anonimizeze sau șteargă
   conținutul jurnalelor. De asemenea, trebuie precizat dacă vizualizarea
   jurnalelor este la rândul său auditată.


.. _background-job-settings:

Setări pentru activitățile de fundal
====================================

Activitățile de fundal permit unui proiect să execute sarcini programate sau
inițiate manual fără interacțiune continuă cu utilizatorul. Acestea pot fi
utilizate pentru operații precum:

* întreținerea datelor privind denumirile speciilor;
* validarea înregistrărilor;
* importarea sau exportarea datelor;
* curățarea tabelelor temporare;
* executarea analizelor; și
* reîmprospătarea vizualizărilor materializate.

O activitate de fundal este un program autonom. Activitățile OpenBioMaps
sunt scrise de obicei în PHP, dar serverul poate accepta și programe scrise
în Python, R, Bash sau alt limbaj instalat.

Interfața de administrare poate fi utilizată pentru:

* instalarea activităților predefinite dintr-un depozit Git central;
* încărcarea unei activități specifice proiectului;
* examinarea activităților instalate;
* configurarea parametrilor și programărilor activităților;
* activarea sau dezactivarea activităților;
* pornirea manuală a unei activități;
* inspectarea rezultatelor recente și a stării execuției; și
* editarea codului sursă al activității acolo unde această funcție este
  activată.

Jurnalele detaliate sunt disponibile prin secțiunea **Jurnalele
serverului**.

Editarea sau încărcarea unei activități este echivalentă cu instalarea de
cod executabil pe server. Aceste funcții trebuie limitate la administratori
de încredere, iar activitățile personalizate trebuie verificate pentru
injectarea comenzilor, acces nesigur la fișiere, expunerea datelor de
autentificare și utilizarea excesivă a resurselor.

.. TODO: Documentați structura necesară a pachetului, manifestul, punctul de
   intrare, limbajele acceptate, utilizatorul de execuție, directorul de
   lucru, variabilele de mediu, dependențele, limita de timp și limitele de
   resurse ale unei activități.

.. TODO: Explicați cum sunt autentificate, versionate, actualizate și
   verificate activitățile din depozitul central. Clarificați dacă
   modificările locale sunt suprascrise de o actualizare și cum poate fi
   restaurată o versiune anterioară.


Pentru mai multe informații, consultați :doc:`Activități <../jobs>`.

Programarea activităților
-------------------------

Mai întâi trebuie configurat planificatorul de la nivelul sistemului al
serverului. Într-o instalare Docker, acesta este de obicei un proces cron pe
gazdă. Acesta invocă periodic planificatorul proiectului, care pornește
activitățile ajunse la termen.

Înainte de a programa o activitate instalată sau modificată recent:

#. verificați configurația și sursa acesteia;
#. utilizați **Run** pentru a o executa manual;
#. așteptați finalizarea execuției;
#. inspectați rezultatul și jurnalele acesteia; și
#. configurați programarea recurentă numai după reușita testului.

Planificatorul proiectului utilizează câmpuri de tip cron pentru minute, ore
și zile. Un asterisc înseamnă fiecare valoare validă din câmpul
corespunzător.

.. TODO: Documentați toate câmpurile planificatorului și sintaxa cron
   acceptată de acestea, inclusiv intervalele, listele, pașii, luna, ziua
   săptămânii și fusul orar. Clarificați dacă este împiedicată suprapunerea
   execuțiilor aceleiași activități.


Exemplu Docker la nivel de sistem
---------------------------------

Următorul exemplu invocă planificatorul unui proiect de pe gazdă:

.. code-block:: console

   */5 * * * * /usr/local/bin/docker-compose -f /srv/docker/openbiomaps/docker-compose.yml exec -u www-data -T app php /var/www/html/biomaps/root-site/projects/myproject/jobs.php

Înlocuiți fișierul Compose, serviciul, calea proiectului și utilizatorul de
execuție cu valori corespunzătoare instalării.

.. TODO: Verificați această comandă în raport cu instalarea Docker acceptată
   în prezent. Instalările mai noi pot utiliza ``docker compose`` în loc de
   ``docker-compose``.

.. TODO: Precizați intervalul de invocare recomandat și explicați dacă
   executarea acestei comenzi la fiecare cinci minute împiedică activitățile
   programate la intervale de un minut să ruleze la momentul preconizat.
   Includeți recomandări privind jurnalizarea și notificarea erorilor pentru
   sarcina cron de la nivelul gazdei.


.. _project-description:

Descrierea proiectului
======================

Secțiunea **Descrierea proiectului** definește numele proiectului afișat în
antetul paginii și descrierea detaliată a proiectului. Pot fi furnizate
valori separate pentru fiecare limbă activă.

Descrierile scurtă și detaliată pot fi utilizate și în metadatele
proiectului, șabloanele de mesaje și paginile de sinteză. Prin urmare,
acestea trebuie să identifice clar proiectul și să furnizeze informații de
contact sau contextuale actuale, după caz.

.. TODO: Documentați formatarea acceptată, lungimile maxime, limba de rezervă
   și fiecare interfață în care apar descrierile scurtă și detaliată.
   Clarificați dacă aceste valori corespund exact variabilelor
   ``%PROJECT_TITLE%`` și ``%PROJECT_DESCRIPTION%`` din șabloanele de
   mesaje.


.. _data-management-page:

Gestionarea datelor
===================

Secțiunea **Gestionarea datelor** oferă sinteze ale încărcărilor și listelor
de observații. Aceasta îi poate ajuta pe administratori să examineze
trimiterile recente, să identifice colaboratorii și să navigheze între
înregistrările, încărcările și traseele GPS asociate.

Funcțiile documentate includ:

* enumerarea listelor de observații după utilizatorul care le-a încărcat,
  dată sau traseu GPS;
* sintetizarea numărului de înregistrări încărcate de fiecare utilizator și
  în fiecare tabel;
* afișarea listelor de observații trimise în ultimele 90 de zile; și
* afișarea traseelor GPS trimise în ultimele 30 de zile.

Tabelele interactive oferă filtrare și sortare acolo unde sunt acceptate.

.. TODO: Definiți o ``listă de observații`` și explicați relația acesteia cu
   o încărcare, înregistrările individuale și un traseu GPS. Documentați
   legăturile și acțiunile disponibile în fiecare sinteză.

.. TODO: Confirmați dacă intervalele de 90 și 30 de zile sunt fixe,
   configurabile sau doar valori implicite. Explicați ce fus orar și ce
   marcaj temporal sunt utilizate pentru selectarea activității recente.

.. TODO: Clarificați dacă sintezele includ încărcările șterse, respinse sau
   finalizate parțial și modul în care restricțiile de acces la nivel de
   rând afectează valorile afișate unui administrator.
