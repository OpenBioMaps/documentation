.. |br| raw:: html

    <br>
    
API documentation
*****************
HTTP methods:  GET, POST, PATCH

API tools:  Authentication, Data retrieval, Data push, Settings update


API handlers:
-------------
Authentication handler (OAUTH):

/oatuh/token.php: Authentication

Authentication-based interface (PDS):

/projects/*API_VERSION*/*projectname*/pds.php: Data retrieval, Data push, Settings update 

Non-authenticated requests (web):

/projects/*projectname*/index.php

PDS API version:
................
Example: http://openbiomaps.org/projects/dead_animals/v2.1/pds.php
The default version setting (if the version string missing from the URL) is 1.1., which is compatible with 2.0 and backward compatible with 1.0.


OAUTH
-----------
An oauth2 implementation based on ttps://bshaffer.github.io/oauth2-server-php-docs/. OAUTH is used in the web interface and in the PDS as well.

Variables
.........
grant_type:     password
username:       a registered email address
password:       password string
scope:          list of requested scope access in the authenticated session
access_token:   a valid access token

HTML authentication of clients is necessary

Available clients are mobile, R, web


PDS API
-------
The main OBM API interface. Basically designed for R and mobile clients. It uses OAUTH for authentication.

Variables
.........
scope:      data methods: see below

value:      Most scopes use

header:     (put data) JSON list of table columns' names

ignore_warning: (put data) ignore upload warnings

form_id:        (put_data) set form id

data:           (put data) JSON array of uploaded data


GET type scopes
...............
**get_project_vars**

 Query general project variables (also available for non-logged-in users).

 Additional parameters: 

 - project [text]: if not set default is the *template* project

 Returns:

 - project_url [url string]: The web address of the project
 - project_description [text string]: Short description of the project 
 - game [on/off]: game available for Android mobile app
 - public_mapserv [url string]: URL of publicly accessible map service
 - rserver_port [numeric]: numeric port number of R-Shiny server, accessible on project_url

