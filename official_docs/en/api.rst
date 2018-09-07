.. |br| raw:: html

    <br>
    
API documentation
*****************
HTTP methods:  GET, POST, PATCH

API tools:  Authentication, Data retrieval, Data push, Settings update


API handlers:
-------------
Authentication handler (oauth):

/oatuh/token.php: Authentication

Authentication based interface (pds):

/projects/*API_VERSION*/*projectname*/pds.php: Data retrieval, Data push, Settings update 

Non authenticated requests (web):

/projects/*projectname*/index.php

PDS API version:
................
Example: http://openbiomaps.org/projects/dead_animals/v2.1/pds.php
The default version setting (if the version string missing from the URL) is 1.1., which compatible with the 2.0 and backward compatible with the 1.0.


OAUTH
-----------
An oauth2 implementation based on ttps://bshaffer.github.io/oauth2-server-php-docs/. OAUTH used in the web interface and in the PDS as well.

Variables
.........
grant_type:     password
username:       a rergistered email address
password:       password string
scope:          list of requested scope access in the autenticated session
access_token:   a valid access token

html authentication of clients is nesessary

Available clients are mobile,R,web


PDS 
----
OBM API interface. Created for R and mobile interface. It uses the OAUTH interface for authentication.

Variables
.........
scope:      data methods: see below

value:      some scope uses it

header:     (put data) JSON list of table columns' names

ignore_warning: (put data) ignore upload warnings

form_id:        (put_data) set form id

data:           (put data) JSON array of upload data


GET type scopes
...............
get_project_vars: query general project variables (available for non logined users as well). 
 Additional parameters: 
     project [text]: if not set default is the *template* project

 Returns:

 - project_url [url string]: web address of the project
 - project_description [text string]: short description of project 
 - game [on/off]: game available for android mobile app
 - public_mapserv [url string]: url of publicly accessible map service
 - rserver_port [numeric]: numeric port number of R-Shiny server, accessible on project_url

