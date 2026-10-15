# Petcommerce

Petcommerce is an early-stage e-commerce monorepo focused on a pet-products domain. It combines an Angular frontend with a Spring Boot backend and PostgreSQL persistence.

> **Status:** Work in progress. The backend includes user/authentication integration and database models/migrations for product categories, products, and orders. The frontend route table is currently empty, so the repository should not yet be treated as a complete, customer-ready storefront.

## Tech stack

- **Frontend:** Angular 20, TypeScript, Angular SSR, Nx
- **Backend:** Java 21, Spring Boot 3.5, Spring Data JPA, Spring Security OAuth2 Resource Server
- **Database:** PostgreSQL 16, Liquibase migrations
- **Identity:** Kinde JWT/OIDC integration
- **Local development:** Docker Compose

## Prerequisites

- Node.js and npm
- JDK 21
- Docker Engine or Docker Desktop with the Compose plugin
- A Kinde development application for authenticated backend flows

## Configure local development

Create a repository-root `.env` file. Keep it local and never commit it.

```dotenv
POSTGRES_USER=petcommerce
POSTGRES_DB=petcommerce
POSTGRES_PASSWORD=replace-with-a-strong-local-password
KINDE_CLIENT_ID=your-kinde-client-id
KINDE_CLIENT_SECRET=your-kinde-client-secret
```

Configure the Kinde issuer/audience and callback settings to match your development application. The values above are placeholders, not working credentials.

## Start the application

Install JavaScript dependencies:

```bash
npm ci
```

Start PostgreSQL from the repository root:

```bash
docker compose up -d database
```

In separate terminals, start the backend and frontend:

```bash
npx nx serve demo
```

```bash
npx nx serve ecom-frontend
```

- Frontend: [http://localhost:4200](http://localhost:4200)
- Backend: [http://localhost:8080](http://localhost:8080)

The backend uses Liquibase for schema changes. If startup fails, check the local database credentials, Kinde configuration, and backend logs.

## Useful commands

Build the frontend:

```bash
npx nx build ecom-frontend
```

Run backend tests:

```bash
./apps/ecom-backend/mvnw -f apps/ecom-backend/pom.xml test
```

## Security and repository hygiene

- Local environment files and database volumes are excluded from version control.
- The Compose database binds to loopback and requires a password supplied through local environment configuration.
- Use development-only identity-provider credentials and never commit tokens or secrets.
- Before deployment, configure managed secrets, TLS, database backups, monitoring, and production-grade authentication settings.

## Next steps

- Implement and test the customer-facing routes and core shopping flows.
- Add frontend end-to-end tests and backend integration tests.
- Document screenshots and API examples once the corresponding flows are implemented.
