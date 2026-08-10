Server administration
*********************

This page describes the low-level configuration of an OpenBioMaps server.
Current installations normally run OpenBioMaps as a collection of Docker
Compose services. The application web server and PHP runtime are provided by
the ``app`` container, while MapServer and PostgreSQL run in separate
containers.

The examples on this page are based on the OpenBioMaps application image and
the reference Docker Compose configuration. Image contents and service
definitions can change between releases. Always compare this documentation
with the files shipped with the version being deployed.

Do not store real passwords, client secrets, encryption keys, or other
credentials in documentation or a source-code repository.

Supervisor
==========

Supervisor is a standalone web application for low-level configuration,
updates, and project maintenance. It is installed as part of an OpenBioMaps
server installation and is normally available at one of the following URLs:

* ``https://YOUR_SERVER/supervisor/``
* ``https://YOUR_SERVER/supervisor.php``

The exact URL depends on the server and reverse-proxy configuration.

Supervisor has two operating modes:

System mode
  Provides system-level maintenance and updates, including management of the
  system configuration.

Project mode
  Provides project updates, project creation and database maintenance,
  management of ``local_vars.php.inc``, and a file manager for the project's
  ``local`` directory.

Project mode can also be made available to project administrators through the
project administration interface.

Restrict access to Supervisor to trusted administrators. Use HTTPS and a
strong, unique password, and consider additional network-level restrictions.

Regenerating the Supervisor password
------------------------------------

On the Docker host, the Supervisor password can be regenerated with the
post-installation script:

.. code-block:: console

   cd /srv/docker/openbiomaps
   ./obm_post_install.sh update supervisor

The exact installation directory may differ. Run the command from the
directory containing the OpenBioMaps installation scripts and review its
output for errors.

After changing the password, verify that Supervisor is accessible and store
the new credential in an appropriate password manager.

System variable files
=====================

OpenBioMaps uses system-level variable files in addition to each project's
``local_vars.php.inc`` file.

The application image currently includes a base file at:

``/var/www/html/biomaps/root-site/server_vars.php.inc``

The Docker image also declares ``/etc/openbiomaps`` as a volume. The
administrator-managed system configuration is normally stored there, for
example:

``/etc/openbiomaps/system_vars.php.inc``

The precise relationship and loading order of ``server_vars.php.inc`` and
``system_vars.php.inc`` can vary between OpenBioMaps releases. Do not assume
that the two files are interchangeable. Use Supervisor and the templates
provided with the installed release, and verify the effective configuration
after an update.

Because ``/etc/openbiomaps`` is mounted from the ``etc_openbiomaps`` Docker
volume in the reference Compose configuration, changes made there persist
when the ``app`` container is replaced.

The following sections describe the settings previously shown in the
``system_vars.php.inc`` example. Values are examples and must be reviewed for
the actual installation.

Network and URL settings
------------------------

.. list-table::
   :header-rows: 1
   :widths: 24 28 48

   * - Variable
     - Example value
     - Description
   * - ``USE_NON_STANDARD_HTTP_PORTS``
     - ``false``
     - Enables support for a local installation that is not behind a proxy
       and uses non-standard HTTP ports. It is optional and disabled in the
       example.
   * - ``OB_DOMAIN``
     - ``localhost/biomaps``
     - Public server address and deployment path used by OpenBioMaps. Replace
       it with the actual host name and path. The value must be consistent
       with the reverse proxy and TLS configuration.
   * - ``POSTGRES_PORT``
     - ``5432``
     - PostgreSQL service port used by OpenBioMaps.
   * - ``GISDB_HOST``
     - ``localhost``
     - Database host inserted into newly created project configurations. In a
       Docker installation this will normally need to be a Docker network
       name or alias such as ``gisdata`` rather than ``localhost``.
   * - ``MAPSERVER_HOST``
     - ``mapserver``
     - MapServer service host inserted into newly created project
       configurations. In the reference Compose environment, ``mapserver`` is
       the Docker Compose service name.

