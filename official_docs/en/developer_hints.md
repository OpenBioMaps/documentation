# Developer hints

## Restore previous mapserver image

List the available mapserver images and find the latest with the `<none>` tag

`docker images | grep mapserver`

Tag this image as old:

`docker tag <ID> openbiomaps/mapserver:old`

Point the docker-compose.yml to this old tag:

``` yml
...
mapserver
    image: openbiomaps/mapserver:old
    ...
```

`docker-compose up -d mapserver`


## Turn off php opcache

In the /var/www/html/biomaps/project/YOUR_PROJECT/.htaccess file:

php_flag opcache.enable Off


## Using pg_top
On host machine

pg_top -W -d "host=localhost user=biomapsadmin dbname=gisdata"
