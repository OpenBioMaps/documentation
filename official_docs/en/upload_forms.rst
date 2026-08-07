.. _manage-upload-forms:

Upload form management
======================

List of available forms
-----------------------
Existing forms can be selected for editing, deletion, or blocking.


Form header definition
----------------------

Destination table
.................
Which project table does the upload form apply to?

Name of the form
................
The name for the upload form. This should be unique within a project.

You can make a copy of a form by renaming it.

This name can be multilingual if you use the ``str_`` tag. See more about translations :ref:`translations`

Form access
...........
Define who can see/use the form:

- public (anyone), 
- all logged-in users, 
- only specified groups
	
If "only specified groups" is chosen, the list of available users/groups select field will be active, allowing users or groups to be selected for access to this form.

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
Use the following format to define a list of available references: "4326:wgs84,23700:eov". It is a comma-separated list of EPSG reference IDs and visible labels.

Form grouping
..............
The form can be organised into groups in the form choose interface on the web form. The group names can be defined or chosen here.
This option is not available on the mobile app yet.

Form publish
............
A form can be locked by publishing it (orange publish button in the form-header area). Any updates to a published form create a new version. The old versions are available for API clients (mobile app). A draft version can be created from the published forms for testing (create a draft version button at the bottom of the page). The draft version is only available to the creator of the draft (by default). The draft version can be published to the form's published branch.

.. observationevents:

Observation events
..................

Glossary: Observation Event vs. Observation

In line with international data-sharing standards (Darwin Core / GBIF), the OpenBioMaps data structure divides field data collection into two distinct levels: the **Observation Event** and the **Observation**. This division ensures that both structured surveys and casual observations can be accurately recorded.

1. Observation Event

An **Observation Event** is a predefined spatial and temporal context representing a specific data collection or sampling activity.

 **- Key point:** The event itself is the field activity (the act of sampling), not the organism found.

**Main characteristics:**

It always has a **recorded location** (coordinates or a fixed point) and a **time** (or time interval).

It is often associated with a specific methodology or protocol (e.g. 5-minute point count, trapping).

**Handling 'zero observations' (absence):** An Observation Event is created and remains valid in the system even if the researcher did not observe a single species during the survey. 

 - This 'negative data' is crucial for scientific analysis and for documenting sampling effort.

**Hierarchy:** An Observation Event may contain **zero, one or more** individual observations (Observation). The observations recorded during the event share a common identifier: the observation_list_id.

2. Observation

An **Observation** is the individual detection or recording of a specific taxon (species, genus, etc.) in the field.

 - Essence: This is the biological data itself, evidence of the organism’s presence.

**Main characteristics:**

It contains the **taxon name** (species name), as well as the counted or estimated **number of individuals** (or other quantitative indicator).
It always includes a location and a date and time.

**Types in the system:**

 **- Event-linked observation:** Species data recorded as part of a structured survey (Observation Event). In this case, the location and time data are inherited from the event or specified within it.
 **- Opportunistic Observation:** An individual sighting that is not part of a pre-planned protocol or survey, but is recorded immediately on an ad hoc basis (e.g. a rare bird spotted whilst out and about).

Summary table for developers and users

| Characteristic | Observation | Event Observation |
| -------------- | ----------- | ----------------- |
| **What does it represent?** | The context of fieldwork/sampling. | The sighting of a specific organism. |
| **Can it be left blank?** | **Yes.** If, according to the protocol, nothing was found, the event still exists. | **No.** It must always include species and number of individuals. |
| **Quantitative indicator** | The sampling effort (duration, area size). | Number of individuals, coverage, count. |
| **GBIF / DwC equivalent** | Event / Sampling-event data | Occurrence / Occurrence data |

A time limit (expressed in minutes) can be set for the observation event; when this limit is reached, the mobile app alerts the user that the time has expired, but otherwise nothing happens, and the user can continue with their observations.

A 'forced observation event' means that the form can only be launched in event mode. If this option is enabled but not set to 'forced', the user has the option to use the form in either event mode or ad hoc observation mode.


.. tracklog:

Tracklog
........
Automatic recording of the route log whilst using the form. This may also be mandatory or optional. Tracklog recording is only available in event mode.


.. periodic-notification:

