# OpenBioMaps Documentation Translation Conventions

## Purpose

Translate the OpenBioMaps documentation from English to Hungarian.

The English documentation is the source of truth.
The Hungarian documentation must preserve the structure and technical meaning
of the English documentation.

## General translation rules

- Translate human-readable English text into natural, precise Hungarian.
- Do not translate literally when that would produce unnatural Hungarian.
- Preserve the technical meaning exactly.
- Do not add information that is not present in the English source.
- Do not remove information from the English source.
- Do not summarize or simplify the source text.
- Keep terminology consistent throughout the documentation.
- Use established Hungarian technical terminology where appropriate.
- When there is no well-established Hungarian equivalent, retain the English
  technical term rather than inventing an unnatural translation.

## Sphinx RST

Preserve all Sphinx syntax.

Never modify:

- directive names
- role names
- labels
- reference targets
- document targets
- anchors
- substitution names
- option names

For example, preserve:

    :ref:`translations`

    :doc:`Administrative settings <../admin_settings#database-columns>`

The visible text of a reference may be translated, but its target must not
be changed.

For example:

    :doc:`Adminisztrációs beállítások <../admin_settings#database-columns>`

is allowed.

But this is NOT allowed:

    :doc:`Adminisztrációs beállítások <../admin_beallitasok#database-columns>`

## RST directives

Do not translate directive names.

Examples:

    .. note::
    .. warning::
    .. important::
    .. code-block::
    .. image::
    .. figure::
    .. list-table::
    .. csv-table::

The content of a directive should be translated when it is human-readable.

Directive options must not be translated.

For example:

    .. code-block:: javascript
       :linenos:

must remain structurally unchanged.

## RST labels

Never translate or modify labels.

For example:

    .. _translations:

must remain exactly:

    .. _translations:

even if the surrounding text is translated.

## Markdown

Preserve Markdown syntax.

Do not modify:

- heading levels
- links
- URLs
- image paths
- anchors
- HTML tags
- code fences
- table structure

Translate only the human-readable content.

## Links

Preserve all URLs exactly.

For example:

    https://openbiomaps.org

must never be translated or modified.

For links, translate the visible link text but preserve the target.

## Code

Never translate code.

This includes:

- SQL
- PostgreSQL
- PostGIS
- JavaScript
- PHP
- Python
- shell commands
- CSS
- JSON
- YAML
- configuration files
- regular expressions

Do not modify code merely to make comments or variable names Hungarian.

Code examples must remain executable.

## File paths and identifiers

Never translate or modify:

- file names
- directory names
- database names
- schema names
- table names
- column names
- variable names
- function names
- class names
- API endpoints
- configuration keys
- command names

Examples:

    project_forms
    system.uploadings
    shared.n2000_sites
    createGroupSelector()
    PostgreSQL
    PostGIS

must remain unchanged.

## OpenBioMaps terminology

Use the following terminology consistently.

OpenBioMaps
- Always: OpenBioMaps
- Do not translate the product name.

project
- Use: projekt

database
- Use: adatbázis

table
- Use: tábla

field
- Use: mező
- In database-specific contexts, "mező" is preferred over "oszlop" unless
  the source explicitly refers to a database column.

column
- Use: oszlop

record
- Use: rekord

observation
- Use: megfigyelés

event
- Use: esemény

sampling event
- Use: mintavételi esemény

taxon
- Use: taxon

species
- Use: faj

individual
- Use: egyed

data management
- Use: adatkezelés

data collection
- Use: adatgyűjtés

data entry
- Use: adatrögzítés

data upload
- Use: adatfeltöltés

form
- Use: űrlap

upload form
- Use: feltöltési űrlap

user
- Use: felhasználó

user group
- Use: felhasználói csoport

access rights
- Use: hozzáférési jogosultságok

permission
- Use: jogosultság

administrator
- Use: adminisztrátor

administrative settings
- Use: adminisztrációs beállítások

project administrator
- Use: projektadminisztrátor

map
- Use: térkép

layer
- Use: réteg

spatial data
- Use: térbeli adatok

geometry
- Use: geometria

