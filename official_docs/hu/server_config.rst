Szerverkonfiguráció
*******************

Supervisor
----------
A Supervisor önálló webalkalmazás az OpenBioMaps-szerver és a projektek
alacsony szintű konfigurálásához, valamint a frissítések karbantartásához.
A Supervisor az OpenBioMaps-szerver telepítésekor szintén települ, és a
saját gyökér-URL-jén érhető el, például:
yourserver.com/supervisor/ vagy yourserver.com/supervisor.php

A Supervisor bejelentkezési jelszava az ``obm_post_install.sh`` parancs
futtatásával hozható létre újból:

.. code-block:: sh

  /srv/docker/openbiomaps# /obm_post_install.sh update supervisor

A Supervisor két működési móddal rendelkezik: rendszer- és projektmóddal.
Rendszermódban rendszerszintű frissítések érhetők el, és módosítható a
``system_vars.php.inc`` fájl. Projektmódban projektfrissítések érhetők el,
módosítható a ``local_vars.php.inc`` fájl, továbbá elvégezhetők a projekt
létrehozásához kapcsolódó adatbázisszintű módosítások. Projektmódban
fájlkezelő is rendelkezésre áll a projekt ``local`` könyvtárának
kezeléséhez. A Supervisor projektmódja a projektadminisztrációs felületen
is elérhető a projektadminisztrátorok számára.



system_vars.php.inc
-------------------
Az OpenBioMaps rendszerbeállításai a ``system_vars.php.inc`` fájlban
találhatók. Ez a Supervisor használatával módosítható.

``/etc/openbiomaps/system_vars.php.inc``

.. code-block:: php

  # If you use OBM in a local environment without a proxy but non-standard HTTP ports, set it to true!
  #define("USE_NON_STANDARD_HTTP_PORTS",false);

  # Set it according to the real server address
  define("OB_DOMAIN", "localhost/biomaps");
  
  # The default is /var/lib/openbiomaps/
  # define("OB_SYSDIR", "/var/lib/openbiomaps/");

  define("OB_TMP", "/var/lib/openbiomaps/tmp/");

  define("OB_ROOT", "/var/www/html/biomaps/root-site");

  define("OB_ROOT_SITE", "/var/www/html/biomaps/root-site/");

  define("POSTGRES_PORT", "5432");

  define("GISDB_HOST", "localhost");     // for creating new project

  define("MAPSERVER_HOST", "mapserver"); // for creating new project

  define("OB_RESOURCES", "/var/www/html/biomaps/resources/");

  define('biomapsdb_user', '...');

  define('biomapsdb_pass', '...');

  define('biomapsdb_name', '...');

  define('biomapsdb_host', 'localhost');

  // Postgis version - not necessary to set, it only has historical value
  define('POSTGIS_V', '2.5');

  // Default sendmail opetion, can be override in project level in local_vars.php.inc 
  define('SENDMAIL', 'smtp'); # sendmail | smtp

  // memcache type - choose this
  define('CACHE', 'memcache');

  // R-Shiny Server ports, for the projects where R Shiny Server should be enabled
  define('RSERVER_PORT_someproject', 7982);

  // Supported languages
  define('LANGUAGES', 'en, hu, ro');

  // bug report system can be activated by put AUTO_BUGREPORT_ADDRESS constant
  // ask the issue-key from the gitlab-repo mainteners
  define('AUTO_BUGREPORT_ADDRESS', 'incoming+openbiomaps...'); 

  // mandatory constant for web auth. The same value should be set in the database: biomaps->oauth_clients->web->oauth_secret
  define('WEB_CLIENT_SECRET', '...');


Apache-szerver
--------------
- cgi-bin beállítások
 
MapServer
---------
- FastCGI-beállítások
- MapCache-beállítások

PHP
---
- memcache-beállítások

cron
----
Érdemes beállítani néhány ajánlott cron-feladatot. Példák:

- Docker-frissítés

  https://github.com/OpenBioMaps/scripts/tree/master/docker-auto-update
  
.. code-block:: shell

  # m h  dom mon dow   command
  0 4,16 * * * /srv/docker/openbiomaps/auto_update.sh > /srv/docker/openbiomaps/system_update_job.log

- archiválás

  A https://github.com/OpenBioMaps/scripts/blob/master/obm_archive.sh
  parancsfájl használatával, a ``.archive_list.txt`` és az
  ``obm_archive_settings.sh`` fájllal.

.. code-block:: shell

  # m h  dom mon dow   command
  0 2 * * *  /path_to/obm_archive.sh normal
  15 2 * * * /path_to/obm_archive.sh system
  15 3 1 * * /path_to/obm_archive.sh full
  0 5 * * *  /path_to/obm_archive.sh clean
  # remote servers
  0 4 * * *  /path_to/obm_archive.sh sync remote_user@remote-server.com /remote_path_to_archives
  
Docker használata esetén kövesse az ``obm_archive_settings.sh`` végén
található utasításokat.

- háttérfolyamat-futtató
  
.. code-block:: bash

  # m h  dom mon dow   command
  */5 * * * * /path_to/docker-compose -f /srv/docker/openbiomaps/docker-compose.yml exec -u www-data -T app php /var/www/html/biomaps/root-site/projects/PROJECTTABLE/jobs.php
