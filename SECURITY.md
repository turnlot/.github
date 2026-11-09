# Security Policy

Security is an important part of TurnLot's engineering practices. We are committed to protecting dealership data, maintaining secure infrastructure, and responsibly addressing security vulnerabilities.

## Scope

This policy covers TurnLot's hosted services, including the TurnLot web application and API at `turnlot.ai` and its subdomains.

## Reporting a Vulnerability

If you discover a potential security vulnerability, please report it privately by email to **[security@turnlot.ai](mailto:security@turnlot.ai)**.

**Do not open a public GitHub issue or pull request to disclose a security vulnerability.**

Please include:

- A description of the issue and the affected service or URL.
- Steps to reproduce.
- The potential impact.

We will acknowledge your report, review it, and prioritize remediation based on severity and potential impact.

## Supported Versions

TurnLot is a hosted service. Security fixes are applied to the currently deployed version.

## Responsible Disclosure

We ask security researchers to:

- Avoid accessing, modifying, or disclosing data belonging to TurnLot or its customers.
- Avoid degrading the availability of TurnLot's services.
- Allow reasonable time for investigation and remediation before publicly disclosing a reported vulnerability.

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

## Policy Updates

This policy may be updated as TurnLot's platform, infrastructure, and security requirements evolve.
