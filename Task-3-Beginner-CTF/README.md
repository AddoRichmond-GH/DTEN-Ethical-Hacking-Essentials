# Task 3: Beginner CTF Write-Up

## Overview

As part of the Daryl Tech & Educational Network (DTEN) Ethical Hacking Essentials internship, I completed a beginner-level Capture The Flag (CTF) challenge on TryHackMe.

The objective of the challenge was to perform basic reconnaissance and web application enumeration against an intentionally vulnerable laboratory environment, identify exposed functionality, and use the information discovered during enumeration to answer the challenge questions.

All activities were performed within the authorized TryHackMe laboratory environment.

---

## Platform

**Platform:** TryHackMe
**Room:** Getting Started
**Target:** BFFs Web Application
**Target IP:** `10.129.149.198`
**Testing Environment:** TryHackMe AttackBox

---

## Objectives

The main objectives of this CTF exercise were to:

* Perform basic network reconnaissance.
* Identify running services and technologies.
* Enumerate the target web application.
* Inspect HTML source code for useful information.
* Identify hidden or exposed application functionality.
* Investigate an exposed administrative interface.
* Identify information about the application's administrator and registered users.
* Answer the challenge questions using information discovered during enumeration.

---

## Tools Used

* Nmap
* Web Browser
* HTML Source Inspection
* TryHackMe AttackBox

---

# 1. Network Reconnaissance

The first step was to perform a service and version scan against the target machine.

The following Nmap command was used:

```bash
nmap -sC -sV 10.129.149.198
```

### Results

The scan identified the following open ports:

| Port     | Service | Information                       |
| -------- | ------- | --------------------------------- |
| 22/tcp   | SSH     | OpenSSH 8.2p1                     |
| 80/tcp   | HTTP    | Node.js / Express web application |
| 3000/tcp | HTTP    | Node.js / Express web application |

The web application was identified as **BFFs**.

The Nmap results provided the initial attack surface for further enumeration.

---

# 2. Web Application Enumeration

After identifying the HTTP services, the BFFs web application was accessed through the browser.

The application presented a login portal requiring a username and password.

Initial testing with invalid credentials confirmed that the application was processing login requests and returning an authentication failure message when incorrect credentials were supplied.

---

# 3. HTML Source Code Analysis

The HTML source code of the BFFs login page was inspected to identify potentially exposed information.

During the inspection, the following comment was discovered:

```html
<!-- don't forget to remove admin page on /test-admin -->
```

This revealed the existence of an administrative page at:

```text
/test-admin
```

This was an important enumeration finding because the administrative functionality appeared to remain accessible through the web application.

### Finding

**Exposed Administrative Endpoint**

The application source code disclosed the location of an administrative page that appeared to be intended for removal before production deployment.

---

# 4. Administrative Page Enumeration

The discovered endpoint was accessed through the browser:

```text
http://10.129.149.198/test-admin
```

The page displayed an administrative interface intended for managing users before the application went into production.

Further investigation of the page revealed information about the administrator and the users registered on the portal.

---

# 5. Administrator Identification

The administrative interface identified the administrator as:

**John Doe**

This information was used to answer one of the challenge questions.

---

# 6. Registered User Enumeration

The administrative interface also displayed the users registered on the portal.

The total number of registered users identified was:

**3 users**

This information was used to correctly answer another challenge question.

---

# 7. Challenge Questions

The information discovered during reconnaissance and web enumeration was used to answer the TryHackMe challenge questions.

Successfully identified information included:

| Question                       | Finding       |
| ------------------------------ | ------------- |
| What is the secret admin page? | `/test-admin` |
| Who is the administrator?      | John Doe      |
| How many users are registered? | 3             |

The answers were submitted successfully within the TryHackMe room.

---

# 8. Evidence

Screenshots were captured throughout the investigation to document the methodology and findings.

The evidence includes:

1. Nmap service enumeration results.
2. BFFs login page.
3. HTML source code revealing the `/test-admin` endpoint.
4. Exposed administrative page.
5. Administrator information.
6. Registered user information.

Screenshots are available in the `screenshots` directory accompanying this write-up.

---

# 9. Key Findings

The exercise demonstrated several important security issues and enumeration techniques:

### Information Disclosure

Sensitive application information was exposed through HTML source code. The source contained a comment revealing the location of an administrative endpoint.

### Exposed Administrative Functionality

The `/test-admin` endpoint remained accessible even though the page indicated that it was intended for pre-production use.

### User Information Exposure

The administrative interface exposed information about registered users.

### Excessive Information Exposure

Application functionality and administrative information that should normally be restricted or removed before deployment were accessible through the web interface.

---

# 10. Security Recommendations

The following measures could help prevent similar issues in a production environment:

* Remove development and testing endpoints before deploying applications to production.
* Avoid leaving sensitive information in HTML comments or client-side source code.
* Implement strong authentication and authorization controls for administrative functionality.
* Restrict administrative interfaces to authorized users.
* Minimize the amount of user information displayed through administrative interfaces.
* Perform security testing before production deployment.
* Conduct regular web application vulnerability assessments.
* Review application source code for accidentally exposed development functionality.

---

# 11. Skills Demonstrated

This CTF exercise helped demonstrate practical skills in:

* Network reconnaissance
* Nmap scanning
* Service enumeration
* Web application enumeration
* HTML source-code analysis
* Information disclosure identification
* Administrative endpoint discovery
* Basic authentication testing
* Security documentation
* Capture The Flag methodology

---

# 12. Lessons Learned

The exercise demonstrated that useful security information can sometimes be discovered without immediately attempting complex exploitation.

A simple combination of network scanning, application enumeration, and source-code inspection was sufficient to discover an administrative endpoint and obtain information required to complete the challenge.

The exercise also reinforced the importance of removing development functionality and sensitive information before deploying an application to a production environment.

---

## Conclusion

The TryHackMe Getting Started CTF provided practical experience with the early stages of a web application security assessment.

Through Nmap reconnaissance, web application enumeration, and HTML source-code inspection, I identified the BFFs application, discovered the hidden `/test-admin` administrative endpoint, identified the administrator, and determined the number of registered users.

The challenge strengthened my understanding of reconnaissance, information disclosure, web application enumeration, and the importance of secure application deployment practices.

All testing was conducted within the authorized TryHackMe laboratory environment as part of the DTEN Ethical Hacking Essentials internship.
