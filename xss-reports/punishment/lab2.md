## Title

Reflected Cross-Site Scripting (XSS) via `lname` Parameter

## Vulnerability Type

Reflected XSS

## Summary

The application reflects user-controlled input from the `lname` parameter without proper sanitization or output encoding, allowing arbitrary JavaScript execution in the victim’s browser.

The `fname` parameter appears to be properly handled, while the `lname` parameter remains vulnerable.

## Vulnerable Endpoint

```http
http://kzlabs.com/punishment/2.php?fname=%22xicorr%3E%3CsCript%3Ealert%28%22xicorXSS1%22%29%3C%2FsCript%3E&lname=%22xicorr%3E%3CsCript%3Ealert%28%22xicorXSS2%22%29%3C%2FsCript%3E
```

## Vulnerable Parameter

```http
lname
```

## Steps to Reproduce

1. Open the following URL in a browser:

```http
http://kzlabs.com/punishment/2.php?fname=%22xicorr%3E%3CsCript%3Ealert%28%22xicorXSS1%22%29%3C%2FsCript%3E&lname=%22xicorr%3E%3CsCript%3Ealert%28%22xicorXSS2%22%29%3C%2FsCript%3E
```

2. Observe that a JavaScript alert popup is triggered from the `lname` parameter payload.

## Payload Used

```html
"xicorr><sCript>alert("xicorXSS2")</sCript>
```

## Proof of Concept

The application reflects attacker-controlled input from the `lname` parameter directly into the page without proper sanitization.

As a result, arbitrary JavaScript executes automatically when the crafted URL is visited.

### Screenshot 1 — Reflected XSS Triggered via `lname` Parameter

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/b48b4378-5e09-4b77-b684-b4e8bccb0fcf" />


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
