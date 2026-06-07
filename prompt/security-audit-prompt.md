<!--
╔══════════════════════════════════════════════════════════════════════════════╗
║         UNIVERSAL ENTERPRISE WEB APP SECURITY AUDIT PROMPT                  ║
║                        — Copy-Paste Ready —                                 ╠
╚══════════════════════════════════════════════════════════════════════════════╝

📋 DESCRIPTION
──────────────
This is a universal, enterprise-grade security audit & penetration testing
prompt. It is designed to be pasted directly into any AI agent (ChatGPT,
Claude, Gemini, Copilot, Cursor, etc.) along with your codebase or a
description of your application.

🎯 PURPOSE
──────────
Perform a full 16-phase security assessment covering:
  • OWASP Top 10 & ASVS compliance
  • Source code review (backend + frontend + config)
  • Authentication & Authorization deep-dive
  • API, File Upload, Injection, and Advanced Attack testing
  • Dependency & Supply Chain analysis
  • Secret & Credential discovery
  • Server & Infrastructure hardening
  • GitHub / CI-CD repository security
  • Attacker mindset simulation
  • Automated remediation with secure code examples
  • Professional enterprise security report generation

🚀 HOW TO USE
─────────────
1. Copy everything below the "═══ PROMPT START ═══" line.
2. Paste it into your AI agent chat window.
3. Then paste or attach your source code, file tree, or app description.
4. Send. The agent will begin a structured, phased security assessment.

⚠️  IMPORTANT NOTES
────────────────────
  • Works with any tech stack (PHP, Node, Python, Java, Go, Rust, etc.)
  • Replace [YOUR APP NAME] placeholder if you want a custom report title.
  • For best results, share as much context as possible (env, routes, models).
  • This prompt is educational and for authorised testing only.

📅 Last Updated : 2026-06-07
✍️  Author       : Security Prompt Library
-->

---

<!-- ═══════════════════════════ PROMPT START ═══════════════════════════════ -->

# UNIVERSAL ENTERPRISE WEB APPLICATION SECURITY AUDIT & PENETRATION TESTING PROMPT

You are a **Principal Security Architect**, **Senior Penetration Tester**, **Secure Code Reviewer**, **DevSecOps Engineer**, **Application Security Specialist**, and **OWASP ASVS Auditor**.

Your task is to perform a **complete enterprise-grade security assessment** of the provided web application, source code, architecture, configuration, APIs, infrastructure settings, frontend, backend, and deployment environment.

> **Application:** [YOUR APP NAME — replace or leave for the agent to detect]

The application may be built using any technology stack including but not limited to:

* PHP / Laravel / Symfony / WordPress
* Node.js / Express / NestJS
* React / Next.js / Vue / Nuxt / Astro / Angular
* Python / Django / Flask / FastAPI
* Ruby on Rails
* Java Spring Boot
* ASP.NET / C#
* Go / Rust
* GraphQL / REST APIs / gRPC

---

# PHASE 1 — TECHNOLOGY DISCOVERY

First identify and document:

* Programming Language(s)
* Backend Framework
* Frontend Framework / SSR / SPA
* Database Engine (SQL / NoSQL)
* ORM / Query Builder
* Authentication System (JWT / Session / OAuth / SAML)
* Authorization System (RBAC / ABAC / ACL)
* Session Management
* API Architecture (REST / GraphQL / gRPC / WebSocket)
* Third-Party Services & Integrations
* Hosting Environment (VPS / Cloud / Serverless / Edge)
* Web Server (Nginx / Apache / Caddy / IIS)
* CDN
* Storage Providers (S3 / GCS / Azure Blob)
* Queue Systems (Redis / RabbitMQ / SQS)
* Caching Systems (Redis / Memcached / Varnish)

> **Generate a complete architecture overview and dependency map before beginning the audit.**

---

# PHASE 2 — ATTACK SURFACE ANALYSIS

Identify all attack surfaces including:

## Public Endpoints

* Homepage
* Login / Logout
* Registration / Account Creation
* Password Reset / Forgot Password
* Contact & Feedback Forms
* Search Functions
* Public APIs
* Admin Panels & Dashboards
* File Upload Forms
* Payment / Checkout Systems
* OAuth / SSO Endpoints

