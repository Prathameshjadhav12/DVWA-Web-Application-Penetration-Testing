# File Upload Security

**Evidence status:** Attempted; no conclusive evidence included in the reviewed screenshots  
**Lab module:** DVWA File Upload

## Objective
Assess whether the upload feature safely validates file content, type, name, and storage location.

## Evidence status
The reviewed screenshots do not conclusively demonstrate an unsafe upload or a successful bypass.

## What to document in a future test
- The normal multipart upload request.
- Server response and resulting stored-file behavior.
- Whether validation relies only on the filename or client-supplied MIME type.
- Whether uploaded files are stored outside the web root or served as inert content.
- Safe tests using harmless files in the local lab.

## Remediation
- Use allowlisted file types and verify file content server-side.
- Generate server-side filenames.
- Enforce size limits.
- Store uploads outside the web root where possible.
- Disable execution in upload directories.
- Apply malware scanning where appropriate.
