---
title: "Plan"
description: "Analyze execution plan stability, create SQL baselines, profiles, and patches."
weight: 30
---

# Plan

`orclT database performance plan` provides SQL execution plan analysis and management. It identifies unstable plans, regressed SQL, and implicit type conversions, and can create SQL baselines, profiles, and patches to stabilise performance.

## Sub-commands

| Sub-command | Description |
|-------------|-------------|
| `unstable` | Report SQL statements with multiple cached execution plans |
| `regression` | Report SQL that currently executes slower than its historical best plan |
| `implicit-conversion` | Report SQL statements performing implicit type conversions |

## Unstable Plans

Identifies SQL in the shared pool that has more than one cached execution plan, which often indicates plan instability or cardinality issues.

```bash
orclT database performance plan unstable \
  -u <user> -p <password> -d <host>:<port>/<service> \
  --report-file plan_unstable.xlsx
```

## Plan Regression

Compares currently executing plans against AWR-stored historical best plans.

```bash
orclT database performance plan regression \
  -u <user> -p <password> -d <host>:<port>/<service> \
  --min-factor 1.5 \
  --min-seconds 5 \
  --report-file plan_regression.xlsx
```

### Regression Flags

| Flag | Description |
|------|-------------|
| `--limit` | Maximum rows to return (0 = unlimited) |
| `--min-factor` | Minimum slowdown factor to include (e.g. `1.5` = 50% slower) |
| `--min-seconds` | Minimum elapsed time delta in seconds |
| `--include-improved` | Also include SQL statements that have improved |

## SQL Plan Management

Use the `plan` command to create SQL baselines, profiles, or patches for specific SQL IDs:

```bash
orclT database performance plan \
  -u <user> -p <password> -d <host>:<port>/<service> \
  --sql-id-analysis \
  --sql-id <sql_id> \
  --create-sql-baseline \
  --fixed
```

### Plan Management Flags

| Flag | Description |
|------|-------------|
| `--sql-id` | Target SQL ID |
| `--plan-hash-value` | Specific plan hash value to use |
| `--create-sql-baseline` | Create a SQL Plan Baseline |
| `--fixed` | Mark the SQL baseline as fixed |
| `--disabled` | Create the baseline as disabled |
| `--create-sql-profile` | Create a SQL Profile |
| `--sql-profile-name` | Name for the SQL profile |
| `--sql-profile-category` | SQL profile category (default `DEFAULT`) |
| `--sql-profile-force-match` | Enable `FORCE MATCHING` |
| `--sql-profile-replace` | Replace an existing profile |
| `--create-sql-patch` | Create a SQL Patch |
| `--hint` | Hint text to embed in the SQL patch |
| `--show-plan-info` | Display detailed plan information |
| `--show-plan-outline` | Display the plan outline |
