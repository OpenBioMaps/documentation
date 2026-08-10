# Új OpenBioMaps-szerver telepítése

Ez az oldal rövid áttekintést nyújt a szerver telepítéséről, és ismerteti a
`local_vars.php.inc` legfontosabb projektszintű beállításait.

A legtöbb telepítéshez a Docker-alapú környezetet érdemes használni. A szerver
telepítése után az alacsony szintű rendszer- és projektkonfiguráció a
Supervisor felületén kezelhető.

> **Fontos:** Az alábbi értékek konfigurációs példák, nem pedig egy teljes
> konfigurációs fájl részei. Használat előtt minden értéket ellenőrizzen. Ne
> véglegesítsen jelszavakat, klienstitkokat, titkosítási kulcsokat vagy más
> hitelesítési adatokat forráskód-tárolóba.

## Az OpenBioMaps telepítése Docker használatával

A támogatott Docker-alapú telepítési folyamatot lásd itt:

[Docker-telepítési útmutató](docker.html)

## Telepítések és frissítések hibaelhárítása

Az új telepítés vagy frissítés után előforduló gyakori problémákról lásd:

[Gyakori hibák](common_errors.html)

## Szerverkonfiguráció

A rendszerszintű beállításokkal, a Supervisor, a PHP és a MapServer
konfigurációjával, valamint az ajánlott cron-feladatokkal kapcsolatban lásd:

[Szerverkonfiguráció](server_administration.html)

## Projektszintű konfiguráció

Számos alacsony szintű projektbeállítást a `local_vars.php.inc` tárol. A fájlt
általában egy szerveradminisztrátor kezeli a Supervisor felület
projektspecifikus módjában.

A normál projektadminisztrációs felületen elérhető beállításokat általában ott
kell kezelni. Csak akkor szerkessze a `local_vars.php.inc` fájlt, ha a
szükséges beállítás nem érhető el ezen a felületen.

A fájl helye a telepítéstől és a projekttől függ. Szabványos
Docker-telepítésben a projekt könyvtárában, az OpenBioMaps webalkalmazás alatt
található.

A fájl módosítása után:

1. ellenőrizze a PHP-szintaxist;
2. töltse újra az érintett projektoldalt;
3. vizsgálja meg az alkalmazás- és szervernaplókat, hogy vannak-e bennük
   hibák; valamint
4. tesztelje az érintett funkciót megfelelő felhasználói fiókkal.

Az elérhető konstansok OpenBioMaps-kiadásonként eltérhetnek. Tartsa meg a
projekttelepítő vagy a Supervisor által létrehozott beállításokat, kivéve, ha
konkrét oka van a módosításukra. Ne másoljon át teljes konfigurációt egy másik
projektből a projektnevek, URL-ek, adatbázis-hitelesítési adatok és biztonsági
értékek ellenőrzése nélkül.

A következő szakaszokban szereplő értékek példák. Az olyan értékeket, mint a
jelszavak, állomásnevek, projektnevek, tartományok és titkos értékek, a
telepítésnek megfelelő értékekre kell cserélni.

## Adatbázis-kapcsolat

Ezek a beállítások határozzák meg a projekt PostgreSQL-kapcsolatát.

| Változó | Példaérték | Leírás |
| --- | --- | --- |
| `gisdb_user` | `YOUR_PROJECT_ADMIN` | A projekt által használt PostgreSQL-felhasználó. |
| `gisdb_pass` | `xxxxxxx` | A PostgreSQL-felhasználó jelszava. Cserélje erős, véletlenszerű jelszóra, és tartsa titokban. |
| `gisdb_name` | `POSTGRES_DB_NAME` | A projektet tartalmazó PostgreSQL-adatbázis neve. |
| `gisdb_host` | `POSTGRES_HOST_NAME` | A PostgreSQL-szerver állomásneve. Konténeralapú telepítésben ez általában az adatbázis-szolgáltatás neve. |

