:author: Miklós Bán
:date: 2026-08-09

Colectarea datelor
******************

Colectarea datelor privind biodiversitatea înregistrează apariția,
abundența, starea sau alte caracteristici ale organismelor vii, împreună cu
contextul în care au fost obținute informațiile. Acest context include în mod
obișnuit locul și momentul colectării, observatorul sau sursa datelor, metoda
de eșantionare și volumul efortului de eșantionare.

Proiectarea unui proces de colectare a datelor determină întrebările
științifice la care pot răspunde datele rezultate. O înregistrare a apariției
unei specii poate documenta faptul că specia a fost detectată într-un anumit
loc și la un anumit moment, însă estimarea absenței, abundenței, distribuției
sau schimbărilor temporale necesită, în general, un plan structurat de
eșantionare și informații despre efortul de eșantionare [MacKenzie2002]_
[Isaac2014]_.

OpenBioMaps nu impune un singur model de date sau protocol de eșantionare. În
schimb, oferă tabele configurabile ale bazei de date, formulare de introducere
a datelor, reguli de validare, câmpuri spațiale și controale de acces care pot
fi adaptate diferitelor proiecte privind biodiversitatea. Prin urmare, planul
de eșantionare și semnificația câmpurilor înregistrate trebuie definite de
proiect înainte de configurarea bazei de date și a formularelor.

Această pagină oferă îndrumări generale pentru conectarea unui plan de
colectare a datelor privind biodiversitatea la un proiect OpenBioMaps.
Instrucțiuni detaliate pentru configurarea formularelor sunt oferite în
:doc:`Gestionarea formularelor de încărcare <upload_forms>`.


Planificarea colectării datelor
===============================

Înainte de a crea tabele ale bazei de date sau formulare de introducere a
datelor, definiți scopul colectării și întrebările la care se așteaptă să
răspundă datele. Deciziile importante privind proiectarea includ:

* organismele, grupurile taxonomice, habitatele sau variabilele de mediu care
  vor fi înregistrate;
* dacă observațiile vor fi colectate oportunist sau conform unui protocol
  prestabilit;
* dacă evenimentele de nedetectare sau cu zero observații trebuie păstrate;
* unitățile spațiale și temporale care vor fi utilizate;
* dacă trebuie înregistrate efortul de eșantionare, metodologia și condițiile
  de mediu;
* dacă eșantionarea va fi repetată în aceleași locuri;
* persoanele care vor colecta, valida, gestiona și utiliza datele;
* vocabularele controlate și referințele taxonomice care vor fi utilizate; și
* metadatele și informațiile privind proveniența care trebuie păstrate.

Aceste decizii trebuie luate înainte de definitivarea structurii tehnice a
bazei de date. Adăugarea ulterioară a unui câmp lipsă poate permite colectarea
unor informații noi, dar nu poate reconstitui informațiile contextuale care
nu au fost înregistrate în timpul studiilor anterioare.

Proiectele destinate să contribuie la evaluări mai ample ale biodiversității
trebuie să analizeze și modul în care observațiile lor se raportează la
concepte și standarde consacrate. Variabilele esențiale ale biodiversității
oferă un cadru pentru conectarea observațiilor locale la monitorizarea mai
amplă a biodiversității [Pereira2013]_. Darwin Core oferă un vocabular
utilizat pe scară largă pentru schimbul de informații despre taxoni,
apariții, evenimente, locații și date conexe privind biodiversitatea
[Wieczorek2012]_.


Principalele abordări de colectare a datelor
============================================

Observațiile privind biodiversitatea pot fi colectate în mai multe moduri.
Următoarele categorii nu se exclud reciproc: un singur proiect OpenBioMaps
poate utiliza formulare și tabele diferite pentru mai multe abordări.


Observații oportuniste
----------------------

O observație oportunistă, incidentală sau ocazională înregistrează un
organism întâlnit fără respectarea unui plan prestabilit de eșantionare.
Printre exemple se numără o pasăre rară observată în timpul unei plimbări,
fotografia unei plante necunoscute sau un animal ucis pe șosea raportat de un
membru al publicului.

În mod normal, o observație oportunistă utilă trebuie să includă:

* taxonul observat;
* data și, dacă este disponibilă, ora observației;
* locația;
* observatorul sau sursa înregistrării;
* o indicație privind abundența sau numărul de indivizi, acolo unde este
  relevant; și
