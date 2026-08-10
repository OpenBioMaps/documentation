# Modules

Modules are configurable extensions to the OpenBioMaps web application. They
can add user-interface components, data-processing functions, export formats,
administrative tools, APIs, or integrations with external services.

There are two main module scopes:

- **Project-level modules** provide functions that apply to the whole project,
  such as spatial-shape management, attachment support, or PostgreSQL user
  creation.
- **Table-level modules** apply to a particular data table, such as map-page
  filters, result displays, data transformations, or export formats.

Modules are connected to hooks in the application. Most user-facing hooks are
located on the map page and the profile page, although modules can also add
administration pages, APIs, background jobs, and upload-related functions.

Most modules accept parameters in JSON format. Some modules instead provide a
dedicated administration interface, and some require both JSON parameters and
additional database or MapServer configuration.

> **Version compatibility:** The available modules and their parameters can
> change between OpenBioMaps releases. The module administration page of the
> installed application is the authoritative list of modules available to a
> project. Check the module source and release notes before copying a
> configuration from another installation.

## Module administration

Modules can be enabled and configured on the **Project administration →
Modules** page.

A module can usually be:

- added to the project;
- assigned to users or groups;
- configured with JSON parameters;
- enabled or disabled; and
- opened through a module-specific administration page, if one is provided.

Module names and JSON keys are case-sensitive. Validate JSON before saving it.
JSON does not allow comments or trailing commas.

### Adding a custom module

Custom modules can be uploaded and added to a project. Developers should use
the example modules in `resources/includes/modules/examples/` as a starting
point and compare their implementation with modules included in the installed
OpenBioMaps release.

Custom module code must be reviewed before deployment. A module runs as part
of the application and may have access to project data, the authenticated
user's session, and database connections.

### Module access

The same module can be added more than once with different access settings or
parameters. This allows administrators to provide different configurations
to different users, groups, or tables.

For example:

- `allowed_columns` can expose different columns to different groups; and
- `text_filter` can provide table-specific filter columns in a project that
  contains multiple data tables.

The **Access** column controls the general audience of a module instance. The
available choices include public access and access restricted to logged-in
users.

The **Group access** column further restricts the module instance to selected
project groups or individual users.

When several instances of the same module apply to one user, test which
configuration is selected or combined by the installed OpenBioMaps version.
Avoid overlapping access rules unless their behaviour is understood.

### Enabling and disabling modules

Each configured module instance can be enabled or disabled. Disabling a
module preserves its configuration but prevents it from being used.

After changing a module's status, test the relevant page with users from each
affected access group. Some modules also create database objects or retain
module-specific settings when disabled.

### Removing modules

The module administration interface does not currently provide a general
option for removing an installed module from the application.

A configured module instance may be disabled. Do not manually delete module
files or database objects unless the module's removal procedure is known and
a backup is available.

### Module parameters

Most modules accept JSON parameters directly on the module administration
page. Other modules provide a dedicated administration tab for module-specific
tasks. `box_load_selection` is an example of a module with its own
administrative interface.

Examples in this document use placeholders such as `YOURTABLE`, `column_name`,
and `schema.table`. Replace these placeholders with identifiers from the
project.

## Project-level modules

### `box_load_selection`

The `box_load_selection` module manages reusable spatial shapes.

It provides the following functions:

- Users can upload points, lines, and polygons. ESRI Shapefile is commonly
  used, but other standard spatial formats may also be supported.
- Uploaded shapes can be used to define the spatial extent of a data query.
- A shape can provide the geometry of a record during web or file upload.
- Shapes can be shared with other users.
- Shapes available to the user can be downloaded and displayed by the mobile
  application.

Newly uploaded shapes are not visible to other users by default. Project
administrators can grant users permission to use each shape for queries or
data uploads.

Users can manage shared shapes through the **Shared geometries** module block
on their profile page. Project administrators can manage these permissions
through the `box_load_selection` administration tab.

