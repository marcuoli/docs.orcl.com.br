---
title: "Backup"
description: "Back up files, directories, and Oracle ASM disks to local, NFS, S3, or MinIO destinations."
weight: 40
---

`orclT backup` archives and uploads Oracle database files, RMAN backups, or arbitrary directories to a configurable backend storage target.

## Usage

```bash
orclT backup \
  --src /u01/app/oracle/oradata \
  --backend local \
  --dest-path /backup/oracle \
  --backup-type oracle
```

## Core Flags

| Flag | Description |
|------|-------------|
| `--src` | Source path (file or directory) to back up |
| `--name` | Backup object name (defaults to a timestamp) |
| `--backend` | Storage backend: `local`, `nfs`, `s3`, or `minio` |
| `--archive` | Create a `tar.gz` archive before upload (default `true`) |
| `--backup-type` | Backup profile: `oracle`, `rac`, or `host` (default `host`) |
| `--parallel` | Parallelism level for upload (default 2) |
| `--include` | Include only paths containing these substrings |
| `--exclude` | Exclude paths containing these substrings |
| `--follow-symlinks` | Follow symbolic links |
| `--preserve-perms` | Preserve file permissions inside the archive |
| `--include-asm-disks` | Include Oracle ASM disk devices (raw copy) |

## Local / NFS Backend

| Flag | Description |
|------|-------------|
| `--dest-path` | Destination directory path |

## S3 Backend

| Flag | Description |
|------|-------------|
| `--s3-bucket` | Bucket name |
| `--s3-region` | AWS region |
| `--s3-endpoint` | Custom endpoint URL (for S3-compatible stores) |
| `--s3-profile` | AWS credentials profile name |
| `--s3-force-path-style` | Use path-style addressing instead of virtual-hosted-style |

## MinIO Backend

| Flag | Description |
|------|-------------|
| `--minio-endpoint` | MinIO endpoint in `host:port` format |
| `--minio-access-key` | MinIO access key |
| `--minio-secret-key` | MinIO secret key |
| `--minio-bucket` | Bucket name |
| `--minio-secure` | Use HTTPS (default `true`) |
