.. raw:: html

    <style> 
    .red {color:#ff0000;font-weight:bold;}
    .green {color:#00ff00;font-weight:bold;}
    </style>

Frequently Asked Questions
**************************

What is OpenBioMaps?
--------------------
OpenBioMaps is a software and services platform for managing biological data. It can be used on its own or as a service. It can be used to create database-based projects that can be used simultaneously by multiple users with different devices and access privilege levels. If you do not wish to maintain your own server, you can use it as a service, as some institutions also operate servers that host research or citizen-science projects for no charge.

What is OpenBioMaps consortium?
-------------------------------
OpenBioMaps is a consortium of public institutions and social organisations. Their aim is to develop OpenBioMaps software and maintain freely available services based on it. The members of the consortium are equal partners and they have all contributed to achievenig this objective in some ways. The partnership can be extended, if the parties wishing to join are willing to accept the system's fundamentals, satisfy the specified conditions set and the partners accept the new member.


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

contact: Edgár Papp, 


**Danube-Dráva National Park Directorate**

contact: Ákos Gáborik


**Fertő-Hanság National Park Directorate**

contact: Gábor Takács


The OpenBioMaps consortium established at September 1, 2015. The OpenBioMaps Consortium Agreement will be available `here <docs/consortium_agreement_2015.pdf>`_.

How can I contact the consortium?
---------------------------------
By email:

management@lists.openbiomaps.org

How can I create/found a new database-project?
----------------------------------------------
You can set up new database to store biological data which contain geometrical data as well. That could be a database of a scientific project, which is used everyday, or that could be archive. Furthermore in the light of Open Access agreements of a scientific journal or grant you can use that database to store and present your data.

Every registered user can set up new database, but the database can get its final status only after the ratification of the OpenBioMaps consortium. The logined users can set up new database with the online templates. You can set up a new, empty database during couple of minutes.

How can I upload data?
----------------------
Simply answered: using data upload forms.
Or perhaps using any PostgreSQL client, although this solution is only recommended for occasional imports of large amounts of data.

How can I access data?
----------------------
- Via the web interface with map or text queries. 
- Using a PostgeSQL client.
- Using the OpenBioMaps R package.
- Using data sharing via the web interface.
- Data export via the web interface.

How can I sign up for an OpenBioMaps project?
---------------------------------------------
Invitation is required to registration. Any registered member can invite new users.

For more information on registration and invitations, please contact the creators or administrators of the database you wish to join.

Is there a programmable interface for developers?
--------------------------------------------------
Yes. The Project Data Service (PDS) allows you to query projects and user data on a per-project basis through URL requests from databases.

Example: https://openbiomaps.org/pds.php?scope=get_project_list

For more information visit the API documentation.

What language support is available?
-----------------------------------
There are no language restrictions, but the OpenBioMaps is currently available in Hungarian, nglish Romanian, Spanish and partially in Russian. Additional languages or translations can be added through https://translate.openbiomaps.org interface.

Each project can have individual language settings and associated translations.


How can I contribute to OpenBioMaps?
------------------------------------
 *   Creating/founding database-project
 *   Uploading data into a database-project
 *   Creating new OpenBioMaps server
 *   Hosting databases in your server
 *   Adding new or improving existing translations
 *   Software development
 *   Financial support

Shoud I pay for anything?
-------------------------
All OpenBioMaps services and components are completely free!

How and where the OpenBioMaps stores the data?
----------------------------------------------
Each OpenBioMaps server stores the data in its own database and file system.

Is there any backup solution?
-----------------------------
No centralised backup, as there is no centralised data management in OpenBioMaps. Each server has its own backup solution, but some servers use each other's storage capacity for archiving.

I lost my password, how can I get a new?
----------------------------------------
Don't worry, it's very easy to get a new password.

Follow the "lost password" link on the login page.

There you can enter your login email address. Once you submit it, you will receive an email from the system containing a link that you can follow to log in to your account and set a new password.

Pink squares appear on the map page
-----------------------------------
This may be due to some kind of configuration error, which may be related to the map layers or the settings of the data queries.

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

Is it possible to assign a DOI to databases?
--------------------------------------------
Yes, all databases in a finalized state can receive a DOI using the DataCite DOI Service.


All databases has a DOI metadata page like:

https://dinpi.openbiomaps.org/projects/danubefish/index.php?metadata

Our DOI prefix in DataCite is: 10.18426

The DOI suffixes are automatically generated and they are unique.

In every database it is possible to assigne additional DOI-s for datasets.

Where can I find the list of the existing OpenBioMaps servers?
--------------------------------------------------------------
The servers that have registered can be found in the OpenBioMaps database at https://openbiomaps.org/projects/openbiomaps_network .

How does the OpenBioMaps mobile app work?
-----------------------------------------
On Iphone or Android. Only registered users can access the forms available to them. After logging in and downloading the forms, the app can be used offline.

Where can I found the OpenBioMaps R package?
--------------------------------------------
For now, only available as a developer package here: https://github.com/OpenBioMaps/obm.r

