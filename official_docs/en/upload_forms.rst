.. _manage-upload-forms:

Upload form management
======================

List of available forms
-----------------------
Existing forms can be selected for editing or can be deleted or blocked of using.


Form header definition
----------------------

Destination table
.................
Which project table the upload form applies to.

Name of the form
................
The name for the upload form. This sholud be unique within a project.

You can make a copy of a form by renaming it.

This name can be multilingual, if you use the ''str_'' tag. See more about translations :ref:`translations`

Form access
...........
Define who can see / use the form: 
	- public (anyone), 
	- all logged in users, 
	- only specified groups
	
If "only specified groups" chose,  the list of available users/groups select field will be active, where users or groups can be chosen for accessing this form.

Data access
...........
Uploaded data will only be available to the specified groups here. By default, data can be read and edited by the uploader.

Form type
.........
Should be at least one from the following three options:

web form, file upload form, API (externally accessible form, e.g. mobile app)

Form description
................
A shorter or longer description of the form. This can be used to give instructions for uploaders.

Form SRID
.........
Any kind of spatial reference can be coosed for the uploaded which is available in https://spatialreference.org/. The default srid is "epsg:4326 (WGS84)". If a list of sptial references specified here, uploaders can choose only from these options. 
Use the following format for define a list of available references: "4326:wgs84,23700:eov". It is a comma separated list of epsg reference id and visible labels.

Form groupping
..............
Form can be organized into groups for the form choose interface on the web form. The group names can be defined or choosed here.
This option is not available on the mobile app yet.

Form publish
............
A form can be locked by publishing it (orange publish button in the form-header area). Any updates on a published form creates a new version of the form. The old versions are available for API clients (mobile-app). Draft version can be created from the published forms for testing (create draft version button at the bottom of the page). The dtaft version is only available the creator of the draft (by default). The draft version can be publised in the published branch of the form.

.. observationlists:

Observation list
................
A series of observations can be combined, for example, observations of transect counting or observations of time limit counting. A time limit (in minutes) can be set, when reached the mobile application will warn when the time is up, but nothing else happens, the user can continue the observation. A forced observation list means that the form can only be started in list mode, as an individual the user can also start a list observation with the form if this option is enabled.

.. tracklog:

Tracklog
........
Automatic traclog recording while using the form.

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
It is a small empty input box (by default) next to "included" option.

Column
......
There are two strings here: The visible name of the column (it can be edited to make it unique to a form), and the original name of the column.
    
Obligatory
..........
Three options are avilable here: yes, no, soft-error
    - Yes (colour: burgundy), then the form cannot be submitted without filling in the column cell.
    - No (colour: gray), then form can be subbmitted with empty cell in the  rows with this column.
    - Soft-error (colour: pink), allows empty cells or difference from restrictions but uploader should confirm this for every affected lines.

    
Column description
..................
Short description of the field.
    
Column type
...........
    - text: arbitrary text - minimum and maximum lengths can be specified.
        
    - numeric: arbitrary number - minimum and maximum lengths can be specified
        
    - list: drop-down list of values separated by the comma you specify. The drop-down list can be specified in name:value format, with the elements and real values of the drop-down list being filled out. The "name", if prefixed with "str\_", will automatically translate to the selected language version, if defined. The words 'true' and 'false' are translated according to str_true and str_false. 
        Multiple labels can be specified for a value, the first of which will be displayed in a web form case, and any label or value from the file cell value will give a correct match in a file upload. Tags must be specified with # characters between them. E.g.: female#boy:f,male#male#him:m,juvenile#juvenile:j,adult#old:a
        
        In this case, the possible labels for the "f" value are the words "female", "tojo" and "egg"
        
    - true-false: boolen false/true value. The order of the value can be controlled in the list definition field. e.g. "false,true"
        
    - date: Separated by any character in order of year month day. Stored in database as date type.
        
    - date and time: after a blank frame, the date is in hour:minute:second format. If a second is missing, the program automatically considers it as 00, but warns you to accept it. If the minute is missing, the program will automatically treat it as 00 but warn to accept it. Stored in database as datetime type.
        
    - time: (timetominutes): hours:minutes format which the program converts to an integer value. Stored in database as integer.
        
    - time: hours:minutes. As time type in the database.
        
    - time interval: (timeinterval) Pl: 2014-02-25 12:00:00 2014-02-25 13:00:00. Stored in database as timeinterval type.
        
    - autocomplete: generates an autocomplete list from the sql table column specified in the list_definition field. The syntax is table_name.column. The table is searched (by default) in the public schema in the gisdata database.

    - autocompletelist: Similar to the autocomplete field, just here it is possible autocompleting multiple values into a single field
        
   - photo id: if the photo module is enabled, the program enters the uploaded photo IDs here.
        
   - geometria: point: WKT POINT()
        
   - geometria: line: WKT LINE()
        
   - geometria: polygon: WKT POLYGON()
        
   - geometria: any: WKT
   
   See different geometry types in action: https://openbiomaps.org/projects/checkitout/upload/?form=736&type=web
        
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

