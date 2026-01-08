# Planned build: scopes, roles, and bindings

This registry is a **catalog-only** source of reusable governance building blocks:

- **Patterns**: reusable architecture patterns (no instantiations)
- **Contracts**: interface/shape requirements that patterns can compose
- **Policies**: governance rules modules can apply

Modules (and project-specific “build” artifacts) live outside this repo (for example in `~/.local/local-governor`).

## Scope levels

Every artifact declares a `scope.level` that describes how broadly it is intended to apply.

Recommended meanings:

- `component`: One cohesive subsystem within a repo (often a folder boundary with a single responsibility).
- `module`: A single module boundary (library module, service module, adapter module).
- `package`: A distributable package (often a published unit).
- `repo`: A repository-wide convention or layout.
- `org`: An organization-wide convention spanning multiple repos.
- `multi-repo`: A coordinated set of repos that together form one product/workspace.
- `system`: Ecosystem-level conventions.

Notes:

- Scope is **intent**, not enforcement. Enforcement is handled by tooling and by project build files.
- Prefer the smallest scope that fits: start at `component`/`module`, escalate only when needed.

## Roles

Artifacts may optionally declare `scope.roles` as a list of role ids (kebab-case strings) that are relevant for adoption and review.

Roles are intended to communicate **accountability** (who should care) rather than to imply an org chart.

Examples (non-normative): `security-review`, `platform-review`, `data-steward`, `operator`, `api-owner`.

## Binding patterns/contracts/policies in projects (LLM-soft)

Projects bind to catalog artifacts via project-owned governance files (for example module/build manifests). The binding lives with the code it governs.

Example (illustrative):

```yaml
kind: module
metadata:
  name: storacle-rpc
  version: "0.1.0"

implements:
  - pattern: semantic-client@0.1.0
    at: src/storacle/clients/
  - pattern: executor-owned-auth@0.1.0
    at: src/storacle/rpc.py
```

Guidance for LLM-assisted work:

- Treat this registry as **constraints and vocabulary**, not as a generator of code.
- Bind artifacts to **specific surfaces/components** (via `at:`) to avoid contradictory “global” application.
- If a pattern’s scope is broader than the place you’re binding it, add a note in the project build file explaining the local interpretation.

## Registry layout

Patterns are organized by scope level:

- `patterns/<level>/<name>/<name>.pattern.yaml`

For editor schema validation in pattern YAML files:

```yaml
# yaml-language-server: $schema=../../../schemas/pattern.schema.json
```
