# Codex Security Threat Model — witnessops-catalog-iso27001

Status: `repo_prep_seed_for_codex_security`

This document is a repository-specific seed for Codex Security review and GitHub PR review. It is not a vulnerability report, not a scan result, not legal advice, not an official ISO interpretation, and not proof of ISO/IEC 27001 certification or compliance.

## Scope

This repository is the machine-readable ISO/IEC 27001 workflow catalog for WitnessOps.

It owns:

- ISO/IEC 27001-aligned workflow catalog rows under `catalog/`
- catalog schemas under `schemas/`
- workflow-row fixtures under `tests/fixtures/`
- local catalog validation through `scripts/validate_catalog.py`
- CI validation for catalog, schema, validator, and workflow changes
- implementation support for ISMS workflow design, ownership, and evidence handling

## Out of scope

This repository does not own:

- official ISO standard text
- official ISO schema authority
- certification decisions
- legal applicability decisions
- audit opinions
- source-system evidence
- evidence bundles
- certification packaging
- proof-run execution
- proof-engine package generation
- offline verifier implementation
- public website presentation
- customer evidence custody
- production compliance claims

Do not infer that a passing Codex Security review verifies any out-of-scope system.

## Authority boundaries

- `main` in `witnessops/witnessops-catalog-iso27001` is the code/content authority for this catalog repo.
- `schemas/` defines catalog structure only.
- `catalog/` contains implementation catalog rows only.
- `tests/fixtures/` proves expected validator behavior.
- `scripts/validate_catalog.py` is the local validation mechanism.
- Catalog validity is structural/catalog validity only; it is not ISO certification, audit acceptance, legal applicability, operational proof, or compliance proof.
- Codex Security may identify findings and suggest patches.
- Codex Security findings do not authorize merge, release, catalog-semantic changes, schema-semantic changes, fixture truth changes, legal interpretation, certification claims, execution behavior, proof claims, deploy, or customer-impacting changes.
- Human maintainer review remains required for changes that affect catalog rows, schema acceptance, ISO mapping language, fixture truth, validator behavior, or certification/compliance-language boundaries.

## Primary review surfaces

Treat the following as first-class review surfaces:

1. `catalog/iso27001-workflows.v1.json`
   - workflow IDs and names
   - triggers and owners
   - deadlines
   - required evidence
   - status states
   - ISO 27001 mapping
   - no overclaim that catalog row equals certification or legal applicability

2. `schemas/workflow-catalog.schema.json`
   - top-level workflow row contract
   - required fields
   - `additionalProperties` boundaries
   - owner and mapping constraints

3. `tests/fixtures/`
   - valid workflow-row fixtures
   - invalid workflow-row fixtures
   - owner, mapping, or required-field failure behavior

4. `scripts/validate_catalog.py`
   - local schema resolution
   - catalog validation behavior
   - fixture corpus behavior
   - no implicit network fetch reliance

5. `.github/workflows/validate-catalog.yml`
   - deterministic validation for catalog/schema/validator changes
   - no secrets or external system dependency

6. `README.md` and docs
   - boundary language
   - no protected/full ISO standard text reproduction
   - no certification or compliance overclaims

## Untrusted inputs

Review all handling of:

- catalog row JSON
- schema JSON
- fixture JSON
- deadline values
- owner values
- ISO clause references
- ISMS surface strings
- validator path resolution
- schema `$ref` resolution if introduced later
- any value that resembles real customer evidence, confidential audit material, certification records, secrets, credentials, tokens, production system names, private evidence paths, or private client data

## Security invariants

The following must remain true unless an explicit design change is reviewed and approved:

- This repo must not be described as an official ISO schema.
- This repo must not make legal applicability, audit, or certification decisions.
- Catalog validity must not be presented as ISO/IEC 27001 certification, audit readiness, or compliance proof.
- The repo must not reproduce protected/full ISO standard text.
- Valid fixtures must pass and invalid fixtures must fail.
- Invalid fixture coverage must not be weakened to make catalog changes pass.
- Catalog rows must not include production customer data, private evidence, confidential audit material, secrets, credentials, tokens, or private system details.
- Authority, execution, proof, and presentation must remain separate.

## High-priority finding classes

Treat the following as P1 for review purposes:

- invalid fixtures validate successfully
- valid fixtures stop proving intended behavior because validator coverage is weakened
- schema accepts undeclared fields that can smuggle legal, proof, evidence, authority, audit, or certification claims
- validator begins relying on implicit network fetches for local schemas
- catalog row includes secrets, customer evidence, confidential audit material, credentials, tokens, production targets, or private evidence paths
- docs or catalog language claims official ISO authority, legal applicability, audit success, certification, or compliance proof without a named mechanism outside this repo
- protected/full ISO standard text is copied into repo files
- schema or catalog changes erase required evidence or status-state semantics in a way that makes workflow rows less bounded

## Lower-priority but relevant finding classes

Review but do not automatically treat as P1 without demonstrated impact:

- cosmetic README wording that preserves boundaries
- missing web-app security headers, because this repo is not a web app
- dependency advisories not reachable through local validation behavior
- broad performance concerns without a concrete schema-validation amplification path

## Review instructions for Codex

When reviewing this repository:

- prefer small, surgical findings over broad refactors
- name the affected catalog row, schema, fixture, validator path, workflow, or documentation boundary
- include a concrete schema-bypass, fixture-drift, overclaim, protected-text, or local-resolution failure path where possible
- do not weaken schemas or negative fixtures to make catalog rows pass
- do not add legal interpretation, official ISO claims, certification claims, compliance proof claims, execution logic, proof-engine behavior, verifier behavior, or customer evidence
- do not add production credentials, customer data, confidential audit material, protected standard text, or private proof bundles as fixtures
- preserve `python scripts/validate_catalog.py` as the baseline validation command unless a separate tooling lane changes it

## Suggested Codex Security scan configuration

Initial scan seed:

- repository: `witnessops/witnessops-catalog-iso27001`
- branch: `main`
- history window: `180 days`
- environment family: `Python / JSON Schema catalog`
- setup command: `python -m pip install jsonschema==4.22.0`
- validation command for proposed catalog/schema patches: `python scripts/validate_catalog.py`
- agent secrets: none
- production credentials: prohibited
- customer data fixtures: prohibited
- private evidence fixtures: prohibited
- protected/full ISO standard text: prohibited
- certification or compliance proof claims: prohibited

## Closure condition for this prep artifact

This prep artifact is sufficient when:

- Codex Security scan context can be seeded from this file.
- `AGENTS.md` points reviewers to this file.
- A private-reporting `SECURITY.md` exists for the repo.
- No catalog rows, schemas, fixtures, validator behavior, workflow behavior, production settings, secrets, customer evidence, legal interpretation, certification claims, compliance claims, protected standard text, or proof claims were changed by this prep pass.
