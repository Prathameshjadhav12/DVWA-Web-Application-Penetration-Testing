# OS Command Injection

**Evidence status:** Demonstrated in local DVWA  
**Lab module:** DVWA Command Injection  
**Evidence folder:** `../Evidence/Command-Injection/`

## Objective
Check whether user-controlled input is passed to an operating-system command without safe handling.

## Method
A loopback address was supplied with a command separator and a harmless marker command. The request and response were inspected in Burp Suite.

## Observation
The marker appeared in the response after the ping output. This demonstrates command execution in the local lab context.

## Potential impact
Depending on the web server account's privileges, command injection can expose files, disclose data, disrupt services, or enable further compromise.

## Remediation
- Avoid shell commands when a library/API is available.
- Do not concatenate untrusted input into shell commands.
- Use safe process APIs and strict allowlists if execution is unavoidable.
- Run the application with least privilege.
- Monitor unexpected child-process execution.

## Scope limitation
This was demonstrated only in the local DVWA lab.
