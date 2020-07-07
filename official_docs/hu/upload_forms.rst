.. _manage-upload-forms:

Adatfeltöltő űrlapok kezelése
=============================

Űrlapok listája
--------------------
Űrlapokat lehet kiválasztani szerkesztésre, törölésre vagy a használatból való letiltásra.


Űrlap fejléc beállítások
------------------------

.. _destination-table:

Űrlap tábla kiválasztása
........................
melyik projekt táblára vonatkozik a feltöltő űrlap.

.. _name-of-the-form:

Űrlap neve
..........
Az űrlap nevét lehet megadni, amelynek egyedinek kell lennie egy projektben.

Egy űrlapról másolat készíthető annak átnevezésével.

Az űrlap neve többnyevű is lehet, ha _str előtaggal van megadva és a projekt nyelvi beállításokban meg van adva az adott nyelvi definíció minden egyes nyelvre.

.. _form-access:

Űrlap hozzáférés
................
Azoknak a meghatározása akik láthatják/használhatják az űrlapot: bárki, bejelentkezett felhasználóknak, meghatározott csoport.

.. _group-access:

Csoport hozzáférés
..................
Amennyiben "csoport hozzáférés" van megadva az űrlap hozzáférésre, akkor itt lehet megadni a csoportokat

.. _data-access:

Adat hozzárendelés
..................
A feltölött adatoknak az itt megadott csoportoknak lesz hozzáférése. Alapesetben a feltöltőnek van írási és olvasási hozzáférése az adatokhoz és a projekt globális beállításai érvényesülnek.

.. _form-type:

Űrlap típusa
............
webes felület, fájl feltöltés, API (pl. mobil alkalmazás)

.. _form-description:

Űrlap leírás
............
Tetszőleges leírás az űrlaphoz. Fordítható ez is.

.. _form-srid:

Űrlap térbeli referencia rendszer
.................................
Bármilyen térbeli referencia rendszer választható amelybeől a feltöltött adatok származnak amely elérhető az  https://spatialreference.org/ oldalon. It egy vesszővel elávlasztott felsorolás definiálható az adott űrlap számára eléhető referncia rendszerek megadására a következő módon: srid:címke,srid:címke. Pl.: "4326:wgs84,23700:eov"

.. _form-groupping:

Csoportosítás
.............
Az űrlapok csoportokba rendezhetőek a webes űrlap választó felületen való megjelenítéshez (a mobilon még nem elérhető ez az opció)

.. _form-publish:

Űrlap publikálás
................
Az űrlapok lezárhatók publikálással (narancssárga gomb az űrlap fejléc területen). A publikált űrlapok minden további módosítása egy új verzió készítését okozzák. A korábbi verziók elérhetőek maradnak minden API kliens számára, pl. mobil alkalmazás. A publikált űrlapokból teszt verziók készthetőek (teszt verzió készítése gomb a lap alján). A teszt verzók csak annak késztője számára elérhetőek (alapbeállítás szerint). A teszt verziók publikálhatóak a saját publikált águkba.



Űrlap mező definíciók
---------------------

.. _included:

Tartalmazza
...........
ha be van jelölve, akkor jelenik meg az ürlapon az adott oszlop

.. _column-order:

Oszlop sorrend
..............
itt állatható egyedileg az űrlapra az oszlopsorrend

.. _column:

Oszlop
......
Két szó szerepel itt egymás alatt. A megjelenített oszlop név, amely szerkeszthető, amivel egyedivé lehet tenni minden űrlapra.
A másik az oszlop neve az adattáblában.

.. _obligatory:

Kötelező
........
	- Ha `igen` (háttérszín: bordó), akkor az űrlap nem küldhető el, ha nincs megadva a mezőben érték;
	- Ha `nem` (háttérszín: szürke), akkor be lehet az adott mező üres;
	- Ha `puha hiba`, akkor az adatfeltöltő minden egy sorra figyelmeztetést, ha a mező üres, vagy eltérések vannak benne a megkötésektől. Soronként egyesével meg kell erősíteni, hogy megengedi az adott eltéréseket.

.. _column-description:

Mező leírás
...........
rövid leírás a mezőről. Fordítható.

.. _column-type:

