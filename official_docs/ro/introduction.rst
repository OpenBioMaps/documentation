:author: Miklós Bán
:date: 2026-08-08

Introducere
***********

De ce OpenBioMaps?
==================

Una dintre provocările majore în cercetarea biodiversității și conservarea naturii nu este colectarea observațiilor pe teren, ci documentarea, gestionarea și utilizarea fiabilă a datelor colectate. Observațiile de teren trebuie înregistrate într-un mod structurat, stocate în siguranță, verificate pentru identificarea erorilor și făcute accesibile pentru analize și utilizări ulterioare. Atunci când aceste sarcini sunt realizate cu ajutorul unor instrumente neconectate și al unor procese manuale, gestionarea datelor poate deveni inutil de complicată și consumatoare de timp.

OpenBioMaps a fost dezvoltat pentru a soluționa această problemă. Acesta conectează colectarea datelor pe teren cu stocarea, gestionarea, validarea, vizualizarea, analizarea și accesarea datelor într-un cadru unic și flexibil de gestionare a datelor.

Pentru personalul de teren, aceasta înseamnă că observațiile pot fi înregistrate și transferate într-o bază de date structurată fără o prelucrare ulterioară extinsă. Pentru cercetători și managerii de date, aceasta înseamnă că datele pot fi verificate, organizate, interogate, analizate și partajate folosind un sistem coerent. Scopul nu este înlocuirea instrumentelor utilizate de cercetători, ci conectarea acestora într-un flux de lucru coerent și reproductibil.

Ce este OpenBioMaps?
====================

OpenBioMaps este un sistem și un cadru open-source de gestionare a datelor privind biodiversitatea, dezvoltat în colaborare cu specialiști în conservarea naturii și cercetători. Este conceput în principal pentru gestionarea observațiilor și a datelor asociate referitoare la organismele vii, în special în cercetarea biodiversității și conservarea naturii.

O instalare OpenBioMaps oferă un mediu de gestionare a datelor bazat pe PostgreSQL, care poate fi configurat în funcție de cerințele unui anumit proiect. Structura bazei de date, interfețele de introducere a datelor, regulile de acces, fluxurile de lucru și procesele de gestionare a datelor pot fi adaptate nevoilor proiectului.

OpenBioMaps poate fi operat pe serverul propriu al unei organizații sau utilizat prin intermediul unui server întreținut de un partener de încredere. Astfel, poate fi creat un mediu de gestionare a datelor pe termen lung fără dependență de o bază de date controlată central sau de un singur model de date predefinit.

Conectarea colectării și utilizării datelor
==========================================

Un principiu central al OpenBioMaps este că procesul de colectare a datelor nu trebuie separat de gestionarea și utilizarea ulterioară a acestora.

Un flux de lucru tipic poate include:

* colectarea observațiilor pe teren;
* încărcarea sau introducerea observațiilor în baza de date;
* validarea și documentarea datelor;
* organizarea și gestionarea datelor în cadrul proiectului;
* interogarea și filtrarea datelor;
* vizualizarea și analizarea datelor cu ajutorul unor instrumente externe precum QGIS sau R;
* publicarea sau partajarea datelor selectate; și
* reutilizarea datelor pentru cercetare, monitorizare, planificarea conservării sau în alte scopuri.

Deoarece aceste activități sunt conectate printr-un mediu comun de gestionare a datelor, numeroase operațiuni care altfel ar necesita transferul manual al datelor sau prelucrarea repetată a acestora pot fi automatizate. Acest lucru reduce riscul de erori și permite personalului de teren și cercetătorilor să petreacă mai puțin timp cu sarcinile administrative.

Prin urmare, OpenBioMaps nu este doar o bază de date pentru stocarea observațiilor. Acesta oferă un cadru pentru construirea unui flux de lucru complet și reproductibil de gestionare a datelor privind biodiversitatea.

Abordarea OpenBioMaps
=====================

Abordarea OpenBioMaps se bazează pe mai multe principii:

* **Flexibilitate:** proiectele își pot defini propriile structuri ale bazelor de date, câmpuri de date, fluxuri de lucru și reguli de acces.
* **Integrare:** datele pot fi accesate de alte sisteme și instrumente și transferate către acestea, inclusiv QGIS, R și baze de date externe.
* **Reproductibilitate:** interogările și prelucrarea datelor pot fi documentate, repetate și citate.
* **Gestionarea datelor pe termen lung:** datele sunt stocate într-o bază de date structurată, în loc să fie legate de foi de calcul individuale sau de fișiere izolate.
* **Automatizare:** validarea, transferul datelor și alte operațiuni repetitive pot fi automatizate pentru a reduce munca manuală și erorile.
* **Deschidere:** OpenBioMaps se bazează pe software open-source și oferă servicii comunitare accesibile gratuit.
* **Descentralizare:** bazele de date pot fi operate de organizații independente fără a necesita controlul central al datelor.
* **Dezvoltare comunitară:** sistemul este dezvoltat și întreținut în colaborare cu cercetători, specialiști în conservarea naturii și alți utilizatori.

OpenBioMaps este conceput pentru a se adapta cerințelor în schimbare, nu pentru a impune fiecărui proiect un flux de lucru fix. Un proiect poate începe cu o structură de date relativ simplă și poate evolua pe măsură ce se dezvoltă programul său de monitorizare, întrebările de cercetare sau cerințele de gestionare a datelor.


Proprietăți principale
======================
* Servicii OpenBioMaps gratuite și accesibile publicului.
* Structuri ale bazelor de date, interfețe de introducere a datelor, fluxuri de lucru și reguli de acces personalizabile.
* Încărcarea datelor prin interfața web într-o varietate de formate (ods, xls, xlsx, gpx, shp, csv etc.).
* Acces prin API pentru interogarea și încărcarea datelor.
* Interogări repetabile și citabile.
* Identificatori persistenți (DOI) pentru baze de date și interogări.
* Exportarea datelor în diverse formate (shp, csv, gpx, json etc.).
* Integrarea cu R, QGIS, baze de date la distanță și alte sisteme externe.
* Integrarea cu aplicații mobile pentru colectarea datelor pe teren.
* Interfețe personalizabile de gestionare a datelor.
* Legături către baze de date și platforme externe privind biodiversitatea, precum GBIF și iNaturalist.


Implementare tehnică
====================

Pentru o descriere tehnică a modului în care OpenBioMaps conectează configurația proiectului, obiectele bazei de date PostgreSQL, metadatele, fluxurile de încărcare, regulile de acces, interogările și clienții externi, consultați:

:doc:`Fluxul de date și integrarea bazelor de date în OpenBioMaps <obm_workflow>`

Următoarele diagrame oferă o prezentare generală a schemei de interogare:

:download:`Schema de interogare (PDF) <docs/query_scheme.pdf>` |
:download:`Schema de interogare (ODP) <docs/query_scheme.odp>`

Consorțiul OpenBioMaps
======================

OpenBioMaps este dezvoltat și întreținut de un consorțiu format din instituții de cercetare, organizații de conservare și alți parteneri. Consorțiul coordonează dezvoltarea software-ului și întreține serviciile comunitare.

:doc:`Consorțiul OpenBioMaps <consortium>`

:doc:`Primii pași cu OpenBioMaps <getting_started>`
