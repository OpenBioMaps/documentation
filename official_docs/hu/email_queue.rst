.. _email-queue:

Emailküldési sor
****************

Az OpenBioMaps a támogatott kimenő emailértesítéseket projektenkénti sorba
helyezi. A :ref:`központi háttérfeladat-worker <central-background-worker>`
a projekt levelezési beállításaival küldi el őket. A sorba állítás önmagában
nem jelenti a sikeres kézbesítést.

Az arra jogosult projektadminisztrátorok a **Profil > Projektadminisztráció >
Email queue** oldalon tekinthetik meg saját projektjük sorát. Az oldal mutatja
az állapotok szerinti darabszámot, a legrégebben várakozó email korát,
valamint a címzettet, a tárgyat, az időpontokat, a kísérletek számát, az SMTP
kódot és az utolsó hibát. A táblázat szűrhető és rendezhető. Az **Attempts**
gombbal a kézbesítési előzmények tekinthetők meg.

Állapotok és műveletek
======================

``queued``
   Az első kézbesítési kísérletre vár. A **Cancel** művelet elérhető.

``processing``
   A worker feldolgozza. Várja meg az eredményt; kézi művelet nincs.

``retry``
   Átmeneti hiba után a következő kísérletre vár. A **Cancel** elérhető. A
   következő időpont és az utolsó hiba segíti a hibakeresést.

``sent``
   A worker sikeres küldést rögzített. Ez önmagában nem bizonyítja, hogy a
   címzett postafiókja átvette a levelet.

``failed``
   A kézbesítés véglegesen meghiúsult, vagy elfogytak az újrapróbálkozások.
   A **Retry** csak akkor érhető el, ha a levél egy tárolt projektüzenethez
   kapcsolódik, amelyből a tartalma visszaállítható.

``cancelled``
   A várakozó levelet törölték a sorból; a worker nem küldi el.

A **Retry** újra sorba állítja a megfelelő meghiúsult levelet, és új
próbálkozási sorozatot kezd. A **Cancel** csak ``queued`` és ``retry``
állapotban használható. Mindkét művelet csak a kiválasztott levélre hat. A
levél tartalma végleges állapot után törlődik; a régi, lezárt feladatok a
megőrzési idő lejártával eltávolításra kerülnek.

Hibaelhárítás
=============

Ha egy levél ``queued`` vagy ``retry`` állapotban marad, ellenőrizze a
:ref:`háttérworker szolgáltatást <central-background-worker>` és a naplóit.
Kapcsolódási vagy hitelesítési hiba esetén ellenőrizze a projekt SMTP
beállításait. A **Retry** előtt nézze meg az **Attempts** és **Last error**
mezőket. Worker-megszakítás után a küldés megismétlődhet, ezért duplikáció
vizsgálatakor ellenőrizze a címzettet és az üzenet előzményeit.