* dovezi justificative, cum ar fi o fotografie, o înregistrare sonoră, o
  referință la un specimen sau un comentariu, dacă sunt disponibile.

Înregistrările oportuniste pot documenta aparițiile, pot extinde cunoștințele
despre locurile în care a fost detectată o specie și pot sprijini studiile
ulterioare. De asemenea, acestea pot contribui la modelarea distribuției sau
la analiza tendințelor atunci când distorsiunile lor de eșantionare sunt
luate în considerare în mod explicit.

Cu toate acestea, o colecție de apariții raportate nu indică în mod normal
locurile în care observatorii au căutat o specie fără a o detecta. De
asemenea, aceasta poate fi afectată de efortul de înregistrare neuniform, de
accesibilitate, de preferințele observatorilor și de variațiile aptitudinilor
de identificare. În consecință, înregistrările oportuniste brute nu trebuie
interpretate în general, în mod izolat, drept estimări nepărtinitoare ale
ocupării, abundenței, dimensiunii populației, distribuției sau schimbărilor
temporale [Isaac2014]_.

Un protocol poate îmbunătăți consecvența observațiilor ocazionale prin
definirea câmpurilor obligatorii, a dovezilor acceptabile, a validării
taxonomice și a preciziei spațiale sau temporale. Astfel de cerințe
îmbunătățesc înregistrările, dar nu transformă prin ele însele colectarea
oportunistă într-un studiu probabilistic sau sistematic.


Evenimente de eșantionare și observare
--------------------------------------

Un eveniment de eșantionare sau observare reprezintă o activitate definită de
colectare a datelor într-un anumit loc și la un anumit moment. Evenimentul
poate specifica și o metodă, o durată, o suprafață eșantionată, lungimea unui
transect, numărul de capcane, numărul de observatori sau o altă măsură a
efortului de eșantionare.

Un eveniment poate conține:

* nicio observație a organismelor, atunci când studiul a fost finalizat, dar
  nu a fost detectat niciunul dintre organismele vizate;
* o observație; sau
* mai multe observații asociate aceleiași activități de eșantionare.

Păstrarea evenimentelor fără detectări este importantă atunci când absența
unei înregistrări are o semnificație definită. O nedetectare documentată
arată că eșantionarea a avut loc conform unui protocol specificat, în timp ce
absența unei înregistrări oportuniste nu arată că cineva a căutat în locul
respectiv. Datele repetate privind detectarea și nedetectarea pot sprijini
modelarea ocupării și estimarea detectării imperfecte atunci când planul
studiului și ipotezele modelului sunt adecvate [MacKenzie2002]_.

În OpenBioMaps, informațiile comune despre eveniment pot fi stocate o singură
dată într-o înregistrare de eveniment sau de listă de observații, în timp ce
observațiile individuale ale taxonilor sunt legate de înregistrarea
respectivă printr-un identificator comun. Astfel se evită repetarea inutilă
și se poate păstra un eveniment chiar și atunci când nu conține observații
ale organismelor.

Pentru o explicație mai detaliată a diferenței, consultați
:doc:`Evenimente de observare și observații ocazionale <observation_events>`.


Monitorizare repetată
---------------------

Monitorizarea implică observații colectate în mod repetat pentru evaluarea
stării sau a schimbărilor. Aceasta utilizează în mod obișnuit locații de
eșantionare fixe sau selectate, o metodă documentată, un program definit și
măsuri comparabile ale efortului.

Un plan de monitorizare poate necesita înregistrarea:

* identității și locației sitului de eșantionare;
* începutului și sfârșitului fiecărui eveniment de eșantionare;
* protocolului și echipamentului utilizat;
* duratei, suprafeței, distanței sau unei alte măsuri a efortului;
* detectărilor și nedetectărilor explicite;
* numărătorilor, gradului de acoperire, biomasei, stării sau unei alte
  variabile de răspuns;
* condițiilor de mediu și factorilor care afectează detectabilitatea;
* modificărilor protocolului sau sitului de eșantionare; și
* informațiilor privind controlul calității și validarea.

Baza de date trebuie să facă distincție între entitățile stabile, precum
siturile de eșantionare și protocoalele, evenimentele repetate și observațiile
efectuate în timpul acelor evenimente. În general, acest lucru necesită
tabele corelate, în locul unui singur tabel care conține toate tipurile de
informații.

