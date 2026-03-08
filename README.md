 Gemini said
1shot.sh: Automated Reconnaissance Framework

A streamlined, single-entry bash script designed for security researchers to automate the initial discovery and vulnerability assessment phases. This tool chains the ProjectDiscovery ecosystem to transform a single target into a comprehensive attack surface map.
🚀 Overview

1shot.sh automates a multi-stage reconnaissance pipeline. It handles everything from workspace organization and asset discovery to deep crawling and vulnerability scanning in one execution.
Key Features

    Intelligent Input Handling: Automatically detects whether the input is an IP address or a domain name and adjusts the discovery logic accordingly.

    Automated Workspace Management: Creates time-stamped directories (e.g., recon_example.com_2026-03-08) to ensure data persistence and organization.

    Pre-flight Safety Checks: Includes logic to verify that the Go-based httpx is being used rather than the Python library, preventing common environment pathing errors.

    Integrated Pipeline: Seamlessly passes data between Subfinder, Naabu, httpx, Katana, and Nuclei.

🛠 Workflow Pipeline

The script executes the following stages in sequence:
Stage	Tool	Description
1. Discovery	Subfinder	Performs passive subdomain enumeration for domains.
2. Port Scanning	Naabu	Scans identified assets for open ports at a high rate (1000 pps).
3. Web Probing	httpx	Fingerprints web services, identifying technologies and status codes.
4. Crawling	Katana	Spiders live URLs to find hidden endpoints and JavaScript files.
5. Vuln Scan	Nuclei	Runs template-based scans (Low to Critical) against all endpoints.
📋 Prerequisites

You must have the following ProjectDiscovery tools installed and available in your $PATH:

    subfinder

    naabu

    httpx

    katana

    nuclei

    jq (for JSON processing)

💻 Usage

    Clone or copy the script:
    Bash

    chmod +x 1shot.sh

    Run against a domain:
    Bash

    ./1shot.sh example.com

    Run against an IP:
    Bash

    ./1shot.sh 1.1.1.1

📂 Output Artifacts

The script generates a summary report in the terminal and saves all raw data in the generated workspace folder:

    targets.txt: List of all identified subdomains or IPs.

    open_ports.txt: List of assets with active open ports.

    web_assets.json: Full technical fingerprinting of web services.

    crawled_endpoints.txt: A comprehensive list of URLs found via spidering.

    vulnerabilities.json: Identified security flaws categorized by severity.