Within a container, ``localhost`` refers to that container itself. It does
not refer to another Compose service. For example, the ``app`` container
should normally reach MapServer as ``mapserver`` and the database through one
of the database service's network names or aliases.

The reference database service is named ``biomaps_db`` and has the aliases
``biomaps`` and ``gisdata``. Existing OpenBioMaps templates may expect one of
these aliases. Before changing ``GISDB_HOST``, inspect a working project
configuration and verify which name is expected by the installed release.

Directory settings
------------------

.. list-table::
   :header-rows: 1
   :widths: 24 31 45

   * - Variable
     - Example value
     - Description
   * - ``OB_SYSDIR``
     - ``/var/lib/openbiomaps/``
     - Base directory for persistent OpenBioMaps system data. This is the
       documented default and is optional in the example.
   * - ``OB_TMP``
     - ``/var/lib/openbiomaps/tmp/``
     - Directory used for OpenBioMaps temporary files. It is stored within
       the persistent ``var_lib`` volume in the reference Compose
       configuration.
   * - ``OB_ROOT``
     - ``/var/www/html/biomaps/root-site``
     - Application document-root directory. The example does not include a
       trailing slash.
   * - ``OB_ROOT_SITE``
     - ``/var/www/html/biomaps/root-site/``
     - Application root-site directory. Some application code expects this
       form with a trailing slash.
   * - ``OB_RESOURCES``
     - ``/var/www/html/biomaps/resources/``
     - Directory containing shared OpenBioMaps resources.

Do not change paths without checking the Docker image, Apache document root,
volume mounts, project paths, and all scripts that refer to them.

System database connection
--------------------------

These variables define the connection to the OpenBioMaps system database.
They are distinct from the project-specific ``gisdb_*`` settings documented
in the server installation guide.

.. list-table::
   :header-rows: 1
   :widths: 24 26 50

   * - Variable
     - Example value
     - Description
   * - ``biomapsdb_user``
     - Secret installation-specific value
     - PostgreSQL user used to access the OpenBioMaps system database.
   * - ``biomapsdb_pass``
     - Secret installation-specific value
     - Password for the system database user. Use a strong random value and
       do not commit it to a repository.
   * - ``biomapsdb_name``
     - Installation-specific value
     - Name of the OpenBioMaps system database.
   * - ``biomapsdb_host``
     - ``localhost``
     - Host running the system database. In the reference Docker environment,
       use the appropriate database service name or alias instead of
       ``localhost`` unless PostgreSQL actually runs in the ``app`` container.
   * - ``POSTGIS_V``
     - ``2.5``
     - Historical PostGIS-version marker. It is not normally necessary to set
       this value and it may not represent the version currently installed.

The reference Compose file uses the
``openbiomaps/database:pg17-3.5`` image. The image name indicates a newer
PostgreSQL/PostGIS combination than the historical ``POSTGIS_V`` example.
Do not use ``POSTGIS_V`` to determine the actual server version. Query the
database server when version information is required.

Mail delivery
-------------

.. list-table::
   :header-rows: 1
   :widths: 24 24 52

   * - Variable
     - Example value
     - Description
   * - ``SENDMAIL``
     - ``smtp``
     - Default mail-delivery method. Documented values are ``sendmail`` and
       ``smtp``. A project may override this setting in
       ``local_vars.php.inc``.

When SMTP is selected, configure the required SMTP host, authentication,
sender, port, and transport-security settings at the appropriate system or
project level. Do not store SMTP credentials in public configuration files.

Cache
-----

.. list-table::
   :header-rows: 1
   :widths: 24 24 52

   * - Variable
     - Example value
     - Description
   * - ``CACHE``
     - ``memcache``
     - Selects the cache implementation used by OpenBioMaps.

The reference application image also defines these environment defaults:

