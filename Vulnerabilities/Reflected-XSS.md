# Reflected Cross-Site Scripting (XSS)

**Evidence status:** Reflection observed; JavaScript execution unconfirmed  
**Lab module:** DVWA Reflected XSS  
**Evidence folder:** `../Evidence/Reflected-XSS/`

## Objective
Check whether user-supplied input is reflected into an HTML response without appropriate output encoding.

## Method
A script-like input was submitted through the vulnerable parameter and the response was inspected.

## Observation
The input was reflected into the response. However, the captured JavaScript payload was malformed, so the screenshot does not prove that the browser executed JavaScript.

## Potential impact if executable
Attacker-controlled script may execute in a victim's browser in the vulnerable site's origin, potentially enabling page manipulation or unauthorized actions as the victim.

## Remediation
- Apply context-aware output encoding.
- Use safe templating and avoid unsafe DOM sinks.
- Validate input as an additional control.
- Consider a restrictive Content Security Policy as defense in depth.

## Evidence needed to confirm execution
Capture a corrected harmless test in the local lab and document the browser behavior alongside the request and response.
