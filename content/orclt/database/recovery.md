---
title: "Recovery — Verify"
description: "Verify the integrity of an Oracle control file."
weight: 60
---

# Recovery — Verify

`orclT database recovery verify` checks the structural integrity of an Oracle control file without mounting a database instance. It is useful for validating backup copies of control files before attempting a recovery operation.

## Usage

```bash
orclT database recovery verify \
  --control-file /path/to/control_file.bkp
```

## Flags

| Flag | Description |
|------|-------------|
| `--control-file` | Path to the control file to verify |

## Output

The command reports whether the control file is structurally valid, the database name and DBID encoded in the file, the sequence number, and the SCN range. A non-zero exit code indicates a corrupt or unreadable file.
