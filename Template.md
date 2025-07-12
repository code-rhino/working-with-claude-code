# CLAUDE.md - Development Guide

*Original framework by Sabrina Ramonov*  
*Generic template and refactoring workflows by Tariq Hook*

## Project Overview

[Brief description of your project and its purpose]

### Core Technology Stack
- **Framework**: [Primary framework/language - e.g., Next.js, Spring Boot 3.x, FastAPI, Express.js]
- **Database**: [Database technology - e.g., PostgreSQL, MongoDB, MySQL]
- **Authentication**: [Auth system - e.g., JWT, OAuth2, Auth0, Firebase Auth]
- **Cloud Services**: [Cloud provider and services - e.g., file storage, serverless functions, hosting]
- **External Integrations**: [Third-party APIs - e.g., payment processing, email service, third-party data]
- **Build Tool**: [Build system - e.g., Vite, Maven, npm/yarn, Gradle]
- **Testing**: [Testing framework - e.g., Jest, JUnit, pytest]

### Key Dependencies
[List your main dependencies here - frameworks, libraries, tools]

---

## Implementation Best Practices

### 0 — Purpose

These rules ensure maintainability, safety, and developer velocity.
**MUST** rules are enforced by CI; **SHOULD** rules are strongly recommended.

---

### 1 — Before Coding

- **BP-1 (MUST)** Ask the user clarifying questions.
- **BP-2 (SHOULD)** Draft and confirm an approach for complex work.
- **BP-3 (SHOULD)** If ≥ 2 approaches exist, list clear pros and cons.
- **BP-4 (SHOULD)** Consider [external integration] impact for [relevant feature changes].
- **BP-5 (MUST)** For [new feature/version] development, ALWAYS first examine existing functionality, understand current implementation, then design improvements.
- **BP-6 (MUST)** Before starting work, ask which current [API endpoints/components/modules] it connects with.

---

### 2 — While Coding

- **C-1 (MUST)** Follow TDD: scaffold stub -> write failing test -> implement.
- **C-2 (MUST)** Name [functions/methods/classes] with existing domain vocabulary for consistency.
- **C-3 (SHOULD NOT)** Introduce [classes/components] when simple [functions/utilities] suffice.
- **C-4 (SHOULD)** Prefer simple, composable, testable [functions/methods].
- **C-5 (MUST)** Use [type-safe IDs/strong typing] for domain identifiers
  ```[language]
  // ✅ Good - type-safe approach
  type UserId = Brand<string, 'UserId'>
  
  // ❌ Bad - primitive obsession  
  let userId: string
  ```
- **C-6 (MUST)** Use explicit imports, avoid wildcard imports.
- **C-7 (SHOULD NOT)** Add comments except for critical caveats; rely on self‑explanatory code.
- **C-8 (SHOULD)** Prefer composition over inheritance; use interfaces for contracts.
- **C-9 (SHOULD NOT)** Extract a new [function/method] unless it will be reused elsewhere, is the only way to unit-test otherwise untestable logic, or drastically improves readability.
- **C-10 (MUST)** Use [nullable types/Optional] for nullable return types, never return null for collections.
- **C-11 (SHOULD)** Prefer immutable objects; use [readonly/final/const] when possible.
- **C-12 (MUST)** Use proper [dependency injection/module system] patterns.
- **C-13 (MUST)** For [external API] integration, handle [authentication/rate limiting/error responses] properly.

---

### 3 — Testing

- **T-1 (MUST)** For simple [functions/methods], colocate unit tests following project structure.
- **T-2 (MUST)** For any API change, add/extend integration tests.
- **T-3 (MUST)** ALWAYS separate pure-logic unit tests from [database/network]-touching integration tests.
- **T-4 (SHOULD)** Prefer integration tests over heavy mocking; use mocks sparingly.
- **T-5 (SHOULD)** Unit-test complex algorithms thoroughly with [parameterized tests].
- **T-6 (SHOULD)** Test the entire structure in one assertion if possible
  ```[language]
  expect(result).toEqual([expectedValue]); // Good

  expect(result).toHaveLength(1);        // Bad
  expect(result[0]).toBe(expectedValue); // Bad
  ```