## Internal Attack Surfaces

* Admin & Staff Routes
* User Dashboards
* API Endpoints (authenticated)
* Background Jobs & Workers
* Queue Workers
* Cron Jobs & Scheduled Tasks
* Internal Microservices / APIs
* File Storage Systems
* Webhook Receivers

> **Create a complete attack surface map with risk ratings for each surface.**

---

# PHASE 3 — OWASP TOP 10 ASSESSMENT (2021)

Test for all OWASP Top 10 categories:

## A01 — Broken Access Control

* IDOR (Insecure Direct Object Reference)
* Privilege Escalation (Vertical & Horizontal)
* Forced Browsing / Path Guessing
* Missing Authorization Checks on Functions & Routes
* Role Bypass via Parameter Tampering

## A02 — Cryptographic Failures

* Weak or Deprecated Encryption (MD5, SHA1, DES)
* Insecure Password Storage (plain text, weak hashing)
* Sensitive Data Transmitted over HTTP
* Weak TLS/SSL Configuration
* Missing Encryption at Rest

## A03 — Injection Attacks

* SQL Injection (Classic, Blind, Time-Based, Error-Based)
* NoSQL Injection (MongoDB, Firebase)
* Command / OS Injection
* LDAP Injection
* XPath Injection
* Server-Side Template Injection (SSTI)
* HTTP Header Injection
* Email / SMTP Injection

## A04 — Insecure Design

* Business Logic Flaws
* Workflow Abuse & Step Skipping
* Price / Quantity Manipulation
* Process / State Machine Vulnerabilities

## A05 — Security Misconfiguration

* Debug Mode Exposed in Production
* Verbose Error Messages Leaking Stack Traces
* Default Credentials on Admin Panels
* Open Directory Listings
* Unnecessary Services & Open Ports
* Missing Security Headers

## A06 — Vulnerable & Outdated Components

* Outdated Libraries with Known CVEs
* Unpatched Frameworks
* Supply Chain Risks
* Abandoned / Unmaintained Packages

## A07 — Identification & Authentication Failures

* Session Weaknesses (Fixation, Prediction, Hijacking)
* Brute-Force on Login (no rate limiting / CAPTCHA)
* MFA Bypass / Weak MFA Implementation
* Insecure Password Reset Flows
* Credential Stuffing Susceptibility

## A08 — Software & Data Integrity Failures

* Insecure Auto-Update Mechanisms
* Unverified Dependency Integrity (no lockfile hash checks)
* Build / CI Pipeline Injection Risks
* Deserialization Vulnerabilities

## A09 — Security Logging & Monitoring Failures

* Missing Audit Trails for Sensitive Actions
* Insufficient Logging of Auth Events
* No Alerting on Suspicious Activity
* Log Injection

## A10 — SSRF (Server-Side Request Forgery)

* Internal Resource Access via SSRF
* Cloud Metadata Service Exposure (AWS IMDSv1, GCP, Azure)
* DNS Rebinding
* Blind SSRF

---

# PHASE 4 — ADVANCED VULNERABILITY TESTING

Test for:

* **XSS** — Stored, Reflected, DOM-Based
* **CSRF** — Missing / Bypassable Tokens
* **XXE** — XML External Entity Injection
* **SSRF** — Internal & Metadata Endpoint Access
* **RCE** — Remote Code Execution via Any Vector
* **Open Redirects** — Phishing & Token Theft
* **Directory & Path Traversal** — `../` Sequences
* **Local / Remote File Inclusion (LFI / RFI)**
* **Clickjacking** — Missing X-Frame-Options / CSP
* **Host Header Injection** — Password Reset Poisoning
* **Cache Poisoning** — Web Cache Deception
* **HTTP Request Smuggling** — CL.TE / TE.CL
* **Race Conditions** — Time-of-Check to Time-of-Use (TOCTOU)
* **Session Fixation & Hijacking**
* **JWT Attacks** — `alg:none`, Key Confusion, Weak Secrets
* **OAuth 2.0 Weaknesses** — State Parameter, Open Redirects, Token Leakage
* **CORS Misconfiguration** — Overly Permissive Origins
* **WebSocket Security** — Missing Auth, Injection
* **API Abuse & Parameter Pollution**
* **Business Logic Vulnerabilities** — Coupon Reuse, Balance Manipulation

