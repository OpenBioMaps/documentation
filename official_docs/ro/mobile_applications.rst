:author: Miklós Bán
:date: 2026-08-10

Aplicații mobile
****************

Mai multe aplicații mobile acceptă funcționalități OpenBioMaps. Acestea includ
instrumente pentru preluarea și colectarea datelor în medii online și offline
și variază de la aplicații web progresive (PWA) până la aplicații mobile
native.

Aplicație offline pentru dispozitive Android și iOS
===================================================

.. TODO: Sunt necesare dezvoltări suplimentare:
   Trebuie precizate denumirea oficială a aplicației, precum și linkurile către Google Play și App Store.
   Ar fi utilă prezentarea prin capturi de ecran a selectării serverului și proiectului, a sincronizării și a gestionării evenimentelor de observare.
   Trebuie clarificat modul în care funcționează selectarea serverului și dacă poate fi adăugat un server OpenBioMaps personalizat.
   Trebuie documentată gestionarea erorilor de sincronizare și situațiile în care datele sincronizate pot fi șterse în siguranță de pe dispozitiv.
   Ar fi utilă descrierea detaliată a formatelor de backup și export, precum și a restaurării acestora.
   Ar trebui oferite recomandări bazate pe măsurători privind efectul filtrelor GPS de timp și distanță asupra consumului bateriei.
   Trebuie precizate versiunile Android și iOS acceptate de aplicație.
   Informațiile privind confidențialitatea și permisiunile — în special gestionarea datelor de localizare, a fișierelor atașate și a backupurilor pentru depanare — ar trebui rezumate și într-o secțiune separată.



Prezentare generală
-------------------

Aplicația mobilă offline este concepută pentru colectarea datelor pe teren.
Aceasta oferă o interfață flexibilă pentru activități de colectare a datelor
specifice proiectului și poate fi utilizată fără o conexiune continuă la
internet după descărcarea proiectelor și formularelor necesare.

OpenBioMaps nu oferă un singur formular sau o singură metodă predefinită
pentru colectarea datelor. Fiecare proiect își definește propriile formulare
și câmpuri de date. În consecință, următoarele depind de configurația
proiectului și de permisiunile utilizatorului curent:

* proiectele disponibile;
* formularele disponibile în cadrul proiectelor respective;
* câmpurile care apar în fiecare formular; și
* modul în care se comportă câmpurile respective.

Numai utilizatorii autentificați pot colecta date cu ajutorul aplicației.
Aplicația nu oferă o funcție generală de înregistrare, deși unele proiecte pot
accepta un proces simplu sau automat de înregistrare în afara aplicației.

Dezvoltare
----------

Aplicația este dezvoltată de Ecollab Ltd. utilizând React Native și Expo.

Noțiuni introductive
--------------------

Este necesară o conexiune la internet pentru selectarea unui server și a unui
proiect, autentificare și descărcarea formularelor. După descărcarea
formularelor necesare, acestea pot fi utilizate și offline.

Selectarea unui server
^^^^^^^^^^^^^^^^^^^^^^

Selectați serverul OpenBioMaps care găzduiește proiectul pe care doriți să îl
utilizați. Este necesară o conexiune la internet pentru conectarea la server
și preluarea informațiilor despre proiectele disponibile.

Selectarea unui proiect
^^^^^^^^^^^^^^^^^^^^^^^

Selectați un proiect dintre proiectele disponibile pe serverul ales.
Proiectele afișate depind de configurația serverului și de permisiunile
dumneavoastră de acces.

Este necesară o conexiune la internet la prima încărcare a unui proiect sau la
reîmprospătarea configurației acestuia.

Autentificarea
^^^^^^^^^^^^^^

Autentificați-vă utilizând adresa de e-mail și parola. Este necesară o
conexiune la internet pentru autentificare.

După autentificarea cu succes, pot fi accesate proiectele și formularele
disponibile pentru contul dumneavoastră. De asemenea, pot fi afișate proiecte
și formulare disponibile public.

Selectarea unui formular
^^^^^^^^^^^^^^^^^^^^^^^^

Selectați și deschideți un formular în timp ce sunteți online pentru a
descărca informațiile necesare utilizării offline. După încărcarea cu succes
a formularului, acesta rămâne disponibil offline până când datele sale locale
sunt eliminate sau formularul trebuie actualizat.

Fixarea unui formular pe ecranul principal
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Formularele utilizate frecvent pot fi fixate pe ecranul principal pentru
acces mai rapid. Atingeți pictograma pioneză de lângă numele unui formular
pentru a-l fixa sau desprinde.