Mező típusa
...........

        - szöveg: tetszőleges szöveg - habár a minimum és maximum hossz megadható
        
        - szám: tetszőleges szám - habár a minimum és maximum hossz megadható
        
        - lista: legördülő lista a megadott vesszővel elválasztott értékekből. A legördülő lista kiírt elemei és valós értékei név:érték formátumban megadhatók. A "név" amennyiben "str\_" előtaggal kezdődik, akkor automatikusan lefordul a kiválasztott nyelvi változatra, ha az definiálva van. A "true" és "false" szavak str_true és str_false fordítás szerint fordulnak le. 

            Megadható több címke egy értékhez amikből webes űrlapesetén az első jelenik meg, file feltöltésnél pedig a fájl cella értékéből bármelyik cimke vagy az érték helyes egyezést ad. A cimkéket # karakterekkel tagolva kell megadni. Pl: female#tojó:f,male#hím#him:m,juvenil#fiatal:j,adult#öreg:a
        
            Ez esetben az "f" érték lehetséges cimkéi a "female", "tojo" és "tojó" szavak
        
            Ha formátuma SELECT:táblanév.oszlopnév, akkor a public.gisdata adatbázis megadott oszlopából készít DISTINCT listát.
        
        - igaz-hamis: boolen false/true érték. Az érték sorrendje a lista definíciós mezőben szabályozható. pl: "false,true"
        
        - dátum: tetszőleges karakterrel elválasztva év hónap nap sorrendben. Adatbázisban date típusként tárolva.
        
        - dátum és idő: üres karektert követően a dátum után óra:perc:másodperc formátumban. Ha hiányzik a másodperc a program automatikusan 00-nak tekinti, de figyelmeztet az elfogadására. Ha hiányzik a perc a program automatikusan 00-nak tekinti, de figyelmeztet az elfogadására. Adatbázisban datetime típusként tárolva.
        
        - idő (timetominutes): óra:perc formátum amit a program egész szám értékké számol át. Adatbázisban egész számként tárolva.
        
        - idő: óra:perc formátum. Adatbázuisban time típusként tárolva.
        
        - idő intervallum: (timeinterval) Pl: 2014-02-25 12:00:00 2014-02-25 13:00:00. Adatbázisban timeinterval típusként tárolva.
        
        - autocomplete: a lista_definíció mezőben megadott sql tábla oszlopából autocomplete listát készít. A szintaxis táblanév.oszlop. A táblát a public sémában keresi a program a gisdata adatbázisban.
        
        - autocompletelist: hasonló az autocomplet-hez, de egymás után több, vesszővel elválasztott értéket is bevihetünk a mezőbe
        
        - photo id: fotó modul bekapcsolása esetén ide írja be a feltöltött fotó azonosítókat a program.
        
        - geometria: pont: WKT POINT()
        
        - geometria: vonal: WKT LINE()
        
        - geometria: polygon: WKT POLYGON()
        
        - geometria: bármi: WKT
        
        - colour rings: színesgyűrű kombináció megadására ad lehetőséget, ahol piros, rózsaszín, zöld, világos zöld, narancs, sárga, kék, világos kék, fehér, fekete, barna, lila, ibolya és fémgyűrű kombinációkat lehet létrehozni. A szögletes zárójelben levő rész a különböző láb-részeken megadandó maximális gyűrűk számát kódolja, az ezt követő rész a lehetséges színek egyénileg megadott cimkéi. Pl: [XX],Blue:B, red:R, green:G

.. _input-control:

bevitel kontrol
...............
a bevitt karakterek számának ellenőrzése
        - nincs ellenőrzés
        - min - max
        - regexp
        - térbeli
        - egyéni ellenőrzés

.. _list-definition:

Lista definíció
...............
Többféle lista definíció megadható itt. Egyszeres választós lista, többszörös választós, autó-kiegészítős lista. A listák tartalma megadható itt is az elemek felsorolásával, vagy megadható egy tábla és feltételek ahonnan az alkalmazás lekérdezi a lista elemeket.

Ha az általunk definiált lista kevés választható elemet tartalmaz, akkor ezt listát akár felsorolással is megadhatjuk. Lásd alább - ebben az esetben megadtuk a listánk értékeit, amit egy legördülő menüből tudunk majd kiválasztani a adatfeltöltés folyamán. Ezek az értékek ("nőstény", "hím") fognak az adatbázisba is bekerülni.

.. code-block:: json

    {
      "list": {
        "nőstény":[],
        "hím":[]
       }
    }

Abban az esetben, ha egyes változókat más írási móddal, vagy más formában szeretnénk megjeleníteni. Például, ha a változó értéke szám, de a listában szöveges leírást akarunk megjeleníteni, akkor lehetőség van az értéktől éltérő cimkék megadására. A cimke értékek automatikusan fordíthatóak is, ha az str_ előtagot használjuk és a nyelvi fordítást megadtuk. Így az alábbi példában az adatbázisban "male" és "female" értékek fognak bekerülni, de a legördülő listában "nőstény" és "hím" értékek jelennek meg magyarul és "female", "male" angolul.

