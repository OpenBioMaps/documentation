# Instalarea unui server OpenBioMaps nou

Această pagină oferă o scurtă prezentare generală a instalării serverului și
explică cele mai importante setări la nivel de proiect din
`local_vars.php.inc`.

Majoritatea instalărilor trebuie să utilizeze mediul bazat pe Docker. După
instalarea serverului, utilizați interfața Supervisor pentru a gestiona
configurația de nivel inferior a sistemului și a proiectelor.

> **Important:** Valorile de mai jos sunt exemple de configurare, nu un
> fișier de configurare complet. Verificați fiecare valoare înainte de a o
> utiliza. Nu includeți parole, secrete ale clienților, chei de criptare sau
> alte date de autentificare într-un depozit de cod sursă.

## Instalarea OpenBioMaps cu Docker

Pentru procesul de instalare bazat pe Docker acceptat, consultați:

[Tutorial de instalare Docker](docker.html)

## Depanarea instalărilor și actualizărilor

Pentru problemele frecvente întâlnite după o instalare nouă sau o
actualizare, consultați:

[Erori frecvente](common_errors.html)

## Configurarea serverului

Pentru setările la nivel de sistem, Supervisor, PHP, MapServer și
activitățile cron recomandate, consultați:

[Configurarea serverului](server_administration.html)

## Configurarea la nivel de proiect

Mai multe setări de nivel inferior ale proiectului sunt stocate în
`local_vars.php.inc`. Fișierul este întreținut în mod normal de un
administrator de server prin modul specific proiectului al interfeței
Supervisor.

Setările disponibile prin interfața obișnuită de administrare a proiectului
trebuie gestionate în general acolo. Editați `local_vars.php.inc` numai
atunci când opțiunea necesară nu este disponibilă prin interfața respectivă.

Locația fișierului depinde de instalare și de proiect. Într-o instalare
Docker standard, acesta se află în directorul proiectului din aplicația web
OpenBioMaps.

După modificarea fișierului:

1. verificați sintaxa PHP;
2. reîncărcați pagina proiectului afectat;
3. inspectați jurnalele aplicației și ale serverului pentru a identifica
   erorile; și
4. testați funcția relevantă cu un cont de utilizator adecvat.

Constantele disponibile pot varia între versiunile OpenBioMaps. Păstrați
setările generate de programul de instalare a proiectului sau de Supervisor,
cu excepția cazului în care există un motiv concret pentru a le modifica. Nu
copiați o configurație completă dintr-un alt proiect fără a verifica numele
proiectelor, URL-urile, datele de autentificare ale bazei de date și valorile
referitoare la securitate.

Valorile din secțiunile următoare sunt exemple. Valorile precum parolele,
numele gazdelor, numele proiectelor, domeniile și secretele trebuie
înlocuite cu valori adecvate instalării.

## Conexiunea la baza de date

Aceste setări definesc conexiunea PostgreSQL a proiectului.

| Variabilă | Valoare exemplificativă | Descriere |
| --- | --- | --- |
| `gisdb_user` | `YOUR_PROJECT_ADMIN` | Utilizatorul PostgreSQL folosit de proiect. |
| `gisdb_pass` | `xxxxxxx` | Parola utilizatorului PostgreSQL. Înlocuiți-o cu o parolă aleatorie puternică și păstrați-o secretă. |
| `gisdb_name` | `POSTGRES_DB_NAME` | Numele bazei de date PostgreSQL care conține proiectul. |
| `gisdb_host` | `POSTGRES_HOST_NAME` | Numele gazdei serverului PostgreSQL. Într-o instalare bazată pe containere, acesta este de obicei numele serviciului bazei de date. |

## Numele tabelului SQL al proiectului

| Variabilă | Valoare exemplificativă | Descriere |
| --- | --- | --- |
| `PROJECTTABLE` | `your_database_table_name` | Numele tabelului SQL principal al proiectului și identificatorul proiectului. În instalările care urmează structura standard a directoarelor, acesta poate fi obținut alternativ din numele directorului proiectului. |

Valoarea trebuie să corespundă proiectului creat de programul de instalare
sau Supervisor. Modificarea acesteia într-un proiect existent poate
împiedica OpenBioMaps să găsească datele și configurația proiectului.

## Restricțiile datelor proiectului

