Upload data
===========
`Upload interface usage: Video tutorial (balkanherps example) english <https://youtu.be/qsu-0UeC46g>`_

`Upload interface usage: Video tutorial (Milvus general forms) română <https://www.youtube.com/watch?v=BknizNC8pvc&t=102s>`_

`Upload interface usage: Video tutorial (Milvus atlas form) română <https://www.youtube.com/watch?v=kFnSxYp4zNM&t=33s>`_

`Upload interface usage: Video tutorial (Milvus nocturnal birds form) română <https://www.youtube.com/watch?v=NmuIdfsXYjk>`_

Query Data
==========

Share Data
==========

New project
===========

Database access
===============

Virtual servers
===============

Docker
------

It is the currently supported up-to-date virtual environment release of OpenBioMaps.

It is good for testing, developing or it can be applied in production environment after some updates.

Using docker is easy! Only 3 steps needed:
1. Install docker compose
2. Get obm-docker image
3. start your docker environment


Prepare/Install Docker & Compose
................................

```console
foo@bar:~$ sudo curl -L https://github.com/docker/compose/releases/download/1.22.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose

foo@bar:~$ sudo chmod +x /usr/local/bin/docker-compose

foo@bar:~$ docker-compose --version

docker-compose version 1.22.0, build f46880fe
```

