.. _manage-upload-forms:

Upload form management
======================

List of available forms
-----------------------
Existing forms can be selected for editing or can be deleted or blocked from use.


Form header definition
----------------------

Destination table
.................
Which project table does the upload form apply to?

Name of the form
................
The name for the upload form. This should be unique within a project.

You can make a copy of a form by renaming it.

This name can be multilingual if you use the ''str_'' tag. See more about translations :ref:`translations`

Form access
...........
Define who can see/use the form:

- public (anyone), 
- all logged-in users, 
- only specified groups
	
If "only specified groups" are chosen,  the list of available users/groups select field will be active, where users or groups can be chosen for accessing this form.

Data access
...........
Uploaded data will only be available to the specified groups here. By default, data can be read and edited by the uploader.

Form type
.........
There should be at least one of the following three options:

web form, file upload form, API (externally accessible form, e.g. mobile app)

Form description
................
A shorter or longer description of the form. This can be used to give instructions to uploaders.

Form SRID
.........
Any kind of spatial reference can be chosen for the uploaded which is available at https://spatialreference.org/. The default SRID is "epsg:4326 (WGS84)". If a list of spatial references is specified here, uploaders can choose only from these options. 
Use the following format to define a list of available references: "4326:wgs84,23700:eov". It is a comma-separated list of EPSG reference ID and visible labels.

Form groupping
..............
Form can be organized into groups for the form choose interface on the web form. The group names can be defined or chosen here.
This option is not available on the mobile app yet.

Form publish
............
A form can be locked by publishing it (orange publish button in the form-header area). Any updates on a published form create a new version of the form. The old versions are available for API clients (mobile-app). A draft version can be created from the published forms for testing (create a draft version button at the bottom of the page). The draft version is only available to the creator of the draft (by default). The draft version can be published in the published branch of the form.

.. observationlists:

Observation list
................
A series of observations can be combined, for example, observations of transect counting or observations of time limit counting. A time limit (in minutes) can be set, when reached the mobile application will warn when the time is up, but nothing else happens, and the user can continue the observation. A forced observation list means that the form can only be started in list mode, as an individual the user can also start a list observation with the form if this option is enabled.

.. tracklog:

Tracklog
........
Automatic tracklog recording while using the form.

.. periodic-notification:

Periodic notification
.....................
At specified intervals (minutes), the app will alert you to record a new observation. Meanwhile, the counter runs continuously. When the user records an observation, the timer will always restart.


Form column definitions
-----------------------

Included
........
If checked, the column will appear on the form.
    
Column order
............
It is a small empty input box (by default) next to the "included" option.

Column
......
There are two strings here: The visible name of the column (it can be edited to make it unique to a form), and the original name of the column.
    
Obligatory
..........
Three options are available here: yes, no, soft-error

- Yes (colour: burgundy), then the form cannot be submitted without filling in the column cell.
- No (colour: grey), then the form can be submitted with an empty cell in the  rows with this column.
- Soft-error (colour: pink), allows empty cells or differences from restrictions but the uploader should confirm this for every affected line.
    
Column description
..................
Short description of the field.
    
