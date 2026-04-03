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
  // `group` data read/mod only for group members
  define('ACC_LEVEL','public');
  define('MOD_LEVEL','group');
  
**Language settings**

.. code-block:: php
  
  // the corresponding language file should be exists
  // default language
  define('LANG','hu');

  // Project languages, the first is the default
  define('LANGUAGES', array(
    'en'=>'in English',
    'hu'=>'magyarul',
    'ro'=>'română',
    'ru'=>'русский'));
  
**Path and URL settings**

.. code-block:: php
  
  // On openbiomaps.org is /projects
  // else maybe empty
  define('PATH','/biomaps/resources');
  define('URL',sprintf("%s%s",'TYPE-YOUR-SERVER-DOMAIN_HERE',PATH));
  
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
  //define('SHINYURL',false);
  //define('RSERVER',false);
  
**Which page loaded after log in? profile, mainpage, map
default is map**
  
.. code-block:: php
  
  define('LOGINPAGE','map');
  // *Deprecated feature...*
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

**Docker specific setting for creating email alerts on new uploads**

.. code-block:: php
  
  define('OB_PROJECT_DOMAIN',OB_DOMAIN);

  
**Which style folder used**

.. code-block:: php
  
  define('STYLE',array(
    'template'=>'evolvulus'
  ));
  
**Header and Footer configuration**

.. code-block:: php
  
  define('FOOTER',array(
    'links'=>'map|upload|about|terms|usage|privacy',
    'languages'=>'languages',
    'partners' => array(
            array('img'=>'obm_logo.png','size'=>'110','url'=>'https://openbiomaps.org'),
            array('img'=>'unideb_logo.png','size'=>'','url'=>'https://unideb.hu')
        ))
  );

  define('HEADER',array(
    'links' => 'upload|map|messages|profile|localize',
    'layout' => 'obm'
    )
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

**Max image size of attachments in bytes**
.. code-block:: php
  
  define('ALLOWED_FILE_SIZE',4194304);

**Use temporary_tables.obs_... table for observation list uploadings**

.. code-block:: php

  define('USE_TEMPTABLES_FOR_OBSLISTS','true');

**Data export setting**

.. code-block:: php

  // *Above this limit the data export working instead of normal download*
  define('DATA_EXPORT_BGPROC_LIMIT',1000);

**Extra schemas for the project**

.. code-block:: php
  
  define('PROJECT_SCHEMAS',array('sablon_archive'));
  

**Security check  - It is turning on are you human? check over the usage limits for the TTL time**
**It is is working with a REDIS server**

.. code-block:: php

  define('SECURITY_CHECK',true);         // Security chech on
  define('REDIS_HOST','127.0.0.1');      // Default is 127.0.0.1
  define('REDIS_PORT','6379');          // Default is 6379
  define('SECURITY_IP_LIMIT','30');     // Max request / 10 sec / IP; false turn off IP check; Default is 30
  define('SECURITY_GLOBAL_LIMIT','10'); // Max 10 request / sec together; Default is 10
  define('SECURITY_ATTACK_TTL','600');  // How long stay in "attack mode" 5 min; Default is 600

**Developer options**

.. code-block:: php
  
  // *Switch to an other GIT branch*
  define('branch','testing');
  // *Extra logging for PDS actions*
  define('DEBUG_PDS', true);
  
local_vars.php.inc
