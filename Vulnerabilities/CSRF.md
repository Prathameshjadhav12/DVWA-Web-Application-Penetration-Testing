# Cross-Site Request Forgery (CSRF)

**Evidence status:** Attempted; no conclusive evidence included in the reviewed screenshots  
**Lab module:** DVWA CSRF

## Objective
Determine whether a state-changing request can be triggered without adequate anti-CSRF protection.

## Evidence status
The available reviewed screenshot set does not establish whether the request was vulnerable or protected.

## What to document in a future test
- The normal state-changing request.
- Whether a unique, validated anti-CSRF token is present.
- Whether the server checks Origin/Referer where appropriate.
- Whether cookie SameSite settings provide defense in depth.
- A safe local reproduction and the resulting state change.

## Remediation
- Use unpredictable anti-CSRF tokens and validate them server-side.
- Set appropriate SameSite cookie attributes.
- Validate Origin/Referer as defense in depth.
- Require re-authentication for sensitive actions where appropriate.
