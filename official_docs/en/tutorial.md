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
foo@bar:~$ git clone git@gitlab.com:openbiomaps/docker/obm-composer.git

foo@bar:~$ cd obm-composer/

foo@bar:~$ docker-compose up -d
```

Visit these pages on your browser
.................................
[http://localhost:9880/biomaps/](http://localhost:9880/biomaps/)

[http://localhost:9880/biomaps/projects/sablon/](http://localhost:9880/biomaps/projects/sablon/)

Log in your template databse using *valaki@openbiomaps.org* user name and *abc123* password;

You can access your postgres database at

[http://localhost:9881/adminer/](http://localhost:9881/adminer/)

[http://localhost:9882/phppgadmin/](http://localhost:9882/phppgadmin/)

with *sablon_admin* username and *12345* password. You can manage your database with *biomapsadmin* user and *abcd1234* password.

If you change these passwords, should be updated the following places:

/etc/openbiomaps/system_vars.php.inc

/var/www/html/biomaps/projects/sablon/local_vars.php.inc

/var/www/html/biomaps/projects/sablon/private/private.map

In the mapfile, the new encrypted password can be generated with the ms-access-key located in /var/lib/openbiomaps/maps/access.key

You can access OBM server admin interface: 
[http://localhost:9880/biomaps/supervisor.php](http://localhost:9880/biomaps/supervisor.php)

with *supervisor* username and *12345* password. This password is located at /etc/openbiomaps/.htaccess.


Updates: update application with Docker
.......................................
```console
foo@bar:~$ git pull git@gitlab.com:openbiomaps/docker/obm-composer.git
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

Resources
.........
* https://gitlab.com/openbiomaps/web-app
* https://gitlab.com/openbiomaps/docker
* https://hub.docker.com/r/gaspara/obm-web-app

VirtualBox
----------

1. Download virtualbox from [https://www.virtualbox.org/wiki/Downloads](https://www.virtualbox.org/wiki/Downloads)
2. Download the latest .ova image from [http://openbiomaps.org/downloads](http://openbiomaps.org/downloads/virtual-image/)
3. Read this readme for the the next steps: [http://openbiomaps.org/downloads/virtual-image/README](http://openbiomaps.org/downloads/virtual-image/README)
