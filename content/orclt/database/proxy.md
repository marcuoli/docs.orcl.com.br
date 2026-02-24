---
title: "Database Proxy"
description: "Run a transparent TCP proxy in front of an Oracle listener with SSL support and live connection statistics."
weight: 50
---

# Database Proxy

`orclT database proxy` starts a lightweight TCP proxy that sits in front of an Oracle listener. It forwards connections to a target database, optionally adding SSL/TLS termination, and provides real-time connection metrics.

## Usage

Start the proxy:

```bash
orclT database proxy \
  --proxy-port 1522 \
  --target-host <db-host> \
  --target-port 1521 \
  --target-service <service> \
  --max-connections 100
```

Start with SSL termination:

```bash
orclT database proxy \
  --proxy-port 1522 \
  --target-host <db-host> --target-port 1521 --target-service <service> \
  --ssl --ssl-mode require \
  --cert-file /path/to/cert.pem \
  --key-file /path/to/key.pem
```

## View Connection Statistics

```bash
orclT database proxy status \
  --proxy-host localhost --proxy-port 1522
```

## Flags

| Flag | Description |
|------|-------------|
| `--proxy-host` | Proxy server bind address (default listens on all interfaces) |
| `--proxy-port` | Port the proxy listens on |
| `--proxy-user` | Proxy management username |
| `--proxy-password` | Proxy management password |
| `--target-host` | Target Oracle listener hostname |
| `--target-port` | Target Oracle listener port (default 1521) |
| `--target-service` | Target database service name |
| `--ssl` | Enable SSL/TLS termination |
| `--ssl-mode` | SSL mode: `disable`, `allow`, `prefer`, or `require` |
| `--cert-file` | SSL certificate file path |
| `--key-file` | SSL private key file path |
| `--ca-file` | CA certificate file path |
| `--max-connections` | Maximum concurrent connections |
| `--connection-timeout` | Connection timeout in seconds (default 30) |
| `--enable-logging` | Log all connections |
| `--log-level` | Log verbosity: `debug`, `info`, `warn`, or `error` |
| `--show-stats` | Print current proxy statistics and exit |
