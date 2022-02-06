Common errors
=============

No data on map or pink map
--------------------------

1) Symptoms: No points on map, no error messages. 
   Problem: If no write permission on mapserver log file the mapserv service will not start on request. 
   Solution: Owner of log file should be the www-data and the mapserver directory in /tmp directory also should be owned by mapserver.
2) Symptoms: No points on map, error messages about connection errors. 
   Problem: Bad hostname in sql connections in the mapfile. 
   Solution: E.g. localhost instead of gisdata in Docker installation.
3) Symptoms: No points on map, error messages about connection errors. 
   Problem: Bad database name in sql connections in the mapfile.
   Solution:
4) Symptoms: No points on map, error messages about connection errors. 
   Problem: Bad password in sql connections in the mapfile. 
   Solution: Try to regenerate the encrypted password string.

No css rules, incorrect appearance of the application
-----------------------------------------------------

1) URL constants should be set up correctly in local_vars.php.inc
2) http and https protocol calls are mixed. Try to set protocol setting in the projects table.

Mobile clients can't connect
----------------------------

1) pds.php missing from the project's root directory
2) 
