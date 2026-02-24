---
title: "CLI Flags"
description: "Master reference for every orclT flag, grouped by command."
weight: 1
---

This page lists every flag exposed by the `orclT` CLI. Flags are grouped by command and subcommand. All examples use placeholder values — replace `<user>`, `<host>`, `<port>`, `<service>`, `<email>`, and `<password>` with your actual values.

## Root flags (`orclT`)

| Flag | Short | Description |
|------|-------|-------------|
| `--debug` | `-D` | Enable debug mode |
| `--delete-credentials` | | Delete all credentials (MOS, SSH, and DB) from keystore |
| `--help` | `-h` | Show help information |
| `--log` | `-L` | Append execution details to the log file |
| `--no-confirmation` | `-Y` | Disable confirmation prompts |
| `--save-credentials` | | Save all credentials (MOS, SSH, and DB) to keystore |
| `--verbose` | `-V` | Enable verbose output |

---

## `orclT app packages`

| Flag | Short | Description |
|------|-------|-------------|
| `--list` | `-l` | List every dependency with license and GitHub metadata |

---

## `orclT asm disks`

| Flag | Description |
|------|-------------|
| `--list-asmdisks` | List ASM disks with detailed attributes |
| `--qemu-devices` | List QEMU/SCSI devices with their IDs |

---

## `orclT backup`

| Flag | Description |
|------|-------------|
| `--src` | Source path to back up (file or directory) |
| `--name` | Backup object name (defaults to timestamp) |
| `--backend` | Backend type: `s3`, `minio`, `nfs`, or `local` (default `local`) |
| `--archive` | Create tar.gz from source before upload (default `true`) |
| `--backup-type` | Backup profile: `oracle`, `rac`, or `host` (default `host`) |
| `--parallel` | Parallelism for multi-part uploads (default `2`) |
| `--include` | Include only paths containing any of these substrings |
| `--exclude` | Exclude paths containing any of these substrings |
| `--follow-symlinks` | Follow symbolic links during archiving |
| `--preserve-perms` | Preserve file permissions inside the archive |
| `--include-asm-disks` | Include Oracle ASM disks (raw copy) in the backup |
| `--dest-path` | Destination path for `local` or `nfs` backend |
| `--s3-bucket` | S3 bucket name |
| `--s3-region` | S3 region |
| `--s3-endpoint` | Custom S3 endpoint (optional, for S3-compatible stores) |
| `--s3-profile` | S3 credentials profile (optional) |
| `--s3-force-path-style` | Use path-style addressing for S3-compatible stores |
| `--minio-endpoint` | MinIO endpoint (`<host>:<port>`) |
| `--minio-access-key` | MinIO access key |
| `--minio-secret-key` | MinIO secret key |
| `--minio-bucket` | MinIO bucket name |
| `--minio-secure` | Use HTTPS when connecting to MinIO (default `true`) |

---

## `orclT database` — common connection flags

These flags are available on every `database` subcommand.

| Flag | Short | Description |
|------|-------|-------------|
| `--username` | `-u` | Database username |
| `--password` | `-p` | Database password |
| `--db-url` | `-d` | `host:port/service` connection string |
| `--sysdba` | | Connect as SYSDBA (enables local BEQ when `--db-url` is omitted) |
| `--oracle-client-path` | | Path to Oracle Client libraries |
| `--oracle-instant-client-path` | | Path to Oracle Instant Client directory |
| `--use-godror` | | Use the godror driver (requires Oracle Client libraries) |
| `--sql-timeout` | | Max duration in seconds for SQL statements (`0` disables timeout) |

---

### `orclT database benchmark connection`

| Flag | Description |
|------|-------------|
| `--target-host` | Target database hostname or IP address |
| `--target-port` | Target database port (default `1521`) |
| `--service-name` | Database service name |
| `--connections` | Number of concurrent connections (default `10`) |
| `--duration` | Benchmark duration in seconds (default `30`) |
| `--max-requests` | Max requests per connection (`0` = unlimited) |
| `--connection-timeout` | Connection timeout in seconds (default `30`) |
| `--think-time` | Think time between operations in milliseconds (default `1000`) |
| `--connection-mode` | Session mode: `NONE`, `DEDICATED`, `SHARED`, or `DRCP` |
| `--report-file` | Output report file path |

