---
title: "Gold Image"
description: "Download and assemble an Oracle Gold Image patch bundle from My Oracle Support."
weight: 20
---

# Gold Image

`orclT patch goldimage` downloads and assembles an Oracle Gold Image — a pre-applied, self-contained Oracle software image suitable for rapid provisioning. It uses the same MOS download engine as `patch download` but targets Gold Image artifacts.

## Usage

```bash
orclT patch goldimage \
  --mosuser <email> --mospass <password> \
  --version 19 \
  --platform 226 \
  --targetdir /images/oracle19c
```

Include tooling bundles:

```bash
orclT patch goldimage \
  --mosuser <email> --mospass <password> \
  --version 19 \
  --platform 226 \
  --include-opatch \
  --include-ahf \
  --targetdir /images/oracle19c
```

## Flags

| Flag | Description |
|------|-------------|
| `--mosuser` | My Oracle Support username (email) |
| `--mospass` | My Oracle Support password |
| `--patchid` | Comma-separated list of patch numbers |
| `--platform` | Comma-separated list of platform IDs |
| `--regexp` | Regular expression filter for filenames |
| `--targetdir` | Download destination directory |
| `--version` | Oracle major version |
| `--release` | Specific Oracle release (e.g. `19.25`) |
| `--recommended` | Download recommended patches |
| `--force` | Overwrite existing files |
| `--justlist` | List matching artifacts without downloading |
| `--list-platforms` | List supported platform IDs and exit |
| `--parallel` | Enable parallel downloads |
| `--parallel-limit` | Maximum parallel downloads (default 4) |
| `--chunksize` | Download chunk size in KB (default 8192) |
| `--include-ahf` | Include Autonomous Health Framework |
| `--include-opatch` | Include OPatch |
| `--include-autoupgrade` | Include AutoUpgrade |
| `--include-cvu` | Include Cluster Verification Utility |
| `--include-all-tools` | Include all available tooling bundles |
| `--include-gold-images` | Include Gold Images |
| `--exclude-ru` | Exclude Release Updates |
