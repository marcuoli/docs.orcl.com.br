---
title: "Database"
description: "Oracle database commands: performance monitoring, LOB analysis, proxy, recovery, segment, and benchmark."
weight: 30
---

The `database` command group provides tools for Oracle database analysis, monitoring, and management.

All `database` subcommands share the following connection flags:

| Flag | Short | Description |
|------|-------|-------------|
| `--username` | `-u` | Database username |
| `--password` | `-p` | Database password |
| `--db-url` | `-d` | Connection URL (`host:port/service`) |
| `--sysdba` | | Connect as SYSDBA (requires `--use-godror`) |
| `--use-godror` | | Use the godror driver instead of go_ora |
| `--oracle-client-path` | | Path to Oracle Client libraries |
| `--oracle-instant-client-path` | | Path to Oracle Instant Client directory |
| `--sql-timeout` | | SQL statement timeout in seconds (0 = no limit) |
