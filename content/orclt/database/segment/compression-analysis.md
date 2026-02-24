---
title: "Segment Compression Analysis"
description: "Analyse the compression types currently applied to each data block in a table or schema."
weight: 10
---

# Segment Compression Analysis

`orclT database segment compression-analysis` calls `DBMS_COMPRESSION.GET_COMPRESSION_TYPE` for sampled blocks in a table and produces a breakdown of how many rows are stored under each compression type.

> **Note:** This command requires `EXECUTE` privilege on `DBMS_COMPRESSION`. A tablespace is needed for scratch space during analysis.

## Usage

Analyse a specific table:

```bash
orclT database segment compression-analysis \
  -u <user> -p <password> -d <host>:<port>/<service> \
  --schema <SCHEMA> \
  --table <TABLE>
```

Analyse all non-Oracle-maintained schemas:

```bash
orclT database segment compression-analysis \
  -u <user> -p <password> -d <host>:<port>/<service> \
  --all-non-oracle-maintained \
  --report-file segment_compression.xlsx
```

## Flags

| Flag | Short | Description |
|------|-------|-------------|
| `--schema` | `-s` | Target schema name |
| `--table` | `-t` | Target table name |
| `--all-non-oracle-maintained` | `-a` | Include all non-Oracle-maintained schemas |
| `--parallel` | `-P` | Degree of parallelism (default 1) |
| `--scratch-tablespace` | `-S` | Tablespace used for scratch space (default `USERS`) |
| `--report-file` | `-r` | Output Excel filename |

## Compression Types Reported

| Compression Type | Description |
|-----------------|-------------|
| No Compression | Uncompressed row |
| Basic | Basic table compression (DDL + direct path load) |
| Advanced | Advanced Row Compression (OLTP) |
| HCC Query High | Hybrid Columnar Compression for Query — high ratio |
| HCC Query Low | Hybrid Columnar Compression for Query — low ratio |
| HCC Archive High | Hybrid Columnar Compression for Archive — high ratio |
| HCC Archive Low | Hybrid Columnar Compression for Archive — low ratio |
| LOB High | High compression for LOB operations |
| LOB Medium | Medium compression for LOB operations |
| LOB Low | Low compression for LOB operations |

## Output

An Excel report with a cover sheet (`REPORT_INFO`) and a `GENERAL` sheet listing each table, the total block count sampled, and the distribution of rows across compression types.