---

### `orclT database lob` — common LOB flags

| Flag | Short | Description |
|------|-------|-------------|
| `--schema` | `-s` | Schema name (required unless `--all-non-oracle-maintained`) |
| `--table` | `-t` | Table name |
| `--column` | `-c` | Column name |
| `--partition` | `-n` | Partition name |
| `--lob` | `-l` | LOB segment name |
| `--table-as-whole` | `-w` | Ignore partition filter and scan the whole table |
| `--all-non-oracle-maintained` | `-a` | Include all non-Oracle maintained schemas |
| `--parallel` | `-P` | Degree of parallelism (default `1`) |
| `--report-file` | `-r` | Output Excel file name |
| `--size-in-bytes` | `-b` | Display sizes in bytes instead of human-readable units |

#### `database lob storage-analysis`

| Flag | Description |
|------|-------------|
| `--use-dictionary-statistics` | Use dictionary statistics instead of scanning tables |
| `--lob-row-limit-threshold` | LOB size threshold in bytes (default `4000`) |
| `--lob-null-percentage-threshold` | Null percentage threshold (default `50`) |
| `--space-wasted-percentage-threshold` | Space waste percentage threshold (default `50`) |
| `--chunk-avg-size-ratio-threshold` | Chunk to average LOB size ratio threshold (default `1.0`) |

#### `database lob compression-analysis`

| Flag | Description |
|------|-------------|
| `--compression-type` | Compression type: `COMP_LOB_HIGH`, `COMP_LOB_MEDIUM`, `COMP_LOB_LOW` |
| `--subset-rows` | Row sampling level for compression ratio estimation |
| `--scratch-tablespace` | Scratch tablespace (default `USERS`) |

---

### `orclT database performance compare`

| Flag | Description |
|------|-------------|
| `--target-username` | Target database username |
| `--target-password` | Target database password |
| `--target-db-url` | `host:port/service` for the target database |
| `--target-sysdba` | Connect to target as SYSDBA |
| `--target-sysoper` | Connect to target as SYSOPER |
| `--target-connection-mode` | Target session mode: `DEDICATED`, `SHARED`, or `DRCP` |
| `--source-alias` | Label for source columns (default `SOURCE`) |
| `--target-alias` | Label for target columns (default `TARGET`) |
| `--ignore-parameter` | Parameter name to ignore (repeatable) |
| `--show-all` | Display all parameters, not only differences |
| `--report-file` | Generate an Excel report (defaults to a timestamped filename) |

---

### `orclT database performance osdbperf`

| Flag | Description |
|------|-------------|
| `--hostsfile` | File containing the list of hosts to check |
| `--host` | Single host to check |
| `--username` | SSH username |
| `--password` | SSH password |
| `--ssh-key-file` | SSH private key file |
| `--total_count` | Total collection iterations (default `1`) |
| `--interval` | Interval between iterations in seconds (default `5`) |
| `--timestamp` | Include timestamp in output |
| `--sortbyses` | Sort output by session count |
| `--dbbyrow` | Transpose output (databases by row, servers by column) |
| `--dbsession` | Include database session distribution |
| `--ccpuusage` | Include cumulative CPU usage |
| `--icpuusage` | Include immediate CPU usage |

---

### `orclT database performance plan`

| Flag | Description |
|------|-------------|
| `--create-sql-baseline` | Create a SQL baseline |
| `--create-sql-profile` | Create a SQL profile |
| `--create-sql-patch` | Create a SQL patch |
| `--sql-id-analysis` | Analyze SQL statements by SQL ID |
| `--sql-id` | SQL ID to analyze |
| `--plan-hash-value` | Plan hash value to analyze |
| `--fixed` | Create SQL baseline as fixed |
| `--disabled` | Create SQL baseline as disabled |
| `--hint` | Hint text for SQL patch creation |
| `--show-plan-info` | Display detailed plan information |
| `--show-plan-outline` | Display plan outline |
| `--sql-profile-category` | SQL profile category (default `DEFAULT`) |
| `--sql-profile-name` | SQL profile name |
| `--sql-profile-force-match` | Enable `FORCE MATCHING` for profile |
| `--sql-profile-replace` | Replace existing SQL profile |
| `--sql-profile-recreate` | Drop and recreate SQL profile |
| `--sql-profile-child-number` | Child number of SQL plan |

