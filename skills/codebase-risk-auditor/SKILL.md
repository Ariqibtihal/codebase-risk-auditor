---
name: codebase-risk-auditor
description: audit software projects for production readiness, security, authentication, authorization, data privacy, scalability, maintainability, reliability, testing, deployment safety, and database/API risk. use when the user asks to review, audit, inspect, check, harden, assess, or evaluate a codebase, repository, app, backend, frontend, API, dashboard, SaaS product, internal tool, or AI-generated project beyond visual UI quality.
---

# Codebase Risk Auditor

Use this skill to audit software projects for technical quality, risk, and production readiness.

Apply it to web apps, mobile apps, backend services, APIs, dashboards, SaaS products, admin panels, internal tools, automation systems, full-stack apps, AI-generated projects, and database-backed systems.

Focus on whether the project is safe, scalable, maintainable, reliable, testable, and ready for real users.

Do not focus only on UI or visual design.

---

# Core Principles

1. Inspect before judging.
2. Identify project type, framework, runtime, package manager, architecture, and main folders.
3. Locate routing, authentication, authorization, API handlers, database access, services, configuration, environment variables, and deployment files.
4. Prioritize real technical risk over cosmetic issues.
5. Be stricter with AI-generated projects.
6. Never assume frontend-only restrictions are secure.
7. Do not refactor or change business logic unless explicitly requested.
8. Prefer precise, evidence-backed findings over generic advice.

---

# Audit Modes

Use the appropriate mode based on the user's request.

## Quick Audit

Use for fast reviews.

Return the top 5–10 highest-risk issues with:

- evidence
- impact
- recommended fix
- priority order

## Full Audit

Use for complete production-readiness reviews.

Inspect all audit categories:

1. Security
2. Authentication
3. Authorization and access control
4. Data privacy
5. Data integrity and business logic
6. Input validation
7. Scalability
8. Database and query performance
9. Reliability and error handling
10. Maintainability
11. Type safety and data contracts
12. Testing
13. Deployment safety
14. Observability
15. Backup and recovery
16. Accessibility and usability
17. Performance

## Security-Focused Audit

Use when the user mentions security, hardening, auth, privacy, permissions, API protection, or production risk.

Prioritize:

- secrets
- authentication
- authorization
- access control
- API protection
- data exposure
- validation
- injection risks
- file upload safety
- CORS
- dependencies
- deployment safety

## Fix Plan Audit

Use when the user wants a remediation plan without code changes.

Return:

- critical fixes
- important fixes
- quality improvements
- implementation order
- suggested tests

## Patch Mode

Only use when the user explicitly asks to fix, modify, patch, or update code.

In Patch Mode:

- inspect first
- explain intended changes
- keep changes minimal
- avoid broad refactors
- preserve business logic unless approved
- summarize changed files
- include tests or validation steps where possible

---

# Evidence Rules

1. Do not report a finding unless it is supported by inspected files, code paths, configs, dependency manifests, command output, or a clear absence of required implementation.
2. If something is only possible but not confirmed, label it as **Potential Risk**.
3. Every confirmed finding must include a concrete file path, folder path, code pattern, config, dependency, or observed missing control.
4. If relevant files are missing or inaccessible, place the item under **Unverified Areas**, not **Findings**.
5. Do not invent project behavior.
6. Do not assume framework features are secure unless code or configuration confirms it.
7. If runtime environment, credentials, logs, production infrastructure, or external services are unavailable, mark the item as partially verified.
8. If the code appears demo, mock, scaffolded, or AI-generated, state that explicitly.

---

# Execution Protocol

## 1. Inspect Repository Structure

Identify:

- project type
- framework
- language
- runtime
- package manager
- frontend/backend architecture
- routing system
- database or storage layer
- authentication method
- deployment target
- key folders and files

Look for:

```txt
package.json
pnpm-lock.yaml
yarn.lock
package-lock.json
requirements.txt
pyproject.toml
composer.json
go.mod
Cargo.toml
Dockerfile
docker-compose.yml
.env
.env.example
.gitignore
README.md
src/
app/
pages/
routes/
api/
server/
backend/
components/
services/
lib/
config/
database/
migrations/
prisma/
supabase/
tests/
```

## 2. Identify Critical Files

Locate files related to:

- routing
- middleware
- authentication
- authorization
- API handlers
- database models
- queries
- services
- validation schemas
- configuration
- environment variables
- deployment
- logging
- tests

## 3. Map Critical Flows

Identify important flows:

- login
- logout
- registration
- password reset
- role-based access
- dashboard access
- create/update/delete data
- file upload
- payment
- approval workflow
- admin actions
- API access
- database writes
- external integrations
- webhooks
- background jobs

