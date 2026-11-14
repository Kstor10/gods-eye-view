# Plans & Architecture Decisions

This folder contains implementation plans and Architecture Decision Records (ADRs).

## What Goes Here

### Implementation Plans
Created by `/plan [feature]` command. Format:
```
plans/YYYY-MM-DD-feature-name.md
```

Example: `plans/2026-02-15-user-authentication.md`

### Architecture Decision Records (ADRs)
Significant technical decisions that affect the codebase structure. Format:
```
plans/adr-XXX-decision-title.md
```

Example: `plans/adr-001-use-postgresql-over-mongodb.md`

Use the template at `templates/adr-template.md`

## Current ADRs

| ADR | Title | Status | Date |
|-----|-------|--------|------|
| 001 | [Decision title] | Accepted | YYYY-MM-DD |
| 002 | [Decision title] | Proposed | YYYY-MM-DD |

## Implementation Plans Index

| Date | Feature | Status | Complexity |
|------|---------|--------|------------|
| YYYY-MM-DD | [Feature name] | ✅ Implemented | Medium |
| YYYY-MM-DD | [Feature name] | 🚧 In Progress | Complex |
| YYYY-MM-DD | [Feature name] | 📋 Planned | Simple |

## Workflow

1. **Before coding**: Run `/plan [feature]` to create implementation plan
2. **Review plan**: Discuss with team, iterate if needed
3. **Approve**: Give Claude explicit approval to proceed
4. **Implement**: Run `/implement [feature]`
5. **Mark complete**: Update status in this README

## When to Create an ADR

Create an ADR when:
- Choosing between significant alternatives (e.g., REST vs GraphQL)
- Making decisions with long-term impact (e.g., monolith vs microservices)
- Adopting new technologies or patterns (e.g., adding Redis)
- Establishing team conventions (e.g., error handling strategy)

**Don't create ADRs for**: Small refactorings, bug fixes, minor dependency updates

## Archive

After 6 months, move implemented plans to `plans/archive/` to keep this folder clean.
