# AGENTS.md

## Identity

This repository is the machine-readable ISO/IEC 27001 workflow catalog for WitnessOps. It is a catalog and schema repo, not an official ISO schema, not a certification authority, not legal advice, not an execution engine, and not a proof package producer.

## Ownership

This repo owns:

- ISO/IEC 27001-aligned workflow catalog rows under `catalog/`
- catalog schemas under `schemas/`
- workflow-row fixtures under `tests/fixtures/`
- local catalog validation through `scripts/validate_catalog.py`
- CI validation for catalog, schema, validator, and workflow changes

This repo does not own:

- official ISO standard text
- official ISO schema authority
- certification decisions
- legal applicability decisions
- source-system evidence
- evidence bundles
- certification packaging
- proof-run execution
- proof-engine package generation
- offline verifier implementation
- public website presentation
- customer evidence custody

## Non-Negotiable Rules

- Do not describe this repository as an official ISO schema or certification authority.
- Do not reproduce protected/full ISO standard text.
- Do not let catalog coherence imply ISO certification, legal applicability, audit success, or operational proof.
- Do not weaken schemas or fixture behavior to make a catalog row pass.
- Do not remove negative fixtures unless replacing them with equal or stronger failure coverage.
- Do not add execution logic, evidence bundles, certification packaging, production customer data, secrets, credentials, tokens, or private evidence.
- Keep authority, execution, proof, and presentation separate.

## Codex Security review

Use [`docs/CODEX_SECURITY_THREAT_MODEL.md`](./docs/CODEX_SECURITY_THREAT_MODEL.md) as the seed context for Codex Security review.

Codex Security may identify findings and propose patches, but it does not authorize merge, release, catalog-semantic changes, schema-semantic changes, fixture truth changes, legal interpretation, certification claims, execution behavior, proof claims, deploy, or customer-impacting changes.

For security-sensitive changes, preserve these boundaries:

- the catalog is implementation support, not official ISO authority
- schemas define catalog structure only
- valid fixtures must pass and invalid fixtures must fail
- catalog validity is not proof that an organization is certified, compliant, audit-ready, or in scope
- ISO references must remain bounded to permitted references and must not reproduce protected standard text

## Validation

Install validator dependency:

```bash
python -m pip install jsonschema==4.22.0
```

Run catalog validation:

```bash
python scripts/validate_catalog.py
```

GitHub Actions runs the same validator for catalog, schema, validator, and workflow changes.
