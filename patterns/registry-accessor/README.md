# registry-accessor (migration note)

This pattern previously existed as three files:
- `registry-accessor.arch.yaml`
- `registry-accessor.policy.yaml`
- `registry-accessor.state.yaml`

It is now represented as a single pattern artifact:
- `registry-accessor.pattern.yaml`

Rationale:
- The old triad encouraged conversational, non-checkable content.
- The new catalog uses explicit suffixes: `.pattern.yaml`, `.contract.yaml`, `.policy.yaml`, `.module.yaml`.