## A projekt SQL-táblájának neve

| Változó | Példaérték | Leírás |
| --- | --- | --- |
| `PROJECTTABLE` | `your_database_table_name` | A projekt elsődleges SQL-táblájának neve és projektazonosítója. A szabványos könyvtárelrendezést követő telepítésekben ez a projekt könyvtárnevéből is származtatható. |

Az értéknek meg kell egyeznie a telepítő vagy a Supervisor által létrehozott
projekttel. Egy meglévő projektben történő módosítása megakadályozhatja, hogy
az OpenBioMaps megtalálja a projekt adatait és konfigurációját.

## Projektadatok korlátozásai

| Változó | Példaérték | Leírás |
| --- | --- | --- |
| `ACC_LEVEL` | `public` | Az adathozzáférést szabályozza. A `public` mindenki számára engedélyezi az adatok olvasását, a `group` pedig a projekt felhasználói csoportjainak tagjaira korlátozza a hozzáférést. |
| `MOD_LEVEL` | `group` | Az adatok módosítását szabályozza. A `public` mindenki számára engedélyezi az adatok módosítását, a `group` pedig a projekt felhasználói csoportjainak tagjaira korlátozza a módosítást. |

Használja a projektnek megfelelő legszigorúbb beállítást, és ellenőrizze az
eredményt hitelesített és nem hitelesített felhasználókkal egyaránt.

## Nyelvi beállítások

| Változó | Példaérték | Leírás |
| --- | --- | --- |
| `LANG` | `hu` | A projekt alapértelmezett nyelve. Léteznie kell egy megfelelő nyelvi fájlnak. |
| `LANGUAGES` | `en: in English`, `hu: magyarul`, `ro: română`, `ru: русский` | A projektben felkínált nyelvek és megjelenített címkéik. A lista első eleme az alapértelmezett nyelv azoknál az összetevőknél, amelyek a lista sorrendjére támaszkodnak. |

Tartsa összhangban a `LANG` értékét a projekt beállított nyelveivel.

## Elérési út- és URL-beállítások

| Változó | Példaérték | Leírás |
| --- | --- | --- |
| `PATH` | `/biomaps/resources` | Az az URL-útvonal, amelyen a projekt erőforrásai elérhetők. Az `openbiomaps.org` esetében ez általában `/projects`; más telepítésben lehet üres, vagy használhat a telepítésre jellemző útvonalat. |
| `URL` | `TYPE-YOUR-SERVER-DOMAIN_HERE`, majd a `PATH` | A projekt erőforrásainak teljes alap-URL-je. Cserélje le a tartomány helyőrzőjét, és adja meg a megfelelő sémát, állomást, opcionális portot és telepítési útvonalat. |

Ha például a szerver alap-URL-je `https://example.org`, a `PATH` pedig
`/biomaps/resources`, akkor az eredményül kapott `URL`:
`https://example.org/biomaps/resources`.

## MapServer- és MapCache-beállítások

| Változó | Példaérték | Leírás |
| --- | --- | --- |
| `PRIVATE_MAPSERV` | `URL/private/proxy.php` | A privát MapServer-proxy projekt-URL-je. Az `URL` értékéből épül fel. |
| `PUBLIC_MAPSERV` | `URL/public/proxy.php` | A nyilvános MapServer-proxy projekt-URL-je. Az `URL` értékéből épül fel. |
| `PRIVATE_MAPCACHE` | `URL/private/cache.php` | A privát MapCache-proxy projekt-URL-je. Az `URL` értékéből épül fel. |
| `PUBLIC_MAPCACHE` | `URL/public/cache.php` | A nyilvános MapCache-proxy projekt-URL-je. Az `URL` értékéből épül fel. |
| `MAPSERVER` | `http://localhost/cgi-bin/mapserv.fcgi` | MapServer-végpont önálló telepítéshez. |
| `MAPSERVER` | `http://mapserver/cgi-bin/mapserv` | MapServer-végpont Docker-telepítéshez. Az önálló telepítés értéke helyett ezt használja, ha a `mapserver` szolgáltatás elérhető a Docker-hálózaton keresztül. |
| `MAPCACHE` | `http://localhost/mapcache` | MapCache-végpont. A MapCache használata további szerverkonfigurációt igényel; lásd a MapServer dokumentációját. |
| `MAP` | `PMAP` | A projekt által használt térképobjektum neve. |
| `PRIVATE_MAPFILE` | `private.map` | A projekt által használt privát MapServer-mapfile. Ez a beállítás kompatibilitási okokból maradt meg, és egy későbbi verzióban átkerülhet a PostgreSQL-ben kezelt projektbeállítások közé. |

