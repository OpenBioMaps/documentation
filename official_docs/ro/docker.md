
# Server virtual cu Docker

Aceasta este versiunea actualizată și acceptată în prezent a mediului virtual OpenBioMaps.

Este adecvată atât pentru testare și dezvoltare, cât și pentru utilizarea într-un mediu de producție.

Pentru utilizarea obm-docker sunt necesari 4 pași:
1. Instalați docker-compose
2. Obțineți imaginea obm-docker
3. Configurați Docker în funcție de particularitățile gazdei (de exemplu, SSL, SMTP)
4. Porniți mediul Docker


## Pregătirea/instalarea Docker și Compose

```console
sudo curl -L https://github.com/docker/compose/releases/download/1.29.2/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose

docker-compose --version
```
docker-compose version 1.29.2, build f46880fe


Pentru mai multe informații despre instalarea Docker, vizitați această pagină:

[https://docs.docker.com/compose/install/](https://docs.docker.com/compose/install/)


## Instalarea/configurarea unei instanțe OpenBioMaps

Într-un singur pas:

``curl -s https://gitlab.com/openbiomaps/docker/obm-composer/-/raw/master/install.sh > /tmp/install.sh && sudo bash /tmp/install.sh``

## Accesarea aplicației OBM

[http://YOUR_SERVER_NAME:9080/](http://YOUR_SERVER_NAME:9080/)

[http://YOUR_SERVER_NAME:9080/projects/sablon/](http://YOUR_SERVER_NAME:9080/projects/sablon/)

Autentificați-vă în baza de date șablon folosind numele de utilizator *valaki@openbiomaps.org* și parola *abc123*. După prima autentificare, modificați această parolă implicită!

Dacă ați instalat Docker pe calculatorul local, puteți accesa serviciile de mai sus prin localhost.

Actualizați serverul și proiectul sablon urmând acest ghid:

:doc:`Tutorial pentru instalarea unui server nou <../server_install>`


## Accesul la baza de date

Puteți accesa baza de date Postgres prin următoarele aplicații online preconfigurate pentru administrarea bazelor de date. Totuși, acest lucru depinde de relația dintre gazdă și Docker.

!PhpPgAdmin nu este disponibil în prezent!

*Phppgadmin: [http://YOUR_SERVER_NAME:9881/](http://YOUR_SERVER_NAME:9881/)*

  Observații privind PhpPgadmin:
  
  Este un instrument foarte ușor de utilizat, dar, din păcate, nu mai este întreținut în prezent, așadar trebuie să ne creăm propria ediție sau să așteptăm ca altcineva să o facă...

Adminer: [http://YOUR_SERVER_NAME:9882/](http://YOUR_SERVER_NAME:9882/)

  Observații privind Adminer:
  
    server = openbiomaps_biomaps_db_1
    db_name = biomaps | gisadmin
    db_user = biomapsadmin | sablon_admin | YOUR_PROJECT_admin
    password = (check the .env file for the biomapsadmin's password or the local_vars.php.inc for ..._admin's password)

Puteți administra baza de date cu utilizatorul *biomapsadmin*. Acesta este un superutilizator. Parola sa este generată de sistem în timpul instalării și poate fi găsită în fișierul /srv/docker/openbiomaps/.env.

Pentru fișierul mapfile MapServer, parola criptată pentru conexiunea la baza de date poate fi generată cu /var/lib/openbiomaps/maps/access.key.

OpenBioMaps creează implicit două baze de date. Baza de date „biomaps” conține tabelele necesare funcționării sistemului, iar „gisdata” conține tabelele de date ale bazelor de date ale proiectelor. Cu alte cuvinte, în cea din urmă vor fi stocate datele colectate de utilizatori și la aceasta se pot conecta utilizatorii. „biomapsadmin” este un superutilizator în ambele baze de date. Parola sa este generată de sistem în timpul instalării și este stocată în fișierul /srv/docker/openbiomaps/.env.

## Aplicație pentru întreținerea Docker

Acest pas nu este obligatoriu, dar poate fi util dacă aveți nevoie de o interfață web de administrare complexă pentru gestionarea Docker. 

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

Accesați aplicația de administrare Docker (Portainer)

[http://YOUR_SERVER_NAME:9000/](http://YOUR_SERVER_NAME:9000/)

Autentificați-vă în aplicație folosind numele de utilizator *admin* și parola dumneavoastră.

Dacă ați instalat Docker pe calculatorul local, puteți accesa serviciile de mai sus prin localhost.


## Întreținerea OBM: Supervisor

Puteți accesa interfața de administrare a serverului OBM la: 
[http://localhost:9880/supervisor.php](http://localhost:9880/supervisor.php)

sau 

[https://yourserver.com/supervisor.php](https://yourserver.com/supervisor.php)

cu numele de utilizator *supervisor* și parola creată de obm_post_install.sh. Această parolă se află în /etc/openbiomaps/.htpasswd.

Puteți regenera parola pentru Supervisor cu comanda `./obm_post_install.sh update supervisor`.


## Actualizări: actualizarea aplicației cu Docker
Aceste comenzi sunt sigure și nu distrug modificările efectuate prin interfața web OpenBioMaps.

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

Actualizarea unui singur container
```console
foo@bar:~$ docker-compose up -d app
```

## Configurarea e-mailului pentru proiecte


**Trebuie să configurați accesul la un server de e-mail** pentru a trimite e-mailuri din aplicație.

Presupunând că serverul nou nu are propriul nume de domeniu, valoarea implicită pentru trimiterea e-mailurilor este setată la SMTP (/etc/openbiomaps/system_vars.php.inc), ceea ce necesită configurarea serverelor SMTP de ieșire și a autentificării asociate pentru fiecare proiect (/var/www/html/biomaps/projects/.../local_vars.php.inc).

Aceste fișiere de configurare pot fi editate în interfața Supervisor.

Găsiți secțiunea cu setările pentru e-mail și configurați gazda SMTP și autentificarea, dacă este necesară.

Dacă există un server SMTP extern, iată un exemplu:
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

Dacă SMTP_SENDER nu este setat, SMTP_USERNAME va fi expeditorul. Trimiterea e-mailurilor prin Google nu este posibilă cu aceste setări simple, deoarece Google utilizează stratul xoauth pentru autentificare! Este posibilă includerea stratului respectiv aici!

Dacă sistemul gazdă va fi serverul SMTP:
```console
 // Mail settings
define('SMTP_AUTH',false);
define('SMTP_HOST','172.17.0.1');
define('SMTP_PORT','25');
define('SMTP_SENDER','info@you-smtp-server');
```
Pentru adresa IP de mai sus, verificați pe gazdă cu „ip addr | grep docker0”.

Pe gazdă, în funcție de MTA utilizat, aveți câteva exemple:

### Exim4

În fișierul /etc/exim4/update-exim4.conf

 dc_relay_nets='172.21.0.0/16'
 
 dc_local_interfaces='127.0.0.1 ; ::1 ; 172.17.0.1' 

aceste linii trebuie actualizate, dar, în funcție de configurația Exim, este posibil să fie necesare și alte modificări.

În fișierul /etc/exim4/exim4.config

linia „hostlist   relay_from_hosts...” trebuie extinsă cu rețeaua obm_back, de exemplu:

  hostlist   relay_from_hosts = localhost :172.20.0.0/16 :172.17.0.0/16 :172.21.0.0/16
 
  Observație: „Este posibil ca una dintre cele trei rețele de mai sus să fie suficientă; acest lucru nu a fost încă testat.”

### Postfix

inet_interfaces = 172.17.0.1

mynetworks = 172.21.0.4 172.20.0.6

Iată cum puteți afla rețelele Docker și adresele IP: 

```console
docker container ls
```
Căutați obm-composer_app_1.

```console
docker inspect xxxxx_obm-composer_app_1
```
Căutați interfețele obm_back și obm_web:

  obm-composer_obm_back {
  
  ...
  
  "IPAddress": "172.20.0.6",
  
  }
  
  obm-composer_obm_web {
  
  ...
  
  "IPAddress": "172.21.0.4",
  
  }

### Firewall

Este posibil să fie necesară și actualizarea firewall-ului pentru a permite mesajele primite de la imagine către gazdă. Adresa de rețea obm_back trebuie permisă drept rețea de intrare în firewall. De exemplu:
```console
ufw allow from 172.20.0.0/16 proto tcp to any port 25
```
### Setări SMTP globale

Cel mai probabil, veți dori să utilizați aceleași setări SMTP pentru toate proiectele de pe server. În acest caz, utilizați parametrii:

   - SMTP_GLOBAL_HOST
   - SMTP_GLOBAL_AUTH
   - SMTP_GLOBAL_USERNAME
   - SMTP_GLOBAL_PASSWORD
   - SMTP_GLOBAL_SECURE
   - SMTP_GLOBAL_PORT
   - SMTP_GLOBAL_SENDER
 
în sytem_vars.php.inc. Cel puțin SMTP_GLOBAL_HOST trebuie setat dacă doriți să utilizați parametrii globali. Parametrii locali îi suprascriu întotdeauna pe cei globali.
 

## Configurarea accesului **ssl**/**https** (foarte recomandată)


Este posibil să fie necesară actualizarea setării protocolului de acces al proiectului în Supervisor; totuși, aceasta depinde de configurația gazdei.

*Nu există niciun server web pe gazdă, dar gazda furnizează certificate SSL pentru Docker.*

O modalitate posibilă este utilizarea certificatelor SSL ale gazdei prin montarea directoarelor necesare de pe gazdă în Docker.
Puteți crea certificate letsencrypt:
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

*Gazda are un server web și furnizează un proxy pentru Docker.*

O altă modalitate este utilizarea proxy-ului Apache al gazdei.

Gazdă: /etc/apache2/sites-enabled/000-default.conf
```
RedirectMatch permanent ^(?!/.well-known/.*) https://YOURDOMAIN/
```

Gazdă: /etc/apache2/sites-enabled/default-ssl.conf
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
În acest caz, nu este necesară utilizarea protocolului HTTPS în setările proiectului, deoarece OBM poate recunoaște solicitarea HTTPS prin setările HTTP-X-FORWARD.


*Utilizarea Traefik pentru procesarea solicitărilor către domenii diferite la nivelul Docker. De exemplu, aveți mai multe containere Docker pe gazdă...*

Pentru configurarea unui router de trafic HTTPS bazat pe Docker, recomandăm utilizarea Traefik 2.x într-un alt container:

https://gitlab.com/openbiomaps/docker/traefik2.0-proxy

Și actualizați fișierul docker-compose.yml pentru a comunica cu Traefik:

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

Este posibil ca acest ultim exemplu să nu fie încă complet...

Dacă oferiți acces la PostgreSQL, trebuie să configurați și SSL pentru PostgreSQL.

Dacă utilizați Traefik, puteți configura acolo accesul SSL. În caz contrar, puteți furniza certificate SSL containerului bazei de date și configura PostgreSQL astfel încât să accepte conexiuni numai prin SSL.

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

În containerul biomaps_db:
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
Puteți testa conexiunea PostgreSQL fără SSL:
```console
psql "postgresql://gisadmin@YOURDMAIN:5432/gisdata?sslmode=disable"
```

Dacă obligativitatea SSL funcționează, veți primi un mesaj de eroare asemănător cu acesta:

psql: FATAL:  no pg_hba.conf entry for host "xxxxxxx", user "gisadmin", database "gisdata", SSL off 


## Întreținerea Docker

### Oprirea Docker

```console
foo@bar:~$ docker-compose down
```

### Ștergerea tuturor elementelor (inclusiv datele și bazele de date)

```console
foo@bar:~$ docker-compose down -v
```


### Accesul la shell-ul sistemului din imaginea containerului

```console
foo@bar:~$ docker-compose exec app bash
```
Aici am accesat serviciul **app**. Consultați numele serviciilor în fișierul docker-compose.yml.


### Citirea jurnalelor

```console
foo@bar:~$ docker-compose logs -f app
```

### Utilizarea pgtop

docker-compose exec -u postgres <service_name> pg_top

### Repornirea aplicației

Nu reporniți Apache din shell-ul Docker, ci din exterior:
```console
foo@bar:~$ docker-compose restart app
```

### Eliminarea unui număr mare de imagini Docker vechi și neutilizate

Avem multe?
```console
docker images | grep "<none>"
```
Să le ștergem...
```console
docker images | grep "<none>" | awk '{print $3}' | sed -e 's/^/docker rmi /' | bash
```
Este posibil să fie necesară editarea fișierelor traefik2.0/traefik.yml, traefik2.0/docker-compose.yml și traefik2.0/acme.json.

### Actualizarea automată a Docker

https://github.com/OpenBioMaps/scripts/blob/master/docker-auto-update.readme

## Arhivarea tabelelor, datelor, ...

Pentru scripturi, consultați acest depozit:

https://github.com/OpenBioMaps/scripts

- utilizați archive.sh pentru a configura exporturi SQL periodice ale tabelelor importante

### Exemple de setări crontab pentru archive.sh

```sh
   #dumping normal tables from Monday to Saturday
   15 04 * * 1-6 /root/archive.sh normal &
   #dumping all tables and whole databases on every Sunday
   15 04 * * 7 /root/archive.sh full &
```

### Exemple de setări în obm_archive_settings.sh

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

### Exportarea unui tabel din baza de date utilizând Docker

docker-compose exec -T biomaps_db bash -c "pg_dump -U biomapsadmin --table public.YOUR_TABLE gisdata" > YOUR_TABLE.sql



## Resurse


* https://gitlab.com/openbiomaps/web-app
* https://gitlab.com/openbiomaps/docker/obm-composer
