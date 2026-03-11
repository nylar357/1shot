# 1shot.sh: Automated Reconnaissance Framework

![preview](img/headshot.png)

![Bash](https://img.shields.io/badge/Language-Bash-4EAA25?style=flat-square&logo=gnu-bash&logoColor=white)
![ProjectDiscovery](https://img.shields.io/badge/Powered%20By-ProjectDiscovery-0080FF?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-blue.svg?style=flat-square)

A streamlined, single-entry bash script designed for security researchers to automate the initial discovery and vulnerability assessment phases. This tool chains the **ProjectDiscovery** ecosystem to transform a single target into a comprehensive attack surface map.

---

## 📖 Table of Contents
- [Overview](#-overview)
- [Workflow Pipeline](#-workflow-pipeline)
- [Prerequisites](#-prerequisites)
- [Installation](#-installation)
- [Usage](#-usage)
- [Output Artifacts](#-output-artifacts)
- [Disclaimer](#%EF%B8%8F-disclaimer)

---

## 🚀 Overview

`1shot.sh` automates a multi-stage reconnaissance pipeline. It handles everything from workspace organization and asset discovery to deep crawling and vulnerability scanning in one execution.

### Key Features

* **Intelligent Input Handling:** Automatically detects whether the input is an IP address or a domain name and adjusts the discovery logic accordingly.
* **Automated Workspace Management:** Creates time-stamped directories (e.g., `recon_example.com_2026-03-08`) to ensure data persistence and organization.
* **Pre-flight Safety Checks:** Includes logic to verify that the Go-based `httpx` is being used rather than the Python library, preventing common environment pathing errors.
* **Integrated Pipeline:** Seamlessly passes data between Subfinder, Naabu, httpx, Katana, and Nuclei.

---

## 🛠 Workflow Pipeline

The script executes the following stages in sequence:

| Stage | Tool | Description |
| :--- | :--- | :--- |
| **1. Discovery** | `Subfinder` | Performs passive subdomain enumeration for domains. |
| **2. Port Scanning** | `Naabu` | Scans identified assets for open ports at a high rate (1000 pps). |
| **3. Web Probing** | `httpx` | Fingerprints web services, identifying technologies and status codes. |
| **4. Crawling** | `Katana` | Spiders live URLs to find hidden endpoints and JavaScript files. |
| **5. Vuln Scan** | `Nuclei` | Runs template-based scans (Low to Critical) against all endpoints. |

---

## 📋 Prerequisites

You must have the following [ProjectDiscovery](https://projectdiscovery.io/) tools installed and available in your `$PATH`:

* `subfinder`
* `naabu`
* `httpx`
* `katana`
* `nuclei`
* `jq` (Standard command-line JSON processor)

> **Note:** Ensure your ProjectDiscovery tools are updated to their latest versions for the best results and syntax compatibility.

---

## ⚙️ Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/nylar357/1shot.git
   cd 1shot

## 💻 Usage

1. Run the script by providing a single target (Domain or IP).

2. Run against a domain:

```./1shot.sh example.com```

3. Run against an IP address:

```./1shot.sh 1.1.1.1```

---

## 📂 Output Artifacts

The script generates a summary report in the terminal and saves all raw data in the dynamically generated workspace folder (recon_<target>_<date>):

    targets.txt: List of all identified subdomains or IPs.

    open_ports.txt: List of assets with active open ports.

    web_assets.json: Full technical fingerprinting of web services.

    live_urls.txt: Parsed list of live HTTP/HTTPS URLs.

    crawled_endpoints.txt: A comprehensive list of URLs found via spidering.

    final_scan_list.txt: Combined list of base URLs and crawled endpoints.

    vulnerabilities.json: Identified security flaws categorized by severity.

## ⚖️ Disclaimer

This script is intended for authorized security testing, educational, and research purposes only. Always ensure you have explicit permission before scanning any infrastructure that you do not own or operate. The authors are not responsible for any misuse or damage caused by this tool.