When the module is enabled, a **Spatial query** box appears on the map page.
Users can select an available shape and run a spatial query against it. For
polygon geometries, the interface may allow users to choose whether records
intersecting the polygon boundary are included.

If an upload form uses an `obm_geometry` field, its map control can offer a
**Geometry from list** option. Selecting a named shape inserts its WKT
geometry into the upload field.

The mobile application can display available upload shapes semi-transparently
on form maps, labelled with their names.

**Parameters:** None. The module uses its dedicated administration interface.

### `photos`

The `photos` module enables photo and other attachment fields on upload forms
and displays attached images on record data-sheet pages.

File-size limits, permitted file types, storage, access control, and backup
requirements must also be configured at the application and server levels.

**Parameters:** None.

### `create_pg_user`

The `create_pg_user` module allows authorised users to create personal
PostgreSQL accounts.

When the module is enabled:

- a **Create PostgreSQL user** box appears on the profile page for authorised
  users;
- users can create and renew their own database account;
- the generated account is assigned to the project's PostgreSQL user group;
  and
- the account can be used by database clients such as QGIS.

By default, the generated account:

- has read access to the project's database tables;
- is limited to one simultaneous client connection; and
- expires after one year.

The generated account is added to the PostgreSQL group named after the
project, commonly in the form `PROJECT_user`. A database administrator can
grant additional permissions, such as write access to selected tables, but
should follow the principle of least privilege.

Users can renew their access before or after expiry, subject to the installed
module's rules.

The following screenshot shows an example PostgreSQL/PostGIS connection in
QGIS:

![Adding an OpenBioMaps PostGIS connection in QGIS](images/qgis_connect.jpg)

Do not expose PostgreSQL to the public internet without appropriate firewall,
TLS, authentication, and access-control settings.

**Parameters:** None. Current releases may provide a dedicated administration
page.

### `computation`

The `computation` module provides project-specific computation functions.

Its exact behaviour depends on the installed module version and project
configuration. Review the module implementation before enabling it in a
production project.

**Parameters:** None documented.

### `custom_filetype`

The `custom_filetype` module supports project-specific preparation of custom
download formats, such as an Observado-style CSV file.

The output format and any required custom implementation depend on the
project.

**Parameters:** None documented.

### `taxon_meta`

The `taxon_meta` module provides taxon-related metadata functions.

Its user interface, required database structure, and configuration should be
verified against the installed module version.

**Parameters:** None documented.

## Table-level modules

### `additional_columns`

The `additional_columns` module defines columns used to associate records
across multiple data tables.

When tables are connected through a shared identifier, queries can include
the related records for that identifier. Users can bypass these joins by
selecting **Ignore table joins** on the map page.

For example, a project may store parent and offspring records in separate
tables and use a shared burrow identifier as the join column.

Use this module together with `join_tables`.

The module returns:

- an array of columns at index `0`; and
- an associative array of column names at index `1`.

**Parameters:**

```json
[
  "column_name_1",
  "column_name_2"
]
```

### `allowed_columns`

The `allowed_columns` module supplements row-level data-access rules with
column-level restrictions.

Row-level rules determine which records a user can access. This module
determines which columns remain visible when a record is subject to a
`restricted` or `no-geom` rule, or when no matching rule exists.

The module is intended for projects whose base access level is not public and
whose data tables use the corresponding rules table.

**Parameters:**

```json
{
  "for_sensitive_data": [
    "column_visible_for_sensitive_records"
  ],
  "for_no-geom_data": [
    "column_visible_for_records_without_geometry_access"
  ],
  "for_general": [
    "column_visible_when_no_rule_matches"
  ]
}
```

Parameter meanings:

- `for_sensitive_data` lists columns visible for sensitive records.
- `for_no-geom_data` lists columns visible for `no-geom` records. If this key
  is omitted, all columns are accessible for those records.
- `for_general` lists columns visible when no rule matches. If this key is
  omitted, all columns are restricted in that case.

