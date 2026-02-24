---
title: "OS/DB Performance (osdb)"
description: "Collect OS and Oracle session metrics from multiple hosts simultaneously over SSH."
weight: 40
---

# OS/DB Performance (osdb)

`orclT database performance osdb` connects to one or more database hosts over SSH and collects OS-level metrics alongside Oracle session counts. It is designed for quick, multi-host snapshots when evaluating operating system impact on database performance.

## Usage

Check a single host:

```bash
orclT database performance osdb \
  --host <host> \
  --username <ssh-user> \
  --password <ssh-password>
```

Check multiple hosts from a file:

```bash
orclT database performance osdb \
  --hostsfile hosts.txt \
  --username <ssh-user> \
  --ssh-key-file ~/.ssh/id_rsa \
  --total_count 5 \
  --interval 10
```

## Flags

| Flag | Description |
|------|-------------|
| `--hostsfile` | Path to a file containing a list of hostnames (one per line) |
| `--host` | Single hostname or IP address |
| `--username` | SSH username |
| `--password` | SSH password |
| `--ssh-key-file` | SSH private key file path |
| `--total_count` | Number of collection iterations (default 1) |
| `--interval` | Seconds between iterations (default 5) |
| `--timestamp` | Include a timestamp column in output |
| `--sortbyses` | Sort output by session count |
| `--dbbyrow` | Transpose output so databases appear as rows |
| `--dbsession` | Include per-database session distribution |
| `--ccpuusage` | Include cumulative CPU usage |
| `--icpuusage` | Include immediate CPU usage |