.. list-table::
   :header-rows: 1
   :widths: 24 24 52

   * - Environment variable
     - Default value
     - Description
   * - ``CACHE_HOST``
     - ``memcached``
     - Host name of the Memcached service. It matches the service name in the
       reference Compose file.
   * - ``CACHE_PORT``
     - ``11211``
     - Port used by Memcached inside the Docker network.

The ``memcached`` service is attached to the private ``obm_back`` network and
does not need to publish a port on the Docker host.

Optional R Shiny services
-------------------------

.. list-table::
   :header-rows: 1
   :widths: 32 22 46

   * - Variable
     - Example value
     - Description
   * - ``RSERVER_PORT_someproject``
     - ``7982``
     - Project-specific R Shiny Server port. Replace ``someproject`` with the
       relevant project identifier. Configure this only for projects that
       still use the R Shiny integration.

R Shiny support is a legacy or optional integration. Confirm that it is
supported by the installed OpenBioMaps release before configuring it.

Supported languages
-------------------

.. list-table::
   :header-rows: 1
   :widths: 24 25 51

   * - Variable
     - Example value
     - Description
   * - ``LANGUAGES``
     - ``en, hu, ro``
     - Comma-separated list of languages supported by the server. Relevant
       language files must be installed.

This system-level value is separate from project-level language selection.
Project language settings must use languages available on the server.

Automatic bug reports
---------------------

.. list-table::
   :header-rows: 1
   :widths: 28 30 42

   * - Variable
     - Example value
     - Description
   * - ``AUTO_BUGREPORT_ADDRESS``
     - An incoming issue address supplied by the repository maintainers
     - Enables integration with an issue tracker through an incoming address.
       Request the appropriate issue key or address from the OpenBioMaps
       repository maintainers.

Treat the complete incoming address as a secret because anyone who obtains it
may be able to create issues or submit unwanted content. Review logs and
outgoing reports to ensure that sensitive project or user data is not
included.

Web authentication secret
-------------------------

.. list-table::
   :header-rows: 1
   :widths: 28 28 44

   * - Variable
     - Example value
     - Description
   * - ``WEB_CLIENT_SECRET``
     - Secret installation-specific value
     - Mandatory secret used by web authentication. The same value must be
       stored for the ``web`` OAuth client in the system database.

The configuration value and the corresponding database value must remain
synchronised. Generate a strong random secret, restrict access to it, and plan
secret rotation carefully because changing only one copy will break web
authentication.

Applying system-variable changes
--------------------------------

After changing a system setting:

#. Check the syntax of the modified configuration.
#. Restart or recreate the affected service if required.
#. Inspect the service logs.
#. Test Supervisor and a representative project.
#. Test authentication, database access, maps, and background jobs when the
   changed setting affects those components.

For example:

.. code-block:: console

   docker compose config
   docker compose restart app
   docker compose logs --tail=200 app

The exact Docker Compose command may be ``docker-compose`` on older systems.

The application image configures PHP OPcache with timestamp validation
disabled. Consequently, changed PHP files may not be detected immediately by
a running process. Restarting the ``app`` container after PHP configuration
or application changes avoids serving stale cached code.

Docker service architecture
===========================

The reference Compose configuration creates a private bridge network named
``obm_back``. Services on this network can communicate through their Compose
service names and configured network aliases.

The core services are:

.. list-table::
   :header-rows: 1
   :widths: 21 29 50

   * - Service
     - Image
     - Purpose
   * - ``app``
     - ``registry.gitlab.com/openbiomaps/web-app:latest``
     - Runs Apache HTTP Server, PHP, the OpenBioMaps web application, and
       Supervisor.
   * - ``mapserver``
     - ``openbiomaps/mapserver``
     - Runs the MapServer service used to render project maps.
   * - ``biomaps_db``
     - ``openbiomaps/database:pg17-3.5``
     - Runs PostgreSQL and PostGIS for the system and, in the default
       topology, project databases.
   * - ``memcached``
     - ``memcached:latest``
     - Provides the shared application cache.
   * - ``obm-server-api``
     - ``registry.gitlab.com/openbiomaps/api/obm-server-api:latest``
     - Provides the separate OpenBioMaps server API.
   * - ``adminer``
     - ``adminer``
     - Provides a browser-based database administration interface.

