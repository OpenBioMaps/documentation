.. _data-policy:

Politica privind datele
***********************

Un proiect OpenBioMaps trebuie să aibă o politică documentată privind datele,
care să descrie modul în care datele sunt colectate, gestionate, revizuite,
accesate, partajate, păstrate și, în cele din urmă, arhivate sau șterse.
Politica îi ajută pe contribuitori, administratorii de proiect, utilizatorii
datelor și partenerii externi să înțeleagă la ce se pot aștepta din partea
proiectului și ce responsabilități au.

Această pagină oferă un cadru pentru pregătirea unei politici privind datele,
specifice unui proiect. Ea nu reprezintă în sine o politică completă și nu
constituie consultanță juridică. Regulile adecvate depind de scopul
proiectului, organizațiile implicate, categoriile de date prelucrate,
operatorul serverului și legislația aplicabilă.

Setările tehnice de acces ale unui proiect OpenBioMaps trebuie să pună în
aplicare politica publicată, dar nu o înlocuiesc. În mod similar, o politică
nu trebuie să promită restricții, perioade de păstrare, copii de siguranță sau
servicii care nu sunt implementate efectiv și verificate periodic.

Pentru informații despre configurarea permisiunilor tehnice, consultați
:doc:`Accesul la date <../data_access>`.


Relația cu alte documente
=========================

O politică privind datele proiectului poate fi însoțită de mai multe
documente conexe. Domeniul de aplicare al acestora trebuie delimitat clar.

``Politica privind datele``
   Descrie guvernanța și ciclul de viață al datelor proiectului, inclusiv
   colectarea, controlul calității, accesul, reutilizarea, păstrarea și
   responsabilitățile.

``Nota de informare privind confidențialitatea``
   Explică modul în care sunt prelucrate datele cu caracter personal,
   identifică operatorul sau operatorii relevanți și informează persoanele
   vizate cu privire la drepturile lor.

``Termenii și condițiile``
   Definesc regulile contractuale pentru utilizarea serverului, proiectului,
   aplicației sau serviciilor conexe.

``Nota de informare privind modulele cookie``
   Descrie modulele cookie sau tehnologiile similare utilizate de aplicația
   web în browser.

``Licența sau acordul de utilizare a datelor``
   Definește ce pot face destinatarii cu datele și condițiile asociate
   accesului sau reutilizării.

``Acordul contribuitorului``
   Definește ce este autorizat să trimită un contribuitor și ce permisiuni
   acordă acesta proiectului.

Un singur document poate acoperi mai multe dintre aceste subiecte, dar
domeniul de aplicare al fiecărei reguli trebuie să fie clar. Termenii valabili
la nivelul întregului server nu definesc automat politica de guvernanță a
fiecărui proiect găzduit pe serverul respectiv.

Serviciul public OpenBioMaps oferă exemple de
`termeni și condiții <https://openbiomaps.org/terms/>`_,
o `notă de informare privind confidențialitatea <https://openbiomaps.org/privacy/>`_
și o `notă de informare privind modulele cookie
<https://openbiomaps.org/cookies/>`_. Aceste documente sunt exemple pentru un
anumit serviciu și nu trebuie copiate pentru alt server sau proiect fără
verificarea organizațiilor, operațiunilor de prelucrare, jurisdicției,
datelor și informațiilor de contact.

.. TODO: Identificați termenii, nota de informare privind confidențialitatea
   și nota de informare privind modulele cookie valabile la nivelul
   serverului pentru proiectele găzduite pe fiecare server OpenBioMaps.
   Explicați care prevederi sunt moștenite de un proiect și care trebuie
   definite de operatorul proiectului.

.. TODO: Stabiliți dacă OpenBioMaps poate stoca sau afișa o politică privind
   datele, o notă de informare privind confidențialitatea, termeni și o
   licență specifice proiectului prin interfața de administrare. Documentați
   câmpurile de configurare, șabloanele și ordinea de rezervă aplicabile.


Pregătirea unei politici privind datele proiectului
===================================================

O politică privind datele trebuie pregătită înainte de începerea colectării
obișnuite a datelor. Aceasta trebuie revizuită ori de câte ori se modifică
scopul proiectului, structura bazei de date, modelul de acces, organizațiile
participante, integrările externe sau cerințele juridice.

Politica trebuie redactată într-un limbaj pe care utilizatorii cărora li se
adresează îl pot înțelege. Dacă un proiect funcționează în mai multe limbi,
politica trebuie să precizeze care versiune este autoritară și cum sunt
întreținute traducerile.

Politica trebuie să răspundă cel puțin la următoarele întrebări:

* Care este scopul proiectului?
* Ce date colectează?
* Cine operează proiectul și cine poate fi contactat?
* Cine este autorizat să trimită, să vizualizeze, să modifice, să valideze,
  să exporte sau să publice date?
* Cum este evaluată și documentată calitatea datelor?
* Ce înregistrări sau câmpuri sunt sensibile?
* În ce condiții pot fi reutilizate datele?
* Cum trebuie citați proiectul și contribuitorii săi?
* Cât timp sunt păstrate datele, fișierele atașate, jurnalele și copiile de
  siguranță?
* Cum pot fi raportate erorile, problemele legate de drepturi, incidentele de
  securitate sau solicitările de eliminare?
* Cum și când poate fi modificată politica?

.. TODO: Decideți dacă proiectelor trebuie să li se ofere un șablon standard
   de politică, o listă de verificare sau ambele. Dacă este introdus un
   șablon standard, identificați clauzele obligatorii și cele opționale.


