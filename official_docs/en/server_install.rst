Install new OBM Server guide
----------------------------

Several low-level settings coming from the local_vars.php.inc file which can be updated by the server admin

local_vars.php.inc
..................
. code-block:: php

  // Database connection definitions
  // Please change the passwords for an other random string
  define('gisdb_user','YOUR_PROJECT_ADMIN');
  define('gisdb_pass','xxxxxxx');
  define('gisdb_name','POSTGRES_DB_NAME');
  define('gisdb_host','POSTGRES_HOST_NAME');
  
  // project's sql table name 
  define('PROJECTTABLE','your_database_table_name');
  #define('PROJECTTABLE',basename(__DIR__));
  
  // default project data restriction level
  // `public` data read/mod for everybody
  // `login` data read/mod only for logined users
  // `group` data read/mod only for group members
  define('ACC_LEVEL','public');
  define('MOD_LEVEL','group');
  
  // default language
  // the corresponding language file should be exists
  // see the language file inclusion in the prepare_vars.php
  define('LANG','hu'); # en, ro, ru, ...
  
  // On openbiomaps.org is /projects
  // else maybe empty
  define('PATH','/biomaps/resources');
  define('URL',sprintf("%s%s",$_SERVER['SERVER_NAME'],PATH));
  
  // mapserver variable
  define('PRIVATE_MAPSERV',sprintf("%s/private/proxy.php",URL));
  define('PUBLIC_MAPSERV',sprintf("%s/public/proxy.php",URL));
  define('PRIVATE_MAPCACHE',sprintf("%s/private/cache.php",URL));
  define('PUBLIC_MAPCACHE',sprintf("%s/public/cache.php",URL));
  define('MAPSERVER','http://localhost/cgi-bin/mapserv.fcgi');
  define('MAPCACHE','http://localhost/mapcache');
  define('MAP','PMAP');
  
  // MAP's JS OBJ variables
  // should move into postgresql vars
  define('PRIVATE_MAPFILE','private.map');
  
  // Invitations
  // If 0, only admin can send invitations
  // otherwise the specified number of active invitation can be, so can't send more the xx invitations at once
  // default is 11
  define('INVITATIONS',11);
  
  # MAIL settings, if no local mail agent...
  #define('SMTP_AUTH',true);
  # local smtp server example 
  #define('SMTP_HOST','mail.your-smtp-server.org');
  #define('SMTP_USERNAME','MAIL USER');
  #define('SMTP_PASSWORD','xxxxxx');
  #define('SMTP_PORT','PORT-NUMBER');
  #define('SMTP_SENDER','mail_user@your-smtp-server.org');
  # Google example, it not works, updates needed!!!
  #define('SMTP_HOST','smtp.gmail.com');
  #define('SMTP_USERNAME','your-user@gmail.com');
  #define('SMTP_PASSWORD','xxxxxxxxx');
  #define('SMTP_SECURE','tls');
  #define('SMTP_PORT','587');
  
  //define('TURN_OFF_LAYERS','layer_data_points');
  define('MAP_OVER_MAINPAGE',0);
  define('LOAD_INTROPAGE',0);
  define('SHINYURL',false);
  define('RSERVER',false);
  define('LOGINPAGE','map');
  define('TRAINING',false);
  
  // used by the read_table module to encrypt the table name, ...
  define('MyHASH','password-string');

