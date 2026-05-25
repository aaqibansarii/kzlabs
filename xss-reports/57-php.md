## Title

Cross-Site Scripting (XSS) via `returnTo` Parameter Using `javascript:` URI

## Vulnerability Type

Reflected XSS

## Summary

The `returnTo` parameter accepts a `javascript:` URI without proper validation or sanitization, allowing arbitrary JavaScript execution when the user interacts with the affected functionality.

The payload executes after clicking the **Continue** button on the account confirmation page.

## Vulnerable Endpoint

```http
https://kzlabs.com/57.php
```

### Vulnerable Parameter

```http
returnTo
```

## Steps to Reproduce

1. Open the following URL:

```http
https://kzlabs.com/57.php?returnTo=javascript:alert(document.cookie)
```

2. Fill the required form fields if needed.

3. Click on the **Continue** button.

4. Observe that a JavaScript alert popup is triggered.

## Payload Used

```javascript
javascript:alert(document.cookie)
```

## Proof of Concept

The application allows user-controlled input inside the `returnTo` parameter without validating dangerous URI schemes such as `javascript:`.

When the victim clicks the **Continue** button, the payload executes in the browser context.

### Screenshot 1 — Alert Popup Triggered After Clicking Continue

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/fd80283f-5eaa-4b6d-9612-6392b4485495" />


## Impact

An attacker can exploit this vulnerability to:

- Execute arbitrary JavaScript in the victim’s browser
- Hijack authenticated user sessions
- Perform unauthorized actions on behalf of users
- Exfiltrate sensitive information
- Conduct phishing attacks using trusted application context

## Recommendations for Fix

- Reject dangerous URI schemes such as:`javascript`
  
- Strictly validate and sanitize the `returnTo` parameter
- Allow only trusted internal paths or approved domains
- Implement contextual output encoding where applicable
- Consider deploying a strict Content Security Policy (CSP)
