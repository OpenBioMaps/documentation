API documentation
*****************

HTTP methods: GET, POST, PATCH
Data methods: Authentication, Data retrieval, Data push, Settings update


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

POST types/scopes
-------------
put_data:        send/upload data using a selected form

PATCH types/scopes
-------------
*set_rules:*     update specific settings

API handlers:
-------------
/oatuh/token.php:: Authentication

/projects/checkitout/pds.php:: Data retrieval, Data push, Settings update

Examples
-------------
Authentication::
    curl -u mobile:123 http://openbiomaps.org/oauth/token.php -d "grant_type=password&username=foo@foobar.hu&password=abc123&scope=get_form_data+get_form_list+put_data"

Data retrieval (form list)::
    curl -v http://openbiomaps.org/projects/checkitout/pds.php -d "access_token=d4fba6585303bba8da3e6afc1eb9d2399499ef3e&scope=get_form_list&value=NULL,table=checkitout"

Result of a successful get_form_list call::
    {"status":"success","data":[{"id":"93","visibility":"lepke űrlap"},{ ...
    Ezt cseréljük majd le hogy így legyen:
    {"status":"success","data":[{"form_id":"93","form_name":"lepke űrlap"},{ …

Data retrieval (form fields)::
    curl -v http://openbiomaps.org/projects/checkitout/pds.php -d "access_token=d4fba6585303bba8da3e6afc1eb9d2399499ef3e&scope=get_form_data&value=93,table=checkitout"

Result of a successful get_form_data call::
    {"status":"success",
    "data":[
    {"description":null,"default_value":null,"column":"egyedszam","short_name":"egyedszam","list":"","control":"minmax","count":"{30,40}","type":"numeric","genlist":null,"obl":"3","api_params":null},
    {"description":"faj neve","default_value":null,"column":"faj","short_name":"faj","list":"","control":"nocheck","count":"{}","type":"text","genlist":null,"obl":"1","api_params":null},{... ]}


API answers
-----------
JSON::
    {"status":"X","data":"","message":""}
X: success, error, fail
