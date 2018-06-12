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
get_project_vars: query general project variables (available for non logined users as well). Returns:

 - project_url: [url string] web address of the project
 - login_url: [url string] login address of the project
 - game: [on/off] game available for android mobile app
 - public_mapserv: [url string] url of publicly accessible map service
 - rserver_port: [numeric] numeric port number of R-Shiny server, accessible on project_url

get_project_list: get list and basis info of database projects available on the server. Returns:

 - project_table: [string]
 - creation_date: [date string]
 - Creator: [string]
 - email: [string]
 - stage: [string] experimental/testing/stable
 - doi: [string]
 - running_date: [date string],
 - licence: [string],
 - rum: [string],
 - collection_dates: [date range string],
 - subjects: [text]

 Additional parameters: 
    only-project [text], query project parameters only for the selected project, default is to query all accessible projects
    accessible [text] all/**accessible**
    If accessible parameter given and its value is "accessible" (default)
        If user already logined, get list of those projects where user has account and where there are public query/upload interfaces. 
        If the user not logined, query public projects only.

get_form_list:   query the list of available upload forms,

get_form_data:   query the fields of the selected form, Returns: see below.

 additional parameters: value [numeric] numeric id of a form

get_profile:     get profile data of a selected user

get_data:        get data rows from a selected data table (observation data)

get_specieslist: get species list from a project

get_history:     get history of a selected data row

get_report:      perform a predefined query and get the result

get_tables:      get list of tables in a project


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

qtable:         (non-authenicated table setting for data retreive)

report:         (non-authenticated data retreive using stored query)

output:         (non-authenticated data output setting)

LQ:             (non-authenticated) display data from a stored query result


Form Data (get_form_data results) Explanations
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
Obl: 1,2,3 (non obligatory, obligatory, soft error) Soft error can be handled as non obligatory.
Api_params: jason array of control values. Currently only 'sticky'
Spatial_limit: WKT polygon string of spatial limit. It is used if the Control type is spatial.

Examples
--------
Authentication:
    curl \\ |br|
    -u mobile:123 http://openbiomaps.org/oauth/token.php \\ |br|
    -d "grant_type=password&username=foo@foobar.hu&password=abc123&scope=get_form_data+get_form_list+put_data"

Data retrieval (form list):
    curl \\ |br|
    -v http://openbiomaps.org/projects/checkitout/pds.php \\ |br|
    -d "access_token=d4fba6585303bba8da3e6afc1eb9d2399499ef3e&scope=get_form_list&value=NULL&table=checkitout"

Result of a successful get_form_list call:
    {"status":"success","data":[{"form_id":"93","form_name":"lepke űrlap"},{ …

Data retrieval (form fields):
    curl \\ |br|
    -v http://openbiomaps.org/projects/checkitout/pds.php \\ |br|
    -d "access_token=d4fba6585303bba8da3e6afc1eb9d2399499ef3e&scope=get_form_data&value=93&table=checkitout"

Result of a successful get_form_data call:
    {"status":"success",
    
    "data":[
    
    {"description":null,"default_value":null,"column":"egyedszam","short_name":"egyedszam","list":"","control":"minmax","count":"{30,40}","type":"numeric","genlist":null,"obl":"3","api_params":null},
    
    {"description":"faj neve","default_value":null,"column":"faj","short_name":"faj","list":"","control":"nocheck","count":"{}","type":"text","genlist":null,"obl":"1","api_params":null},{... ]}

Data push:
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

Data push with attached files:
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
