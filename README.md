# Agent Submissions

Ce repository stocke les bundles generes par Claude API / Cowork pour validation et integration dans le monorepo AutoMecanik.

> **ADR-011 (2026-03-07)** : OpenClaw supprime. Claude API est le nouveau moteur de generation de bundles.

> **Status actuel** : En pause. Dernier bundle soumis : 2026-02-06 (`bundle-20260206001-messaging-gateway-typing`).

## Structure

- `bundles/` — Bundles de changements signes (HMAC-SHA256)
- `logs/` — Logs d'execution des agents

## Workflow

1. Claude API / Cowork genere un bundle
2. Bundle signe HMAC-SHA256 et pousse vers ce repo
3. Airlock importe et valide le bundle contre les regles ADR
4. PR automatique creee vers `nestjs-remix-monorepo`
5. Review humaine + merge

## Securite

- Bundles signes (HMAC-SHA256)
- Zero-Trust (read-only monorepo, write bundles only)
- ADR compliance (REG-001, ADR-002/007/008/009/011)

## References

- [ADR-002](https://github.com/ak125/governance-vault/blob/main/02-decisions/adr/ADR-002-airlock-zero-trust.md) — Airlock & Zero-Trust Agents (v2.0)
- [ADR-011](https://github.com/ak125/governance-vault/blob/main/02-decisions/adr/ADR-011-openclaw-claude-api-replacement.md) — Remplacement OpenClaw par Claude API
- [BUNDLE-SPEC](https://github.com/ak125/governance-vault/blob/main/03-policies/BUNDLE-SPEC.md) — Format obligatoire des bundles
