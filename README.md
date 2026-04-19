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

## Validation

Local validation:

```bash
python -m pip install jsonschema==4.22.0
python scripts/validate_catalog.py
```

CI validation:
- runs on pushes to `main`
- runs on pull requests affecting catalog, schema, validator, or workflow files
- fails the build if any catalog JSON file no longer conforms to the schema

## Design notes

The catalog intentionally separates:
- authority
- execution
- proof
- presentation

This repository currently stores the workflow catalog only. It does not yet contain execution logic, evidence bundles, or certification packaging.

## Next useful additions

- normalized enums for owner and clause references
- dedicated schema for `iso27001_mapping`
- golden fixtures for valid and invalid workflow rows
- CSV/JSONL export generation
