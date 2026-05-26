## Title

Reflected Cross-Site Scripting (XSS) via `fname` Parameter

## Vulnerability Type

Reflected XSS

## Summary

The application reflects user-controlled input from the `fname` parameter without proper sanitization or output encoding, allowing arbitrary JavaScript execution in the victim’s browser.

The `lname` parameter appears to be properly handled, while the `fname` parameter remains vulnerable.

## Vulnerable Endpoint

```http
http://kzlabs.com/punishment/3.php?fname=%22xicorr%3E%3CsCript%3Ealert%28%22xicorXSS1%22%29%3C%2FsCript%3E&lname=%22xicorr%3E%3CsCript%3Ealert%28%22xicorXSS2%22%29%3C%2FsCript%3E
```

## Vulnerable Parameter

```http
fname
```

## Steps to Reproduce

1. Open the following URL in a browser:

```http
http://kzlabs.com/punishment/3.php?fname=%22xicorr%3E%3CsCript%3Ealert%28%22xicorXSS1%22%29%3C%2FsCript%3E&lname=%22xicorr%3E%3CsCript%3Ealert%28%22xicorXSS2%22%29%3C%2FsCript%3E
```

2. Observe that a JavaScript alert popup is triggered from the `fname` parameter payload.

## Payload Used

```html
"xicorr><sCript>alert("xicorXSS1")</sCript>
```

## Proof of Concept

The application reflects attacker-controlled input from the `fname` parameter directly into the page without proper sanitization.

As a result, arbitrary JavaScript executes automatically when the crafted URL is visited.

### Screenshot 1 — Reflected XSS Triggered via `fname` Parameter

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/5c0923ff-bb02-404e-b981-3a640e8b1d8e" />


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