The exact service list depends on the installed Compose file. Optional
services may be disabled, removed, or replaced.

For production deployments, consider pinning images to tested release tags
or immutable digests instead of using ``latest``. This makes upgrades
predictable and simplifies rollback.

Application service: Apache and PHP
===================================

The ``app`` image is based on the official ``php:8.4-apache-trixie`` image.
Apache and PHP therefore run in the same container.

Apache configuration
--------------------

The image performs the following Apache configuration:

* enables the ``headers``, ``proxy``, ``proxy_http``, ``rewrite``, and ``ssl``
  modules;
* changes the default document root to
  ``/var/www/html/biomaps/root-site``; and
* installs the OpenBioMaps Apache configuration as
  ``/etc/apache2/conf-enabled/openbiomaps.conf``.

The reference Compose file publishes container ports 80 and 443 on the same
host ports:

.. code-block:: text

   80:80
   443:443

When another reverse proxy terminates TLS, the published ports and Apache
virtual-host configuration may need to be adjusted. Ensure that the public
scheme, host, path, and forwarded headers agree with ``OB_DOMAIN`` and the
project URLs.

Custom Apache configuration should be supplied through a maintained image,
a bind mount, or another reproducible deployment mechanism. Avoid editing a
running container directly because those changes are lost when the container
is replaced.

The reference Compose file includes commented examples for mounting TLS
certificates and a custom SSL virtual host. Generate and renew certificates
outside the container unless the deployment deliberately uses another
certificate-management design.

After changing Apache configuration, validate it inside the container:

.. code-block:: console

   docker compose exec app apache2ctl configtest
   docker compose restart app
   docker compose logs --tail=200 app

PHP configuration
-----------------

The application image installs PHP extensions required by OpenBioMaps,
including PostgreSQL, PDO PostgreSQL, internationalisation, ZIP, GD, Exif,
Memcached, YAML, and mcrypt support.

The reference Compose file demonstrates how to override PHP settings by
mounting individual INI files into ``/usr/local/etc/php/conf.d``:

.. code-block:: text

   ./php-date.timezone.ini -> /usr/local/etc/php/conf.d/php-date.timezone.ini
   ./php-upload.ini        -> /usr/local/etc/php/conf.d/php-upload.ini

This approach can be used for settings such as:

* ``date.timezone``;
* ``upload_max_filesize``;
* ``post_max_size``;
* ``memory_limit``;
* ``max_execution_time``; and
* session-related settings.

When configuring uploads, keep all relevant limits consistent. For example,
``post_max_size`` must be large enough for the complete request, not only the
uploaded file. A reverse proxy may impose an additional request-size limit.

Inspect the effective PHP configuration inside the container rather than
assuming that a mounted file was loaded:

.. code-block:: console

   docker compose exec app php --ini
   docker compose exec app php -i
   docker compose logs --tail=200 app

Restart the ``app`` service after changing mounted INI files.

Application logs
----------------

The image creates ``/var/log/openbiomaps.log`` and assigns it to the web
server user. The reference Compose file bind-mounts this file from the Docker
host:

.. code-block:: text

   ./openbiomaps.log -> /var/log/openbiomaps.log

The host file must exist with permissions that allow the container's
``www-data`` user to write to it. Also inspect the container's standard
output and Apache logs:

.. code-block:: console

   docker compose logs --tail=200 app
   docker compose logs -f app

Configure rotation for host-side log files to prevent them from consuming all
available disk space. Avoid logging passwords, tokens, complete database
connection strings, or sensitive observation data.

MapServer service
=================