OpenBioMaps poate reprezenta astfel de relații prin tabele, identificatori,
formulare de încărcare, interogări și fluxuri de prelucrare a datelor
specifice proiectului. Structura adecvată depinde de planul de monitorizare
și trebuie revizuită de persoane familiarizate atât cu metoda științifică,
cât și cu modelarea relațională a datelor.


Alte surse de date privind biodiversitatea
------------------------------------------

Proiectele pot gestiona și date provenite de la specimene, analize de
laborator, dispozitive de înregistrare acustică, camere-capcană, dispozitive
de urmărire, teledetecție, baze de date externe sau alte sisteme automatizate.

Aceste surse pot necesita entități și metadate suplimentare, precum:

* identificatori pentru specimene, eșantioane sau materiale media;
* evenimente de instalare și recuperare;
* identitatea și configurația dispozitivului;
* informații privind calibrarea și prelucrarea;
* metode de laborator și măsurători derivate;
* legături între materialul-sursă și înregistrările derivate;
* rezultate ale identificării automate și valori de încredere; și
* versiunea software-ului, modelului sau bazei de date de referință utilizate
  pentru prelucrare.

OpenBioMaps poate stoca sau lega astfel de informații, însă proiectul trebuie
să definească modelul de date necesar, strategia de stocare a fișierelor,
procesul de validare și regulile privind proveniența.


Reprezentarea unei colecții în OpenBioMaps
==========================================

O implementare OpenBioMaps trebuie să păstreze conceptele și relațiile
definite de planul de colectare a datelor. Comoditatea bazei de date nu
trebuie să înlocuiască distincția științifică dintre o activitate de
eșantionare, o observație, un taxon, o locație, o persoană și o etapă de
prelucrare.


Tabele și relații
-----------------

O colecție oportunistă simplă poate fi reprezentată printr-un singur tabel
principal de observații. Colecțiile mai structurate pot necesita tabele
separate pentru:

* situri de eșantionare;
* evenimente de eșantionare sau observare;
* observații individuale ale organismelor;
* taxoni sau concepte taxonomice;
* protocoale;
* observatori și organizații;
* specimene, eșantioane sau materiale media;
* dispozitive sau instalări; și
* rezultate ale validării și prelucrării.

Pentru conectarea înregistrărilor corelate trebuie utilizați identificatori
stabili. Aceștia nu trebuie deduși numai din nume, coordonate sau etichete de
afișare, deoarece valorile respective se pot modifica sau pot să nu fie
unice.

Descrierile tabelelor și câmpurilor trebuie să explice semnificația, unitatea,
vocabularul și conținutul așteptat al datelor. Aceste descrieri fac parte din
metadatele proiectului și ajută utilizatorii să interpreteze și să
reutilizeze colecția.


Formulare și fluxuri de lucru
-----------------------------

Un proiect poate defini mai multe formulare de încărcare pentru același
tabel. Formularele separate pot fi utile pentru:

* observații oportuniste;
* studii de teren structurate;
* observații care aparțin unui eveniment de eșantionare;
* importarea seturilor de date istorice;
* trimiteri publice sau de tip citizen science;
* validarea de către experți; și
* colectarea mobilă a datelor.

Fiecare formular trebuie să prezinte numai câmpurile relevante pentru fluxul
său de lucru. Câmpurile obligatorii, listele controlate, valorile implicite,
regulile de validare și textele de ajutor trebuie să reflecte protocolul de
colectare.

Trebuie furnizate descrieri pentru formulare și câmpuri. Aceste descrieri pot
ajuta utilizatorii să înțeleagă ce trebuie introdus și pot fi puse și la
dispoziția clienților mobili compatibili.

.. TODO: Confirmați care aplicații mobile OpenBioMaps afișează descrierile
   formularelor și câmpurilor, ce câmpuri de descriere utilizează și dacă
   descrierile sunt disponibile offline.


Informații de bază recomandate
==============================

Câmpurile exacte necesare unui proiect depind de scopul acestuia, însă
majoritatea colecțiilor de observații trebuie să ia în considerare
următoarele categorii.


Informații despre taxon
-----------------------

Numele taxonilor trebuie selectate, de preferință, dintr-o listă taxonomică
controlată și documentată. Un câmp de completare automată poate ajuta
utilizatorii să găsească denumirile științifice acceptate și, acolo unde este
configurat, denumirile comune sau naționale.

