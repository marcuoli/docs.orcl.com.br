---
title: "SSH"
description: "Manage SSH tunnels with keep-alive monitoring and throughput statistics."
weight: 70
---

`orclT ssh` manages persistent SSH tunnels. It supports multiple concurrent tunnels, keep-alive pings, throughput monitoring, and displays tunnel status in a live TUI.

## Tunnels

`orclT ssh tunnels` starts one or more SSH tunnels defined either on the command line or in a JSON configuration file.

```bash
orclT ssh tunnels \
  --ssh-host <bastion-host> \
  --ssh-user <ssh-user> \
  --ssh-port 22 \
  --use-keyfile \
  --keyfile ~/.ssh/id_rsa
```

Using a configuration file (recommended for multiple tunnels):

```bash
orclT ssh tunnels --config-file tunnels.json
```

### Flags

| Flag | Type | Default | Description |
|------|------|---------|-------------|
| `--config-file` | string | | Path to a JSON tunnel configuration file |
| `--ssh-host` | string | | SSH server hostname or IP address |
| `--ssh-port` | int | 22 | SSH server port |
| `--ssh-user` | string | | SSH username |
| `--ssh-password` | string | | SSH password |
| `--use-keyfile` | bool | false | Authenticate with an SSH key file |
| `--keyfile` | string | `~/.ssh/id_rsa` | Path to the SSH private key |

### Configuration File

A JSON file can describe multiple tunnels at once:

```json
[
  {
    "name": "db-tunnel",
    "ssh_host": "<bastion-host>",
    "ssh_port": 22,
    "ssh_user": "<ssh-user>",
    "use_keyfile": true,
    "keyfile": "~/.ssh/id_rsa",
    "local_port": 15210,
    "remote_host": "<target-db-host>",
    "remote_port": 1521
  }
]
```

> **Security:** Never commit configuration files containing passwords. Use key-based authentication or the keystore instead.

### Features

- **Keep-alive**: maintains tunnel stability with configurable heartbeat pings
- **Throughput monitoring**: live bytes-in / bytes-out per tunnel
- **Ping latency**: round-trip time to both the SSH host and the remote target
- **TUI status view**: see all active tunnels, connection counts, and health in one screen
