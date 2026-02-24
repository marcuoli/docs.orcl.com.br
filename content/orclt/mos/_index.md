---
title: "My Oracle Support (MOS)"
description: "Upload files to My Oracle Support service requests directly from the command line."
weight: 60
---

`orclT mos` provides tooling for interacting with My Oracle Support. MOS credentials can be saved to the keystore to avoid entering them on every invocation.

## Upload

`orclT mos upload` uploads a file to a specific MOS Service Request.

```bash
orclT mos upload \
  --mosuser <email> --mospass <password> \
  --file /path/to/diagnostics.zip \
  --sr <SR-number>
```

Rename the file upon upload:

```bash
orclT mos upload \
  --mosuser <email> --mospass <password> \
  --file /path/to/trace.trc \
  --sr <SR-number> \
  --rename-uploaded-file incident_trace_$(date +%Y%m%d).trc
```

### Upload Flags

| Flag | Short | Description |
|------|-------|-------------|
| `--mosuser` | | My Oracle Support username (email) |
| `--mospass` | | My Oracle Support password |
| `--delete-mos-credentials` | | Remove MOS credentials from the keystore |
| `--file` | `-f` | Path to the file to upload |
| `--sr` | `-s` | Service Request number |
| `--rename-uploaded-file` | `-r` | Rename the file as shown on MOS after upload |

> Use the root-level `--save-credentials` flag to persist MOS credentials so you can omit `--mosuser` and `--mospass` on future runs.