- **T-7 (MUST)** Use [Docker/Testcontainers/test databases] for integration tests, not in-memory alternatives.
- **T-8 (SHOULD)** Use appropriate test types for different layers [unit/integration/e2e].
- **T-9 (SHOULD)** Mock external API calls in tests; use [test doubles/mock servers] for integration testing.

---

### 4 — Data Layer

- **D-1 (MUST)** Use [proper data models/entities]; avoid anemic domain models.
- **D-2 (SHOULD)** Use [transactions/atomic operations] appropriately.
- **D-3 (MUST)** Use [query builders/ORMs/raw SQL] appropriately for complex queries.
- **D-4 (MUST)** Use [migration system] for schema changes; never modify existing migrations.
- **D-5 (SHOULD)** Use database-appropriate types in migrations but application types in code.
- **D-6 (MUST)** Follow existing [migration/schema] patterns.

---

### 5 — Code Organization

- **O-1 (MUST)** Place shared code in [shared/common/utils] only if used by ≥ 2 modules.
- **O-2 (MUST)** Follow existing package/folder structure:
  ```
  [project-root]/
  ├── [config/settings]/           # Configuration
  ├── [src/lib]/
  │   ├── [shared/common]/         # Shared components  
  │   ├── [feature1]/              # Feature modules
  │   ├── [feature2]/              # Feature modules
  │   └── [integrations]/          # External integrations
  ├── [tests]/                     # Test files
  └── [docs]/                      # Documentation
  ```
- **O-3 (MUST)** Keep configuration in appropriate [config/env] location.
- **O-4 (SHOULD)** Use [feature/module] organization for major architectural changes.
- **O-5 (MUST)** Place [external integration]-specific code in dedicated modules.

---

### 6 — Tooling Gates

- **G-1 (MUST)** [Code formatting tool] passes (e.g., `prettier --check`, `black --check`).
- **G-2 (MUST)** [Build/compile] passes without warnings.
- **G-3 (MUST)** [Linting tool] passes (e.g., `eslint`, `pylint`, `checkstyle`).
- **G-4 (SHOULD)** [Static analysis] quality gates pass (e.g., SonarQube, CodeClimate).

---

### 7 - Git

- **GH-1 (MUST)** Use Conventional Commits format: https://www.conventionalcommits.org/en/v1.0.0
- **GH-2 (SHOULD NOT)** Refer to Claude or Anthropic in commit messages.
- **GH-3 (SHOULD)** Use TREF workflow before significant refactoring to create safety checkpoints.
- **GH-4 (SHOULD)** Clean up working branches after successful merges with TMERGE.

---

## Build and Development Commands

### [Build Tool] Commands
```bash
# Build the application
[build command - e.g., npm run build, ./mvnw compile, python setup.py build]

# Run tests
[test command - e.g., npm test, ./mvnw test, pytest]

# Run the application (development)
[dev command - e.g., npm run dev, ./mvnw spring-boot:run, python manage.py runserver]

# Install dependencies
[install command - e.g., npm install, pip install -r requirements.txt]
```

### Database Management
```bash
# Run migrations
[migration command - e.g., npx prisma migrate dev, python manage.py migrate]

# Create new migration
[migration create - e.g., npx prisma migrate dev --name, python manage.py makemigrations]

# Rollback migration
[rollback command if available]
```

### Local Development Setup
```bash
# Start local dependencies (Docker)
docker-compose up -d

# Or individual services
docker run -d --name [service] -p [port]:[port] [image]
```

## Environment Configuration

### Available Environments
1. **Development** ([config file]): Local development configuration
2. **Staging** ([config file]): Pre-production environment
3. **Production** ([config file]): Production configuration
4. **Test** ([config file]): Testing environment

### Environment Variables
- **[APP_PORT]**: Application port (default: [port])
- **[DATABASE_URL]**: Database connection string
- **[API_KEYS]**: External service API keys
- **[AUTH_CONFIG]**: Authentication configuration
- **[STORAGE_CONFIG]**: File/media storage configuration

---

## Writing [Functions/Methods] Best Practices

When evaluating whether a [function/method] you implemented is good, use this checklist:

