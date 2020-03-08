.. _new-upload-form:

Create new data upload form
---------------------------

Destination table
.................
Which project table the upload form applies to.

Name of the form
................
Please enter a name for your upload form!

This name can be multilingual, if you use the ''str_'' tag. See more about translations :ref:`translations`

Form access
...........
Define who can see / use the form: anyone, logged in users, specific group.

Form type
.........
Should be at least one from the following three options:

web form, file upload form, API (externally accessible form, e.g. mobile app)

Form description
................
A shorter or longer description of the form. This can be used to give instructions for uploaders.

Form columns
............

    - included?:	If checked, the column will appear on the form.
    
    - column order: It is a small empty input box (by default) next to "included" option.
    
    - obligatory:	If yes (burgundy), then the form cannot be submitted without filling in the column cell.
    
    - column:	
        - The visible name of the column. It can be edited to make it unique to a form.
        - The original name of the column.
    
    - description:	Short description of the field.
    
    - type:
    
        - text: arbitrary text - minimum and maximum lengths can be specified.
        
        - numeric: arbitrary number - minimum and maximum lengths can be specified
        
        - list: legördülő lista a megadott vesszővel elválasztott értékekből. A legördülő lista kiírt elemei és valós értékei név:érték formátumban megadhatók. A "név" amennyiben "str\_" előtaggal kezdődik, akkor automatikusan lefordul a kiválasztott nyelvi változatra, ha az definiálva van. A "true" és "false" szavak str_true és str_false fordítás szerint fordulnak le. 
        Megadható több címke egy értékhez amikből webes űrlapesetén az első jelenik meg, file feltöltésnél pedig a fájl cella értékéből bármelyik cimke vagy az érték helyes egyezést ad. A cimkéket # karakterekkel tagolva kell megadni. Pl: female#tojó:f,male#hím#him:m,juvenil#fiatal:j,adult#öreg:a
        
        Ez esetben az "f" érték lehetséges cimkéi a "female", "tojo" és "tojó" szavak
        
        - true-false: boolen false/true value. Az érték sorrendje a lista definíciós mezőben szabályozható. pl: "false,true"
        
        - date: tetszőleges karakterrel elválasztva év hónap nap sorrendben. Adatbázisban date típusként tárolva.
        
        - date and time: üres karektert követően a dátum után óra:perc:másodperc formátumban. Ha hiányzik a másodperc a program automatikusan 00-nak tekinti, de figyelmeztet az elfogadására. Ha hiányzik a perc a program automatikusan 00-nak tekinti, de figyelmeztet az elfogadására. Adatbázisban datetime típusként tárolva.
        
        - time: (timetominutes): hours:minutes formátum amit a program egész szám értékké számol át. Adatbázisban egész számként tárolva.
        
        - time: hours:minutes. As time type in the database.
        
        - time interval: (timeinterval) Pl: 2014-02-25 12:00:00 2014-02-25 13:00:00. Adatbázisban timeinterval típusként tárolva.
        
        - autocomplete: a lista_definíció mezőben megadott sql tábla oszlopából autocomplete listát készít. A szintaxis táblanév.oszlop. A táblát a public sémában keresi a program a gisdata adatbázisban.

        - autocompletelist: Similar to the autocomplete field, just here it is possible autocompleting multiple values into a single field
        
        - photo id: fotó modul bekapcsolása esetén ide írja be a feltöltött fotó azonosítókat a program.
        
        - geometria: point: WKT POINT()
        
        - geometria: line: WKT LINE()
        
        - geometria: polygon: WKT POLYGON()
        
        - geometria: any: WKT
        
        - colour rings: színesgyűrű kombináció megadására ad lehetőséget, ahol piros, rózsaszín, zöld, világos zöld, narancs, sárga, kék, világos kék, fehér, fekete, barna, lila, ibolya és fémgyűrű kombinációkat lehet létrehozni. A szögletes zárójelben levő rész a különböző láb-részeken megadandó maximális gyűrűk számát kódolja, az ezt követő rész a lehetséges színek egyénileg megadott cimkéi. Pl: [XX],Blue:B, red:R, green:G
        Megengedett színek és jelölések: 
            R = 'red'
            P = 'pink'
            G = 'green'
            g = 'lightgreen'
            O = 'orange'
            Y = 'yellow'
            B = 'blue'
            b = 'lightblue'
            W = 'white'
            K = 'black'
            N = 'brown'
            U = 'purple'
            V = 'violet'
            M = 'silver'

        
    - input control: checks the number of characters entered
        - no check
        - min - max
        - regular expression
        - spatial
        - custom check
    
    - list definítion:	lista típusnál vesszővel elválasztott lista megadaása. Autocoplete típusnál adatbázis és oszlop megadása "SELECT:" előtaggal. Pl.: SELECT:my_project.species, igaz/hamis típusnál sorrend megadása. Bármilyen listánál ha a kezdő vagy záró karakter vessző, üres elemmel kezdődik vagy zárul a lista. A SELECT típusú listázásnál meg lehet adni egy másik oszlopot ami a listában megjelenő értékeket adja. Pl: SELECT:my_project.species:national_name ami esetben a national_name oszlop értékei jelennek meg a listában, de a hozzá tartozó species elemek lesznek az értékek.
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
      "selected":["val1"],
    }
    
    - default values:	Uniform value for each line of the form. You can define a fill value, an optional value, and a fixed value.

    Ha üres input mezőt szeretnénk, akkor _input értéket kell megadni, ha választó listát szeretnénk kapni a _list értéket kell megadni (a lista fefiníció elemeit tölti be), ha geometra választást, akkor _geometry értéket, az _datum pedig a dátum választó mezőt eredményez.

    - api-params:
    relations: Megadható hogy a táblából egy más oszlop értéke esetén az adott oszlopba bevitt értéket hogyan ellenőrízze vagy módosítsa. pl.: weight oszlop esetén ha a sex oszlop tartalma female akkor az értékek min 20 és max 30 numerikus értket vehetnek fel (sex=female) {minmax=20:30}

Check the contents of columns depending on the contents of other columns


Relations pseudolanguage definition
-----------------------------------

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

Example:

at the tarsus_length column

(clutch_size=!!^([123])$) {obligatory(1)}

Which means it will be mandatory to fill the tarsus length if the nest size is 1, 2 or 3

.. _edit-upload-form:

Edit forms
----------
Existing forms can be selected for editing. Forms can be deleted or blocked.
By renaming the forms, a new name will be created for the form!
