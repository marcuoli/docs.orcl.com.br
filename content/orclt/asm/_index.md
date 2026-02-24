---
title: "ASM"
description: "Inspect ASM disks and QEMU/SCSI devices."
weight: 80
---

`orclT asm` provides inspection utilities for Oracle ASM (Automatic Storage Management) disk groups and the underlying block devices managed by QEMU/SCSI layers.

## Disks

`orclT asm disks` lists the ASM disks visible on the current host with detailed attributes such as disk path, size, disk group membership, reliability, and ASM header information.

```bash
orclT asm disks --list-asmdisks
```

To include QEMU/SCSI device identifiers alongside ASM attributes:

```bash
orclT asm disks --list-asmdisks --qemu-devices
```

### Flags

| Flag | Type | Default | Description |
|------|------|---------|-------------|
| `--list-asmdisks` | bool | false | List all ASM disks with detailed attributes |
| `--qemu-devices` | bool | false | Include QEMU/SCSI device IDs alongside ASM disk data |

### Output

The `--list-asmdisks` flag prints a table with columns such as:

| Column | Description |
|--------|-------------|
| Name | ASM disk path (e.g. `/dev/oracleasm/disks/DATA01`) |
| Header Status | ASM header state (e.g. `MEMBER`, `FORMER`) |
| Disk Group | Disk group the disk belongs to |
| Total (GiB) | Total disk size |
| Free (GiB) | Free space in the disk group |
| Redundancy | Disk group redundancy type (NORMAL, HIGH, EXTERNAL) |
| Failure Group | Failure group name |
| OS Device | Underlying OS block device |

When `--qemu-devices` is also specified, an additional column shows the QEMU/SCSI serial or device ID that corresponds to each ASM disk.

> **Note:** Root or appropriate OS privileges may be required to read some ASM disk headers.