1. Can you read the [function/method] and HONESTLY easily follow what it's doing? If yes, then stop here.
2. Does it have very high cyclomatic complexity? (nested if-else statements, multiple paths)
3. Are there any common data structures and algorithms that would make this much easier to follow?
4. Are there any unused parameters?
5. Are there any unnecessary type casts that can be moved to parameters?
6. Is it easily testable without mocking core features? If not, can it be tested as part of an integration test?
7. Does it have hidden untested dependencies that could be factored into arguments?
8. Brainstorm 3 better names and see if the current name is best and consistent with codebase.

IMPORTANT: you SHOULD NOT refactor out a separate [function/method] unless there is a compelling need:
- the refactored [function/method] is used in more than one place
- the refactored [function/method] is easily unit testable while the original is not AND you can't test it any other way
- the original [function/method] is extremely hard to follow and you resort to putting comments everywhere

## Writing Tests Best Practices

When evaluating whether a test you've implemented is good, use this checklist:

1. SHOULD parameterize inputs; never embed unexplained literals directly in tests.
2. SHOULD NOT add a test unless it can fail for a real defect. Trivial asserts are forbidden.
3. SHOULD ensure the test name states exactly what the final assertion verifies.
4. SHOULD compare results to independent, pre-computed expectations, never to the [function/method]'s output re-used as the oracle.
5. SHOULD follow the same formatting, linting, and style rules as production code.
6. SHOULD express invariants or axioms rather than single hard-coded cases when practical.
7. Unit tests should be grouped logically [by class/module/feature].
8. Use appropriate matchers for unknown values (e.g., `expect.any()`, wildcards).
9. ALWAYS use strong assertions over weaker ones.
10. SHOULD test edge cases, realistic input, unexpected input, and value boundaries.
11. SHOULD NOT test conditions caught by the type system/compiler.
12. SHOULD use fluent assertions when available.

## Architecture Overview