#### `database performance plan regression`

| Flag | Description |
|------|-------------|
| `--limit` | Limit number of rows (`0` = unlimited) |
| `--min-factor` | Minimum regression factor to include |
| `--min-seconds` | Minimum regression seconds delta to include |
| `--include-improved` | Include improved SQL statements |

---

### `orclT database performance top`

#### View selection

| Flag | Description |
|------|-------------|
| `--sessions-only` | Start in Sessions fullscreen view |
| `--asm-only` | Start in ASM fullscreen view |
| `--longops-only` | Start in LongOps fullscreen view |
| `--engineered-only` | Start in Engineered Systems fullscreen view |
| `--rman-only` | Start in RMAN fullscreen view |
| `--locks-only` | Start in Locks fullscreen view |
| `--rac-only` | Start in RAC fullscreen view |
| `--io-only` | Start in IO fullscreen view |
| `--dataguard-only` | Start in Data Guard fullscreen view |
| `--objects-only` | Start in Objects fullscreen view |
| `--tablespaces-only` | Start in Tablespaces fullscreen view |
| `--statistics-only` | Start in Statistics fullscreen view |
| `--memory-only` | Start in Memory fullscreen view |
| `--os-only` | Start in OS Statistics fullscreen view |
| `--sqlregression-only` | Start in SQL Regression fullscreen view |
| `--top-sql` | Start in Top SQL fullscreen view |

#### HTML dashboard

| Flag | Description |
|------|-------------|
| `--html` | Serve a Redwood-styled HTML dashboard |
| `--html-port` | Port for the HTML server (default `8080`) |

#### Top SQL

| Flag | Description |
|------|-------------|
| `--sql-sort` | Sort metric: `elapsed`, `cpu`, `gets`, `reads`, or `execs` |
| `--sql-limit` | Row limit for Top SQL (default `50`) |

#### Row limits

| Flag | Default | Description |
|------|---------|-------------|
| `--longops-limit` | 0 (auto) | Row limit for LongOps view |
| `--rman-limit` | 0 (auto) | Row limit for RMAN view |
| `--locks-limit` | 0 (auto) | Row limit for Locks view |
| `--rac-limit` | 0 (auto) | Row limit for RAC view |
| `--io-limit` | 0 (auto) | Row limit for IO view |
| `--objects-limit` | 0 (auto) | Row limit for Objects view |
| `--tablespaces-limit` | 0 (auto) | Row limit for Tablespaces view |
| `--os-limit` | 0 (auto) | Row limit for OS Statistics view |

#### Refresh intervals

| Flag | Default (s) | Description |
|------|------------|-------------|
| `--database-interval` | 60 | Database summary tiles |
| `--sessions-interval` | 30 | Sessions grid |
| `--instances-interval` | 60 | RAC instances overview |
| `--pdbs-interval` | 60 | PDB heat-map |
| `--events-interval` | 60 | Wait events panel |
| `--engineered-db-interval` | 5 | Engineered DB nodes |
| `--engineered-cell-interval` | 5 | Engineered cell nodes |
| `--engineered-cell-hw-interval` | 30 | Engineered cell hardware metrics |
| `--engineered-cell-alerts-interval` | 30 | Engineered cell alerts |
| `--asm-clients-interval` | 10 | ASM clients |
| `--asm-attributes-interval` | 30 | ASM attributes |
| `--asm-diskgroups-interval` | 15 | ASM disk groups |
| `--asm-disks-interval` | 15 | ASM disks |
| `--asm-volumes-interval` | 30 | ASM volumes |
| `--rman-interval` | 10 | RMAN summary |
| `--locks-interval` | 5 | Locks |
| `--rac-interval` | 5 | RAC services |
| `--io-interval` | 5 | IO performance |
| `--objects-interval` | 30 | Hot objects |
| `--tablespaces-interval` | 60 | Tablespaces capacity |
| `--dataguard-config-interval` | 30 | Data Guard configuration |
| `--dataguard-standby-interval` | 10 | Data Guard standby metrics |
| `--dataguard-managed-standby-interval` | 10 | Data Guard managed standby processes |
| `--dataguard-recovery-progress-interval` | 10 | Data Guard recovery progress |
| `--dataguard-mrp0-status-interval` | 10 | Data Guard MRP0 status |
| `--statistics-outdated-interval` | 60 | Outdated statistics |
| `--statistics-system-interval` | 300 | System statistics |
| `--statistics-calibration-interval` | 300 | In-memory statistics calibration |
| `--statistics-jobs-interval` | 120 | Statistics jobs |
| `--statistics-config-interval` | 300 | Statistics configuration |
| `--memory-interval` | 30 | Memory overview |
| `--os-interval` | 30 | OS Statistics |
| `--sqlregression-interval` | 30 | SQL Regression panel |
| `--sql-interval` | 5 | Top SQL |
| `--longops-interval` | 10 | Long operations |