You can define here several list, eg.: simple/multiple choice or autocomplete lists. You can define the list with specification of elements or you can use elements from a other datatables also you can define rules and terms to filter those elements.

If our list have only a couple of elements, we can create a simple specification. See below - in this case we define our list values what we can chooose from a roll-down menu during data upload. These values ("female", "male") will get into your database.

.. code-block:: json

    {
      "list": {
        "female":[],
        "male":[]
       }
    }

If more labels mean the same value (eg.: "F", "f", "female" mean "female"), we can define which labels belong to which value. During data upload only the value will get into your database not the different labels. This became remarkable during file upload, when you have many data from previous years from many observer. They possibly used different labels to the same value, but using different labels to the same values are non-rewarding either during query or analysing your data.

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

Also we can create our list based on another table variable.

.. code-block:: json

    {
        "list": {
          "val1": [
	      "label1", "label2"
	  ]
        },
        "optionsSchema": "e.g. public",
        "optionsTable": "table name",
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

Example of pre filtering:

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



Joint lists 
............
Create a list in a column (starter column), which determines the list of your choosed column ("list in the list"). First of all you have to create a background table (animal_taxons), which contain data about which groups include which groups. For example, this table can show which genre belong to which family and/or which families belong to which order, like vertebrates (animal_supergoup) contain amphibian, reptile, bird, mammal (animal_group_name) and invertebrates include (animal_supergroup) cnidaria, insects (animal_group_name) etz...

You can add your code of "joint list" in the "list definition" field. The first part of the code determine that which column will affected by the "starter column" (you have to type it in the json field of the starter column):

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
	"labelColumn" - create the list in the affected column based on strater column

The next step to determine in our affected column, from which column it should take the values out (you have to type it in the json field of the affected column):

.. code-block:: json

    {
        "optionsTable": "animal_taxons",
        "valueColumn": "animal_group_name",
        "labelColumn": "animal_group_name",
        "filterColumn": "animal_supergroup",
        "Function": "select_list",
        "optionsSchema": "shared"
    }

Code explanation (only the new variables explained here):
	"filterColumn" - determine which was the starer column

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

"triggerTargetColumn" all the time trigger the next column. "filterColumn" always mark to the previous column. "valueColumn" and the "labelColumn" always mark the actual column.

Other examples:
1. Determine buildings inside the settlement. We collect data from species breeding in artificial nestboxes. We would like to create an autocomplete list for the settlement column, also we would like to create a simple list in the building column. Our background table (tytoalba_buildings) contain the nestboxes spatial distribution: on which buildings in which settlement. The building column of out background table contains huge amount of possible values, but not the all building occur in all settlement. Therefore we would like to create a filtered building list based on the settlement list.

FIRST STEP: we establish the autocomplete list of settlement column. We turn the column type to autocomplete, than we determine which values are we need from our background table and also we point to the building column:

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

Second step: we establish the simple list of building column. We turn the column type to list, than we determine the value of our list and filter based on settlement column:

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
        Field not displayed.
    - read only
        Field value cannot be modified.
    - once
        Field displayed only once in observation-list in mobile app at the end of observation
        (This option will used in the web form to pull out a field from the table over the table. Currenty, using the default value option do this for the web form)
    - list element as buttons
        List element will be diplayed as buttons. Pictures can be used in the buttons. 
          Pictures should be defined in for all list elements in the list definition like in this example:
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
You can specify how to check or modify the value entered from the table for a value in another column. e.g.: for weight column, if the sex column is female, the values can take min 20 and max 30 numeric values (sex=female) {minmax(20:30)}

Check the contents of columns depending on the contents of other columns

See in action: https://openbiomaps.org/projects/checkitout/upload/?form=938&type=web

Pseudo columns
..............
Columns from other upload-forms can be added here with the following format: form-name:column1,column2,columnN
The listed column will be appear after this column. The data entered in the pseudo-columns will be uploaded using the the other form's definition. Using this feature let uploaders to upload data into two tables at once.


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

Examples
........

On the `tarsus_length` column

	(clutch_size=!!^([123])$) {obligatory(1)}

Which means it will be mandatory to fill the tarsus length if the nest size is 1, 2 or 3

On the `end_date` column. If the `found_date` field not empty, check, the `end_date` is grater than the `found_date`. If yes, returning TRUE else FALSE, which causing upload error.

    (found_date=!!^(.+)$) {inequality(+>=.)}

On a date field which not contains year part. If the `year` column is not empty, then the `date` field will be updated with this year (numbers)

    (year=!!^(d{4})$) {set(.)}

On the `ring_number` field. If the recapture's values is “1” then the `ring_number` will be obligatory.

    (recapture=1) {obligatory(1)}

On the `english_name` column. If the `scientific_name` is empty then the english_name will be obligatory.

    (scientific_name=!!(^$)) {obligatory(1)}

On the `amount_type` field. If the `number_of_individuals` grater than 50 then the `amount_type` will be “estimated value”, else if less or equal than 50, then “exact value”.

    (number_of_individuals>50) {set(estimated value)},(egyedszam<=50) {set(exact value)}