.. code-block:: json

    {
      "list": {
        "female":["str_female"],
        "male":["str_male"]
       }
    }


Lehetőség van több cimke hozzárendeléséhez is egy értékhez. Ebben az esetben weves űrlapon és mobilon a lista első eleme fog megjelenni, de fájlfeltöltés esetén a a fájlban szerepelhet bármelyik cimke vagy érték, mindegyikből a lista értéket fogja az alkalmazás beszúrni. Ahhoz, hogy ez érvényesüljön jelenleg végig kell lapozni a fájlt.

.. code-block:: json

    {
      "list": {
        "nőstény":[
        	"nősteny",
        	"F",
        	"female"],
        "hím":[
                "hím",
        	"M",
        	"male"]
       }
    }

A lista teljes definíciós leírása az alább látható JSON. Ennek összeállítását segíti a webes felületeten a lista szerkesztő és automatikusan ellenőrzi a szintaxisát az alkalmazás. Hibás szintaxis esetén hibaüzenetet kapunk.

.. code-block:: json

    {
      "list": {
            "val1": ["label1", "label2"]
      },
      "optionsTable": "",
      "valueColumn": "",
      "labelColumn": "",
      "filterColumn": "",
      "pictures": {
            "val1": "url-string"
      },
      "triggerTargetColumn": "",
      "Function": "",
      "disabled": ["val1"],
      "preFilterColumn": "",
      "preFilterValue": "",
      "multiselect":"true or false, default is false",
      "selected":["val1"]
    }

Kapcsolt listák kezelése: 
.........................

Létrehozunk egy listát egy olyan oszlopban (indító oszlop), ami meghatározza a befolyásolt oszlopban létrejövő listát ("lista a listában"). Ehhez először létre kell hozzunk egy olyan háttér táblát (állat_csoportok), ami tartalmazza hogy egy csoporton belül milyen kisebb csoportok helyezkednek el. Például tartalmaznia kell, hogy a nagyobb állatcsoportokon belül milyen kisebb egységek fordulnak elő. Tehát a gerincesek csoporton (állat_szupercsoport) belül találhatóak a kétéltűek, hüllők, madarak, emlősök (állat_csoport_nev) és a gerinctelen csoporton (állat_szupercsoport) belül pedig a csalánozók, ízeltlábúak (állat_csoport_nev) stb.

A kapcsolt listák paramétereit a "lista definíciók" mezőben adjuk meg JSON kód segítségével. 

A kód első felét az indító oszlopunkhoz írjuk be, itt határozzuk meg, hogy az indító oszlopunk melyik háttértábla oszlopból vegye ki az értékeket:

.. code-block:: json

    {
    "triggerTargetColumn": [
        "befolyásolt_lista_neve"
    ],
   "Function": "select_list",
    "optionsSchema": "shared",
    "optionsTable": "allat_csoportok",
    "valueColumn": "allat_szupercsoport",
    "labelColumn": "allat_csoport_nev",
    "labelAsValue": true
    }

Kód magyarázat:
	"Function" - mindig "select_list"
	"optionsSchema" - mindig "shared"
	"optionsTable" - "háttér_tábla_neve"
	"valueColumn" - a háttér táblából kiválasztott oszlop, aminek a változóiból létrejön a legördülő lista, abban az oszlopban ahova a kód kerül (indító oszlop)
	"labelColumn" - a befolyásolt oszlopban hoz létre egy olyan listát, ami függ attól hogy melyik opciót választottuk az indító oszlop listájából

A kód második felét a befolyásolt oszlopunkba kell beírni, itt határozzuk meg, hogy a befolyásolt oszlopunk melyik háttértábla oszlopból vegye ki az értékeket:

.. code-block:: json

    {
    "optionsTable": "allat_csoportok",
    "valueColumn": "allat_csoport_név",
    "labelColumn": "allat_csoport_név",
    "filterColumn": "allat_szupercsoport",
    "Function": "select_list",
    "optionsSchema": "shared"
    }

Kód magyarázat (csak az új változókat határozom itt meg):
	"filterColumn" - meghatározza, hogy melyik oszlop volt az indító oszlop

A kapcsolt lista opcióval nem csak két oszlop listáit tudjuk összekapcsolni, hanem több oszlopét is. Tehát ha a háttér táblánkban azt is definiáltuk, hogy a kisebb állatcsoportokhoz (állat_csoport_név) mely fajok tartoznak, akár kétszeres de több változó bevonásával akár ötszörös vagy tízszeres kapcsoltsági hálót is létre tudunk hozni. Az indító és a végső oszlop közötti oszlopokhoz a következő kód tartozik:

