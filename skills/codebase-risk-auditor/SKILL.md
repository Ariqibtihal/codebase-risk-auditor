---
name: codebase-risk-auditor
description: audit software projects for production readiness, security, authentication, authorization, data privacy, scalability, maintainability, reliability, testing, deployment safety, database/api risk, performance, core web vitals, seo, technical seo, desktop usability, and mobile responsiveness. use when the user asks to review, audit, inspect, check, harden, assess, evaluate, benchmark, or improve a codebase, repository, app, backend, frontend, api, dashboard, saas product, internal tool, landing page, ecommerce site, marketing site, or ai-generated project beyond visual ui quality.
---

# Codebase Risk Auditor

Use this skill to audit software projects for technical quality, risk, production readiness, performance, SEO, and real-user readiness across desktop and mobile.

Apply it to web apps, mobile-responsive web apps, backend services, APIs, dashboards, SaaS products, admin panels, internal tools, automation systems, full-stack apps, AI-generated projects, database-backed systems, marketing sites, ecommerce sites, landing pages, and content-heavy websites.

Focus on whether the project is safe, scalable, maintainable, reliable, testable, indexable, discoverable, fast, accessible, and ready for real users.

Do not focus only on UI or visual design.

---

# Core Principles

1. Inspect before judging.
2. Identify project type, framework, runtime, package manager, architecture, rendering mode, and main folders.
3. Locate routing, authentication, authorization, API handlers, database access, services, configuration, environment variables, deployment files, metadata, sitemap, robots rules, image handling, and performance-critical components.
4. Prioritize real technical, security, SEO, and performance risk over cosmetic issues.
5. Be stricter with AI-generated projects.
6. Never assume frontend-only restrictions are secure.
7. Never assume a visually attractive site is fast, crawlable, or production-ready.
8. Do not refactor or change business logic unless explicitly requested.
9. Prefer precise, evidence-backed findings over generic advice.
10. Distinguish static/code evidence from runtime evidence. If browser, Lighthouse, production URL, or analytics data are unavailable, mark runtime performance and SEO conclusions as partially verified.

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

Include SEO/performance issues if they are among the highest-risk findings.

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
17. Performance and Core Web Vitals
18. SEO and technical SEO
19. Desktop UX and responsive behavior
20. Mobile UX and responsive behavior

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

Still flag severe SEO/performance issues if they create business or production risk, such as public pages that cannot be indexed, extremely slow initial load, or client-only rendering that hides critical content from crawlers.

## Performance and SEO Audit

Use when the user mentions performance, speed, Lighthouse, Core Web Vitals, SEO, ranking, indexing, crawling, metadata, desktop performance, mobile performance, responsive layout, landing page quality, marketing site readiness, or conversion readiness.

Prioritize:

- Core Web Vitals: LCP, INP, CLS
- server-side rendering/static rendering for indexable pages
- route-level metadata
- title and meta description quality
- canonical URLs
- robots.txt and sitemap.xml
- noindex/nofollow mistakes
- structured data
- Open Graph and Twitter metadata
- image optimization
- font loading
- JavaScript bundle size
- render-blocking resources
- lazy loading
- caching headers
- mobile viewport and responsive layout
- tap targets and mobile navigation
- desktop layout overflow and large-screen usability
- accessibility issues that affect SEO and conversion

## Mobile/Desktop UX Audit

Use when the user mentions mobile, desktop, responsive, layout, UI behavior, viewport, breakpoints, tablet, navbar, landing page, or frontend polish.

Prioritize:

- layout correctness at mobile, tablet, laptop, and desktop widths
- horizontal overflow
- sticky/fixed elements blocking content
- menu and modal behavior
- tap target size
- form usability
- image aspect ratios
- table/card overflow
- content hierarchy
- keyboard navigation
- focus states
- Lighthouse mobile vs desktop differences

## Fix Plan Audit

Use when the user wants a remediation plan without code changes.

Return:

- critical fixes
- important fixes
- quality improvements
- implementation order
- suggested tests
- suggested performance/SEO validation steps

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
- for SEO/performance patches, avoid superficial metadata-only changes if crawlability, rendering, or route structure is the actual problem

---

# Evidence Rules

