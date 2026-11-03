# Evidence Handling

Screenshots are grouped by the area they support. Before publishing:
- Review every image for session cookies, CSRF tokens, credentials, usernames, IP addresses, and personal information.
- Redact secrets without obscuring the relevant request/response evidence.
- Never commit live session cookies or authentication tokens.
- Keep original unredacted evidence private and secure.
