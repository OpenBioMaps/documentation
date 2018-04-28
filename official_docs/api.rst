API documentation
*****************

HTTP methods:  GET, POST, PATCH

Data methods:  Authentication, Data retrieval, Data push, Settings update


GET types/scopes
-------------
get_form_list:   query the list of available upload forms

get_form_data:   query the fields of the selected form

get_profile:     get profile data of a selected user

get_data:        get data rows from a selected data table (observation data)

get_specieslist: get species list from a project

get_history:     get history of a selected data row

get_report:      perform a predefined query and get the result

get_tables:      get list of tables in a project

query:           (non-authenticated data retreive)

qtable:          (non-authenicated table setting for data retreive)

report:          (non-authenticated data retreive using stored query)

output:          (non-authenticated data output setting)


POST types/scopes
-------------
put_data:        send/upload data using a selected form


PATCH types/scopes
-------------
*set_rules:*     update specific settings


API handlers:
-------------
Authentication handler:

/oatuh/token.php: Authentication

Authentication based interface:

/projects/*projectname*/pds.php: Data retrieval, Data push, Settings update

Non authenticated requests:

/projects/*projectname*/index.php


Examples
-------------
Authentication:
    curl -u mobile:123 http://openbiomaps.org/oauth/token.php -d "grant_type=password&username=foo@foobar.hu&password=abc123&scope=get_form_data+get_form_list+put_data"

Data retrieval (form list):
    curl -v http://openbiomaps.org/projects/checkitout/pds.php -d "access_token=d4fba6585303bba8da3e6afc1eb9d2399499ef3e&scope=get_form_list&value=NULL,table=checkitout"

Result of a successful get_form_list call:
    {"status":"success","data":[{"id":"93","visibility":"lepke űrlap"},{ ...
    Ezt cseréljük majd le hogy így legyen:
    {"status":"success","data":[{"form_id":"93","form_name":"lepke űrlap"},{ …

Data retrieval (form fields):
    curl -v http://openbiomaps.org/projects/checkitout/pds.php -d "access_token=d4fba6585303bba8da3e6afc1eb9d2399499ef3e&scope=get_form_data&value=93,table=checkitout"

Result of a successful get_form_data call:
    {"status":"success",
    "data":[
    {"description":null,"default_value":null,"column":"egyedszam","short_name":"egyedszam","list":"","control":"minmax","count":"{30,40}","type":"numeric","genlist":null,"obl":"3","api_params":null},
    {"description":"faj neve","default_value":null,"column":"faj","short_name":"faj","list":"","control":"nocheck","count":"{}","type":"text","genlist":null,"obl":"1","api_params":null},{... ]}

Data push:
    curl -i -X POST -H "Content-Type:application/x-www-form-urlencoded" -H "Authorization:Bearer   84e2ccd56a9657f3ad768d289fe2c8f09e44203d" -d "scope=put_data" -d "form_id=128" -d "header=[\"obm_geometry\",\"obm_datum\",\"time\",\"datum\",\"comment\",\"longitude\",\"latitude\",\"observer\"]" -d "data=[{\"obm_geometr     y\":\"point(48.071187 19.293714)\",\"obm_datum\":\"2018-04-03 23:05\",\"time\":\"12\",\"datum\":\"2018-04-03\",\"comment\":\"asdad\",\"longitude\":\"0\",\"latitude\":\"0\",\"observer\":\"sdsaada\"}]" -d "ignore_warning=1" 'http://openbiomaps.org/projects/checkitout/pds.php'

Data retrieval (non-authenticated report):
    wget http://localhost/biomaps/projects/dinpi/?report=2@szamossag&output=csv

API answers
-----------
JSON::
    {"status":"X","data":"","message":""}
X: success, error, fail
