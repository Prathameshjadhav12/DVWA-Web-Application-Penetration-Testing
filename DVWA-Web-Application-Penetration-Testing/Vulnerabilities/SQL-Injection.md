# SQL Injection

**Evidence status:** Strong demonstration evidence  
**Lab module:** DVWA SQL Injection  
**Evidence folder:** `../Evidence/SQL-Injection/`

## Objective
Determine whether user-controlled input changes the logic of a database query.

## Method
A baseline request was compared with a request containing a boolean-style SQL input. The request was observed using Burp Suite.

## Observation
The modified request returned multiple user records. This is consistent with SQL injection in the intentionally vulnerable lab.

## Potential impact
Unauthorized data disclosure, data modification or deletion, and possible authentication bypass, depending on the query and database privileges.

## Remediation
- Use prepared statements / parameterized queries.
- Avoid SQL string concatenation with untrusted input.
- Apply least-privilege database permissions.
- Handle errors safely and avoid exposing database details.

## Evidence limitations
The screenshot supports a SQL injection demonstration in DVWA. It does not establish impact on any real application.
