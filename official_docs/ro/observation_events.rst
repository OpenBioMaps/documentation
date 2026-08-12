:author: Miklós Bán
:date: 2026-08-07

.. observation-events:

Evenimente de observare
.......................

Glosar: eveniment de observare și observație

În conformitate cu standardele internaționale pentru partajarea datelor
(Darwin Core / GBIF), structura de date OpenBioMaps împarte colectarea datelor
de teren în două niveluri distincte: **evenimentul de observare** și
**observația**. Această separare garantează că atât studiile structurate, cât
și observațiile ocazionale pot fi înregistrate cu precizie.

1. Eveniment de observare

Un **eveniment de observare** este un context spațial și temporal predefinit,
care reprezintă o anumită activitate de colectare a datelor sau de
eșantionare.

 **- Aspect esențial:** Evenimentul reprezintă activitatea de teren în sine
 (acțiunea de eșantionare), nu organismul găsit.

**Caracteristici principale:**

Are întotdeauna o **locație înregistrată** (coordonate sau un punct fix) și
un **moment** (sau un interval de timp).

Este asociat adesea cu o anumită metodologie sau cu un anumit protocol (de
exemplu, o numărătoare de 5 minute într-un punct, capturarea în capcane).

**Gestionarea „observațiilor zero” (absență):** Un eveniment de observare este
creat și rămâne valid în sistem chiar dacă cercetătorul nu a observat nicio
specie în timpul studiului.

 - Aceste „date negative” sunt esențiale pentru analiza științifică și pentru
 documentarea efortului de eșantionare.

**Ierarhie:** Un eveniment de observare poate conține **zero, una sau mai
multe** observații individuale (Observation). Observațiile înregistrate în
timpul evenimentului au un identificator comun: ``observation_list_id``.

2. Observație

O **observație** este detectarea sau înregistrarea individuală pe teren a unui
anumit taxon (specie, gen etc.).

 - Esență: aceasta reprezintă datele biologice propriu-zise, dovada prezenței
 organismului.

**Caracteristici principale:**

Conține **denumirea taxonului** (denumirea speciei), precum și **numărul de
indivizi** numărați sau estimați (ori alt indicator cantitativ). Include
întotdeauna o locație, precum și data și ora.

**Tipuri în sistem:**

 **- Observație asociată unui eveniment:** Date despre specii înregistrate în
 cadrul unui studiu structurat (eveniment de observare). În acest caz, datele
 privind locația și momentul sunt moștenite de la eveniment sau sunt
 specificate în cadrul acestuia.
 **- Observație oportunistă:** O observație individuală care nu face parte
 dintr-un protocol sau studiu planificat în prealabil, ci este înregistrată
 imediat, în mod ad-hoc (de exemplu, o pasăre rară observată întâmplător în
 timpul unei deplasări).

Tabel recapitulativ pentru dezvoltatori și utilizatori

+-----------------------------+--------------------------------------------+-----------------------------------------+
| Caracteristică              | Observație                                 | Observație asociată unui eveniment      |
+=============================+============================================+=========================================+
| **Ce reprezintă?**          | Contextul activității de teren/eșantionării.| Observarea unui anumit organism.       |
+-----------------------------+--------------------------------------------+-----------------------------------------+
| **Poate rămâne necompletată?**| **Da.** Dacă, potrivit protocolului,     | **Nu.** Trebuie să includă întotdeauna |
|                             | nu a fost găsit nimic, evenimentul există  | specia și numărul de indivizi.          |
|                             | în continuare.                             |                                         |
+-----------------------------+--------------------------------------------+-----------------------------------------+
| **Indicator cantitativ**    | Efortul de eșantionare (durată, suprafață).| Numărul de indivizi, acoperirea,       |
|                             |                                            | numărătoarea.                            |
+-----------------------------+--------------------------------------------+-----------------------------------------+
| **Echivalent GBIF / DwC**   | Date despre eveniment/eveniment de         | Date despre apariție/apariție           |
|                             | eșantionare                                |                                         |
+-----------------------------+--------------------------------------------+-----------------------------------------+
