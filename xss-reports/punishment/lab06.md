## Title

Reflected Cross-Site Scripting (XSS) via `fname` Parameter in Punishment Page

## Vulnerability Type

Reflected XSS

## Summary

The application reflects user-controlled input from the `fname` parameter directly into the HTML response without proper sanitization or output encoding.

By injecting a crafted HTML payload, arbitrary JavaScript execution can be triggered in the victim’s browser.

The vulnerability was confirmed using a `<details>` element with the `ontoggle` event handler.

## Vulnerable Endpoint

```http id="07j6n5"
http://kzlabs.com/punishment/6.php?fname=%3Cdetails+open+ontoggle%3Dalert%281%29%3E&lname=%3Cdetails+open+ontoggle%3Dalert%281%29%3E
```

### Vulnerable Parameter

```http id="q4hf0h"
fname
```

## Steps to Reproduce

1. Open the following URL in a browser:

```http id="i3stte"
http://kzlabs.com/punishment/6.php?fname=%3Cdetails+open+ontoggle%3Dalert%281%29%3E&lname=%3Cdetails+open+ontoggle%3Dalert%281%29%3E
```

2. Observe that a JavaScript alert popup appears automatically.

3. This confirms that the `fname` parameter is reflected without proper sanitization.

## Payload Used

```html id="fgk62f"
<details open ontoggle=alert(1)>
```

## Proof of Concept

The payload executes automatically when the page renders, resulting in arbitrary JavaScript execution in the browser.

### Screenshot 1 — XSS Payload Execution

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/92774d7c-d9a3-4355-b569-3dbbfa5b5d72" />


## Impact

* Session hijacking
* Cookie theft
* Arbitrary JavaScript execution

## Recommendations for Fix

* Properly encode output before rendering user input
* Validate and sanitize all incoming input
* Avoid insecure client-side rendering of unsanitized data
