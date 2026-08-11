:author: Miklós Bán
:date: 2026-08-08


Primii pași
***********

Alegeți cum să utilizați OpenBioMaps
====================================
Pentru a crea un proiect OpenBioMaps, aveți nevoie de acces la un server OpenBioMaps.
Acesta poate fi propriul server, un server închiriat sau un server deja administrat de
altcineva pentru găzduirea proiectelor OpenBioMaps.

Alăturați-vă unui server existent
---------------------------------
Cea mai simplă modalitate de a crea un proiect nou (denumit uneori bază de date) este
să utilizați un server OpenBioMaps existent. Consultați lista serverelor cunoscute pentru
a vedea dacă aveți acces la unul dintre ele. Există servere publice dedicate care
găzduiesc numeroase baze de date diferite.

Configurați propriul server
---------------------------
Dacă aveți nevoie de o capacitate mai mare sau doriți să controlați accesul la întregul
server, puteți instala propriul server OpenBioMaps.

:doc:`Instalarea serverului OpenBioMaps <../server_install>`

Pentru o instalare bazată pe Docker, consultați:

:doc:`Instalarea cu Docker <../docker>`


Creați un proiect OpenBioMaps
=============================
Un server OpenBioMaps poate găzdui mai multe proiecte (baze de date). Înainte de a crea un
proiect, aveți nevoie de acces la un proiect existent pe server. După ce vi s-a acordat
accesul, puteți crea și configura proiectul în funcție de cerințele colectării datelor.

Pașii necesari sunt descriși în tutorial aici: https://openbiomaps.org/documents/en/tutorials.html#new-project și
aici: https://openbiomaps.org/documents/en/new_project.html

Înțelegeți modelul datelor de observație
========================================
Înainte de a proiecta baza de date și formularele de colectare a datelor, este util
să înțelegeți modul în care OpenBioMaps reprezintă observațiile privind biodiversitatea.

:doc:`Evenimente de observație și observații ocazionale <../observation_events>`


Configurați datele
==================
După crearea proiectului, următorul pas este să definiți modul în care
datele vor fi structurate și colectate.

OpenBioMaps vă permite să creați și să gestionați tabele și câmpuri ale bazei de date
specifice proiectului. Structura bazei de date trebuie să reflecte informațiile
pe care doriți să le înregistrați și relațiile dintre diferitele tipuri de date.

Definiți structura bazei de date
--------------------------------

Tabelele proiectului și coloanele acestora sunt gestionate prin intermediul
interfeței administrative. Tabelele și câmpurile înregistrate acolo devin disponibile
în interfețele OpenBioMaps și pot fi utilizate pentru interogări și colectarea datelor.

Se recomandă să furnizați descrieri pentru tabele și câmpuri. Aceste
descrieri fac parte din metadatele proiectului și îi ajută pe utilizatori să înțeleagă
semnificația și utilizarea prevăzută a datelor.

:doc:`Setări administrative <../admin_settings>`

Creați formulare de colectare a datelor
---------------------------------------

După definirea structurii bazei de date, puteți crea formulare de încărcare
pentru introducerea și colectarea datelor.

Un formular de încărcare stabilește câmpurile disponibile utilizatorilor, câmpurile
obligatorii, modul în care sunt introduse valorile și modul în care sunt colectate datele.
Formularele pot fi utilizate pentru introducerea datelor prin interfața web, încărcarea
fișierelor și accesul prin API.

:doc:`Gestionarea formularelor de încărcare <../upload_forms>`

Structura bazei de date și formularele de colectare a datelor definesc împreună
fluxul de bază pentru colectarea datelor într-un proiect OpenBioMaps.

Gestionarea și accesarea datelor
================================

Înainte de a începe colectarea datelor, luați în considerare modul în care acestea vor fi
gestionate și modul în care va fi controlat accesul la ele.

* :doc:`Accesul la date <../data_access>`
* :doc:`Politica de gestionare a datelor <../data_policy>`


Conectați-vă la proiect
=======================
Proiectele OpenBioMaps pot fi accesate prin mai multe interfețe și
instrumente, în funcție de modul în care datele sunt colectate, gestionate sau analizate.

Interfața web
-------------
Interfața web este instrumentul central pentru gestionarea unui proiect
OpenBioMaps. Aceasta oferă instrumente pentru gestionarea datelor, gestionarea
utilizatorilor, configurare și administrare.

:doc:`Interfața cu utilizatorul <../user_interface>`

:doc:`Interfața de administrare <../admin_settings>`

OpenBioMaps oferă și interfețe programatice pentru aplicațiile client externe.

:doc:`API-ul OpenBioMaps <../api>`


Integrarea cu QGIS
------------------
Pluginul OpenBioMaps pentru QGIS oferă acces la datele OpenBioMaps din QGIS.

`Pluginul OpenBioMaps pentru QGIS <https://plugins.qgis.org/plugins/obm_connect/>`_

Pachetul R
----------
Pachetul R ``obm`` oferă instrumente pentru accesarea și prelucrarea
datelor OpenBioMaps în R.

`obm pe CRAN <https://cran.r-project.org/web/packages/obm/index.html>`_

Alte integrări
--------------
Appsmith, Nextcloud, aveți nevoie de altceva?


Începeți colectarea și gestionarea datelor
==========================================
Proiectul OpenBioMaps este acum pregătit pentru colectarea datelor.

În funcție de fluxul de lucru, datele pot fi introduse prin interfața
web, încărcate din fișiere, colectate cu ajutorul aplicațiilor mobile
sau transferate prin API-ul OpenBioMaps.

După ce datele sunt în sistem, acestea pot fi validate, gestionate, interogate,
vizualizate, analizate și partajate în conformitate cu fluxul de lucru și regulile
de gestionare a datelor ale proiectului.

Pentru informații despre anumite fluxuri de colectare a datelor, consultați
:doc:`Exemple de colectare a datelor cu OpenBioMaps: <../data_collection_examples>`.