Domeniu de aplicare și scop
===========================

Politica trebuie să înceapă prin identificarea proiectului și definirea
scopului său. Acest lucru ajută la stabilirea datelor relevante și împiedică
utilizarea fără informare a datelor colectate într-un anumit scop pentru un
scop incompatibil.

Domeniul de aplicare trebuie să includă:

* denumirea publică și identificatorul bazei de date a proiectului;
* scopul științific, de conservare, educațional sau operațional;
* domeniul geografic, taxonomic și temporal;
* tabelele de date și principalele categorii de date acoperite;
* interfețele web, mobile, API și pentru clienți externi acoperite;
* orice baze de date sau servicii conexe;
* utilizatorii și beneficiarii vizați; și
* activitățile care se află în mod explicit în afara domeniului de aplicare
  al proiectului.

Dacă proiectul are medii experimentale, de testare și de producție, politica
trebuie să clarifice care medii conțin date reale și ce reguli se aplică
fiecăruia.

.. TODO: Definiți terminologia OpenBioMaps actuală pentru un proiect
   experimental, de testare, stabil, arhivat și întrerupt. Confirmați dacă
   acestea sunt stări formale ale proiectului implementate de aplicație sau
   doar concepte de guvernanță.

.. TODO: Adăugați un scurt exemplu de declarație privind domeniul de aplicare
   pentru un proiect privind aparițiile biodiversității și altul pentru un
   proiect de monitorizare bazat pe evenimente de observare repetate.


Definiții
=========

Termenii utilizați în politică trebuie definiți în mod consecvent. În funcție
de proiect, pot fi utile următoarele definiții:

``Proiect``
   Baza de date OpenBioMaps, interfețele sale configurate și fluxul de
   gestionare a datelor asociat.

``Operatorul serverului``
   Organizația responsabilă cu operarea serverului OpenBioMaps și a
   infrastructurii sale de bază.

``Operatorul proiectului``
   Persoana sau organizația responsabilă cu guvernanța unui anumit proiect.

``Contribuitor``
   O persoană sau organizație care trimite date proiectului.

``Proprietarul datelor`` sau ``titularul drepturilor``
   Persoana sau organizația care deține anumite drepturi asupra datelor
   trimise. Semnificația exactă trebuie definită, nu presupusă.

``Responsabilul cu administrarea datelor``
   O persoană responsabilă cu întreținerea datelor și metadatelor în
   conformitate cu politica proiectului.

``Validator`` sau ``custode``
   O persoană autorizată să revizuiască, să adnoteze, să accepte, să
   corecteze sau să respingă datele trimise.

``Utilizatorul datelor``
   O persoană sau aplicație care vizualizează, interoghează, descarcă sau
   prelucrează în alt mod datele proiectului.

``Înregistrare``
   Un rând sau un set de rânduri conectate logic care reprezintă o
   observație, un eveniment, un taxon, o locație, un eșantion sau o altă
   entitate a proiectului.

``Fișier atașat``
   Un fișier asociat unei înregistrări, precum o fotografie, o înregistrare
   audio, un document sau un fișier de date.

``Metadate``
   Informații care descriu proiectul, tabelele și coloanele sale, un set de
   date, o încărcare sau o înregistrare individuală.

``Date cu caracter personal``
   Informații referitoare la o persoană identificată sau identificabilă,
   conform definiției din legislația aplicabilă operațiunii de prelucrare
   relevante.

``Date sensibile privind biodiversitatea``
   Date a căror divulgare ar putea crea un risc pentru o specie, un habitat,
   o zonă protejată, un proprietar de teren, un contribuitor, o activitate de
   cercetare sau o acțiune de conservare.

Definițiile nu trebuie să sugereze că un proiect a dobândit dreptul de
proprietate asupra datelor doar pentru că le stochează. Drepturile de autor,
drepturile asupra bazelor de date, obligațiile de confidențialitate,
contractele de muncă și alte drepturi se pot aplica diferit în jurisdicții
diferite.

.. TODO: Armonizați termenii ``project owner``, ``project founder``,
   ``project host``, ``operator``, ``administrator``, ``data owner`` și
   ``uploader`` în întreaga documentație și interfață OpenBioMaps.

.. TODO: Obțineți o analiză juridică a termenilor ``data owner`` și
   ``ownership of data``. După caz, înlocuiți-i cu noțiuni mai precise,
   precum titular al drepturilor, contribuitor, custode, operator sau sursă.


Guvernanță și responsabilități
==============================

Un proiect poate implica mai multe organizații și niveluri administrative.
Responsabilitățile trebuie atribuite explicit, nu deduse din permisiunile
tehnice.

Politica trebuie să identifice responsabilitatea pentru:

* operarea și securizarea serverului;
* guvernanța proiectului;
* definirea structurii bazei de date și a metadatelor;
* aprobarea contribuitorilor și a apartenenței la grupuri;
* crearea și întreținerea formularelor de încărcare;
* revizuirea regulilor de acces la date;
* validarea și corectarea înregistrărilor;
* răspunsul la solicitările persoanelor vizate și ale titularilor de
  drepturi;
* examinarea solicitărilor de export sau acces la date;
* întreținerea licențelor și a informațiilor de atribuire;
* copiile de siguranță, restaurarea și recuperarea în caz de dezastru;
* răspunsul la incidente;
* păstrarea sau ștergerea datelor;
* întreținerea integrărilor externe; și
* revizuirea și publicarea modificărilor politicii.

