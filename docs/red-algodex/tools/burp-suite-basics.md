---
tags:
  - Security
  - Tool
  - Burp Suite
  - Proxy
  - Bug Bounty
---

# Burp Suite: Grundlagen & Praxiseinsatz

**Burp Suite** (von PortSwigger) ist das zentrale Werkzeug für Penetrationstests und Bug Bounty Hunting im Web. Es agiert als **Man-in-the-Middle (MitM) HTTP-Proxy** zwischen deinem Webbrowser und dem Zielserver.

---

## Architektur: Wie Burp Suite arbeitet

Normalerweise kommuniziert dein Browser verschlüsselt direkt mit dem Webserver über HTTPS. Schaltest du Burp Suite dazwischen, fängt Burp jeden Request ab, bevor er den Rechner verlässt, und jede Response, bevor der Browser sie rendert:

```mermaid
graph LR
    Browser["Webbrowser (z. B. Firefox)"] -->|HTTP/S Request| Proxy["Burp Suite Proxy (Port 8080)"]
    Proxy -->|Modifizierter Request| Server["Zielserver (Web Application)"]
    Server -->|HTTP Response| Proxy
    Proxy -->|Analysierte Response| Browser

    style Browser fill:#3f51b5,stroke:#fff,stroke-width:2px,color:#fff
    style Proxy fill:#ff9800,stroke:#fff,stroke-width:2px,color:#fff
    style Server fill:#4caf50,stroke:#fff,stroke-width:2px,color:#fff
```

Damit Burp Suite verschlüsselten HTTPS-Verkehr entschlüsseln und anzeigen kann, muss einmalig das **Burp CA-Zertifikat** (`http://burp/cert`) als vertrauenswürdige Stammzertifizierungsstelle im Browser importiert werden.

---

## Die Kernmodule im Überblick

### 1. Proxy & Intercept
- **Intercept is on/off:** Wenn aktiviert, hält Burp jeden HTTP-Request an. Du kannst Parameter, Header oder Cookies im Klartext editieren und dann mit *Forward* absenden oder mit *Drop* verwerfen.
- **HTTP History:** Protokolliert jeden einzelnen Request und Response chronologisch mit URL, Statuscode, MIME-Typ und Antwortlänge. Dies ist das wichtigste Werkzeug, um die Funktionsweise einer Webapplikation zu verstehen.
- **Match and Replace:** Ermöglicht automatisierte Header-Ersetzungen (z. B. automatisches Hinzufügen von `X-Forwarded-For: 127.0.0.1` oder Ändern des User-Agents).

### 2. Repeater (Shortcut: Strg + R)
Das Herzstück manueller Analysen:
- Schicke einen beliebigen Request aus der HTTP History mit <kbd>Strg</kbd> + <kbd>R</kbd> an den Repeater.
- Du kannst Parameter verändern, Payloads testen und den Request beliebig oft mit *Send* neu absenden, ohne die Seite im Browser neu laden zu müssen.
- Ideal zum schnellen Testen von SQL Injections, IDORs und XSS.

### 3. Intruder (Shortcut: Strg + I)
Automatisiertes Fuzzing und Brute-Forcing von Parametern.

#### Die 4 Angriffstypen (Attack Types):
1. **Sniper:** Testet eine einzige Payload-Liste nacheinander über alle markierten Positionen (eine Position nach der anderen).
2. **Battering Ram:** Setzt dieselbe Payload gleichzeitig an alle markierten Stellen ein.
3. **Pitchfork:** Nutzt mehrere Payload-Listen synchron (z. B. Liste 1 für Benutzernamen, Liste 2 für Passwörter; Zeile 1 mit Zeile 1, Zeile 2 mit Zeile 2).
4. **Cluster Bomb:** Testet jede Kombination aller Payload-Listen kartesisch durch (z. B. 100 Passwörter für jeden von 10 Benutzern = 1.000 Requests).

### 4. Decoder
Ermöglicht schnelles Konvertieren und Transformieren von Strings direkt in Burp:
- URL-Encoding / Decoding (`%20`, `%27`, `%22`)
- HTML-Entity-Encoding (`&lt;script&gt;`)
- Base64-Encoding / Decoding (JWTs, Basic Auth)
- Hashing (MD5, SHA-256)

### 5. Comparer
Ermöglicht den schnellen visuellen Diff zweier Responses oder Requests:
- **Byte-by-Byte / Word-by-Word:** Hilft bei Blind SQL Injection oder Timing-Angriffen, minimale Unterschiede (z. B. fehlende Fehlermeldung oder verändertes Token) sofort farblich hervorzuheben.

### 6. Burp Collaborator (OAST – Out-of-Band Testing)
Erkennt Schwachstellen, bei denen der Server keine direkte Fehlermeldung im HTTP-Response anzeigt (*Blind Vulnerabilities*), sondern im Hintergrund eine Verbindung nach außen aufbaut:
- Generiert eine eindeutige Subdomain (z. B. `xyz.oastify.com`).
- Sendest du diese als Payload bei SSRF oder Blind XXE ein und der Zielserver versucht eine DNS-Auflösung oder HTTP-Verbindung, fängt der Collaborator-Server dies ab und schlägt sofort Alarm.

---

## Wichtige BApp-Extensions für Bug Bounties

In der Burp Suite Community & Professional Edition können über den **BApp Store** Plugins nachinstalliert werden:

1. **Autorize:** Testet vollautomatisch im Hintergrund auf Autorisierungs-Lücken ([Broken Access Control / IDOR](../vulnerabilities/access-control-idor.md)), indem jeder Request deines Admin-Accounts mit den Cookies eines Low-Privilege-Users wiederholt wird.
2. **Turbo Intruder:** Extrem schneller HTTP-Fuzzer auf Python-Basis (entwickelt von James Kettle), unverzichtbar für [Race Condition Exploits](../roadmaps/web-security.md) mit Single-Packet Attacks.
3. **Param Miner:** Sucht automatisch nach versteckten Parametern und Headern (z. B. für Web Cache Poisoning).
4. **Hackvertor:** Tag-basiertes Encoding-Tool zur einfachen Umgehung von Web Application Firewalls (WAFs).

---

## Empfohlener Workflow beim Start

1. Browser über FoxyProxy mit `127.0.0.1:8080` verbinden.
2. Scope in Burp definieren (*Target -> Scope*): Nur die erlaubte Target-Domain aktivieren, um privaten Hintergrund-Traffic auszublenden.
3. Anwendung wie ein normaler Nutzer durchklicken (*Passive Crawling*), um alle Endpunkte in der HTTP History zu sammeln.
4. Interessante Endpunkte (Login, API-Calls, Dateiuploads, Profiländerungen) an den Repeater senden und schrittweise manipulieren.
