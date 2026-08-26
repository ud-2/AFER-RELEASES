# A-FER

**High-Performance Entity Resolution & Record Linkage Engine**

[![Release](https://img.shields.io/github/v/release/ud-2/AFER-RELEASES?color=blue\&label=Release)](https://github.com/ud-2/AFER-RELEASES/releases)
[![Platform](https://img.shields.io/badge/Platform-Linux%20x86__64-brightgreen.svg)](https://github.com/ud-2/AFER-RELEASES/releases)
[![Language](https://img.shields.io/badge/Language-Rust-orange.svg)](https://www.rust-lang.org/)
[![Edition](https://img.shields.io/badge/Edition-Community-blue.svg)](https://github.com/ud-2/AFER-RELEASES/releases)

A-FER (*Adaptive Fast Entity Resolution*) is a high-performance record linkage engine built in Rust for deterministic entity resolution and cross-dataset matching.

It is designed to identify corresponding records across datasets despite common variations such as spelling differences, formatting inconsistencies, and noisy input data.

## Key Highlights

* **High Performance.** Efficient local processing designed for high-throughput entity matching.
* **Robust Matching.** Designed to handle spelling variations, formatting differences, and noisy records.
* **Deterministic.** Produces consistent results for the same input and configuration.
* **Privacy-First.** Runs entirely on-premise with no external API calls or cloud data transfer.
* **Self-Contained Binary.** Distributed as a statically linked Linux binary with no external runtime dependencies.
* **Configurable.** Matching behavior can be adjusted through command-line parameters.
* **Lightweight.** Designed for efficient deployment on standard Linux environments.

## Current Release

- **Version:** `v0.1.0`
- **Platform:** Linux x86_64
- **Architecture:** x86_64 / amd64
- **Runtime:** Self-contained static binary

This release provides the **Community Edition** of A-FER for local CSV-based entity resolution.

## Quick Start

### 1. Download

Download the latest release:

```bash
curl -LO https://github.com/ud-2/AFER-RELEASES/releases/download/v0.1.0/afer-linux-x86_64.tar.gz
curl -LO https://github.com/ud-2/AFER-RELEASES/releases/download/v0.1.0/afer-linux-x86_64.tar.gz.sha256
```

### 2. Verify Integrity

Always verify the downloaded archive before execution:

```bash
sha256sum -c afer-linux-x86_64.tar.gz.sha256
```

Expected result:

```text
afer-linux-x86_64.tar.gz: OK
```

### 3. Extract

```bash
tar -xzf afer-linux-x86_64.tar.gz
chmod +x afer-linux-x86_64
```

Verify the installation:

```bash
./afer-linux-x86_64 --version
```

For available options:

```bash
./afer-linux-x86_64 --help
```

## Running A-FER

A-FER processes a reference dataset and a query dataset, then writes the resolved matches to an output CSV file.

```bash
./afer-linux-x86_64 \
  --master path/to/master.csv \
  --query path/to/queries.csv \
  --output path/to/matches.csv \
  --name-cols <column1>,<column2>,...,<columnN>
```

### Example

```bash
./afer-linux-x86_64 \
  --master data/master.csv \
  --query data/queries.csv \
  --output data/matches.csv \
  --name-cols lastname,firstname
```

## Input Format

A-FER currently accepts **semicolon-delimited CSV files**.

Both the reference and query datasets must contain a unique `id` column used as the primary key.

The `--name-cols` parameter accepts a comma-separated list of column names to use for entity matching.

### Reference Dataset

```csv
id;lastname;firstname
M001;KAMDEM;Eric
M002;FOTSO;Jean-Pierre
M003;MAKEME;Dominique
```

### Query Dataset

```csv
id;lastname;firstname
Q101;KANDEM;Erick
Q102;MAKKEME;Dominik
```

The examples illustrate the type of variations A-FER is designed to handle during entity resolution.

## Output Format

A-FER generates a structured CSV containing the resolved entities and matching information.

| Column       | Description                                          |
| ------------ | ---------------------------------------------------- |
| `query_id`   | Identifier from the query dataset                    |
| `master_id`  | Identifier of the matched reference entity           |
| `score`      | Overall matching score                               |

Example:

```csv
query_id;master_id;score
Q101;M001;0.90
Q102;M003;0.90
```

## CLI Reference

```text
Usage: afer-linux-x86_64 [OPTIONS] --master <MASTER> --query <QUERY> --output <OUTPUT> --name-cols <NAME_COLS>

Options:
      --master <MASTER>
          Path to the reference dataset

      --query <QUERY>
          Path to the query dataset

      --output <OUTPUT>
          Path for the generated matches

      --name-cols <NAME_COLS>
          Comma-separated list of columns used for matching

  -h, --help
          Print help

  -V, --version
          Print version
```

For the complete list of available options and their current defaults:

```bash
./afer-linux-x86_64 --help
```

## Community Edition Limits

The `v0.1.0` Community Edition is intended for evaluation, development, prototyping, and small-scale deployments.

| Resource          | Community Edition |
| ----------------- | ----------------: |
| Reference records |   Up to **1,000** |
| Query records     |     Up to **500** |
| Input             |               CSV |
| Output            |               CSV |
| Execution         |             Local |
| External services |              None |

These limits are specific to the Community Edition and may differ from commercial deployments.

## Privacy & Security

A-FER is designed for environments where sensitive records should remain under the operator's control.

The standalone binary:

* Runs locally
* Does not require an internet connection
* Does not send records to external APIs
* Does not require a cloud service
* Does not include telemetry by default

Input datasets remain within the execution environment.

## Platform Support

### Current Release

| Platform | Architecture   | Status    |
| -------- | -------------- | --------- |
| Linux    | x86_64 / amd64 | Supported |

The distributed binary is statically linked and designed for broad compatibility across Linux environments.

Additional platforms may be provided in future releases.

## Release Verification

Each binary release includes a SHA-256 checksum.

Verify the downloaded archive with:

```bash
sha256sum -c afer-linux-x86_64.tar.gz.sha256
```

Only execute the binary after confirming that the checksum matches.

## Licensing

A-FER Community Edition is distributed under the licensing terms included with the release.

See the accompanying `LICENSE` file for the applicable terms.

Commercial and enterprise licensing is handled separately.

## Releases

Official binary releases are published through the A-FER Releases repository:

[https://github.com/ud-2/AFER-RELEASES/releases](https://github.com/ud-2/AFER-RELEASES/releases)

Each release contains the corresponding versioned binary artifacts and integrity checksums.

## Commercial & Enterprise

An Enterprise Edition of A-FER is currently in development and will be available in a future release.

The Enterprise Edition will target organizations requiring larger-scale processing, private deployments, custom integrations, and advanced enterprise capabilities.

**Enterprise availability and pricing will be announced separately.**

## Author

**VUIDE OUENDEU FRANCK JORDAN**

Software Engineer  
`ouendeufranck@gmail.com` | `github.com/ud-2`