Accesul administrativ trebuie să respecte principiul privilegiului minim. De
exemplu, responsabilii cu gestionarea utilizatorilor nu trebuie să primească
automat permisiunea de a executa SQL, de a edita activități în fundal sau de
a exporta toate fișierele atașate.

Pentru o prezentare generală a funcțiilor administrative care pot fi
atribuite, consultați
:doc:`Setări administrative <../admin_settings>`.

.. TODO: Creați o matrice a responsabilităților care să includă operatorul
   serverului, fondatorul proiectului, operatorul proiectului,
   administratorul, responsabilul cu administrarea datelor, custodele,
   contribuitorul și utilizatorul datelor.

.. TODO: Documentați acțiunile administrative înregistrate într-un jurnal de
   audit și durata de păstrare a informațiilor de audit.

.. TODO: Definiți o procedură pentru transferarea responsabilității atunci
   când un fondator sau operator de proiect părăsește organizația
   participantă.


Colectarea datelor
==================

Politica trebuie să descrie ce date pot fi trimise, de către cine și prin ce
interfețe. Proiectele OpenBioMaps pot accepta date prin formulare web,
încărcări de fișiere, aplicații mobile, API, conexiuni directe la baza de date
sau importuri automatizate.

Pentru fiecare flux de colectare, documentați:

* scopul colectării;
* sursa de date preconizată;
* câmpurile obligatorii și opționale;
* tipurile de fișiere și fișiere atașate permise;
* regulile de validare aplicabile;
* atribuirea și proveniența necesare;
* autoritatea juridică sau organizațională necesară pentru trimiterea datelor;
* dacă este permisă trimiterea anonimă sau fără autentificare;
* clasificarea inițială de acces a înregistrărilor noi; și
* ce se întâmplă atunci când o trimitere este incompletă sau respinsă.

Contribuitorii trebuie să trimită numai date pe care sunt autorizați să le
furnizeze. Aceasta include verificarea drepturilor și obligațiilor de
confidențialitate asociate fotografiilor, înregistrărilor audio, rapoartelor,
datelor copiate din altă bază de date și informațiilor despre persoane
identificabile.

Formularele de încărcare sunt descrise în :doc:`Gestionarea formularelor de
încărcare <../upload_forms>`.

.. TODO: Documentați dacă OpenBioMaps poate solicita contribuitorilor să
   accepte un acord specific proiectului înainte de trimitere și dacă
   versiunea acordului acceptat este înregistrată împreună cu încărcarea.

.. TODO: Definiți comportamentul și regulile privind proprietatea sau
   custodia datelor trimise fără autentificare. Confirmați dacă încărcările
   anonime sunt acceptate de toate interfețele actuale.

.. TODO: Adăugați îndrumări pentru importarea datelor din servicii externe,
   precum GBIF sau iNaturalist, inclusiv proveniența, compatibilitatea
   licențelor, detectarea duplicatelor și actualizările ulterioare.


Metadate și proveniență
=======================

Datele trebuie să fie însoțite de suficiente metadate pentru ca semnificația,
sursa, calitatea și utilizarea permisă a acestora să fie inteligibile.

Metadatele la nivel de proiect trebuie să includă în mod normal:

* titlul și descrierea proiectului;
* organizațiile și persoanele de contact responsabile;
* acoperirea geografică, temporală și taxonomică;
* metodele de colectare a datelor;
* procesele de control al calității;
* condițiile de acces și reutilizare;
* licențele;
* citările preferate; și
* frecvența actualizărilor.

Metadatele la nivel de tabel și coloană trebuie să explice semnificația,
unitățile, valorile permise, sistemele de referință ale coordonatelor,
convențiile taxonomice, reprezentarea valorilor lipsă și orice transformări
aplicate datelor.

Proveniența la nivel de înregistrare sau încărcare poate include:

* contribuitorul sau organizația-sursă;
* colectorul sau observatorul;
* identificatorul înregistrării originale;
* datele trimiterii și observării;
* formularul de încărcare sau procesul de import utilizat;
* setul de date sursă și versiunea acestuia;
* transformările efectuate în timpul importului;
* starea validării; și
* legături către înregistrările derivate sau înlocuite.

Descrierile introduse pentru tabelele și coloanele bazei de date fac parte
din metadatele proiectului. Consultați :ref:`Tabelele și coloanele bazei de
date <database-columns>`.

.. TODO: Definiți metadatele minime necesare pentru ca un proiect OpenBioMaps
   să fie considerat pregătit pentru producție sau publicare.

.. TODO: Mapați metadatele OpenBioMaps la nivel de proiect, tabel, coloană,
   încărcare și înregistrare la standarde relevante, precum Darwin Core,
   Ecological Metadata Language, DataCite și ISO 19115, după caz.

.. TODO: Documentați informațiile de proveniență pe care OpenBioMaps le
   înregistrează automat și câmpurile care trebuie adăugate la schema
   proiectului.


Calitatea și validarea datelor
==============================

Politica trebuie să explice că stocarea unei înregistrări nu confirmă în mod
necesar corectitudinea acesteia. Trebuie să definească stările de validare
disponibile și cine le poate atribui sau modifica.

Controalele de calitate pot include:

* validarea câmpurilor obligatorii și a tipurilor de date;
* liste controlate și verificarea intervalelor;
* validarea numelor taxonomice;
* verificarea consecvenței datelor și coordonatelor;
* detectarea duplicatelor;
* verificarea sistemelor de referință ale coordonatelor;
* revizuirea fișierelor atașate sau a dovezilor justificative;
* identificarea de către experți;
* verificări spațiale sau temporale automatizate;
* compararea cu date de referință externe; și
* comentarii ale contribuitorilor sau evaluatorilor.

