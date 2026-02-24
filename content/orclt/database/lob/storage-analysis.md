---
title: "LOB Storage Analysis"
description: "Identify wasted space, oversized chunks, and null LOB columns with a detailed Excel report."
weight: 10
---

# LOB Storage Analysis

`orclT database lob storage-analysis` scans LOB segments and produces an Excel report covering segment sizes, chunk configuration, null percentages, wasted space estimates, and recommendations.

## Usage

```bash
orclT database lob storage-analysis \
  -u <user> -p <password> -d <host>:<port>/<service> \
  --schema <SCHEMA> \
  --table <TABLE>
```

Analyse all non-Oracle-maintained schemas:

```bash
orclT database lob storage-analysis \
  -u <user> -p <password> -d <host>:<port>/<service> \
  --all-non-oracle-maintained \
  --report-file lob_storage.xlsx
```

## Flags

| Flag | Short | Description |
|------|-------|-------------|
| `--schema` | `-s` | Target schema name |
| `--table` | `-t` | Target table name |
| `--column` | `-c` | Specific LOB column name |
| `--partition` | `-n` | Restrict analysis to a single partition |
| `--lob` | `-l` | LOB segment name |
| `--table-as-whole` | `-w` | Ignore partition filter and scan the entire table |
| `--all-non-oracle-maintained` | `-a` | Include all non-Oracle-maintained schemas |
| `--parallel` | `-P` | Degree of parallelism (default 1) |
| `--report-file` | `-r` | Output Excel filename |
| `--size-in-bytes` | `-b` | Display sizes in bytes instead of human-readable units |
| `--use-dictionary-statistics` | | Use cached dictionary statistics rather than scanning |
| `--lob-row-limit-threshold` | | LOB size threshold in bytes (default 4000) |
| `--lob-null-percentage-threshold` | | Null percentage threshold to flag (default 50) |
| `--space-wasted-percentage-threshold` | | Wasted space percentage threshold (default 50) |
| `--chunk-avg-size-ratio-threshold` | | Chunk-to-average LOB size ratio threshold (default 1.0) |

## Output

The Excel report includes a cover sheet (`REPORT_INFO`) with database metadata, analysis parameters, and a data dictionary. The `GENERAL` sheet lists each LOB segment with columns such as schema, table, column, segment size, chunk size, null percentage, wasted space, and recommendations for resizing or compression.
