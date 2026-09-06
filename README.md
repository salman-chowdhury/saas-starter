# SaaS Workspace Prototype

A personal Next.js/TypeScript project exploring workspace membership, invitations, authentication and subscription-billing flows. Prisma uses **SQLite in the committed schema**. It is a learning prototype with tests, not a production-readiness certification.

## Inspect the implementation

| Area | Evidence |
| --- | --- |
| Workspace membership and invitations | [Server actions](src/server/actions/workspace-actions.ts), [workspace security tests](tests/unit/workspaces-security.test.ts) |
| Billing access checks | [Billing authorisation tests](tests/unit/billing-authorization.test.ts) |
| Webhook processing | [Webhook route](src/app/api/billing/webhook/route.ts), [tests](tests/unit/billing-webhook.test.ts) |
| Authentication | [Auth configuration](src/server/auth.ts) |
| Browser smoke tests | [Playwright specifications](tests/e2e) |

## Local setup

Requires Node.js 20+. Use a local development environment and Stripe test configuration only.

```bash
git clone https://github.com/salman-chowdhury/saas-starter.git
cd saas-starter
cp .env.example .env
# Replace AUTH_SECRET with a locally generated secret before running.
# Remove placeholder Stripe values for the documented stub/demo path.
npm ci
npm run setup
npm run dev
```

See [installation](docs/install.md), [demo guide](docs/demo-guide.md) and [architecture](docs/architecture.md) for configuration. `npm run setup` generates Prisma, synchronises the local development database and seeds demo records; do not point it at a production database.

## Verification commands

```bash
npm run lint
npm run typecheck
npm run test:unit
npm run test:e2e
```

The [existing health report](docs/HEALTH_REPORT.md) records an earlier validation pass and its residual risks. This documentation refresh does not claim a new full test run or a verified live deployment.

## Scope and limitations

- PostgreSQL requires a schema/provider and migration change; changing only the connection string is insufficient.
- Demo credentials and seed records are for local development. Authentication and billing integrations need environment-specific validation.
- Browser coverage is smoke-level; inspect the test cases before assuming complete tenant isolation or billing correctness.
- Rate limiting and other safeguards require review for the intended deployment topology.
- Dependency, authentication and payment configuration need review before any real-user deployment.

MIT licence — see [LICENSE](LICENSE).
