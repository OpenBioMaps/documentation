.. _email-queue:

Coada de e-mail
***************

OpenBioMaps pune notificările de e-mail acceptate într-o coadă separată
pentru fiecare proiect. :ref:`Workerul central <central-background-worker>`
le trimite folosind configurația de e-mail a proiectului. Introducerea în
coadă nu confirmă livrarea.

Administratorii de proiect cu acces pot inspecta coada proiectului din
**Profil > Administrarea proiectului > Email queue**. Pagina afișează
numărul de mesaje pentru fiecare stare, vechimea celui mai vechi mesaj în
așteptare, precum și destinatarul, subiectul, momentele relevante, numărul
încercărilor, codul SMTP și ultima eroare. Tabelul poate fi filtrat și
sortat. Folosiți **Attempts** pentru istoricul încercărilor de livrare.

Stări și acțiuni
================

``queued``
   Așteaptă prima încercare de livrare. **Cancel** este disponibil.

``processing``
   Este preluat de worker. Așteptați rezultatul; nu există acțiune manuală.

``retry``
   Așteaptă o nouă încercare după o eroare temporară. **Cancel** este
   disponibil. Momentul următoarei încercări și ultima eroare ajută la
   diagnosticare.

``sent``
   Workerul a înregistrat trimiterea reușită. Aceasta nu dovedește că mesajul
   a fost acceptat de căsuța destinatarului.

``failed``
   Livrarea a eșuat definitiv sau încercările au fost epuizate. **Retry**
   este disponibil numai dacă e-mailul este legat de un mesaj de proiect
   stocat, din care conținutul poate fi restaurat.

``cancelled``
   Mesajul în așteptare a fost anulat; workerul nu îl va trimite.

**Retry** pune din nou în coadă un mesaj eligibil și începe o nouă serie de
încercări. **Cancel** se aplică numai stărilor ``queued`` și ``retry``.
Ambele acțiuni afectează numai mesajul selectat. Conținutul mesajului este
șters după o stare finală; înregistrările vechi ale activităților încheiate
sunt eliminate după perioada de păstrare.

Depanare
========

Dacă un mesaj rămâne în starea ``queued`` sau ``retry``, verificați
:ref:`serviciul worker <central-background-worker>` și jurnalele sale. Dacă
încercările indică erori de conectare sau autentificare, verificați
configurația SMTP a proiectului. Consultați **Attempts** și **Last error**
înainte de **Retry**. O întrerupere a workerului poate duce la retrimitere;
verificați destinatarul și istoricul mesajului când investigați duplicatele.
