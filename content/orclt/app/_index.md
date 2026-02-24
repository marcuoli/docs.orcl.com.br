---
title: "App"
description: "Inspect orclT's own build dependencies, licenses, and GitHub metadata."
weight: 90
---

`orclT app` provides transparency into the software supply chain of orclT itself — listing every Go module dependency along with its license and available GitHub metadata.

## Packages

`orclT app packages` prints all dependencies bundled in the orclT binary.

```bash
orclT app packages --list
```

### Flags

| Flag | Short | Description |
|------|-------|-------------|
| `--list` | `-l` | List every dependency with its module path, version, license, and GitHub metadata |

### Output

Each row in the output includes:

| Column | Description |
|--------|-------------|
| Module | Go module path (e.g. `github.com/charmbracelet/bubbletea`) |
| Version | Tagged release version |
| License | SPDX license identifier (e.g. `MIT`, `Apache-2.0`) |
| Stars | GitHub star count (where available) |
| Description | Short repository description |
