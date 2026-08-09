# Virtuális szerver Docker használatával

Ez az OpenBioMaps jelenleg támogatott és naprakész virtuáliskörnyezet-kiadása.

Teszteléshez, fejlesztéshez és éles környezetben egyaránt megfelelő.

Az obm-docker használatához négy lépés szükséges:

1. A docker-compose telepítése.
2. Az obm-docker lemezkép beszerzése.
3. A Docker konfigurálása a gazdagép sajátosságainak megfelelően, például SSL és SMTP használatához.
4. A Docker-környezet elindítása.


## A Docker és a Compose előkészítése és telepítése

```console
sudo curl -L https://github.com/docker/compose/releases/download/1.29.2/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose

docker-compose --version
```

docker-compose version 1.29.2, build f46880fe

A Docker telepítésével kapcsolatos további információért keresse fel ezt az
oldalt:

[https://docs.docker.com/compose/install/](https://docs.docker.com/compose/install/)


## OpenBioMaps-példány telepítése és beállítása

Egyetlen lépésben:

``curl -s https://gitlab.com/openbiomaps/docker/obm-composer/-/raw/master/install.sh > /tmp/install.sh && sudo bash /tmp/install.sh``

## Az OpenBioMaps-alkalmazás megnyitása

[http://YOUR_SERVER_NAME:9080/](http://YOUR_SERVER_NAME:9080/)

[http://YOUR_SERVER_NAME:9080/projects/sablon/](http://YOUR_SERVER_NAME:9080/projects/sablon/)

Jelentkezzen be a sablonadatbázisba a *valaki@openbiomaps.org*
felhasználónévvel és az *abc123* jelszóval. Az első bejelentkezést követően
változtassa meg ezt az alapértelmezett jelszót.

Ha a Dockert a helyi számítógépére telepítette, a fenti szolgáltatások
localhost használatával érhetők el.

A szerver és a sablonprojekt frissítéséhez kövesse ezt az útmutatót:

:doc:Új szerver telepítési útmutató <../server_install>


## Adatbázis-hozzáférés

A PostgreSQL-adatbázis az alábbi előre konfigurált online
adatbázis-kezelő alkalmazásokon keresztül érhető el. Ez azonban a gazdagép
és a Docker közötti kapcsolattól is függ.

A PhpPgAdmin jelenleg nem érhető el.

*PhpPgAdmin: [http://YOUR_SERVER_NAME:9881/](http://YOUR_SERVER_NAME:9881/)*

  Megjegyzések a PhpPgAdmin használatához:

  Nagyon felhasználóbarát eszköz, jelenleg azonban nincs karbantartva, ezért
  saját kiadást kell létrehoznunk, vagy meg kell várnunk, amíg valaki más
  elkészíti.

Adminer: [http://YOUR_SERVER_NAME:9882/](http://YOUR_SERVER_NAME:9882/)

  Megjegyzések az Adminer használatához:

    server = openbiomaps_biomaps_db_1
    db_name = biomaps | gisadmin
    db_user = biomapsadmin | sablon_admin | YOUR_PROJECT_admin
    password = (check the .env file for the biomapsadmin's password or the local_vars.php.inc for ..._admin's password)

Az adatbázis a *biomapsadmin* felhasználóval kezelhető. Ez egy
szuperfelhasználó. Jelszavát a rendszer a telepítés során hozza létre, és a
/srv/docker/openbiomaps/.env fájlban található.

A MapServer mapfile adatbázis-kapcsolatához szükséges titkosított jelszó a
/var/lib/openbiomaps/maps/access.key fájllal hozható létre.

Az OpenBioMaps alapértelmezés szerint két adatbázist hoz létre. A
``biomaps`` a rendszer működéséhez szükséges táblákat tartalmazza, míg a
``gisdata`` a projektadatbázisok adattábláit tartalmazza. Más szóval az
utóbbi tárolja a felhasználók által gyűjtött adatokat, és ehhez
kapcsolódhatnak a felhasználók. A ``biomapsadmin`` mindkét adatbázisban
szuperfelhasználó. Jelszavát a rendszer a telepítés során hozza létre, és a
/srv/docker/openbiomaps/.env fájlban tárolja.

## Docker-karbantartó alkalmazás

Ez a lépés nem kötelező, de hasznos lehet, ha hatékony webes
adminisztrációs felületre van szüksége a Docker kezeléséhez.

```
mkdir -p /srv/docker/portainer && cd /srv/docker/portainer

git clone https://gitlab.com/openbiomaps/docker/obm-portainer.git .

sudo su

docker-compose pull

# Genereate a strong random password for the admin user
bash ./password_gen.sh

docker-compose up -d

On the portainer interface use the "Get started" button...

```

Nyissa meg a Docker-adminisztrációs Portainer alkalmazást:

[http://YOUR_SERVER_NAME:9000/](http://YOUR_SERVER_NAME:9000/)

Jelentkezzen be az alkalmazásba az *admin* felhasználónévvel és a
jelszavával.

Ha a Dockert a helyi számítógépére telepítette, az alkalmazás localhost
használatával érhető el.


## OpenBioMaps-karbantartás: Supervisor

Az OpenBioMaps szerveradminisztrációs felülete itt érhető el:

[http://localhost:9880/supervisor.php](http://localhost:9880/supervisor.php)

vagy:

[https://yourserver.com/supervisor.php](https://yourserver.com/supervisor.php)

A bejelentkezéshez használja a *supervisor* felhasználónevet és az
``obm_post_install.sh`` által létrehozott jelszót. Ez a jelszó az
/etc/openbiomaps/.htpasswd fájlban található.

A Supervisor jelszava az ``./obm_post_install.sh update supervisor``
paranccsal hozható létre újból.


## Frissítések: az alkalmazás frissítése Docker használatával

Ezek a parancsok biztonságosak, és nem törlik az OpenBioMaps webes
felületén végzett módosításokat.

```console
foo@bar:~$ docker-compose pull 
Pulling biomaps_db ... done
Pulling mapserver  ... done
Pulling app        ... done
## Pulling phppgadmin ... done -- There is no PhpPgAdmin currently 
Pulling adminer    ... done

foo@bar:~$ docker-compose up -d
Creating obm-composer_biomaps_db_1 ... done
Creating obm-composer_mapserver_1  ... done
Creating obm-composer_adminer_1    ... done
## Creating obm-composer_phppgadmin_1 ... done
Creating obm-composer_app_1        ... done
```

Csak egy konténer frissítése:

```console
foo@bar:~$ docker-compose up -d app
```

## A projektek e-mail-beállításai

Az alkalmazásból történő e-mail-küldéshez **be kell állítani egy
levelezőszerver elérését**.

Feltételezve, hogy az új szerver nem rendelkezik saját tartománynévvel, az
alapértelmezett levélküldési érték SMTP-re van állítva az
/etc/openbiomaps/system_vars.php.inc fájlban. Ehhez minden projekthez be
kell állítani a kimenő SMTP-szervert és a kapcsolódó hitelesítést a
/var/www/html/biomaps/projects/.../local_vars.php.inc fájlban.

Ezek a konfigurációs fájlok a Supervisor felületén szerkeszthetők.

Keresse meg a levelezési beállításokat, és szükség esetén állítsa be az
SMTP-gazdagépet és a hitelesítést.

Példa külső SMTP-szerver használatára:

```console
 // Mail settings
 define('SMTP_AUTH',true); # true
 define('SMTP_HOST','mail.my-mail-server.com');
 define('SMTP_USERNAME','my-name@my-mail-server.com');
 define('SMTP_PASSWORD','something');
 define('SMTP_SECURE','tls'); # Or starttls
 define('SMTP_PORT','587'); # 465
 define('SMTP_SENDER','openbiomaps@my-mail-server.com');
```

Ha az ``SMTP_SENDER`` nincs beállítva, az ``SMTP_USERNAME`` lesz a feladó.
A Google használatával ezek az egyszerű beállítások nem elegendők
levélküldéshez, mert a Google XOAUTH-réteget használ a hitelesítéshez. Ez a
réteg itt is hozzáadható.

Ha a gazdagép maga az SMTP-szerver:

```console
 // Mail settings
define('SMTP_AUTH',false);
define('SMTP_HOST','172.17.0.1');
define('SMTP_PORT','25');
define('SMTP_SENDER','info@you-smtp-server');
```

A fenti IP-címet ellenőrizze a gazdagépen az ``ip addr | grep docker0``
paranccsal.

A gazdagépen használt MTA-tól függően az alábbi példák használhatók.

### Exim4

Az /etc/exim4/update-exim4.conf fájlban:

 dc_relay_nets='172.21.0.0/16'
 
 dc_local_interfaces='127.0.0.1 ; ::1 ; 172.17.0.1' 

Ezeket a sorokat frissíteni kell, de az Exim konfigurációjától függően más
módosításra is szükség lehet.

Az /etc/exim4/exim4.config fájlban:

A ``hostlist relay_from_hosts...`` sort ki kell egészíteni az ``obm_back``
hálózattal, például:

  hostlist   relay_from_hosts = localhost :172.20.0.0/16 :172.17.0.0/16 :172.21.0.0/16

Megjegyzés: lehetséges, hogy a fenti három hálózat közül egy is elegendő;
ez még nincs tesztelve.

### Postfix

inet_interfaces = 172.17.0.1

mynetworks = 172.21.0.4 172.20.0.6

A Docker-hálózatok és IP-címek a következőképpen deríthetők ki:

```console
docker container ls
```

Keresse meg az ``obm-composer_app_1`` konténert.

```console
docker inspect xxxxx_obm-composer_app_1
```

Keresse meg az ``obm_back`` és az ``obm_web`` interfészeket:

  obm-composer_obm_back {
  
  ...
  
  "IPAddress": "172.20.0.6",
  
  }
  
  obm-composer_obm_web {
  
  ...
  
  "IPAddress": "172.21.0.4",
  
  }

### Tűzfal

A tűzfalat is frissíteni kellhet, hogy engedélyezze a lemezképből a
gazdagépre érkező leveleket. Az ``obm_back`` hálózati címét engedélyezni
kell bejövő hálózatként a tűzfalon. Például:

```console
ufw allow from 172.20.0.0/16 proto tcp to any port 25
```

### Globális SMTP-beállítások

Valószínűleg ugyanazokat az SMTP-beállításokat szeretné használni a szerver
összes projektjéhez. Ebben az esetben használja a következő paramétereket a
``system_vars.php.inc`` fájlban:

   - SMTP_GLOBAL_HOST
   - SMTP_GLOBAL_AUTH
   - SMTP_GLOBAL_USERNAME
   - SMTP_GLOBAL_PASSWORD
   - SMTP_GLOBAL_SECURE
   - SMTP_GLOBAL_PORT
   - SMTP_GLOBAL_SENDER

Ha globális paramétereket szeretne használni, legalább az
``SMTP_GLOBAL_HOST`` értékét be kell állítani. A helyi paraméterek mindig
felülírják a globálisakat.


## SSL- és HTTPS-hozzáférés beállítása – erősen ajánlott

Előfordulhat, hogy frissíteni kell a projekt hozzáférési protokollját a
Supervisor felületén, ez azonban a gazdagép beállításaitól függ.

*A gazdagépen nincs webszerver, de a gazdagép biztosítja az SSL-tanúsítványokat a Docker számára*

Az egyik lehetséges megoldás a gazdagép SSL-tanúsítványainak használata úgy,
hogy a szükséges könyvtárakat a gazdagépről a Dockerbe csatolja.

Let’s Encrypt-tanúsítvány létrehozása:

``` console
apt install dehydrated
vi /etc/dehydrated/domain.txt
    YOURDOMAIN
dehydrated -c
```

docker-compose.yml:

```console
services:
  app:
    image: registry.gitlab.com/openbiomaps/web-app:latest
    volumes:
      ...
      - /etc/letsencrypt/YOURDOMAIN:/etc/apache2/certs
      - ./apache2/default-ssl.conf:/etc/apache2/sites-enabled/default-ssl.conf
    ports:
     - 80:80
     - 443:443
    ... 
```

*A gazdagép webszervert futtat, és proxyt biztosít a Docker számára*

Egy másik lehetőség a gazdagép Apache proxyjának használata.

Gazdagép: /etc/apache2/sites-enabled/000-default.conf

```
RedirectMatch permanent ^(?!/.well-known/.*) https://YOURDOMAIN/
```

Gazdagép: /etc/apache2/sites-enabled/default-ssl.conf

```
RequestHeader set X-Forwarded-Proto 'https'
RequestHeader set X-Forwarded-Host 'YOURDOMAIN'
RequestHeader set X-Forwarded-Port "443"

ProxyPass /.well-known !
ProxyPass / 
http://localhost:8090/

ProxyPassReverse / 
http://localhost:8090/

ProxyPreserveHost On
<Proxy *>
allow from all
</Proxy> 
```

docker-compose.yml:

```console
services:
  app:
  ...
      ports:
      - 80:8090
  ...
```

Ebben az esetben nem szükséges HTTPS-protokollt használni a projekt
beállításaiban, mert az OpenBioMaps a HTTP ``X-FORWARD`` beállítások alapján
felismeri a HTTPS-kérést.


*Traefik használata a különböző tartományokra érkező kérések Docker-szintű feldolgozásához, például ha több Docker-konténer fut a gazdagépen*

Docker-alapú HTTPS-forgalomirányító beállításához a Traefik 2.x használatát
javasoljuk egy külön konténerben:

https://gitlab.com/openbiomaps/docker/traefik2.0-proxy

A Traefikkel való kommunikációhoz frissítse a docker-compose.yml fájlt:

```console
networks:
   traefik20_default:
    external: true 
  #obm_web:
  #  external: true

services:
  app:
  ....
# Do not use ports, traefik provides them!!!
#    ports:
#      - 80:80
#      - 443:443
    networks:
      - obm_back
      #- obm_web
      - traefik20_default
    labels:
      - traefik.enable=true
      - traefik.docker.network=traefik20_default
      - traefik.http.routers.obm-secured.rule=Host(`YOUR_DOMAIN`)
      - traefik.http.routers.obm-secured.entrypoints=https
      - traefik.http.routers.obm-secured.middlewares=hsts@file
      - traefik.http.routers.obm-secured.tls.certresolver=letsencrypt
      - "traefik.http.middlewares.obm-biotika-redirect.redirectregex.regex=^https?://biotika.YOURDOMAIN(.*)"
      - "traefik.http.middlewares.obm-biotika-redirect.redirectregex.replacement=https://YOUR_DOMAIN/projects/YOURPROJECT/"
      - traefik.http.middlewares.obm-biotika-redirect.redirectregex.permanent=true
  
  phppgadmin:
  ...
    networks:
        #- obm_web
      - obm_back
      - traefik20_default
    labels:
      - "traefik.enable=true"
      - "traefik.docker.network=traefik20_default"
      - "traefik.http.routers.obm-pgadmin.rule=Host(`phppgadmin.YOURDOMAIN`)"
      - "traefik.http.routers.obm-pgadmin.entrypoints=https"
      - "traefik.http.routers.obm-pgadmin.tls.certresolver=letsencrypt"
      - "traefik.http.services.obm-pgadmin.loadbalancer.server.port=8080"
volumes:
  ...
    traefik20_letsencrypt:
    external: true
```

Ez az utóbbi példa még nem feltétlenül teljes.

Ha PostgreSQL-hozzáférést biztosít, SSL-t is be kell állítani a PostgreSQL
kapcsolatához.

Traefik használata esetén az SSL-hozzáférés ott konfigurálható. Más esetben
SSL-tanúsítványokat adhat az adatbázis-konténernek, és beállíthatja a
PostgreSQL rendszert úgy, hogy kizárólag SSL-en keresztül fogadjon
kapcsolatokat.

docker-compose.yml:

```console
services:
...
  biomaps_db:
     volumes:
       - /PATH_TO_CERTS/ssl.cert:/etc/ssl/certs/YOURDOMAIN.cert
       - /PATH_TO_CERTS/ssl.key:/etc/ssl/certs/YOURDOMAIN.key
       - ./postgresql.conf:/var/lib/postgresql/data/postgresql.conf 
       - ./pg_hba.conf:/var/lib/postgresql/data/pg_hba.conf 
```

A ``biomaps_db`` konténerben:

/..../pg_hba.conf:

```console
hostssl all all all md5 
```

/..../postgres.conf:

```console
ssl = on
ssl_cert_file = '/etc/ssl/certs/YOURDOMAIN.cert'
ssl_key_file = '/etc/ssl/certs/YOURDOMAIN.key' 
```

A PostgreSQL-kapcsolat SSL nélkül a következőképpen tesztelhető:

```console
psql "postgresql://gisadmin@YOURDMAIN:5432/gisdata?sslmode=disable"
```

Ha az SSL megkövetelése megfelelően működik, ehhez hasonló hibaüzenet
jelenik meg:

psql: FATAL:  no pg_hba.conf entry for host "xxxxxxx", user "gisadmin", database "gisdata", SSL off


## Docker-karbantartás

### A Docker leállítása

```console
foo@bar:~$ docker-compose down
```

### Minden törlése, beleértve az adatokat és adatbázisokat is

```console
foo@bar:~$ docker-compose down -v
```


### Parancsértelmező elérése a konténer lemezképében

```console
foo@bar:~$ docker-compose exec app bash
```

Itt az **app** szolgáltatást nyitottuk meg. A szolgáltatások nevei a
docker-compose.yml fájlban találhatók.


### Naplók olvasása

```console
foo@bar:~$ docker-compose logs -f app
```

### A pg_top használata

docker-compose exec -u postgres <service_name> pg_top

### Az alkalmazás újraindítása

Ne indítsa újra az Apache szervert a Docker parancsértelmezőjéből, hanem a
konténeren kívülről:

```console
foo@bar:~$ docker-compose restart app
```

### Nagy mennyiségű régi, használaton kívüli Docker-lemezkép eltávolítása

Sok ilyen lemezkép van?

```console
docker images | grep "<none>"
```

Töröljük őket:

```console
docker images | grep "<none>" | awk '{print $3}' | sed -e 's/^/docker rmi /' | bash
```

Előfordulhat, hogy szerkesztenie kell a ``traefik2.0/traefik.yml``,
``traefik2.0/docker-compose.yml`` és ``traefik2.0/acme.json`` fájlokat.

### A Docker automatikus frissítése

https://github.com/OpenBioMaps/scripts/blob/master/docker-auto-update.readme

## Táblák, adatok és más erőforrások archiválása

A parancsfájlok ebben a repository-ban találhatók:

https://github.com/OpenBioMaps/scripts

- Az ``archive.sh`` használatával rendszeres SQL-adatmentés állítható be a fontos táblákhoz.

### Példák az archive.sh crontab-beállításaira

```sh
   #dumping normal tables from Monday to Saturday
   15 04 * * 1-6 /root/archive.sh normal &
   #dumping all tables and whole databases on every Sunday
   15 04 * * 7 /root/archive.sh full &
```

### Példabeállítások az obm_archive_settings.sh fájlban

```sh
  #path of table list
  table_list="${HOME}/.archive_list.txt"

  #postgres parameters
  project_database="gisdata"
  system_database="biomaps"
  admin_user="gisadmin"
  archive_path="/home/archives"
  pgport="5432"
  pg_dump="pg_dump -p $pgport"
  psql="psql -p $pgport"

  #FOR DOCKER based OBM systems
  #docker="/usr/bin/docker-compose -f /path/to/docker-compose.yml exec -T"
  #pg_dump="$docker biomaps_db pg_dump -p $pgport"
  #psql="$docker biomaps_db psql -p $pgport"
  
  #table dayof_week dayofmonth month
  #foo at every day
  #foo * * *
  #bar every Monday
  #bar 1 * *
  #casbla at every 1st day of every June
  #casbla * 1 6
```

### Tábla mentése az adatbázisból Docker használatával

docker-compose exec -T biomaps_db bash -c "pg_dump -U biomapsadmin --table public.YOUR_TABLE gisdata" > YOUR_TABLE.sql



## Erőforrások

* https://gitlab.com/openbiomaps/web-app
* https://gitlab.com/openbiomaps/docker/obm-composer
