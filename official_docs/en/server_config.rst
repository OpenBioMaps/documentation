Server configuration
********************

Supervisor
----------
The Supervisor is a standalone web application to perform low-level configuration of OBM server and projects and to maintain updates. Supervisor is also installed during the OBM server installation and can be accessed from its root URL, e.g. yourserver.com/supervisor/ or yourserver.com/supervisor.php

The Supervisor login password can be regenerated by running the obm_post_install.sh command:

.. code-block:: sh

  /srv/docker/openbiomaps# /obm_post_install.sh update supervisor

Supervisor has two modes of operation, system and project. In system mode, system level updates are available and ``system_vars.php.inc`` can be modified. In project mode, project updates are available and ``local_vars.php.inc`` can be modified, as well as database level modifications related to the project that are related to the project creation. Furthermore, in project mode, a file manager is available to manage the contents of the project/local folder. Supervisor project mode is also available from the project administration interface for project administrators.



system_vars.php.inc
-------------------
The system settings for OpenBioMaps can be found in the system_vars.php.inc file. This can be modified via the Supervisor.

``/etc/openbiomaps/system_vars.php.inc``

.. code-block:: php

  # If you use OBM in a local environment without proxy but non-standard http ports, set it true!
  #define("USE_NON_STANDARD_HTTP_PORTS",false);

  # Set it according to the real server address
  define("OB_DOMAIN","localhost/biomaps");
  
  # The default is /var/lib/openbiomaps/
  # define("OB_SYSDIR","/var/lib/openbiomaps/");

  define("OB_TMP","/var/lib/openbiomaps/tmp/");

  define("OB_ROOT","/var/www/html/biomaps/root-site");

  define("OB_ROOT_SITE","/var/www/html/biomaps/root-site/");

  define("POSTGRES_PORT","5432");

  define("GISDB_HOST",'localhost');     // for creating new project

  define("MAPSERVER_HOST",'mapserver'); // for creating new project

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

  // mandatory constant for web auth. The same value should be set in the database: biomaps->oauth_clients->web->oauth_secret
  define('WEB_CLIENT_SECRET','...');


apache server
-------------
- cgi-bin settings
 
mapserver
---------
- fastcgi settings
- mapcache settings

PHP
---
- memcache settings

cron
----
There are some recommended cron jobs to set up (examples):

- docker update

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

- jobs runner
  
.. code-block:: bash

  # m h  dom mon dow   command
  */5 * * * * /path_to/docker-compose -f /srv/docker/openbiomaps/docker-compose.yml exec -u www-data -T app php /var/www/html/biomaps/root-site/projects/PROJECTTABLE/jobs.php

