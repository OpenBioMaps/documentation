Clienți
*******

QGIS
====
QGIS (denumit anterior Quantum GIS) este un sistem informațional geografic 
(GIS) gratuit și open source, care permite afișarea, editarea și analizarea 
datelor geografice, precum și crearea hărților profesionale. Dezvoltat în 
cadrul proiectului OSGeo, software-ul este una dintre cele mai populare 
aplicații GIS desktop din lume, oferind o alternativă completă la soluțiile 
comerciale costisitoare bazate pe licență (precum ArcGIS).

Pluginul OpenBioMaps pentru QGIS oferă acces la datele OpenBioMaps din QGIS.

`Pluginul OpenBioMaps pentru QGIS <https://plugins.qgis.org/plugins/obm_connect/>`_


Utilizarea R
============
R este un limbaj de programare și un mediu software gratuit, conceput pentru 
calcule statistice, analiza datelor și grafică. Creat în 1993 de Ross Ihaka și 
Robert Gentleman la University of Auckland, acesta este utilizat pe scară 
largă de cercetători, specialiști în explorarea datelor și statisticieni.

Pachetul R ``obm`` oferă instrumente pentru accesarea și utilizarea datelor 
OpenBioMaps din R.

`obm pe CRAN <https://cran.r-project.org/web/packages/obm/index.html>`_

Clienți PostgreSQL
==================
Gestionare completă și multiplatformă a bazelor de date

`pgAdmin este un client PostgreSQL profesional care poate fi utilizat pentru gestionarea bazelor de date PostgreSQL OBM <https://www.pgadmin.org/>`_

Clienți MapServer
=================
Clienții MapServer sunt interfețe software, aplicații GIS desktop sau biblioteci 
de cartografiere web care utilizează servicii web OGC (precum WMS, WFS și WCS) 
furnizate de MapServer. Printre clienții obișnuiți se numără aplicații desktop 
precum QGIS și ArcGIS, biblioteci web precum OpenLayers și Leaflet, precum și 
funcționalitatea internă a MapServer de a acționa drept client pentru servere 
aflate la distanță.
OpenBioMaps este randat în principal utilizând MapServer, astfel încât programele 
client MapServer se pot conecta la serviciile de hărți OpenBioMaps, deși acest 
lucru depinde în mare măsură de configurația proiectului.

Clienți OAuth
=============
JWT (JSON Web Token) este un format de token compact și autonom, utilizat pentru 
transmiterea securizată a datelor. OAuth 2.0 este un cadru de autorizare care 
deleagă accesul. Acestea nu sunt opțiuni concurente; OAuth utilizează frecvent un 
JWT semnat drept token de acces sau format de token ID pentru a transmite 
revendicările utilizatorului fără păstrarea stării.

Appsmith
========
Appsmith este o platformă de dezvoltare open source, low-code, care permite 
crearea extrem de rapidă a instrumentelor interne pentru afaceri, a interfețelor 
administrative, a tablourilor de bord și a fluxurilor de lucru personalizate. 
Avem propria instanță!
`OBM Appsmith <https://appsmith.openbiomaps.org/user/login>`_

Nextcloud
=========
Nextcloud este o platformă open source, găzduită local, pentru colaborarea asupra 
conținutului, care vă oferă control deplin asupra propriilor date. Este o 
alternativă excelentă, axată pe confidențialitate, la servicii cloud populare 
precum Google Drive, Microsoft OneDrive și Dropbox. Desigur, Nextcloud poate fi 
integrat cu OpenBioMaps, după cum demonstrează baza de date Camptrap, în care 
utilizatorii încarcă imagini într-un cont Nextcloud; o aplicație construită în 
cadrul proiectului OBM analizează apoi aceste imagini și le încarcă înapoi în 
contul Nextcloud.

Clienți API
===========
OpenBioMaps oferă și interfețe programatice pentru aplicații client externe. Una 
dintre cele mai mari aplicații client ale noastre este aplicația mobilă de teren 
OpenBioMaps, dezvoltată de ECOLLAB.

:doc:`API OpenBioMaps <../api>`