## 4. Search for High-Risk Patterns

Prioritize:

- hardcoded secrets
- missing API protection
- client-controlled roles or status
- unsafe database queries
- missing ownership checks
- unbounded queries
- unsafe uploads
- weak validation
- broad CORS
- sensitive logs
- mock/demo code in production paths

## 5. Run Safe Read-Only Commands

Only run safe commands unless the user explicitly asks for fixes.

Useful inspection commands:

```bash
pwd
ls
find . -maxdepth 3 -type f
find . -maxdepth 2 -type d
cat package.json
cat requirements.txt
cat pyproject.toml
cat Dockerfile
cat docker-compose.yml
cat .env.example
cat README.md
```

Search commands:

```bash
grep -R "API_KEY\|SECRET\|TOKEN\|PASSWORD\|PRIVATE_KEY\|process.env\|import.meta.env" -n .
grep -R "dangerouslySetInnerHTML\|innerHTML\|eval(\|Function(" -n .
grep -R "TODO\|FIXME\|HACK\|XXX" -n .
grep -R "admin\|role\|permission\|auth\|session\|jwt" -n src app pages routes server backend lib services
```

For Node or TypeScript projects, only run scripts that exist in `package.json`:

```bash
npm run lint
npm test
npm run build
npm audit --omit=dev
```

For Python projects:

```bash
python --version
pytest
python -m pytest
```

For Prisma projects:

```bash
npx prisma validate
```

Do not run database-mutating commands unless explicitly requested.

---

# Unsafe Commands

Never run destructive or high-risk commands unless the user explicitly asks and the impact is clearly explained.

Avoid:

```bash
rm -rf
git reset --hard
git clean -fd
drop database
truncate
delete from
npm audit fix --force
npm install
pnpm install
yarn add
pip install
docker compose down -v
docker system prune
prisma migrate deploy
prisma migrate reset
```

Do not:

- install packages unless explicitly requested
- rewrite architecture without approval
- run migrations without approval
- delete files without approval
- modify environment files without approval
- change business logic without explaining the impact

---

# Audit Checklist

## 1. Security

Check for:

- hardcoded secrets
- exposed API keys
- committed `.env` files
- unsafe environment usage
- insecure token/session storage
- missing API protection
- missing server-side authorization
- missing rate limiting
- XSS
- SQL/NoSQL injection
- CSRF where applicable
- unsafe file uploads
- overly permissive CORS
- vulnerable dependencies
- sensitive logs or error messages
- unsafe redirects
- insecure webhook verification
- missing request size limits
- insecure cookies
- weak security headers

## 2. Authentication

Check:

- login
- logout
- registration
- password handling
- password hashing
- session/token expiration
- refresh token handling
- expired session behavior
- password reset
- brute-force protection
- account enumeration through error messages

Avoid:

```txt
Email not found.
```

Prefer:

```txt
Email or password is incorrect.
```

## 3. Authorization and Access Control

Check access control in:

- UI/menu visibility
- route guards
- middleware
- backend/API handlers
- database query scoping
- server-side business logic

Check for:

- role spoofing
- IDOR
- direct API bypass
- admin route bypass
- ownership check failures
- unsafe role/status updates from client
- missing tenant or organization scoping
- missing permission checks on reads and writes

Frontend-only authorization is not enough.

## 4. Data Privacy

Check whether sensitive data is:

- minimized
- protected by role or ownership
- not overfetched
- not exposed in client bundles
- not logged unnecessarily
- not stored insecurely
- not returned from APIs unless needed
- not cached unsafely
- not included in analytics events
- not exposed through error responses or source maps

## 5. Input Validation and Sanitization

Check validation on both frontend and backend/API.

Review:

- required fields
- length limits
- allowed values
- enum validation
- date validation
- numeric validation
- file type and size validation
- URL/email validation
- output escaping
- schema validation
- request body size limits
- route/query parameter validation

Frontend validation improves UX, but backend validation is mandatory.

## 6. Data Integrity and Business Logic

Check for:

- invalid state transitions
- client-controlled status changes
- missing ownership checks
- duplicate submissions
- race conditions
- timezone/date bugs
- missing transactions
- optimistic UI desync
- inconsistent business rules
- missing uniqueness constraints
- unsafe delete behavior
- missing idempotency
- missing audit trail for sensitive actions

## 7. Scalability

Check for:

- fetching all records without pagination
- large unbounded API responses
- dashboard calculations done entirely on frontend
- missing server-side filtering/search
- missing indexes
- N+1 queries
- inefficient loops over large datasets
- repeated unnecessary requests
- no caching strategy
- no queue/background job strategy
- synchronous long-running requests
- unbounded file processing