| Variabilă | Valoare exemplificativă | Descriere |
| --- | --- | --- |
| `ACC_LEVEL` | `public` | Controlează accesul la date. `public` permite tuturor să citească datele; `group` limitează accesul la membrii grupului proiectului. |
| `MOD_LEVEL` | `group` | Controlează modificarea datelor. `public` permite tuturor să modifice datele; `group` limitează modificarea la membrii grupului proiectului. |

Utilizați cea mai restrictivă setare adecvată proiectului și verificați
rezultatul atât cu utilizatori autentificați, cât și cu utilizatori
neautentificați.

## Setări de limbă

| Variabilă | Valoare exemplificativă | Descriere |
| --- | --- | --- |
| `LANG` | `hu` | Limba implicită a proiectului. Trebuie să existe un fișier corespunzător pentru limbă. |
| `LANGUAGES` | `en: in English`, `hu: magyarul`, `ro: română`, `ru: русский` | Limbile oferite de proiect și etichetele afișate ale acestora. Prima intrare este limba implicită utilizată de componentele care se bazează pe ordinea acestei liste. |

Păstrați `LANG` în concordanță cu limbile configurate ale proiectului.

## Setări pentru căi și URL-uri

| Variabilă | Valoare exemplificativă | Descriere |
| --- | --- | --- |
| `PATH` | `/biomaps/resources` | Calea URL la care sunt disponibile resursele proiectului. Pe `openbiomaps.org`, aceasta este în mod obișnuit `/projects`; într-o altă instalare poate fi goală sau poate utiliza o cale specifică implementării. |
| `URL` | `TYPE-YOUR-SERVER-DOMAIN_HERE` urmat de `PATH` | URL-ul de bază complet pentru resursele proiectului. Înlocuiți substituentul domeniului și includeți schema, gazda, portul opțional și calea de implementare corecte. |

De exemplu, dacă URL-ul de bază al serverului este `https://example.org`,
iar `PATH` este `/biomaps/resources`, valoarea `URL` rezultată este
`https://example.org/biomaps/resources`.

## Setări MapServer și MapCache

| Variabilă | Valoare exemplificativă | Descriere |
| --- | --- | --- |
| `PRIVATE_MAPSERV` | `URL/private/proxy.php` | URL-ul proiectului pentru proxy-ul MapServer privat. Este construit din `URL`. |
| `PUBLIC_MAPSERV` | `URL/public/proxy.php` | URL-ul proiectului pentru proxy-ul MapServer public. Este construit din `URL`. |
| `PRIVATE_MAPCACHE` | `URL/private/cache.php` | URL-ul proiectului pentru proxy-ul MapCache privat. Este construit din `URL`. |
| `PUBLIC_MAPCACHE` | `URL/public/cache.php` | URL-ul proiectului pentru proxy-ul MapCache public. Este construit din `URL`. |
| `MAPSERVER` | `http://localhost/cgi-bin/mapserv.fcgi` | Punctul final MapServer pentru o instalare autonomă. |
| `MAPSERVER` | `http://mapserver/cgi-bin/mapserv` | Punctul final MapServer pentru o instalare Docker. Utilizați această valoare în locul valorii pentru instalarea autonomă atunci când serviciul `mapserver` este disponibil prin rețeaua Docker. |
| `MAPCACHE` | `http://localhost/mapcache` | Punctul final MapCache. Utilizarea MapCache necesită o configurare suplimentară a serverului; consultați documentația MapServer. |
| `MAP` | `PMAP` | Numele obiectului hartă utilizat de proiect. |
| `PRIVATE_MAPFILE` | `private.map` | Fișierul mapfile MapServer privat utilizat de proiect. Această setare este păstrată pentru compatibilitate și poate fi mutată în viitor în setările proiectului gestionate prin PostgreSQL. |

Configurați o singură valoare `MAPSERVER`. Valoarea corectă depinde de
faptul că MapServer rulează local sau ca serviciu Docker separat.

## Invitații

| Variabilă | Valoare exemplificativă | Descriere |
| --- | --- | --- |
| `INVITATIONS` | `0` | Numărul maxim de invitații active pe care le poate avea simultan un utilizator. Atunci când valoarea este `0`, numai administratorii pot trimite invitații. Valoarea implicită documentată este `11`. |

## Setări pentru e-mail

Aceste setări opționale sunt utilizate atunci când nu este disponibil un
agent local de e-mail adecvat.