Csak egyetlen `MAPSERVER` értéket állítson be. A helyes érték attól függ, hogy
a MapServer helyben vagy külön Docker-szolgáltatásként fut-e.

## Meghívók

| Változó | Példaérték | Leírás |
| --- | --- | --- |
| `INVITATIONS` | `0` | Az egy felhasználóhoz egyidejűleg tartozó aktív meghívók maximális száma. Ha az érték `0`, csak az adminisztrátorok küldhetnek meghívókat. A dokumentált alapértelmezett érték `11`. |

## Levelezési beállítások

Ezek az opcionális beállítások akkor használhatók, ha nem áll rendelkezésre
megfelelő helyi levéltovábbító ügynök.

| Változó | Példaérték | Leírás |
| --- | --- | --- |
| `SMTP_AUTH` | `true` | Engedélyezi az SMTP-hitelesítést. |
| `SMTP_HOST` | `mail.your-smtp-server.org` | Az SMTP-szerver állomásneve. |
| `SMTP_USERNAME` | `MAIL USER` | Az SMTP-szerveren történő hitelesítéshez használt felhasználónév. |
| `SMTP_PASSWORD` | `xxxxxx` | SMTP-jelszó. Tartsa titokban, és ne véglegesítse a kódtárolóba. |
| `SMTP_PORT` | `PORT-NUMBER` | Az SMTP-szerver portja. Válassza ki a szerver titkosítási és hitelesítési konfigurációjának megfelelő portot. |
| `SMTP_SENDER` | `mail_user@your-smtp-server.org` | A projekt kimenő leveleihez használt feladói cím. |
| `SMTP_SECURE` | `tls` | Opcionális SMTP-átvitelbiztonsági mód. |

Egy korábbi Google SMTP-példa a következő értékeket használta:

| Változó | Korábbi példaérték |
| --- | --- |
| `SMTP_HOST` | `smtp.gmail.com` |
| `SMTP_USERNAME` | `your-user@gmail.com` |
| `SMTP_PASSWORD` | `xxxxxxxxx` |
| `SMTP_SECURE` | `tls` |
| `SMTP_PORT` | `587` |

Előfordulhat, hogy a korábbi Google-példa további szolgáltatói konfiguráció
nélkül már nem működik, ezért nem szabad lemásolni a Google aktuális
hitelesítési követelményeinek ellenőrzése nélkül.

A következő, levelezéshez kapcsolódó beállítások elavultak, ezért új
projektekhez nem használhatók:

| Változó | Példaérték | Leírás |
| --- | --- | --- |
| `SHINYURL` | `false` | Elavult Shiny URL-beállítás. |
| `RSERVER` | `false` | Elavult R-szerver-beállítás. |

## Bejelentkezés után megjelenő oldal

| Változó | Példaérték | Leírás |
| --- | --- | --- |
| `LOGINPAGE` | `map` | A bejelentkezés után betöltődő oldal. A dokumentált támogatott lehetőségek: `profile`, `mainpage` és `map`. Az alapértelmezett érték `map`. |
| `TRAINING` | `false` | Elavult oktatási mód beállítás. Új projektekhez ne használja. |

## Főoldal-konfiguráció