Ask:

```txt
What happens when the data grows 10x or 100x?
```

## 8. Database and Query Performance

Check:

- schema design
- indexes
- foreign keys
- query limits
- pagination
- aggregation strategy
- migration files
- transaction safety
- seed/demo data separation
- soft delete vs hard delete
- createdAt/updatedAt usage
- relation loading strategy
- tenant scoping
- uniqueness constraints
- cascade behavior
- connection pooling assumptions

## 9. Maintainability

Check for:

- oversized files
- oversized components/classes
- duplicated logic
- mixed UI and business logic
- scattered API calls
- inconsistent naming
- hardcoded values
- magic strings
- scattered constants
- unclear folder structure
- unused files
- dead code
- tightly coupled modules
- inconsistent error handling
- unclear domain boundaries

Prefer structure such as:

```txt
components/
features/
services/
hooks/
lib/
types/
config/
database/
tests/
```

## 10. Type Safety and Data Contracts

For typed projects, check:

- excessive `any`
- missing API response types
- missing domain types
- unsafe casts
- stringly typed roles/statuses
- untyped form data
- inconsistent nullable handling
- mismatched frontend/backend types
- duplicated types across layers

For untyped projects, check whether validation schemas or clear data contracts exist.

## 11. Reliability and Error Handling

Check major flows for:

- loading state
- error state
- empty state
- unauthorized state
- forbidden state
- network failure handling
- retry behavior
- form submission failure handling
- success feedback
- timeout handling
- fallback UI
- graceful degradation
- clear user-facing errors
- non-leaky server errors

Avoid blank screens and silent failures.

## 12. Performance

Check:

- large bundle size
- unused dependencies
- unoptimized images/assets
- missing lazy loading
- unnecessary re-renders
- expensive client-side computation
- large lists without pagination or virtualization
- repeated API calls
- blocking scripts
- poor caching
- slow initial load
- unnecessary hydration
- heavy dependencies for simple tasks

## 13. Accessibility and Usability

Check:

- form labels
- keyboard navigation
- focus states
- color contrast
- semantic HTML
- button semantics
- alt text
- visible validation errors
- readable error messages
- mobile usability
- table overflow
- tap target size
- ARIA usage where appropriate
- modal focus trapping

## 14. Testing

Check whether tests cover:

- authentication
- authorization
- protected routes
- protected APIs
- form validation
- business logic
- database/service logic
- error states
- critical UI rendering
- integration flows
- E2E flows
- role-based scenarios
- tenant/ownership boundaries
- destructive actions
- webhook/payment flows

If tests are missing, recommend a minimal critical-path test plan.

## 15. Deployment Safety

Check:

- environment variables
- production build config
- `.env` leakage
- CI/CD config
- deployment scripts
- database migrations
- rollback strategy
- demo credentials
- source map exposure
- dependency vulnerabilities
- staging vs production separation
- dev-only code in production
- runtime version pinning
- Docker image safety
- build-time vs runtime secret exposure

## 16. Observability

Check whether the project has:

- structured logging
- error tracking
- audit logs for sensitive actions
- monitoring
- health checks
- meaningful server logs
- client-side error reporting
- request IDs or correlation IDs
- performance monitoring
- alerting

Logs must not leak sensitive data.

## 17. Backup and Recovery

If the project stores important data, check:

- backup strategy
- restore process
- migration safety
- soft delete vs hard delete
- data retention assumptions
- disaster recovery plan
- rollback process
- export process
- recovery time assumptions
- recovery point assumptions

If no database or storage layer exists, state that this cannot be fully assessed.

---

# Stack-Specific Guidance

## Next.js / React

Inspect:

```txt
app/
pages/
middleware.ts
next.config.*
src/
components/
lib/
server/
api/
.env.example
```

Check for:

- server/client boundary mistakes
- secrets exposed to client bundles
- missing API route authorization
- frontend-only route protection
- unsafe server actions
- insecure middleware assumptions
- unvalidated route params
- public environment variable misuse
- overfetching in client components

## Express / Node Backend

Inspect:

```txt
server/
routes/
controllers/
middleware/
services/
models/
config/
```

Check for:

- missing auth middleware
- route-level authorization gaps
- unsafe CORS
- missing security headers
- missing rate limiting
- unsafe error middleware
- unvalidated request bodies
- direct query construction
- missing centralized error handling

## Python Backend

Inspect:

```txt
app/
api/
routes/
models/
schemas/
services/
config/
```

Check for:

- missing validation schemas
- unsafe ORM queries
- missing auth dependencies
- insecure config defaults
- missing exception handling
- dependency vulnerabilities
- missing tests for service logic

## Database-Backed Apps

