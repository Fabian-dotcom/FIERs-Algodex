---
tags:
  - Security
  - Vulnerability
  - Web Security
  - Business Logic
  - JWT
  - Authentication
---

# Business Logic Flaws & JWT-Sicherheitslücken

Business Logic Flaws und Authentifizierungsfehler basieren selten auf technischem Syntax-Fehlverhalten, sondern auf fehlerhaften Annahmen im Anwendungsdesign.

---

## 1. Business Logic Flaws (Logikfehler)

Logikfehler lassen sich selten durch automatisierte Scanner (wie Burp Scanner oder Nessus) finden. Sie erfordern menschliches Verständnis für den Geschäftsprozess.

### Typische Logikfehler-Muster:

1. **Negative Zahlen & Integer Overflow:**
   - Beim Bestellen im Onlineshop sendet der Angreifer:
     `{"item_id": 1, "quantity": -5}`
   - Der Server multipliziert den Einzelpreis mit `-5`, und die Gesamtsumme sinkt oder wird negativ (Guthaben wird gutgeschrieben).

2. **Überspringen von Workflow-Schritten:**
   - Ein 3-stufiger Checkout:
     `Schritt 1: Adresse eingeben` $\to$ `Schritt 2: Zahlung durchführen` $\to$ `Schritt 3: Bestellung bestätigen`.
   - Der Angreifer ruft nach Schritt 1 direkt `/order/confirm` auf und umgeht die Zahlungsprüfung vollständig.

3. **Gutschein-Wiederverwendung (Coupon Stacking):**
   - Ein Rabattcode `DISCOUNT10` wird angewendet, entfernt und erneut angewendet, wodurch der Rabatt mehrfach akkumuliert.

---

## 2. JWT (JSON Web Token) Schwachstellen

JWTs werden häufig für staatenlose Authentifizierung in REST-APIs und Single-Page-Apps verwendet. Ein JWT besteht aus drei Base64Url-kodierten Teilen:
$$\text{Header} \,.\, \text{Payload} \,.\, \text{Signature}$$

```text
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyIjoidmljdGltIiwicm9sZSI6InVzZXIifQ.dBjftJeZ4CVP-mB92K27uhbUJU1p1r_wW1gFWFOEjXk
```

```mermaid
graph LR
    H["Header: {'alg': 'HS256'}"] --- P["Payload: {'user': 'victim'}"] --- S["Signatur: HMAC(H + P, Secret)"]

    style H fill:#3f51b5,stroke:#fff,stroke-width:2px,color:#fff
    style P fill:#009688,stroke:#fff,stroke-width:2px,color:#fff
    style S fill:#e91e63,stroke:#fff,stroke-width:2px,color:#fff
```

### Die wichtigsten Angriffsvektoren:

1. **Der `alg: none` Angriff:**
   - Der JWT-Standard erlaubt den Algorithmus `none` (unsignierter Token).
   - Der Angreifer ändert im Header `{"alg": "none"}`, ändert im Payload `{"role": "admin"}` und entfernt die Signatur (lässt nur den abschließenden Punkt stehen).
   - Viele unsichere Bibliotheken akzeptieren diesen Token ohne Signaturprüfung!

2. **Schwache HMAC-Secrets (Brute-Force):**
   - Wenn für `HS256` ein schwaches Passwort (z. B. `secret`, `123456`) genutzt wird, kann der Signaturschlüssel offline mit Tools wie `hashcat` oder `jwt-cracker` in Sekunden geknackt werden:
     ```bash
     hashcat -a 0 -m 16500 jwt.txt rockyou.txt
     ```
   - Ist das Secret bekannt, kann der Angreifer beliebig signierte Admin-Tokens generieren.

3. **Algorithm Confusion (Key Confusion: RS256 zu HS256):**
   - Normalerweise signiert der Server Tokens asymmetrisch mit einem privaten RSA-Schlüssel (`RS256`), und APIs verifizieren mit dem öffentlichen Schlüssel.
   - Der Angreifer ändert den Algorithmus im Header auf `HS256` (symmetrischer HMAC).
   - Wenn der Server denselben öffentlichen Schlüssel als HMAC-Secret nutzt (welcher oft öffentlich unter `/.well-known/jwks.json` abrufbar ist), akzeptiert er die vom Angreifer mit dem öffentlichen Schlüssel signierte Fälschung!
