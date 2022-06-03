Frequently Asked Questions
**************************

What is OpenBioMaps?
--------------------
The OpenBioMaps is a framework for biological data with spatial attributes. In this framework it is allowed to create databases. The biological and spatial data in these databases are available for anyone.

The framework contains several different databases which served by more servers. These applications are the UMN Mapserver (which serve the web maps), the PostgreSQL database server (where cthe framework's and the databases' data stored), the PostGIS library (which handle the spatial queries), the Apache webserver (which handle the web output), the OpenLayers Javascript library (which handle the web map displaying in the browsers) and finally the Debian Linux operating system which serves the backround for the whole system. 

What is OpenBioMaps consortium?
-------------------------------
The OpenBioMaps consortium has been established through cooperation between public institutions and social organizations. Their goal was to develop and operate the OpenBioMap community database framework. The members of the consortium are equal partners and they have all contributed to achievenig this objective in some ways. The partnership can be extended, if the parties wishing to join are willing to accept the system's fundamentals, satisfy the specified conditions set and the partners accept the new member.


Current OpenBioMaps partners:


**University of Debrecen**

contact: Dr. Miklós Bán, banm@vocs.unideb.hu.


**Danube-Ipoly National Park Directorate**

contact: Zsolt Baranyai, baranyaizs@dinpi.hu.


**Eötvös Loránd University**

contact: Dávid Ritter


**WWF World Wildlife Fund for Nature Hungary**

contact: Katalin Sipos, katalin.sipos@wwf.hu


**Eszterházy Károly University**

contact: Dr. Erika Pénzesné Kónya, konya.erika@uni-eszterhazy.hu


**Milvus Group Association**

contact: István Kovács, 

**Danube-Dráva National Park Directorate**

contact: Ákos Gáborik

**Fertő-Hanság National Park Directorate**

contact: Gábor Takács


The OpenBioMaps consortium established at September 1, 2015. The OpenBioMaps Consortium Agreement will be available `here <docs/consortium_agreement_2015.pdf>`_.

How can I contact the consortium?
---------------------------------
By email:

management@lists.openbiomaps.org

How can I create a new database?
--------------------------------
You can set up new database to store biological data which contain geometrical data as well. That could be a database of a scientific project, which is used everyday, or that could be archive. Furthermore in the light of Open Access agreements of a scientific journal or grant you can use that database to store and present your data.

Every registered user can set up new database, but the database can get its final status only after the ratification of the OpenBioMaps consortium. The logined users can set up new database with the online templates. You can set up a new, empty database during couple of minutes.

How can I upload data?
----------------------
Data are stored in a PostgreSQL/PostGIS database. Every database has a project manager, and the project manager can decide who can upload data to the given database. You can type your data row by row into the database, or you can upload data eg. from gpx or excel files into the database with previously defined uploading templates.

How can I store queries and how can I refere them?
--------------------------------------------------
The logined users can save their queries on the web page. The saved queries have unique thread-mark and you can refer them, furthermore you can repeat those queries at any time. The wfs/wms url will be saved as well, therefore you can easily follow the database changes between the first query and its repeat.

The type of the reference: http://openbiomaps.org/projects/database/?loadquery=xx@abcd1234

If you load your reference into the browser, you will see the data points on a project map, furthermore the webpage will present the other values of the specific data points.

How can I sign up for OpenBioMaps?
----------------------------------
Invitation is required to registration. Any registered user can invite anyone.

For more information about registration, invitations, contact the creators, managers, or members of the databases.

Is there a programmable interface for developers?
--------------------------------------------------
The Project Data Service (PDS) allows you to query projects and user data on a per-project basis through URL requests from databases.

Example: http://openbiomaps.org/pds.php?scope=get_project_list

In this example, we list the projects available from the openbiomaps.org server in JSON format.

PDS returns the requested data in JSON format.

Returns an error message when a query is syntactically incorrect or invalid.

PDS takes into account the query authority. If the poller is not logged in, he / she will receive a response for basic authority queries

