# Fejlesztői tanácsok

## Korábbi MapServer-lemezkép visszaállítása

Listázza az elérhető MapServer-lemezképeket, és keresse meg a legutóbbi, `<none>` címkével ellátott lemezképet:

`docker images | grep mapserver`

Címkézze fel ezt a lemezképet `old` címkével:

`docker tag <ID> openbiomaps/mapserver:old`

Állítsa be a docker-compose.yml fájlban ennek a régi címkének a használatát:

``` yaml
...
mapserver
    image: openbiomaps/mapserver:old
    ...
```

`docker-compose up -d mapserver`


## A PHP opcache kikapcsolása

A /var/www/html/biomaps/project/YOUR_PROJECT/.htaccess fájlban:

php_flag opcache.enable Off


## A pg_top használata

A gazdagépen:

pg_top -W -d "host=localhost user=biomapsadmin dbname=gisdata"
