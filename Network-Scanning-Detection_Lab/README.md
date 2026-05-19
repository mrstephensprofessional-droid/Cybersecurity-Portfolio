# Host-Based Port Scan Identification & Analysis via Splunk

## Overview
Built a defensive security monitoring lab using Kali Linux, Windows Server 2025, and Splunk Enterprise to simulate internal network reconnaissance and analyze target telemetry. Investigated an offensive visibility gap regarding default host-based firewall configurations, implemented advanced auditing commands to capture connection states, and engineered structural SIEM dashboard metrics to aggregate and isolate port scan patterns.

## Lab Environment
* **Hypervisor:** VirtualBox
* **Server OS:** Windows Server 2025 Standard
* **Attacker OS:** Kali Linux (Rolling Edition)
* **Network Type:**
  * Internal Network (Isolated target framework)
  * NAT Adapter (External access for package maintenance)

## Objectives
* Validate multi-homed interface configurations on an offensive workspace.
* Perform stealth active host discovery across a private subnet block.
* Conduct high-fidelity service version and operating system fingerprinting.
* Diagnose telemetry blind spots within default Windows Security logging configurations.
* Leverage command-line administration tools to manipulate advanced system audit policies.
* Ingest, parse, and visualize hostile connection spikes using Splunk SPL metrics.

## Network Configuration

### Domain Controller
* **Static IP:** 192.168.10.10
* **DNS:** 192.168.10.10
* **Domain:** Stephenslab.com

### Attacker Instance
* **Interface eth0:** NAT Network (DHCP allocated)
* **Interface eth1:** 192.168.10.100
* **Subnet Mask:** 255.255.255.0

### SIEM Configuration
* **Platform:** Splunk Enterprise
* **Deployment:** Hosted locally on Windows Server 2025
* **Purpose:** High-volume host-based firewall logging and ingestion configuration

## Steps Completed
1. Verified operational internal network interface bindings on the Kali Linux machine using `ifconfig`.
2. Executed a local network ping sweep (`nmap -sn`) to map live infrastructure assets on the private subnet.
3. Identified the active Windows Server instance target sitting at static IP address `192.168.10.10`.
4. Discovered an initial telemetry gap where aggressive scans generated zero events inside the SIEM dashboard due to restrictive default OS parameters.
5. Opened an Administrative Command Prompt on the target machine to modify structural event logging boundaries.
6. Configured advanced local host policy variables using `auditpol` strings to force explicit telemetry tracking for network connections and packet drops.
7. Conducted a deep-probing version detection and operating system fingerprinting scan (`nmap -sV -O`) against the Domain Controller.
8. Parsed out critical exposed infrastructure endpoints from the attack surface map including Kerberos, LDAP, SMB, and MSRPC.
9. Pivoted to the Splunk Enterprise Search console to isolate attacker actions filtering by the malicious source IP address (`192.168.10.100`).
10. Engineered an analytical aggregation query using Search Processing Language (SPL) to transform raw logs into a structured visual dashboard panel.

## Group Policy / Policy Example
Modified advanced system auditing tracking parameters using direct command strings to dynamically update the active security parameters:

```cmd
C:\Users\Administrator>auditpol /set /subcategory:"Filtering Platform Connection" /success:enable /failure:enable
The command was successfully executed.

C:\Users\Administrator>auditpol /set /subcategory:"Filtering Platform Packet Drop" /success:enable /failure:enable
The command was successfully executed.