---

### `orclT database proxy`

| Flag | Description |
|------|-------------|
| `--proxy-host` | Proxy server hostname or IP address |
| `--proxy-port` | Proxy server port (default `1521`) |
| `--proxy-user` | Proxy server username |
| `--proxy-password` | Proxy server password |
| `--target-host` | Target database hostname or IP address |
| `--target-port` | Target database port (default `1521`) |
| `--target-service` | Target database service name |
| `--ssl` | Enable SSL/TLS for proxy connections |
| `--ssl-mode` | SSL mode: `disable`, `allow`, `prefer`, or `require` |
| `--cert-file` | SSL certificate file path |
| `--key-file` | SSL private key file path |
| `--ca-file` | SSL CA certificate file path |
| `--max-connections` | Maximum concurrent connections |
| `--connection-timeout` | Connection timeout in seconds (default `30`) |
| `--enable-logging` | Enable proxy connection logging |
| `--log-level` | Log level: `debug`, `info`, `warn`, or `error` |
| `--show-stats` | Display proxy statistics and connection information |

The `database proxy status` subcommand accepts the same flags as `database proxy`.

---

### `orclT database recovery verify`

| Flag | Description |
|------|-------------|
| `--control-file` | Path to the control file to verify |

---

### `orclT database segment`

| Flag | Short | Description |
|------|-------|-------------|
| `--compression-analysis` | `-e` | Analyze compression ratio for segments |
| `--schema` | `-s` | Schema name |
| `--table` | `-t` | Table name |
| `--column` | `-c` | Column name |
| `--all-non-oracle-maintained` | `-a` | Include all non-Oracle maintained schemas |
| `--parallel` | `-P` | Degree of parallelism (default `1`) |
| `--scratch-tablespace` | `-S` | Scratch tablespace (default `USERS`) |
| `--report-file` | `-r` | Output Excel file name |

---

## `orclT mos`

| Flag | Description |
|------|-------------|
| `--mosuser` | My Oracle Support username |
| `--mospass` | My Oracle Support password |

### `orclT mos upload`

| Flag | Short | Description |
|------|-------|-------------|
| `--delete-mos-credentials` | | Delete MOS credentials from the keystore |
| `--file` | `-f` | Path to the file to upload |
| `--sr` | `-s` | Service Request ID to associate with the upload |
| `--rename-uploaded-file` | `-r` | Rename the uploaded file |

---

## `orclT patch download`

| Flag | Description |
|------|-------------|
| `--mosuser` | My Oracle Support username |
| `--mospass` | My Oracle Support password |
| `--delete-mos-credentials` | Delete MOS credentials from the keystore |
| `--patchid` | Comma-separated list of patch numbers |
| `--platform` | Comma-separated list of platform identifiers |
| `--regexp` | Regular expression filter for patch filenames |
| `--target-dir` | Download destination directory |
| `--create-directory-tree` | Create directory tree (`BUNDLE`, `ONEOFF`, `TOOLS`) |
| `--version` | Oracle version (downloads latest RU for that version) |
| `--release` | Oracle release (e.g. `19.25`) |
| `--include-ahf` | Include Autonomous Health Framework |
| `--include-opatch` | Include OPatch |
| `--include-cvu` | Include Cluster Verification Utility |
| `--include-rda` | Include Remote Diagnostic Agent |
| `--include-autoupgrade` | Include AutoUpgrade |
| `--include-apex` | Include Oracle APEX |
| `--include-apex-bundle` | Include APEX bundle patches |
| `--include-oeda` | Include Oracle Exadata Deployment Assistant |
| `--include-patchmgr` | Include Exadata Patch Manager |
| `--include-all-tools` | Include all available tooling bundles |
| `--include-exadata-tools` | Include Exadata-specific tools |
| `--include-gold-images` | Include Oracle Gold Images |
| `--exclude-ru` | Exclude Release Updates |
| `--recommended` | Download recommended patches (MOS 555.1 / 888.1) |
| `--just-list` | List matching patches without downloading |
| `--list-platforms` | List platforms supported by the query |
| `--force` | Overwrite existing files |
| `--online` | Run in online mode |
| `--parallel` | Number of concurrent downloads (`0` = auto) |
| `--chunksize` | Download chunk size in KB (default `8192`) |
| `--download-timeout` | Download timeout per patch in seconds (default `600`) |