Periodic notification
.....................
At specified intervals (minutes), the app will alert the observer to record a new observation. Meanwhile, the counter runs continuously. When the user records an observation, the timer will always restart.


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
There are two strings here: The visible name of the column (it can be edited to make it unique to a form) and the original name of the column.
    
Obligatory
..........
Three options are available here: yes, no, soft-error

- Yes (colour: burgundy), then the form cannot be submitted without filling in the column cell.
- No (colour: grey), then the form can be submitted with an empty cell in the  rows with this column.
- Soft-error (colour: pink), allows empty cells or differences from restrictions, but the uploader should confirm this for every affected line.
    
Column description
..................
Short description of the field.
    
Column type
...........
- text: arbitrary text - minimum and maximum lengths can be specified.     
- numeric: arbitrary number - minimum and maximum lengths can be specified
- list: drop-down list, with one selectable item by default
- true-false: boolean false/true value. The order of the value can be controlled in the list definition field. e.g. "false, true"
- date: Separated by any character in order of year, month, day. Stored in the database as a date type.
- date and time: after a blank frame, the date is in hour:minute:second format. If a second is missing, the program automatically treats it as 00 and warns you to accept it. If the minute is missing, the program will automatically treat it as 00, but warn to accept it. Stored in the database as a datetime type.
- time: (timetominutes): hours:minutes format, which the program converts to an integer value. Stored in the database as an integer.
- time: hours:minutes. As time is typed in the database.
- time interval: (timeinterval) Pl: 2014-02-25 12:00:00 2014-02-25 13:00:00. Stored in database as timeinterval type.
- autocomplete: generates an autocomplete list from the SQL table column specified in the list_definition field. The syntax is table_name.column. The table is searched (by default) in the public schema in the "gisdata" database.
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
First of all, if you wish to use a list during data upload, you have to change the "Type" to list, autocomplete or autocomplete list.

You can define several lists here, e.g., simple/multiple-choice or autocomplete lists. You can define the list with specifications of elements, or you can use elements from other data tables, or you can define rules and terms to filter those elements.

If our list has only a couple of elements, we can create a simple specification. See below - in this case, we define the list values that we can choose from a roll-down menu during data upload. These values ("female", "male") will be stored in your database.

.. code-block:: json

    {
      "list": {
        "female":[],
        "male":[]
       }
    }

If more labels mean the same value (eg, "F", "f", "female" mean "female"), we can define which labels belong to which value. During data upload, only the value will be stored in your database, not the different labels. This became remarkable during file upload when you have data from previous years from many observers. They may have used different labels for the same value, but using different labels for the same value is non-rewarding either during a query or when analysing your data.

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

  A list can be specified not only in JSON, but also in plain text format, for easier creation. In this case, all values must be entered on separate lines. When you save the form, the list is automatically converted from plain text to JSON, which you can then edit in JSON format.


The values in the list can also come from an SQL table. In this case, we need to specify the path to the table (schema name (optionsSchema), table name (optionsTable)), and the column name we want to use as the value (valueColumn) and the label (labelColumn).

We can also filter the table's values according to specified criteria. In this case, we need to specify which columns (preFilterColumn) to filter against and which values to filter by (preFilterValue). Example of using a prefilter:

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

The full definition of the list is JSON, shown below. It is compiled in the web interface using the list editor and automatically checked for syntax by the application. If the syntax is incorrect, an error message is returned.

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
Create a list in a column (starter column), which determines the list of your chosen column ("list in the list"). First of all, you have to create a background table (animal_taxons) that contains data on which groups include which other groups. For example, this table can show which genre belongs to which family and/or which families belong to which order, such as vertebrates (animal_supergroup) containing amphibians, reptiles, birds, mammals (animal_group_name), and invertebrates (animal_supergroup) including cnidaria, insects (animal_group_name), etc.

You can add your code of "joint list" in the "list definition" field. The first part of the code determines which column will be affected by the "starter column" (you have to type it in the JSON field of the starter column):

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
	"valueColumn" - column from the background table, which you use for the list, where the code is in (starter_column)
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

With the "joint list" option, you can also connect more than 2 columns.

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

"triggerTargetColumn" all the time triggers the next column. "filterColumn" always marks the previous column. "valueColumn" and "labelColumn" always mark the actual column.

