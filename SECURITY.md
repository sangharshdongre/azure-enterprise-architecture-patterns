# Security Policy

## Reporting a security concern

Do not publicly disclose a suspected vulnerability, exposed credential or
sensitive-data issue through a public discussion.

Open a private security advisory when private vulnerability reporting is
available. Otherwise, contact the repository owner through an appropriate
private professional channel.

## Sensitive information

Contributions must not include:

- Credentials, tokens, keys or certificates
- Customer or employer-confidential information
- Production IP addresses or hostname
- Tenant, subscription or resource identifiers from real environments
- Proprietary source code or documentation
- Personal or regulated data

Any exposed credential must be treated as compromised and revoked. Removing
it from the latest commit alone is not sufficient because Git history may
retain previous content.

## Supported content

Only the latest repository release is actively maintained.

## Reference-material limitation

The architecture patterns and examples in this repository are not production
security guarantees. Each implementation requires its own threat model,
security assessment and organizational approval.