Test the effective permissions with public, authenticated, group-member, and
administrator accounts. Column restrictions must not be treated as a
replacement for correct database and API access control.

### `bold_yellow`

The `bold_yellow` module identifies important fields in result summaries.

Configured columns are highlighted in bold yellow in detailed result lists.
The mobile application also uses this configuration to select values shown in
the **Collected data** summary labels.

**Parameters:**

```json
[
  "column_name_1",
  "column_name_2"
]
```

### `box_load_coord`

The `box_load_coord` module adds a **Position** block below the map.

The block:

- displays the coordinates of the current pointer position; and
- allows a user to enter latitude and longitude values and place the
  corresponding point on the map.

The parameters map user-facing coordinate-system names to EPSG codes.

**Parameters:**

```json
{
  "wgs84": "4326",
  "eov": "23700"
}
```

Only configure coordinate systems supported by the project and its mapping
components.

### `box_load_last_data`

The `box_load_last_data` module adds a **Quick queries** box to the map page.

It provides queries for:

- the current user's most recent upload;
- the most recent upload by any user; and
- the most recently uploaded records.

The first two options return one record. The parameter controls the number of
records returned by the third option. The documented default is 10.

**Parameters:**

```json
[
  10
]
```

### `box_custom`

The `box_custom` module loads a project-specific custom box on the map page.

The custom implementation must be placed in the project's
`local/includes/modules/` directory. Its class must provide at least the
`print_box()` and `print_js()` methods.

For a custom module stored in:

`local/includes/modules/hrsz_query.php`

the parameter contains the file's base name:

```json
[
  "hrsz_query"
]
```

The corresponding class is expected to be named `hrsz_query_Class`.

Custom module code must validate input, escape output, enforce permissions,
and use parameterised database queries.

### `identify_point`

The `identify_point` module allows users to identify one or more points on the
map and displays selected attribute values in a map popup.

**Parameters:**

```json
[
  "column_name_1",
  "column_name_2"
]
```

Only include columns that the module's intended audience is permitted to
access.

### `cameratrap_api`

The `cameratrap_api` module provides communication between a camera-trap
dashboard and the Nextcloud API.

Its functions include:

- managing cameras and analyses;
- uploading and downloading images;
- starting analyses; and
- managing the Nextcloud credentials required by the integration.

The module creates or uses module-specific database objects. Review its SQL
installation file and access requirements before enabling it.

**Parameters:** None documented.

### `nextcloud_connect`

The `nextcloud_connect` module connects OpenBioMaps to a Nextcloud server. It
provides user-profile integration and issues JWT tokens for authentication.

Nextcloud URLs, credentials, signing secrets, token lifetimes, and TLS
validation must be configured securely through the mechanisms expected by the
installed release.

**Parameters:** None documented.

### `validation`

The `validation` module provides an internal API and administration interface
for data-validation algorithms.

Its functions include:

- managing validation rules;
- validating records; and
- logging validation actions.

Project-specific validation implementations may perform additional checks on
uploaded data.

**Parameters:** None documented. Additional rules are managed through the
module's administration interface and validation components.

### `download_restricted`

The `download_restricted` module introduces an administrator-controlled
download-authorisation workflow.

Instead of receiving immediate access to a download, users submit a request
describing the intended use of the data. Administrators can approve or reject
the request through the module administration interface.

The module provides:

- a download-request form;
- an administrator approval workflow; and
- integration with `results_buttons`.

When it is used with `results_buttons`, export options are made available only
to users whose request and permissions allow the download.

Enabling this module does not remove the need for server-side access checks.
Test direct export URLs and APIs to verify that download restrictions cannot
be bypassed.

**Parameters:** None. The module uses its dedicated administration interface.

### `extra_params`

The `extra_params` extension supplies additional input parameters to forms.

The exact syntax and availability of this extension must be checked against
the installed OpenBioMaps release because a standalone module with this name
may not be present in every version.