A `MAINPAGE` a projekt főoldalának elrendezését és tartalmát szabályozó
beállításokat foglalja csoportba.

| Kulcs | Példaérték | Leírás |
| --- | --- | --- |
| `template` | `gridbox` | Főoldalsablon. Az `intropage` egy másik dokumentált sablonérték. |
| `content1` | `map` | Az első fő terület tartalma. A dokumentált értékek közé tartozik a `map`, az `upload-table` és a `slideshow`. |
| `sidebar1` | `column_dinpi.altema\|custom_countries\|members\|uploads\|data\|species\|species_stat` | Az oldalsáv összetevőinek függőleges vonallal elválasztott listája. A gyakori összetevők közé tartozik a `members`, az `uploads`, a `data`, a `species` és a `species_stat`; projektspecifikus összetevők is megadhatók. |
| `system_footer` | `on` | `on` érték esetén megjeleníti a rendszer láblécét. |
| `system_header` | `off` | `off` érték esetén elrejti a rendszer fejlécét. |
| `custom_skeleton` | `1` | Opcionális egyéni oldalváz-választó. A példakonfigurációban le van tiltva. |
| `restrictaded_pages` | `map`, `id`, `history`, `profile`, `data`, `table`, `editrecord`, `qtable`, `query`, `show`, `LQ`, `metadata` | A korlátozás alá eső oldalak opcionális listája. A kulcs az alkalmazással való kompatibilitás érdekében `restrictaded_pages` alakban szerepel. A példakonfigurációban le van tiltva. |

A projektspecifikus oldalsáv-összetevőknek létezniük kell, és megfelelően be
kell állítani őket, mielőtt hozzáadná őket a `sidebar1` értékéhez.

## Docker-projekttartomány

| Változó | Példaérték | Leírás |
| --- | --- | --- |
| `OB_PROJECT_DOMAIN` | Az `OB_DOMAIN` értéke | Docker-specifikus projekttartomány, amelyet az új feltöltésekről szóló e-mailes értesítések létrehozásakor használ a rendszer. Az érték a rendszerszintű `OB_DOMAIN` beállításból öröklődik. |

## Stíluskonfiguráció

A `STYLE` választja ki a projekt stílusát.

| Kulcs | Példaérték | Leírás |
| --- | --- | --- |
| `template` | `evolvulus` | A projekt által használt stílus- vagy sablonkönyvtár neve. A megnevezett stílusnak telepítve kell lennie. |

## Lábléc-konfiguráció

A `FOOTER` a projekt láblécében megjelenő hivatkozásokat, nyelvválasztót és
partnerlogókat szabályozza.

| Kulcs | Példaérték | Leírás |
| --- | --- | --- |
| `links` | `map\|upload\|about\|terms\|usage\|privacy` | A lábléc hivatkozásainak függőleges vonallal elválasztott listája. |
| `languages` | `languages` | Engedélyezi vagy azonosítja a lábléc nyelvválasztóját. |
| `partners` | OpenBioMaps- és University of Debrecen-bejegyzések | A partnerlogók definícióinak listája. |

A `partners` minden eleme a következő mezőket tartalmazhatja:

| Mező | Példaérték | Leírás |
| --- | --- | --- |
| `img` | `obm_logo.png` | A partnerhez megjelenített kép fájlja. |
| `size` | `110` | Opcionális megjelenítési méret. Üres érték esetén nincs meghatározva a méret. |
| `url` | `https://openbiomaps.org` | A partnerlogóról megnyitott cél-URL. |

A példakonfiguráció a következő partnereket tartalmazza:

| Kép | Méret | URL |
| --- | --- | --- |
| `obm_logo.png` | `110` | `https://openbiomaps.org` |
| `unideb_logo.png` | üres | `https://unideb.hu` |

## Fejléc-konfiguráció

A `HEADER` a projekt fejlécének hivatkozásait és elrendezését szabályozza.

