---
title: "Top — Live Monitor"
description: "Real-time Oracle database performance dashboard with multiple views, CDB/PDB support, and optional HTML output."
weight: 10
---

# Top — Live Monitor

`orclT database performance top` launches an interactive, terminal-based performance dashboard. It continuously queries Oracle dynamic views and renders a multi-view TUI that refreshes at configurable intervals.

## Quick Start

```bash
orclT database performance top \
  -u <user> -p <password> -d <host>:<port>/<service>
```

Press `?` inside the TUI to display the keyboard shortcut help overlay.

## Views

Navigate between views using the keyboard shortcuts shown in the menu bar. Available views include:

| View | Description |
|------|-------------|
| **Overview** | Instances, Database, PDB heat-map, Sessions overview, SQL/Session overview |
| **Sessions** | Active sessions with state, event, SQL ID, and wait details |
| **SQL** | Top SQL by elapsed time, CPU, I/O; per-snap AWR consumers |
| **Memory** | SGA/PGA/AMM components, top PGA consumers (by SQL and session) |
| **RMAN** | Backup status, RMAN configuration, Block Change Tracking, corruption alerts |
| **Locks** | Lock holder and waiter chains |
| **RAC** | RAC services and inter-connect metrics |
| **IO** | I/O performance metrics per datafile and tablespace |
| **Data Guard** | Standby configuration, apply lag, MRP0 status |
| **ASM** | Disk groups, disks, volumes, and ASM clients |
| **Engineered** | Exadata DB nodes, storage cells, HW metrics, and cell alerts |
| **Objects** | Hot objects and tablespace usage |
| **Statistics** | Outdated statistics, calibration, jobs, and configuration |
| **LongOps** | Long-running operations (sort, hash join, direct load, etc.) |
| **OS Stats** | OS-level statistics reported by Oracle |
| **SQL Regression** | SQL statements that have regressed in elapsed time |

## View-Selection Flags

Start the TUI directly in a specific fullscreen view:

| Flag | View |
|------|------|
| `--sessions-only` | Sessions |
| `--top-sql` | Top SQL |
| `--memory-only` | Memory |
| `--rman-only` | RMAN |
| `--locks-only` | Locks |
| `--rac-only` | RAC |
| `--io-only` | IO |
| `--dataguard-only` | Data Guard |
| `--asm-only` | ASM |
| `--engineered-only` | Engineered Systems |
| `--objects-only` | Objects |
| `--tablespaces-only` | Tablespaces |
| `--statistics-only` | Statistics |
| `--longops-only` | Long Operations |
| `--os-only` | OS Statistics |
| `--sqlregression-only` | SQL Regression |

## HTML Dashboard

```bash
orclT database performance top \
  -u <user> -p <password> -d <host>:<port>/<service> \
  --html --html-port 8080
```

Launches an HTTP server on the specified port and serves an Oracle Redwood-styled HTML dashboard instead of the TUI.

## Row Limits

| Flag | Default | Description |
|------|---------|-------------|
| `--sql-limit` | 50 | Maximum rows in the Top SQL view |
| `--longops-limit` | auto | Maximum rows in the LongOps view |
| `--rman-limit` | auto | Maximum rows in the RMAN view |
| `--locks-limit` | auto | Maximum rows in the Locks view |
| `--rac-limit` | auto | Maximum rows in the RAC view |
| `--io-limit` | auto | Maximum rows in the IO view |
| `--objects-limit` | auto | Maximum rows in the Objects view |
| `--tablespaces-limit` | auto | Maximum rows in the Tablespaces view |
| `--os-limit` | auto | Maximum rows in the OS Statistics view |

## Refresh Interval Overrides

All intervals are in seconds. The defaults are tuned for production use, but can be adjusted:

| Flag | Default (s) | Section |
|------|------------|---------|
| `--database-interval` | 60 | Database / Overview tiles |
| `--sessions-interval` | 30 | Sessions grid |
| `--sql-interval` | 5 | Top SQL |
| `--memory-interval` | 30 | Memory overview |
| `--rman-interval` | 10 | RMAN |
| `--locks-interval` | 5 | Locks |
| `--rac-interval` | 5 | RAC |
| `--io-interval` | 5 | IO |
| `--dataguard-standby-interval` | 10 | Data Guard standby |
| `--asm-diskgroups-interval` | 15 | ASM disk groups |
| `--engineered-db-interval` | 5 | Engineered DB nodes |
| `--statistics-outdated-interval` | 60 | Outdated statistics |
| `--longops-interval` | 10 | Long operations |

See the [CLI Flag Reference](/orclt/reference/cli-flags/) for the full list of interval flags.