Proiectul trebuie să înregistreze referința taxonomică sau lista de control
utilizată și, acolo unde este posibil, să păstreze un identificator stabil
pentru conceptul taxonomic. Înregistrarea exclusivă a unui șir de caractere
care reprezintă numele poate crea ambiguități atunci când numele se schimbă
sau același nume este interpretat diferit de autorități diferite.

Proiectele le pot permite utilizatorilor să trimită nume care nu sunt încă
prezente în lista controlată. Astfel de valori trebuie marcate clar pentru
revizuire ulterioară, în loc să fie tratate în mod tacit ca nume de taxoni
acceptate. Validarea automată a numelor poate facilita acest proces, însă
potrivirile incerte și corecțiile trebuie să rămână trasabile.

Proiectele OpenBioMaps pot utiliza roluri semantice ale coloanelor asociate
taxonilor, surse de completare automată, liste extensibile și activități de
validare în fundal pentru a sprijini aceste fluxuri de lucru.

Citiți mai multe despre `Superspecies <https://gitlab.com/superspecies/>`_.

.. TODO: Explicați dacă „superspecies” este denumirea actuală a unei baze de
   date, a unui modul, a unui tabel sau a unui serviciu de completare
   automată pentru taxoni specific OpenBioMaps. Dacă este un termen specific
   unei implementări, înlocuiți-l cu denumirea oficială actuală și adăugați
   un link către documentația sa de configurare.

.. TODO: Documentați scopul și configurația actuale ale coloanei sau opțiunii
   ``auto_species_name``. Clarificați dacă aceasta stochează numele trimis,
   un nume validat, un identificator de taxon sau rezultatul unui proces de
   potrivire automată.


Informații despre observator și atribuire
-----------------------------------------

Persoana sau organizația responsabilă pentru o observație trebuie
înregistrată atunci când acest lucru este adecvat din punct de vedere juridic
și etic. Contul OpenBioMaps autentificat poate fi utilizat pentru asocierea
unei trimiteri cu utilizatorul care a încărcat-o, însă acesta nu este în mod
necesar observatorul, persoana care a înregistrat sau identificat
observația, proprietarul datelor ori titularul drepturilor.

Aceste roluri trebuie stocate separat atunci când diferă. Proiectele trebuie
să definească și modul în care datele cu caracter personal sunt afișate,
exportate, păstrate și partajate.

Un formular poate completa automat un câmp pe baza contului utilizatorului
autentificat, pentru a reduce introducerea repetată a datelor.

.. TODO: Confirmați comportamentul exact al opțiunii de formular de încărcare
   ``login_name``. Documentați atributul utilizatorului pe care îl inserează,
   dacă utilizatorul poate edita valoarea și modul în care sunt tratate
   înregistrările trimise prin API sau fără autentificare.


Data și ora
-----------

O observație trebuie să includă data și, acolo unde este relevant, ora la
care a avut loc. Un eveniment de eșantionare poate necesita atât ora de
început, cât și ora de sfârșit.

Proiectele trebuie să definească:

* dacă ora este obligatorie;
* fusul orar utilizat;
* modul de reprezentare a datelor incerte, aproximative sau incomplete;
* dacă valoarea înregistrată se referă la momentul observării, trimiterii,
  importării sau prelucrării; și
* modul de validare a marcajelor temporale furnizate de dispozitive sau de
  fișierele importate.

Momentul observației nu trebuie înlocuit cu marcajul temporal al inserării în
baza de date. Ambele pot fi utile, însă descriu evenimente diferite.


Locație și geometrie
--------------------

Locația poate fi reprezentată prin coordonate, un câmp de geometrie
OpenBioMaps, un identificator al sitului de eșantionare, o localitate
denumită sau o combinație a acestora.

Câmpul ``obm_geometry`` este utilizat în mod obișnuit pentru geometria
spațială a unei înregistrări. În funcție de colecție, acesta poate conține un
punct, o linie sau un poligon. Proiectul trebuie să documenteze și:

* sistemul de referință al coordonatelor — valoarea implicită este WGS84;
* metoda utilizată pentru obținerea locației;
* incertitudinea coordonatelor sau precizia spațială;
* dacă coordonatele au fost transformate sau generalizate;
* orice restricții aplicate locațiilor sensibile; și
* dacă geometria reprezintă organismul, observatorul, un traseu, o suprafață
  eșantionată sau un alt concept spațial.

