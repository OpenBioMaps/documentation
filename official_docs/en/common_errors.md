Common errors
=============

No data on map or pink map
--------------------------

1) No write permission on mapserver log file. Owner that files should be www-data and the mapserver directory in /tmp also should be owned by mapserver
2) Bad hostname in sql connections in the mapfile. E.g. localhost instead of gisdata in Docker installation.
3) Bad database name in sql connections in the mapfile.
4) Bad password in sql connections in the mapfile. Try to regenerate the encrypted password string.

No css rules, incorrect appearance of the application
-----------------------------------------------------

1) URL constants should be set up correctly in local_vars.php.inc
2) http and https protocol calls are mixed. Try to set protocol setting in the projects table.

Mobile clients can't connect
----------------------------

1) pds.php missing from the project's root directory
2) 
