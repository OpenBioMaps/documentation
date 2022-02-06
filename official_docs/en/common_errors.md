Troubleshooting
===============

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

Mobile or R clients can't connect
---------------------------------

1) Symptoms: No error messages, just can't connect..
   Problem: pds.php missing from the project's root directory
   Solution: copy the missing file from an other project
2) Symptoms: No projects listed on my server
   Problem: A bad url registered in openbiomaps.org/openbiomaps_networks
   Solution: Go to https://openbiomaps.org/openbiomaps_network/ and modify your project domain (beginning with protocol: http or https !).
3) Symptoms: There are lots of strange and unexpeted error messages.
   Problem: The *pds* and/or *oauth* is not up-to-date in the default project (usally the *sablon* project)
   Solution: update these *pds* and *oauth* direcories with supervisor. Check your system_vars.php.inc for the DEFAULT_PROJECT. If is not set there, the default project is the *sablon*.
4) Symptoms: Mobile client not listing your server
   Problem: Your server is not registered in openbiomaps.org/openbiomaps_networks
   Solution: Go to https://openbiomaps.org/openbiomaps_network/ and register your project.
