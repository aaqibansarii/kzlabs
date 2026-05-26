## Title

Reflected Cross-Site Scripting (XSS) via `fname` and `lname` Parameters

## Vulnerability Type

Reflected XSS

## Summary

The application reflects user-controlled input from the `fname` and `lname` parameters without proper sanitization or output encoding, allowing arbitrary JavaScript execution in the victim’s browser.

An attacker can craft a malicious URL containing JavaScript payloads in these parameters, which execute automatically when the page is loaded.

## Vulnerable Endpoint

```http
http://kzlabs.com/punishment/1.php?fname=%22xicorr%3E%3CsCript%3Ealert%28%22xicorXSS%22%29%3C%2FsCript%3E&lname=%22xicorr%3E%3CsCript%3Ealert%28%22xicorXSS%22%29%3C%2FsCript%3E
```

## Vulnerable Parameters

```http
fname
lname
```

## Steps to Reproduce

1. Open the following URL in a browser:

```http
http://kzlabs.com/punishment/1.php?fname=%22xicorr%3E%3CsCript%3Ealert%28%22xicorXSS%22%29%3C%2FsCript%3E&lname=%22xicorr%3E%3CsCript%3Ealert%28%22xicorXSS%22%29%3C%2FsCript%3E
```

2. Observe that a JavaScript alert popup is triggered automatically.

## Payload Used

```html
"xicorr><sCript>alert("xicorXSS")</sCript>
```

## Proof of Concept

The application reflects attacker-controlled input from the `fname` and `lname` parameters directly into the page without proper sanitization.

As a result, arbitrary JavaScript executes automatically when the crafted URL is visited.

### Screenshot 1 — Reflected XSS Triggered via Query Parameters -fname

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/c71d0585-5d6c-4284-9c8c-5508096807b8" />

### Screenshot 2 — Reflected XSS Triggered via Query Parameters -lname

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/4e82f8bd-86d9-436b-baa2-08765ad72f1b" />

## Impact

An attacker can exploit this vulnerability to:

- Execute arbitrary JavaScript in the victim’s browser
- Hijack authenticated user sessions
- Perform unauthorized actions on behalf of users
- Exfiltrate sensitive information
- Conduct phishing attacks using trusted application context

## Recommendations for Fix

- Properly sanitize and encode all user-controlled input before rendering
- Apply contextual output encoding for HTML contexts
- Avoid rendering raw query parameter values directly into the page
- Validate input against expected formats
- Implement a strict Content Security Policy (CSP)