Column type
...........
- text: arbitrary text - minimum and maximum lengths can be specified.     
- numeric: arbitrary number - minimum and maximum lengths can be specified
- list: drop-down list, with one selectable item by default
- true-false: boolean false/true value. The order of the value can be controlled in the list definition field. e.g. "false,true"
- date: Separated by any character in order of year month day. Stored in the database as a date type.
- date and time: after a blank frame, the date is in hour:minute:second format. If a second is missing, the program automatically considers it as 00, but warns you to accept it. If the minute is missing, the program will automatically treat it as 00 but warn to accept it. Stored in the database as datetime type.
- time: (timetominutes): hours:minutes format which the program converts to an integer value. Stored in the database as an integer.
- time: hours:minutes. As time type in the database.
- time interval: (timeinterval) Pl: 2014-02-25 12:00:00 2014-02-25 13:00:00. Stored in database as timeinterval type.
- autocomplete: generates an autocomplete list from the sql table column specified in the list_definition field. The syntax is table_name.column. The table is searched (by default) in the public schema in the gisdata database.
- autocompletelist: Similar to the autocomplete field, just here it is possible to autocomplete multiple values into a single field
- photo id: if the photo module is enabled, the program enters the uploaded photo IDs here.
- geometry: point: WKT POINT()
- geometry: line: WKT LINE()
- geometry: polygon: WKT POLYGON()
- geometry: any: WKT (See different geometry types in action: https://openbiomaps.org/projects/checkitout/upload/?form=736&type=web)
- colour rings: allows you to specify a colour ring combination, where you can create red, pink, green, light green, orange, yellow, blue, light blue, white, black, brown, purple, violet and metal ring combinations. The section in square brackets codes the maximum number of rings that can be specified on the different leg sections, followed by the individual colour codes of the possible colours. Eg: [XX],Blue:B, red:R, green:G
        Allowed colours and markings: 
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

   See in action: https://openbiomaps.org/projects/checkitout/upload/?form=939&type=web

        
Input control
.............
checks the number of characters entered

- no check
- min - max
- regular expression
- spatial
- custom check
    
List definition
...............
First of all, if you wish to use list during data upload you have to change the "Type" to list, autocomplete or autocomplete list.

You can define here several lists, eg.: simple/multiple choice or autocomplete lists. You can define the list with specifications of elements or you can use elements from other data tables also you can define rules and terms to filter those elements.

If our list has only a couple of elements, we can create a simple specification. See below - in this case, we define the list values that we can choose from a roll-down menu during data upload. These values ("female", "male") will get into your database.

.. code-block:: json

    {
      "list": {
        "female":[],
        "male":[]
       }
    }

If more labels mean the same value (eg.: "F", "f", "female" mean "female"), we can define which labels belong to which value. During data upload, only the value will get into your database, not the different labels. This became remarkable during file upload when you have data from previous years from many observers. They possibly used different labels to the same value, but using different labels to the same values is non-rewarding either during a query or analysing your data.

.. code-block:: json

    {
      "list": {
        "female":[
        	"F",
        	"f",
        	"female"],
        "male":[
                "M",
        	"m",
        	"male"]
       }
    }

GOOD TO KNOW!

  A list can be specified not only in JSON, but also in plain text format, for easier creation. In this case, all values must be entered on a new line. When you save the form, the list in JSON format is automatically converted from the plain text list, which you can then edit in JSON format.


The values in the list can also come from an SQL table. In this case, we need to specify the path to the table (schema name (optionsSchema), table name (optionsTable)) and the column name we want to use as value (valueColumn) and label (labelColumn).

We also can filter values from the table according to specified criteria. In this case, we need to specify which columns (preFilterColumn) we filter against and which values we specify (preFilterValue). Example of using a prefilter:

.. code-block:: json
 
    {
        "optionsTable": "milvus_taxon",
        "valueColumn": "word",
        "preFilterColumn": [
            "lang",
            "status"
        ],
        "preFilterValue": [
            "obm_taxon",
            [
                "accepted",
                "undefined"
            ]
        ],
        "orderBy": "taxon_db",
        "order": "desc"
    }

The full definition of the list is JSON, shown below. It is compiled in the web interface with the help of the list editor and automatically checked for syntax by the application. If the syntax is incorrect, an error message is returned.

.. code-block:: json

    {
        "list": {
          "val1": [
	      "label1", "label2"
	  ]
        },
        "optionsSchema": "e.g. public",
        "optionsTable": "a table name",
        "valueColumn": "a column from the table",
        "labelColumn": "a column from the table - optional",
        "filterColumn": "",
        "pictures": {
            "an element from the `list`, e.g. val1": "url-string"
        },
        "triggerTargetColumn": [""],
        "Function": "",
        "disabled": [
	    "an element from the `list`, e.g. val1"
	],
        "preFilterColumn": [
	    ""
	],
        "preFilterValue": [
	    ""
	],
        "preFilterRelation": [
	    ""
	],
        "multiselect": "true or false, default is false",
        "selected":[
            "an element from the `list`, e.g. val1"
        ],
        "size": "a numeric value"
        "orderBy": [
            "column or SQL expression"
        ],
        "order": [
            "ASC or DESC"
        ],
        "limit": "numeric value"
    }

Joint lists 
............
Create a list in a column (starter column), which determines the list of your chosen column ("list in the list"). First of all, you have to create a background table (animal_taxons), which contains data about which groups include which groups. For example, this table can show which genre belongs to which family and/or which families belong to which order, like vertebrates (animal_supergoup) contain amphibian, reptile, bird, mammal (animal_group_name) and invertebrates include (animal_supergroup) cnidaria, insects (animal_group_name) etz...

You can add your code of "joint list" in the "list definition" field. The first part of the code determines which column will affected by the "starter column" (you have to type it in the JSON field of the starter column):

.. code-block:: json

    {
        "triggerTargetColumn": [
            "affected_list_name"
        ],
        "Function": "select_list",
        "optionsSchema": "shared",
        "optionsTable": "animal_taxons",
        "valueColumn": "animal_group_name",
        "labelColumn": "animal_group_name",
        "labelAsValue": true
    }

Code explanation:
	"Function" - always "select_list"
	"optionsSchema" - always "shared"
	"optionsTable" - "background_table_name"
	"valueColumn" - column from the background table, what you use for the list, where the code is in (starter_column)
	"labelColumn" - create the list in the affected column based on the starter column

The next step is to determine in our affected column, from which column it should take the values out (you have to type it in the JSON field of the affected column):

.. code-block:: json

    {
        "optionsTable": "animal_taxons",
        "valueColumn": "animal_group_name",
        "labelColumn": "animal_group_name",
        "filterColumn": "animal_supergroup",
        "Function": "select_list",
        "optionsSchema": "shared"
    }

Code explanation (only the new variables are explained here):
	"filterColumn" - determine which was the starter column

With the "joint list" option you can connect more than 2 columns also.

.. code-block:: json

    {
        "optionsSchema": "shared",
        "optionsTable": "animal_taxons",
        "filterColumn": "animal_supergroup",
        "Function": "select_list",
        "valueColumn": "animal_group_name",
        "triggerTargetColumn": [
            "species"
        ],
        "labelColumn": "animal_group_name"
    }

"triggerTargetColumn" all the time triggers the next column. "filterColumn" always marks the previous column. "valueColumn" and "labelColumn" always marks the actual column.

Other examples:
1. Determine buildings inside the settlement. We collect data from species breeding in artificial nestboxes. We would like to create an autocomplete list for the settlement column, also we would like to create a simple list in the building column. Our background table (tytoalba_buildings) contains the nestboxes spatial distribution: on which buildings in which settlement. The building column of our background table contains a huge amount of possible values, but not all buildings occur in all settlements. Therefore we would like to create a filtered building list based on the settlement list.

FIRST STEP: we establish the autocomplete list of settlement columns. We turn the column type to autocomplete, then we determine which values we need from our background table and also we point to the building column:

.. code-block:: json

    {
        "triggerTargetColumn": [
            "building"
        ],
        "Function": "select_list",
        "optionsSchema": "public",
        "optionsTable": "tytoalba_buildings",
        "valueColumn": "settlement"
    }

Second step: we establish the simple list of building columns. We turn the column type to list, then we determine the value of our list and filter based on the settlement column:

.. code-block:: json

    {
        "optionsTable": "tytoalba_buildings",
        "filterColumn": "settlement",
        "Function": "select_list",
        "valueColumn": "building"
    }

Default values
..............
You can predefine a value for a field. There are several dynamic predefined values:
    - _autocomplete
    - _input
    - _list
    - _geometry
    - _login_name
    - _email
    - _boolean
    - _attacment
    - _datum
    - _auto_geometry

    If you want an empty input field, you have to specify _input, if you want a selection list, you have to specify _list (it fills the list with the elements of the definition), if you want a geometry selection, you have to specify _geometry, and _datum results in a date selection field.
    
    See in action: https://openbiomaps.org/projects/checkitout/upload/?form=421&type=web

Field display options 
.....................
    - sticky
        This has real significance in the mobile application. If this option is selected, the field will retain its value when new rows start.
    - hidden
        The field is not displayed.
    - read only
        The field value cannot be modified.
    - once
        The field displayed only once in observation-list in the mobile app at the end of the observation
        (This option will used in the web form to pull out a field from the table over the table. Currently, using the default value option do this for the web form)
    - list elements as buttons
        List elements will be displayed as buttons. Pictures can be used in the buttons. 
          Pictures should be defined for all list elements in the list definition like in this example:
          If the list has the following values: animals, plants, mushrooms, bats

.. code-block:: json

    {
        "pictures": {
            "animals": "http://....png",
            "plants": "http://....png",
            "mushrooms": "http://....png",
            "bats": "http://....png"
        }
    }
    
Column relations
................
You can specify how to check or modify the value entered from the table for a value in another column. e.g.: for the weight column, if the sex column is female, the values can take min 20 and max 30 numeric values (sex=female) {minmax(20:30)}

Check the contents of columns depending on the contents of other columns

See in action: https://openbiomaps.org/projects/checkitout/upload/?form=938&type=web

Pseudo columns
..............
Columns from other upload-forms can be added here with the following format: form-name:column1,column2,columnN
The listed column will appear after this column. The data entered in the pseudo-columns will be uploaded using the other form's definition. Using this feature lets uploaders upload data into two tables at once.


Relations pseudolanguage definition
-----------------------------------

( rel_field = rel_statement ) { rel_type = rel_value } , ( rel_field = rel_statement ) { rel_type = rel_value } , ...

IF an other cell value (rel_field) match to (rel_statement) THEN  this cell (rel_type) value should be (rel_value)

rel_type is a function related to the field type

     datum:          year            extract year component from a datum string
     
     text, numeric:   minmax          min-max range check
     
     any type:       obligatory      change obligatory setting                
                     inequality      check inequality with these symbols: <>= between the index and current field. Causing an error message.
		     
rel_statement can be a regexp-based function. In this case statement should be started with !! and followed by a regexp expression e.g.  !!^(\d{2})$ 

     If the statement is regexp rel_value also can be a function
     
     .       which means replacing the current cell value with matched string from the matched string from the rel_field
     
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

Examples
........

On the `tarsus_length` column

	(clutch_size=!!^([123])$) {obligatory(1)}

This means it will be mandatory to fill the tarsus length if the nest size is 1, 2 or 3

On the `end_date` column. If the `found_date` field is not empty, check, the `end_date` is greater than the `found_date`. If yes, return TRUE else FALSE, which causes an upload error.

    (found_date=!!^(.+)$) {inequality(+>=.)}

On a date field which does not contain the year part. If the `year` column is not empty, then the `date` field will be updated with this year (numbers)

    (year=!!^(d{4})$) {set(.)}

On the `ring_number` field. If the recapture's value is “1” then the `ring_number` will be obligatory.

    (recapture=1) {obligatory(1)}

On the `english_name` column. If the `scientific_name` is empty then the english_name will be obligatory.

    (scientific_name=!!(^$)) {obligatory(1)}

On the `amount_type` field. If the `number_of_individuals` is greater than 50 then the `amount_type` will be the “estimated value”, else if less or equal to 50, then the “exact value”.

    (number_of_individuals>50) {set(estimated value)},(egyedszam<=50) {set(exact value)}
