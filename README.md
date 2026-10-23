# CyberLab — Network Vulnerability Assessment

## Project Overview

This project documents a hands-on network security assessment conducted in an isolated virtual laboratory.

The objective was to develop practical cybersecurity skills by configuring a controlled testing environment, discovering network services, identifying security weaknesses, validating vulnerabilities, and documenting findings using professional reporting practices.

## Lab Environment

| Component | Configuration |
|---|---|
| Virtualisation | Oracle VirtualBox |
| Assessment Machine | Parrot OS 6.4 Security Edition |
| Target Machine | Metasploitable 2 |
| Network Type | Internal Network (CyberLab) |
| Assessment IP | 192.168.56.10 |
| Target IP | 192.168.56.20 |

Both virtual machines were configured to communicate through an isolated VirtualBox internal network.

## Assessment Scope

All testing was performed against Metasploitable 2, a deliberately vulnerable training machine.

No public networks, production systems, or unauthorised third-party infrastructure were assessed.

## Assessment Methodology

The assessment followed a structured process:

1. Lab configuration: Configured Parrot OS and Metasploitable 2 on an isolated VirtualBox internal network.
2. Connectivity verification: Confirmed communication between the assessment machine and the target using ICMP ping.
3. Service enumeration: Used Nmap to identify open TCP ports, running services and software versions.
4. Security testing: Investigated anonymous FTP access and tested the identified vsFTPd service for a known backdoor vulnerability.
5. Vulnerability validation: Used the Nmap Scripting Engine to validate CVE-2011-2523. The script reported successful execution of the `id` command with root privileges.
6. Documentation: Preserved scan outputs and prepared a structured vulnerability finding, including supporting evidence and assessment limitations.

## Key Findings

| Finding | Evidence | Status |
|---|---|---|
| Anonymous FTP access | [FTP anonymous access evidence](scans/ftp-anonymous-test.txt) | Confirmed |
| vsFTPd 2.3.4 backdoor (CVE-2011-2523) | [vsFTPd backdoor scan evidence](scans/ftp-backdoor-check.txt) | Validated through Nmap NSE |

The vsFTPd vulnerability was validated using an automated Nmap script. An independent interactive shell was not established during this assessment.

## Evidence

Raw scan outputs are preserved in the `scans/` directory.

The detailed vulnerability report is available in [Finding 001 — vsFTPd Backdoor](findings/FINDING-001-vsftpd-backdoor.md).
