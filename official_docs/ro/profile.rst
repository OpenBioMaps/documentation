.. _profile:

Pagina de profil
****************

Datele utilizatorului
---------------------

Setări
------
    Adresă de e-mail vizibilă pentru membrii proiectului:
    Primiți e-mailuri de la proiect:
    Ștergeți profilul
    

Profil ORCID
------------
   Adăugați ID-ul profilului ORCID, încărcați datele profilului ORCID (dacă este completat corect)


Informații despre utilizator
----------------------------
stare: normal sau master
evaluare: O valoare între 0 și 1; această valoare provine din evaluarea datelor și din evaluările utilizatorilor care ni se aplică.

Alte baze de date
-----------------
Lista tuturor bazelor de date gestionate de dumneavoastră.


Activitate
----------
Această parte afișează numărul încărcărilor și al datelor dumneavoastră. De asemenea, afișează numărul înregistrărilor modificate.
Statistici privind speciile: Aceasta este o listă a speciilor din încărcările dumneavoastră și o evaluare a acestei liste.


Importuri întrerupte
--------------------
În timpul încărcării datelor noi prin formularele web sau prin încărcarea fișierelor există opțiunea de a salva starea curentă a datelor pregătite.

Când salvați procesul de încărcare, datele și setările dumneavoastră vor fi stocate pe serverul OBM. Puteți restaura starea salvată prin încărcarea identificatorului acesteia.

Identificatorii sunt generați automat. Într-o SESSION și pentru un formular există un singur identificator. Prin urmare, nu există backup incremental!

Puteți urmări importurile salvate pe pagina de profil făcând clic pe linkul „importuri întrerupte”.


Partajarea datelor
------------------
Rezultatele interogărilor pot fi stocate și partajate. În acest caz, persoanele cărora le-ați partajat o interogare nu văd datele stocate în baza de date, ci versiunea stocată a acestora. Starea rezultatului stocat nu se modifică; după creare, aceasta este complet independentă de baza de date. Orice persoană care deține linkul de partajare poate accesa datele stocate în interogare. Un link de partajare este un identificator persistent care poate fi asociat unui identificator DOI.


Marcaje
-------
Interogările pot fi salvate și repetate utilizând linkuri de marcaj. Linkurile de marcaj nu pot fi partajate; acestea funcționează numai după autentificare și numai pentru creatorul lor. Marcajele stochează interogarea propriu-zisă, nu rezultatul interogării, astfel încât modificările conținutului bazei de date vor modifica rezultatele obținute cu ajutorul marcajului.


Chei API
--------
Cheile API active. Aceasta este o funcție asociată autentificării. Vă puteți urmări conexiunile și le puteți închide manual. Este utilizată în principal de dezvoltatori.

Următoarele elemente ale paginii sunt opționale și sunt asociate anumitor module activate în proiectul dumneavoastră.

Setări specifice modulelor
--------------------------
Unele module pot pune la dispoziție aici interfețe de gestionare. De exemplu: modulul pentru crearea utilizatorilor PostgreSQL, modulul pentru încărcarea geometriilor, modulul pentru cererile de descărcare etc.

Gestionarea geometriilor personalizate
......................................
Această funcție este disponibilă numai atunci când modulul shared_geoms o permite.

Geometriile personalizate pot fi încărcate sau desenate pentru acțiuni ulterioare. Aceste acțiuni pot consta în efectuarea interogărilor spațiale sau atribuirea unei geometrii datelor încărcate.

Puteți gestiona geometriile personalizate pe pagina de profil urmând două linkuri: geometrii partajate și geometrii proprii.

Urmând linkul către geometriile proprii, puteți șterge sau partaja geometriile, le puteți redenumi și le puteți modifica opțiunile de vizualizare. Opțiunile de vizualizare sunt următoarele: afișare în lista de selectare spațială și afișare în lista formularelor spațiale denumite pentru atribuirea la datele încărcate.

Urmând linkul către geometriile partajate, puteți redenumi geometriile și le puteți modifica opțiunile de vizualizare. Nu puteți șterge geometriile partajate!

Crearea unui utilizator PostgreSQL
..................................
Creați un utilizator activ timp de un an, cu acces de citire la tabelele de date ale proiectului prin intermediul programelor client SQL. Este necesar pentru utilizarea QGIS!



Opinii
------
Opiniile utilizatorilor despre activitățile dumneavoastră.
