# Testing Methodology

## Scope
The assessment covered selected DVWA modules on the local lab at `127.0.0.1:42001`. The application is intentionally vulnerable and is not representative of a production environment.

## Process
1. Confirm the target is the local lab.
2. Configure Burp Proxy and verify interception.
3. Capture a baseline request for each module.
4. Inspect parameters, headers, cookies, and response behavior.
5. Use Repeater for controlled manual request changes.
6. Use Intruder for bounded payload testing in the lab.
7. Compare baseline and test responses.
8. Capture evidence and redact secrets.
9. Assign a status: confirmed, strong evidence, reflection observed, inconclusive, or not demonstrated.
10. Recommend defensive controls.

## Evidence quality
A finding should include the relevant request, response, affected parameter, observed behavior, and enough context to reproduce it. A screenshot showing a tool configuration alone is evidence of workflow, not proof of a vulnerability.
