Server configuration
********************

The system settings for OpenBioMaps are located in

`/etc/openbiomaps/system_vars.php.inc`

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

Further settings can be:

 - apache server settings
   - cgi-bin settings
 - mapserver settings
   - fastcgi settings
   - mapcache settings
 - memcache settings