Structura aplicației
--------------------

Ecranul principal
^^^^^^^^^^^^^^^^^

Ecranul principal oferă acces la:

* hartă;
* formulare;
* datele colectate;
* setări;
* jurnalele traseelor; și
* instrumente.

Formularele fixate sunt afișate pe ecranul principal pentru acces rapid. Dacă
un eveniment de observare este în curs, starea acestuia este afișată pe
butonul formularului fixat corespunzător.

Ecranul hărții
^^^^^^^^^^^^^^

Ecranul hărții este utilizat pentru vizualizarea observațiilor înregistrate
și a locațiilor permanente de eșantionare.

Informațiile afișate pe hartă depind de proiectul selectat, de datele
descărcate și de configurația proiectului.

Ecranul formularelor
^^^^^^^^^^^^^^^^^^^^

Ecranul formularelor poate conține formulare pentru:

* observații ocazionale; și
* evenimente de observare.

Un semn de exclamare lângă un formular indică disponibilitatea unei
actualizări. Apăsați lung numele formularului pentru a forța actualizarea de
pe server. Actualizarea unui formular necesită o conexiune la internet.

Formularele descărcate pentru utilizare offline sunt marcate astfel încât să
poată fi deosebite de formularele care nu sunt încă disponibile offline.

Evenimentele de observare în curs sunt indicate lângă numele formularului
corespunzător.

Ecranul datelor colectate
^^^^^^^^^^^^^^^^^^^^^^^^^

Ecranul datelor colectate enumeră observațiile înregistrate pe dispozitiv. În
funcție de configurația de pe server, valori importante, precum numele unei
specii sau numărul de indivizi, pot fi evidențiate în listă. Acest
comportament poate fi configurat cu modulul ``bold_yellow``.

Din acest ecran, utilizatorii pot:

* revizui înregistrările colectate;
* sincroniza înregistrările cu serverul;
* edita înregistrările care nu au fost încă sincronizate; și
* șterge de pe dispozitiv înregistrările sincronizate.

Sincronizarea necesită o conexiune la internet. Înainte de ștergerea
înregistrărilor locale, verificați dacă sincronizarea s-a încheiat cu succes.

Ecranul jurnalelor traseelor
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Jurnalele traseelor pot fi înregistrate independent de un formular activ. În
timpul sincronizării, jurnalele traseelor înregistrate sunt încărcate în
tabelul jurnalelor traseelor al proiectului.

Din acest ecran, utilizatorii pot:

* vizualiza jurnalele traseelor înregistrate;
* începe înregistrarea unui jurnal al traseului;
* opri înregistrarea unui jurnal al traseului; și
* sincroniza jurnalele traseelor cu serverul.

Ecranul instrumentelor
^^^^^^^^^^^^^^^^^^^^^^

Ecranul instrumentelor oferă utilitare care pot fi folositoare în timpul
activității pe teren, inclusiv:

* un generator de numere aleatorii; și
* un generator de liste personalizate, care poate fi utilizat, de exemplu,
  pentru crearea unei liste de numere de inele.

Setări
------

Limbă
^^^^^

Aplicația acceptă în prezent limbile engleză, română, maghiară, franceză,
germană, kârgâză și rusă.

Puteți contribui la traduceri prin intermediul
`proiectului de traducere a aplicației OpenBioMaps
<https://translate.openbiomaps.org/projects/ecollab/expo-app/>`_.

Temă
^^^^

Aplicația oferă trei opțiuni de temă:

* setarea implicită a sistemului;
* întunecată; și
* luminoasă.

Backup și export
^^^^^^^^^^^^^^^^

Se poate crea un backup pentru păstrarea datelor aplicației sau pentru
furnizarea informațiilor necesare depanării.

Funcția de export pune datele stocate de aplicație la dispoziție pentru
utilizarea cu alte programe. În funcție de datele disponibile, exportul poate
conține formate standard precum CSV și GPX, împreună cu imaginile JPEG
atașate.

Backupurile și exporturile pot conține date sensibile despre proiect,
localizare sau utilizatori. Stocați și transferați aceste fișiere în
siguranță.

Setările formularelor
^^^^^^^^^^^^^^^^^^^^^

Aplicația oferă mai multe opțiuni pentru gestionarea valorilor fixate ale
câmpurilor:

