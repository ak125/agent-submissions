# Agent Submissions

Ce repository stocke les bundles générés par OpenClaw pour validation et intégration.

## Structure

-  - Bundles de changements signés (HMAC-SHA256)
-  - Logs d'exécution des agents

## Workflow

1. OpenClaw génère un bundle dans 
2. Bundle poussé vers ce repo (branche )
3. Airlock importe et valide le bundle
4. PR automatique créée vers nestjs-remix-monorepo
5. Review humaine + merge

## Sécurité

- ✅ Bundles signés (HMAC-SHA256)
- ✅ Zero-Trust (read-only monorepo, write bundles only)
- ✅ ADR compliance (REG-001, ADR-002/007/008/009)
