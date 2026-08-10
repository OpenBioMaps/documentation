Landing page
============
We can create custom landing pages for projects.
This opening page can be the built-in mainpage, which can be configured through the main-page-editor admin page and through direct configuration editing on the ``local_vars.php.inc``.

If the LOGINPAGE variable is set to mainpage, the main page template configured in the MAINPAGE variable will be loaded.

See the `server_install` for example settings for the local_vars.php.inc.

It is also possible to run a complete and independent application as a landing page, which is the so called custom_page application. This is also can be configured through its administrative pages. The custom page app recommended to written in javascript + html magt be with supoorting a JS framework like, VUEJS or Alpine.

The third option is using a single-page application which can be installed through the single-page-application (spa) modul. If you want to use a single-page-app as a landing page, you have to modify the project's router.

See the `modules` for more information about single page applications.


Here are some screenshot examples from different projects:

.. figure:: images/nyitolap_1.jpg
   :scale: 50 %
   :alt: Single-page app as landing page
   
    Single-page app as landing page

.. figure:: images/nyitolap_2.jpg
   :scale: 50 %
   :alt: Built-in landing page
   
   Built-in landing-page with basic settings and map

.. figure:: images/nyitolap_3.jpg
   :scale: 50 %
   :alt: Built-in landing page
   
   Built-in landing-page with image gallery

.. figure:: images/nyitolap_4.jpg
   :scale: 50 %
   :alt: boxed landing page
   
   Full screen with slide-in image gallery


.. figure:: images/nyitolap_5.jpg
   :scale: 50 %
   :alt: Built-in landing page
   
   Built-in landing-page with basic settings and custom summary table


.. figure:: images/nyitolap_6.jpg
   :scale: 50 %
   :alt: map landing page leaflet with map
   
   Project embedded in a landing page interface

.. figure:: images/nyitolap_7.jpg
   :scale: 50 %
   :alt: single-page app 
   
   A single-page app as a landing page

.. figure:: images/nyitolap_8.jpg
   :scale: 50 %
   :alt: single-page app 
   
   A single-page app as a landing page

.. figure:: images/nyitolap_9.jpg
   :scale: 50 %
   :alt: Built-in landing page
   
   Built-in landing-page with built-in custom project-managemnet application