get_project_list: get list and basis info of database projects available on the server. 
 Additional parameters:
     only-project [text]: query project parameters only for the selected project, default is to query all accessible projects
     accessible [text]: all/**accessible**. If *accessible* parameter given and its value is "accessible" (default)
     
     - If user already logined, get list of those projects where user has account and where there are public query/upload interfaces. 
     - If the user not logined, query public projects only.

 Returns:

 - project_table [string],
 - creation_date [date string],
 - Creator [string],
 - email [string],
 - stage [string] experimental/testing/stable,
 - doi [string],
 - running_date [date string],
 - licence [string],
 - rum [string],
 - collection_dates [date range string],
 - subjects [text],

get_form_list:   query the list of available upload forms,

get_form_data:   query the fields of the selected form

 Additional parameters: value [numeric] numeric id of a form.
 
 Returns: see below.

get_profile:     get profile data of a selected user

get_data:        get data rows from a selected data table (observation data)

get_specieslist: get species list from a project

get_history:     get history of a selected data row

get_report:      perform a predefined query and get the result

get_tables:      get list of tables in a project

get_trainings:  get list of available trainings/forms

 Returns: set of traning titles, ids and descriptions,...

get_training_questions: get list of questions for the selected training

 Additional parameters: value [numeric] numeric id of a training.
 
 Returns: set of questions,answers and settings

training_results:   status list of users' trainings per forms. Status can be -1 (not sent), 0 (not validated yet), 1 (done, ok)

training_toplist: toplist of trainings. Mean, Max, Count values for each forms.
 Additional parameters: value [text] summary without names (nonames).
 
get_mydata_rows: json array of uploaded data
 Additional parameters: value [numeric] limit of array length. If 0, no limit, default is no limit.


POST type scopes
................
put_data:        send/upload data using a selected form


PATCH type scopes
.................
*set_rules:*     update specific settings


WEB API
-------
Some kind of data access available on the web interface using stored unique URLs. These

Variables
.........
query:          (non-authenticated data retreive)

query_api:      (non-authenticated data retreive, resulting JSON, XML, CSV output)

qtable:         (non-authenicated table setting for data retreive)

report:         (non-authenticated data retreive using stored query)

output:         (non-authenticated data output setting)

LQ:             (non-authenticated) display data from a stored query result

Get list of active (known) OpenBioMaps servers using query_api:

curl http://openbiomaps.org/projects/openbiomaps_network/index.php -G -d 'query_api={"available":"up"}&output=json&filename='


Form Data (get_form_data results) explanations
----------------------------------------------
Description: Optional column description
Default value: Fix value for all observation. It can be controlled with some options.
 
 - '_input' it works as any other field with sticky flag. 
 - '_list' it works as any other list type field with sticky flag.

in any other case the value can not be changed by the user users and the field can be hidden.

Column: The name of the column in the database

Short_name: Visible name of the column for the users

List: json array for menu items of a select menu. Can be {key:value} or [value,value] format

Control: Data checking commands: custom_check, minmax, spatial, nocheck, NULL

Count: (json array) If the control='minmax' this field contains the limit values, e.g 1:100

Type: column's openbiomaps type:
 
 - autocomplete	(json array)
 - boolen	
 - crings (colour rings - text)	
 - date (YYYY-MM-DD or other clear format)
 - datetime (YYYY-MM-DD HH:mm:ss)
 - file_id (file names as id by the server) 
 - line (WKT geometry string)
 - list (json array)
 - numeric	
 - point	(WKT geometry string)
 - polygon (wkt geometry string)
 - text 
 - time (HH:mm)
 - timetominutes (numeric value between  0 and 1440)
 - tinterval idő intervallum (HH:mm - HH:mm)
 - wkt (WKT sting)

Genlist: json array for menu items of an autocomplete menu. Can be  {key:value} or [value,value] format
Obl: 1,2,3 (obligatory, non-obligatory, soft error) Soft error can be handled as non obligatory.
Api_params: jason array of control values. Currently only 'sticky'
Spatial_limit: WKT polygon string of spatial limit. It is used if the Control type is spatial.

Training explanations and examples
----------------------------------
Examples:

curl -F 'scope=get_trainings' -F 'access_token=9d45...' -F 'project=dinpi' http://localhost/biomaps/pds.php

Result of a successful call:
    {"status":"success","data":[{"id":"1","form_id":"95","html":"<div>...",,"task_description":"<div>...","enabled":"t","title":"Gyakorlás I.","qorder":"1","project_table":"dinpi"},{
    
curl -F 'scope=get_training_questions' -F 'access_token=9d45...' -F 'project=dinpi' http://localhost/biomaps/pds.php

Result of a successful call:
    {"status":"success","data":[{"qid":"1","training_id":"1","caption":"...?","answers":"[{"Answer": "...","isRight": "false" }, ]","qtype":"multiselect"}]}
    
    qtype can be multiselect or singleselect
    
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

Examples
--------
Authentication:
    curl \\ |br|
    -u mobile:123 http://openbiomaps.org/oauth/token.php \\ |br|
    -d "grant_type=password&username=foo@foobar.hu&password=abc123&scope=get_form_data+get_form_list+put_data"

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
    
  OR with access token to retrieve data of a restricted form
    curl \\ |br|
    -F 'access_token=...' \\ |br|
    -F 'scope=get_form_data' \\ |br|
    -F 'value=124' \\ |br|
    -F 'project=checkitout' \\ |br|
    http://openbiomaps.org/projects/checkitout/pds.php
    

Result of a successful get_form_data call:
    {"status":"success",
    
    "data":[
    
    {"description":null,"default_value":null,"column":"egyedszam","short_name":"egyedszam","list":"","control":"minmax","count":"{30,40}","type":"numeric","genlist":null,"obl":"3","api_params":null},
    
    {"description":"faj neve","default_value":null,"column":"faj","short_name":"faj","list":"","control":"nocheck","count":"{}","type":"text","genlist":null,"obl":"1","api_params":null},{... ]}

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
The ZIP file name is 'Sun May 13 08:52:51 CEST 2018.zip' which created from the observation date-time sting. The note.txt contains the observation comment which can be associated with one column of the form. In this example it is the 'faj'. The other 3 columns shouldn't be replaced or neglected. If there are some obligatory column in the form, those can be filled by the default_value parameter. In this example the 'egyedszam' column is an obligatory field which will be filled with '1'. Packed lines can be super packed. In this case 'packed_line' parameter should be changed to 'multipacked_lines' and the zip archive should contains zip files detailed above.
    
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
    
Project list (using central pds):
    curl \\ |br|
    -F 'scope=get_project_list' \\ |br|
    http://localhost/biomaps/pds.php
    
    Returns: |br|
    JSON array of those project which has public upload forms, or the user (if logined) member of it.

General API answers
-------------------
Based on: https://labs.omniti.com/labs/jsend

JSON:
    {"status":"X","data":"","message":""}

X: success, error, fail