| Variabilă | Valoare exemplificativă | Descriere |
| --- | --- | --- |
| `SMTP_AUTH` | `true` | Activează autentificarea SMTP. |
| `SMTP_HOST` | `mail.your-smtp-server.org` | Numele gazdei serverului SMTP. |
| `SMTP_USERNAME` | `MAIL USER` | Numele utilizatorului folosit pentru autentificarea la serverul SMTP. |
| `SMTP_PASSWORD` | `xxxxxx` | Parola SMTP. Păstrați-o secretă și nu o includeți în depozit. |
| `SMTP_PORT` | `PORT-NUMBER` | Portul serverului SMTP. Selectați portul corespunzător configurației de criptare și autentificare a serverului. |
| `SMTP_SENDER` | `mail_user@your-smtp-server.org` | Adresa expeditorului utilizată pentru e-mailurile trimise de proiect. |
| `SMTP_SECURE` | `tls` | Modul opțional de securitate a transportului SMTP. |

Un exemplu istoric pentru Google SMTP utiliza următoarele valori:

| Variabilă | Valoare exemplificativă istorică |
| --- | --- |
| `SMTP_HOST` | `smtp.gmail.com` |
| `SMTP_USERNAME` | `your-user@gmail.com` |
| `SMTP_PASSWORD` | `xxxxxxxxx` |
| `SMTP_SECURE` | `tls` |
| `SMTP_PORT` | `587` |

Este posibil ca exemplul istoric Google să nu mai funcționeze fără o
configurare suplimentară a furnizorului și nu trebuie copiat fără a verifica
cerințele actuale de autentificare ale Google.

Următoarele setări asociate e-mailului sunt depreciate și nu trebuie
utilizate pentru proiecte noi:

| Variabilă | Valoare exemplificativă | Descriere |
| --- | --- | --- |
| `SHINYURL` | `false` | Setare Shiny URL depreciată. |
| `RSERVER` | `false` | Setare R server depreciată. |

## Pagina afișată după autentificare

| Variabilă | Valoare exemplificativă | Descriere |
| --- | --- | --- |
| `LOGINPAGE` | `map` | Pagina încărcată după autentificare. Opțiunile documentate acceptate sunt `profile`, `mainpage` și `map`. Valoarea implicită este `map`. |
| `TRAINING` | `false` | Setare depreciată pentru modul de instruire. Nu o utilizați pentru proiecte noi. |

## Configurarea paginii principale

`MAINPAGE` grupează setările care controlează structura și conținutul paginii
principale a proiectului.

| Cheie | Valoare exemplificativă | Descriere |
| --- | --- | --- |
| `template` | `gridbox` | Șablonul paginii principale. `intropage` este o altă valoare documentată pentru șablon. |
| `content1` | `map` | Conținutul primei zone principale. Valorile documentate includ `map`, `upload-table` și `slideshow`. |
| `sidebar1` | `column_dinpi.altema\|custom_countries\|members\|uploads\|data\|species\|species_stat` | Lista componentelor barei laterale, separate prin bară verticală. Componentele obișnuite includ `members`, `uploads`, `data`, `species` și `species_stat`; pot fi incluse și componente specifice proiectului. |
| `system_footer` | `on` | Afișează subsolul sistemului atunci când este setată la `on`. |
| `system_header` | `off` | Ascunde antetul sistemului atunci când este setată la `off`. |
| `custom_skeleton` | `1` | Selector opțional pentru structura personalizată a paginii. Este dezactivat în configurația exemplificativă. |
| `restrictaded_pages` | `map`, `id`, `history`, `profile`, `data`, `table`, `editrecord`, `qtable`, `query`, `show`, `LQ`, `metadata` | Lista opțională a paginilor supuse restricțiilor. Cheia este scrisă `restrictaded_pages` pentru compatibilitate cu aplicația. Este dezactivată în configurația exemplificativă. |

Componentele barei laterale specifice proiectului trebuie să existe și să
fie configurate corect înainte de a fi adăugate la `sidebar1`.

## Domeniul proiectului Docker

| Variabilă | Valoare exemplificativă | Descriere |
| --- | --- | --- |
| `OB_PROJECT_DOMAIN` | Valoarea lui `OB_DOMAIN` | Domeniul proiectului specific Docker, utilizat la crearea alertelor prin e-mail pentru încărcările noi. Valoarea este moștenită din setarea `OB_DOMAIN` de la nivelul sistemului. |

## Configurarea stilului

`STYLE` selectează stilul proiectului.

| Cheie | Valoare exemplificativă | Descriere |
| --- | --- | --- |
| `template` | `evolvulus` | Numele directorului stilului sau șablonului utilizat de proiect. Stilul denumit trebuie să fie instalat. |