**Parameters:** No stable parameter format is documented here.

### `grid_view`

The `grid_view` module displays data using alternative polygon grids. Examples
include UTM grids, KEF grids, snapped points, and dynamically generated grid
polygons.

When a grid view is active, the geometry supplied by the module is used in
place of the record's original geometry for the relevant display.

The module implementation exposes methods including:

- `print_box()`;
- `default_grid_geom()`; and
- `get_grid_layer()`.

#### Parameters

```json
{
  "layer_options": [
    "kef_5 (layer_data_grid)",
    "original (layer_data_points)"
  ]
}
```

Each `layer_options` entry associates a geometry column with a MapServer
layer:

- the text before the parentheses is a column in `YOURTABLE_qgrids`; and
- the text inside the parentheses is the corresponding MapServer layer name.

In the example:

- `kef_5` is a geometry column in `YOURTABLE_qgrids`;
- `layer_data_grid` is the MapServer polygon layer used to display it;
- `original` stores the source geometry; and
- `layer_data_points` displays the original points.

A grid geometry requires a compatible MapServer layer. For example,
`layer_data_grid` must be a polygon layer if it displays polygon grids.

#### Grid table

The module creates `YOURTABLE_qgrids` if it does not already exist. The table
can then be extended with the geometry columns required by the project.

The module may also create an `update_grid_geoms` trigger and initial column
comments. These generated objects normally require project-specific review
and modification.

Set the user-facing names of grid options as column comments:

```sql
COMMENT ON COLUMN public.YOURTABLE_qgrids.original IS 'Original';
COMMENT ON COLUMN public.YOURTABLE_qgrids.kef_5 IS 'KEF 5×5';
```

Keep SQL identifiers consistent. For example, do not configure `kef_5` in the
module and create a column named `kef5`.

#### Trigger on the grid table

The following example invokes a project-specific grid-update function:

```sql
CREATE TRIGGER update_grid_geoms
BEFORE INSERT OR UPDATE ON public.YOURTABLE_qgrids
FOR EACH ROW
EXECUTE PROCEDURE public.update_qgrid_geoms_arg(
  '0.1',
  '0.1',
  't',
  't',
  't',
  't',
  '0.05'
);
```

> **Important:** The number and order of trigger arguments must exactly match
> the installed definition of `update_qgrid_geoms_arg()`. The historical
> example function below reads argument indexes up to `TG_ARGV[8]`, while the
> example trigger above supplies only seven arguments. Do not deploy these
> examples unchanged. Inspect the installed `grid_view.sql` and the database
> function, then provide every required argument.

#### Trigger on the source table

The source table requires a trigger to copy changes into the grid table:

```sql
CREATE TRIGGER qgrids
BEFORE INSERT OR DELETE OR UPDATE ON public.YOURTABLE
FOR EACH ROW
EXECUTE PROCEDURE insert_originalgeom_into_qgrids();
```

An example function body is:

```sql
BEGIN
  IF TG_OP = 'INSERT' THEN
    EXECUTE format(
      'INSERT INTO %I_qgrids (row_id, original) SELECT %L, %L::geometry',
      TG_TABLE_NAME,
      NEW.obm_id,
      NEW.obm_geometry
    );
    RETURN NEW;
  END IF;

  IF TG_OP = 'UPDATE' THEN
    EXECUTE format(
      'UPDATE %I_qgrids SET original = %L::geometry WHERE row_id = %L',
      TG_TABLE_NAME,
      NEW.obm_geometry,
      NEW.obm_id
    );
    RETURN NEW;
  END IF;

  IF TG_OP = 'DELETE' THEN
    EXECUTE format(
      'DELETE FROM %I_qgrids WHERE row_id = %L',
      TG_TABLE_NAME,
      OLD.obm_id
    );
    RETURN OLD;
  END IF;

  RETURN NULL;
END;
```

This is only the body of a trigger function, not a complete
`CREATE FUNCTION` statement.