Coordonatele obținute de la un dispozitiv mobil nu trebuie considerate
automat ca fiind exacte. Precizia poate varia în funcție de dispozitiv,
mediu, metoda de poziționare și timpul alocat obținerii unei poziții.


Cantitate și detectare
----------------------

Acolo unde este relevant, colecția trebuie să înregistreze numărul de
indivizi, procentul de acoperire, biomasa, prezența, starea detectării sau o
altă cantitate definită. Unitatea și interpretarea valorii trebuie precizate
în mod explicit.

Valoarea zero trebuie utilizată numai atunci când protocolul stabilește că
eșantionarea a avut loc, iar ținta nu a fost detectată. Aceasta nu trebuie
utilizată în locul informațiilor lipsă.


Metodă și efort de eșantionare
------------------------------

Studiile structurate trebuie să înregistreze suficiente informații pentru
interpretarea și, acolo unde este posibil, repetarea activității de
eșantionare. Acestea pot include protocolul, durata, distanța, suprafața,
numărul de capcane, efortul observatorilor, echipamentul și condițiile de
mediu.

Informațiile privind metoda și efortul trebuie asociate evenimentului de
eșantionare atunci când se aplică tuturor observațiilor din cadrul
evenimentului respectiv.


Dovezi, validare și proveniență
-------------------------------

Fotografiile, înregistrările sonore, specimenele, comentariile și alte
materiale justificative pot ajuta la validarea unei observații. Proiectele
trebuie să păstreze relația dintre o observație și dovezile sale, împreună cu
informațiile privind originea și drepturile materialului atașat.

Validarea nu trebuie să suprascrie în mod tacit informațiile trimise inițial.
Acolo unde este posibil, proiectele trebuie să păstreze:

* valoarea trimisă;
* valoarea acceptată sau corectată;
* identitatea sau rolul validatorului;
* data validării;
* starea validării și comentariile; și
* metoda sau referința utilizată pentru luarea deciziei.

Păstrarea provenienței face corecțiile inteligibile și sprijină reutilizarea
ulterioară. Într-un sens mai larg, datele privind biodiversitatea trebuie
gestionate astfel încât să poată fi găsite, să fie accesibile în condiții
definite, interoperabile și reutilizabile [Wilkinson2016]_.


Denumirea câmpurilor și interoperabilitatea
===========================================

Denumirile clare și stabile ale câmpurilor facilitează întreținerea unui
proiect. Denumirile câmpurilor trebuie însoțite de descrieri și nu trebuie să
se bazeze pe abrevieri a căror semnificație este cunoscută numai de echipa
inițială a proiectului.

Atunci când datele vor fi schimbate cu sisteme externe, proiectele trebuie să
ia în considerare maparea câmpurilor lor la vocabulare consacrate, precum
Darwin Core [Wieczorek2012]_. Utilizarea unor denumiri inspirate din Darwin
Core poate simplifica maparea, însă atribuirea unei denumiri familiare unui
câmp nu este suficientă în sine. Semnificația, unitatea, cardinalitatea,
vocabularul și relația câmpului trebuie, de asemenea, să fie compatibile cu
termenul corespunzător.

Un proiect nu trebuie să stocheze toate datele direct într-un format de
schimb. Acesta poate utiliza o structură potrivită fluxului său de colectare
și poate crea un export sau o transformare documentată care mapează
înregistrările la standardul necesar.


Listă de verificare practică
============================

Înainte ca un formular de colectare să fie pus la dispoziție, verificați
dacă:

* scopul științific și populația țintă sunt definite;
* observațiile oportuniste și evenimentele de eșantionare structurată sunt
  diferențiate acolo unde este necesar;
* evenimentele finalizate fără detectări pot fi păstrate atunci când
  protocolul impune acest lucru;
* taxonii sunt legați de o listă controlată adecvată sau de un flux de
  revizuire;
* marcajele temporale ale observației și trimiterii nu sunt confundate;
* geometriile au o semnificație definită și un sistem de referință al
  coordonatelor;
* incertitudinea spațială și locațiile sensibile pot fi reprezentate;
* rolurile de observator, utilizator care efectuează încărcarea,
  identificator, proprietar și titular al drepturilor sunt diferențiate
  acolo unde este necesar;
* cantitățile și unitățile sunt documentate;
* metodele și efortul de eșantionare pot fi înregistrate;
* câmpurile obligatorii și regulile de validare reflectă protocolul;
* valorile originale și corecțiile ulterioare rămân trasabile;
* descrierile formularelor și câmpurilor sunt inteligibile pentru persoanele
  care colectează datele;
