# Turnlot Architecture

## Overview

Turnlot is a dealership lead-matching platform that identifies opportunities to reconnect existing CRM leads with vehicles in dealership inventory.

The system ingests dealership CRM and inventory data, normalizes and persists that data, identifies relevant lead-to-vehicle matches, and presents results through a secure, dealership-facing dashboard.

Turnlot uses a multi-repository architecture with clearly defined responsibilities and shared internal Python packages.

## Repository Structure

The Turnlot GitHub organization contains six repositories:

| Repository | Responsibility | Technology |
|---|---|---|
| `database` | Database models, migrations, and persistence | Python, SQLAlchemy, Alembic, PostgreSQL |
| `ingestion` | CRM and inventory data ingestion | Python |
| `matching` | Lead-to-vehicle matching engine | Python |
| `api` | Backend API, authentication, and application logic | Python, FastAPI |
| `dashboard` | Dealership-facing web application | TypeScript, Next.js |
| `infrastructure` | Cloud infrastructure and deployment configuration | Terraform, AWS |

Each repository owns a distinct responsibility and can evolve independently, subject to its dependencies and integration contracts.

## System Architecture

```text
              Dealership Users
                     |
                     v
             +---------------+
             |   Dashboard   |
             |    Next.js    |
             +---------------+
                     |
                   HTTPS
                     |
                     v
             +---------------+
             |      API      |
             |    FastAPI    |
             +---------------+
                     |
                     v
             +---------------+
             |   PostgreSQL  |
             +---------------+
                     ^
                     |
          +----------+----------+
          |                     |
  +---------------+    +---------------+
  |   Ingestion   |    |    Matching   |
  |  Batch Jobs   |    |  Batch Jobs   |
  +---------------+    +---------------+
          ^                     ^
          |                     |
    CRM / Inventory      Stored Leads
       Exports           & Inventory
```

The diagram illustrates the logical system. Components do not necessarily represent independently running services.

## Components

### Database

**Repository:** `turnlot/database`

Owns the shared data model and persistence layer.

Responsibilities include:

- SQLAlchemy ORM models
- PostgreSQL schema definitions
- Alembic database migrations
- Database relationships and constraints
- Shared persistence utilities

Published internally as `turnlot-db` through AWS CodeArtifact.

The database package is used by applications requiring direct database access.

### Ingestion

**Repository:** `turnlot/ingestion`

Responsible for importing dealership data into Turnlot.

Responsibilities include:

- Parsing CRM lead exports
- Parsing vehicle inventory exports
- Validating incoming records
- Normalizing data formats
- Deduplicating and updating existing records
- Persisting normalized data
- Reporting import results and errors

Initially supports manually supplied files, such as CSV exports.

Future implementations may support direct CRM integrations and automated synchronization.

Ingestion runs as an independent Python application and consumes `turnlot-db`.

It does not initially require publishing as a reusable package.

### Matching

**Repository:** `turnlot/matching`

Contains the core lead-to-vehicle matching logic.

Responsibilities include:

- Evaluating lead vehicle preferences
- Filtering inventory against lead interests
- Applying matching rules
- Persisting match results
- Preventing duplicate matches

Matching logic is maintained independently from data ingestion and presentation.

Published internally as `turnlot-matching` through AWS CodeArtifact.

Consumes `turnlot-db`.

### API

**Repository:** `turnlot/api`

Provides the backend interface for Turnlot applications.

Planned responsibilities include:

- Authenticated endpoints
- Organization-scoped data access
- Lead and inventory retrieval
- Match retrieval and filtering
- Dashboard-facing business logic
- Authorization and access control

Built using FastAPI.

The API consumes `turnlot-db` and may consume `turnlot-matching` when synchronous matching functionality is required.

Batch matching can execute independently of the API.

### Dashboard

**Repository:** `turnlot/dashboard`

Provides the dealership-facing web application.

Planned responsibilities include:

- User login and authenticated sessions
- Displaying matched leads and vehicles
- Filtering and reviewing matches
- Presenting relevant lead and inventory details
- Displaying processing and import status where useful

Built using Next.js and TypeScript.

The dashboard communicates with the API over HTTPS.

It does not directly access PostgreSQL or depend on internal Python packages.

### Infrastructure

**Repository:** `turnlot/infrastructure`

Defines and manages Turnlot's cloud infrastructure.

Responsibilities include:

- AWS account configuration
- Networking and security groups
- IAM roles and policies
- GitHub Actions OIDC integration
- AWS CodeArtifact configuration
- Terraform state management
- Application deployment infrastructure

Infrastructure is managed through Terraform.

## Dependency Management

Turnlot uses versioned internal Python packages distributed through AWS CodeArtifact.

The intended dependency relationships are:

```text
turnlot-db
    |
    +-- ingestion
    |
    +-- turnlot-matching
    |         |
    |         +-- api (if required)
    |
    +-- api

dashboard -- HTTPS --> api
```

The `infrastructure` repository provisions resources but is not an application-level package dependency.

### Principles

1. Shared packages expose reusable functionality rather than application-specific behavior.
2. Applications depend on shared packages through explicitly declared versions.
3. Dependencies should flow in one direction without circular references.
4. Database schema changes are managed through versioned migrations.
5. Internal packages are published through CodeArtifact when independent distribution is necessary.
6. Applications should not require direct source-code dependencies on other application repositories.

## Pilot Execution Model

The initial pilot is designed for one dealership.

The expected workflow is:

1. Receive CRM lead and inventory exports.
2. Run ingestion to validate, normalize, and persist records.
3. Execute matching against the latest available inventory.
4. Persist newly identified matches.
5. Allow authenticated dealership users to review results in the dashboard.

Ingestion and matching can run manually or through scheduled batch executions.

The initial matching frequency is approximately twice per week.

The pilot does not require continuously running ingestion or matching services.

## Security and Data Isolation

Turnlot handles dealership business and customer information.

The architecture should enforce:

- Authenticated access to dealership-facing functionality
- Authorization scoped to the appropriate dealership or organization
- Tenant isolation in all relevant database queries
- Secure handling of customer contact information
- Secrets managed outside source control
- Least-privilege AWS IAM permissions
- Encrypted communication between application components

Production deployment details and security controls will be refined during implementation.

## Engineering Principles

**Separation of concerns**

Each repository owns a clear functional responsibility.

**Avoid unnecessary complexity**

Do not introduce additional services, repositories, or shared packages without a concrete engineering need.

**Independent application deployments**

The dashboard, API, and batch applications should be independently deployable where practical.

**Versioned internal dependencies**

Shared Python packages use explicit versions to support reproducible builds and controlled upgrades.

**Pilot-first development**

Prioritize reliable ingestion, matching accuracy, secure data access, and a usable dealership dashboard before introducing additional platform complexity.

**Incremental evolution**

Architecture decisions may evolve as Turnlot moves from its initial pilot to supporting multiple dealerships.

---

*This document describes Turnlot's working architecture. Planned components and implementation details may change as development progresses.*