Visit this page for further inforamtion about installing docker
[https://docs.docker.com/compose/install/](https://docs.docker.com/compose/install/)


OBM docker install
..................

```console
foo@bar:~$ git clone https://gitlab.com/openbiomaps/docker/obm-composer.git

foo@bar:~$ cd obm-composer/

foo@bar:~$ sudo groupadd -g 996 docker

foo@bar:~$ sudo adduser foo docker

foo@bar:~$ docker network create obm_web

foo@bar:~$ docker-compose up -d
```

Visit your OBM app
..................
[http://localhost:9880/biomaps/](http://localhost:9880/biomaps/)

[http://localhost:9880/biomaps/projects/sablon/](http://localhost:9880/biomaps/projects/sablon/)

Log in your template databse using *valaki@openbiomaps.org* user name and *abc123* password;


Database access
...............
You can access your postgres database on the following preconfigured online database manager applications:

[phppgadmin](http://localhost:9881/)

[adminer](http://localhost:9882/)

with *sablon_admin* username and *12345* password. You can manage your database with *biomapsadmin* user and *abcd1234* password.

If you change these passwords, should be updated the following places:

/etc/openbiomaps/system_vars.php.inc

/var/www/html/biomaps/projects/sablon/local_vars.php.inc

/var/www/html/biomaps/projects/sablon/private/private.map

In the mapfile, the new encrypted password can be generated with the ms-access-key located in /var/lib/openbiomaps/maps/access.key

The two databases 'biomaps' and 'gisdata' have root postgres users respectively *biomaps* and *gisdata* (instead of the ususal *postgres*) and both password is *changeMe*.


OBM maintenance
...............
You can access OBM server admin interface: 
[http://localhost:9880/biomaps/supervisor.php](http://localhost:9880/biomaps/supervisor.php)

with *supervisor* username and *12345* password. This password is located at /etc/openbiomaps/.htaccess.


Updates: update application with Docker
.......................................
```console
foo@bar:~$ git pull https://gitlab.com/openbiomaps/docker/obm-composer.git
foo@bar:~$ docker-compose pull 
Pulling gisdata    ... done
Pulling biomaps    ... done
Pulling mapserver  ... done
Pulling app        ... done
Pulling phppgadmin ... done
Pulling adminer    ... done

foo@bar:~$ docker-compose up -d
Starting obm-composer_gisdata_1 ... done
Starting obm-composer_biomaps_1 ... done
Starting obm-composer_mapserver_1  ... done
Starting obm-composer_adminer_1    ... done
Starting obm-composer_phppgadmin_1 ... done
Recreating obm-composer_app_1      ... done
```

Stopping docker
...............
```console
foo@bar:~$ docker-compose down
```

Drop everything (including data and databases)
..............................................
```console
foo@bar:~$ docker-compose down -v
```

Shell access of web app
.......................
```console
foo@bar:~$ docker-compose exec app bash
```

Reading logs
............
```console
foo@bar:~$ docker-compose logs -f app
```

Restart app
...........
Do not restart apache from docker shell, but from outside
```console
foo@bar:~$ docker-compose restart app
```
Set up mailing
..............
Assuming that the new servers do not have their own domain name, the default value for sending mail is set to smtp (/etc/openbiomaps/system_vars.php.inc), which requires you to configure outgoing smtp servers and associated authentication for each projects (/var/www/html/biomaps/projects/.../local_vars.php.inc)

These config files as a template can be accessed from your "obm-composer" directory:
```console
ls -l obm-composer/econf/
-rw-r--r-- 1 foo bar 2059 Feb  5 20:59 local_vars-sablon.php.inc
-rw-r--r-- 1 foo bar  417 Feb  5 20:45 server_vars.php.inc
-rw-r--r-- 1 foo bar  819 Feb  5 20:36 system_vars.php.inc
```
To be able to apply a new setting here in the running system, you have to edit your Docker config file
```console
vi obm-composer/docker-compose.yml
 20       # comment out to enable local config files
 21       # - ./econf/system_vars.php.inc:/etc/openbiomaps/system_vars.php.inc
 22       # - ./econf/server_vars.php.inc:/var/www/html/biomaps/server_vars.php.inc
 23       # - ./econf/local_vars-sablon.php.inc:/var/www/html/biomaps/projects/sablon/local_vars.php.inc
```
As you can see, there are commented references for these external files which will be included "on the fly" in your running system. 

So, you have to edit your obm-composer/econf/local_vars-sablon.php.inc file for the default "sablon" project.

Find the Mail Settings section
```console
 45 // Mail settings
 46 define('SMTP_AUTH',false); # true
 47 define('SMTP_HOST','...');
 48 define('SMTP_USERNAME','...');
 49 define('SMTP_PASSWORD','...');
 50 define('SMTP_SECURE','tls'); # ssl
 51 define('SMTP_PORT','587'); # 465
 52 define('SMTP_SENDER','openbiomaps@...');
```
Set these variables as you need. E.g.
```console
 45 // Mail settings
 46 define('SMTP_AUTH',false); # true
 47 define('SMTP_HOST','mail.my-mail-server.com');
 48 define('SMTP_USERNAME','my-name@my-mail-server.com');
 49 define('SMTP_PASSWORD','something');
 50 define('SMTP_SECURE','tls'); # ssl
 51 define('SMTP_PORT','587'); # 465
 52 define('SMTP_SENDER','openbiomaps@my-mail-server.com');
```
If SMTP_SENDER is not set the SMTP_USERNAME will be the sender. Sending mails with google, with these simple settings is not possible, because google uses xoauth layer to authenticate! It is possible to include that layer here!

Docker maintenance
..................
Remove huge amount of old, not used docker images...

Do we have a lot?
```console
docker images | grep "<none>"
```
Let drop them....
```console
docker images | grep "<none>" | awk '{print $3}' | sed -e 's/^/docker rmi /' | bash
```

Founding a new project in Docker
................................
Some updates....
```console
docker cp obm-composer_app_1:/var/www/html/biomaps/projects/YOUR_PROJECT/local_vars.php.inc ./econf/local_vars-YOUR_PROJECT.inc
```
Include this econf path below the app volumes as like sablon example.


Resources
.........
* https://gitlab.com/openbiomaps/web-app
* https://gitlab.com/openbiomaps/docker
* https://hub.docker.com/r/gaspara/obm-web-app

VirtualBox
----------
The VirtualBox edition currently is outdated, not recommended to use it!

1. Download virtualbox from [https://www.virtualbox.org/wiki/Downloads](https://www.virtualbox.org/wiki/Downloads)
2. Download the latest .ova image from [http://openbiomaps.org/downloads](http://openbiomaps.org/downloads/virtual-image/)
3. Read this readme for the the next steps: [http://openbiomaps.org/downloads/virtual-image/README](http://openbiomaps.org/downloads/virtual-image/README)
