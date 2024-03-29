Szerver beállítások
*******************

Supervisor
----------
A Supervisor egy önálló webes alkalmazás az OBM szerver és projektek alacsonyabb szintű beállításainak elvégzéséhez és a frissítések karbantartásához. A Supervisor az OBM szerver telepítése során szintén feltelepül és elérhető URL gyökér címéből, pl. yourserver.com/supervisor/ vagy yourserver.com/supervisor.php

A Supervisor belépési jelszavát az obm_post_install.sh parancs futtatásával újra lehet generálni:

.. code-block:: sh

  /srv/docker/openbiomaps# /obm_post_install.sh update supervisor

A Supervisor-nak két működési módja van, a rendszer és a projekt. Rendszer módban a rendszer szintű frissítések érhetőek el és a ``system_vars.php.inc`` módosítható. Projekt módban a projekt frissítések érhetőek el és a ``local_vars.php.inc`` módosítható, illetve a projekthez tartozó olyan adatbázis szintű módosítások, amelyek a projekt létrehozáshoz kapcsolódnak. Továbbá projekt módban rendelkezésre áll egy fájlkezelő, amelyen keresztül a projekt/local mappa tartalmát lehet kezelni. A Supervisor projekt mód elérhető a projekt adminisztrációs felületéről is a projekt rendszergazdái számára.



system_vars.php.inc
-------------------
Az OpenBioMaps rendszerbeállításai a system_vars.php.inc fájlban találhatók. Ez a Supervisoron keresztül módosítható.

``/etc/openbiomaps/system_vars.php.inc``

.. code-block:: php

  define("OB_DOMAIN",".../biomaps");

  define("OB_SYSDIR","/mnt/data/");

  define("OB_TMP","/mnt/data/tmp/");

  define("OB_ROOT","/var/www/html/biomaps/");

  define("OB_ROOT_SITE","/var/www/html/biomaps/root-site/");

  define("POSTGRES_PORT","5432");

  define("GISDB_HOST",'localhost');     // for creating new project

  define("MAPSERVER_HOST",'localhost'); // for creating new project

  define("OB_RESOURCES","/var/www/html/biomaps/resources/");

  define('biomapsdb_user','...');

  define('biomapsdb_pass','...');

  define('biomapsdb_name','...');

  define('biomapsdb_host','localhost');

  // Postgis version - not necessary to set, it only has historical value
  define('POSTGIS_V','2.1');

  // Default sendmail opetion, can be override in project level in local_vars.php.inc 
  define('SENDMAIL','smtp'); # sendmail | smtp

  // memcache tpye - choose this
  define('CACHE','memcache');

  // R-Shiny Server ports, for the projects where R shiny server should be enabled
  define('RSERVER_PORT_someproject',7982);

  // Supported languages
  define('LANGUAGES','en,hu,ro');

  // bug report system can be activated by put AUTO_BUGREPORT_ADDRESS constant
  // ask the issue-key from the gitlab-repo mainteners
  define('AUTO_BUGREPORT_ADDRESS','incoming+openbiomaps...'); 


apache szerver
--------------
- cgi-bin beállítások
 
mapserver
---------
- fastcgi beállítások
- mapcache beállítások

PHP
---
- memcache beállítások

cron
----
Van néhány ajánlott cron feladat beállítás (példák):

- docker frissítés

  https://github.com/OpenBioMaps/scripts/tree/master/docker-auto-update
  
.. code-block:: shell

  # m h  dom mon dow   command
  0 4,16 * * * /srv/docker/openbiomaps/auto_update.sh > /srv/docker/openbiomaps/system_update_job.log

- archiver

  using the https://github.com/OpenBioMaps/scripts/blob/master/obm_archive.sh script (with .archive_list.txt and obm_archive_settings.sh)
.. code-block:: shell

  # m h  dom mon dow   command
  0 2 * * *  /path_to/obm_archive.sh normal
  15 2 * * * /path_to/obm_archive.sh system
  15 3 1 * * /path_to/obm_archive.sh full
  0 5 * * *  /path_to/obm_archive.sh clean
  # remote servers
  0 4 * * *  /path_to/obm_archive.sh sync remote_user@remote-server.com /remote_path_to_archives
  
  On Docker use the instructions at the end of obm_archive_settings.sh

- Háttérfolyamat futtatás
  
.. code-block:: bash

  # m h  dom mon dow   command
  */5 * * * * /path_to/docker-compose -f /srv/docker/openbiomaps/docker-compose.yml exec -u www-data -T app php /var/www/html/biomaps/root-site/projects/PROJECTTABLE/jobs.php