MapServer runs in the separate ``mapserver`` service. The ``app`` container
normally reaches it through the host name ``mapserver`` on the private Docker
network.

The reference Compose configuration shares these resources with MapServer:

.. list-table::
   :header-rows: 1
   :widths: 29 31 40

   * - Source
     - Container path
     - Purpose
   * - ``mapserver_log`` volume
     - ``/tmp/mapserver``
     - Shared MapServer log and temporary data.
   * - ``var_lib`` volume
     - ``/var/lib/openbiomaps``
     - Shared OpenBioMaps system data.
   * - ``projects`` volume
     - ``/var/www/html/biomaps/root-site/projects``
     - Project files and project-specific mapfiles.
   * - ``./openbiomaps.conf``
     - ``/etc/apache2/conf-enabled/openbiomaps.conf``
     - MapServer container Apache configuration.
   * - ``./00_msencrypt-wrapper.conf``
     - ``/etc/apache2/conf-enabled/00_msencrypt-wrapper.conf``
     - Apache configuration for the MapServer encryption wrapper.
   * - ``./msencrypt-wrapper.pl``
     - ``/usr/local/bin/msencrypt-wrapper.pl``
     - Wrapper used by the MapServer service.

Changes to the host-mounted MapServer Apache configuration or wrapper should
be validated and followed by a restart of the ``mapserver`` service:

.. code-block:: console

   docker compose exec mapserver apache2ctl configtest
   docker compose restart mapserver
   docker compose logs --tail=200 mapserver

Project mapfiles are normally managed through OpenBioMaps project
administration and Supervisor. Because the ``projects`` volume is shared,
both the application and MapServer can access the same project files.

MapServer does not publish a host port in the reference Compose file. This is
intentional: requests should normally pass through the OpenBioMaps application
or its configured proxy rather than exposing MapServer directly to the
internet.

MapCache requires additional configuration and is not enabled merely by
defining a MapCache URL. If MapCache is introduced, document its storage,
cache invalidation, resource limits, and network exposure.

PostgreSQL and PostGIS service
==============================

The ``biomaps_db`` service runs PostgreSQL and PostGIS using the
``openbiomaps/database:pg17-3.5`` image. Its data directory is stored in the
persistent ``biomaps_data`` volume:

``/var/lib/postgresql/data``

The service has the following names on the private network:

* Compose service name: ``biomaps_db``;
* network alias: ``biomaps``; and
* network alias: ``gisdata``.

Use the name expected by the installed OpenBioMaps configuration. Do not use
``localhost`` from the ``app`` or ``mapserver`` container to refer to this
database service.

The database port is not published to the Docker host in the reference
configuration. This reduces exposure and is sufficient for application
services attached to ``obm_back``. Publish PostgreSQL only when external
access is required, and then restrict access with firewall rules, PostgreSQL
access controls, and TLS where appropriate.

Database credentials
--------------------

The reference Compose file does not set a fixed
``POSTGRES_PASSWORD`` directly. Its comments indicate that the database image
creates a random password unless credentials are explicitly supplied.

Use the installation and Supervisor workflow to manage credentials. Before
replacing or recreating the database service, confirm where the generated
credentials are stored and ensure that a tested backup is available.

Do not change a database password without updating every system and project
configuration that uses it.

Database storage and backup
---------------------------

The ``biomaps_data`` volume contains persistent database data. Copying the
volume while PostgreSQL is actively writing is not, by itself, a guaranteed
consistent database backup. Use PostgreSQL-aware backup tools or the supported
OpenBioMaps archive procedure.

Regularly test restoration into an isolated environment. A backup that has
not been restored successfully should not be considered verified.

To inspect the database service:

.. code-block:: console

   docker compose ps biomaps_db
   docker compose logs --tail=200 biomaps_db

Do not remove the ``biomaps_data`` volume when recreating the service unless
the database is intentionally being deleted and a verified recovery plan
exists.

Separate project database
-------------------------

The reference Compose file contains a commented example for a separate
``gisdata`` database service. If system and project databases are separated:

* adjust Docker network aliases;
* update system and project database host settings;
* configure separate credentials;
* update backup and monitoring procedures; and
* verify access from both ``app`` and ``mapserver``.

Avoid publishing the database port unless clients outside the Docker network
must connect.

Memcached service
=================

The ``memcached`` service provides the application cache. It is addressed as
``memcached:11211`` from the ``app`` container through the private Docker
network.

Memcached does not provide authentication in the reference configuration.
Do not expose its port publicly. If custom Docker networking is used, ensure
that only trusted application services can reach it.

Cached data is disposable and should not be treated as persistent storage.
Restarting or replacing Memcached may clear cached entries without deleting
the underlying OpenBioMaps data.

API service
===========

The ``obm-server-api`` service runs a separate OpenBioMaps API image. It:

* mounts the deployment's ``.env`` file read-only;
* runs its initialisation script before starting Apache; and
* publishes container port 80 as host port 9001 in the reference
  configuration.

Review every value in ``.env`` and restrict file permissions on the Docker
host. The file may contain credentials or other secrets.

Publishing ``9001:80`` makes the API reachable on all host interfaces unless
Docker or firewall configuration limits it. In production, prefer routing the
API through the configured HTTPS reverse proxy or bind it to a restricted
interface.

Inspect API initialisation and runtime errors with:

.. code-block:: console

   docker compose logs --tail=200 obm-server-api

Database administration service
================================

The reference configuration includes Adminer and publishes it on host port
9882.

A database administration interface is security-sensitive. Do not expose it
to the public internet without strong additional access controls. Prefer one
of the following approaches:

* enable it only while performing maintenance;
* bind it to the loopback interface;
* restrict it through a firewall or private network; or
* access it through a secure administrative tunnel.

For example, binding the published port to localhost would use a Compose port
mapping equivalent to ``127.0.0.1:9882:8080``.

Remove or disable the service when it is not required.

Persistent volumes
==================

The reference Compose configuration defines the following named volumes:

.. list-table::
   :header-rows: 1
   :widths: 27 73

   * - Volume
     - Purpose
   * - ``root-private``
     - Private application files under
       ``/var/www/html/biomaps/root-site/private``.
   * - ``projects``
     - Project directories shared by the application and MapServer.
   * - ``var_lib``
     - Persistent OpenBioMaps system data under
       ``/var/lib/openbiomaps``.
   * - ``mapserver_log``
     - Shared MapServer log and temporary files under ``/tmp/mapserver``.
   * - ``etc_openbiomaps``
     - Administrator-managed OpenBioMaps configuration under
       ``/etc/openbiomaps``.
   * - ``biomaps_data``
     - PostgreSQL data under ``/var/lib/postgresql/data``.

Named volumes survive normal container replacement, but they can still be
deleted explicitly. Include all volumes containing required data or
configuration in the backup and disaster-recovery plan.

The Compose file also shows how a named volume can be replaced by a bind
mount. Bind mounts make host paths easier to inspect but require correct
absolute paths, ownership, permissions, and backup procedures.

Configuration workflow
======================

Choose the configuration mechanism according to the type of setting:

.. list-table::
   :header-rows: 1
   :widths: 34 66

   * - Configuration type
     - Recommended mechanism
   * - OpenBioMaps system variables
     - Supervisor and the persistent ``/etc/openbiomaps`` volume.
   * - Project variables
     - Project administration or Supervisor project mode.
   * - Apache settings in ``app``
     - A maintained custom image or explicit configuration mount.
   * - PHP settings
     - INI files mounted into ``/usr/local/etc/php/conf.d``.
   * - MapServer Apache settings
     - Host files mounted into the ``mapserver`` container.
   * - Project mapfiles
     - Project administration or Supervisor, stored in the shared
       ``projects`` volume.
   * - Database settings
     - Compose environment, OpenBioMaps configuration, and the database
       image's supported configuration mechanism.
   * - Secrets
     - Restricted environment files or a dedicated secrets-management
       mechanism.

