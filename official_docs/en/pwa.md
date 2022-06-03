What is PWA application?
------------------------

It is an online-offline hybrid application for supprting field work. Width this app you can read the online database easily. How it works? 
While you are online, you can see data as a layer above the base map. Practically it is cluster styled layer, where the number of feature points is the label
in the cluster symbols. There is a filter/query option on the map to fetch the a lot of data from the database. The default filtering option is the viewport, 
so appplying this filter will fetch all records data from the database that you can see on the map. Practically it is a bad idea to zoom out for much larger are
than you really need, because huge amount of fetched data can freeze your app. After the fetching finished the cluster layer style will a slighty change which
indicates that these features are available on your device. The displaying method still clustered due to displaying large amount of features can freeze the app.
When you click on a cluster sympbol the attribution appear in a scrollable modal dialog, so you can read all attributes of the clicked features.

The PWA app running in browser, but can operates without the browser window. So it look likes as a standalone mobile application. The fetched data stored in an offline 
storage, but the base map actually is not, but maybe can cached if you browse it before an offline usage.
When you visit the app's url from CHROME browser it will offer to install it as a desktop app. Use this option the access the offline usage features of the app and
the window size will be a bit larger without the browser frame.

Features
- Show your location (yellow dot)
- Show the GPS accuracy (gray circle around the location symbol)
- Show your tracklog
- Turn off-on traclog
- Zoom to your location
- Query features from the online database by drawing circle, polygon or actual viewport
- Display fetched data's attributes



Configuration settings for PWA application
------------------------------------------

Few settings needed on the project admin interface.
On the Maps settings page you have to create a new mapserver layer:

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
            "wms_title"            "zzz Cluster layer"
            "wms_srs"              "epsg:4326 epsg:900913"
        END

        DATA "obm_geometry FROM (SELECT * FROM YOUR_PROJECT) as new_table USING UNIQUE obm_geometry USING srid=4326"

        CLUSTER
            MAXDISTANCE 50
            REGION "ellipse"
        END

        LABELITEM "Cluster_FeatureCount"
        CLASSITEM "Cluster_FeatureCount"

        CLASS
            NAME 'Clustered points'
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
            EXPRESSION "1"
            STYLE
                SIZE 12
                SYMBOL "circle"
                COLOR 000 130 255
                OUTLINECOLOR 30 30 30
                OUTLINEWIDTH 1
            END
            TEXT "[species]"
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
More, you have to create an SQL query on the SQL QUERY SETTINGS page:

```
SELECT obm_id, obm_geometry, species %selected% 
FROM YOUR_PROJECT 
%morefilter%
WHERE %qstr%
```