Other examples:
1. Determine buildings inside the settlement. We collect data from species breeding in artificial nestboxes. We would like to create an autocomplete list for the settlement column and a simple list for the building column. Our background table (tytoalba_buildings) contains the nestboxes spatial distribution: on which buildings in which settlement. The column in our background table contains a large number of possible values, but not all buildings occur in all settlements. Therefore, we would like to create a filtered list of buildings based on the settlement list.

FIRST STEP: We establish the autocomplete list of settlement columns. We turn the column type to autocomplete, then we determine which values we need from our background table, and also we point to the building column:

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

Second step: we establish a simple list of building columns. We turn the column type to list, then we determine the value of our list and filter based on the settlement column:

.. code-block:: json

    {
        "optionsTable": "tytoalba_buildings",
        "filterColumn": "settlement",
        "Function": "select_list",
        "valueColumn": "building"
    }


.. default-values:

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

    If you want an empty input field, you have to specify _input; if you want a selection list, you have to specify _list (it fills the list with the elements of the definition), if you want a geometry selection, you have to specify _geometry, and _datum results in a date selection field.
    
    See in action: https://openbiomaps.org/projects/checkitout/upload/?form=421&type=web

.. api-params:

Field display options 
.....................
    - sticky
        This has real significance in the mobile application. If this option is selected, the field will retain its value when new rows start.
    - hidden
        The field is not displayed.
    - read only
        The field value cannot be modified.
    - once
        The field was displayed only once in the observation list in the mobile app at the end of the observation
        (This option will be used in the web form to pull out a field from the table over the table. Currently, using the default value option does this for the web form.)
    - list elements as buttons
        List elements will be displayed as buttons. Pictures can be used in the buttons. 
          Pictures should be defined for all list elements in the list definition, like in this example:
          If the list has the following values: animals, plants, mushrooms, bats
    - unfolding list
        This is a species list generation solution for the mobile app.
        This option can only be used on autocomplete-type list fields (typically used for the species name field) if the form also contains an individual number field (set at object level in the database table settings). This is because this type enables the mobile application to display the selected (species) names together with their individual numbers in a list, one below the other, and the individual numbers can be modified afterwards. In this case, there is no need to save the record after every single modification; it is sufficient to save it only at the end of the observation event. For this reason, it is preferable to use it on a form treated as an observation event, as in this case the ‘Save observation’ button will effectively serve only as an intermediate save and will not clear the species list we have compiled, complete with individual numbers, from the form.

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


The relations language definition
---------------------------------

( rel_field = rel_statement ) { rel_type = rel_value } , ( rel_field = rel_statement ) { rel_type = rel_value } , ...

IF an other cell value (rel_field) match to (rel_statement) THEN  this cell (rel_type) value should be (rel_value)

rel_type is a function related to the field type

     datum:          year            extract year component from a datum string
     
     text, numeric:   minmax          min-max range check
     
     any type:       obligatory      change obligatory setting                
                     inequality      check inequality with these symbols: <>= between the index and current field. Causing an error message.
		     
rel_statement can be a regexp-based function. In this case, the statement should start with !! and followed by a regexp expression e.g.  !!^(\d{2})$ 

     If the statement is regexp rel_value also can be a function
     
     .       which means replacing the current cell value with matched string from the matched string from the rel_field
     
     .+      means append the current cell value to the matched string from the rel_field 
     
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

Pseudo column examples
......................

On the `tarsus_length` column

	(clutch_size=!!^([123])$) {obligatory(1)}

This means it will be mandatory to fill the tarsus length if the nest size is 1, 2 or 3

On the `end_date` column. If the `found_date` field is not empty, check that the `end_date` is greater than the `found_date`. If yes, return TRUE; else, return FALSE, which causes an upload error.

    (found_date=!!^(.+)$) {inequality(+>=.)}

On a date field which does not contain the year part. If the `year` column is not empty, then the `date` field will be updated with this year (numbers)

    (year=!!^(d{4})$) {set(.)}

On the `ring_number` field. If the recapture's value is “1”, then the `ring_number` will be obligatory.

    (recapture=1) {obligatory(1)}

On the `english_name` column. If `scientific_name` is empty, 'english_name' will be required.

    (scientific_name=!!(^$)) {obligatory(1)}

On the `amount_type` field. If the `number_of_individuals` is greater than 50, then the `amount_type` will be the “estimated value”, else if less than or equal to 50, then the “exact value”.

    (number_of_individuals>50) {set(estimated value)},(egyedszam<=50) {set(exact value)}
