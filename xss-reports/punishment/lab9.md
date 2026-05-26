## Title

Reflected Cross-Site Scripting (XSS) via `lname` Parameter in Punishment Page

## Vulnerability Type

Reflected XSS

## Summary

The application reflects user-controlled input from the `lname` parameter directly into the HTML response without proper sanitization or output encoding.

An attacker can inject malicious HTML/JavaScript payloads which execute in the victim’s browser.

The vulnerability was confirmed using a `<details>` element with the `ontoggle` event handler.

## Vulnerable Endpoint

```http
http://kzlabs.com/punishment/9.php?fname=aaaa&lname=%3Cdetails+open+ontoggle%3Dalert%281%29%3E
```

### Vulnerable Parameter

```http
lname
```

## Steps to Reproduce

1. Open the following URL in a browser:

```http
http://kzlabs.com/punishment/9.php?fname=aaaa&lname=%3Cdetails+open+ontoggle%3Dalert%281%29%3E
```

2. Observe that a JavaScript alert popup appears automatically.

3. This confirms that the `lname` parameter is vulnerable to reflected XSS.

## Payload Used

```html
<details open ontoggle=alert(1)>
```

## Proof of Concept

The payload executes automatically when the page loads, leading to arbitrary JavaScript execution.

### Screenshot 1 — XSS Payload Execution

<img width="1920" height="1078" alt="image" src="https://github.com/user-attachments/assets/f73c0436-9da2-410a-b248-4d149e2d938b" />


## Impact

* Session hijacking
* Cookie theft
* JS execution

## Recommendations for Fix

* Encode output
* Validate input
* Secure rendering