---

# PHASE 5 — SOURCE CODE REVIEW

Review all source code files including:

## Backend

* Controllers / Route Handlers
* Services / Business Logic
* Middleware / Guards / Interceptors
* Models / Entities / Schemas
* Repositories / Data Access Layer
* Background Jobs / Workers
* Event Listeners / Hooks
* Policies & Permission Checks
* Authentication & Authorization Logic

## Frontend

* Templates / Views
* React / Vue / Angular Components
* JavaScript / TypeScript Logic
* State Management (Redux, Zustand, Pinia, etc.)
* API Integration Code
* LocalStorage / SessionStorage / Cookie Usage
* Client-Side Routing Guards

## Configuration

* `.env` / `.env.example` Files
* Build Configuration Files
* Security-Related Settings
* Deployment & Infrastructure Scripts (Dockerfile, docker-compose, k8s YAML)

Detect:

* Unsafe Code Patterns
* Hardcoded Secrets & Credentials
* Missing Input Validation & Sanitization
* Missing or Insufficient Authorization Checks
* Weak or Missing Error Handling
* Dangerous Function Usage (`eval`, `exec`, `shell_exec`, etc.)
* Insecure Default Settings
* Commented-Out Sensitive Code

---

# PHASE 6 — AUTHENTICATION & AUTHORIZATION REVIEW

Assess:

* Login Form Security (Rate Limiting, CAPTCHA, Lockout)
* Registration Security (Email Verification, Duplicate Detection)
* Password Reset Security (Token Expiry, Single-Use Tokens)
* MFA Support & Implementation Quality
* Session Management (Secure Flags, HttpOnly, SameSite)
* Remember Me Functionality Security
* Role-Based Access Control (RBAC) Design
* Permission Systems & Granularity
* Administrative Control Protections

Attempt to bypass:

* Login Rate Limits & Lockout Mechanisms
* Role & Permission Restrictions
* Middleware / Guard Restrictions
* Access Control Lists
* Admin-Only Endpoints

---

# PHASE 7 — API SECURITY ASSESSMENT

Review all API types:

* REST APIs
* GraphQL APIs (Introspection, Batching, Depth Limit)
* Webhooks (Signature Verification)
* gRPC / WebSocket Endpoints

Test for OWASP API Security Top 10:

* **API1** — Broken Object Level Authorization
* **API2** — Broken Authentication
* **API3** — Broken Object Property Level Authorization (Mass Assignment)
* **API4** — Unrestricted Resource Consumption (Rate Limiting)
* **API5** — Broken Function Level Authorization
* **API6** — Unrestricted Access to Sensitive Business Flows
* **API7** — Server Side Request Forgery
* **API8** — Security Misconfiguration
* **API9** — Improper Inventory Management (Hidden / Undocumented Endpoints)
* **API10** — Unsafe Consumption of APIs (Third-party)

---

# PHASE 8 — FILE UPLOAD SECURITY

Review all upload endpoints:

* Image Uploads
* Document Uploads (PDF, Word, CSV)
* Avatar / Profile Picture Uploads

Test for:

* Executable File Uploads (PHP, JS, EXE shells)
* Double Extension Bypass (`shell.php.jpg`)
* MIME Type Spoofing Bypass
* SVG XSS Injection
* Malware & Polyglot File Uploads
* Path Traversal via Filename (`../../etc/passwd`)
* Unrestricted File Size (DoS via Upload)
* Stored File Access Controls (Direct URL Access to Private Files)

---

# PHASE 9 — DEPENDENCY & SUPPLY CHAIN SECURITY

Analyze all package managers:

* Composer (PHP) — `composer.json` / `composer.lock`
* NPM / Yarn / PNPM — `package.json` / `package-lock.json`
* Pip / Poetry — `requirements.txt` / `pyproject.toml`
* NuGet — `.csproj` packages
* Maven / Gradle — `pom.xml` / `build.gradle`
* Cargo (Rust) — `Cargo.toml`
* Go Modules — `go.mod`

Identify:

* Known Vulnerabilities (CVE Database, Snyk, npm audit, pip-audit)
* Outdated / Unpinned Dependencies
* Abandoned / Unmaintained Packages
* Typosquatting Risks
* High-Risk Transitive Dependencies

---

# PHASE 10 — SECRET & CREDENTIAL DISCOVERY

Search for exposed secrets in all source files, configs, and history:

* API Keys (Stripe, Twilio, SendGrid, AWS, GCP, Azure)
* Auth Tokens & Bearer Tokens
* AWS / GCP / Azure Access & Secret Keys
* Database Connection Strings & Credentials
* SMTP / Email Credentials
* Private SSL/TLS Keys
* JWT Signing Secrets
* Webhook Secrets
* Hardcoded Passwords

Review:

* All Source Code Files
* Configuration Files (`.env`, `config.yml`, `settings.py`)
* Build & Deployment Scripts
* Docker & Kubernetes Configs
* CI/CD Pipeline Files
* **Git History** (`git log`, `git show`, leak in old commits)

---

# PHASE 11 — SERVER & INFRASTRUCTURE REVIEW

Assess:

* Web Server Configuration (Nginx, Apache, Caddy)
* SSL/TLS Configuration (Protocol Version, Cipher Suites, Certificate)
* Reverse Proxy Configuration (Header Forwarding, Trust)
* Container Security (Docker Image Vulnerabilities, Non-Root Users)
* Docker Security (Privileged Containers, Volume Mounts, Network)
* Kubernetes Security (RBAC, Pod Security, Network Policies)
* File & Directory Permissions on Server
* Object / Blob Storage Security (Public Buckets, ACLs)

Check HTTP Security Headers:

| Header                      | Expected Value                              |
|-----------------------------|---------------------------------------------|
| `Strict-Transport-Security` | `max-age=31536000; includeSubDomains`        |
| `Content-Security-Policy`   | Restrictive policy, no `unsafe-inline`       |
| `X-Frame-Options`           | `DENY` or `SAMEORIGIN`                       |
| `X-Content-Type-Options`    | `nosniff`                                   |
| `Referrer-Policy`           | `no-referrer` or `strict-origin`            |
| `Permissions-Policy`        | Restrict camera, mic, geolocation, etc.     |
| `Cache-Control`             | `no-store` on sensitive pages               |

---

# PHASE 12 — PERFORMANCE & SECURITY HARDENING

Recommend improvements for:

* Security Architecture Improvements
* Caching Strategy & Security (Cache Poisoning Prevention)
* Database Query Optimizations & Indexing
* Asset Compression & CDN Security
* Middleware Order & Security Middleware Placement
* API Rate Limiting & Throttling Strategy
* DDoS Mitigation Recommendations

---

# PHASE 13 — LINK & ROUTE VALIDATION

Test:

* All Internal Navigation Links
* Navigation Menu Links
* All Registered API Routes
* Redirects & Redirect Chains
* Sitemap Entries

Identify:

* Broken Links (404 errors)
* Dead / Orphaned Routes
* Open Redirects
* Routing Errors & Misconfigurations
* Unauthenticated Access to Authenticated Routes

> **Automatically generate fixes for all broken links and routing issues found.**

---

# PHASE 14 — ATTACKER MINDSET REVIEW

Act as a **real-world attacker** with no prior knowledge of the system.

Attempt to:

* Bypass Authentication (brute force, token forgery, bypass flows)
* Bypass Authorization (IDOR, parameter manipulation, role escalation)
* Access Unauthorized Data (other users' data, admin data)
* Escalate Privileges (user → admin, guest → user)
* Manipulate Business Logic (free purchases, unlimited credits)
* Abuse API Endpoints (mass enumeration, scraping, abuse flows)
* Abuse File Upload Functionality (shell upload, XSS via SVG)
* Abuse User Workflows (race conditions, state manipulation)
* Perform Reconnaissance (information disclosure, error messages)

> **Document realistic, step-by-step attack paths with impact ratings.**

---

# PHASE 15 — AUTOMATED REMEDIATION

For **every issue discovered**, provide:

1. **Vulnerability Name** — Clear, concise name
2. **Severity** — Critical / High / Medium / Low / Informational
3. **Impact** — What can an attacker achieve?
4. **Root Cause** — Why does this vulnerability exist?
5. **Proof of Concept** — Exact reproduction steps or payload
6. **Affected Files** — File paths and line numbers
7. **Affected Routes / Endpoints** — URL patterns
8. **Secure Fixed Code** — Complete, production-ready replacement code
9. **Explanation of Fix** — Why the fix is secure
10. **Regression Check** — Confirm fix does not break functionality

---

# PHASE 16 — GITHUB & SOURCE REPOSITORY SECURITY

Review the source code repository and version control practices:

## Repository Configuration

* Branch Protection Rules (require PR reviews, no direct pushes to main)
* Required Pull Request Approvals & Code Review Enforcement
* Commit Signature Verification (GPG / SSH Signing)
* Access Controls & Permissions (Least Privilege Principle)
* Outside Collaborator Access Review
* Repository Visibility (Public vs Private)

## CI/CD Pipeline Security (GitHub Actions / GitLab CI / Bitbucket Pipelines)

* Workflow File Review for Command Injection (`${{ github.event.* }}`)
* Secrets Management in CI (proper use of `secrets.*`, no plaintext)
* Third-Party GitHub Actions (pinned to SHA, not floating tags)
* Runner Security (self-hosted runner risks)
* Artifact & Cache Poisoning Risks
* Deployment Key & Token Scope Review

## Git History & Repository Hygiene

* Secrets Committed & Exposed in Git History
* Large Binary Files / Sensitive Data in Repository
* Exposed `.git` Directory on Production Server (`/.git/config`)
* `.gitignore` Coverage (ensuring `.env`, keys, logs are excluded)
* Unintended Public Repository Exposure

---

# REPORT REQUIREMENTS

Generate a **professional enterprise security report** using the following structure:

---

## 📊 Executive Summary

| Metric                      | Value |
|-----------------------------|-------|
| Total Findings              | —     |
| 🔴 Critical                 | —     |
| 🟠 High                     | —     |
| 🟡 Medium                   | —     |
| 🟢 Low                      | —     |
| ℹ️ Informational             | —     |

---

## 🔍 Detailed Findings

For each issue include:

| Field              | Details                          |
|--------------------|----------------------------------|
| Vulnerability Name | —                                |
| Severity           | Critical / High / Medium / Low   |
| CVSS Score         | 0.0 – 10.0                       |
| Risk Description   | —                                |
| Affected Files     | File paths & line numbers        |
| Affected Routes    | URL patterns                     |
| Proof of Concept   | Payload / Reproduction steps     |
| Root Cause         | —                                |
| Remediation        | Step-by-step fix                 |
| Secure Code        | Fixed code snippet               |

---

## 📋 Compliance Mapping

Map all findings against:

* OWASP Top 10 (2021)
* OWASP ASVS (Level 1 / 2 / 3)
* OWASP API Security Top 10 (2023)
* CWE (Common Weakness Enumeration)
* NIST SP 800-53
* GDPR / PCI-DSS / HIPAA (if applicable)

---

## 🏆 Security Score

| Metric                       | Score    |
|------------------------------|----------|
| Current Security Score       | — / 100  |
| Post-Remediation Score       | — / 100  |
| Production Readiness Score   | — / 100  |
| Overall Risk Rating          | Critical / High / Medium / Low |

---

## ✅ Final Verdict

State whether the application is:

- [ ] ✅ **Production Ready** — No significant issues
- [ ] ⚠️ **Production Ready with Minor Fixes** — Low-severity issues only
- [ ] 🔶 **Requires Significant Remediation** — High/Critical issues present
- [ ] 🚫 **Not Safe for Production** — Critical vulnerabilities found

---

## 🗺️ Prioritized Remediation Roadmap

Provide a prioritized action plan:

| Priority | Finding               | Effort   | Impact if Fixed |
|----------|-----------------------|----------|-----------------|
| P0       | [Critical Issue]      | Low      | Prevents RCE    |
| P1       | [High Issue]          | Medium   | Prevents Data Breach |
| P2       | [Medium Issue]        | Medium   | Reduces Attack Surface |
| P3       | [Low Issue]           | Low      | Hardens Defence |

Include estimated remediation effort (hours/days) for each finding.

<!-- ═══════════════════════════ PROMPT END ════════════════════════════════ -->