#### Grid-update function

The following historical example demonstrates the intended operations:

```sql
DECLARE
  snap_x numeric := TG_ARGV[0];
  snap_y numeric := TG_ARGV[1];
  kef5 boolean := TG_ARGV[2];
  utm10 boolean := TG_ARGV[5];
  snap boolean := TG_ARGV[6];
  snap_polygon boolean := TG_ARGV[7];
  snap_polygon_size numeric := TG_ARGV[8];
BEGIN
  IF TG_OP = 'UPDATE' THEN
    IF kef5 THEN
      EXECUTE format(
        'SELECT geometry FROM shared."kef_5x5" WHERE ST_Within(%L::geometry, geometry)',
        NEW.original
      )
      INTO NEW.kef_5;
    END IF;

    IF snap THEN
      EXECUTE format(
        'SELECT ST_SnapToGrid(%L::geometry, %L, %L)',
        NEW.original,
        snap_x,
        snap_y
      )
      INTO NEW.snap;
    END IF;

    IF snap_polygon THEN
      EXECUTE format(
        'SELECT ST_Expand(ST_SnapToGrid(%L::geometry, %L, %L), %L)',
        NEW.original,
        snap_x,
        snap_y,
        snap_polygon_size
      )
      INTO NEW.snap_polygon;
    END IF;

    RETURN NEW;
  END IF;

  IF TG_OP = 'INSERT' THEN
    IF kef5 THEN
      EXECUTE format(
        'SELECT geometry FROM shared."kef_5x5" WHERE ST_Within(%L::geometry, geometry)',
        NEW.original
      )
      INTO NEW.kef_5;
    END IF;

    IF snap THEN
      EXECUTE format(
        'SELECT ST_SnapToGrid(%L::geometry, %L, %L)',
        NEW.original,
        snap_x,
        snap_y
      )
      INTO NEW.snap;
    END IF;

    IF snap_polygon THEN
      EXECUTE format(
        'SELECT ST_Expand(ST_SnapToGrid(%L::geometry, %L, %L), %L)',
        NEW.original,
        snap_x,
        snap_y,
        snap_polygon_size
      )
      INTO NEW.snap_polygon;
    END IF;

    RETURN NEW;
  END IF;

  RETURN NEW;
END;
```

This is also only a function body. The `utm10` variable is declared but is
not used by the shown implementation. Review and complete the function for
the project's required grid types.

#### Initial population

After the grid table and triggers are ready, existing source geometries can be
copied into an empty grid table:

```sql
INSERT INTO YOURTABLE_qgrids (row_id, original)
SELECT obm_id, obm_geometry
FROM YOURTABLE;
```

Example update for a snapped geometry:

```sql
UPDATE YOURTABLE_qgrids AS q
SET snap = source.snapped_geometry
FROM (
  SELECT
    obm_id,
    ST_SnapToGrid(obm_geometry, 0.13, 0.09) AS snapped_geometry
  FROM YOURTABLE
) AS source
WHERE q.row_id = source.obm_id;
```

Example update using polygons from a shared grid table:

```sql
UPDATE YOURTABLE_qgrids AS q
SET kef_5 = source.grid_geometry
FROM (
  SELECT
    data.obm_id,
    grid.obm_geometry AS grid_geometry
  FROM YOURTABLE AS data
  LEFT JOIN shared.kef_5x5 AS grid
    ON ST_Within(data.obm_geometry, grid.obm_geometry)
) AS source
WHERE q.row_id = source.obm_id;
```

In this example, `shared.kef_5x5` contains the predefined grid polygons.
Another geometry, such as `snap`, can be generated dynamically.

Run schema changes and bulk updates in a test environment first. Create a
database backup, verify spatial indexes, and check the behaviour for null,
invalid, boundary, and non-point geometries.

### `job_manager` validation jobs

The validation job manager configures background processes for a project.

On its administration page, administrators can configure:

- a simplified schedule containing minute, hour, and day values; and
- job-specific parameters in JSON format.

Adding a job registers it in the project's jobs table and can create template
files in the validation-module and jobs directories.

The availability and exact name of this component may depend on the installed
validation module. Background jobs run only if the project's `jobs.php`
runner is scheduled on the server.

**Parameters:** A list of background-job names.

#### `observation_lists`

The `observation_lists` job processes observation lists uploaded by the
mobile application.

Uploaded observations initially arrive in a temporary table. The job:

- populates `obm_observation_list_id`;
- calculates or copies the list start, end, and duration values; and
- copies complete lists into their target table.

Incomplete lists are skipped for later processing.

Job parameters:

- `list_start_column`: column storing the list start;
- `list_end_column`: column storing the list end;
- `list_duration_column`: column storing the duration;
- `only_time`: whether to store only the time instead of the full timestamp;
- `time_as_int`: whether to convert the time or duration to minutes.

Example:

```json
{
  "YOURTABLE": {
    "list_start_column": "time_of_start",
    "list_end_column": "time_of_end",
    "list_duration_column": "duration",
    "only_time": true,
    "time_as_int": true
  }
}
```

#### `incomplete_observation_lists`

The `incomplete_observation_lists` job handles lists that remain incomplete.

If the difference between the expected and received observations is within
the configured tolerance, the list can be processed by the next
`observation_lists` run and a system message is sent.

If the difference exceeds the tolerance, the job sends a system message but
leaves the list for manual processing.

Job parameters:

- `mail_to`: numeric role ID whose members receive the message;
- `diff_tolerance`: permitted difference before manual processing is required;
- `days_offset`: number of days to wait before processing the incomplete list.

Example:

```json
{
  "YOURTABLE": {
    "mail_to": 1265,
    "diff_tolerance": 2,
    "days_offset": 2
  }
}
```

Test notification recipients and job scheduling before relying on this
workflow in production.

### `join_tables`

The `join_tables` module displays related records on a data-sheet page.

The current documented implementation supports simple `LEFT JOIN` operations
with one equality condition per joined table.

**Parameters:**

```json
[
  {
    "table": "events",
    "join_on": [
      {
        "ref_field": "obm_id",
        "join_field": "patient_id"
      }
    ]
  },
  {
    "table": "measurements",
    "join_on": [
      {
        "ref_field": "obm_id",
        "join_field": "record_id"
      }
    ]
  }
]
```

For each joined table:

- `table` is the table to join;
- `ref_field` is the field in the current record; and
- `join_field` is the matching field in the joined table.

Use this module together with `additional_columns` where required. Ensure that
join fields are indexed and that users are authorised to access data from
every joined table.

### `list_manager`

The `list_manager` module manages reusable term lists for data uploads and
queries.

It provides:

- creation and editing of lists;
- association of lists with database tables and columns;
- generation of list contents from existing data;
- storage of list data in the database; and
- user feedback when a list operation fails.

The module uses a modal dialog for editing list values. Access to its
administrative functions should be limited to users who are permitted to
change upload and query vocabularies.

**Parameters:** None. The module uses its own user interface and
module-specific database objects.

### `massive_edit`

The `massive_edit` module allows authorised users to edit multiple selected
records from the map page through the file-upload interface.

Bulk changes can affect many records. Verify permissions, create a backup, and
test the edited file on a small selection before applying a large update.

**Parameters:** None.

### `move_project`

The `move_project` module moves a project to another OpenBioMaps server.

This is an experimental module. Before using it, create and verify backups and
check the compatibility of application versions, database extensions,
project files, users, modules, MapServer configuration, and secrets on the
destination server.

**Parameters:** None documented.

### `read_table`

The `read_table` module exposes a SQL table or view as a scrollable HTML table
through a unique link.

**Parameters:**

```json
[
  {
    "table": "schema.table_name",
    "label": "Displayed table name",
    "orderby": "column_name"
  }
]
```

