---
title: "Compare"
description: "Compare initialization parameters and SQL execution plans between two Oracle databases."
weight: 20
---

# Compare

`orclT database performance compare` connects to two Oracle databases simultaneously and produces a side-by-side diff of their initialization parameters or SQL execution plans.

## Sub-commands

| Sub-command | Description |
|-------------|-------------|
| `parameters` | Compare `GV$PARAMETER` values between source and target |
| `sql` | Compare SQL execution plans between source and target |

## Parameters Comparison

```bash
orclT database performance compare parameters \
  -u <source-user> -p <source-password> -d <source-host>:<port>/<service> \
  --target-username <target-user> \
  --target-password <target-password> \
  --target-db-url <target-host>:<port>/<service>
```

### Flags

| Flag | Description |
|------|-------------|
| `--target-username` | Target database username |
| `--target-password` | Target database password |
| `--target-db-url` | Target database JDBC URL |
| `--target-sysdba` | Connect to target as SYSDBA |
| `--target-sysoper` | Connect to target as SYSOPER |
| `--target-connection-mode` | Target session mode (`DEDICATED`, `SHARED`, `DRCP`) |
| `--source-alias` | Label for source columns (default `SOURCE`) |
| `--target-alias` | Label for target columns (default `TARGET`) |
| `--ignore-parameter` | Parameter name to exclude (repeatable) |
| `--show-all` | Show all parameters, not only differences |
| `--report-file` | Generate an Excel report (optional filename; timestamped by default) |

## Output

By default, only **differing** parameters are shown. Use `--show-all` to include identical values. An optional Excel report can be generated with `--report-file`.
