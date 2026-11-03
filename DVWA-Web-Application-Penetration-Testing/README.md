# DVWA Web Application Penetration Testing

A practical web application security testing project using **Damn Vulnerable Web Application (DVWA)** and **Burp Suite Community Edition** in a controlled local lab.

> **Project type:** Educational / personal cybersecurity portfolio  
> **Environment:** Local DVWA instance (`127.0.0.1:42001`)  
> **Testing scope:** Selected DVWA vulnerability modules and Burp Suite workflows

## 1. Project Overview

The purpose of this project is to practice a structured web application security assessment: intercepting HTTP traffic, modifying requests, observing server responses, documenting security weaknesses, and recommending mitigations.

The project focuses on demonstrating a repeatable testing process rather than simply collecting screenshots.

## 2. Objectives

- Understand how common web vulnerabilities work.
- Use Burp Suite Proxy to intercept and inspect HTTP requests.
- Use Repeater to modify and resend requests.
- Use Intruder to understand controlled payload testing.
- Compare observed application behavior with expected secure behavior.
- Record evidence, impact, limitations, and remediation advice.
- Communicate results accurately without overstating what the evidence proves.

## 3. Lab Environment

| Item | Details |
|---|---|
| Target application | Damn Vulnerable Web Application (DVWA) |
| Target address | `http://127.0.0.1:42001` |
| Interception tool | Burp Suite Community Edition |
| Testing scope | Local lab only |
| Security level | Low for the captured demonstrations unless otherwise stated |
| Authorization | Owned/local intentionally vulnerable training application |

**Safety note:** The address above is a loopback address. Do not reuse these tests against systems you do not own or have explicit permission to assess.

## 4. Tools

- **DVWA:** Intentionally vulnerable web application for security training.
- **Burp Suite Community Edition:** HTTP interception and request analysis.
- **Web browser:** Used to access DVWA through the configured Burp proxy.

## 5. Testing Workflow

1. Start the local DVWA lab.
2. Configure the browser to use Burp Suite as its proxy.
3. Confirm that requests appear in Proxy HTTP history.
4. Select a DVWA vulnerability module.
5. Submit a normal request to establish baseline behavior.
6. Inspect the request and response.
7. Where appropriate, send the request to Repeater or Intruder.
8. Change one input at a time and observe the response.
9. Save screenshots with sensitive session data redacted.
10. Document the result, impact, limitations, and remediation.

## 6. Modules and Evidence Status

The status below reflects only the screenshots reviewed for this project. An attempted test is not automatically a confirmed vulnerability.

| Area | Evidence status | Summary |
|---|---|---|
| SQL Injection | Strong demonstration evidence | A boolean-style input returned multiple user records. |
| Command Injection | Demonstrated in the lab | A command separator and harmless marker command produced the marker in the response. |
| Reflected XSS | Reflection observed; execution unconfirmed | Input was reflected into the response, but the captured JavaScript payload was malformed. |
| Brute Force | Activity observed; result inconclusive | Intruder activity and a success-looking response were visible, but payload-to-response mapping was not conclusive. |
| CSRF | Attempted; no usable result included | No reviewed screenshot conclusively demonstrates exploitability or protection. |
| File Upload | Attempted; no usable result included | No reviewed screenshot conclusively demonstrates an unsafe upload. |

Proxy and Intruder screenshots also document tool usage. They are not separate vulnerability findings by themselves.

## 7. Key Findings

### Finding 1 — SQL Injection

**Status:** Strong demonstration evidence  
**Evidence:** `Evidence/SQL-Injection/`

A boolean-style SQL input was submitted through the DVWA SQL Injection module. The response displayed multiple user records, consistent with an input that altered the intended database query logic.

**Potential impact:** Depending on the database permissions and query construction, SQL injection can expose, modify, or delete data and may allow authentication bypass.

**Recommended remediation:**
- Use parameterized queries / prepared statements.
- Avoid building SQL statements through string concatenation.
- Apply least-privilege database permissions.
- Validate inputs as an additional control, not as a replacement for parameterization.
- Return generic errors and avoid exposing database details.

### Finding 2 — OS Command Injection

**Status:** Demonstrated in the local lab  
**Evidence:** `Evidence/Command-Injection/`

A request parameter included a loopback address followed by a command separator and a harmless marker command. The marker appeared in the application response, demonstrating that user-controlled input reached an operating-system command context.

