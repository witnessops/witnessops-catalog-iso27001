# witnessops-catalog-iso27001

Machine-readable ISO/IEC 27001 workflow catalog for WitnessOps.

## Purpose

This repository holds a structured catalog of workflows aligned to ISO/IEC 27001 as an implementation and operating catalog.

Boundary:
- this is an implementation catalog, not an official ISO schema
- it is intended to support ISMS workflow design, ownership, and evidence handling
- the current standard baseline used here is ISO/IEC 27001:2022 with Amendment 1:2024 applied as current ISO publication context
- this repository does not reproduce the full standard text

## Current files

- `catalog/iso27001-workflows.v1.json` — initial machine-readable workflow catalog
- `schemas/workflow-catalog.schema.json` — top-level catalog schema
- `schemas/iso27001-mapping.schema.json` — existing dedicated mapping schema
- `schemas/enums/` — retained owner, clause, and deadline-type enum documents
- `tests/fixtures/` — existing workflow-row and mapping examples, including invalid cases
- `scripts/validate_catalog.py` — local validator for catalog JSON files
- `.github/workflows/validate-catalog.yml` — CI gate enforcing schema validation on push and pull request

## Data contract

Each workflow row contains:

- `workflow_id`
- `workflow_name`
- `trigger`
- `owner`
- `deadline`
- `required_evidence`
- `status_states`
- `iso27001_mapping`

## Mapping contract

`iso27001_mapping` currently stores:
- `clauses` — clause references used by the workflow
- `isms_surface` — high-level implementation surface, such as risk management, internal audit, or management review

This repository starts clause-oriented rather than Annex-A-oriented.

The top-level schema already references the dedicated mapping schema. Owner
constraints are defined in the top-level schema's `$defs.ownerEnum`; clause
constraints are in the mapping schema's `$defs.isoClauseEnum`. The standalone
enum documents are not those `$ref` targets. Changing an enum document alone
does not change these active schema constraints.

## Validation

Local validation:

```bash
python -m pip install jsonschema==4.22.0
python scripts/validate_catalog.py
```

CI validation:
- runs on pushes to `main` affecting the configured catalog, schema, validator, or workflow paths
- runs on pull requests affecting catalog, schema, validator, or workflow files
- fails the build if any catalog JSON file no longer conforms to the schema

The validator iterates `catalog/*.json`; it does not replay the standalone files
under `tests/fixtures/`. Fixture presence is not fixture-test acceptance.
README-only changes do not trigger the path-filtered catalog workflow. Catalog
validation establishes structural conformance, not ISO certification, legal
applicability, or operational evidence.

## Design notes

The catalog intentionally separates:
- authority
- execution
- proof
- presentation

This repository currently stores the workflow catalog only. It does not yet contain execution logic, evidence bundles, or certification packaging.

## Next useful additions

The enum definitions, dedicated mapping schema, and example fixtures listed
above already exist. The items below are possible extensions, not approval to
change catalog semantics or claims that those structures are still absent:

- extend owner/clause coverage or mapping fields only for a concrete catalog need, with separate schema review
- expand valid/invalid workflow and mapping fixtures and add explicit fixture replay when that work is selected
- CSV/JSONL export generation
