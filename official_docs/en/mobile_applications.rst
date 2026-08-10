:author: Miklós Bán
:date: 2026-08-09

Mobile applications
*******************

There are numerous mobile apps designed to support and implement OpenBioMaps’ features. 
These include online and offline apps, as well as apps for data retrieval and data collection. 
They range from progressive web apps to native mobile apps.

Offline application for Android and iPhone mobile devices
=========================================================

How does the app work?
----------------------
This is an application designed for offline field data collection, providing a flexible tool for 
supporting custom data collection tasks. Observation data can be recorded by filling in any custom 
forms. There are no pre-defined data collection forms or methods created by OpenBioMaps. All settings 
relating to data collection depend on the settings of the projects included. Consequently, which 
projects a user has access to, which forms within those projects they can access, and what data 
fields are available on those forms and how they work all depend on the project settings.

The app only allows logged-in users to collect data, but it does not offer a registration option, 
although some projects do allow for simple and automatic registration.

Development
-----------
This app is developed by the Ecollab Ltd. in react-native / expo.


Usage first steps
=================

Server choice
.............

You’ll also need an internet connection for this.

Project choice
..............

You’ll also need an internet connection for this.

Log in
......

You’ll also need an internet connection for this.
This is done by entering your email address and password.

Form selection
..............

Once you have logged in, the projects and their forms available on the server 
will become accessible. Projects and forms that are publicly accessible will 
also be visible at this point.
The forms will be available offline usage as well, once you loaded them.

Pin form to the home screen
...........................

You can pin frequently used forms to the home screen for quicker access by tapping 
the thumbtack icon next to the form’s name.

App structure
=============

Main screen
...........
Access to Map, Forms, Collectead data, Settings, Tracklogs, Tools

Quick access to (pinned) forms

Running observation events indicated on pinned form buttons' footer.


Map screen
..........
It is used to view recorded data and permanent sampling locations.


Forms screen
............

* Occasional observation
* Observation event

Form are indicating with a ! if there is an update available. Click on form name long to force server update.
Downloaded (offline avalilbele forms are marked) to distinguish froms not available for offline work.

Running observation events indicated next to form name.

Collected data screen
.....................
List of recorded data, 
  Highlightes values in the records list, such as species name or number of indviduals, depending on the server settings (bold_yellow module)
Data syncronistaion,
Editing option to not syncronised data
Delete syncronised data from the device


Tracklogs screen
................

Tracklogs can be recorded in the app independently of form runs. These tracklogs are 
added to the project’s tracklog table during synchronisation.

On this screen you can view, launch and syncronise tracklogs.

Tools screen
------------
Swiss army knife tools for field biologist.

- Random number generator
- Custom list creator: e.g. ring number list

Settings screen
---------------

Language selection
..................

Currently English, Romanian, Hungarian, French, German, Kyrgyz and Russian supported. 
Please contribute to app translation on https://translate.openbiomaps.org/projects/ecollab/expo-app/

Theme:
......

System, Dark and Light themes are available

Backup and export
.................
Createing backup is useful for debugging application

Export can be used for get all data from the app which can be procceed by other tools. It is creating standard files, like csv, gpx, and jpeg files.


Form settings
.............

Pinned field values: 
    Reiinitailize always when opening forms - This is a safe option to use pins. This is the default behavior. It can becaome annoying if use two forms parallel and the forms forget your pinned values always. 
    Server settings allways - If you don't like the pins and sometimes accidentally pinnig values.
    Keep user settings until syncronisation - This is ususal practiacal setting for those who collect same type of data within a day, and syncronize data at end of the day. In this case next day there will be no pinned values remain in the forms on the next day.
    Always keep user settings - this a quite dangerous settings, only very special cases recommenden to use.

Sound notification on successful or failed data recordings

Collected data
..............

View attached files
Turn on automatic syncronisation
Allways show acton buttons below record data on recorded data screen

GPS and Tracklog settings
.........................

The frequency and distance based filtering of GPS usage. Both settings affect both single point recoring and tracklog point recording.
The distance filter prevent query new position if the mobile device is only moving within the given distance. Keep this number 1 to 5.

The time frequency of tracklog points: default is 5 sec. It has strong effect on accu usage. What is this effect? Is there any guess measurment, what happening if we set this to one from five? Five times more accu usage?

Storage
.......
Delete unused files, sessions; clear selections and autocomplete lists


Permissions
...........
Check and access operating system settings of location service usage


Feedback
........


Mobile application settings on the server
-----------------------------------------

Forms
.....

:doc:`Upload form management <../upload_forms>`



Online application for mobile devices
=====================================

* :doc:`map based data query app <../pwa>`
* :doc:`sampling site manager app <../mapp>`