Reinițializare la fiecare deschidere a formularului
  Valorile fixate sunt resetate la fiecare deschidere a formularului. Aceasta
  este opțiunea implicită și cea mai sigură. Poate fi incomodă atunci când
  două formulare sunt utilizate în paralel, deoarece comutarea între acestea
  poate reseta valorile fixate.

Utilizarea permanentă a setărilor serverului
  Aplicația urmează configurația serverului în loc să păstreze valorile
  fixate definite de utilizator. Această opțiune este utilă pentru
  utilizatorii care nu au nevoie de valori fixate sau tind să fixeze valori
  accidental.

Păstrarea setărilor utilizatorului până la sincronizare
  Valorile fixate definite de utilizator rămân disponibile până la
  sincronizarea datelor. Această opțiune este adesea practică atunci când se
  colectează același tip de date pe parcursul unei sesiuni de lucru pe teren,
  iar sincronizarea are loc la sfârșitul zilei. După sincronizare, valorile
  fixate sunt eliminate.

Păstrarea permanentă a setărilor utilizatorului
  Valorile fixate definite de utilizator rămân active până când sunt
  modificate manual. Această opțiune trebuie utilizată cu atenție, deoarece o
  valoare fixată învechită poate fi inclusă accidental în înregistrări
  ulterioare.

Aplicația poate reda și o notificare sonoră după o încercare reușită sau
eșuată de înregistrare.

Setările datelor colectate
^^^^^^^^^^^^^^^^^^^^^^^^^^

Setările datelor colectate controlează dacă aplicația:

* afișează fișierele atașate;
* sincronizează automat datele colectate; și
* afișează întotdeauna butoanele de acțiune sub detaliile înregistrării pe
  ecranul datelor colectate.

Sincronizarea automată necesită acces la rețea. Verificați starea
sincronizării înainte de ștergerea înregistrărilor sau a datelor aplicației
de pe dispozitiv.

Setări GPS și pentru jurnalele traseelor
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Utilizarea GPS poate fi filtrată în funcție de timp și distanță. Aceste
setări afectează atât înregistrarea unui singur punct, cât și înregistrarea
punctelor jurnalului traseului.

Filtrul de distanță reduce actualizările inutile ale poziției atunci când
dispozitivul s-a deplasat mai puțin decât distanța configurată. Pentru
utilizarea obișnuită este recomandată o valoare între 1 și 5 metri, însă
setarea cea mai potrivită depinde de dispozitiv, de precizia necesară și de
condițiile de teren.

Intervalul de timp determină frecvența cu care sunt înregistrate punctele
jurnalului traseului. Intervalul implicit este de 5 secunde. Intervalele mai
scurte pot produce un traseu mai detaliat, dar pot crește și consumul
bateriei și cantitatea de date stocate. Testați intervalul selectat pe
dispozitivele utilizate de proiect înainte de activitatea pe teren.

Stocare
^^^^^^^

Setările de stocare pot fi utilizate pentru:

* ștergerea fișierelor neutilizate;
* eliminarea sesiunilor neutilizate;
* golirea selecțiilor; și
* golirea listelor de completare automată.

Examinați cu atenție opțiunile disponibile înainte de ștergerea datelor.
Observațiile și jurnalele traseelor nesincronizate trebuie încărcate sau
salvate într-un backup înainte de eliminarea datelor locale ale aplicației.

Permisiuni
^^^^^^^^^^

Ecranul permisiunilor indică dacă aplicația are acces la serviciile necesare
ale sistemului de operare, inclusiv la serviciile de localizare. De asemenea,
oferă acces la setările relevante ale sistemului de operare.

Permisiunea de localizare este necesară pentru colectarea datelor bazată pe
GPS și pentru înregistrarea jurnalelor traseelor. Opțiunile de permisiune
disponibile și comportamentul localizării în fundal pot diferi între Android
și iOS.

Setări pe server pentru aplicația mobilă
----------------------------------------

Formulare
^^^^^^^^^

Formularele mobile pentru colectarea datelor sunt configurate prin interfața
OpenBioMaps de gestionare a formularelor de încărcare.

Pentru mai multe informații, consultați :doc:`Gestionarea formularelor de încărcare <upload_forms>`.

Aplicații online pentru dispozitive mobile
==========================================

OpenBioMaps oferă și aplicații bazate pe browser, adecvate pentru dispozitive
mobile:

* :doc:`Aplicație de interogare a datelor pe hartă <pwa>`
* :doc:`Aplicație pentru gestionarea siturilor de eșantionare <mapp>`