| Kulcs | Példaérték | Leírás |
| --- | --- | --- |
| `links` | `upload\|map\|messages\|profile\|localize` | A fejlécben megjelenített hivatkozások függőleges vonallal elválasztott listája. |
| `layout` | `obm` | A projekt által használt fejléc-elrendezés. |

## Titkosítási hash

| Változó | Példaérték | Leírás |
| --- | --- | --- |
| `MyHASH` | `password-string` | Az olyan modulok által használt titkos érték, mint a `read_table`, amely a táblanevek és a kapcsolódó értékek titkosítására vagy elfedésére szolgál. Cserélje le erős, véletlenszerű értékre, egy meglévő projektben tartsa változatlanul, és ne tegye közzé. |

A `MyHASH` módosítása egy meglévő projektben érvénytelenítheti a régi titkos
értékkel korábban létrehozott értékeket.

## Egyéni gyorsítótár-beállítások

| Változó | Példaérték | Leírás |
| --- | --- | --- |
| `CACHE_HOST` | A `CACHE_HOST` környezeti változó értéke, egyébként `localhost` | A gyorsítótár-szolgáltatást futtató állomás. |
| `CACHE_PORT` | A `CACHE_PORT` környezeti változó értéke, egyébként `11211` | A gyorsítótár-szolgáltatás portja. A Memcached általánosan használt portja az `11211`. |

Docker-telepítésben a `localhost` helyett a gyorsítótár-szolgáltatás nevét
használja, ha a gyorsítótár másik konténerben fut.

## OpenID Connect-bejelentkezés

Az `OPENID_CONNECT` egy vagy több identitásszolgáltató definícióját
tartalmazza. A példa a Google szolgáltatást állítja be.

| Szolgáltató/kulcs | Példaérték | Leírás |
| --- | --- | --- |
| Szolgáltató neve | `google` | Az OpenID Connect-szolgáltató belső azonosítója. |
| `client_id` | `xxxxx.apps.googleusercontent.com` | A szolgáltató által kiadott kliensazonosító. |
| `client_secret` | `xxxxxxx` | A szolgáltató által kiadott klienstitok. Tartsa titokban, és ne véglegesítse a kódtárolóba. |
| `provider_url` | `https://accounts.google.com/` | Az OpenID Connect-szolgáltató alap-URL-je. |
| `OPENID_CONNECT_CERT_PATH` | `/etc/ssl/certs/ca-certificates.crt` | A szolgáltatóval létesített TLS-kapcsolatok ellenőrzéséhez használt megbízható CA-tanúsítványcsomag elérési útja. |

Regisztrálja a szolgáltatónál a pontos OpenBioMaps-átirányítási URI-t, és
ellenőrizze, hogy az alkalmazás képes-e olvasni a beállított
CA-tanúsítványcsomagot.

## PWA-hivatkozás

| Változó | Példaérték | Leírás |
| --- | --- | --- |
| `PWA_LINK` | `on` | Engedélyezi a Progressive Web App hivatkozását a projekt főoldalán. |

## Egyéni oldalak

| Változó | Példaérték | Leírás |
| --- | --- | --- |
| `CUSTOM_PAGES` | `mysite`, `my_other_site` | A projektben elérhető egyéni oldalazonosítók listája. Minden hivatkozott egyéni oldalt meg kell valósítani a projekt megfelelő helyén. |

## Mellékletként feltöltött képek mérete

| Változó | Példaérték | Leírás |
| --- | --- | --- |
| `ALLOWED_FILE_SIZE` | `4194304` | A képmellékletek legnagyobb engedélyezett mérete bájtban. A példaérték 4 MiB. |

A tényleges feltöltési korlátot a PHP, a webszerver, a fordított proxy vagy
más infrastruktúra-beállítások is korlátozhatják.

## Ideiglenes táblák megfigyelési listák feltöltéséhez

