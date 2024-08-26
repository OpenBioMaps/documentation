# Install new OBM Server guide

## New OBM server installation using Docker

:doc:`Docker installation tutorial <../docker>`

## Common errors and solutions after new installations or updates

:doc:`Common errors <../common_errors>`

## Server configuration

:doc:`Server configuration <../server_config>`

## Local variables for a project

Several low-level settings coming from the local_vars.php.inc file which can be updated by the server admin

### The local_vars.php.inc file


**Database connection definitions**

.. code-block:: php

  // Please change the passwords for an other random string
  define('gisdb_user','YOUR_PROJECT_ADMIN');
  define('gisdb_pass','xxxxxxx');
  define('gisdb_name','POSTGRES_DB_NAME');
  define('gisdb_host','POSTGRES_HOST_NAME');
  
**Project's sql table name**

.. code-block:: php
  
  define('PROJECTTABLE','your_database_table_name');
  //define('PROJECTTABLE',basename(__DIR__));
  
**Project data restriction settings**

.. code-block:: php
  
  // `public` data read/mod for everybody
  // `login` data read/mod only for logined users
  // `group` data read/mod only for group members
  define('ACC_LEVEL','public');
  define('MOD_LEVEL','group');
  
**Language settings**

.. code-block:: php
  
  // the corresponding language file should be exists
  // see the language file inclusion in the prepare_vars.php
  define('LANG','hu'); # en, ro, ru, ...
  
**Path and URL settings**

.. code-block:: php
  
  // On openbiomaps.org is /projects
  // else maybe empty
  define('PATH','/biomaps/resources');
  define('URL',sprintf("%s%s",$_SERVER['SERVER_NAME'],PATH));
  
**mapserver variables**

.. code-block:: php
  
  define('PRIVATE_MAPSERV',sprintf("%s/private/proxy.php",URL));
  define('PUBLIC_MAPSERV',sprintf("%s/public/proxy.php",URL));
  define('PRIVATE_MAPCACHE',sprintf("%s/private/cache.php",URL));
  define('PUBLIC_MAPCACHE',sprintf("%s/public/cache.php",URL));
  // Standalone installation
  define('MAPSERVER','http://localhost/cgi-bin/mapserv.fcgi');
  // Docker installation
  define('MAPSERVER','http://mapserver/cgi-bin/mapserv');
  // Using Mapcache needs further settings, see Mapserver documentation
  define('MAPCACHE','http://localhost/mapcache');
  define('MAP','PMAP');
  // MAP's JS OBJ variables
  // should move into postgresql vars
  define('PRIVATE_MAPFILE','private.map');
  
**Invitations**

.. code-block:: php
  
  // If 0, only admin can send invitations
  // otherwise the specified number of active invitation can be, so can't send more the xx invitations at once
  // default is 11
  define('INVITATIONS',0);
  
**MAIL settings, if no local mail agent...**

.. code-block:: php
  
  //define('SMTP_AUTH',true);
  // *local smtp server example*
  //define('SMTP_HOST','mail.your-smtp-server.org');
  //define('SMTP_USERNAME','MAIL USER');
  //define('SMTP_PASSWORD','xxxxxx');
  //define('SMTP_PORT','PORT-NUMBER');
  //define('SMTP_SENDER','mail_user@your-smtp-server.org');
  // *Google example, it not works, updates needed!!!*
  //define('SMTP_HOST','smtp.gmail.com');
  //define('SMTP_USERNAME','your-user@gmail.com');
  //define('SMTP_PASSWORD','xxxxxxxxx');
  //define('SMTP_SECURE','tls');
  //define('SMTP_PORT','587');
  
  // *Deprecated features...*
  //define('TURN_OFF_LAYERS','layer_data_points');
  //define('SHINYURL',false);
  //define('RSERVER',false);
  
**Which page loaded after log in? profile, mainpage, map
default is map**
  
.. code-block:: php
  
  define('LOGINPAGE','map');
  define('TRAINING',false);
  
**MainPage configuration**

.. code-block:: php
  
  define('MAINPAGE',array(
    //'custom_skeleton'=>1,
    'template'=>'gridbox', //intropage
    'content1'=>'map',   // map | upload-table | slideshow
    'sidebar1'=>'column_dinpi.altema|custom_countries|members|uploads|data|species|species_stat', // members uploads data species species_stat
    'system_footer'=>'on',
    'system_header'=>'off',
    //'restrictaded_pages'=>array('map','id','history','profile','data','table','editrecord','qtable','query','show','LQ','metadata')
  ));
  
**Which style folder used**

.. code-block:: php
  
  define('STYLE',array(
    'template'=>'evolvulus'
  ));
  
**Footer configuration**

.. code-block:: php
  
  define('FOOTER',array(
    'links'=>'map|upload|about|terms|usage|privacy',
    'languages'=>'languages',
    'partners' => array(
            array('img'=>'obm_logo.png','size'=>'110','url'=>'https://openbiomaps.org'),
            array('img'=>'unideb_logo.png','size'=>'','url'=>'https://unideb.hu')
        ))
  );
  
**Encrypt hash**

.. code-block:: php
  
  // *used by the read_table module to encrypt the table name, ...*
  define('MyHASH','password-string');

**Custom cache settings**

.. code-block:: php

  define('CACHE_HOST', $_ENV['CACHE_HOST'] ?? 'localhost');
  define('CACHE_PORT', $_ENV['CACHE_PORT'] ?? 11211);

**OpenID-based login settings**

.. code-block:: php

  define('OPENID_CONNECT', [
    'google' => [
        'client_id' => 'xxxxx.apps.googleusercontent.com',
        'client_secret' => 'xxxxxxx',
        'provider_url' => 'https://accounts.google.com/',
    ],
  ]);
  define('OPENID_CONNECT_CERT_PATH', '/etc/ssl/certs/ca-certificates.crt');

**Using PWA app link on mainpage**

.. code-block:: php

  define('PWA_LINK','on');
  
**Developer options**

.. code-block:: php
  
  // *Switch to an other GIT branch*
  define('branch','testing');
  // *Extra logging for PDS actions*
  define('DEBUG_PDS', true);
  
local_vars.php.inc
