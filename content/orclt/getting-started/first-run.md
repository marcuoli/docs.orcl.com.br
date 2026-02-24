---
title: "First Run"
description: "Connect to an Oracle database and verify orclT is working correctly."
weight: 10
---

# First Run

All `database` commands require a connection to an Oracle instance. The three core connection flags are:

| Flag | Short | Description |
|------|-------|-------------|
| `--username` | `-u` | Database username |
| `--password` | `-p` | Database password |
| `--db-url` | `-d` | Connection URL in `host:port/service` format |

## Basic Connection

```bash
orclT database performance top \
  --username <user> \
  --password <password> \
  --db-url <host>:<port>/<service>
```

Replace `<host>`, `<port>`, `<service>`, `<user>`, and `<password>` with your actual connection details.

## SYSDBA Connection

To connect as SYSDBA you must use the `godror` driver with Oracle Client libraries present:

```bash
orclT database performance top \
  --username sys \
  --password <password> \
  --db-url <host>:<port>/<service> \
  --sysdba \
  --use-godror \
  --oracle-instant-client-path /path/to/instantclient
```

## Saving Credentials

To avoid entering credentials on every invocation, use the root-level `--save-credentials` flag. Credentials are stored in an encrypted local keystore.

```bash
orclT database performance top \
  --username <user> \
  --password <password> \
  --db-url <host>:<port>/<service> \
  --save-credentials
```

On subsequent runs, omit the credential flags — orclT will read them from the keystore automatically.

To remove saved credentials:

```bash
orclT --delete-credentials
```

## Useful Global Flags

| Flag | Short | Description |
|------|-------|-------------|
| `--debug` | `-D` | Enable debug output for troubleshooting |
| `--verbose` | `-V` | Increase output verbosity |
| `--log` | `-L` | Append execution details to a log file |
| `--no-confirmation` | `-Y` | Skip interactive confirmation prompts |
| `--sql-timeout` | | Maximum seconds for any single SQL statement (0 = no limit) |
