# Protocol package format, version 1

This document defines the first protocol package contract for the protocol
installer. The package is declarative YAML: it describes project tables,
columns, lists, and forms. It does not contain executable code or SQL.

The [field observations example](https://gitlab.com/openbiomaps/share-your-protocol/-/blob/main/minimal/protocol.yml)
and [PDS package](https://gitlab.com/openbiomaps/share-your-protocol/-/blob/main/pds-mobile-test/protocol.yml) are publishable
packages in the protocol repository. The installer reads packages with this
format from the configured GitLab catalogue.

## Package files and versioning

A GitLab catalogue is a `catalog.yml` file at a configured repository path. Each
catalogue entry identifies a protocol and points to its package YAML by a
repository-relative path. A package declares:

- `format_version`: the integer version of this file contract;
- `protocol_id`: a stable reverse-DNS identifier that remains the same across
  releases, such as `org.openbiomaps.pds-mobile-test`;
- `protocol_version`: the release of the protocol, independent of the format.

The catalogue repeats the protocol ID and version so clients can list packages
without loading every package. The package values must match the catalogue entry.
The repository commit identifies the exact published catalogue and package
content; a package path must remain inside the repository.

The initial contract uses format version `1`. A reader must reject an unsupported
format version and unknown properties rather than silently ignoring settings.
Protocol versions are independent of the format version. The installer supports
additive upgrades; changes to existing definitions require manual review.

The installer reads a public GitLab project configured in the server's
`/etc/openbiomaps/system_vars.php.inc` file. Define
`PROTOCOL_INSTALLER_GITLAB_PROJECT` as the GitLab project path (`group/project`).
The optional `PROTOCOL_INSTALLER_GITLAB_REF` constant selects a branch
(default `main`), and `PROTOCOL_INSTALLER_GITLAB_CATALOGUE_PATH` selects the
repository-relative catalogue file (default `catalog.yml`). This first version
does not use a token or support private repositories.

```php
define('PROTOCOL_INSTALLER_GITLAB_PROJECT', 'openbiomaps/share-your-protocol');
define('PROTOCOL_INSTALLER_GITLAB_REF', 'main');
define('PROTOCOL_INSTALLER_GITLAB_CATALOGUE_PATH', 'catalog.yml');
```

## Identifiers and names

Tables, columns, forms, and lists have stable package-local IDs. References use
these IDs, never suggested database names. IDs use lowercase letters, digits,
and underscores, begin with a letter, and are unique within their respective
kind. `suggested_name` is a human-readable local name for newly created objects;
it is a hint and can be changed or mapped to a compatible existing object.
Packages must not specify a database, schema, project table name, or database
owner.

Every table declares a `target`:

- `project_main` means the project's existing main table, which may be extended;
- `create` means a new data table that the administrator can map to a compatible
  existing table or create.

The format does not let a package declare an arbitrary physical destination.
System-managed OBM columns and table infrastructure are provided by the
installer and must not be repeated as protocol columns. Forms may refer to the
reserved column IDs `system.geometry` and `system.files` for the standard
geometry and attachment fields. These IDs are not package-defined columns and
cannot be renamed in a package.

## Tables and columns

Each column has a stable `id`, a `suggested_name`, a portable `data_type`, and
optional `description` and `required` metadata. Version 1 data types are:
`text`, `varchar`, `integer`, `decimal`, `boolean`, `date`, `time`, `datetime`, `interval`,
and `text_array`. Types describe stored values, not form widgets. Geometry and
attachments use the reserved system columns described above. There is no raw SQL
type escape hatch.

`varchar` requires a positive integer `max_length` and creates a
`varchar(max_length)` column. For example:

```yaml
- id: species
  suggested_name: species
  data_type: varchar
  max_length: 255
```

A `varchar(n)` package column can reuse `varchar(m)` when `m >= n`, or an
unbounded `varchar` or `text` column. An unbounded package `text` column cannot
reuse bounded `varchar(n)`: the destination might reject future values longer
than `n`. To reuse an existing bounded species column, publish a protocol
version that declares `varchar` and an appropriate `max_length`.

Column names are suggestions, not identity. The installer compares selected
existing columns by compatible type and capacity. It must not implicitly convert
data or alter existing column definitions.

## Lists

Every list has a stable `id` and one of these `kind` values:

- `fixed`: package-owned ordered `{code, label}` values. A form stores `code`;
  `label` is display text. `multiselect` is optional and defaults to false.
- `project`: a project-specific list slot. The administrator supplies or selects
  the local source during installation; the package can provide a prompt, but
  cannot require a particular local list.
- `table`: a list read from another package table. `table`, `value_column`, and
  `label_column` are stable logical references to package IDs, not SQL names.

A table list may include `filter_column` and `filter_value`, which must reference
a declared column and a scalar value. This supports filtered choices without
embedding SQL. A form field refers to a list by its stable ID. Lists preserve
codes and labels when the administrator chooses an equivalent local source.

## Forms and fields

Each form declares a stable `id`, a `suggested_name`, a `mode` (`web` or `api`),
a destination table ID, optional description, settings, and ordered fields.
Version 1 settings are `observationlist_mode` (`false`, `true`, or `force`),
`observationlist_time` (non-negative integer minutes), and `tracklog_mode`
(`false`, `force`, or empty string). Omitted settings use the application default.

Each field references a declared column ID or a reserved system column ID and
declares a UI `type`. Version 1
UI types are `text`, `textarea`, `numeric`, `boolean`, `date`, `time`,
`datetime`, `timetominutes`, `tinterval`, `array`, `list`, `autocomplete`,
`autocompletelist`, `point`, `line`, `polygon`, `wkt`, and `file_id`. Optional
properties are `required` (boolean), `default` (scalar or null), `api_params`
(a list of supported application parameter strings), and `list` (a list ID).
The `list` property is required for `list`, `autocomplete`, and
`autocompletelist`; it is invalid for other field types. Defaults are literal
values, except for the currently supported application-resolved defaults
`_email`, `_login_name`, and `_login_email`. Other magic values require explicit
installer support before packages can use them.

Version 1 field and storage type compatibility is:

| Form field type | Compatible column |
| --- | --- |
| `text`, `textarea`, `list`, `autocomplete`, `autocompletelist` | `text` or `varchar` |
| `numeric` | `integer` or `decimal` |
| `boolean` | `boolean` |
| `date` | `date` |
| `time` | `time` |
| `datetime` | `datetime` |
| `timetominutes` | `integer` |
| `tinterval` | `interval` |
| `array` | `text_array` |
| `point`, `line`, `polygon`, `wkt` | `system.geometry` |
| `file_id` | `system.files` |

The parser must reject duplicate IDs, unknown properties and enum values,
undeclared references, incompatible field/column combinations, invalid list
sources, and invalid form settings. Validation must happen before any database
write. Cross-reference and compatibility checks are semantic checks in addition
to YAML/schema parsing.

## Catalogue shape

The catalogue has `catalogue_format_version: 1` and a `protocols` list. Every
entry contains `protocol_id`, `protocol_version`, `title`, `description`, and
`package`. `package` is a repository-relative path to the package YAML file.
Entries are unique by `(protocol_id, protocol_version)`.

See the [published catalogue](https://gitlab.com/openbiomaps/share-your-protocol/-/blob/main/catalog.yml)
and :ref:`the package author and administrator guide <protocol-installer-guide>`.