Each entry contains:

- `table`: schema-qualified table or view name;
- `label`: user-facing label; and
- `orderby`: column used for the default ordering.

A unique or difficult-to-guess link is not sufficient access control. Verify
that the module enforces the intended project, group, and record-level
permissions.

### `results_asList`

The `results_asList` module displays query results as collapsible,
slide-like entries.

**Parameters:** None.

### `results_asGPX`

The `results_asGPX` module exports query results as a GPX file.

**Parameters:**

```json
{
  "name": "name_column",
  "description": [
    "description_column_1",
    "description_column_2"
  ]
}
```

The `name` column supplies the GPX feature name. Values from the
`description` columns are included in the feature description.

Only geometries compatible with the installed GPX exporter can be exported.

### `results_asCSV`

The `results_asCSV` module exports query results as a CSV file.

**Parameters:**

```json
{
  "sep": ",",
  "quote": "\""
}
```

- `sep` defines the field separator.
- `quote` defines the field-enclosure character.

Choose settings compatible with the software used to open the export. The
export must still enforce all applicable row- and column-level access rules.

### `results_asJSON`

The `results_asJSON` module exports query results as JSON.

**Parameters:** None.

### `results_asTable`

The `results_asTable` module displays query results as a full-screen HTML
table containing all available fields.

It provides:

- full record display;
- sortable columns; and
- links for viewing or editing records when the user has the required
  permissions.

Displaying every available field can be expensive for large result sets and
may expose fields that should be restricted. Configure access-control modules
and test the output for each user group.

**Parameters:** None.

### `results_asKML`

The `results_asKML` module exports query results as a KML file.

**Parameters:**

```json
{
  "name": "name_column",
  "description": [
    "description_column_1",
    "description_column_2"
  ]
}
```

The `name` column supplies the KML feature name. Values from the
`description` columns are included in the feature description.

### `results_buttons`

The `results_buttons` module adds controls for downloading, saving, sharing,
and bookmarking query results on the map page.

Available download formats depend on the corresponding enabled export
modules. These may include CSV, GPX, KML, SHP, and JSON.

The module can provide:

- download buttons;
- saved queries and results;
- saved spatial selections;
- bookmarks;
- sharing with users or other OpenBioMaps projects; and
- integration with `download_restricted`.

Example configuration:

```json
{
  "bookmarks": "off",
  "sharing": "off",
  "server_share": "on"
}
```

Configuration keys:

- `bookmarks` enables or disables query bookmarks;
- `sharing` enables or disables general sharing; and
- `server_share` enables or disables sharing with another server or project.

The documented defaults enable bookmarks and disable sharing and server
sharing. Download buttons appear when their corresponding export modules are
enabled.

When `download_restricted` is active, download availability also depends on
the request and approval workflow.

### `results_asStable`

The `results_asStable` module displays a compact, sortable result table on the
map page.

Unlike a full result table, it displays only the configured columns. It can
also include links to view or edit records when the user has the required
permissions.

**Parameters:**

```json
[
  "column_name_1",
  "column_name_2"
]
```

The module name uses the historical spelling `results_asStable`; do not rename
it in the configuration.

### `results_specieslist`

The `results_specieslist` module summarises the species present in the current
query result.

It can display:

- species names;
- the number of records for each species;
- the number of recorded individuals; and
- alphabetical or taxonomic sorting options.

The columns used for species names and individual counts depend on the
project's schema and module implementation.

**Parameters:** None documented.

### `results_summary`

The `results_summary` module displays the total number of distinct records
returned by the current query.

It integrates with access rules so that restricted records are counted only
when the user is permitted to access them.

A summary count can itself disclose sensitive information. Test the module
with restricted records and each relevant access level.

**Parameters:** None.

### `results_table`

The `results_table` extension creates a full HTML table from query results.

Depending on the OpenBioMaps release, this functionality may be provided by a
module with another implementation name, such as `results_asTable` or
`results_asHtmlTable`. Use the exact module name shown by the installed module
administration page.

