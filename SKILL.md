---
name: svg-create
description: >-
  Creates valid standalone .svg files: dark minimal diagrams, structural
  architecture diagrams (knowledge and engineering types), flowcharts, and
  node graphs. Use for SVG, vector diagrams, .svg edits, or embeddable graphics.
---

# SVG Create

## Purpose

Produce **valid standalone `.svg`** files: explicit `viewBox`, semantic XML structure, crisp vectors, dark minimal styling.

**In scope:** `.svg` create, edit, restyle; six **structural diagram types**. **Out of scope:** React/TSX, React Flow, HTML canvas, CSS-only graphics, animated web UI.

## Quick Start

**Structural diagram:**

1. Classify type → [structural-spec.md](references/structural-spec.md#diagram-type-selection)
2. Model nodes/edges → [knowledge-diagrams.md](references/knowledge-diagrams.md) or [engineering-diagrams.md](references/engineering-diagrams.md)
3. Layout ID → [layouts.md](references/layouts.md#diagram-type--layout-id)
4. Tokens → [tokens.md](references/tokens.md#semantic-bindings)
5. Implement → [quality.md](references/quality.md); check [checklists.md](references/checklists.md) L1 → L0

**Generic SVG:** nodes from user → [layouts.md](references/layouts.md) graph-shape matrix → [tokens.md](references/tokens.md) + [quality.md](references/quality.md).

## Structural diagram types

| Family | Type | Spec |
|--------|------|------|
| Knowledge | Concept Tree | [knowledge-diagrams.md#concept-tree](references/knowledge-diagrams.md#concept-tree) |
| Knowledge | Capability Map | [knowledge-diagrams.md#capability-map](references/knowledge-diagrams.md#capability-map) |
| Knowledge | Learning Path | [knowledge-diagrams.md#learning-path](references/knowledge-diagrams.md#learning-path) |
| Knowledge | Domain Model | [knowledge-diagrams.md#domain-model](references/knowledge-diagrams.md#domain-model) |
| Engineering | Module Dependency | [engineering-diagrams.md#module-dependency](references/engineering-diagrams.md#module-dependency) |
| Engineering | Data Flow | [engineering-diagrams.md#data-flow](references/engineering-diagrams.md#data-flow) |
| Engineering | C4 Level 2 Container | [engineering-diagrams.md#c4-level-2-container](references/engineering-diagrams.md#c4-level-2-container) |

Cross-type rules and glossary: [structural-spec.md](references/structural-spec.md).

## Intent matrix

| User intent | Action | Reference |
|-------------|--------|-----------|
| Concept taxonomy | structural | Concept Tree |
| Business capabilities | structural | Capability Map |
| Curriculum / onboarding | structural | Learning Path |
| DDD domain structure | structural | Domain Model |
| Module depends-on | structural | Module Dependency |
| Logical data movement | structural | Data Flow |
| C4 containers | structural | C4 L2 |
| Generic flowchart / graph | generic | layouts + tokens + quality |
| edit / restyle | edit | Preserve topology, `viewBox`, `id`s |
| recolor only | edit | `fill`/`stroke` only |

## Guardrails

- Well-formed SVG (`xmlns`, `viewBox`).
- Do not add nodes/edges user did not imply.
- On `edit`, preserve geometry unless restructure requested.
- No HTML/React wrappers.
- **Structural:** one type per file (SD-S-005); no mixed knowledge/engineering roles (SD-S-004) unless user requests derived view.
- Closed node/edge enums only.

## Workflow

```
- [ ] 1. Structural type or generic
- [ ] 2. List node/edge roles (structural: from type spec)
- [ ] 3. Layout ID from layouts.md matrix
- [ ] 4. viewBox + tokens
- [ ] 5. Draw; legend if required
- [ ] 6. checklists L1 → quality L0 → deliver
```

SOP: [structural-spec.md § Seven-step SOP](references/structural-spec.md#seven-step-sop).

## Validation

- [ ] [quality.md § L0](references/quality.md#l0--markup--export)
- [ ] Structural: [checklists.md](references/checklists.md) L1 + L0-S items

## Delivery format

1. **Files** — `.svg` path(s)
2. **Diagram type** — six types or `generic`
3. **Structure** — node/edge summary with roles
4. **Layout** — layout ID
5. **Rule IDs** — satisfied; exceptions noted
6. **Checklists** — L0, L1 (structural), L2 if applicable
7. **Deviations** — token overrides

## References

| File | Role |
|------|------|
| [structural-spec.md](references/structural-spec.md) | Selection, SOP, boundaries, glossary |
| [knowledge-diagrams.md](references/knowledge-diagrams.md) | 4 knowledge types |
| [engineering-diagrams.md](references/engineering-diagrams.md) | 3 engineering types |
| [checklists.md](references/checklists.md) | L1, L2; L0 → quality |
| [layouts.md](references/layouts.md) | Layout IDs + type matrix |
| [tokens.md](references/tokens.md) | Visual + semantic bindings |
| [quality.md](references/quality.md) | L0 markup |
