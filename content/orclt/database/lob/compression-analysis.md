---
title: "LOB Compression Analysis"
description: "Estimate the compression ratio achievable on LOB segments before committing to SecureFile migration."
weight: 20
---

# LOB Compression Analysis

`orclT database lob compression-analysis` estimates the compression ratio that Oracle SecureFile LOB compression would achieve on a given LOB segment. The analysis uses `DBMS_COMPRESSION` to sample rows and calculate a ratio without altering the data.

## Usage

Analyse a specific table's LOB columns:

```bash
orclT database lob compression-analysis \
  -u <user> -p <password> -d <host>:<port>/<service> \
  --schema <SCHEMA> \
  --table <TABLE> \
  --compression-type COMP_LOB_HIGH
```

Analyse all non-Oracle-maintained schemas:

```bash
orclT database lob compression-analysis \
  -u <user> -p <password> -d <host>:<port>/<service> \
  --all-non-oracle-maintained \
  --report-file lob_compression.xlsx
```

## Flags

| Flag | Short | Description |
|------|-------|-------------|
| `--schema` | `-s` | Target schema name |
| `--table` | `-t` | Target table name |
| `--column` | `-c` | Specific LOB column name |
| `--partition` | `-n` | Restrict to a single partition |
| `--lob` | `-l` | LOB segment name |
| `--table-as-whole` | `-w` | Ignore partition filter, scan the entire table |
| `--all-non-oracle-maintained` | `-a` | Include all non-Oracle-maintained schemas |
| `--parallel` | `-P` | Degree of parallelism (default 1) |
| `--report-file` | `-r` | Output Excel filename |
| `--size-in-bytes` | `-b` | Display sizes in bytes instead of human-readable units |
| `--compression-type` | | SecureFile compression level: `COMP_LOB_HIGH`, `COMP_LOB_MEDIUM`, or `COMP_LOB_LOW` |
| `--subset-rows` | | Row sampling level for ratio estimation |
| `--scratch-tablespace` | | Tablespace used for scratch space during analysis (default `USERS`) |

## Output

An Excel report with one sheet per analysed table. Each row shows the LOB column, current size, estimated compressed size, and the projected compression ratio. A cover sheet (`REPORT_INFO`) captures the database metadata and all analysis parameters used.

## Compression Types

| Type | Description |
|------|-------------|
| `COMP_LOB_HIGH` | Maximum compression — highest CPU cost |
| `COMP_LOB_MEDIUM` | Balanced compression and CPU usage |
| `COMP_LOB_LOW` | Minimum compression — lowest CPU cost |
