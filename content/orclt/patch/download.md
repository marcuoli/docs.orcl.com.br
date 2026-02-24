---
title: "Patch Download"
description: "Download Oracle patches, Release Updates, and tools from My Oracle Support."
weight: 10
---

# Patch Download

`orclT patch download` authenticates to My Oracle Support and downloads patches by ID, version, or release. It supports parallel downloads, pattern filtering, and optional inclusion of bundled tools such as OPatch, AutoUpgrade, and AHF.

## Usage

Download specific patches by ID:

```bash
orclT patch download \
  --mosuser <email> --mospass <password> \
  --patchid 35787242,35942994 \
  --platform 226 \
  --target-dir /patches
```

Download the latest Release Update for Oracle 19c:

```bash
orclT patch download \
  --mosuser <email> --mospass <password> \
  --version 19 \
  --include-opatch \
  --include-ahf \
  --target-dir /patches/19c
```

List available patches without downloading:

```bash
orclT patch download \
  --mosuser <email> --mospass <password> \
  --version 19 \
  --just-list
```

## Flags

| Flag | Description |
|------|-------------|
| `--mosuser` | My Oracle Support username (email) |
| `--mospass` | My Oracle Support password |
| `--delete-mos-credentials` | Remove MOS credentials from the keystore |
| `--patchid` | Comma-separated list of patch numbers |
| `--platform` | Comma-separated list of platform IDs |
| `--regexp` | Regular expression filter for patch filenames |
| `--target-dir` | Download destination directory |
| `--create-directory-tree` | Organise into `BUNDLE/`, `ONEOFF/`, and `TOOLS/` subdirectories |
| `--version` | Oracle major version (downloads latest RU for that version) |
| `--release` | Specific Oracle release (e.g. `19.25`) |
| `--recommended` | Download recommended patches (MOS notes 555.1 / 888.1) |
| `--force` | Overwrite already-downloaded files |
| `--just-list` | Print matching patches without downloading |
| `--list-platforms` | List supported platform IDs and exit |
| `--parallel` | Number of concurrent downloads (0 = auto) |
| `--chunksize` | Download chunk size in KB (default 8192) |
| `--download-timeout` | Timeout per patch download in seconds (default 600) |

### Tool Inclusion Flags

| Flag | Tool |
|------|------|
| `--include-ahf` | Autonomous Health Framework |
| `--include-opatch` | OPatch |
| `--include-cvu` | Cluster Verification Utility |
| `--include-rda` | Remote Diagnostic Agent |
| `--include-autoupgrade` | AutoUpgrade |
| `--include-apex` | Oracle APEX |
| `--include-apex-bundle` | APEX bundle patches |
| `--include-oeda` | Oracle Exadata Deployment Assistant |
| `--include-patchmgr` | Exadata Patch Manager |
| `--include-all-tools` | All of the above |
| `--include-exadata-tools` | Exadata-specific tools only |
| `--include-gold-images` | Oracle Gold Images |
| `--exclude-ru` | Exclude Release Updates |
