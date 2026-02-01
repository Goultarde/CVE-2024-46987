# CVE-2024-46987 - Camaleon CMS Authenticated Arbitrary File Read

This repository contains a Proof of Concept (PoC) script for **CVE-2024-46987**, which allows for arbitrary file reading (LFI / Path Traversal) on **Camaleon CMS**.

## Description

A Path Traversal vulnerability has been identified in Camaleon CMS versions 2.8.0 to < 2.8.2 (strangely work on 2.9.0 too). It is located in the `download_private_file` method of the `MediaController`.

This vulnerability allows an **authenticated** user to download arbitrary files from the server by manipulating the `file` parameter. If the application runs with elevated privileges or if sensitive files are accessible to the system user running the CMS, this can lead to critical information leakage (configuration files, source code, etc.).

**Technical Details:**
- **CVE ID**: CVE-2024-46987
- **CVSS Score**: 7.7 (High)
- **Type**: Authenticated Path Traversal / Arbitrary File Read
- **Affected Versions**: 2.8.0 <= version < 2.8.2

## Prerequisites

- Python 3.x
- `requests`

You can install the dependencies with the following command:

```bash
pip install requests
```

## Usage

The script requires a valid user account on the target CMS to authenticate and retrieve the CSRF token needed for exploitation.

```bash
python3 CVE-2024-46987.py -u <URL> -l <USERNAME> -p <PASSWORD> <FILE_TO_READ>
```

### Arguments

- `-u`, `--url`: Base URL of the target site (e.g., `http://example.com`).
- `-l`, `--user`: Username for authentication.
- `-p`, `--password`: Password for authentication.
- `--path`: (Optional) Path to the vulnerable endpoint. Default: `admin/media/download_private_file`.
- `-v`, `--verbose`: Enable verbose mode to see connection steps.
- `file`: The path of the file to read on the server (e.g., `/etc/passwd`).

### Examples

Read the `/etc/passwd` file:

```bash
python3 CVE-2024-46987.py -u http://target-cms.local -l admin -p password123 /etc/passwd
```

Use verbose mode:

```bash
python3 CVE-2024-46987.py -u http://target-cms.local -l user -p pass -v /etc/hosts
```

## Disclaimer

This code is provided for **educational and security research purposes only**. Using this script against targets without prior authorization is illegal. The author disclaims any responsibility for misuse.

Always ensure you have explicit permission before conducting penetration tests.
# CVE-2024-46987