1. Do not report a finding unless it is supported by inspected files, code paths, configs, dependency manifests, command output, rendered output, network traces, Lighthouse output, browser observation, production URL behavior, or a clear absence of required implementation.
2. If something is only possible but not confirmed, label it as **Potential Risk**.
3. Every confirmed finding must include a concrete file path, folder path, code pattern, config, dependency, observed missing control, runtime observation, or command output.
4. If relevant files, production URL, browser access, analytics, credentials, or runtime environment are missing or inaccessible, place the item under **Unverified Areas**, not **Findings**.
5. Do not invent project behavior.
6. Do not assume framework features are secure, performant, or SEO-friendly unless code or configuration confirms it.
7. If runtime environment, credentials, logs, production infrastructure, external services, Lighthouse, Search Console, or analytics data are unavailable, mark the item as partially verified.
8. If the code appears demo, mock, scaffolded, or AI-generated, state that explicitly.
9. For SEO claims, distinguish **technical SEO evidence** from **ranking assumptions**. Do not promise ranking improvements.
10. For performance claims, distinguish **static risk** from **measured runtime performance**. Static code review can identify likely causes, but cannot prove real-user speed without measurements.

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
- rendering strategy: SSR, SSG, ISR, CSR, SPA, MPA, API-only, hybrid
- database or storage layer
- authentication method
- deployment target
- key folders and files
- public/static asset structure
- SEO metadata strategy
- image/font strategy
- test setup

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
public/
static/
assets/
app/layout.*
app/sitemap.*
app/robots.*
pages/_document.*
pages/_app.*
next.config.*
vite.config.*
astro.config.*
nuxt.config.*
remix.config.*
robots.txt
sitemap.xml
manifest.json
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
- metadata and SEO config
- canonical URL handling
- sitemap generation
- robots rules
- Open Graph images
- image components/loaders
- font loading
- analytics/tracking scripts
- service workers/PWA config
- responsive layout primitives

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
- public landing page rendering
- public content page rendering
- navigation from mobile and desktop
- form submission from mobile and desktop
- search/filter/list pages
- product/detail/content pages

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
- client-only rendering for pages that need SEO
- missing or duplicated metadata
- no sitemap/robots strategy
- accidental `noindex`
- poor image optimization
- large unoptimized dependencies
- large client components that should be server-rendered
- blocking third-party scripts
- missing responsive constraints causing horizontal overflow

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
grep -R "metadata\|generateMetadata\|<title\|description\|canonical\|robots\|sitemap\|openGraph\|twitter" -n src app pages public .
grep -R "noindex\|nofollow\|robots.txt\|sitemap.xml" -n src app pages public .
grep -R "<img\|next/image\|Image from\|loading=\|priority\|fetchPriority" -n src app pages components .
grep -R "viewport\|max-width\|overflow-x\|fixed\|sticky\|min-h-screen\|w-screen\|100vw" -n src app pages components .
grep -R "analytics\|gtag\|pixel\|script\|third-party\|iframe" -n src app pages components public .
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

For SEO/performance audits, only run available read-only scripts if they already exist in `package.json`, such as:

```bash
npm run analyze
npm run lighthouse
npm run lhci
npm run build:analyze
```

Do not install Lighthouse, Playwright, Puppeteer, bundle analyzers, or browser tooling unless the user explicitly requests it. If tooling is unavailable, perform static analysis and mark runtime metrics as unverified.

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
- run crawlers, load tests, Lighthouse against production, or aggressive benchmark tools without user approval
- submit URLs to search engines or modify indexing rules without explicit approval

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

## 12. Performance and Core Web Vitals

Check static and, when available, runtime evidence for:

- slow initial load
- poor LCP candidate selection
- hero images not prioritized
- unoptimized images/assets
- missing responsive image sizes
- missing lazy loading for below-the-fold media
- layout shifts from images, ads, embeds, fonts, or dynamic content
- poor INP risk from heavy client-side JavaScript
- excessive hydration
- large JavaScript bundles
- unnecessary client components
- unused dependencies
- heavy libraries for simple interactions
- render-blocking scripts/styles
- blocking third-party scripts
- missing route-level code splitting
- large lists without pagination or virtualization
- repeated API calls
- poor caching
- missing compression assumptions
- missing CDN/static asset strategy
- expensive client-side computation
- slow server-side data fetching
- no loading skeletons or progressive rendering for slow routes

For measured audits, report mobile and desktop separately when data exists:

```txt
Mobile: LCP / INP or TBT / CLS / Performance score
Desktop: LCP / INP or TBT / CLS / Performance score
```

If only static inspection is possible, say:

```txt
Runtime Core Web Vitals were not measured. Findings are based on static code/config inspection.
```

## 13. SEO and Technical SEO

Check public pages and route configuration for:

- unique title per indexable page
- unique meta description per indexable page
- canonical URLs
- robots meta tags
- accidental noindex/nofollow
- robots.txt
- sitemap.xml or generated sitemap
- correct HTTP status behavior for not-found and redirects
- structured data where relevant: Organization, Website, BreadcrumbList, Product, Article, FAQ, LocalBusiness, etc.
- Open Graph and Twitter metadata
- social preview images
- indexable content present in HTML for SEO-critical pages
- SSR/SSG/ISR for public marketing/content pages where appropriate
- duplicate content risk
- pagination and faceted navigation indexing strategy
- hreflang for multilingual sites
- clean URL structure
- semantic heading hierarchy
- internal linking
- breadcrumb patterns
- alt text for meaningful images
- public pages blocked by auth, middleware, robots, or client-only rendering
- environment-specific base URL/canonical mismatch
- search result quality risks from placeholder, duplicate, or thin content

Do not claim keyword rankings will improve. Report technical readiness and likely SEO blockers.

## 14. Desktop UX and Responsive Behavior

Check desktop and large viewport behavior for:

- layout width constraints
- content density
- navigation visibility
- modal and dropdown positioning
- table/data grid usability
- hover/focus states
- high-resolution image quality
- large-screen whitespace misuse
- sticky headers/sidebars blocking content
- desktop form usability
- keyboard navigation
- desktop-specific overflow

## 15. Mobile UX and Responsive Behavior

Check mobile and small viewport behavior for:

- viewport meta configuration
- breakpoint coverage
- horizontal scrolling/overflow
- mobile navigation/menu behavior
- tap target size
- sticky/fixed elements blocking content
- modal bottom-sheet behavior
- form field usability
- keyboard-safe spacing
- readable font sizes
- table/card/list behavior
- image scaling and aspect ratio
- above-the-fold content priority
- mobile-specific CLS risk
- mobile Lighthouse difference from desktop

## 16. Accessibility and Usability

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

Accessibility issues can also affect SEO, conversion, and legal/compliance risk.

## 17. Testing

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
- SEO metadata generation
- sitemap/robots output
- critical responsive layouts
- performance regression budgets when available

If tests are missing, recommend a minimal critical-path test plan.

## 18. Deployment Safety

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
- production canonical/base URL configuration
- public asset caching assumptions
- source maps and error reporting exposure

## 19. Observability

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
- Core Web Vitals/RUM capture
- alerting

Logs must not leak sensitive data.

## 20. Backup and Recovery

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
public/
app/layout.*
app/page.*
app/sitemap.*
app/robots.*
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
- excessive `use client` usage
- SEO-critical pages rendered entirely on the client
- missing `metadata` or `generateMetadata`
- duplicate metadata across pages
- missing canonical/base URL configuration
- incorrect `robots` metadata
- missing `sitemap.ts` or sitemap strategy
- unoptimized `img` usage instead of `next/image` where appropriate
- missing width/height on images
- poor font loading strategy
- blocking scripts in layout

## Vite / React SPA

Inspect:

```txt
index.html
src/
public/
vite.config.*
```

Check for:

- SEO-critical content hidden behind client-only rendering
- missing or static-only title/meta for dynamic routes
- lack of prerendering/SSR for public pages
- poor code splitting
- large client bundle
- missing image optimization process
- missing sitemap/robots in public assets
- client-side route 404 behavior not reflected in HTTP status

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
- cache headers for public/static routes
- compression/static asset handling when server serves frontend assets

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
- cache/header behavior for public endpoints where applicable

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
- inefficient queries feeding public listing pages
- missing pagination/cursor strategy for SEO-relevant listings

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
- placeholder metadata repeated across all pages
- no sitemap/robots/canonical strategy
- poor mobile responsiveness hidden by desktop-only screenshots
- heavy client-side JavaScript without production performance review

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
- public pages accidentally blocked from indexing
- SEO-critical pages not renderable/indexable because content exists only after client execution
- severe mobile usability failure that blocks core conversion or task completion
- severe performance risk on critical pages, such as oversized bundles, blocking scripts, or missing image constraints likely to cause unusable loading

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
- missing metadata/canonical/sitemap controls on important public pages
- avoidable Core Web Vitals degradation
- mobile/desktop layout problems that degrade but do not fully block usage

Use **Low** for:

- minor duplication
- naming inconsistency
- minor accessibility gaps
- minor performance concerns
- documentation gaps
- non-critical cleanup
- small type-safety improvements
- minor UX reliability gaps
- minor SEO polish that is not blocking crawlability or indexability

