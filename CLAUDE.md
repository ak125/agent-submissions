# CLAUDE.md

## Project Overview

This is the **agent-submissions** repository — a bundle management system for OpenClaw-generated code changes targeting the `nestjs-remix-monorepo`. Bundles contain signed (HMAC-SHA256) patches, manifests, evidence, and constraints that flow through an automated validation pipeline before human review.

## Repository Structure

```
agent-submissions/
├── bundles/          # Signed code change bundles (one directory per bundle)
│   └── bundle-*/     # Each bundle: manifest.json, changes.patch, evidence.json, constraints.json, report.md
├── logs/             # Agent execution logs
├── constraints.json  # Global governance constraints
├── evidence.json     # Validation evidence template
└── README.md         # Workflow documentation (French)
```

## Workflow

1. OpenClaw generates a bundle in `bundles/`
2. Bundle is pushed to this repo on a feature branch
3. Airlock imports and validates the bundle
4. Automatic PR created against `nestjs-remix-monorepo`
5. Human review and merge

## Target Monorepo Tech Stack

- **Backend:** NestJS (TypeScript, strict mode)
- **Frontend:** Remix (React)
- **Validation:** Zod schemas
- **Database:** Supabase
- **Package manager:** npm

## Validation Commands (run against the target monorepo)

```sh
npm test          # Unit/integration tests
npm run lint      # ESLint/Prettier
npm run typecheck # tsc --noEmit (strict mode)
npm run build     # Full build
```

## Governance Rules

- **Allowed paths:** `backend/src/**`, `frontend/app/**`, `packages/**`
- **Forbidden paths:** `.env`, `*.key`, `credentials/**`
- **Deployment target:** `main` branch
- **All validation gates must pass:** tests, lint, typecheck
- **Human approval required** before merge
- **Security:** Zero-trust model — read-only monorepo access, write-only bundle submission

## Bundle Format

Each bundle directory must contain:

| File               | Purpose                                      |
|--------------------|----------------------------------------------|
| `manifest.json`    | Bundle metadata, file list, HMAC-SHA256 signature |
| `changes.patch`    | Git-format patch with the code modifications |
| `evidence.json`    | Validation results (tests, lint, typecheck)  |
| `constraints.json` | Bundle-specific enforcement rules            |
| `report.md`        | Human-readable change analysis               |

## Coding Standards (for bundle contents)

- No `any` types in TypeScript — use `unknown`, specific interfaces, or `Record<string, unknown>`
- Strict null checks enabled
- Follow existing NestJS patterns (decorators, dependency injection)
- Zod for runtime validation at API boundaries