Inspect:

```txt
migrations/
schema files
model definitions
query services
repository layer
API handlers that read/write data
```

Check for:

- missing indexes
- missing foreign keys
- missing ownership checks
- missing tenant scoping
- unsafe deletes
- missing transactions
- missing uniqueness constraints
- unbounded list queries

## AI-Generated Projects

Be stricter.

Common issues:

- fake authentication
- frontend-only admin protection
- mock data treated as production data
- no backend validation
- no database constraints
- no tests
- no deployment safety
- no error handling
- hardcoded secrets or sample keys
- attractive UI masking incomplete logic
- role values controlled by the client
- unsafe direct object access

Clearly distinguish between:

- works as demo
- safe for production

---

# Severity Guide

Use **High** for issues that may cause:

- unauthorized access
- data leakage
- privilege escalation
- account takeover
- broken authentication
- broken authorization
- destructive data corruption
- production outage
- secrets leakage
- critical business logic bypass
- payment or webhook abuse
- tenant data exposure

Use **Medium** for issues that may cause:

- poor scalability
- unreliable behavior
- inconsistent data
- weak validation
- missing important error handling
- hard-to-maintain code
- missing tests for important flows
- degraded production readiness
- avoidable operational risk

Use **Low** for:

- minor duplication
- naming inconsistency
- minor accessibility gaps
- minor performance concerns
- documentation gaps
- non-critical cleanup
- small type-safety improvements
- minor UX reliability gaps

When severity is uncertain, explain the uncertainty.

---

# Output Format

Return the audit using this structure:

```md
# Technical Audit Report

## Summary

- Project type:
- Stack detected:
- Overall risk level:
- Production readiness:
- Main concern:
- Audit mode:
- Confidence level:

## Scope Inspected

List the main files, folders, configs, commands, and flows inspected.

## Highest-Risk Issues

1. <Risk level> — <Issue summary>
2. <Risk level> — <Issue summary>
3. <Risk level> — <Issue summary>

## Findings

### 1. <Finding Title>

- Risk: High / Medium / Low
- Category: Security / Authentication / Authorization / Scalability / Maintainability / Reliability / etc.
- Location: <file or folder>
- Evidence:
- Problem:
- Impact:
- Recommendation:
- Suggested Fix:

## Potential Risks

List plausible risks that could not be fully confirmed from available files.

## Priority Fix Plan

### Priority 1

Critical fixes related to security, authentication, authorization, data privacy, and data integrity.

### Priority 2

Important fixes related to validation, scalability, database performance, and reliability.

### Priority 3

Quality improvements related to maintainability, type safety, testing, accessibility, usability, and performance.

## Suggested Tests

List the most important tests to add.

## Unverified Areas

List anything that could not be checked because files, environment, database, credentials, logs, production configuration, or external services were unavailable.
```

---

# Priority Order

Use this order unless the user requests otherwise:

1. Security
2. Authentication
3. Authorization and access control
4. Data privacy
5. Data integrity and business logic
6. Input validation
7. Scalability
8. Database/query performance
9. Reliability and error handling
10. Maintainability
11. Type safety and data contracts
12. Testing
13. Deployment safety
14. Observability
15. Backup and recovery
16. Accessibility and usability
17. Performance

---

# Reporting Rules

- Do not focus only on UI.
- Do not assume frontend-only restrictions are secure.
- Do not treat mock/demo behavior as production-ready.
- Do not perform destructive changes.
- Do not introduce new libraries unless necessary.
- Do not make large refactors unless explicitly requested.
- Do not change business logic without explaining the impact.
- If files are missing, state what cannot be verified.
- If the project has no backend, state which security checks cannot be fully verified.
- If the project has no database, state which scalability and recovery checks cannot be fully verified.
- If credentials, logs, or production configuration are unavailable, mark them as unverified.
- If the project is AI-generated, apply stricter review to security, authorization, validation, scalability, maintainability, and testing.
- If a finding has no concrete evidence, move it to Potential Risks or Unverified Areas.
- If command output contradicts an initial assumption, trust the command output.
- If a dependency vulnerability scan is not available, do not claim dependencies are safe.
- If tests are not run, do not claim the project passes tests.
- If a production build is not run, do not claim the project builds successfully.

---

# Final Response Style

Use clear, direct, technical language.

For serious issues:

- state the risk plainly
- explain the exploit or failure mode
- recommend the smallest safe fix
- identify whether the issue blocks production readiness

For missing evidence:

- say what was not available
- explain why it matters
- avoid guessing

For AI-generated or prototype projects:

- distinguish between "works as demo" and "safe for production"
- explicitly identify frontend-only or mock-only logic
- prioritize production blockers first
