# Engineering Standards

TurnLot's engineering standards establish consistent expectations for software development, testing, security, and maintenance across its repositories.

Standards apply across components while allowing repository-specific tools and implementation decisions.

## Code Quality

- Code must be readable, maintainable, and organized around clearly defined responsibilities.
- Components must respect established architectural boundaries and interfaces.
- Reusable functionality should minimize duplication without introducing unnecessary abstraction.
- Public interfaces and non-obvious behavior must be documented.
- Logical sections should use consistent, language-appropriate headings or comment separators where they improve readability.
- Code must follow repository-specific formatting, linting, and type-checking conventions.

### Comment Conventions

Logical sections and subsections should use consistent comment separators where they improve readability.

**Sections**

```text
# ========================
# ----- Section Name -----
# ========================
```

**Subsections**

```text
# --- Subsection Name ---
```

These conventions are preferred for Makefiles, configuration files, and scripts. They should not replace appropriate code organization or introduce unnecessary visual clutter.

## Testing & CI/CD

- New functionality and bug fixes should include appropriate automated tests.
- Tests must be reliable, reproducible, and independent of production data.
- Required automated checks must pass before changes are merged.
- Builds, deployments, and package publishing must follow controlled, reproducible processes.
- Production changes must be traceable to their source revisions.

## Version Control

- Changes should be developed through focused branches and pull requests.
- Commits must describe meaningful, logically related changes.
- Pull requests must summarize changes, relevant testing, and potential impacts.
- Protected branches must restrict unauthorized direct changes.

## Dependencies & Versioning

- Dependencies must be explicitly declared and appropriately version-constrained.
- Shared libraries must be versioned independently of consuming applications.
- Published package versions must be immutable.
- Breaking interface changes must be documented and coordinated with affected consumers.

## Security

- Secrets, credentials, and sensitive customer information must not be committed to source control.
- Access permissions must follow the principle of least privilege.
- Sensitive information must be protected during storage, processing, and transmission.
- External inputs must be validated before use in security-sensitive operations.

## Data Integrity

- Database schema changes must use versioned migrations and account for existing data.
- Data transformations and AI-assisted interpretations must be validated before persistence.
- Processing must preserve data integrity and support safe retries where applicable.

## Documentation

- Each repository must maintain a README describing its purpose and development setup.
- Documentation must be updated alongside changes affecting documented behavior.
- Significant technical decisions must remain consistent with TurnLot's shared architectural documentation.

## Operations

- Applications and workflows must provide sufficient logging and diagnostics to investigate failures.
- Operational processes must support recovery from expected failure conditions.