Corecțiile trebuie să păstreze proveniența relevantă. Acolo unde este
posibil, proiectul trebuie să diferențieze valoarea trimisă inițial de o
normalizare, interpretare sau corecție ulterioară.

Datele publicate trebuie să fie însoțite de precizările corespunzătoare.
Absența unui avertisment sau indicator de validare nu trebuie prezentată ca o
garanție a exactității, integralității, adecvării pentru un anumit scop sau a
interpretării taxonomice actuale.

.. TODO: Documentați modelul de evaluare a datelor implementat de
   OpenBioMaps, inclusiv evaluările înregistrărilor, încărcărilor și
   utilizatorilor și semnificația exactă a oricăror scoruri numerice sau
   stări de validare.

.. TODO: Explicați dacă istoricul înregistrărilor stochează valorile
   anterioare și noi, identitățile editorilor, marcajele temporale și
   motivele modificărilor. Definiți cine poate inspecta și restaura valorile
   istorice.

.. TODO: Adăugați un flux recomandat pentru corecții, care să acopere
   erorile raportate, revizuirea de către custode, consultarea
   contribuitorului, corectarea, respingerea, retragerea și notificarea
   destinatarilor anteriori ai datelor.


Acces și divulgare
==================

Politica trebuie să precizeze ce date sunt publice, restricționate la
utilizatorii autentificați, restricționate la grupuri, disponibile numai după
aprobare sau accesibile numai administratorilor de proiect.

OpenBioMaps poate combina:

* setări de acces la nivel de proiect;
* reguli de acces la nivel de rând;
* restricții la nivel de coloană;
* apartenența la grupuri;
* roluri administrative; și
* fluxuri de autorizare a exporturilor.

Configurația tehnică efectivă trebuie testată utilizând conturi
reprezentative pentru fiecare grup relevant de utilizatori și, acolo unde
este activat accesul public, fără autentificare.

Pentru detalii privind controalele disponibile, consultați
:doc:`Accesul la date <../data_access>`.

Politica trebuie să diferențieze următoarele acțiuni:

* aflarea existenței unei înregistrări;
* vizualizarea unei înregistrări pe hartă;
* vizualizarea atributelor sale;
* vizualizarea geometriei sale exacte;
* interogarea și filtrarea acesteia;
* descărcarea acesteia;
* vizualizarea sau descărcarea fișierelor atașate;
* modificarea sau ștergerea acesteia;
* obținerea acesteia prin API;
* accesarea acesteia prin SQL sau o aplicație externă; și
* primirea acesteia printr-o solicitare de date aprobată.

Aceste acțiuni pot expune cantități diferite de informații și nu trebuie să
aibă în mod obligatoriu aceleași permisiuni.

.. TODO: Documentați algoritmul exact OpenBioMaps pentru soluționarea
   permisiunilor și utilizați-l pentru a crea exemple de politică testate
   pentru date publice, autentificate, restricționate la grup, accesibile
   numai proprietarului și restricționate la nivel de coloană.

.. TODO: Confirmați modul în care previzualizările și exporturile fișierelor
   atașate, rezultatele API, straturile hărții, fișierele stocate în memoria
   cache și conexiunile SQL directe aplică regulile de acces la nivel de rând
   și coloană.

.. TODO: Definiți o procedură periodică de revizuire a accesului, care să
   acopere apartenența la grupuri, permisiunile administrative,
   acreditările API, conturile directe ale bazei de date și linkurile de
   descărcare generate.


Date sensibile privind biodiversitatea
======================================

Locațiile exacte, metodele de colectare, identitățile observatorilor sau alte
atribute pot crea riscuri pentru speciile amenințate, habitate, proprietarii
de terenuri, contribuitori și activitățile de conservare. Un proiect trebuie
să definească modul în care sunt evaluate astfel de riscuri și ce măsuri de
protecție sunt aplicate.

Măsurile de protecție posibile includ:

* ascunderea câmpurilor selectate;
* restricționarea înregistrărilor complete la anumite grupuri;
* ascunderea geometriei exacte față de utilizatorii publici;
* publicarea coordonatelor generalizate;
* amânarea publicării;
* solicitarea aprobării individuale pentru exporturi;
* separarea fișierelor atașate publice de cele restricționate; și
* înregistrarea unui motiv și a unei date de revizuire pentru restricție.

Restricțiile trebuie să fie proporționale, documentate și revizuite. O
înregistrare nu trebuie să rămână restricționată pe termen nelimitat doar
pentru că starea sa nu a fost reevaluată niciodată.

Tabelul de reguli acceptă în anumite configurații de proiect valori asociate
sensibilității, precum ``sensitive``, ``restricted``, ``no-geom`` și
``only-owner``. Comportamentul exact al acestora trebuie verificat înainte de
a vă baza pe ele.

.. TODO: Confirmați lista completă și efectul exact al valorilor de
   sensibilitate acceptate în interfața web, pe hărți, în interogări,
   descărcări, API, fișiere atașate și operațiuni de scriere.

.. TODO: Documentați dacă OpenBioMaps acceptă generalizarea coordonatelor sau
   doar ascunde geometria. Dacă generalizarea este acceptată, descrieți
   algoritmul, precizia, consecvența și tratarea exporturilor derivate.