## Configurarea subsolului

`FOOTER` controlează legăturile, selectarea limbii și siglele partenerilor
afișate în subsolul proiectului.

| Cheie | Valoare exemplificativă | Descriere |
| --- | --- | --- |
| `links` | `map\|upload\|about\|terms\|usage\|privacy` | Lista legăturilor din subsol, separate prin bară verticală. |
| `languages` | `languages` | Activează sau identifică selectorul de limbă din subsol. |
| `partners` | Intrări OpenBioMaps și University of Debrecen | Lista definițiilor siglelor partenerilor. |

Fiecare element din `partners` poate conține următoarele câmpuri:

| Câmp | Valoare exemplificativă | Descriere |
| --- | --- | --- |
| `img` | `obm_logo.png` | Fișierul imagine afișat pentru partener. |
| `size` | `110` | Dimensiunea opțională de afișare. O valoare goală lasă dimensiunea nespecificată. |
| `url` | `https://openbiomaps.org` | URL-ul destinației deschise de la sigla partenerului. |

Configurația exemplificativă conține următorii parteneri:

| Imagine | Dimensiune | URL |
| --- | --- | --- |
| `obm_logo.png` | `110` | `https://openbiomaps.org` |
| `unideb_logo.png` | gol | `https://unideb.hu` |

## Configurarea antetului

`HEADER` controlează legăturile și structura antetului proiectului.

| Cheie | Valoare exemplificativă | Descriere |
| --- | --- | --- |
| `links` | `upload\|map\|messages\|profile\|localize` | Lista legăturilor afișate în antet, separate prin bară verticală. |
| `layout` | `obm` | Structura antetului utilizată de proiect. |

## Hash de criptare

| Variabilă | Valoare exemplificativă | Descriere |
| --- | --- | --- |
| `MyHASH` | `password-string` | Valoare secretă utilizată de module precum `read_table` pentru criptarea sau mascarea numelor tabelelor și a valorilor asociate. Înlocuiți-o cu o valoare aleatorie puternică, păstrați-o stabilă pentru un proiect existent și nu o publicați. |

Modificarea `MyHASH` într-un proiect existent poate invalida valorile create
anterior cu vechiul secret.

## Setări cache personalizate

| Variabilă | Valoare exemplificativă | Descriere |
| --- | --- | --- |
| `CACHE_HOST` | Valoarea variabilei de mediu `CACHE_HOST`, în caz contrar `localhost` | Gazda care rulează serviciul cache. |
| `CACHE_PORT` | Valoarea variabilei de mediu `CACHE_PORT`, în caz contrar `11211` | Portul serviciului cache. Portul `11211` este utilizat în mod obișnuit de Memcached. |

În instalările Docker, utilizați numele serviciului cache în loc de
`localhost` atunci când serviciul cache rulează într-un alt container.

## Autentificarea OpenID Connect

`OPENID_CONNECT` conține una sau mai multe definiții ale furnizorilor de
identitate. Exemplul configurează Google.

| Furnizor/cheie | Valoare exemplificativă | Descriere |
| --- | --- | --- |
| Numele furnizorului | `google` | Identificatorul intern al furnizorului OpenID Connect. |
| `client_id` | `xxxxx.apps.googleusercontent.com` | Identificatorul clientului emis de furnizor. |
| `client_secret` | `xxxxxxx` | Secretul clientului emis de furnizor. Păstrați-l secret și nu îl includeți în depozit. |
| `provider_url` | `https://accounts.google.com/` | URL-ul de bază al furnizorului OpenID Connect. |
| `OPENID_CONNECT_CERT_PATH` | `/etc/ssl/certs/ca-certificates.crt` | Calea către pachetul de certificate CA de încredere utilizat pentru validarea conexiunilor TLS la furnizor. |

Înregistrați URI-ul exact de redirecționare OpenBioMaps la furnizor și
verificați dacă aplicația poate citi pachetul configurat de certificate CA.

## Legătura PWA

| Variabilă | Valoare exemplificativă | Descriere |
| --- | --- | --- |
| `PWA_LINK` | `on` | Activează legătura Progressive Web App pe pagina principală a proiectului. |

## Pagini personalizate

| Variabilă | Valoare exemplificativă | Descriere |
| --- | --- | --- |
| `CUSTOM_PAGES` | `mysite`, `my_other_site` | Lista identificatorilor paginilor personalizate disponibile în proiect. Fiecare pagină personalizată menționată trebuie implementată în locația corespunzătoare a proiectului. |

