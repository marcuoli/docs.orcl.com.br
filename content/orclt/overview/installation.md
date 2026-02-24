---
title: "Installation"
description: "How to download and install orclT on Linux and Windows."
weight: 20
---

# Installation

## Download a Pre-built Binary

Pre-built binaries for Linux x86\_64 and Windows x86\_64 are available on the [GitHub Releases page](https://github.com/marcuoli/orclT/releases/latest).

Download the archive for your platform, extract it, and place the `orclT` binary (or `orclT.exe` on Windows) somewhere on your `PATH`.

**Linux example:**

```bash
# Download the latest release tarball for Linux
tar -xzf orclT_linux_amd64.tar.gz
chmod +x orclT
sudo mv orclT /usr/local/bin/
orclT --help
```

**Windows:** Extract the `.zip` archive and add the directory to your `%PATH%`.

## Build from Source

Requirements: [Go 1.24+](https://golang.org/dl/)

```bash
git clone https://github.com/marcuoli/orclT.git
cd orclT
go build -o orclT .
```

The resulting binary has no external runtime dependencies when using the default `go_ora` driver.

## Using the godror Driver (Optional)

The `godror` driver enables SYSDBA connections and uses Oracle's official OCI layer. To use it:

1. Install [Oracle Instant Client](https://www.oracle.com/database/technologies/instant-client.html) and ensure the libraries are on `LD_LIBRARY_PATH` (Linux) or `PATH` (Windows).
2. Pass `--use-godror` (and optionally `--oracle-instant-client-path`) when connecting.

The default `go_ora` driver requires no Oracle client libraries.

## Verify the Installation

```bash
orclT --help
```

You should see the list of available commands and global flags.
