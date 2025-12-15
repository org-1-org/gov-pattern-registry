# gov-pattern-registry

Public, catalog-only registry of governance building blocks.

## What belongs here

- `pattern`: reusable architecture patterns (no instantiations)
- `contract`: interface/shape requirements patterns can compose
- `policy`: governance rules that modules can apply
- `examples/`: non-normative reference implementations (not validated)

**Guardrail:** `module` artifacts do **not** belong in this repo. Modules live in the org repo (e.g., `~/.local/local-governor`) and reference catalog artifacts. The `module.schema.json` is provided for tooling that validates modules in other repos.

## Layout + naming

Directory layout:

- `patterns/<name>/<name>.pattern.yaml`
- `contracts/<name>/<name>.contract.yaml`
- `policies/<name>/<name>.policy.yaml`
- `schemas/*.schema.json` (JSON Schema for each kind)
- `examples/<project>/` (non-normative examples)

References inside YAML use `name@x.y.z` (or `name` if versionless).

## Validation

Schemas are intended to be used by tooling for validation. A quick local check can validate all YAML files by loading `schemas/*.schema.json` and validating each artifact by its `kind`.

For editor support, add this directive at the top of YAML files:

```yaml
# yaml-language-server: $schema=../../schemas/pattern.schema.json
```

## Validation

Schemas are intended to be used by tooling for validation. A quick local check can validate all YAML files by loading `schemas/*.schema.json` and validating each artifact by its `kind`.