## Dimensiunea imaginilor atașate

| Variabilă | Valoare exemplificativă | Descriere |
| --- | --- | --- |
| `ALLOWED_FILE_SIZE` | `4194304` | Dimensiunea maximă permisă pentru imaginile atașate, în octeți. Valoarea exemplificativă este 4 MiB. |

Limita efectivă de încărcare poate fi constrânsă și de setările PHP, ale
serverului web, ale proxy-ului invers sau ale altor componente de
infrastructură.

## Tabele temporare pentru încărcarea listelor de observații

| Variabilă | Valoare exemplificativă | Descriere |
| --- | --- | --- |
| `USE_TEMPTABLES_FOR_OBSLISTS` | `true` | Activează utilizarea tabelelor denumite după modelul `temporary_tables.obs_*` în timpul încărcării listelor de observații. În configurația documentată, această valoare este stocată ca șirul `true`, nu ca valoare booleană. |

Utilizatorul bazei de date trebuie să aibă permisiunile necesare pentru
schema tabelelor temporare.

## Exportul datelor în fundal

| Variabilă | Valoare exemplificativă | Descriere |
| --- | --- | --- |
| `DATA_EXPORT_BGPROC_LIMIT` | `1000` | Numărul de înregistrări peste care exportul datelor este procesat ca activitate de fundal, în locul unei descărcări directe obișnuite. |

Exporturile în fundal necesită configurarea și rularea executorului de
activități al proiectului.

## Scheme suplimentare ale proiectului

| Variabilă | Valoare exemplificativă | Descriere |
| --- | --- | --- |
| `PROJECT_SCHEMAS` | `sablon_archive` | Lista schemelor PostgreSQL suplimentare asociate proiectului. |

Asigurați-vă că utilizatorul bazei de date a proiectului are privilegiile
necesare pentru fiecare schemă enumerată.

## Verificări de securitate și ale solicitărilor automate

Aceste setări activează verificările ratei solicitărilor susținute de Redis.
Atunci când limitele definite sunt depășite, OpenBioMaps poate intra într-un
mod de protecție împotriva atacurilor și poate afișa o verificare „Sunteți
om?” pe durata configurată.

| Variabilă | Valoare exemplificativă | Descriere |
| --- | --- | --- |
| `SECURITY_CHECK` | `true` | Activează verificarea de securitate. |
| `REDIS_HOST` | `127.0.0.1` | Gazda serverului Redis. Valoarea implicită documentată este `127.0.0.1`. În Docker, utilizați numele serviciului Redis dacă Redis rulează într-un alt container. |
| `REDIS_PORT` | `6379` | Portul serverului Redis. Valoarea implicită documentată este `6379`. |
| `SECURITY_IP_LIMIT` | `30` | Numărul maxim de solicitări permise de la o singură adresă IP în 10 secunde. Setați valoarea la `false` pentru a dezactiva verificarea per adresă IP. Valoarea implicită documentată este `30`. |
| `SECURITY_GLOBAL_LIMIT` | `10` | Rata totală maximă a solicitărilor pe secundă. Valoarea implicită documentată este `10`. |
| `SECURITY_ATTACK_TTL` | `600` | Durata în secunde pentru care modul de protecție împotriva atacurilor rămâne activ. Valoarea implicită documentată este `600` de secunde. |

Alegeți limitele în funcție de traficul așteptat, configurația proxy-ului și
numărul de utilizatori care par să utilizeze aceeași adresă IP sursă. Dacă
OpenBioMaps se află în spatele unui proxy invers, verificați dacă aplicația
primește adresele IP corecte ale clienților.

## Opțiuni pentru dezvoltatori

Aceste opțiuni sunt destinate dezvoltării și depanării, nu utilizării normale
în producție.

| Variabilă | Valoare exemplificativă | Descriere |
| --- | --- | --- |
| `branch` | `testing` | Selectează o altă ramură Git, precum ramura de testare. Proiectele de producție trebuie să utilizeze în mod normal ramura de producție acceptată. |
| `DEBUG_PDS` | `true` | Activează înregistrarea suplimentară în jurnal pentru acțiunile PDS. Dezactivați înregistrarea detaliată pentru depanare după finalizarea depanării, deoarece aceasta poate mări volumul jurnalelor sau poate expune detalii operaționale sensibile. |

După activarea unei opțiuni pentru dezvoltatori, monitorizați jurnalele
aplicației și reveniți asupra opțiunii atunci când nu mai este necesară.
