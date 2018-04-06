Administrative pages
********************

Database columns
----------------

Groups
------

Upload forms
------------
Új form létrehozása

Űrlap tábla kiválasztása: melyik projekt táblára vonatkozik a feltöltő űrlap.

Űrlap neve:

Űrlap hozzáférés: Azoknak a meghatározása akik láthatják/használhatják az űrlapot: bárki, bejelentkezett felhasználóknak, meghatározott csoport.

Űrlap típusa: webes felület, fájl feltöltés, programozott felület

Űrlap leírás:

Űrlap oszlopok:

    tartalmazza?:	ha be van jelölve, akkor jelenik meg az ürlapon az adott oszlop
    kötelező:	ha igen (bordó), akkor az űrlap nem küldhető el, ha nincs kitöltve itt érték
    oszlop:	az adatbázis oszlopk felületen meghatározott - megjelenített oszlop név
    leírás:	rövid leírás a beírandó adatokról
    típus:
        szöveg: tetszőleges szöveg - habár a minimum és maximum hossz megadható
        szám: tetszőleges szám - habár a minimum és maximum hossz megadható
        lista: legördülő lista a megadott vesszővel elválasztott értékekből. A legördülő lista kiírt elemei és valós értékei név:érték formátumban megadhatók. A "név" amennyiben "str_" előtaggal kezdődik, akkor automatikusan lefordul a kiválasztott nyelvi változatra, ha az definiálva van. A "true" és "false" szavak str_true és str_false fordítás szerint fordulnak le. Ha formátuma SELECT:táblanév.oszlopnév, akkor a public.gisdata adatbázis megadott oszlopából készít DISTINCT listát.
        igaz-hamis: boolen false/true érték. Az érték sorrendje a lista definíciós mezőben szabályozható. pl: "false,true"
        dátum: tetszőleges karakterrel elválasztva év hónap nap sorrendben. Adatbázisban date típusként tárolva.
        dátum és idő: üres karektert követően a dátum után óra:perc:másodperc formátumban. Ha hiányzik a másodperc a program automatikusan 00-nak tekinti, de figyelmeztet az elfogadására. Ha hiányzik a perc a program automatikusan 00-nak tekinti, de figyelmeztet az elfogadására. Adatbázisban datetime típusként tárolva.
        idő (timetominutes): óra:perc formátum amit a program egész szám értékké számol át. Adatbázisban egész számként tárolva.
        idő: óra:perc formátum. Adatbázuisban time típusként tárolva.
        idő intervallum: (timeinterval) Pl: 2014-02-25 12:00:00 2014-02-25 13:00:00. Adatbázisban timeinterval típusként tárolva.
        autocomplete: a lista_definíció mezőben megadott sql tábla oszlopából autocomplete listát készít. A szintaxis táblanév.oszlop. A táblát a public sémában keresi a program a gisdata adatbázisban.
        photo id: fotó modul bekapcsolása esetén ide írja be a feltöltött fotó azonosítókat a program.
        geometria: pont: WKT POINT()
        geometria: vonal: WKT LINE()
        geometria: polygon: WKT POLYGON()
        geometria: bármi: WKT
    bevitel hossz:	ellenőrzés a bevitt karakterek számára
    lista definíció:	lista típusnál vesszővel elválasztott lista megadaása. Autocoplete típusnál adatbázis és oszlop megadása "SELECT:" előtaggal. Pl.: SELECT:my_project.species, igaz/hamis típusnál sorrend megadása. Bármilyen listánál ha a kezdő vagy záró karakter vessző, üres elemmel kezdődik vagy zárul a lista. A SELECT típusú listázásnál meg lehet adni egy másik oszlopot ami a listában megjelenő értékeket adja. Pl: SELECT:my_project.species:national_name ami esetben a national_name oszlop értékei jelennek meg a listában, de a hozzá tartozó species elemek lesznek az értékek.
    alap értékek:	A form minden sora számára egységes érték. Lehet kitölthető, választható és fix értéket definiálni.

    ha üres input mezőt szeretnénk, akkor _input értéket kell megadni, ha választó listát szeretnénk kapni a _list értéket kell megadni (a lista fefiníció elemeit tölti be), ha geometra választást, akkor _geometry értéket, az _datum pedig a dátum választó mezőt eredményez.

    api-params:
    relations: Megadható hogy a táblából egy más oszlop értéke esetén az adott oszlopba bevitt értéket hogyan ellenőrízze vagy módosítsa. pl.: weight oszlop esetén ha a sex oszlop tartalma female akkor az értékek min 20 és max 30 numerikus értket vehetnek fel (sex=female) {minmax=20:30}

Oszlopok tartalmának ellenőrzése más oszlopok tartalmának függvényében

Relations pseudolanguage definition:

( rel_field = rel_statement ) { rel_type = rel_value } , ( rel_field = rel_statement ) { rel_type = rel_value } , ...

IF an other cell value (rel_field) match to (rel_statement) THEN  this cell (rel_type) value should be (rel_value)

rel_type is a function related with the field type
     datum:          year            extraxt year component from a datum string
     text,numeric:   minmax          minmax range check
     any type:       obligatory      change obligatory setting
                     inequality      check inequality with these symbols: <>= between index and current field. Causing error message.
rel_statement can be a regexp based function. In this case statement should be started with !! and followed by a regexp expression e.g.  !!^(\d{2})$ 
     If statement is regexp rel_value also can be a function
     .       means replace current cell value with matched string from the matched string from the rel_field
     .+      means append current cell value to matched string from the rel_field 
     +.      means append matched string from the rel_field to the current cell value  

rel_value:
     IF rel_type is inequality according to php comparison operators
             +<.
             +<=.
             +>=.
             +=.
             +<>.
             WHERE + is the matched rel_field value and . is the current cell value
     Else can be anything - may be ignored - depending on the used function

Példa:

tarsus_length oszlopnál

(clutch_size=!!^([123])$) {obligatory(1)}

Ami azt jelenti, hogy kötelező lesz kitölteni a tarsus hosszát, ha a fészekalj mérete 1,2 vagy 3


Form szerkesztése
Új formot lehet létrehozni meglévő form új néven való elmentésével!


Functions
---------

Species names
-------------

Access
------

Language files
--------------

Modules
-------

Saves imports
-------------

File manager
------------

SQL query settings
------------------

Web Map Layers
--------------

Members
-------

Mapserver settings
------------------

Server logs
-----------