.. TODO: Elaborați o procedură de evaluare a sensibilității care să
   identifice cine poate clasifica o înregistrare, ce motive pot fi
   utilizate, cum sunt înregistrate deciziile și când trebuie revizuite
   restricțiile.

.. TODO: Adăugați exemple privind speciile amenințate, cuiburile active,
   terenurile private, locațiile arheologice sau peșterile, cercetările aflate
   sub embargo și siguranța contribuitorilor.


Date cu caracter personal și confidențialitate
==============================================

Datele privind biodiversitatea pot conține date cu caracter personal chiar
dacă proiectul nu este destinat în principal colectării informațiilor despre
persoane. Exemplele pot include:

* numele contribuitorilor, observatorilor, colectorilor, validatorilor și
  fotografilor;
* adrese de e-mail și informații din profilurile utilizatorilor;
* locații precise asociate locuinței sau deplasărilor unei persoane;
* jurnalele traseelor din aplicația mobilă;
* fotografii, înregistrări audio și note în text liber;
* adrese IP și jurnale ale aplicației;
* proprietatea asupra înregistrărilor și istoricul modificărilor; și
* comentarii sau evaluări asociate utilizatorilor.

Nota de informare privind confidențialitatea aplicabilă trebuie să identifice
operatorul sau operatorii relevanți, scopurile prelucrării, temeiurile
juridice, categoriile de date, destinatarii, perioadele de păstrare,
transferurile internaționale, măsurile de securitate, informațiile de contact
și drepturile persoanelor vizate, conform cerințelor legislației aplicabile.

Politica privind datele proiectului trebuie să facă trimitere la nota de
informare privind confidențialitatea aplicabilă, fără a încerca să o
înlocuiască. Declarațiile privind temeiurile juridice și drepturile legale
trebuie revizuite de o persoană calificată pentru jurisdicția relevantă.

Este necesară o atenție deosebită atunci când datele se referă la copii,
persoane vulnerabile, locuințe private, monitorizarea angajaților, urmărirea
continuă a locației sau categorii speciale de date cu caracter personal.

.. TODO: Stabiliți rolurile și responsabilitățile respective privind
   confidențialitatea ale operatorului serverului, operatorului proiectului,
   organizațiilor participante, contribuitorilor și furnizorilor externi de
   servicii pentru fiecare flux de prelucrare.

.. TODO: Actualizați și supuneți unei analize juridice nota de informare
   implicită privind confidențialitatea. Exemplul disponibil este datat 2022
   și este posibil să nu reflecte organizațiile, operațiunile de prelucrare,
   tehnologiile, perioadele de păstrare sau cerințele aplicabile actuale
   privind protecția datelor.

.. TODO: Inventariați toate datele cu caracter personal prelucrate de
   aplicația web actuală, aplicațiile mobile, API, serviciul de autentificare,
   jurnale, activități în fundal, copii de siguranță, serviciul de e-mail și
   integrările externe.

.. TODO: Documentați modul în care sunt primite, autentificate, atribuite,
   finalizate și înregistrate solicitările de acces, corectare,
   restricționare, portabilitate, opoziție și ștergere.

.. TODO: Clarificați modul în care ștergerea contului afectează
   înregistrările încărcate, atribuirea, istoricul, comentariile,
   evaluările, tokenurile API, sesiunile active, activitățile programate,
   jurnalele, copiile de siguranță și copiile deja exportate de alți
   utilizatori.


Drepturi, licențe și reutilizarea permisă
=========================================

Politica trebuie să precizeze ce drepturi trebuie să dețină contribuitorii
asupra datelor trimise și ce permisiuni acordă proiectului. De asemenea,
trebuie să precizeze licența sau celelalte condiții în care destinatarii pot
reutiliza datele.

Se pot aplica drepturi diferite pentru:

* observații individuale;
* baze de date compilate;
* fotografii și înregistrări audio;
* rapoarte și alte fișiere atașate;
* date taxonomice sau geografice de referință;
* dale și hărți de bază;
* metadate;
* software și definiții ale formularelor; și
* conținut importat dintr-o sursă externă.

Un proiect nu trebuie să descrie datele ca fiind deschise decât dacă
destinatarii au permisiunea clară de a le reutiliza. Vizibilitatea publică nu
reprezintă în sine o licență.

Atunci când se aplică mai multe licențe, exporturile trebuie să păstreze
suficiente informații pentru a stabili licența și atribuirea aplicabile
fiecărei înregistrări sau fiecărui fișier atașat. Licențele surselor
incompatibile nu trebuie combinate sub o licență nouă fără permisiune.

.. TODO: Definiți licențele acceptate sau recomandate de OpenBioMaps pentru
   date, metadate și materiale media. Explicați diferențele dintre accesul
   public, accesul restricționat, CC0, CC BY, CC BY-NC și acordurile
   personalizate de utilizare a datelor.

.. TODO: Documentați unde pot fi stocate informațiile privind licența la
   nivel de proiect, tabel, încărcare, înregistrare și fișier atașat și dacă
   acestea sunt incluse automat în exporturi și răspunsurile API.

.. TODO: Stabiliți o procedură pentru soluționarea revendicărilor aflate în
   conflict privind proprietatea, calitatea de autor, licența,
   confidențialitatea sau eliminarea.

.. TODO: Supuneți unei analize juridice orice regulă care transferă
   operatorului proiectului drepturile asupra datelor trimise anonim.
   Asigurați-vă că interfața cu utilizatorul prezintă termenii aplicabili
   înainte de trimitere.


Citare și atribuire
===================

