# DOM-Based Cross-Site Scripting (XSS) via `location.hash`

## Summary

A DOM-Based Cross-Site Scripting (XSS) vulnerability exists in the application where user-controlled input from `location.hash` is processed by client-side JavaScript without proper sanitization.

The payload executes in the browser, resulting in arbitrary JavaScript execution.

---

## Vulnerable Endpoint

```text id="w65o6n"
http://kzlabs.com/68.php
```

---

## Payload Used

```html id="z7clt7"
<Script>alert(1)</script>
```

---

## Steps to Reproduce

1. Open the following URL in a browser:

   ```text
   http://kzlabs.com/68.php/#<Script>alert(1)</script>
   ```

2. Observe that the JavaScript payload executes in the browser.

3. Inspect the DOM to confirm that the payload is processed through `location.hash`.

---

## Proof of Concept

```text id="f2y5wo"
http://kzlabs.com/68.php/#<Script>alert(1)</script>
```

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/5c40bc65-a147-4513-9f5a-d4ebbabb8c5a" />


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
