What is the OBM PWA application?
--------------------------------

Wants to learn more about PWA (Progressive Web Application) apps? Start here: https://web.dev/progressive-web-apps/

Our PWA APP is an online-offline hybrid application for supporting fieldwork. Width this app you can read the online database easily. How does it work? 

While you are online, you can see data as a layer above the base map. Practically it is a cluster styled layer, where the number of feature points is the label in the cluster symbols. There is a filter/query option on the map to fetch a lot of data from the database. The default filtering option is the viewport, so applying this filter will fetch all records of data from the database that you can see on the map. Practically, it is a bad idea to zoom out to a much larger area than you really need because a huge amount of fetched data can freeze your app. After the fetching is finished, the cluster layer style will have a slight change which indicates that these features are available on your device. The displaying method is still clustered due to displaying numerous features that can freeze the app. When you click on a cluster symbol, the attribution appears in a scrollable modal dialogue, so you can read all attributes of the clicked features.

The PWA app runs in the browser but can operate without the browser window. So it looks like a standalone mobile application. The fetched data is stored in offline storage, but the base map actually is not, but maybe can be cached if you browse it before an offline usage.

When you visit the app's URL from the CHROME browser, it will offer to install it as a desktop app. Use this option to access the offline usage features of the app, and the window size will be a bit larger without the browser frame.

Features
- Show your location (yellow dot)
- Show the GPS accuracy (grey circle around the location symbol)
- Show your tracklog
- Turn off-on tracklog
- Zoom to your location
- Query features from the online database by drawing a circle, polygon or actual viewport
- Display fetched data's attributes

Limitations
- It only supports POINT features
- Base maps can't be stored offline
- Fetching a large number of records (>50.000) can cause problems for offline storing and more...

Where is it?
- https://YOUR_SERVER/projects/YOUR_PROJECT/pwa/


Configuration settings for PWA application
------------------------------------------

Few settings are needed on the project admin interface.
On the Maps settings page, you have to create a new MapServer layer in the *private map* file:

```
  LAYER
        NAME "my_cluster"
        TYPE point
        STATUS on

        CONNECTIONTYPE postgis
        CONNECTION "host=localhost dbname=gisdata password={} user=YOUR_PROJECT_admin options='--client_encoding=UTF8'"

        PROJECTION
            "init=epsg:4326"
        END

        METADATA
            "wms_title"            "YOUR_PROJECT Cluster layer"
            "wms_srs"              "epsg:4326 epsg:900913"
        END

        DATA "obm_geometry FROM (SELECT * FROM YOUR_PROJECT WHERE ST_GeometryType(obm_geometry)='ST_Point') as new_table USING UNIQUE obm_geometry USING srid=4326"

        CLUSTER
            MAXDISTANCE 50
            REGION "ellipse"
        END

        LABELITEM "Cluster_FeatureCount"
        CLASSITEM "Cluster_FeatureCount"

        CLASS
            NAME 'Clustered points'
            MAXSCALEDENOM 100000
            EXPRESSION ("[Cluster_FeatureCount]" != "1")
            STYLE
                SYMBOL "circle"
                SIZE 30
                COLOR 51 153 204
                OUTLINECOLOR 30 30 30
                OUTLINEWIDTH 1
            END
            LABEL
                #FONT arial
                #TYPE TRUETYPE
                SIZE 8
                COLOR 255 255 255
                ALIGN CENTER
                PRIORITY 10
                BUFFER 1
                PARTIALS TRUE
                POSITION cc
            END
        END
        CLASS
            NAME "Single point"
            MAXSCALEDENOM 100000
            EXPRESSION "1"
            STYLE
                SIZE 12
                SYMBOL "circle"
                COLOR 000 130 255
                OUTLINECOLOR 30 30 30
                OUTLINEWIDTH 1
            END
            TEXT "[NAME_OF_YOUR_LABELING_COLUMN]"
            LABEL
                #FONT arial
                #TYPE TRUETYPE
                SIZE 8
                COLOR 0 0 0
                OUTLINECOLOR 255 255 255
                ALIGN CENTER
                PRIORITY 9
                BUFFER 1
                PARTIALS FALSE
                POSITION ur
            END
        END
        TOLERANCE 50
        UNITS PIXELS
    END #wms cluster layer
```

The *NAME_OF_YOUR_LABELING_COLUMN* is a column name which will be used as a label. Most common, is the species-name column.

The *YOUR_PROJECT* is the target table name which will used. Most commonm is the base project table.

MAXSCALEDENOM 100000 means that no features displayed over 1:100.000 zoom level which is generally a good pratcice to prevent overloading your mapserver when it tries to calculates millions of clusters...

More, you have to create an SQL query on the SQL QUERY SETTINGS page:

```
SELECT obm_id, obm_geometry, NAME_OF_YOUR_LABELING_COLUMN %selected% 
FROM YOUR_PROJECT 
%morefilter%
WHERE ST_GeometryType(obm_geometry)='ST_Point' AND %qstr%
```
As you can see, there is a predefined filter that uses only POINT data, which is because clustering cannot merge line and polygon data. 


Installation
------------

Load the following url at once to make your app ready to use: 

https://YOUR_SERVER/projects/YOUR_PROJECT/pwa/setup.php

**Make sure you connect using https (secure connection), otherwise the application will not work properly!**