* regulile de acces și cerințele privind datele cu caracter personal au fost
  revizuite;
* au fost trimise înregistrări de test prin fiecare interfață avută în
  vedere; și
* înregistrările rezultate pot fi interogate, exportate și interpretate fără
  a depinde de cunoștințe nedocumentate.

Structura trebuie testată cu exemple realiste, inclusiv valori lipsă,
identificări incerte, observații din afara zonei așteptate, evenimente fără
detectări, mai multe observații în cadrul unui singur eveniment și
înregistrări trimise din fiecare client web, mobil sau API acceptat.


Exemple de colecții de date
===========================

Exemplele practice pot ilustra modul în care diferite planuri de colectare
sunt reprezentate prin tabele și formulare OpenBioMaps.

Consultați :doc:`Exemple de colecții de date OpenBioMaps <data_collection_examples>`.


Referințe
=========

.. [Isaac2014] Isaac, N. J. B., van Strien, A. J., August, T. A.,
   de Zeeuw, M. P., and Roy, D. B. (2014). Statistics for citizen science:
   extracting signals of change from noisy ecological data. *Methods in
   Ecology and Evolution*, 5(10), 1052–1060.
   https://doi.org/10.1111/2041-210X.12254

.. [MacKenzie2002] MacKenzie, D. I., Nichols, J. D., Lachman, G. B.,
   Droege, S., Royle, J. A., and Langtimm, C. A. (2002). Estimating site
   occupancy rates when detection probabilities are less than one.
   *Ecology*, 83(8), 2248–2255.
   https://doi.org/10.1890/0012-9658(2002)083%5B2248:ESORWD%5D2.0.CO;2

.. [Pereira2013] Pereira, H. M., Ferrier, S., Walters, M., Geller, G. N.,
   Jongman, R. H. G., Scholes, R. J., Bruford, M. W., Brummitt, N.,
   Butchart, S. H. M., Cardoso, A. C., Coops, N. C., Dulloo, E.,
   Faith, D. P., Freyhof, J., Gregory, R. D., Heip, C., Höft, R.,
   Hurtt, G., Jetz, W., Karp, D. S., McGeoch, M. A., Obura, D.,
   Onoda, Y., Pettorelli, N., Reyers, B., Sayre, R., Scharlemann,
   J. P. W., Stuart, S. N., Turak, E., Walpole, M., and Wegmann, M.
   (2013). Essential Biodiversity Variables. *Science*, 339(6117),
   277–278. https://doi.org/10.1126/science.1229931

.. [Wieczorek2012] Wieczorek, J., Bloom, D., Guralnick, R., Blum, S.,
   Döring, M., Giovanni, R., Robertson, T., and Vieglais, D. (2012).
   Darwin Core: An evolving community-developed biodiversity data standard.
   *PLOS ONE*, 7(1), e29715.
   https://doi.org/10.1371/journal.pone.0029715

.. [Wilkinson2016] Wilkinson, M. D., Dumontier, M., Aalbersberg, I. J.,
   Appleton, G., Axton, M., Baak, A., Blomberg, N., Boiten, J.-W.,
   da Silva Santos, L. B., Bourne, P. E., Bouwman, J., Brookes, A. J.,
   Clark, T., Crosas, M., Dillo, I., Dumon, O., Edmunds, S., Evelo,
   C. T., Finkers, R., Gonzalez-Beltran, A., Gray, A. J. G.,
   Groth, P., Goble, C., Grethe, J. S., Heringa, J.,
   't Hoen, P. A. C., Hooft, R., Kuhn, T., Kok, R., Kok, J.,
   Lusher, S. J., Martone, M. E., Mons, A., Packer, A. L.,
   Persson, B., Rocca-Serra, P., Roos, M., van Schaik, R.,
   Sansone, S.-A., Schultes, E., Sengstag, E., Slater, T.,
   Strawn, G., Swertz, M. A., Thompson, M., van der Lei, J.,
   van Mulligen, E., Velterop, J., Waagmeester, A., Wittenburg, P.,
   Wolstencroft, K., Zhao, J., and Mons, B. (2016). The FAIR Guiding
   Principles for scientific data management and stewardship.
   *Scientific Data*, 3, 160018.
   https://doi.org/10.1038/sdata.2016.18