**Potential impact:** Depending on the privileges of the web server process, command injection can lead to unauthorized file access, data exposure, service disruption, or broader system compromise.

**Recommended remediation:**
- Avoid invoking operating-system commands where a library/API can perform the task.
- Do not concatenate user input into shell commands.
- If process execution is unavoidable, use safe process APIs with argument arrays and strict allowlists.
- Run the application with least privilege.
- Restrict outbound access and monitor process execution.

### Finding 3 — Reflected Cross-Site Scripting (XSS)

**Status:** Reflection observed; JavaScript execution not confirmed  
**Evidence:** `Evidence/Reflected-XSS/`

The supplied input was reflected into the response as script-like markup. The captured payload was malformed, so the screenshot does not prove that JavaScript executed in the browser.

**Potential impact if executable:** Reflected XSS can allow attacker-controlled script to run in a victim's browser in the security context of the vulnerable site. Depending on the application, this may enable page manipulation or actions performed as the victim.

**Recommended remediation:**
- Contextually encode untrusted output.
- Use framework-provided safe templating.
- Validate input where appropriate.
- Deploy a restrictive Content Security Policy as defense in depth.
- Avoid unsafe DOM sinks such as `innerHTML` for untrusted data.

### Finding 4 — Brute-Force Testing

**Status:** Test activity observed; effectiveness inconclusive  
**Evidence:** `Evidence/Brute-Force/`

Burp Intruder activity against the DVWA brute-force endpoint was visible. A response displayed a welcome message for an administrator account, but the available screenshot does not conclusively link that response to a particular payload or establish the complete test result.

**Potential impact if protections are absent:** Repeated password guessing may lead to account compromise, especially where passwords are weak or reused.

**Recommended remediation:**
- Apply rate limiting and progressive delays.
- Use multi-factor authentication.
- Monitor and alert on repeated failed logins.
- Use breached-password checks and strong password policies.
- Consider account protection controls that resist denial-of-service abuse.

## 8. Limitations

- Testing was performed against an intentionally vulnerable local DVWA instance, not a production application.
- The reviewed evidence is a limited set of screenshots, not a complete request/response export.
- SQL Injection and Command Injection have useful demonstration evidence; other outcomes are qualified as inconclusive where appropriate.
- The reflected XSS screenshot does not prove JavaScript execution.
- The Brute Force screenshot does not conclusively map a successful response to a specific credential pair.
- CSRF and File Upload attempts are not supported by conclusive evidence in the reviewed screenshot set.
- No claim is made that every DVWA module was successfully exploited.

## 9. How to Reproduce

1. Set up DVWA locally using its official installation instructions.
2. Keep the application isolated from public networks.
3. Open Burp Suite Community Edition.
4. Configure the browser to use Burp's proxy listener.
5. Log in to DVWA and set the desired security level.
6. Navigate to a module and capture its HTTP request.
7. Use Repeater or Intruder only within the local lab.
8. Record baseline and modified responses.
9. Save evidence after removing cookies, tokens, passwords, and other secrets.

## 10. Repository Structure

```text
DVWA-Web-Application-Penetration-Testing/
├── README.md
├── Disclaimer.md
├── .gitignore
├── Reports/
│   └── DVWA_Burp_Practical_Assessment_Report.docx
├── Evidence/
│   ├── SQL-Injection/
│   ├── Command-Injection/
│   ├── Reflected-XSS/
│   ├── Brute-Force/
│   ├── Proxy/
│   └── Intruder/
├── Methodology/
│   └── Testing-Methodology.md
└── Vulnerabilities/
    ├── SQL-Injection.md
    ├── Command-Injection.md
    ├── Reflected-XSS.md
    ├── Brute-Force.md
    ├── CSRF.md
    └── File-Upload.md
```

## 11. Learning Outcomes

- HTTP request and response inspection.
- Proxy interception and request modification.
- Repeater-based manual testing.
- Intruder payload-position and attack-type concepts.
- Basic web vulnerability identification.
- Evidence handling and technical reporting.
- Distinguishing confirmed findings from inconclusive tests.

## 12. Disclaimer

This repository is for educational purposes. All demonstrations were conducted in a local, intentionally vulnerable DVWA environment. Only test systems for which you have explicit authorization. Do not use the techniques or payloads in this repository against real systems without written permission.