**get_project_list**

 Get a list and basic info on database projects available on the server. If a user is already logged in, get a list of those projects where the user has an account and where there are public query/upload interfaces. If the user is not logged in, query public projects only.
 
 Additional parameters:

 - only-project [text]: query project parameters only for the selected project, default is to query all accessible projects
 - accessible [text]: all/**accessible**. If the *accessible* parameter is given and its value is "accessible" (default)

 Returns:

 - project_table [string],
 - creation_date [date string],
 - Creator [string],
 - email [string],
 - stage [string] experimental/testing/stable,
 - doi [string],
 - running_date [date string],
 - license [string],
 - rum [string],
 - collection_dates [date range string],
 - subjects [text],

**get_form_list**
 
 Query the list of available upload forms.

**get_form_data**
 
 Query the fields of the selected form.

 Additional parameters: 

 - value [numeric] numeric id of a form.
 
 Returns: :ref:`see in examples below <get_form_data_example>`.

**get_profile**
 
 Get profile data of a selected user

**get_data**

 Get data rows from a selected data table (observation data).

**get_specieslist**
 
 Get the species list from a project.

**get_history**

 Get the history of a selected data row.

**get_report**

 Perform a predefined query and get the result.

**get_tables**
 
 Get the list of tables in a project

*get_trainings*

 Get the list of available trainings/forms.

 Not available from API 2.6

 Returns:

 - the set of training titles, ids, and descriptions,...

*get_training_questions*

 Get the list of questions for the selected training.

 Not available from API 2.6

 Additional parameters:

 - value [numeric] numeric id of a training.
 
 Returns:

 - The set of questions, answers, and settings

*training_results*
 
 Status list of users' training for each form. Status can be -1 (not sent), 0 (not validated yet), 1 (done, ok).
 
 Not available from API 2.6

*training_toplist*

 Toplist of trainings. Mean, Max, and Count values for each form.
 
 Not available from API 2.6
 
 Additional parameters:

 - value [text] summary without names (nonames).
 
**get_mydata_rows**

 JSON array of uploaded data.

 Additional parameters:

 - Value [numeric] limit of array length. If 0, no limit, default is no limit.


POST type scopes
................
**put_data**
 
 Send/upload data using a selected form


PATCH type scopes
.................
*set_rules*     

 Update specific settings


WEB API
-------
The index.php is also an API service in some cases (?query=) for _GET requests only and for unauthenticated requests.
This API uses text_filter modules to assemble an SQL query statement.

Variables
.........
query:          (API endpoint)

qtable:         (data table for data retrieve)

report:         (data retreive using stored queries)

output:         (JSON, XML, CSV, ... file output; If not set, the output is the web interface)

filename:       (the file name of the output file)

Get the list of active (known) OpenBioMaps servers using query API:

``curl http://openbiomaps.org/projects/openbiomaps_network/index.php -G -d 'query={"available":"up"}&output=json&filename=results.json'``

Get a filtered table from a non-default table:

``curl https://openbiomaps.org/projects/pollimon/index.php -G -d 'query={"q":"2"}&output=json&qtable=pollimon_sample_plots'``

LQ API endpoint:

LQ:             (display data from a stored query result)


.. _get_form_data_example:

**get_form_data** examples
--------------------------
Usage example:
``curl -F 'access_token=c53c9ec690fede4c3' -F 'scope=get_form_data' -F 'value=246' -F 'project=dead_animals' https://openbiomaps.org/projects/dead_animals/v2.3/pds.php | jq``

Error messages:

.. code-block:: json

  {
    "status": "error",
    "message": "The access token provided is invalid"
  }

or

.. code-block:: json

  {
    "status": "error",
    "message": "The request requires higher privileges than provided by the access token"
  }

Successful response:

.. code-block:: json

  {
  "status": "success",
  "message": "",
  "data": {
    "form_header": {
      "login_name": "Gipsz Jakab",
      "login_email": "jakab.gipsz@openbiomaps.jupyter.ga",
      "boldyellow": [
        "species"
      ],
      "num_ind": "quantity",
      "tracklog_mode": "",
      "observationlist_mode": "false",
      "observationlist_time_length": "0",
      "periodic_notification_time": null
    },
    "form_data": [
        {
        "description": "...",
        "default_value": "...",
        "column": "species",
        "short_name": "Scientific species name",
        "list": [...],
        "control": "nocheck",
        "count": "{}",
        "type": "list",
        "genlist": null,
        "obl": "1",
        "api_params": {
          "sticky": "on",
          "hidden": "off",
          "readonly": "off",
          "list_elements_as_buttons": "on",
          "once": "off",
          "unfolding_list": "off"
        },
        "spatial_limit": null,
        "list_definition": {
          "multiselect": false,
          "selected": null,
          "triggerTargetColumn": [],
          "Function": ""
        },
        "custom_function": null,
        "column_label": null,
        "field_description": "..."
      }, {...} ]}}

Explanations of variables:

*default value*: Fix value for all observations. It can be controlled with the following options:
 
 - '_input' works as any other field with a sticky flag. 
 - '_list' works as any other list-type field with a sticky flag.
 - '_geometry' works as a geometry-type field
 - '_login_name' this value is overridden by the user's name if logged in or returns as _input
 - '_email' this value overridden by the user's email address if logged in or returns as _input
 - '_autocomplete' alias of input
 - '_boolean' display as a normal boolean list
 - '_attachment' display as normal attachments field
 - '_datum' display as a normal date field
 - '_auto_geometry' geometry field without extra options (map, set)
 - '_none' not used
 
*column*: The name of the column in the database

*short_name*: Visible name of the column for the users

*list*: JSON array for menu items of a select menu. Can be {key:value} or [value,value] format

*control*: Data checking commands: custom_check, minmax, spatial, nocheck, NULL

*count*: (JSON array) If the control='minmax' this field contains the limit values, e.g 1:100

*type*: column's openbiomaps type:
 
 - autocomplete	(JSON array)
 - autocomplete_list (JSON array)
 - boolean (two elements list)	
 - crings (color rings - text)	
 - date (YYYY-MM-DD or other clear format)
 - datetime (YYYY-MM-DD HH:mm:ss)
 - file_id (file names as id by the server) 
 - line (WKT geometry string)
 - list (JSON array)
 - numeric	
 - point	(WKT geometry string)
 - polygon (WKT geometry string)
 - text 
 - time (HH:mm)
 - timetominutes (numeric value between  0 and 1440)
 - tinterval idő intervallum (HH:mm - HH:mm)
 - wkt (WKT string)
 - array (JSON array)

*genlist*: JSON array for menu items of an autocomplete menu. Can be  {key:value} or [value,value] format

*obl*: 1,2,3 (obligatory, non-obligatory, soft error) Soft error can be handled as non-obligatory.

*api_params*: JSON array of control values. Till API v2.0 only 'sticky' as an array element. 

Above API v2.0:

.. code-block:: json

    {"sticky":"off","hidden":"off","readonly":"off","list_elements_as_buttons":"off","once":"off","unfolding_list": "off"}

*spatial_limit*: WKT polygon string of spatial limit. It is used if the Control type is spatial.

*list_definition*: JSON array of the complex list definition

*custom_function*: null

*custom_label*: 

*field_description*:



Training explanations and examples
----------------------------------
Examples:

curl -F 'scope=get_trainings' -F 'access_token=9d45...' -F 'project=dinpi' http://localhost/biomaps/pds.php

Result of a successful call:
    {"status":"success","data":[{"id":"1","form_id":"95","html":"<div>...",,"task_description":"<div>...","enabled":"t","title":"Gyakorlás I.","qorder":"1","project_table":"dinpi"},{
    
curl -F 'scope=get_training_questions' -F 'access_token=9d45...' -F 'project=dinpi' http://localhost/biomaps/pds.php

Result of a successful call:
    {"status":"success","data":[{"qid":"1","training_id":"1","caption":"...?","answers":"[{"Answer": "...","isRight": "false" }, ]","qtype":"multiselect"}]}
    
    qtype can be multi-select or single select
    
curl -F 'scope=training_results' -F 'access_token=9bb4...' -F 'project=dinpi' http://localhost/biomaps/pds.php

Result of a successful call:
    {"status":"success","data":"{"95":1,"96":0,"97":-1,"98":-1}"}
    
    Meaning of values: form-95 done, form-96 done, but not validated yet, form-97,98 not completed yet
    
curl -F 'scope=training_toplist' -F 'value=nonames' -F 'access_token=5ac3...' -F 'project=dinpi' http://localhost/biomaps/pds.php

Result of a successful call:
    {"status":"success","data":{"95":{"mean":"0.50000000000000000000","count":"2","max":"0.7"},"96":{"mean":"0.70000000000000000000","count":"1","max":"0.7"},"97":{"mean":"0.70000000000000000000","count":"1","max":"0.7"},"98":{"mean":null,"count":"1","max":null}}}
    
curl -F 'scope=training_toplist' -F 'access_token=5ac3...' -F 'project=dinpi' http://localhost/biomaps/pds.php

    {"status":"success","data":{ \\ |br|
        "95":{"Bán Miki":{"mean":"0.30000000000000000000","count":"1","max":"0.3"}, \\ |br|
              "Dr. Bán Miklós":{"mean":"0.70000000000000000000","count":"1","max":"0.7"}}, \\ |br|
        "96":{"Dr. Bán Miklós":{"mean":"0.70000000000000000000","count":"1","max":"0.7"}}, \\ |br|
        "97":{"Dr. Bán Miklós":{"mean":"0.70000000000000000000","count":"1","max":"0.7"}}, \\ |br|
        "98":{"Dr. Bán Miklós":{"mean":null,"count":"1","max":null}}}}


Authentication examples
-----------------------

`    curl \\ |br|
    -u mobile:123 http://openbiomaps.org/oauth/token.php \\ |br|
    -d "grant_type=password&username=foo@foobar.hu&password=abc123&scope=get_form_data+get_form_list+put_data"`

Data retrieval (form list):
    curl \\ |br|
    -v http://openbiomaps.org/projects/checkitout/pds.php \\ |br|
    -d "access_token=d4fba6585303bba8da3e6afc1eb9d2399499ef3e&scope=get_form_list"

Result of a successful get_form_list call:
    {"status":"success","data":[{"form_id":"93","form_name":"lepke űrlap"},{ …

Data retrieval (form fields):
    curl \\ |br|
    -v http://openbiomaps.org/projects/checkitout/pds.php \\ |br|
    -d "access_token=d4fba6585303bba8da3e6afc1eb9d2399499ef3e&scope=get_form_data&value=93"
    
  OR with central pds
    curl \\ |br|
    -F 'scope=get_form_data' \\ |br|
    -F 'value=93' \\ |br|
    -F 'project=checkitout' \\ |br|
    http://openbiomaps.org/projects/checkitout/pds.php
    
  OR with the access token to retrieve data from a restricted form
    curl \\ |br|
    -F 'access_token=...' \\ |br|
    -F 'scope=get_form_data' \\ |br|
    -F 'value=124' \\ |br|
    -F 'project=checkitout' \\ |br|
    http://openbiomaps.org/projects/checkitout/pds.php
    

Result of a successful get_form_data call:

API < v.2.1

    {"status": "success",
    
    "data":[    
    {"description":null,"default_value":null,"column":"egyedszam","short_name":"egyedszam","list":"","control":"minmax","count":"{30,40}","type":"numeric","genlist":null,"obl":"3","api_params":null},
    
    {"description":"faj neve","default_value":null,"column":"faj","short_name":"faj","list":"","control":"nocheck","count":"{}","type":"text","genlist":null,"obl":"1","api_params":null},{...}]}
    
API >= v.2.1

    {"status": "success",
    
    "data":[
    
    "form_header":{"login_name":"John Smith","login_email":"jsmith@openbiomaps.org"},
    "form_data":[
        {"description":"faj neve","default_value":null,"column":"faj","short_name":"faj","list":"","control":"nocheck","count":"{}","type":"text","genlist":null,"obl":"1","api_params":{"sticky":"off","numeric":"off","list_elements_as_buttons":"off"}},{...}]]}
    

Data upload:
    curl \\ |br|
    -i \\ |br|
    -X POST \\ |br|
    -H "Content-Type:application/x-www-form-urlencoded" \\ |br|
    -H "Authorization:Bearer ..." \\ |br|
    -d "scope=put_data" \\ |br|
    -d "form_id=128" \\ |br|
    -d "header=[\"obm_geometry\",\"obm_datum\",\"time\",\"datum\",\"comment\",\"longitude\",\"latitude\",\"observer\"]" \\ |br|
    -d "data=[{\"obm_geometr     y\":\"point(48.071187 19.293714)\",\"obm_datum\":\"2018-04-03 23:05\",\"time\":\"12\",\"datum\":\"2018-04-03\",\"comment\":\"asdad\",\"longitude\":\"0\",\"latitude\":\"0\",\"observer\":\"sdsaada\"}]" \\ |br|
    -d "ignore_warning=1" \\ |br|
    'http://openbiomaps.org/projects/checkitout/pds.php'

Data upload with multiple attachments (files):
    curl \\ |br|
    -F "access_token=..." \\ |br|
    -F 'scope=put_data' \\ |br|
    -F 'form_id=58' \\ |br|
    -F 'header=["faj","obm_geometry","obm_files_id"]' \\ |br|
    -F 'batch=[\\ |br|
    {"data":[{"faj":"Sylvia curruca","obm_geometry":"POINT(22.0 46.3)"}],"attached_files":"file1,file2"},\\ |br|
    {"data":[{"faj":"Lanius Collurio","obm_geometry":"POINT(21.5 47.1)"}],"attached_files":"file3"}]' \\ |br|
    -F 'file1=@file1' \\ |br|
    -F 'file2=@file2' \\ |br|
    -F 'file3=@file3' \\ |br|
    http://localhost/biomaps/projects/template/pds.php
    
Packed data upload. Data line in ZIP archive. This is the old mobile app's export format. The ZIP file contains the following files: |br|
    geometry.wkt |br|
    PICT01.JPG |br|
    PICT02.JPG |br|
    note.txt |br|
The ZIP file name is 'Sun May 13 08:52:51 CEST 2018.zip' which was created from the observation date-time sting. The note.txt contains the observation comment which can be associated with one column of the form. In this example, it is the 'faj'. The other 3 columns shouldn't be replaced or neglected. If there are some obligatory columns in the form, those can be filled by the default_value parameter. In this example, the 'egyedszam' column is an obligatory field that will be filled with '1'. Packed lines can be super packed. In this case 'packed_line' parameter should be changed to 'multipacked_lines' and the zip archive should contain the zip files detailed above.
    
    curl \\ |br|
    -F 'scope=put_data' \\ |br|
    -F 'table=dinpi' \\ |br|
    -F 'form_id=58' \\ |br|
    -F 'header=["obm_geometry","obm_files_id","faj","dt_to"]' \\ |br|
    -F 'default_values={"egyedszam":"1"}' \\ |br|
    -F 'packed_line=@Sun May 13 08:52:51 CEST 2018.zip' \\ |br|
    http://localhost/biomaps/pds.php

Data retrieval (non-authenticated report):
    wget http://localhost/biomaps/projects/dinpi/?report=2@szamossag&output=csv

Refresh token (from R):
    curl \\ |br|
    -F 'grant_type=refresh_token' \\ |br|
    -F 'refresh_token=...' \\ |br|
    -F 'client_id=R' \\ |br|
    http://openbiomaps.org/oauth/token.php
    
    Returns: |br|
    {"access_token":"...", |br|
    "expires_in":3600, |br|
    "token_type":"Bearer", |br|
    "scope":"get_form_data ...", |br|
    "refresh_token":"..."}
    
Project list (using central PDS):
    curl \\ |br|
    -F 'scope=get_project_list' \\ |br|
    http://localhost/biomaps/pds.php
    
    Returns: |br|
    JSON array of those project which has public upload forms, or the user (if logged) member of it.

General API answers
-------------------
Based on: https://labs.omniti.com/labs/jsend

JSON:
    {"status":"X","data":"","message":""}

X: success, error, fail
