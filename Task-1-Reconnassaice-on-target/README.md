# Task 1: Reconnaissance & Footprinting Report

## Overview

As part of the Daryl Tech & Educational Network (DTEN) Ethical Hacking Essentials internship, a reconnaissance and service enumeration exercise was conducted against an intentionally configured laboratory environment.

The objective was to identify the target's exposed network services, determine the technologies associated with those services, and document the findings in a structured manner similar to an initial security assessment.

All testing was performed within an authorized laboratory environment.

---

## Objectives

The main objectives of this task were to:

* Perform active reconnaissance against the designated laboratory target.
* Identify open TCP ports.
* Enumerate services running on discovered ports.
* Identify technologies associated with exposed services.
* Determine the web application running on the target.
* Document reconnaissance findings as a security analyst.

---

## Lab Environment

| Component           | Details                         |
| ------------------- | ------------------------------- |
| Security Testing OS | Kali Linux                      |
| Virtualization      | VirtualBox                      |
| Target Environment  | Windows-based laboratory target |
| Web Application     | OWASP Juice Shop                |
| Primary Tool        | Nmap                            |

---

## Reconnaissance Methodology

The assessment followed a basic reconnaissance workflow:

1. Identify the target system.
2. Perform a network scan.
3. Enumerate open ports.
4. Identify running services and versions.
5. Identify the exposed web application.
6. Record and analyze the results.

---

## Nmap Service Enumeration

The target was scanned using Nmap with default scripts and service/version detection:

```bash
nmap -sC -sV <target-ip>
```

The scan identified several exposed services.

### Discovered Services

| Port     | Service / Protocol      | Finding                          |
| -------- | ----------------------- | -------------------------------- |
| 135/tcp  | Microsoft Windows RPC   | RPC service exposed              |
| 139/tcp  | NetBIOS Session Service | NetBIOS service exposed          |
| 445/tcp  | Microsoft SMB           | SMB service exposed              |
| 3000/tcp | HTTP                    | OWASP Juice Shop web application |
| 3306/tcp | MySQL                   | MySQL database service exposed   |

The scan also indicated that the target was running a Windows-based environment.

---

## Web Application Identification

Further investigation of the HTTP service on port 3000 identified the application as:

**OWASP Juice Shop**

OWASP Juice Shop is an intentionally vulnerable web application designed for security training and penetration-testing practice.

The application's presence provided a suitable environment for the subsequent web application security assessment performed in Task 2.

---

## Key Findings

The reconnaissance phase identified several services that contributed to the target's attack surface.

### Windows RPC

Port 135 was identified as an exposed Microsoft Windows RPC service.

### NetBIOS

Port 139 was identified as an exposed NetBIOS session service.

### SMB

Port 445 was identified as an exposed Microsoft SMB service.

### Web Application

Port 3000 exposed an HTTP service hosting OWASP Juice Shop.

### MySQL

Port 3306 exposed a MySQL database service.

---

## Security Observations

The presence of multiple network services increases the overall attack surface of a system.

During a real-world assessment, each exposed service would require further investigation to determine:

* Whether access is necessary.
* Whether authentication is properly configured.
* Whether the service is securely configured.
* Whether the software is up to date.
* Whether known vulnerabilities affect the deployed version.
* Whether network-level access restrictions are in place.

Because this assessment was conducted against an intentionally vulnerable laboratory environment, the discovered services were used for learning and security testing purposes.

---

## Evidence

Screenshots were captured during the reconnaissance process.

The evidence includes:

* Nmap scan results.
* Identified open ports and services.
* OWASP Juice Shop web application.

Screenshots are stored in the `screenshots` directory.

---

## Tools Used

### Nmap

Nmap was used for:

* Host/service discovery.
* Port enumeration.
* Service detection.
* Version identification.
* Basic script-based enumeration.

---

## Skills Demonstrated

This task provided practical experience with:

* Network reconnaissance.
* Port scanning.
* Service enumeration.
* Service/version detection.
* Attack-surface identification.
* Basic network security analysis.
* Security assessment documentation.
* Nmap usage.

---

## Conclusion

The reconnaissance exercise successfully identified the major network services exposed by the laboratory target and established the initial attack surface for further security testing.

The discovery of the OWASP Juice Shop application on port 3000 provided the basis for the vulnerable web application assessment performed in Task 2.

All reconnaissance activities were performed within the authorized DTEN laboratory environment.