Politica trebuie să ofere o citare preferată pentru proiect și să explice cum
trebuie menționați contribuitorii, organizațiile-sursă, seturile de date și
OpenBioMaps.

În mod normal, o citare trebuie să identifice:

* editorul datelor sau organizația responsabilă;
* titlul proiectului sau al setului de date;
* serverul sau depozitul OpenBioMaps;
* versiunea, data publicării sau data interogării;
* data accesării;
* un identificator persistent, acolo unde este disponibil; și
* licența aplicabilă.

Atunci când un set de date sau o interogare salvată are un DOI sau alt
identificator persistent, acesta trebuie preferat în locul unui URL care se
poate modifica.

Atribuirea la nivel de înregistrare trebuie păstrată atunci când este impusă
de licența sau acordul contribuitorului aplicabil. Utilizatorilor nu trebuie
să li se solicite să publice inutil informații personale de contact.

.. TODO: Definiți și implementați un format standard de citare, care poate fi
   citit automat, pentru proiectele OpenBioMaps, interogările salvate și
   exporturi.

.. TODO: Confirmați ce obiecte OpenBioMaps pot primi în prezent un DOI, cum
   sunt înghețate versiunile și ce modificări rămân posibile după publicare.

.. TODO: Adăugați exemple de citare testate pentru un proiect complet, o
   interogare filtrată, un rezultat API, un fișier atașat descărcat și date
   agregate de la mai mulți contribuitori.


Solicitări de date și exporturi
===============================

Unele proiecte le solicită utilizatorilor să ceară permisiunea înainte de a
descărca date restricționate. Politica trebuie să descrie:

* cine poate depune o solicitare;
* ce informații trebuie să furnizeze solicitantul;
* ce criterii sunt utilizate pentru luarea deciziei;
* cine ia decizia;
* termenele de răspuns preconizate;
* utilizările permise și interzise;
* măsurile de securitate necesare;
* dacă este permisă partajarea ulterioară;
* cerințele privind expirarea și ștergerea;
* cerințele privind raportarea și citarea; și
* procesul de contestație, modificare sau reînnoire.

Deciziile trebuie să fie consecvente și înregistrate. Fișierele exportate
trebuie să conțină numai înregistrările și câmpurile aprobate, iar linkurile
lor de descărcare trebuie protejate și trebuie să expire după o perioadă
adecvată.

.. TODO: Documentați modulul pentru solicitări de export sau descărcare,
   inclusiv fluxul său, rolurile, șabloanele de mesaje, înregistrările de
   audit, fișierele generate, verificările accesului, expirarea linkurilor și
   procedura de curățare.

.. TODO: Stabiliți dacă se pot stoca împreună cu o solicitare condițiile
   aprobării și dacă acestea pot fi prezentate solicitantului înainte de
   descărcare.

.. TODO: Definiți modul în care un proiect poate notifica destinatarii
   anteriori atunci când datele exportate sunt corectate, retrase,
   reclasificate sau se constată că prezintă un risc pentru conservare sau
   confidențialitate.


Partajare și integrări externe
==============================

Datele pot părăsi interfața web OpenBioMaps prin descărcări, API-uri,
conexiuni SQL directe, QGIS, R, clienți mobili, activități în fundal,
servicii de interconectare sau publicarea în depozite externe.

Politica trebuie să identifice destinatarii și integrările obișnuite ale
datelor, datele transmise acestora, scopul, controalele de acces aplicabile,
frecvența actualizărilor, licențele și procesul de ștergere sau corectare.

Publicarea automatizată nu trebuie să expună câmpuri care ar fi ascunse
aceluiași utilizator în interfața web. Acreditările utilizate de integrări
trebuie să primească numai permisiunile necesare și trebuie schimbate sau
revocate atunci când nu mai sunt necesare.

.. TODO: Inventariați interfețele externe acceptate și documentați dacă
   fiecare aplică în mod consecvent restricțiile la nivel de proiect, rând și
   coloană.

.. TODO: Definiți o procedură pentru aprobarea, documentarea, monitorizarea
   și dezactivarea transferurilor automatizate de date.

.. TODO: Explicați modul în care corecțiile și ștergerile sunt propagate
   către servicii externe precum GBIF, iNaturalist, straturi de hărți stocate
   în memoria cache sau baze de date replicate.


Păstrare, ștergere și arhivare
==============================

Politica trebuie să definească perioadele de păstrare sau criteriile de
revizuire pentru toate categoriile majore de informații, inclusiv:

* înregistrările proiectului activ;
* trimiterile respinse și retrase;
* istoricul înregistrărilor;
* adnotările taxonomice și de validare;
* conturile și profilurile utilizatorilor;
* invitațiile și apartenența la grupuri;
* încărcările întrerupte și fișierele temporare;
* fișierele atașate și miniaturile generate;
* comentariile, evaluările și mesajele;
* solicitările și deciziile privind accesul la date;
* exporturile și linkurile de descărcare generate;
* jurnalele aplicației și serverului;
* jurnalele activităților în fundal;
* tokenurile API și sesiunile;
* copiile de siguranță; și
* versiunile arhivate ale proiectului.

Ștergerea din baza de date activă nu elimină neapărat informațiile din
copiile de siguranță, exporturile externe, jurnale, memoria cache sau copiile
obținute anterior de utilizatori. Politica trebuie să explice cu exactitate
aceste limitări.

Atunci când reproductibilitatea științifică pe termen lung necesită
păstrarea, ștergerea poate fi înlocuită cu restricționarea,
pseudonimizarea, retragerea sau publicarea unei înregistrări de tip
tombstone. Astfel de decizii trebuie să se bazeze pe o evaluare juridică și
științifică documentată.