coordinate system
- Use: koordináta-rendszer

attribute
- Use: attribútum

query
- Use: lekérdezés

filter
- Use: szűrő

field type
- Use: mezőtípus

metadata
- Use: metaadat

translation
- Use: fordítás

documentation
- Use: dokumentáció

## Technical terminology

Prefer internationally established technical terms when appropriate.

Do not translate names of technologies, software, standards, protocols,
programming languages, or database systems unless there is a standard
Hungarian name.

Examples:

PostgreSQL
PostGIS
JavaScript
PHP
Python
SQL
REST API
API
JSON
GeoJSON
WMS
WFS
Sphinx
Git
GitLab
Docker
GBIF

must remain unchanged.

## Capitalization

Follow normal Hungarian capitalization rules.

Do not mechanically preserve English title capitalization.

English:

    Data Management

Hungarian:

    Adatkezelés

not:

    AdatKezelés

## Headings

Translate headings while preserving their RST or Markdown level.

For example:

    Data management
    ***************

becomes:

    Adatkezelés
    ***********

Do not change the heading hierarchy.

## Tables

Preserve table structure exactly.

Translate:

- column headings
- cell text

Do not modify:

- separators
- alignment markers
- directives
- links
- code
- identifiers

Pay particular attention to Markdown tables because changing the number or
position of separators can make the table invalid.

## Inline markup

Preserve inline markup.

For example:

    **important**

may become:

    **fontos**

and:

    `project_forms`

must remain:

    `project_forms`

Do not remove or relocate markup unnecessarily.

## UI terminology

When the source refers to a button, menu item, field, checkbox, or other
interface element, translate the descriptive text naturally.

If the exact English UI label is important for identifying an interface
element, retain the English label in parentheses when useful.

Example:

    Click the **Save** button.

may become:

    Kattintson a **Save** gombra.

if "Save" is the actual English interface label.

Do not invent a Hungarian UI label unless the OpenBioMaps interface itself
uses that Hungarian label.

## Names

Do not translate:

- personal names
- organization names
- project names
- software names
- database names
- scientific names

Scientific taxon names should remain unchanged and italicization should be
preserved where present.

## Numbers and units

Do not change numerical values.

Preserve units unless there is a clear localization requirement.

Do not change decimal values, coordinate values, EPSG codes, version numbers,
or dates merely because the surrounding text is translated.

## Cross-reference integrity

The Hungarian documentation must preserve all cross-reference targets from
the English documentation.

Never rename a target merely because the visible text has been translated.

Before considering a translated file complete, check for:

- :ref:
- :doc:
- :download:
- labels
- internal anchors
- relative paths

## Translation quality

The Hungarian text should read as professional technical documentation.

Prefer:

    Az esemény akkor is létrejön, ha a mintavétel során nem találtak
    egyetlen egyedet sem.

over:

    Az esemény még mindig létezik, ha a protokoll szerint semmit nem találtak.

Avoid machine-translation artifacts such as:

- unnecessary anglicisms
- unnatural word order
- excessive passive constructions
- inconsistent terminology
- English sentence structure copied into Hungarian

## Consistency

If the same English term occurs repeatedly with the same meaning, use the same
Hungarian translation throughout the documentation.

Do not introduce synonyms merely to make the text stylistically varied.

Technical documentation benefits from terminological consistency.

## What must never be changed

The following must remain unchanged unless the change is required to fix an
existing error:

- code
- URLs
- file paths
- database identifiers
- schema names
- table names
- column names
- function names
- variable names
- API endpoints
- Sphinx labels
- Sphinx targets
- directive names
- directive options
- Markdown syntax
- RST syntax
- image paths
- downloadable file names
- version numbers
- EPSG codes

## Output requirements

The translated file must remain valid Sphinx RST or Markdown.

Do not add translator comments.

Do not add explanations outside the translated document.

Do not create a translation summary.

Do not modify the English source file.

The Hungarian translation must be written to the corresponding file in the
Hungarian documentation tree.

Example:

    en/data_management.rst
    hu/data_management.rst

The file name must remain identical unless explicitly instructed otherwise.
