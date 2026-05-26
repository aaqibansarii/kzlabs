## Title

Reflected Cross-Site Scripting (XSS) via `fname` Parameter in Punishment Page

## Vulnerability Type

Reflected XSS

## Summary

The application reflects user-controlled input from the `fname` parameter directly into the HTML response without proper sanitization or output encoding.

By injecting a crafted HTML payload, arbitrary JavaScript execution can be triggered in the victim’s browser.

The vulnerability was confirmed using a `<details>` element with the `ontoggle` event handler.

## Vulnerable Endpoint

```http
http://kzlabs.com/punishment/5.php?fname=%3Cdetails+open+ontoggle%3Dalert%281%29%3E&lname=sss
```

### Vulnerable Parameter

```http
fname
```

## Steps to Reproduce

1. Open the following URL in a browser:

```http
http://kzlabs.com/punishment/5.php?fname=%3Cdetails+open+ontoggle%3Dalert%281%29%3E&lname=sss
```

2. Observe that a JavaScript alert popup appears automatically.

3. This confirms that the `fname` parameter is reflected without proper sanitization.

## Payload Used

```html
<details open ontoggle=alert(1)>
```

## Proof of Concept

The payload executes automatically when the page renders, resulting in arbitrary JavaScript execution in the browser.

### Screenshot 1 — XSS Payload Execution

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/b207cdac-4578-4c02-9271-e2682b5c506e" />


## Impact

* Session hijacking
* Cookie theft
* Arbitrary JavaScript execution

## Recommendations for Fix

* Properly encode output before rendering user input
* Validate and sanitize all incoming input
* Avoid insecure client-side rendering of unsanitized data

