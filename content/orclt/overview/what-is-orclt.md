---
title: "What Is orclT"
description: "An overview of orclT's capabilities, command hierarchy, and supported platforms."
weight: 10
---

# What Is orclT

orclT is a single-binary command-line toolkit for Oracle Database administrators. It groups related workflows under intuitive top-level commands, making day-to-day DBA tasks faster and more scriptable.

## Command Overview

| Command | Description |
|---------|-------------|
| `database` | Live monitoring, LOB analysis, performance tools, proxy, recovery, and more |
| `backup` | Database and file-system backup to local, NFS, S3, or MinIO destinations |
| `patch` | Download Oracle patches and create Gold Images from My Oracle Support |
| `mos` | Upload files to My Oracle Support service requests |
| `ssh` | Manage SSH tunnels with keep-alive, throughput monitoring, and TUI status |
| `asm` | List ASM disks and QEMU/SCSI device information |
| `app` | Show application info and list dependency licenses |

## Supported Platforms

- **Linux** — x86\_64 (primary)
- **Windows** — x86\_64

## Oracle Version Support

orclT connects to **Oracle Database 12c through 23ai**, including CDB/PDB multitenant architectures. It automatically detects whether it is connected to a CDB root, an application root, or a specific PDB and adjusts queries accordingly.

## Database Drivers

Two Oracle drivers are available:

| Driver | When to use |
|--------|-------------|
| `go_ora` (default) | Pure Go — no Oracle Client libraries required. Works on any machine. |
| `godror` | Requires Oracle Client or Instant Client libraries. Use with `--use-godror`. Enables SYSDBA connections. |
