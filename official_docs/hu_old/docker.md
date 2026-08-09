
# Virtual szerverek: Docker

It is the currently supported up-to-date virtual environment release of OpenBioMaps.

It is good for testing, and developing or it can be applied in a production environment after some updates.

For using docker 4 steps are needed:
1. Install docker-compose
2. Get the obm-docker image
3. Configure your docker according to the host's specialty (e.g. SSL, SMTP)
4. Start your docker environment


## Előkészítés és telepítés: Docker & Compose

```console
sudo curl -L https://github.com/docker/compose/releases/download/1.29.2/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose

docker-compose --version
```
docker-compose version 1.29.2, build f46880fe


Visit this page for further information about installing docker:

[https://docs.docker.com/compose/install/](https://docs.docker.com/compose/install/)


## Egy OpenBioMaps példány telepítése

It is recommended to put docker files into /srv/docker directory
```
mkdir -p /srv/docker/openbiomaps && cd /srv/docker/openbiomaps

git clone https://gitlab.com/openbiomaps/docker/obm-composer.git .

sudo su

groupadd -g 996 docker

adduser foo docker

docker network create obm_web

docker-compose pull

./obm_pre_install.sh

docker-compose up -d

./obm_post_install.sh

docker-compose restart
```

## A saját OBM alkalmazásunk meglátogatása

[http://YOUR_SERVER_NAME:9880/](http://YOUR_SERVER_NAME:9880/)

[http://YOUR_SERVER_NAME:9880/projects/sablon/](http://YOUR_SERVER_NAME:9880/projects/sablon/)

Log in your template databse using *valaki@openbiomaps.org* user name and *abc123* password;

If you installed the docker in your local computer you can access the services above in localhost.


### Adatbázis hozzáférések

You can access your Postgres database on the following preconfigured online database manager applications. However, it depends on your host-docker relationship.

[phppgadmin](http://YOUR_SERVER_NAME:9881/)

[adminer](http://YOUR_SERVER_NAME:9882/)

with *sablon_admin* username and *12345* password. A *biomapsadmin* felhasználó rendszergazdai szintű hozzáférésű. A jelszava telepítéskor jön létre és a /srv/docker/openbiomaps/.env fájlban található.


In the map file, the new encrypted password can be generated with the ms-access-key located in /var/lib/openbiomaps/maps/access.key

The two databases 'biomaps' and 'gisdata' have root postgres users respectively *biomaps* and *gisdata* (instead of the usual *postgres*) and both password is *changeMe*.

## Docker karbantartó felület

This step is not obligatory but can be useful if you need a strong web admin interface for docker management. 

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

Visit your docker-admin (portainer) app:

[http://YOUR_SERVER_NAME:9000/](http://YOUR_SERVER_NAME:9000/)

Log in to your app using *admin* user name and your password;

If you installed the docker in your local computer you can access the services above in localhost.


## OBM karbantartás


You can access OBM server admin interface: 
[http://localhost:9880/supervisor.php](http://localhost:9880/supervisor.php)

with *supervisor* username and password created by obm_post_install.sh. This password is located at /etc/openbiomaps/.htpasswd.

## Updates: update application with Docker


```console
foo@bar:~$ docker-compose pull 
Pulling biomaps_db ... done
Pulling mapserver  ... done
Pulling app        ... done
Pulling phppgadmin ... done
Pulling adminer    ... done

foo@bar:~$ docker-compose up -d
Creating obm-composer_biomaps_db_1 ... done
Creating obm-composer_mapserver_1  ... done
Creating obm-composer_adminer_1    ... done
Creating obm-composer_phppgadmin_1 ... done
Creating obm-composer_app_1        ... done
```

Update only one container
```console
foo@bar:~$ docker-compose up -d app
```

## After founding a new project


You **must set up a Mail server access** to send emails from the app

Assuming that the new servers do not have their own domain name, the default value for sending mail is set to SMTP (/etc/openbiomaps/system_vars.php.inc), which requires you to configure outgoing smtp servers and associated authentication for each project (/var/www/html/biomaps/projects/.../local_vars.php.inc)

These config files can be edited in the supervisor interface.

Find the mail settings section and set up the SMTP host and authentication if needed.

If there is an external SMTP server here you are an example:
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

If SMTP_SENDER is not set, the SMTP_USERNAME will be the sender. Sending mails with Google, with these simple settings is not possible, because Google uses xoauth layer to authenticate! It is possible to include that layer here!

If the host system will be the SMTP server:
```console
 // Mail settings
define('SMTP_AUTH',false);
define('SMTP_HOST','172.17.0.1');
define('SMTP_PORT','25');
define('SMTP_SENDER','info@you-smtp-server');
```
For the IP address above check host "ip addr | grep docker0"

On the host depending on what MTA you have here you some examples:

### Exim4

In the /etc/exim4/update-exim4.conf file

 dc_relay_nets='172.21.0.0/16'
 dc_local_interfaces='127.0.0.1 ; ::1 ; 172.17.0.1' 

these lines should be updated, but depending on your exim config maybe something else as well.

In the /etc/exim4/exim4.config file

"hostlist   relay_from_hosts..." line, you should extend with the obm_back network e.g.
 hostlist   relay_from_hosts = localhost :172.20.0.0/16 :172.17.0.0/16 :172.21.0.0/16
 
 Comment: "Maybe one of the three networks is enough above, I did not test yet"

### Postfix

inet_interfaces = 172.17.0.1

mynetworks = 172.21.0.4 172.20.0.6

Here's how to find out docker networks and ip addresses: 

```console
docker container ls
```
Search for obm-composer_app_1

```console
docker inspect xxxxx_obm-composer_app_1
```
Search for obm_back and obm_web interfaces:
obm-composer_obm_back {
 ...
 "IPAddress": "172.20.0.6",
}
obm-composer_obm_web {
 ...
 "IPAddress": "172.21.0.4",
}

### Firewall

You may also need to update your firewall to enable incoming mail from the image to the host. The network address of obm_back must be allowed as an incoming network for the firewall. E.g.
```console
ufw allow from 172.20.0.0/16 proto tcp to any port 25
```
### Global smtp settings

Most probably you want to use the same SMTP settings for your all project on your server. In this case, use the

   - SMTP_GLOBAL_HOST
   - SMTP_GLOBAL_AUTH
   - SMTP_GLOBAL_USERNAME
   - SMTP_GLOBAL_PASSWORD
   - SMTP_GLOBAL_SECURE
   - SMTP_GLOBAL_PORT
   - SMTP_GLOBAL_SENDER
 
 parameters in the sytem_vars.php.inc. At least the SMTP_GLOBAL_HOST should be set if you want to use global parameters. The local params override the globals always.
 
 
 

## Setting up **ssl**/**https access** (highly recommended)

You may need to update your project access protocol setting in the Supervisor however it is depending on your host's setting.

*There is no webserver on the Host, but Host provide ssl certs for docker*

One possible way is to use the host's SSL certificates by the way to mount the necessary directories from the host to the docker.
You can create letsencrypt 
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

*Host has a web server and provide a proxy for the docker*

Another way to use the host's Apache proxy

Host: /etc/apache2/sites-enabled/000-default.conf
```
RedirectMatch permanent ^(?!/.well-known/.*) https://YOURDOMAIN/
```

Host: /etc/apache2/sites-enabled/default-ssl.conf
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
In this case you don't need to use https protocol in projects settings because the obm can recognize the https request through the HTTP-X-FORWARD settings.


*Using traefik to process different domain request in the docker level. E.g. you have several docker containers on your host...*

To set up docker based https trafic rooter we recommend to use traefik2.x in an other container:

https://gitlab.com/openbiomaps/docker/traefik2.0-proxy

And update your docker-compose.yml file to communicate with traefik:

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

This latter example is maybe not complete yet...

If you provide Postgres access you also need to set up SSL over Postgres

If you have Traefik you can configure SSL access there. In another case, you can give SSL certs for your database container and set up Postgres to accept connection only through SSL.

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

In biomaps_db container:
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
You can try your postgres connection without ssl:
```console
psql "postgresql://gisadmin@YOURDMAIN:5432/gisdata?sslmode=disable"
```

If your SSL require works, you will get an error message like this:

psql: FATAL:  no pg_hba.conf entry for host "xxxxxxx", user "gisadmin", database "gisdata", SSL off 




## Docker karbantartás


### Stopping docker

```console
foo@bar:~$ docker-compose down
```

### Drop everything (including data and databases)


```console
foo@bar:~$ docker-compose down -v
```


### Shell access of the system in the container image


```console
foo@bar:~$ docker-compose exec app bash
```
Here we accessed the **app** service. See service names in docker-compose.yml file.


### Reading logs


```console
foo@bar:~$ docker-compose logs -f app
```

### Using pgtop


docker-compose exec -u postgres <service_name> pg_top

### Restart app

Do not restart Apache from the Docker shell, but from outside
```console
foo@bar:~$ docker-compose restart app
```

### Remove huge amounts of old, not used docker images

Do we have a lot?
```console
docker images | grep "<none>"
```
Let's drop them...
```console
docker images | grep "<none>" | awk '{print $3}' | sed -e 's/^/docker rmi /' | bash
```
You may need to edit the traefik2.0/traefik.yml, traefik2.0/docker-compose.yml, and traefik2.0/acme.json files

### Auto update of docker

https://github.com/OpenBioMaps/scripts/blob/master/docker-auto-update.readme

## Archive tables, data, ...

https://github.com/OpenBioMaps/scripts


## Resources

* https://gitlab.com/openbiomaps/web-app
* https://gitlab.com/openbiomaps/docker/obm-composer


# Not docker: VirtualBox (outdated!!!)

The VirtualBox edition currently is outdated, not recommended to use it!

1. Download VirtualBox from [https://www.virtualbox.org/wiki/Downloads](https://www.virtualbox.org/wiki/Downloads)
2. Download the latest .ova image from [http://openbiomaps.org/downloads](http://openbiomaps.org/downloads/virtual-image/)
3. Read this readme for the next steps: [http://openbiomaps.org/downloads/virtual-image/README](http://openbiomaps.org/downloads/virtual-image/README)
