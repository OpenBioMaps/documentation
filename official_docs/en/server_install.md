# Installing a new OpenBioMaps server

This page provides a short overview of server installation and the most
important project-level settings in `local_vars.php.inc`.

Most installations should use the Docker-based environment. After installing
the server, use the Supervisor interface to manage low-level system and
project configuration.

> **Important:** The examples below are configuration examples, not a
> complete configuration file. Review every value before using it. Do not
> commit passwords, client secrets, encryption keys, or other credentials to
> a source-code repository.

## Installing OpenBioMaps with Docker

For the supported Docker-based installation process, see:

:doc:`Docker installation tutorial <docker>`

## Troubleshooting installations and updates

For common problems encountered after a new installation or an update, see:

:doc:`Common errors <common_errors>`

## Server configuration

For system-level settings, Supervisor, PHP, MapServer, and recommended cron
jobs, see:

:doc:`Server configuration <server_config>`

## Project-level configuration

Several low-level project settings are stored in `local_vars.php.inc`. The
file is normally maintained by a server administrator through the
project-specific mode of the Supervisor interface.

Settings available through the regular project-administration interface
should generally be managed there. Edit `local_vars.php.inc` only when the
required option is not available through that interface.

The location of the file depends on the installation and project. In a
standard Docker installation, it is located in the project's directory
under the OpenBioMaps web application.

After changing the file:

1. check the PHP syntax;
2. reload the affected project page;
3. inspect the application and server logs for errors; and
4. test the relevant function with an appropriate user account.

## Database connection

These constants define the project's PostgreSQL connection.

Use a strong, unique password and store it securely.


