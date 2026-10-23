# FINDING-001: vsFTPd 2.3.4 Backdoor

Severity: Critical  
CVE: CVE-2011-2523  
Target: Metasploitable 2 — 192.168.56.20  
Affected Port: 21/TCP (FTP)  
Assessment Environment: Isolated VirtualBox CyberLab network

## 1. Executive Summary

A security assessment of the Metasploitable 2 virtual machine identified a backdoored version of the vsFTPd 2.3.4 FTP service.

The vulnerability can allow an unauthenticated attacker to execute commands with root privileges.

During testing, an Nmap vulnerability detection script reported successful execution of the `id` command, returning root privileges.

## 2. Technical Evidence

Service enumeration identified:

- Port: 21/TCP
- Service: FTP
- Version: vsFTPd 2.3.4

The vulnerability scan reported:

```text
VULNERABLE:
vsFTPd version 2.3.4 backdoor
State: VULNERABLE (Exploitable)
CVE: CVE-2011-2523

Exploit results:
Shell command: id
Results: uid=0(root) gid=0(root)
```

## 3. Security Impact

Successful exploitation could allow an attacker to execute arbitrary commands with root privileges.

Potential consequences include complete system compromise, unauthorised access to sensitive files, and modification of system configurations.

## Severity Justification

**Technical Severity: Critical**

The affected FTP service contains a known backdoor that can permit unauthenticated remote command execution with root privileges.

During testing, the Nmap Scripting Engine reported successful execution of the `id` command as root.

A successful attack could result in complete compromise of the affected host.

This rating reflects technical severity. Actual environmental risk is limited by the isolated training environment. No formal CVSS calculation or production exposure assessment was performed.

## 4. Remediation Recommendations

1. Remove the compromised vsFTPd 2.3.4 installation.
2. Replace it with a trusted, supported FTP server version or a secure file-transfer alternative such as SFTP.
3. Restrict network access to file-transfer services.
4. Review system logs and investigate possible unauthorised access.
5. Rebuild affected systems from trusted sources if compromise is suspected.

## 5. Assessment Scope

This finding was identified within a privately controlled, isolated cybersecurity training environment using Parrot OS and Metasploitable 2.

No public or third-party systems were tested.

## 6. Supporting Evidence

The original Nmap scan output is available at:

[FTP Backdoor Verification](../scans/ftp-backdoor-check.txt)

Verification method: Nmap Scripting Engine (NSE)

Script: ftp-vsftpd-backdoor

Observed result: The script reported successful
execution of the `id` command with root privileges.

Assessment limitation: Exploitation was verified
through Nmap's automated script. An independent
interactive shell was not established.
