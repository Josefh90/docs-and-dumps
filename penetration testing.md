# Penetration Testing

This document serves as a concise overview of ethical hacking, rules of engagement, penetration testing stages, and widely recognized methodologies. It is ideal for those learning cybersecurity fundamentals or working on penetration testing engagements.

## Table of Contents

* [1.0 Introduction to Pentesting](#10-introduction-to-pentesting)

  * [1.1 Hacker Categories](#11-summary-of-hacker-categories)
  * [1.2 Rules of Engagement (ROE)](#12-rules-of-engagement-roe)
  * [1.3 Stages of Penetration Testing](#13-stages-of-penetration-testing)
  * [1.4 Testing Approaches](#14-testing-approaches)
  * [1.5 Overview of Methodologies](#15-overview-of-methodologies)

    * [OSSTMM](#osstmm)
    * [OWASP](#owasp)
    * [NIST Cybersecurity Framework 1.1](#nist-cybersecurity-framework-11)
    * [CSC CAF](#csc-caf)

* [2.0 Principles of Security](#20-principles-of-security)

  * [2.1 Defence in Depth](#21-defence-in-depth)
  * [2.2 CIA Triad](#22-cia-triad)

    * [Confidentiality](#confidentiality)
    * [Integrity](#integrity)
    * [Availability](#availability)

* [3.0 Subdomain Enumeration Methods](#30-subdomain-enumeration-methods)

  * [3.1 Certificate Transparency Logs](#31-certificate-transparency-logs)
  * [3.2 Discovering Subdomains with Search Engines](#32-discovering-subdomains-with-search-engines)
  * [3.3 DNS Bruteforce with Tools](#33-dns-bruteforce-with-tools)
  * [3.4 Automated Enumeration with Sublist3r](#34-automated-enumeration-with-sublist3r)
  * [3.5 Virtual Hosts (vHosts) & Host Header Manipulation](#35-virtual-hosts-vhosts--host-header-manipulation)
  * [3.6 Summary](#36-summary)

---

## 1.0 Introduction to Pentesting

### 1.1 Summary of Hacker Categories

| Category      | Description                                                               | Example                                                          |
| ------------- | ------------------------------------------------------------------------- | ---------------------------------------------------------------- |
| **White Hat** | Ethical hackers who work within the law to improve cybersecurity.         | Penetration tester conducting an authorized security assessment. |
| **Grey Hat**  | Hackers who often help others but may bypass legal or ethical boundaries. | Taking down a scam website without authorization.                |
| **Black Hat** | Malicious hackers focused on financial gain or causing harm.              | Ransomware developers encrypting files and demanding payment.    |

### 1.2 Rules of Engagement (ROE)

Before any penetration testing begins, a **Rules of Engagement (ROE)** document must be defined. It typically contains:

| Section        | Description                                                                          |
| -------------- | ------------------------------------------------------------------------------------ |
| **Permission** | Legal consent to perform testing activities.                                         |
| **Test Scope** | Specific systems or applications covered in the assessment.                          |
| **Rules**      | Acceptable and restricted testing techniques (e.g., phishing allowed or disallowed). |

### 1.3 Stages of Penetration Testing

| Stage                     | Description                                           |
| ------------------------- | ----------------------------------------------------- |
| **Information Gathering** | Collect publicly available information (e.g., OSINT). |
| **Enumeration/Scanning**  | Identify active systems and services.                 |
| **Exploitation**          | Use discovered vulnerabilities to gain access.        |
| **Privilege Escalation**  | Expand access (horizontal or vertical).               |
| **Post-Exploitation**     | Maintain access, gather data, pivot, and clean up.    |
| **Reporting**             | Document findings and provide mitigation guidance.    |

### 1.4 Testing Approaches

| Type          | Description                                                                            |
| ------------- | -------------------------------------------------------------------------------------- |
| **Black-Box** | No internal knowledge; tests like a user. Longer enumeration time.                     |
| **Grey-Box**  | Partial knowledge; balances time efficiency and coverage.                              |
| **White-Box** | Full access and knowledge; often used by developers. Most thorough but time-consuming. |

### 1.5 Overview of Methodologies

#### OSSTMM

A detailed, flexible testing standard focused on systems, software, and communication.

* ✅ In-depth strategies for telecom and networks
* ⚠️ Complex terminology and learning curve

#### OWASP

Focused on web applications, OWASP is widely used and regularly updated.

* ✅ Simple and beginner-friendly
* ⚠️ No accreditation or deep audit mechanisms

#### NIST Cybersecurity Framework 1.1

A national standard that outlines risk management and security best practices.

* ✅ Widely adopted in the U.S.
* ⚠️ Less practical guidance for pentesting specifics

#### CSC CAF

Designed for critical infrastructure, it provides principle-based risk assessments.

* ✅ Government-backed and accredited
* ⚠️ Less direct than rule-based frameworks

---

## 2.0 Principles of Security

### 2.1 Defence in Depth

**Defence in Depth** refers to the strategic approach of using multiple, diverse security controls throughout an organization’s systems and infrastructure. The goal is to ensure that if one control fails, others still provide protection — offering **redundancy** and **resilience**.

> Example: An organization may implement firewalls, intrusion detection systems, access control mechanisms, encryption, and user training as layers in their security strategy.

#### Benefits

* Reduces single points of failure
* Increases resilience against sophisticated attacks
* Encourages layered architecture and risk mitigation

### 2.2 CIA Triad

The **CIA Triad** is a core model in information security, serving as a foundation for developing security policies and evaluating risk. Originating as early as 1998, its concepts still apply to both digital and non-digital data management — such as filing cabinets and physical records.

| Component           | Description                                                                                      |
| ------------------- | ------------------------------------------------------------------------------------------------ |
| **Confidentiality** | Ensures that information is only accessible to those who have proper authorization.              |
| **Integrity**       | Guarantees that data remains accurate, consistent, and unaltered except by authorized processes. |
| **Availability**    | Ensures that systems and data are accessible when needed by authorized users.                    |

#### Confidentiality

Keeping sensitive information hidden from unauthorized access.

* 🔐 Examples: Encryption, access control lists, two-factor authentication

#### Integrity

Maintaining data accuracy and trustworthiness over its lifecycle.

* 🔄 Examples: Checksums, hashing, audit logs

#### Availability

Ensuring users can reliably access systems and data when required.

* ⚙️ Examples: Load balancing, backup systems, failover mechanisms

---

## 3.0 Subdomain Enumeration Methods

### 3.1 Certificate Transparency Logs

When an SSL/TLS certificate is issued, it is logged publicly in **Certificate Transparency (CT) Logs**. These logs are useful for identifying misused or mistakenly issued certificates and often include subdomains.

* Each certificate entry can reveal subdomains.
* Services like [crt.sh](https://crt.sh/) allow querying these logs.
* Effective for identifying both current and historical subdomains.

### 3.2 Discovering Subdomains with Search Engines

Search engines can be used to find indexed subdomains through advanced search queries:

```text
site:*.domain.com -site:www.domain.com
```

* Reveals indexed subdomains excluding the main domain.
* Useful for discovering publicly accessible subdomains.

### 3.3 DNS Bruteforce with Tools

Some subdomains do not appear in DNS records or search engines. **DNS Bruteforce** uses a wordlist to try possible subdomains:

* Tools like `dnsrecon` automate the process.
* Based on wordlists with common subdomain names.
* Helpful for finding undocumented or internal subdomains.

### 3.4 Automated Enumeration with Sublist3r

**Sublist3r** is a tool that aggregates subdomain data from multiple sources:

* Uses search engines, certificate logs, DNS, etc.
* Fast and efficient for automated reconnaissance.
* Combines passive and active data sources.

### 3.5 Virtual Hosts (vHosts) & Host Header Manipulation

Some subdomains are not resolvable via DNS but are configured as virtual hosts on a web server.

* Virtual hosts are selected based on the `Host` HTTP header.
* Tools like `ffuf` can be used to fuzz possible subdomains using the header:

```bash
ffuf -w wordlist.txt \
     -H "Host: FUZZ.targetdomain.tld" \
     -u http://IP_ADDRESS \
     -fs {page_size}
```

* `-fs` filters out default-sized responses (e.g., error pages).
* Reveals hidden services or staging environments.

### 3.6 Summary

| Method                   | Benefit                                 | Use Case                             |
| ------------------------ | --------------------------------------- | ------------------------------------ |
| Certificate Transparency | Reveals historical & current subdomains | Passive enumeration                  |
| Google Search            | Fast discovery of indexed subdomains    | Passive reconnaissance               |
| DNS Bruteforce           | Discovers undocumented subdomains       | Active enumeration                   |
| Sublist3r                | Combines many sources                   | Automated & broad enumeration        |
| Host Header Fuzzing      | Detects hidden virtual hosts            | Identifying internal/staging systems |