.. code-block:: json

    {
    "optionsSchema": "shared",
    "optionsTable": "allat_csoportok",
    "filterColumn": "allat_szupercsoport",
    "Function": "select_list",
    "valueColumn": "allat_csoport_nev",
    "triggerTargetColumn": [
        "species"
    ],
    "labelColumn": "allat_csoport_nev"
    }

A "triggerTargetColumn" mindig a soron következő oszlopra mutasson. A "filterColumn" mindig előző oszlopra mutasson. A "valueColumn" és a "labelColumn" mindig az aktuális oszlopra mutasson.

További példák:
1. Településeken belüli épületek meghatározása. Adatokat gyűjtünk különböző mesterséges odúkban fészkelő fajokról. Az erre létrehozott feltöltő formon belül szeretnénk létrehozni egy autocomplete a település oszlopban. Majd az épület (ahova az odút kihelyezték) oszlopban is szeretnénk egy legördülő menüt létrehozni. A háttértáblánk épület oszlopa viszont rengeteg lehetséges épületet jelöl, de ezek nem mindegyike fordul elő az összes településen. Ennek tükrében szeretnénk összekötni a település és épület oszlopot méghozzá úgy, hogy a kiválasztott település megszűrje az épület oszlopban kialakuló listát

ELSŐ LÉPÉS: beállítjuk a település oszlop autocomplete listáját, úgy hogy az oszlop típusát autocomplet-re állítjuk, majd megadjuk hogy az itt kialakult lista befolyásolja az épület listánkat:

.. code-block:: json

{
    "triggerTargetColumn": [
        "epulet"
    ],
    "Function": "select_list",
    "optionsSchema": "public",
    "optionsTable": "tytoalba_epuletek",
    "valueColumn": "telepules"
}

MÁSODIK LÉPÉS: létrehozzuk a legördülő listánkat az épület oszlopban:

.. code-block:: json

{
    "optionsTable": "tytoalba_epuletek",
    "filterColumn": "telepules",
    "Function": "select_list",
    "valueColumn": "epulet"
}


.. _default-values:

Alap értékek
............
A form minden sora számára egységes érték. Lehet kitölthető, választható és fix értéket definiálni.

        Ha üres input mezőt szeretnénk, akkor _input értéket kell megadni, ha választó listát szeretnénk kapni a _list értéket kell megadni (a lista fefiníció elemeit tölti be), ha geometra választást, akkor _geometry értéket, az _datum pedig a dátum választó mezőt eredményez.

.. _field-display-options:

Mező megjelenítési opciók
.........................
    - sticky (rajzszög)
        A mobil alkalmazásban van igazi jelentősége. A stickyvel jelölt mezők értéke megmarad mindaddig amíg a felhasználó nem ad meg más értéket.
    - hidden (rejetett)
        A mező nem fog látszani. A webes felületeten és a mobil alkalmazásban is működik.
    - read only (csak olvasható)
        A mező értéke nem módosítható.
    - once (egyszer)
        Ez a mező csak egyszer jelenik meg egy megfigyelési lista típusú adatfelvételnél a lista lezárásakkor.
        (Később ez az opció fogja majd a mező kiemeléseket csinálni a webes felületeten)
    - list element as buttons (lista elemek gombonként)
        A lista elemei különálló gombonkként fognak megjelenni az űrlapon. A mobil alkalmazásban és a webes felületen is működik.
        A gombok pictogrammok is defiiálhatók. Ezt a lista definícióban lehet megadni. Pl:

.. code-block:: json
	
	{
          "pictures": {
            "animals": "http://....png",
            "plants": "http://....png",
            "mushrooms": "http://....png",
            "bats": "http://....png"
            }
	 }

.. _column-relations:

Kapcsolat más oszloppal
.......................
Oszlopok tartalmának ellenőrzése más oszlopok tartalmának függvényében
        Megadható hogy a táblából egy más oszlop értéke esetén az adott oszlopba bevitt értéket hogyan ellenőrízze vagy módosítsa. pl.: weight oszlop esetén ha a sex oszlop tartalma female akkor az értékek min 20 és max 30 numerikus értket vehetnek fel (sex=female) {minmax=20:30}

.. _pseudo-column:

Pszeudo oszlopok
................
Más űralpokból átemelhetőek egyes oszlopok ezzel a funkcióval. form-név:oszlop1,oszlop2,oszlopN. Az itt megadott oszlopok a megadott mező után jelennek meg. Ezzel a funkcióval elérhető, hogy egyszerre két adattáblába lehessen feltölteni adatokat.


Kapcsolat más oszlopkkal definíció nyelv
----------------------------------------

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
