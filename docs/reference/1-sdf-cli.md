---
sidebar_position: 1
---

# Command-Line Help for `sdf`

This document contains the help content for the `sdf` command-line program.

**Command Overview:**

* [`sdf`↴](#sdf)
* [`sdf configure`↴](#sdf-configure)
* [`sdf new`↴](#sdf-new)
* [`sdf clean`↴](#sdf-clean)
* [`sdf build`↴](#sdf-build)
* [`sdf describe`↴](#sdf-describe)
* [`sdf deploy`↴](#sdf-deploy)
* [`sdf view`↴](#sdf-view)
* [`sdf trace`↴](#sdf-trace)
* [`sdf system`↴](#sdf-system)
* [`sdf auth`↴](#sdf-auth)
* [`sdf auth login`↴](#sdf-auth-login)
* [`sdf auth status`↴](#sdf-auth-status)

## `sdf`

SDF's modular SQL

**Usage:** `sdf COMMAND`

###### **Subcommands:**

* `configure` — Initialize your SDF environment
* `new` — Create a new SDF workspace at PATH
* `clean` — Remove generated SDF artifacts in workspace
* `build` — Build, run, and save SDF queries
* `describe` — Describe SDF table schemas
* `deploy` — Create a deployment and post it to the SDF service
* `view` — View existing table content
* `trace` — Display lineage for a given column
* `system` — System maintenance and generation of reference documentation
* `auth` — Manage credentials and tokens



## `sdf configure`

Initialize your SDF environment

**Usage:** `sdf configure --client-secret CLIENT_SECRET --client-id <CLIENT_ID>`

###### **Options:**

* `--client-secret CLIENT_SECRET` — Authenticate requests to the SDF service with secret key, i.e., your programmatic password
* `--client-id CLIENT_ID` — Authenticate requests to the SDF service with your client id, i.e., your programmatic user-name



## `sdf new`

Create a new SDF workspace at PATH

**Usage:** `sdf new [OPTIONS] [PATH]`

###### **Arguments:**

* `PATH` — Create a new SDF workspace at PATH

###### **Options:**

* `--list-samples` — List all available samples

  Default value: `false`
* `--sample SAMPLE` — Create a workspace with the sample content at path
* `--quiet` — Do not print sdf log messages

  Default value: `false`



## `sdf clean`

Remove generated SDF artifacts in workspace

**Usage:** `sdf clean [OPTIONS] [INPUT_FILES]...`

###### **Arguments:**

* `INPUT_FILES` — Remove all derived artifacts from a workspace, where workspace is identified by any input location or, if none is given, by the current working directory

###### **Options:**

* `--quiet` — Do not print sdf log messages

  Default value: `false`
* `--config CONFIG` — Build data using [config].workspace.sdf.yml

  Default value: ``
* `--cache CACHE` — Store derived SDF artifacts in a directory named .sdfcache in the root of your project

  Default value: `.sdfcache`



## `sdf build`

Build, run, and save SDF queries

**Usage:** `sdf build [OPTIONS] [INPUT_FILES]...`

###### **Arguments:**

* `INPUT_FILES` — Build these *.sql files or catalog.schema.table targets; no input rebuilds the whole workspace

###### **Options:**

* `--var VAR` — Var bindings of the form: n=1 or year="2022 01 01", only string variables supported
* `--date DATE` — Run all tasks that run on this datetime, [ENV] use prefixes of RFC format, e.g. 2020-12-31T21:07, or 2020-12-31, etc
* `--from FROM` — Backfill from this datetime (inclusive), use prefixes of RFC format, e.g. 2020-12-31T21:07, or 2020-12-31, etc
* `--to TO` — Backfill to this datetime (exclusive), use prefixes of RFC format, e.g. 2020-12-31T21:07, or 2020-12-31, etc (default is now)
* `--remote-location REMOTE_LOCATION` — Write tables to "s3://[BUCKET]", defaults to workspace's remote-location
* `-c`, `--config CONFIG` — Build data using [config].workspace.sdf.yml
* `--cache CACHE` — Store derived SDF artifacts in a directory named .sdfcache in the root of your project

  Default value: `.sdfcache`
* `--dry-run` — Plan but don't execute refills,  output as a shell script in .sdfcache/commands.sh

  Default value: `false`
* `--file-format FILE_FORMAT` — Save tables in this format

  Default value: `parquet`

  Possible values: `parquet`, `csv`, `json`

* `--print-format PRINT_FORMAT` — Show tables in this format

  Default value: `table`

  Possible values: `table`, `csv`, `tsv`, `json`, `nd-json`

* `--no-save` — Don't save non-source tables

  Default value: `false`
* `--no-cache` — Don't cache tables

  Default value: `false`
* `--no-workflow` — Don't run a workflow, just the query

  Default value: `false`
* `--limit LIMIT` — "Limiting number of shown rows. Run with --limit 0 to remove limit.",

  Default value: `10`
* `--no-show` — Don't show the result of queries

  Default value: `false`
* `--quiet` — Do not print sdf log messages

  Default value: `false`
* `--log LOG` — Set log level (by setting env var RUST_LOG)

  Default value: `none`

  Possible values:
  - `trace`:
    Trace internal state changes
  - `debug`:
    Trace internal key metrics, including cache hit, etc
  - `info`:
    Trace internal progress, SQL statements being processed, logical plan being produced
  - `none`:
    No trace, unless RUST_LOG is set

* `--no-summary` — Do not generate a all.sdf.yml file

  Default value: `false`



## `sdf describe`

Describe SDF table schemas

**Usage:** `sdf describe [OPTIONS] [INPUT_FILES]...`

###### **Arguments:**

* `INPUT_FILES` — Describe these *.sql files, or catalog.schema.table targets; no input describes the whole workspace

###### **Options:**

* `--no-propagate` — Propagate labels

  Default value: `false`
* `--region REGION` — The AWS region (default=us-east-1))
* `-c`, `--config CONFIG` — Describe data using [config].workspace.sdf.yml
* `--cache CACHE` — Store derived SDF artifacts in a directory named .sdfcache in the root of your project

  Default value: `.sdfcache`
* `--no-save` — Don't save schema tables

  Default value: `false`
* `--print-format PRINT_FORMAT` — Show tables in this format

  Default value: `table`

  Possible values: `table`, `yml`, `json`

* `--file-format FILE_FORMAT` — Save tables in this format

  Default value: `json`

  Possible values: `table`, `yml`, `json`

* `--no-show` — Don't show the result of queries

  Default value: `false`
* `--quiet` — Do not print sdf log messages

  Default value: `false`
* `--log LOG` — Set log level (by setting env var RUST_LOG)

  Default value: `none`

  Possible values:
  - `trace`:
    Trace internal state changes
  - `debug`:
    Trace internal key metrics, including cache hit, etc
  - `info`:
    Trace internal progress, SQL statements being processed, logical plan being produced
  - `none`:
    No trace, unless RUST_LOG is set

* `--no-summary` — Do not generate a all.sdf.yml file

  Default value: `false`



## `sdf deploy`

Create a deployment and post it to the SDF service

**Usage:** `sdf deploy [OPTIONS] [INPUT_FILES]...`

###### **Arguments:**

* `INPUT_FILES` — Deploy these  *.sql files or catalog.schema.table targets; no input deploys the whole workspace

###### **Options:**

* `--var VAR` — Var bindings of the form: n=1 or year="2022 01 01", only string variables supported
* `--propagate` — Propagate labels for deployed targets

  Default value: `false`
* `--date DATE` — Backfill all tasks that run (only) on this datetime, [ENV] use prefixes of RFC format, e.g. 2020-12-31T21:07, or 2020-12-31, etc
* `--from FROM` — Backfill from this datetime (inclusive), use prefixes of RFC format, e.g. 2020-12-31T21:07 or 2020-12-31
* `--to TO` — Backfill to this datetime (exclusive), use RFC format, e.g., e.g. 2020-12-31T21:07:14-07:00, with optional T part
* `--remote-location REMOTE_LOCATION` — Read tables from "s3://[BUCKET]", defaults to use workspace's remote-location
* `-c`, `--config CONFIG` — Deploy environment using [config].workspace.sdf.yml (uses just workspace if [config].workspace.sdf.yml does not exist)
* `--cache CACHE` — Store derived SDF artifacts in a directory named .sdfcache in the root of your project

  Default value: `.sdfcache`
* `--execute EXECUTE` — When to execute this job run; defaults to recurring: if --from/--to are given

  Default value: `once-immediately`

  Possible values: `once-immediately`, `once-on-last-landed`, `once-on-next-landing`, `recurring`

* `--dry-run` — Create a deploy.json and archive.tar.gz but don't post it to the service

  Default value: `false`
* `--quiet` — Do not print sdf log messages

  Default value: `false`
* `--log LOG` — Set log level (by setting env var RUST_LOG)

  Default value: `none`

  Possible values:
  - `trace`:
    Trace internal state changes
  - `debug`:
    Trace internal key metrics, including cache hit, etc
  - `info`:
    Trace internal progress, SQL statements being processed, logical plan being produced
  - `none`:
    No trace, unless RUST_LOG is set




## `sdf view`

View existing table content

**Usage:** `sdf view [OPTIONS] INPUT_FILE`

###### **Arguments:**

* `INPUT_FILE` — Input is catalog.schema.table target, or a .json, .csv, or .parquet file, or a directory ending in '/' containing parquet files

###### **Options:**

* `--date DATE` — View catalog.schema.table of this datetime, [ENV] use prefixes of RFC format, e.g. 2020-12-31T21:07, or 2020-12-31 with default T00:00, etc
* `--from FROM` — View catalog.schema.table from this datetime (inclusive), use prefixes of RFC format, e.g. 2020-12-31T21:07, or 2020-12-31 with default T00:00
* `--to TO` — View catalog.schema.table to this datetime (exclusive), use prefixes of RFC format, e.g. 2020-12-31T21:07, or 2020-12-31 with default T23:59
* `--remote-location REMOTE_LOCATION` — View catalog.schema.table from "s3://[BUCKET]" location
* `-c`, `--config CONFIG` — Build data using [config].workspace.sdf.yml
* `--cache CACHE` — Store derived SDF artifacts in a directory named .sdfcache in the root of your project

  Default value: `.sdfcache`
* `--limit LIMIT` — "Limiting number of shown rows. Run with --limit 0 to remove limit.",

  Default value: `10`
* `--print-format PRINT_FORMAT` — Show tables in this format

  Default value: `table`

  Possible values: `table`, `csv`, `tsv`, `json`, `nd-json`

* `--file-format FILE_FORMAT` — Read tables having this format

  Default value: `parquet`

  Possible values: `parquet`, `csv`, `json`

* `--no-header` — Assumes that .csv files have a header, use --no-header if they have none

  Default value: `false`
* `--quiet` — Do not print sdf log messages

  Default value: `false`
* `--log LOG` — Set log level (by setting env var RUST_LOG)

  Default value: `none`

  Possible values:
  - `trace`:
    Trace internal state changes
  - `debug`:
    Trace internal key metrics, including cache hit, etc
  - `info`:
    Trace internal progress, SQL statements being processed, logical plan being produced
  - `none`:
    No trace, unless RUST_LOG is set




## `sdf trace`

Display lineage for a given column

**Usage:** `sdf trace [OPTIONS] INPUT_FILE`

###### **Arguments:**

* `INPUT_FILE` — The specification of the table for whose columns to compute lineage

###### **Options:**

* `--column COLUMN` — The column for which to compute lineage
* `--forward` — Whether to compute downstream lineage. (The default is upstream)

  Default value: `false`
* `--collapse` — Whether to collapse the output into a single level of dependencies. (Only relevant for forward=false)

  Default value: `false`



## `sdf system`

System maintenance and generation of reference documentation

**Usage:** `sdf system [OPTIONS]`

###### **Options:**

* `--show SHOW` — Print reference documents on stdout

  Possible values:
  - `cli-markdown`:
    Print cli commands and options in markdown format
  - `sdf-json-schema`:
    Print json schema for *.sdf.yml documents
  - `deploy-json-schema`:
    Print json schema for deploy.json documents

* `--update` — Update SDF in place to the latest version

  Default value: `false`
* `--uninstall` — Uninstall SDF from the system

  Default value: `false`
* `--quiet` — Do not print sdf log messages

  Default value: `false`



## `sdf auth`

Manage credentials and tokens

**Usage:** `sdf auth COMMAND`

###### **Subcommands:**

* `login` — Obtain credentials for accessing remote resources
* `status` — Show status of credentials / tokens



## `sdf auth login`

Obtain credentials for accessing remote resources

**Usage:** `sdf auth login [OPTIONS]`

###### **Options:**

* `--id-token ID_TOKEN` — Path to a file containing an OIDC identity token (a JWT)



## `sdf auth status`

Show status of credentials / tokens

**Usage:** `sdf auth status`



   Finished system in 0.000 secs


