---
title: "Authentication & Credentials"
description: "How to manage database, SSH, and MOS credentials securely with the orclT keystore."
weight: 20
---

# Authentication & Credentials

orclT includes a built-in encrypted keystore so you do not have to pass passwords on the command line every time.

## Credential Types

| Type | Used by |
|------|---------|
| Database credentials | All `database` commands |
| SSH credentials | `ssh tunnels` |
| MOS credentials | `mos`, `patch download`, `patch goldimage` |

## Saving Credentials

Add `--save-credentials` to any command that accepts connection flags. orclT encrypts and stores the credentials locally.

```bash
# Save database credentials
orclT database performance top \
  -u <user> -p <password> -d <host>:<port>/<service> \
  --save-credentials

# Save MOS credentials
orclT patch download \
  --mosuser <mos-email> --mospass <mos-password> \
  --save-credentials
```

On subsequent runs, omit the credential flags entirely — they will be retrieved from the keystore automatically.

## Deleting Credentials

```bash
orclT --delete-credentials
```

This removes **all** stored credentials (database, SSH, and MOS) from the keystore.

## Database Driver Selection

| Driver | Flag | Requirements |
|--------|------|--------------|
| `go_ora` | (default) | None — pure Go, no Oracle libraries needed |
| `godror` | `--use-godror` | Oracle Client or Instant Client libraries on `LD_LIBRARY_PATH` / `PATH` |

Pass `--oracle-client-path` or `--oracle-instant-client-path` to point orclT to the Oracle libraries when using `godror`.

## Connection Modes

The `--connection-mode` flag (available on benchmark and proxy commands) accepts:

- `NONE` — default Oracle behaviour
- `DEDICATED` — dedicated server process
- `SHARED` — shared server (MTS)
- `DRCP` — Database Resident Connection Pooling