.. TODO: Creați un program de păstrare pentru instalarea OpenBioMaps
   implicită și identificați perioadele configurabile la nivel de server și
   proiect.

.. TODO: Documentați efectul exact al ștergerii unei înregistrări, încărcări,
   unui fișier atașat, cont de utilizator, grup, proiect și export generat.

.. TODO: Definiți un flux acceptat pentru închiderea proiectului, care să
   includă exportul final, publicarea metadatelor, transferul către un
   operator nou, arhivarea în mod doar în citire, ștergerea, notificarea
   utilizatorilor și eliminarea acreditărilor.


Copii de siguranță și restaurare
================================

O politică privind datele trebuie să diferențieze copiile de siguranță de
arhive.

O copie de siguranță este păstrată în principal pentru restaurarea unui
sistem după pierderea accidentală, coruperea sau o defecțiune tehnică. O
arhivă este păstrată pentru conservarea pe termen lung și interpretarea
continuă a datelor. O copie de siguranță nu înlocuiește o arhivă documentată,
iar executarea cu succes a unei activități de creare a copiilor de siguranță
nu dovedește că restaurarea va funcționa.

Politica trebuie să precizeze:

* ce obiecte și fișiere ale bazei de date sunt incluse în copiile de
  siguranță;
* dacă sunt incluse fișierele atașate;
* frecvența copiilor de siguranță;
* perioada de păstrare;
* locația stocării și jurisdicția geografică;
* criptarea și controalele de acces;
* responsabilitatea pentru monitorizarea reușitei copiilor de siguranță;
* prioritățile restaurării și intervalele de timp preconizate;
* frecvența testării restaurării; și
* ce se întâmplă cu datele șterse sau restricționate din copiile de siguranță
  păstrate.

Exemplele disponibile de termeni precizează că tabelele SQL ale proiectelor
de pe anumite servicii OpenBioMaps sunt incluse zilnic în copii de siguranță
și păstrate timp de două săptămâni, în timp ce fișierele atașate sunt
excluse. Acest lucru nu trebuie prezentat drept o garanție generală
OpenBioMaps fără verificarea serverului în cauză.

.. TODO: Confirmați și documentați separat configurațiile actuale ale
   copiilor de siguranță pentru fiecare tip de server OpenBioMaps acceptat,
   inclusiv instalările Docker și serverele operate independent.

.. TODO: Adăugați o procedură testată de creare și restaurare a copiilor de
   siguranță care să includă baza de date PostgreSQL, configurația
   proiectului, fișierele atașate încărcate, fișierele generate, șabloanele
   de mesaje, modulele, activitățile și configurația hărții.

.. TODO: Definiți obiectivele privind punctul și timpul de recuperare și
   stabiliți un program pentru testele de restaurare documentate.


Securitate și răspuns la incidente
==================================

Politica trebuie să rezume măsurile organizaționale și tehnice utilizate
pentru protejarea datelor, fără a publica informații care ar putea slăbi
securitatea.

Controalele relevante pot include:

* conexiuni de rețea criptate;
* autentificarea și gestionarea securizată a sesiunilor;
* accesul la grupuri și administrativ bazat pe privilegiul minim;
* acreditări protejate pentru baza de date și API;
* actualizări ale serverului și dependențelor;
* înregistrare în jurnale și monitorizare;
* protecția copiilor de siguranță;
* restricții privind activitățile în fundal executabile;
* controale privind tipurile de fișiere și fișierele atașate;
* revizuiri periodice ale accesului; și
* gestionarea vulnerabilităților și incidentelor.

O procedură documentată pentru incidente trebuie să definească modul în care
sunt raportate și gestionate suspiciunile de acces neautorizat, publicarea
accidentală, pierderea datelor, încărcările rău intenționate, acreditările
compromise sau regulile de acces incorecte.

.. TODO: Definiți responsabilitățile operatorului serverului și ale
   operatorului proiectului în materie de securitate, inclusiv aplicarea
   corecțiilor, monitorizarea, gestionarea acreditărilor, revizuirea accesului
   și comunicarea incidentelor.

.. TODO: Adăugați un proces de răspuns la incidente care să acopere
   detectarea, limitarea efectelor, păstrarea dovezilor, evaluarea riscurilor,
   corectarea, notificarea, recuperarea și revizuirea ulterioară incidentului.

.. TODO: Documentați modul în care administratorii de proiect pot raporta în
   siguranță o vulnerabilitate fără a o divulga printr-un canal public de
   raportare a erorilor.


Modificări ale politicii
========================

Politica trebuie să conțină un număr de versiune, data publicării, data
intrării în vigoare, editorul responsabil și istoricul modificărilor.
Modificările semnificative trebuie comunicate înainte de intrarea lor în
vigoare, acolo unde este necesar.

Proiectul trebuie să definească:

* cine poate aproba o modificare a politicii;
* cum sunt notificați utilizatorii afectați;
* dacă este necesară o nouă acceptare;
* cum este înregistrată acceptarea;
* cum rămân accesibile versiunile anterioare; și
* ce se întâmplă dacă un contribuitor sau utilizator respinge noii termeni.

Modificările setărilor tehnice de acces, licențelor, perioadelor de păstrare,
scopurilor sau organizațiilor responsabile trebuie să declanșeze o revizuire
a politicii.

