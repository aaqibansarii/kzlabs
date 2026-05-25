## Title

Stored Cross-Site Scripting (XSS) via Article Body HTML Editor

## Vulnerability Type

Stored XSS

## Summary

The article body HTML editor allows arbitrary HTML/JavaScript input without proper sanitization before storing and rendering it back to users.

An attacker can inject malicious JavaScript inside the article body, which executes automatically whenever the article page is viewed.

## Vulnerable Endpoint

```http
https://kzlabs.com/61.php
```

## Vulnerable Parameter

```http
Article Body (HTML Editor)
```

## Steps to Reproduce

1. Log in to your account.

2. Navigate to the article creation page:

```http
https://kzlabs.com/61.php
```

3. Switch the editor to the `HTML` tab.

4. Insert the following payload inside the article body:

```html
"><img src=a onerror=alert("xicorr")>
```

5. Publish the article.

6. Visit the article listing/page.

7. Observe that a JavaScript alert popup is triggered automatically.

## Payload Used

```html
"><img src=a onerror=alert("xicorr")>
```

## Proof of Concept

The application stores arbitrary HTML input from the article body without sanitization and later renders it directly in the browser.

As a result, attacker-controlled JavaScript executes automatically when the article page loads.

### Screenshot 1 — Malicious Payload Injected in HTML Editor

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/d5c14675-8b13-406a-9750-3c57ea3c0b11" />


### Screenshot 2 — Stored XSS Triggered After Publishing

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/0b57a531-ac2f-4ad5-a210-a7117e2ea7db" />


## Impact

An attacker can exploit this vulnerability to:

- Execute arbitrary JavaScript in other users’ browsers
- Hijack authenticated user sessions
- Perform unauthorized actions on behalf of users
- Exfiltrate sensitive information
- Conduct phishing attacks using trusted application context

## Recommendations for Fix

- Properly sanitize and encode all user-controlled HTML before rendering
- Disallow dangerous HTML tags and event handlers
- Avoid rendering raw user input directly into the DOM
- Apply contextual output encoding
- Implement a strict Content Security Policy (CSP)