| Változó | Példaérték | Leírás |
| --- | --- | --- |
| `USE_TEMPTABLES_FOR_OBSLISTS` | `true` | Engedélyezi a `temporary_tables.obs_*` mintájú táblák használatát megfigyelési listák feltöltésekor. A dokumentált konfigurációban ez az érték a `true` karakterláncként, nem pedig logikai értékként van tárolva. |

Az adatbázis-felhasználónak rendelkeznie kell az ideiglenes táblák sémájához
szükséges jogosultságokkal.

## Háttérben végzett adatexportálás

| Változó | Példaérték | Leírás |
| --- | --- | --- |
| `DATA_EXPORT_BGPROC_LIMIT` | `1000` | Az a rekordszám, amely felett az adatexportálás közvetlen letöltés helyett háttérfeladatként kerül feldolgozásra. |

A háttérben végzett exportálásokhoz be kell állítani és futtatni kell a
projekt feladatfuttatóját.

## További projektsémák

| Változó | Példaérték | Leírás |
| --- | --- | --- |
| `PROJECT_SCHEMAS` | `sablon_archive` | A projekthez társított további PostgreSQL-sémák listája. |

Győződjön meg arról, hogy a projekt adatbázis-felhasználója minden felsorolt
sémához rendelkezik a szükséges jogosultságokkal.

## Biztonsági és automatizáltkérés-ellenőrzések

Ezek a beállítások Redis-alapú kérésgyakorisági ellenőrzéseket engedélyeznek.
A meghatározott korlátok túllépésekor az OpenBioMaps támadásvédelmi módba
léphet, és a beállított időtartamra megjeleníthet egy „Ön ember?” ellenőrzést.

| Változó | Példaérték | Leírás |
| --- | --- | --- |
| `SECURITY_CHECK` | `true` | Engedélyezi a biztonsági ellenőrzést. |
| `REDIS_HOST` | `127.0.0.1` | A Redis-szerver állomása. A dokumentált alapértelmezett érték `127.0.0.1`. Docker használatakor a Redis szolgáltatásnevét használja, ha a Redis másik konténerben fut. |
| `REDIS_PORT` | `6379` | A Redis-szerver portja. A dokumentált alapértelmezett érték `6379`. |
| `SECURITY_IP_LIMIT` | `30` | Egyetlen IP-címről 10 másodpercenként engedélyezett kérések maximális száma. Az IP-címenkénti ellenőrzés letiltásához állítsa `false` értékre. A dokumentált alapértelmezett érték `30`. |
| `SECURITY_GLOBAL_LIMIT` | `10` | Az összes kérés maximális gyakorisága másodpercenként. A dokumentált alapértelmezett érték `10`. |
| `SECURITY_ATTACK_TTL` | `600` | Az az idő másodpercben, ameddig a támadásvédelmi mód aktív marad. A dokumentált alapértelmezett érték `600` másodperc. |

A korlátokat a várható forgalom, a proxykonfiguráció és az azonos látszólagos
forrás-IP-címet használó felhasználók száma alapján válassza ki. Ha az
OpenBioMaps fordított proxy mögött található, ellenőrizze, hogy az alkalmazás
a megfelelő kliens-IP-címeket kapja-e meg.

## Fejlesztői beállítások

Ezek a beállítások normál éles használat helyett fejlesztéshez és
hibaelhárításhoz készültek.

| Változó | Példaérték | Leírás |
| --- | --- | --- |
| `branch` | `testing` | Másik Git-ágat, például a tesztelési ágat választja ki. Az éles projekteknek általában a támogatott éles ágat kell használniuk. |
| `DEBUG_PDS` | `true` | További naplózást engedélyez a PDS-műveletekhez. A hibaelhárítás után tiltsa le a részletes hibakeresési naplózást, mert növelheti a naplók méretét, vagy bizalmas üzemeltetési adatokat tehet hozzáférhetővé. |

Egy fejlesztői beállítás engedélyezése után figyelje az alkalmazásnaplókat,
és állítsa vissza a beállítást, amikor már nincs rá szükség.
