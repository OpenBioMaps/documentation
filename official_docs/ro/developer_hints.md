# Sugestii pentru dezvoltatori

## Restaurarea imaginii MapServer anterioare

Enumerați imaginile MapServer disponibile și identificați-o pe cea mai recentă care are eticheta `<none>`

`docker images | grep mapserver`

Etichetați această imagine drept old:

`docker tag <ID> openbiomaps/mapserver:old`

Configurați docker-compose.yml să utilizeze această etichetă veche:

``` yaml
...
mapserver
    image: openbiomaps/mapserver:old
    ...
```

`docker-compose up -d mapserver`


## Dezactivarea PHP OPcache

În fișierul /var/www/html/biomaps/project/YOUR_PROJECT/.htaccess:

php_flag opcache.enable Off


## Utilizarea pg_top
Pe mașina gazdă

pg_top -W -d "host=localhost user=biomapsadmin dbname=gisdata"
