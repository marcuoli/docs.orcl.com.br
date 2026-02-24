---
title: "Benchmark — Connection"
description: "Benchmark Oracle database connection throughput and latency with concurrent sessions."
weight: 40
---

# Benchmark — Connection

`orclT database benchmark connection` opens a configurable number of concurrent database connections, runs a workload loop, and reports connection latency, throughput, and error rates.

## Usage

```bash
orclT database benchmark connection \
  -u <user> -p <password> -d <host>:<port>/<service> \
  --connections 20 \
  --duration 60 \
  --report-file benchmark.xlsx
```

## Flags

| Flag | Description |
|------|-------------|
| `--target-host` | Target database hostname or IP address |
| `--target-port` | Target database port (default 1521) |
| `--service-name` | Database service name |
| `--connections` | Number of concurrent connections (default 10) |
| `--duration` | Benchmark duration in seconds (default 30) |
| `--max-requests` | Maximum requests per connection (0 = unlimited) |
| `--connection-timeout` | Connection timeout in seconds (default 30) |
| `--think-time` | Time between operations per connection in milliseconds (default 1000) |
| `--connection-mode` | Session mode: `NONE`, `DEDICATED`, `SHARED`, or `DRCP` |
| `--report-file` | Output report file path |

## Output

The benchmark prints a real-time summary of active connections, requests per second, minimum/average/maximum latency, and error counts. If `--report-file` is specified an Excel report is saved at the end of the run.
