## Title

Stored Cross-Site Scripting (XSS) via `Signature` Field in Profile Settings

## Vulnerability Type

Stored XSS

## Summary

The `Signature` field in the profile settings allows arbitrary HTML/JavaScript input without proper sanitization before storing and rendering it back to users.

An attacker can inject malicious JavaScript into the signature field, which executes automatically after saving the profile and whenever the signature is rendered.

## Vulnerable Endpoint

```http
https://kzlabs.com/62.php
```

## Vulnerable Parameter

```http
Signature
```

## Steps to Reproduce

1. Log in to your account.

2. Navigate to:

```http
https://kzlabs.com/62.php
```

3. Insert the following payload into the `Signature` field:

```html
"><img src=a onerror=alert("xicorr3")>
```

4. Click on **Save Profile**.

5. Observe that a JavaScript alert popup is triggered.

## Payload Used

```html
"><img src=a onerror=alert("xicorr3")>
```

## Proof of Concept

The application stores arbitrary HTML input from the `Signature` field without proper sanitization and renders it directly inside the page.

As a result, attacker-controlled JavaScript executes automatically when the signature is rendered after saving.

### Screenshot 1 — Malicious Payload Injected into Signature Field

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/2225d404-dabe-47a4-9291-6b33756be3c7" />


### Screenshot 2 — Stored XSS Triggered After Saving Profile

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/598e938a-25c0-4480-8d64-10da20401a5a" />


## Impact

An attacker can exploit this vulnerability to:

- Execute arbitrary JavaScript in other users’ browsers
- Hijack authenticated user sessions
- Perform unauthorized actions on behalf of users
- Exfiltrate sensitive information
- Conduct phishing attacks using trusted application context

## Recommendations for Fix

- Properly sanitize and encode all user-controlled input before rendering
- Disallow dangerous HTML tags and event handlers
- Avoid rendering raw HTML from profile fields
- Apply contextual output encoding
- Implement a strict Content Security Policy (CSP)