When severity is uncertain, explain the uncertainty.

---

# Output Format

Return the audit using this structure:

```md
# Technical Audit Report

## Summary

- Project type:
- Stack detected:
- Rendering mode detected:
- Overall risk level:
- Production readiness:
- SEO readiness:
- Performance readiness:
- Mobile readiness:
- Desktop readiness:
- Main concern:
- Audit mode:
- Confidence level:

## Scope Inspected

List the main files, folders, configs, commands, flows, pages, routes, mobile/desktop breakpoints, and runtime checks inspected.

## Highest-Risk Issues

1. <Risk level> — <Issue summary>
2. <Risk level> — <Issue summary>
3. <Risk level> — <Issue summary>

## Findings

### 1. <Finding Title>

- Risk: High / Medium / Low
- Category: Security / Authentication / Authorization / Scalability / Maintainability / Reliability / Performance / SEO / Mobile UX / Desktop UX / etc.
- Location: <file, folder, route, config, command output, or runtime observation>
- Evidence:
- Problem:
- Impact:
- Recommendation:
- Suggested Fix:

## Performance and Core Web Vitals Review

- Mobile performance status:
- Desktop performance status:
- LCP risks:
- INP/TBT risks:
- CLS risks:
- Bundle/script risks:
- Image/font risks:
- Caching/rendering risks:
- Runtime metrics available: Yes / No

## SEO and Technical SEO Review

- Indexability status:
- Crawlability status:
- Metadata status:
- Canonical URL status:
- Sitemap/robots status:
- Structured data status:
- Social preview status:
- Content rendering status:
- Main SEO blockers:

## Mobile and Desktop Responsiveness Review

- Mobile layout status:
- Desktop layout status:
- Breakpoints inspected:
- Navigation/menu behavior:
- Forms/tables/cards behavior:
- Overflow risks:
- Tap target/focus risks:

## Potential Risks

List plausible risks that could not be fully confirmed from available files or runtime access.

## Priority Fix Plan

### Priority 1

Critical fixes related to security, authentication, authorization, data privacy, data integrity, indexability blockers, and severe performance/mobile blockers.

### Priority 2

Important fixes related to validation, scalability, database performance, reliability, Core Web Vitals, metadata, sitemap/robots, canonical URLs, and responsive UX.

### Priority 3

Quality improvements related to maintainability, type safety, testing, accessibility, usability, performance polish, SEO polish, and documentation.

## Suggested Tests and Validation

List the most important tests and validation steps to add, including:

- unit/integration/E2E tests
- role/tenant/authorization tests
- build/lint/typecheck commands
- Lighthouse mobile and desktop checks when tooling is available
- responsive viewport checks
- sitemap/robots validation
- metadata/canonical validation
- critical page screenshot checks

## Unverified Areas

List anything that could not be checked because files, environment, database, credentials, logs, production configuration, production URL, browser runtime, Search Console, analytics, Lighthouse output, or external services were unavailable.
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
16. Performance and Core Web Vitals
17. SEO and technical SEO
18. Mobile UX and responsive behavior
19. Desktop UX and responsive behavior
20. Accessibility and usability

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
- If credentials, logs, production configuration, production URL, Search Console, or analytics are unavailable, mark them as unverified.
- If Lighthouse or browser runtime is unavailable, do not claim measured Core Web Vitals or measured mobile/desktop scores.
- If the project is AI-generated, apply stricter review to security, authorization, validation, scalability, maintainability, testing, SEO, and performance.
- If a finding has no concrete evidence, move it to Potential Risks or Unverified Areas.
- If command output contradicts an initial assumption, trust the command output.
- If a dependency vulnerability scan is not available, do not claim dependencies are safe.
- If tests are not run, do not claim the project passes tests.
- If a production build is not run, do not claim the project builds successfully.
- If SEO metadata exists only in a layout/default file, verify whether important pages override it before calling SEO complete.
- If mobile/desktop behavior is not rendered in a browser, label responsive findings as static risks.

---

# Final Response Style

Use clear, direct, technical language.

For serious issues:

- state the risk plainly
- explain the exploit, crawlability failure, performance failure, or UX failure mode
- recommend the smallest safe fix
- identify whether the issue blocks production readiness

For missing evidence:

- say what was not available
- explain why it matters
- avoid guessing

For AI-generated or prototype projects:

- distinguish between "works as demo" and "safe for production"
- explicitly identify frontend-only, mock-only, SEO-incomplete, mobile-incomplete, or performance-unverified logic
- prioritize production, indexing, and performance blockers first
