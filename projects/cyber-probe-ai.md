# CyberProbe AI: Web Security Attack Surface & Header Auditor

[![Python](https://img.shields.io/badge/Python-3.11%2B-blue.svg)](https://www.python.org/)
[![OWASP](https://img.shields.io/badge/Standard-OWASP%20Top%2010-red.svg)](https://owasp.org/)
[![Pydantic](https://img.shields.io/badge/Validation-Pydantic%20v2-e92063.svg)](https://pydantic.dev/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Privacy](https://img.shields.io/badge/Repository-Private-critical.svg)](#)

An automated web security attack surface scanner and HTTP security header auditor. CyberProbe analyzes live HTTP/S response headers, cookie flags, TLS protocol parameters, and information disclosure leaks to grade web server hardening from A+ down to F, accompanied by actionable remediation directives.

Built on **Playwright**, **Pydantic v2**, **BeautifulSoup4**, and **Rich**.

---

## 🎯 Architecture & Data Flow

```mermaid
flowchart TD
    Target[Target URL / Domain] --> Prober[Async HTTP Probe & TLS Inspector]
    Prober --> HeaderInspector[HTTP Response Headers]
    Prober --> CookieInspector[Cookie Security Attributes]
    Prober --> LeakDetector[Server Banner & Tech Stack Leaks]
    HeaderInspector --> CSP[Content-Security-Policy]
    HeaderInspector --> HSTS[Strict-Transport-Security]
    HeaderInspector --> XFrame[X-Frame-Options & Clickjacking]
    CookieInspector --> CookieFlags[HttpOnly, SameSite, Secure]
    CSP & HSTS & XFrame & CookieFlags & LeakDetector --> RiskMatrix[OWASP Risk Matrix]
    RiskMatrix --> ScoreEngine[Hardening Grade A+ to F]
    ScoreEngine --> Report[Executive Security Report & Hardening Diff]
```

---

## 🔬 Working Model & CLI Execution Walkthrough

### Example Command
```bash
python -m src.main https://insecure-portal.example.com --strict
```

### Live Working Model Output
```text
╭──────────────────────────────────────────────────────────────────────────────╮
│                       🔒 CyberProbe AI v1.0.0                                │
│   Auditing Target: https://insecure-portal.example.com                       │
╰──────────────────────────────────────────────────────────────────────────────╯

Security Header & Policy Audit:
┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━┳━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃ Header Name                ┃ Status     ┃ Severity ┃ Risk Implication        ┃
┣━━━━━━━━━━━━━━━━━━━━━━━━━━━━╋━━━━━━━━━━━━╋━━━━━━━━━━╋━━━━━━━━━━━━━━━━━━━━━━━━━┫
┃ Content-Security-Policy    ┃ MISSING    ┃ HIGH     ┃ Vulnerable to XSS / SRI ┃
┃ Strict-Transport-Security  ┃ PARTIAL    ┃ MEDIUM   ┃ Missing includeSubDomains┃
┃ X-Frame-Options            ┃ CONFIGURED ┃ PASS     ┃ Protected (DENY)        ┃
┃ X-Content-Type-Options     ┃ MISSING    ┃ LOW      ┃ MIME-sniffing possible  ┃
┃ Cookie: session_token      ┃ FLAWED     ┃ HIGH     ┃ Missing 'HttpOnly' flag ┃
┃ Server Header              ┃ DISCLOSED  ┃ LOW      ┃ Leaks: 'nginx/1.18.0'   ┃
┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━┻━━━━━━━━━━━━┻━━━━━━━━━━┻━━━━━━━━━━━━━━━━━━━━━━━━━┛

┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃ Security Audit Scorecard                                                     ┃
┣━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┫
┃ Hardening Score : 54 / 100                                                   ┃
┃ Letter Grade    : Grade D (Immediate Remediation Recommended)                ┃
┃ Recommended Nginx Header Configuration snippet generated in 'security.conf'  ┃
┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

---

## ⚡ Core Features

- **OWASP Compliance Mapping**: Evaluates security posture against OWASP Secure Headers guidelines.
- **Cookie Rigor Validation**: Checks `Secure`, `HttpOnly`, and `SameSite` flags across all session cookies.
- **Server Hardening Snippet Generator**: Automatically outputs ready-to-paste Nginx, Apache, or Caddy configuration snippets to achieve an A+ rating.