[Describe your application's architecture - layers, modules, key patterns]

### [Module/Layer 1]
- **Purpose**: [What this handles]
- **Key Components**: [List main classes/files/components]
- **Patterns Used**: [Architectural patterns]

### [Module/Layer 2]
- **Purpose**: [What this handles]
- **Key Components**: [List main classes/files/components]  
- **Patterns Used**: [Architectural patterns]

### [External Integrations]
- **[Service 1]**: [Description and integration pattern]
- **[Service 2]**: [Description and integration pattern]

## Common Development Tasks

### Adding New [Feature/Entity/Component]
1. Create [main files] in appropriate [module/package]
2. Create [data layer] interfaces
3. Create [business logic] layer
4. Create [API/presentation] layer with proper authorization
5. Add [schema changes/migrations]
6. Write comprehensive tests

### [External Integration] Tasks
1. Create [integration models] in appropriate package
2. Implement [authentication/error handling] patterns
3. Add [data synchronization] methods
4. Consider impact on existing [features/data]

### Adding New [API Endpoints/Routes]
1. Create [controller/route handler] 
2. Implement [authentication/authorization]
3. Add [validation/error handling]
4. Create corresponding [service methods]
5. Write [integration tests]

## Security Considerations

- [Authentication method] validation
- [Authorization system]: [list roles/permissions]
- [API security]: [rate limiting, CORS, headers]
- [Data protection]: [encryption, PII handling]
- [Configuration security]: [environment variables, secrets management]

## Troubleshooting

### Common Issues
- **[Common Issue 1]**: [Solution/check]
- **[Common Issue 2]**: [Solution/check]
- **[External Service]**: [Common problems and solutions]

### Debugging
- Enable [logging configuration]
- Use [debugging tools/endpoints]
- [Performance monitoring] setup

---

## Remember Shortcuts

Remember the following shortcuts which the user may invoke at any time.

### TNEW

When I type "tnew", this means:

```
Understand all BEST PRACTICES listed in this development guide.
Your code SHOULD ALWAYS follow these best practices.
Pay special attention to architecture patterns and external integration guidelines.
```

### TPLAN
When I type "tplan", this means:
```
Analyze similar parts of the codebase and determine whether your plan:
- is consistent with existing architecture and module structure
- follows external integration patterns if applicable
- introduces minimal changes
- reuses existing code
- considers security, performance, and scalability implications
```

## TCODE

When I type "tcode", this means:

```
Implement your plan and make sure your new tests pass.
Always run tests to make sure you didn't break anything else.
Always run [formatting tool] on the newly created files to ensure standard formatting.
Always run [build/compile command] to make sure compilation passes.
Test with appropriate [environment/configuration].
```

### TREF

When I type "tref", this means:

```
Prepare for safe refactoring by creating a checkpoint and working branch:

1. Stage and commit any current work:
   git add .
   git commit -m "checkpoint: save work before refactoring"

2. Create a working branch for the refactoring:
   git checkout -b $(git branch --show-current)-working

3. Proceed with refactoring on this working branch.

Use this BEFORE any significant refactoring that:
- Touches multiple files/modules/classes/components
- Changes function/method/API signatures or structures  
- Modifies core business logic
- Could potentially break existing functionality
- Affects external integrations or core data models

SKIP this for minor changes like:
- Simple bug fixes
- Adding new functions/methods without changing existing ones
- Documentation updates
- Configuration changes
```

### TMERGE

When I type "tmerge", this means:

```
Complete refactoring by merging working branch back:

1. Ensure all tests pass on working branch
2. Switch back to original branch: git checkout <original-branch>
3. Merge the working branch: git merge <original-branch>-working
4. Delete the working branch: git branch -d <original-branch>-working
5. Push the merged changes: git push origin <original-branch>

If refactoring failed or broke things:
1. Switch back to original branch: git checkout <original-branch>  
2. Delete the working branch: git branch -D <original-branch>-working
3. You're back to your safe checkpoint!
```

### TCHECK

When I type "tcheck", this means:

```
You are a SKEPTICAL senior engineer familiar with this project's architecture.
Perform this analysis for every MAJOR code change you introduced (skip minor changes):

1. Development guide checklist: Writing Functions/Methods Best Practices.
2. Development guide checklist: Writing Tests Best Practices.
3. Development guide checklist: Implementation Best Practices.
4. Architecture and module organization compliance.
5. External integration impact assessment.
```

### TCHECKF

When I type "tcheckf", this means:

```
You are a SKEPTICAL senior engineer familiar with this project's architecture.
Perform this analysis for every MAJOR function/method you added or edited (skip minor changes):

1. Development guide checklist: Writing Functions/Methods Best Practices.
```

### TCHECKT

When I type "tcheckt", this means:

```
You are a SKEPTICAL senior engineer familiar with this project's architecture.
Perform this analysis for every MAJOR test you added or edited (skip minor changes):

1. Development guide checklist: Writing Tests Best Practices.
```

### TUX

When I type "tux", this means:

```
Imagine you are a human UX tester of the feature you implemented. 
Output a comprehensive list of scenarios you would test, sorted by highest priority.
Consider key user workflows, external integrations, and platform considerations.
```

### TGIT

When I type "tgit", this means:

```
Add all changes to staging, create a commit, and push to remote.

Follow this checklist for writing your commit message:
- SHOULD use Conventional Commits format: https://www.conventionalcommits.org/en/v1.0.0
- SHOULD NOT refer to Claude or Anthropic in the commit message.
- SHOULD structure commit message as follows:
<type>[optional scope]: <description>
[optional body]
[optional footer(s)]
- commit SHOULD contain the following structural elements to communicate intent: 
fix: a commit of the type fix patches a bug in your codebase (this correlates with PATCH in Semantic Versioning).
feat: a commit of the type feat introduces a new feature to the codebase (this correlates with MINOR in Semantic Versioning).
BREAKING CHANGE: a commit that has a footer BREAKING CHANGE:, or appends a ! after the type/scope, introduces a breaking API change (correlating with MAJOR in Semantic Versioning). A BREAKING CHANGE can be part of commits of any type.
types other than fix: and feat: are allowed, for example @commitlint/config-conventional (based on the Angular convention) recommends build:, chore:, ci:, docs:, style:, refactor:, perf:, test:, and others.
footers other than BREAKING CHANGE: <description> may be provided and follow a convention similar to git trailer format.
```

This template provides a comprehensive development workflow that teams can immediately adopt for any technology stack. The T-command system and refactoring safety workflows have been proven effective in production environments.