What languages are supported?
-----------------------------
There are no language restrictions, the site is currently available in Hungarian, in English and in Romanian and partially in Russian. Additional languages can be added by editing the https://github.com/OpenBioMaps/translations/blob/master/global_project_translations.csv file.

Databases also have independent language files that are independent of each other.

Which operating systems are compatible with OpenBioMaps?
---------------------------------------------------------
The web portal, map and database services are compatible with most of the operating systems.

During the developments we are not test compatibility.

How can I contribute to OpenBioMaps?
------------------------------------
 *   Creating databases
 *   Uploading data
 *   Creating new database servers 
 *   Hosting databases in your servers
 *   Adding new and improving translations
 *   Programmming
 *   With financial support

Shoud I pay for anything?
-------------------------
All OpenBioMaps features are completely free!

How and where the OpenBioMaps stores the data?
----------------------------------------------
Currently we have two servers in Debrecen at the University of Debrecen's computer center and one server in the ELTE Information Park. 1 server at MILVUS group in Târgu Mureș in Romania and one at Duna-Ipoly National Park Directorate.

There is database-level synchronization between servers. The contents of the databases are saved daily.

How can I join OpenBioMaps?
----------------------------------
Invitation is required to registration. Any registered user can invite anyone.

For more information about registration, invitations, contact the owners, managers, or members of the databases.

I lost my password, how can I get a new?
----------------------------------------
Don't worry, It is very easy to get a new password.

Follow the "lost password" link on the login page.

There you can type your login email address. After you sent it the system will send and email for you which contains a link.

Following this link you will be log in temporarily and you can change your password. 

Pink squares appear on the map page
-----------------------------------
It can be related with the layers or the mapfile settings.

How can I control the shared polygons?
--------------------------------------
On the profile page there are two links

    Own polygons
    Shared polygons

Following the first one, you will see those polygons that you uploaded or saved (using the save selection option).

Following the second link, you will see all the shared polygons including your own polygons.

In the own polygon page there is an option to share polygons with all users in the project or all logined users or anybody.

In both pages you can control, where would you like to see these polygons (as map selection or as uploading area). These options are marked by "eye" and "X" pictograms.

In both pages you can rename polygons. You can delete only your not shared polygons.

What is the RUM?
----------------
RUM is acronym of database openness classes:

Read - Upload - Modify

Each element can have a value of [-] or [0] or [+].

where

[-] is not public, [0] is partially public and the [+] is public

and the colors are: [-] black, [0] red and [+] green

e.g.

<font color="red">R</font><font color="green">U</font>M partial public read, public upload and no public modify 

Are there DOI for databases?
----------------------------
Every accepted database can get DOI through the DataCite DOI Service or an external repository.


All databases has a DOI metadata page like:

http://danubedata.org/index.php?metadata

We create an alias of this page as http://danubedata.org/doi/ after the database got its doi.

Our DOI prefix in DataCite is: 10.18426

The DOI suffixes are automatically generated and they are unique.

In every database it is possible to ask additional DOI-s for data subsets. These DOI-s will be extend the original database DOI after a /

How to set up archiving?
------------------------

1. To set up archiving you need to have ssh access to the server.
2. Download the `obm_archive.sh`, the `obm_archive_settings.sh` and the `.archive_list.txt` files from the [OBM scripts](https://github.com/OpenBioMaps/scripts/) repository

```
cd $HOME
mkdir bin && cd bin

wget https://raw.githubusercontent.com/OpenBioMaps/scripts/master/obm_archive.sh
wget https://raw.githubusercontent.com/OpenBioMaps/scripts/master/obm_archive_settings.sh
wget https://raw.githubusercontent.com/OpenBioMaps/scripts/master/.archive_list.txt

chmod 744 obm_archive.sh
```

3. Edit the `obm_archive_settings.sh` and the `.archive_list.txt` files to meet your server's and projects' setup. Further instructions and examples are provided it those files.
4. Set up a cronjob to run the `obm_archive.sh` on a daily basis.

```
15 04 * * 1-6 obm_archive.sh normal &> /dev/null
15 04 * * 7 obm_archive.sh full &> /dev/null
15 05 * * * obm_archive.sh clean &> /dev/null
```