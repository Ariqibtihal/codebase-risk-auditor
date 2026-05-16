---
name: codebase-risk-auditor
description: general audit for any software project, including web apps, mobile apps, backend services, APIs, dashboards, internal tools, full-stack apps, AI-generated projects, and database-backed systems. use when reviewing or checking a project for security, authentication, authorization, data privacy, scalability, maintainability, reliability, performance, testing, deployment safety, and production readiness beyond visual UI quality.
---

# Codebase Risk Auditor

Use this skill to audit any software project for technical quality, risk, and production readiness.

This skill is not limited to a specific domain or application type. Apply it to web apps, mobile apps, backend services, APIs, dashboards, SaaS products, admin panels, internal tools, automation systems, full-stack applications, and AI-generated projects.

Focus on whether the project is safe, scalable, maintainable, reliable, testable, and ready for real users.

Do not focus only on UI or visual design.

---

# Core Audit Principles

1. Inspect before changing.
2. Identify the project type, framework, runtime, package manager, architecture, and main folders.
3. Locate critical areas such as routing, authentication, authorization, API handlers, database access, services, configuration, environment variables, and deployment files.
4. Prioritize real technical risk over cosmetic issues.
5. Be stricter with AI-generated projects, because they often look complete but miss security, validation, scalability, testing, and maintainability.
6. Do not assume hidden buttons, hidden menus, or frontend-only guards are secure.
7. Do not refactor large parts of the project unless explicitly requested.
8. Do not change business logic without explaining the impact.

---

# Audit Workflow

## 1. Identify Project Context

Check:

- project type
- framework
- language
- package manager
- frontend/backend architecture
- routing system
- database or storage layer
- authentication method
- deployment target if visible
- key folders and files

Look for files such as:

```txt
package.json
requirements.txt
pyproject.toml
composer.json
go.mod
Cargo.toml
Dockerfile
docker-compose.yml
.env.example
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
```

## 2. Map Critical Flows

Identify important flows such as:

- login
- logout
- registration
- role-based access
- dashboard access
- create/update/delete data
- file upload
- approval workflow
- payment flow
- admin actions
- API access
- database writes
- external integrations

## 3. Audit Technical Risk

Use the checklist below. Report issues with risk level, file location, impact, and recommended fix.

---

# Audit Checklist

## 1. Security

Check for:

- hardcoded secrets
- exposed API keys
- committed `.env` files
- unsafe environment variable usage
- insecure token/session storage
- missing API protection
- missing server-side authorization
- missing rate limiting
- XSS risks
- SQL/NoSQL injection risks
- CSRF risks where applicable
- unsafe file upload handling
- overly permissive CORS
- vulnerable dependencies
- sensitive data in logs or error messages

## 2. Authentication

Check:

- login flow
- logout flow
- password handling
- password hashing if custom auth exists
- session/token expiration
- refresh token handling if present
- authentication persistence
- expired session behavior
- password reset flow if present
- brute-force protection
- login error messages that may reveal account existence

Avoid:

```txt
Email not found.
```

Prefer:

```txt
Email or password is incorrect.
```

## 3. Authorization and Access Control

Check whether access control exists in:

- UI/menu visibility
- route guards
- middleware
- backend/API handlers
- database query scoping
- server-side business logic

Frontend-only authorization is not enough.

Check for:

- role spoofing
- IDOR vulnerabilities
- direct API access bypass
- admin route bypass
- ownership check failures
- unsafe role/status updates from the client
- missing tenant or organization scoping in multi-tenant apps

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

## 5. Input Validation and Sanitization

Check validation on both frontend and backend/API.

Review:

- required fields
- length limits
- allowed values
- enum validation
- date validation
- numeric validation
- file type and file size validation
- URL/email validation
- output escaping
- schema validation

Frontend validation improves UX, but backend validation is mandatory.

## 6. Data Integrity and Business Logic

Check for:

- invalid state transitions
- client-controlled status changes
- missing ownership checks
- duplicate submissions
- race conditions
- timezone/date bugs
- missing database transactions
- optimistic UI desync
- inconsistent business rules
- missing uniqueness constraints
- unsafe delete behavior

If workflow states exist, identify valid and invalid transitions.

## 7. Scalability

Check for:

- fetching all records without pagination
- large unbounded API responses
- dashboard calculations done entirely on the frontend
- missing server-side filtering/search
- missing database indexes
- N+1 queries
- inefficient loops over large datasets
- repeated unnecessary requests
- no caching strategy
- no queue/background job strategy for heavy tasks

Ask: what happens when the data grows 10x or 100x?

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
- soft delete vs hard delete strategy
- createdAt/updatedAt usage
- relation loading strategy

Important fields to inspect:

- user ID
- role
- status
- foreign keys
- created date
- updated date
- frequently searched fields
- frequently filtered fields

## 9. Maintainability

Check for:

- oversized files
- oversized components/classes
- duplicated logic
- mixed UI and business logic
- API calls scattered in UI files
- inconsistent naming
- hardcoded values
- magic strings
- scattered constants
- repeated styling
- unclear folder structure
- unused files
- dead code
- tightly coupled modules

Prefer clear separation such as:

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

For untyped projects, check whether validation schemas or clear data contracts exist.

## 11. Reliability and Error Handling

Check every major flow for:

- loading state
- error state
- empty state
- unauthorized state
- forbidden state
- network failure handling
- retry behavior where appropriate
- form submission failure handling
- success feedback
- timeout handling
- fallback UI

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

## 14. Testing

Check whether tests cover:

- authentication
- authorization/access control
- protected routes
- protected APIs
- form validation
- business logic
- database/service logic
- error states
- critical UI rendering
- integration flows
- E2E flows

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

## 16. Observability

Check whether the project has:

- structured logging
- error tracking
- audit logs for sensitive actions
- monitoring
- health checks
- meaningful server logs
- client-side error reporting if needed

Logs should be useful but must not leak sensitive data.

## 17. Backup and Recovery

If the project stores important data, check:

- backup strategy
- restore process
- migration safety
- soft delete vs hard delete
- data retention assumptions
- disaster recovery plan

If no database or storage layer exists, state that this cannot be fully assessed.

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

Use **Medium** for issues that may cause:

- poor scalability
- unreliable behavior
- inconsistent data
- weak validation
- missing important error handling
- hard-to-maintain code
- missing tests for important flows

Use **Low** for issues such as:

- minor duplication
- naming inconsistency
- minor accessibility gaps
- minor performance concerns
- documentation gaps
- non-critical cleanup

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

## Highest-Risk Issues

1. <Risk level> — <Issue summary>
2. <Risk level> — <Issue summary>
3. <Risk level> — <Issue summary>

## Findings

### 1. <Finding Title>

- Risk: High / Medium / Low
- Category: Security / Authentication / Authorization / Scalability / Maintainability / Reliability / etc.
- Location: <file or folder>
- Problem:
- Impact:
- Recommendation:
- Suggested Fix:

### 2. <Finding Title>

- Risk:
- Category:
- Location:
- Problem:
- Impact:
- Recommendation:
- Suggested Fix:

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

List anything that could not be checked because files, environment, database, credentials, logs, or production configuration were unavailable.
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

# Rules

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