---
tags:
  - Security
  - Red Team
  - Bug Bounty
  - Overview
---

# FIER's Red Algodex

> Der spezialisierte Sicherheits- und Offensive-Security-Hub von FIER.  
> Hier dokumentiere ich Angriffsmethoden, Web-Schwachstellen, Pentesting-Tools und Bug-Bounty-Workflows nach PortSwigger- und OWASP-Standards.

---

## Bereiche im Red Algodex

- **[Lernpfad: Web Security & Bug Bounty](roadmaps/web-security.md):**    
  Der chronologische Stufenplan von HTTP-Grundlagen über Burp Suite bis hin zu komplexen Desynchronisationsangriffen und Reconnaissance.

- **Vulnerabilities & Exploits:**
  - **[Web-Fundamente (HTTP, SOP, CORS, CSP)](vulnerabilities/http-sop-cors-csp.md):** Protokolle, Session-Sicherheit, SOP-Grenzziehungen und CSP-Direktiven.
  - **[Cross-Site Scripting (XSS)](vulnerabilities/xss.md):** Reflected, Stored und DOM-based XSS, Sources/Sinks und WAF-Bypasses.
  - **[CSRF, CORS-Leaks & Clickjacking](vulnerabilities/client-side-advanced.md):** Auto-Submit PoCs, Origin-Reflection und transparente iFrame-Überlagerungen.
  - **[SQL Injection (SQLi)](vulnerabilities/sqli.md):** Union-Based, Error-Based und Blind SQLi (Boolean/Time) sowie Prepared Statements.
  - **[Server-Side Request Forgery (SSRF)](vulnerabilities/ssrf.md):** Auslesen von Cloud-Metadaten (AWS IMDS), IP-Filter-Bypasses und OAST.
  - **[Broken Access Control & IDOR](vulnerabilities/access-control-idor.md):** Horizontale/vertikale Rechteausweitung und automatisierte IDOR-Erkennung mit Autorize.
  - **[Command Injection, Path Traversal & SSTI](vulnerabilities/command-injection-ssti.md):** Shell-Injektionen, Directory Traversal und Template-RCE.
  - **[Business Logic Flaws & JWT](vulnerabilities/business-logic-jwt.md):** Logikfehler im Checkout, `alg: none` Angriffe und Key Confusion.
  - **[Request Smuggling & Race Conditions](vulnerabilities/advanced-attacks.md):** CL.TE / TE.CL Desynchronisation und Single-Packet Attacks mit Turbo Intruder.

- **Tools & Workflow:**
  - **[Burp Suite Grundlagen](tools/burp-suite-basics.md):** Proxy, Repeater, Intruder, Collaborator und unverzichtbare BApp-Extensions.
  - **[Reconnaissance, Fuzzing & Reporting](tools/recon-reporting.md):** Asset Discovery (`subfinder`, `puredns`), Fuzzing (`ffuf`), `nuclei` und CVSS-Reports.

---

## Zurück zum Algorithmen-Wiki

Über die Hauptnavigation oder diesen Link gelangst du jederzeit zurück zum Core-Bereich:
👉 **[FIER's Algodex (Algorithmen & LeetCode)](../index.md)**