**Parameters:** None documented.

### `restricted_data`

The `restricted_data` module applies rule-based restrictions to project data.

The project must have correctly configured access rules and related database
objects. Test restrictions through the map page, data-sheet page, exports,
APIs, and direct module links.

**Parameters:** None.

### `spa_integration`

The `spa_integration` module integrates a single-page application with an
OpenBioMaps project.

It requires module-specific administration settings. Routing,
authentication, authorisation, static-resource paths, and direct browser
navigation must be tested after configuration.

**Parameters:** Managed through the module administration interface.

### `text_filter`

The `text_filter` module adds text filters to the map page and the query API.
It constructs the filtering portion of the SQL query from configured columns
and filter operators.

Example:

```json
[
  "common_name",
  "obm_taxon",
  "notes::colour_rings",
  "obm_datum",
  "obm_uploading_date",
  "obm_uploader_user",
  "data.abundance:nested(data.count):autocomplete",
  "data.count:values():",
  "obm_files_id",
  "species::autocomplete"
]
```

Entries can contain a column reference followed by module-specific modifiers,
such as:

- `autocomplete`;
- `values()`;
- `nested(...)`; or
- a label or secondary field separated with `::`.

The syntax is compact and version-dependent. Copy known working expressions
carefully, use only trusted database identifiers, and test every filter
through both the map page and query API.

### `text_filter2`

The `text_filter2` module provides advanced taxonomic and general text
filters. Like `text_filter`, it contributes conditions to the SQL query.

**Parameters:**

```json
{}
```

Further settings may be managed through the module's user interface or
project-specific configuration.

### `transform_data`

The `transform_data` module transforms record values before they are displayed
in result areas or included in supported exports.

Available transformations include:

- `geom`: creates a clickable geometry link that opens the location on the
  map;
- `geom_nolink`: displays simplified WKT without a link;
- `geom_wkt`: displays the normal WKT representation;
- `date_yearonly`: extracts the year from a date;
- `translate`: translates predefined text constants into user-facing text;
- `obslistlink`: creates a link from an observation-list identifier; and
- `uplid`: applies the upload-identifier transformation supported by the
  module.

Example:

```json
{
  "obm_geometry": "geom",
  "other_geometry": "geom_nolink",
  "obm_uploading_id": "uplid",
  "date_time_field": "date_yearonly",
  "method": "translate",
  "obm_observation_list_id": "obslistlink"
}
```

Each key is a database column and each value is the transformation applied to
that column.

Transformations affect presentation, not the underlying stored value. Verify
that transformed links and values do not reveal restricted data.

## Modules requiring additional documentation

The current OpenBioMaps repository contains modules that are not yet described
in detail on this page. Depending on the installed version, these may include:

- `custom_data_check`;
- `ebp`;
- `fill_stable_with_column`;
- `ioc_bird_list`;
- `natura2000`;
- `results_asHtmlTable`;
- `results_asPDF`;
- `results_asSHP`;
- `service_envimap`;
- `snap_to_grid`; and
- `turnstile`.

Do not infer a module's behaviour or parameter format solely from its file
name. Review its source, module metadata, SQL installation file, access
checks, and administration interface before enabling it.

## Deployment checklist

Before enabling a module in production:

1. Confirm that the module is included in the installed OpenBioMaps version.
2. Validate its JSON parameters.
3. Identify any required modules, database objects, MapServer layers, jobs,
   external services, or PHP extensions.
4. Review module access and group access.
5. Test with public, authenticated, group-member, and administrator accounts.
6. Test direct URLs, exports, and APIs for access-control bypasses.
7. Check application, PHP, PostgreSQL, and background-job logs.
8. Back up the project before enabling modules that alter database objects or
   perform bulk updates.
9. Document the configuration and the procedure for disabling or rolling back
   the module.
10. Repeat the tests after an OpenBioMaps upgrade.
