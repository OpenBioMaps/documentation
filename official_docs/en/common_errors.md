Troubleshooting
===============

No data on the map or pink map
------------------------------

1) Symptoms: No points on the map, and no error messages. 
   
   Problem: If no write permission on the MapServer log files the mapserv service will not start on request. 
   
   Solution: The owner of the log file should be the www-data and the MapServer directory in /tmp directory also should be owned by www-data user.

2) Symptoms: No points on the map, and no error messages.
   
   Problem: The assignment between OpenLayers and SQL queries is missing or incorrect.
   
   Solution: Check SQL queries to see if an SQL query is set for that table, and then see if Map Settings has an OpenLayers assignment to that SQL query (which starts the Map Server query).

3) Symptoms: No points on the map, and there are error messages about connection errors. 
   
   Problem: Invalid hostname provided in SQL connections in the map file. 
   
   Solution: Update your connection, e.g. gisdata instead of localhost.

4) Symptoms: No points on the map, and there are error messages about connection errors. 
   
   Problem: Invalid database name provided in SQL connections in the map file.
   
   Solution: Update your connection, e.g. biomaps_db.

5) Symptoms: No points on the map, and there are error messages about connection errors. 
   
   Problem: Bad password (or missing password) in SQL connections in the map file. 
   
   Solution: Try to regenerate the encrypted password string.

The incorrect appearance of the application, e.g. no profile page
-----------------------------------------------------------------

1) Problem: PHP Fatal error. Missing Composer Package.
   
   Solution: Composer update needed

2) Problem: PHP Fatal error. Missing files for a Composer Package.
   
   Solution: The supervisor couldn't copy all the necessary files, try to copy them manually.


No CSS rules, the incorrect appearance of the application
---------------------------------------------------------

1) Problem: CSS and js files not loaded (not found)

   Solution: URL constants should be set up correctly in local_vars.php.inc

2) Problem: HTTP and HTTPS protocol calls are mixed. 
   
   Solution: Try to set protocol settings in the projects table.

3) Problem: If you are using a forwarded proxy, the HTTP_X_FORWARDED_* headers are missing
   
   Solution: Put X-FORWARD headers into your host's webserver (apache) config file:
   ```
      RequestHeader set X-Forwarded-Proto 'https'
      RequestHeader set X-Forwarded-Host 'YOURDOMAIN'
      RequestHeader set X-Forwarded-Port "443"
   ```

Mobile or R clients can't connect
---------------------------------

1) Symptoms: No error messages, just can't connect...
   
   Problem: pds.php is missing from the project's root directory.
   
   Solution: Copy the missing file from another project

2) Symptoms: No projects listed on my server
   
   Problem: A bad url registered in openbiomaps.org/openbiomaps_networks
   
   Solution: Go to https://openbiomaps.org/openbiomaps_network/ and modify your project domain (beginning with protocol: HTTP or HTTPS !).

3) Symptoms: There are lots of strange and unexpected error messages.
   
   Problem: The *pds* and/or *oauth* is not up-to-date in the default project (usally the *sablon* project)
   
   Solution: Update *pds* and *oauth* directories with the Supervisor. Check your system_vars.php.inc for the DEFAULT_PROJECT. It is not set there, the default project is the *sablon*.

4) Symptoms: Mobile client does not list your server
   
   Problem: Your server is not registered in openbiomaps.org/openbiomaps_networks
   
   Solution: Go to https://openbiomaps.org/openbiomaps_network/ and register your project.
