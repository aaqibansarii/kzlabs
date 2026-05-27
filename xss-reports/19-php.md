# Stored Cross-Site Scripting (XSS) via Profile Location Field

## Summary

A Stored Cross-Site Scripting (XSS) vulnerability exists in the `Location` field of the user profile management functionality. User-supplied input is stored and rendered without proper sanitization, leading to persistent JavaScript execution in users’ browsers.

---

## Vulnerable Endpoint

```text id="u4p9ad"
http://kzlabs.com/19.php
```

---

## Vulnerable Input Field

```text id="x2m8qa"
Location
```

---

## Payload Used

```html id="h7n3we"
<sCript>alert("x3")</sCript>
```

---

## Steps to Reproduce

1. Open the following page in a browser:

   ```text
   http://kzlabs.com/19.php
   ```

2. Enter the XSS payload into the `Location` field.

3. Submit the profile update form.

4. Observe that the payload is stored and executed when the profile information is rendered.

---

## Proof of Concept

```text id="k6r1ps"
http://kzlabs.com/19.php
```

### Screenshot

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/29687847-4165-4acc-9a7e-58c26f92e3b1" />

---

## Impact

* Session hijacking
* Cookie theft
* Persistent JS execution

---

## Recommendations for Fix

* Encode output
* Validate input
* Sanitize stored content
* Secure rendering
