---
title: "Table Copy"
description: "Copy table data between Oracle databases with parallel stream support."
weight: 70
---

# Table Copy

`orclT database table copy` transfers rows from a table in a source database to an equivalent table in a target database. It supports parallel streams, direct-path inserts, and multi-insert batching for high throughput.

## Usage

```bash
orclT database table copy \
  -u <source-user> -p <source-password> -d <source-host>:<port>/<service> \
  --target-username <target-user> \
  --target-password <target-password> \
  --target-db-url <target-host>:<port>/<service> \
  --schema <SCHEMA> \
  --table <TABLE>
```

> **Tip:** Both databases can be on the same host or on different hosts. The copy reads from the source and writes to the target using a in-process pipeline — no intermediate file is created.

## Notes

- The target table must already exist and have a compatible column structure.
- Use the database connection flags described in the [Database](/orclt/database/) section to control drivers, SYSDBA mode, and timeouts.
