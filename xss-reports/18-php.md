# Stored Cross-Site Scripting (XSS) via Comment Section

## Summary

A Stored Cross-Site Scripting (XSS) vulnerability exists in the comment functionality of the application. User-supplied input is stored in the backend database and rendered without proper sanitization, allowing persistent JavaScript execution in users’ browsers.

---

## Vulnerable Endpoint

```text id="g6p2ar"
http://kzlabs.com/18.php
```

---

## Vulnerable Input Field

```text id="r3n8kd"
Comment Section
```

---

## Payload Used

```html id="q8m4ye"
"><details open ontoggle=confirm('Xicorr')>
```

---

## Steps to Reproduce

1. Open the following page in a browser:

   ```text
   http://kzlabs.com/18.php
   ```

2. Submit the XSS payload in the comment section.

3. Observe that the payload is stored and rendered back in the comments area.

4. When the page loads, the JavaScript executes automatically and triggers a popup dialog.

---

## Proof of Concept

```text id="v1d7sx"
"><details open ontoggle=confirm('Xicorr')>
```
<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/d7e71388-0a7d-4fd4-a61b-bb6663bf34ef" />

---

## Impact

* Session hijacking
* Cookie theft
* Persistent JS execution

---

## Recommendations for Fix

* Encode output
* Validate input
* Sanitize stored content
* Secure rendering
