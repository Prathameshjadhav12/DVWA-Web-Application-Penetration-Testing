# Brute-Force Testing

**Evidence status:** Intruder activity observed; outcome inconclusive  
**Lab module:** DVWA Brute Force  
**Evidence folder:** `../Evidence/Brute-Force/`

## Objective
Evaluate how the login endpoint responds to repeated authentication attempts in the local lab.

## Method
The login request was observed and Intruder was configured with username/password payload positions.

## Observation
A response displayed a welcome message for an administrator account. The available screenshot does not conclusively associate that response with a specific payload pair or establish the full result set.

## Potential impact if controls are insufficient
Weak or reused credentials may be guessed, potentially resulting in account compromise.

## Remediation
- Rate-limit authentication attempts.
- Add progressive delays and abuse monitoring.
- Enable multi-factor authentication.
- Alert on repeated failed logins.
- Use strong password storage and breached-password screening.

## Evidence limitations
Do not claim a confirmed credential discovery until the exact request, payload pair, and corresponding response are documented.