Do not make important changes only inside a running container. Such changes
are not reproducible and disappear when the container is replaced.

After changing the Compose file:

.. code-block:: console

   docker compose config
   docker compose pull
   docker compose up -d
   docker compose ps
   docker compose logs --tail=200

Review release notes and create a verified backup before upgrades. Avoid
blindly pulling and deploying ``latest`` images on production systems.

Recommended scheduled jobs
==========================

Scheduled tasks can be run from the Docker host through cron or an equivalent
systemd timer. Use absolute paths, capture logs, and ensure that overlapping
runs cannot damage data.

The examples below must be adapted to the installation. Test every command
manually before scheduling it.

Docker updates
--------------

The OpenBioMaps scripts repository contains an automatic update script:

https://github.com/OpenBioMaps/scripts/tree/master/docker-auto-update

Example cron entry:

.. code-block:: cron

   # m h  dom mon dow   command
   0 4,16 * * * /srv/docker/openbiomaps/auto_update.sh > /srv/docker/openbiomaps/system_update_job.log 2>&1

Automatic production updates carry operational risk. Before enabling them,
define:

* how backups are created and verified;
* how database migrations are handled;
* how failed upgrades are detected;
* how image versions are recorded;
* how a rollback is performed; and
* who receives failure notifications.

Archive jobs
------------

The archive script is available at:

https://github.com/OpenBioMaps/scripts/blob/master/obm_archive.sh

It uses ``.archive_list.txt`` and ``obm_archive_settings.sh``. Example
schedule:

.. code-block:: cron

   # m h  dom mon dow   command
   0 2 * * *  /path_to/obm_archive.sh normal
   15 2 * * * /path_to/obm_archive.sh system
   15 3 1 * * /path_to/obm_archive.sh full
   0 5 * * *  /path_to/obm_archive.sh clean
   # Synchronise archives to a remote server
   0 4 * * *  /path_to/obm_archive.sh sync remote_user@remote-server.example /remote_path_to_archives

For Docker installations, follow the instructions at the end of
``obm_archive_settings.sh``.

Store at least one backup outside the OpenBioMaps host. Protect remote backup
credentials and test restoration regularly.

Background job runner
---------------------

Projects that use background jobs require their ``jobs.php`` runner to be
executed regularly.

Example:

.. code-block:: cron

   # m h  dom mon dow   command
   */5 * * * * /usr/bin/docker compose -f /srv/docker/openbiomaps/docker-compose.yml exec -u www-data -T app php /var/www/html/biomaps/root-site/projects/PROJECTTABLE/jobs.php

Replace ``PROJECTTABLE`` with the project's directory or identifier and
verify the path used by the installed release.

Cron runs with a restricted environment. Use the absolute path to Docker and,
if necessary, specify the Compose project directory explicitly. On systems
using the legacy command, the executable may instead be
``/usr/local/bin/docker-compose``.

Create a separate entry for each project that needs background processing.
Monitor exit status and logs, and prevent concurrent executions if a job can
run longer than the scheduling interval.

Operational checks
==================

After installation or configuration changes, check the service state:

.. code-block:: console

   docker compose config
   docker compose ps
   docker compose logs --tail=200 app
   docker compose logs --tail=200 mapserver
   docker compose logs --tail=200 biomaps_db
   docker compose logs --tail=200 memcached

Then verify from the application:

#. Supervisor login works.
#. A public project page loads over HTTPS.
#. An authenticated user can log in and log out.
#. The application can read and write permitted database records.
#. Public and private maps render correctly.
#. File uploads respect the configured limits.
#. Email delivery works if configured.
#. Background jobs are processed.
#. Backups complete and can be restored.
#. Administrative services are not exposed more broadly than intended.

Record the image versions, configuration changes, test results, and rollback
procedure for every production deployment.
