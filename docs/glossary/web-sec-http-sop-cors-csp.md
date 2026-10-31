---
tags:
  - Security
  - Web Security
  - HTTP
  - Cookies
  - SOP
  - CORS
  - CSP
---

# Web-Fundamente: HTTP-Protokoll & Browser-Sicherheitsmodelle

Bevor man Sicherheitslücken analysieren kann, muss man verstehen, wie Daten auf Byte-Ebene übertragen werden und welche Sicherheitsgrenzen moderne Webbrowser erzwingen.

---

## 1. Das HTTP-Protokoll (Hypertext Transfer Protocol)

HTTP ist ein zustandsloses Request-Response-Textprotokoll.

### Struktur eines HTTP/1.1 Requests
```http
POST /api/login HTTP/1.1
Host: example.com
User-Agent: Mozilla/5.0 ...
Content-Type: application/json
Content-Length: 43

{"username": "admin", "password": "secret"}
```

- **HTTP-Verben:**
  - `GET`: Ressource abrufen (sollte idempotent und ohne Seiteneffekte sein).
  - `POST`: Daten übermitteln (Erzeugung von Ressourcen, Logins, Formulare).
  - `PUT` / `PATCH`: Ressource vollständig ersetzen (`PUT`) oder partiell aktualisieren (`PATCH`).
  - `DELETE`: Ressource entfernen.
  - `OPTIONS`: Fragt erlaubte Methoden ab (wichtig für CORS-Preflight).

- **Statuscodes:**
  - `2xx (Erfolg)`: z. B. `200 OK`, `201 Created`, `204 No Content`.
  - `3xx (Umleitung)`: z. B. `301 Moved Permanently`, `302 Found`, `304 Not Modified`.
  - `4xx (Client-Fehler)`: z. B. `400 Bad Request`, `401 Unauthorized` (nicht eingeloggt), `403 Forbidden` (eingeloggt, aber keine Rechte), `404 Not Found`.
  - `5xx (Server-Fehler)`: z. B. `500 Internal Server Error`, `502 Bad Gateway`, `504 Gateway Timeout`.

---

## 2. Session Management & Cookie-Sicherheit

Da HTTP zustandslos ist, identifiziert der Server Benutzer über Session-Tokens in Cookies oder Headern.

### Cookie-Sicherheitsflags
Ein Server setzt ein Cookie über den Header `Set-Cookie`:
```http
Set-Cookie: session_id=abc123xyz; Secure; HttpOnly; SameSite=Lax; Path=/; Domain=example.com
```

| Flag | Schutzfunktion | Angriff ohne dieses Flag |
| :--- | :--- | :--- |
| **`HttpOnly`** | Verhindert den Zugriff durch clientseitiges JavaScript (`document.cookie`). | Bei [XSS](web-sec-xss.md) kann der Session-Token sofort gestohlen werden. |
| **`Secure`** | Cookie wird ausschließlich über verschlüsselte HTTPS-Verbindungen gesendet. | Abfangen des Tokens im offenen WLAN (Man-in-the-Middle). |
| **`SameSite=Strict`** | Cookie wird bei seitenübergreifenden Anfragen (Cross-Site) **niemals** mitgesendet. | Verhindert [CSRF](web-sec-client-side-advanced.md) vollständig. |
| **`SameSite=Lax`** | Standard in modernen Browsern. Wird nur bei sicheren Top-Level-Navigationen (z. B. Anklicken eines Links) mitgesendet, nicht bei POST-Requests von fremden Seiten. | Schutz vor den meisten CSRF-Angriffen. |
| **`SameSite=None`** | Cookie wird immer mitgesendet (erfordert zwingend das `Secure`-Flag). | Erlaubt Cross-Site-Tracking und ist anfällig für CSRF ohne Token. |

---

## 3. Browser-Sicherheitsmodelle

### Die Same-Origin Policy (SOP)
Die **Same-Origin Policy** ist das grundlegendste Sicherheitskonzept des Webs. Sie verbietet Skripten einer Origin, auf Ressourcen einer anderen Origin zuzugreifen.

Eine **Origin** wird definiert durch das Tripel:
$$\text{Origin} = (\text{Schema}, \text{Host}, \text{Port})$$

*Vergleich mit `https://example.com:443/app/index.html`:*

| URL | Gleiche Origin? | Grund |
| :--- | :---: | :--- |
| `https://example.com/app/data.json` | Ja | Schema, Host und Port identisch. |
| `http://example.com/app/` | Nein | Anderes Schema (`http` statt `https`). |
| `https://api.example.com/` | Nein | Anderer Host (Subdomain gilt als fremde Origin). |
| `https://example.com:8443/` | Nein | Anderer Port (8443 statt 443). |

---

### Cross-Origin Resource Sharing (CORS)
CORS lockert die SOP kontrolliert auf. Wenn Frontend `https://my-app.com` Daten von API `https://api.com` laden möchte:
1. Browser sendet `Origin: https://my-app.com`.
2. Server antwortet mit `Access-Control-Allow-Origin: https://my-app.com`.
3. Sollen Cookies mitgesendet werden, muss der Server zusätzlich `Access-Control-Allow-Credentials: true` senden.

> **Sicherheitsrisiko:** Spiegelt der Server den eingehenden `Origin`-Header blind zurück und erlaubt Credentials, kann jeder fremde Angreifer sensible Nutzerdaten im Hintergrund auslesen.

---

### Content Security Policy (CSP)
Die CSP ist ein HTTP-Header, der definiert, von welchen vertrauenswürdigen Quellen der Browser Ressourcen (Skripte, Bilder, Styles) ausführen darf:

```http
Content-Security-Policy: default-src 'self'; script-src 'self' https://trustedscripts.com; object-src 'none';
```

- **`'unsafe-inline'`:** Wenn nicht gesetzt, blockiert der Browser Inline-Skripte wie `<script>alert(1)</script>` und Event-Handler (`onerror=...`).
- **Nonces:** Ein kryptografischer Zufallswert pro Request (`script-src 'nonce-rAnd0m123'`). Nur Skripte mit `<script nonce="rAnd0m123">` dürfen ausgeführt werden.
