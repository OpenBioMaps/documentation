PWA Map-query application
=========================

What is the OBM Map-query application?
--------------------------------------

The OBM Map-query application is an online/offline hybrid application, also
known as a Progressive Web App (PWA), designed to support fieldwork. It
provides access to an online OpenBioMaps database, allows users to query
records, and displays their spatial locations.

The application runs in a browser engine and is designed primarily for mobile
devices. Most operations require a network connection, but previously fetched
data can also be accessed offline.

To learn more about Progressive Web Apps, see:

[Progressive Web Apps on web.dev](https://web.dev/progressive-web-apps/)

How does it work?
-----------------

While online, you can display project data as a layer above the base map. The
data is shown as a clustered point layer, where the label inside each cluster
symbol indicates the number of features in that cluster.

The map provides filtering and query tools for fetching data from the online
database. By default, the application uses the current map viewport as the
query area. Applying this filter fetches all matching records visible within
the current extent.

Avoid querying an unnecessarily large area. Fetching and displaying a large
number of records can make the application slow or unresponsive.

After the requested data has been downloaded, the appearance of the cluster
layer changes slightly to indicate that the features are available on the
device. The downloaded features remain clustered because rendering many
individual points could significantly reduce application performance.

Selecting a cluster opens a scrollable modal dialog containing the attributes
of the features in that cluster.

The application runs in a browser but can be installed and launched without
the usual browser interface, making it behave similarly to a standalone
mobile application. Fetched project data is stored in offline storage. Base
maps are not downloaded automatically for offline use, although previously
viewed map tiles may remain available in the browser cache.

Supported browsers may offer an option to install the application on the
device. In Chrome and other Chromium-based browsers, this option may appear
in the address bar or the browser menu. Installing the PWA provides a more
app-like interface and makes its offline features easier to access.

Features
--------

- Display the user's current location as a yellow dot.
- Display GPS accuracy as a grey circle around the location marker.
- Display a track log.
- Start and stop track logging.
- Zoom to the user's current location.
- Query point features from the online database by drawing a circle or
  polygon, or by using the current map viewport.
- Store fetched records for offline access.
- Display the attributes of fetched records.

Limitations
-----------

- Only point features are supported.
- Base maps cannot be explicitly downloaded for offline use.
- Fetching a large number of records, for example more than 50,000, may cause
  performance or offline-storage problems.
- Offline availability of previously viewed base-map tiles depends on browser
  caching and is not guaranteed.
- PWA installation and offline behaviour may vary by browser and operating
  system.

Application URL
---------------

The application is available at the following project-specific URL:

`https://YOUR_SERVER/projects/YOUR_PROJECT/pwa-map/`

Replace:

- `YOUR_SERVER` with the host name of the OpenBioMaps server;
- `YOUR_PROJECT` with the project identifier or project directory name.

Configuration settings for the PWA application
----------------------------------------------

A small number of settings must be configured through the project
administration interface.

### MapServer layer

On the **Maps settings** page, add a new MapServer layer to the project's
*private map* file:

```
LAYER
    NAME "my_cluster"
    TYPE point
    STATUS on

    CONNECTIONTYPE postgis
    CONNECTION "host=localhost dbname=gisdata password={xxxxx} user=YOUR_PROJECT_admin options='--client_encoding=UTF8'"

    PROJECTION
        "init=epsg:4326"
    END

    METADATA
        "wms_title" "YOUR_PROJECT Cluster layer"
        "wms_srs"   "epsg:4326 epsg:900913"
    END

    DATA "obm_geometry FROM (SELECT * FROM YOUR_PROJECT WHERE ST_GeometryType(obm_geometry)='ST_Point') as new_table USING UNIQUE obm_geometry USING srid=4326"

    CLUSTER
        MAXDISTANCE 50
        REGION "ellipse"
    END

    LABELITEM "Cluster_FeatureCount"
    CLASSITEM "Cluster_FeatureCount"

    CLASS
        NAME "Clustered points"
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
END # WMS cluster layer
```

Replace the following placeholders:

- `NAME_OF_YOUR_LABELING_COLUMN` is the name of the column used to label
  individual points. A species-name column is a common choice.
- `YOUR_PROJECT` is the name of the database table queried by the layer. This
  is normally the project's base table.
- `YOUR_PROJECT_admin` is the PostgreSQL user used by the project.
- `{xxxxx}` must be replaced with the correct database password.

`MAXSCALEDENOM 100000` prevents features from being displayed when the map is
zoomed out beyond a scale of 1:100,000. This helps prevent MapServer from
having to calculate a very large number of clusters.

The database connection string must match the server environment. Do not copy
the example password or commit real database credentials to documentation or
a source-code repository. The safest approach is to copy the connection
settings from another working layer in the same project and verify every
value.

The example connection string is:

`CONNECTION "host=localhost dbname=gisdata password={xxxxx} user=YOUR_PROJECT_admin options='--client_encoding=UTF8'"`

The correct database host depends on the deployment. In a container-based
installation, it may be the name of the PostgreSQL service rather than
`localhost`.

### SQL query

On the **SQL query settings** page, create a query for the PWA application:

```
SELECT obm_id, obm_geometry, NAME_OF_YOUR_LABELING_COLUMN %selected%
FROM YOUR_PROJECT
%morefilter%
WHERE ST_GeometryType(obm_geometry)='ST_Point' AND %qstr%
```

Replace `NAME_OF_YOUR_LABELING_COLUMN` and `YOUR_PROJECT` with the same values
used in the MapServer layer.

Do not remove the following OpenBioMaps query placeholders:

- `%selected%`
- `%morefilter%`
- `%qstr%`

The predefined geometry filter restricts the result to point geometries.
This is required because the clustering layer cannot combine line and polygon
features.

Before enabling the application for users, test the query with a small
viewport and verify that:

- only records accessible to the current user are returned;
- every returned record has a valid `obm_id`;
- every returned geometry is a point geometry;
- the selected label column is included in the result; and
- the query completes within an acceptable time.

Installation
------------

After completing the MapServer and SQL-query configuration, open the following
URL once to initialise the application:

`https://YOUR_SERVER/projects/YOUR_PROJECT/pwa-map/setup.php`

Replace `YOUR_SERVER` and `YOUR_PROJECT` with the values used in the
application URL.

After setup has completed, open the application at:

`https://YOUR_SERVER/projects/YOUR_PROJECT/pwa-map/`

Always use HTTPS. A secure context is required for important PWA features,
including service workers, installation, location access, and reliable
offline operation.

After opening the application:

1. verify that the map loads;
2. grant location permission if location and track-log features are needed;
3. run a query over a small area;
4. verify that clusters and record attributes are displayed;
5. install the PWA using the browser's installation option, if available; and
6. test access to previously fetched records after disconnecting from the
   network.