---

## `orclT patch goldimage`

| Flag | Description |
|------|-------------|
| `--mosuser` | My Oracle Support username |
| `--mospass` | My Oracle Support password |
| `--patchid` | Comma-separated list of patch numbers |
| `--platform` | Comma-separated list of platform identifiers |
| `--regexp` | Regular expression filter for patch filenames |
| `--targetdir` | Download destination directory |
| `--version` | Oracle version |
| `--release` | Oracle release |
| `--include-ahf` | Include Autonomous Health Framework |
| `--include-opatch` | Include OPatch |
| `--include-autoupgrade` | Include AutoUpgrade |
| `--include-cvu` | Include Cluster Verification Utility |
| `--include-all-tools` | Include all tooling bundles |
| `--include-gold-images` | Include Oracle Gold Images |
| `--exclude-ru` | Exclude Release Updates |
| `--recommended` | Download recommended patches (MOS 555.1 / 888.1) |
| `--justlist` | List matching patches without downloading |
| `--list-platforms` | List platforms supported by the query |
| `--force` | Overwrite existing files |
| `--parallel` | Enable parallel downloads |
| `--parallel-limit` | Limit parallel downloads (default `4`) |
| `--chunksize` | Download chunk size in KB (default `8192`) |

---

## `orclT ssh`

| Flag | Type | Default | Description |
|------|------|---------|-------------|
| `--config-file` | string | | Path to JSON tunnel configuration file |
| `--ssh-host` | string | | SSH server hostname or IP address |
| `--ssh-port` | int | `22` | SSH server port |
| `--ssh-user` | string | | SSH username |
| `--ssh-password` | string | | SSH password |
| `--use-keyfile` | bool | `false` | Authenticate with an SSH key file |
| `--keyfile` | string | `~/.ssh/id_rsa` | Path to SSH private key |
| `--keypass` | string | | SSH key passphrase |
| `--compression` | bool | `false` | Enable SSH compression |
| `--local-bind` | string | `127.0.0.1` | Local address to bind to |
| `--local-port` | int | | Local port for the tunnel |
| `--target-host` | string | | Target host (as seen from SSH server) |
| `--target-port` | int | | Target port |
| `--connection-timeout` | int | `10` | Connection timeout in seconds |
| `--max-connections` | int | `100` | Maximum concurrent connections |
| `--keep-alive-interval` | int | `30` | Keep-alive interval in seconds |
| `--keep-alive-count` | int | `3` | Keep-alive retry count before timeout |
| `--enable-logging` | string | | Enable debug logging (optional output filename) |
| `--log-level` | string | `info` | Log level: `debug`, `info`, `warn`, or `error` |
| `--show-ping` | bool | `false` | Display SSH and target ICMP latency |
| `--show-details` | bool | `false` | Show detailed connection info in TUI info pane |
| `--show-closed` | bool | `false` | Show closed connections in TUI (toggle with `c`) |
| `--save-known-host` | bool | `true` | Save SSH host key to known_hosts |
| `--ignore-host-key` | bool | `false` | Skip SSH host key verification |
| `--no-ui` | bool | `false` | Run in text mode without TUI |
| `--daemonize` | bool | `false` | Run in background with logging to file |
| `--create-sample-config` | bool | `false` | Generate a sample config file and exit |