.. TODO: Documentați dacă OpenBioMaps poate înregistra versiunea termenilor
   sau a politicii acceptate de fiecare utilizator și poate solicita o nouă
   acceptare după o modificare semnificativă.

.. TODO: Definiți un proces de versionare și publicare pentru documentele de
   politică valabile la nivelul serverului și specifice proiectului.


Structura recomandată a politicii proiectului
=============================================

O politică specifică proiectului poate utiliza următoarea structură:

#. **Informații despre document** — titlu, versiune, proprietar, data
   aprobării, data intrării în vigoare și data revizuirii.
#. **Identitatea și scopul proiectului** — numele proiectului, serverul,
   domeniul de aplicare și utilizarea prevăzută.
#. **Persoane de contact și responsabilități** — operatorul serverului,
   operatorul proiectului, responsabilul cu administrarea datelor și
   persoanele de contact pentru solicitări.
#. **Definiții** — terminologie specifică proiectului.
#. **Date colectate** — înregistrări, metadate, fișiere atașate, proveniență
   și date cu caracter personal.
#. **Reguli de trimitere** — contribuitori autorizați, surse acceptate și
   responsabilitățile contribuitorilor.
#. **Gestionarea calității** — validare, corectare, istoric și precizări.
#. **Clasificarea accesului** — date publice, autentificate, restricționate
   la grup, sensibile și aflate sub embargo.
#. **Drepturi și licențe** — permisiunile contribuitorilor și reutilizarea de
   către destinatari.
#. **Citare și atribuire** — citări preferate și identificatori persistenți.
#. **Solicitări și partajare externă** — exporturi, integrări și fluxuri de
   aprobare.
#. **Păstrare și arhivare** — păstrarea activă, ștergerea, copiile de
   siguranță și închiderea proiectului.
#. **Confidențialitate și securitate** — trimiteri la nota de informare
   privind confidențialitatea și procesul pentru incidente.
#. **Reclamații și solicitări** — persoane de contact și procedura de
   răspuns.
#. **Modificările politicii** — aprobare, notificare, acceptare și istoricul
   versiunilor.

.. TODO: Transformați această structură într-un șablon de politică ce poate
   fi descărcat separat, cu clauzele obligatorii și opționale marcate clar.

.. TODO: Adăugați exemple de text numai după verificarea fiecărui exemplu în
   raport cu funcționalitatea OpenBioMaps actuală și după revizuirea acestuia
   pentru jurisdicțiile în care urmează să fie utilizat.


Lista de verificare a implementării
===================================

Înainte de publicarea unei politici privind datele proiectului, operatorul
proiectului trebuie să verifice dacă:

* scopul și domeniul de aplicare al proiectului sunt corecte;
* organizațiile și persoanele de contact responsabile sunt actuale;
* rolurile tehnice corespund responsabilităților declarate;
* formularele de încărcare colectează numai datele prevăzute;
* metadatele și proveniența necesare sunt înregistrate;
* stările validării și declarațiile privind calitatea sunt inteligibile;
* accesul public, autentificat și de grup a fost testat;
* accesul prin hartă, interogare, API, export, fișiere atașate și SQL
  funcționează în mod consecvent;
* înregistrările și câmpurile sensibile beneficiază de protecția prevăzută;
* licențele și atribuirea sunt incluse în exporturi;
* prelucrarea datelor cu caracter personal corespunde notei de informare
  privind confidențialitatea;
* declarațiile privind păstrarea și ștergerea corespund comportamentului
  efectiv al sistemului;
* copiile de siguranță includ obiectele și fișierele bazei de date promise;
* a fost efectuat un test de restaurare;
* integrările externe sunt documentate;
* persoanele de contact pentru incidente și solicitări sunt monitorizate;
* versiunea în vigoare a politicii este disponibilă utilizatorilor; și
* a fost stabilită o dată pentru următoarea revizuire.

O politică trebuie testată în raport cu fluxurile reale, nu doar revizuită ca
text. În special, administratorii trebuie să utilizeze conturi reprezentative
pentru testarea operațiunilor de încărcare, interogare, hartă, descărcare,
API, fișiere atașate, corectare și ștergere.

.. TODO: Elaborați un raport de audit automatizat sau asistat pentru
   administratori, care să compare politica publicată a proiectului cu
   setările de acces, modulele activate, căile de export, setările de
   păstrare și integrările externe.


Întrebări deschise
==================

Mai multe aspecte trebuie confirmate în aplicația și modelul de guvernanță
OpenBioMaps înainte ca această pagină să poată fi considerată completă:

* relația exactă dintre operatorii serverelor și operatorii proiectelor;
* definițiile autoritare ale rolurilor proiectului și de gestionare a
  datelor;
* algoritmul complet de soluționare a accesului;
* stocarea și prezentarea licențelor și versiunilor politicii;
* domeniul de aplicare și păstrarea informațiilor de audit și istoric;
* tratarea datelor cu caracter personal incluse în înregistrările privind
  biodiversitatea;
* comportamentul exact al fiecărei interfețe la ștergere;
* acoperirea copiilor de siguranță și garanțiile privind restaurarea;
* propagarea corecțiilor și ștergerilor către sistemele externe; și
* ciclul de viață acceptat pentru închiderea sau transferarea unui proiect.

.. TODO: Soluționați aceste întrebări împreună cu responsabilii OpenBioMaps,
   operatorii serverelor, administratori de proiect reprezentativi și
   specialiștii juridici sau în guvernanța datelor corespunzători. Înlocuiți
   blocurile TODO soluționate cu documentație testată și specifică versiunii.
