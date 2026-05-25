## Title

Stored Cross-Site Scripting (XSS) via Report Name Field in Network Reports

## Vulnerability Type

Stored XSS

## Summary

The `Report Name` field in the Network Reports functionality does not properly sanitize user-controlled input before storing and rendering it back to users.

An attacker can inject arbitrary HTML/JavaScript payloads into the report name, which executes automatically whenever any authenticated user views the Reports page.

## Vulnerable Endpoint

```http
https://kzlabs.com/60.php
```

## Vulnerable Parameter

```http
Report Name
```

## Steps to Reproduce

1. Navigate to the following page:

```http
https://kzlabs.com/60.php
```

2. Click on **New Network Report**.

3. Enter the following payload inside the `Report Name` field:

```html
"><img src=a onerror=alert("xicorr")>
```

4. Fill the remaining required fields and save the report.

5. Return to the Reports page.

6. Observe that a JavaScript alert popup is triggered automatically when the stored payload is rendered.

## Payload Used

```html
"><img src=a onerror=alert("xicorr")>
```

## Proof of Concept

The application stores the malicious payload without sanitization and later renders it directly inside the Reports page.

As a result, arbitrary JavaScript executes automatically whenever the page is viewed.

### Screenshot 1 — Malicious Payload Injected in Report Name

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/fea397a8-652c-4c9b-a648-053ae87a5456" />


### Screenshot 2 — Stored XSS Triggered on Reports Page

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/c0038673-dd1b-4194-b88f-0b32ed16592a" />


## Impact

An attacker can exploit this vulnerability to:

- Execute arbitrary JavaScript in other users’ browsers
- Hijack authenticated user sessions
- Perform unauthorized actions on behalf of users
- Exfiltrate sensitive information
- Conduct phishing attacks using trusted application context

## Recommendations for Fix

- Properly sanitize and encode all user-controlled input before rendering it
- Avoid rendering raw HTML from user input
- Apply contextual output encoding
- Validate and filter dangerous HTML tags and event handlers
- Implement a strict Content Security Policy (CSP)
