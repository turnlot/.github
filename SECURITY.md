# Security Policy

Security is an important part of TurnLot's engineering practices. We are committed to protecting dealership data, maintaining secure infrastructure, and responsibly addressing security vulnerabilities.

This policy applies to all repositories maintained by the [TurnLot GitHub organization](https://github.com/turnlot).

## Reporting a Vulnerability

If you discover a potential security vulnerability, please report it privately.

**Do not open a public GitHub issue or pull request to disclose a security vulnerability.**

To report a vulnerability:

1. Navigate to the affected repository's **Security** tab.
2. Select **Report a vulnerability**, if private vulnerability reporting is enabled.
3. Provide a description of the issue, affected components, reproduction steps, and potential impact.

If private vulnerability reporting is unavailable, contact TurnLot through an authorized private communication channel.

We will review security reports and prioritize remediation based on severity and potential impact.

## Supported Versions

TurnLot is currently under active development.

Security fixes are generally applied to the latest maintained version of each component. Older releases may not receive security updates.

## Security Practices

TurnLot follows these principles across its repositories.

### Secrets and Credentials

- Never commit API keys, passwords, access tokens, or other credentials.
- Use approved secret-management mechanisms for application credentials.
- Prefer short-lived credentials and IAM roles over long-lived access keys.
- Apply least-privilege access policies.

### Data Protection

- Treat dealership CRM data, customer information, and inventory records as confidential.
- Do not commit real customer data, CRM exports, or sensitive production records.
- Use synthetic or appropriately anonymized data for development and testing.
- Minimize the collection, storage, and exposure of sensitive information.
- Avoid including customer information in application logs or error reports.

### Infrastructure and Dependencies

- Manage cloud infrastructure through reviewed infrastructure-as-code changes.
- Restrict access to databases, storage, and cloud resources.
- Keep dependencies updated and address known vulnerabilities.
- Require appropriate authentication and authorization for protected services.
- Review changes affecting security-sensitive infrastructure and application components.

### AI-Assisted Processing

- Validate AI-generated interpretations before persisting structured data.
- Treat imported files and external content as untrusted inputs.
- Avoid unnecessarily transmitting sensitive dealership or customer information to AI providers.
- Ensure AI-assisted processing cannot bypass established authorization or data-validation controls.

## Responsible Disclosure

We ask security researchers to avoid accessing, modifying, or disclosing data belonging to TurnLot or its customers.

Please provide reasonable time for investigation and remediation before publicly disclosing a reported vulnerability.

## Policy Updates

This policy may be updated as TurnLot's platform, infrastructure, and security requirements evolve.