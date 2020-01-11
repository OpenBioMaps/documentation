Openstreetmap szerver létrehozása

Ahhoz, hogy az OBM mobilalkalmazás az OpenStreetMap alaptérképhez offline hozzáférhessen, az OBM közösségnek saját openstreetmap szolgáltató hálózatot kell létrehoznia.
Erre azért van szükség, mert az openstreetmap szervereket rendkívül leterhelné az egyidejű, nagy mennyiségű csempeletöltés, ezért ezt a lehetőséget nem teszik lehetővé a kliensek számára.
Saját OSM szerverekkel azonban kikerülhető ez a probléma.

1. Előkészítés

A szerver létrehozása docker környezetben gyorsan és egyszerűen kivitelezhető.

1.1.: A docker telepítése

Számos szerveren már telepítve van a docker.
A docker -v parancs segítségével megtudhatjuk, milyen verzió fut a szerveren.
Ha hibaüzenetet kapunk, akkor szükség van a docker beállítására.

Debian 9 esetében kövessük az alábbi linken található leírást.

https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-debian-9

1.2.: A docker munkakönyvtár áthelyezése

Alapértelmezetten a docker a a konténereket és köteteket a /var/lib mappában tárolja, ezért célszerű a minkakönyvtárát megváltoztani, és ezeket áthelyezni.

Ehhez segítséget nyújthat az alábbi bejegyzés

https://blog.adriel.co.nz/2018/01/25/change-docker-data-directory-in-debian-jessie/

2. Az openstreetmap szerver telepítése (https://hub.docker.com/r/overv/openstreetmap-tile-server/ alapján)

2.1. Docker Pull parancs

Az alábbi paranccsal tölthetjük le a szervert:

docker pull overv/openstreetmap-tile-server

2.2: Létre kell hozni egy kötetet az alábbi paranccsal:

docker volume create openstreetmap-data

2.3.: Le kell tölteni egy .osm.pbf fájlt, amely tartalmazza a számunkra érdekes terület állományait. Ilyen adatokhoz férünk hozzá például a download.geofabrik.de weboldalon.
Magyarországot például az alábbi linken érhetjük el: http://download.geofabrik.de/europe/hungary.html. A szükséges állomány pedig a http://download.geofabrik.de/europe/hungary-latest.osm.pbf linken található.

Az adatállomány mellett a szolgáltatott terület határát is megadhatjuk a szervernek, így az adatállomány automatikus frissítési is lehetővé válik.

Ehhez a fenti példa alapján a http://download.geofabrik.de/europe/hungary.poly

A letöltött állományokat importálni kell a szerver PotgreSQL adatbázisába:

docker run -v /home/bnpadmin/hungary-latest.osm.pbf:/data.osm.pbf -v /home/bnpadmin/hungary.poly:/data.poly -v openstreetmap-data:/var/lib/postgresql/12/main overv/openstreetmap-tile-server import

Ha a konténer hibaüzenet nélkül kilép, akkor az állomány importálása sikeresen megtörtént (Magyarország esetében is eltarthat akár 10-15 percig is az import.

2.4 A szerver futtatása.

A kiszolgáló a csempéket az első megjelenítés során rendereli, amely ilyenkor lassabb megjelenítést eredményez. Annak érdekében, hogy a csempék egy esetleges újraindítást követően is megmaradjanak, egy önálló köteten kell elhelyezni, az alábbi parancs kiadásával:

docker volume create openstreetmap-rendered-tiles

A későbbiekben az indítás során adjuk meg a csempék mentésének helyét a szervernek.

Ha olyan szerverre telepítjük, ahol már fut egy webkiszolgáló (például az OBM szerver), akkor másik portra kell irányítanunk a konténert.

Az automatikus frissítéseket is az indítás során engedélyezzük.

A fentiek alapján a szervert az alábbi parancs segítségével futassuk:

docker run -p 83:80 -e UPDATES=enabled -v openstreetmap-data:/var/lib/postgresql/12/main -v openstreetmap-rendered-tiles:/var/lib/mod_tile -d overv/openstreetmap-tile-server run

Így a 83-as portot használja majd kifelé az osm szerverünk, az elérési út tehát az alábbi lesz: myserver:83. Pl. obm.bnpi.hu:83

A böngészőben a világtérképet látjuk majd, ahonnan a megfelelő területre nagyítva jelenthetjük meg a csempéinket.



