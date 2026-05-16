# Codebase Risk Auditor

A reusable AI coding audit guide for reviewing software projects across security, authentication, authorization, data privacy, scalability, maintainability, reliability, testing, deployment safety, and production readiness.

This guide is designed for use with AI coding assistants or manual code review. It helps identify technical risks that are often missed when a project only appears complete from the UI.

## Use Cases

Use this audit guide to review:

- Web apps
- Mobile apps
- Backend services
- APIs
- Dashboards
- Admin panels
- Internal tools
- Full-stack applications
- AI-generated projects
- Database-backed systems

## What It Checks

- Security
- Authentication
- Authorization and access control
- Data privacy
- Input validation and sanitization
- Business logic integrity
- Scalability
- Database/query performance
- Maintainability
- Type safety and data contracts
- Reliability and error handling
- Performance
- Accessibility and usability
- Testing
- Deployment safety
- Observability
- Backup and recovery

## Repository Structure

```txt
codebase-risk-auditor/
├── SKILL.md
├── README.md
├── LICENSE
├── agents/
│   └── openai.yaml
└── references/
    └── audit-categories.md
```

## Usage

Use this repository as a structured audit reference for AI coding assistants or human reviewers.

Example prompt:

```txt
Use the instructions in this repository to audit this project for technical quality and production readiness. Do not focus only on UI. Check security, authentication, authorization, data privacy, scalability, maintainability, reliability, testing, deployment safety, and performance. Return findings with risk level, file location, impact, and recommended fixes.
```

## Recommended Workflow

1. Ask the AI coding assistant to inspect the project structure first.
2. Ask it to identify the framework, architecture, routing, API layer, database layer, authentication, authorization, and deployment configuration.
3. Ask it to audit the project using the categories in `SKILL.md`.
4. Ask it to return findings by risk level.
5. Fix high-risk issues first.
6. Re-run the audit after important changes.

## Priority Order

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

## License

MIT
