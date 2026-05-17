# Structural Diagram Spec (v1)

Cross-type rules, glossary, selection, and SOP for **six structural diagram types** as static SVG. Type details: [knowledge-diagrams.md](knowledge-diagrams.md), [engineering-diagrams.md](engineering-diagrams.md). Visuals: [tokens.md](tokens.md), [layouts.md](layouts.md), [quality.md](quality.md). Checklists: [checklists.md](checklists.md).

**Out of scope:** sample SVGs, CI/lint, C4 L1-only context posters, deployment topology, sequence diagrams.

## Document map

| File | Role |
|------|------|
| [structural-spec.md](structural-spec.md) | This file — boundaries, glossary, SOP, selection |
| [knowledge-diagrams.md](knowledge-diagrams.md) | Concept Tree, Capability Map, Learning Path, Domain Model |
| [engineering-diagrams.md](engineering-diagrams.md) | Module Dependency, Data Flow, C4 L2 Container |
| [layouts.md](layouts.md) | Layout IDs + **diagram-type → layout matrix** (single source) |
| [tokens.md](tokens.md) | Visual tokens + **semantic role bindings** (single source) |
| [quality.md](quality.md) | L0 SVG markup (single source) |
| [checklists.md](checklists.md) | L1 per type, L2 publish; L0 → quality.md |

One **SVG file = one diagram type** unless the user explicitly requests a derived composite (document exceptions in delivery).

## Diagram-type selection

| Goal | Audience | Diagram type |
|------|----------|----------------|
| Taxonomy of ideas | Learners, analysts | Concept Tree |
| Outcome-oriented abilities | Product, architecture | Capability Map |
| Ordered curriculum / onboarding | L&D, tech leads | Learning Path |
| DDD concepts and relationships | Domain experts, devs | Domain Model |
| Package / module depends-on | Developers | Module Dependency |
| Logical data movement | Developers, integration | Data Flow |
| Deployable containers in one system | Architects | C4 Level 2 Container |

**Shortcuts:** pedagogical order → Learning Path; business concepts → Domain Model; deployable units → C4 L2; sub-container packages → Module Dependency.

**Generic SVG:** no listed type → [layouts.md](layouts.md) + [tokens.md](tokens.md) + [quality.md](quality.md) only.

## Seven-step SOP

1. Clarify intent and audience.
2. Select diagram type (table above).
3. Model nodes/edges from type spec (closed enums).
4. Pick layout ID from [layouts.md § Diagram type → Layout ID](layouts.md#diagram-type--layout-id).
5. Apply [tokens.md § Semantic bindings](tokens.md#semantic-bindings).
6. Implement SVG per [quality.md](quality.md).
7. [checklists.md](checklists.md) L1 → [quality.md § L0](quality.md#l0--markup--export); L2 if publishing.

## Rule entry schema

```text
ID:        SD-{K|E}-{TYPE}-{nnn}
Level:     MUST | MUST NOT
Applies-to: diagram type or AllStructural
Node/Edge:  role name(s) or "—"
Layout:     layout ID or "—" (see layouts.md matrix)
Token-ref:  see tokens.md or "—"
Rationale / Violation: one sentence each
```

## Naming and IDs

| Item | Convention |
|------|------------|
| SVG group | `<g id="node-{kebab-id}">` |
| Layers | `row-{n}`, `lane-{n}`, `group-{id}` per [layouts.md](layouts.md) |
| Caption (delivery) | `{Diagram type} — {scope} — spec v1` |

**SD-S-001** MUST use kebab-case for `node-{id}`. **SD-S-002** MUST NOT duplicate `id`s.

## Abstraction span

| Type | Max levels |
|------|------------|
| Default | 2 |
| Learning Path | 1 primary chain per file |
| C4 L2 | 2 (boundary + containers) |
| Domain Model | 2 |

**SD-S-003** MUST NOT use three or more semantic levels on one canvas without documented exception.

## One type per file

**SD-S-004** MUST NOT mix knowledge and engineering node roles on one canvas unless user requests a derived view (document exceptions).

**SD-S-005** MUST NOT apply two diagram type specs to one file.

## Knowledge ↔ engineering boundaries

| Risk | Rule |
|------|------|
| Domain Model vs C4 L2 | **SD-S-010** Aggregates/entities MUST NOT be containers. **SD-S-011** Containers = deployable boundaries only. |
| Capability vs Module | **SD-S-012** No capabilities on Module Dependency. **SD-S-013** No modules on Capability Map. |
| Learning Path vs Data Flow | **SD-S-014** No `edge-data` for `precedes`. **SD-S-015** No runtime flow on Learning Path. |
| Data Flow vs C4 L2 | **SD-S-016** No packet-level flow on C4 L2. **SD-S-017** No Data Flow processes for container `uses`. |
| Module vs C4 L2 | **SD-S-018** All deployable boxes → C4 L2. **SD-S-019** Module Dependency = sub-container only. |

## Shared vs exclusive symbols

| Role / edge | Knowledge | Engineering |
|-------------|-----------|---------------|
| `concept`, `capability`, `learning-unit` | Yes | No |
| `aggregate`, `entity`, `value-object` | Yes | No |
| `module`, `process`, `data-store` | No | Yes |
| `container`, `external-system`, `person` | No | Yes |
| `precedes` | Learning Path | No |
| `depends-on`, `flows-to`, `uses` | No | Yes |

Full bindings: [tokens.md](tokens.md#semantic-bindings).

## Layout and density

**SD-S-020** One layout ID per file — [layouts.md](layouts.md). **SD-S-021** MUST NOT mix `hub-spoke` and `swimlane` unless user requests.

**SD-S-022** Split files when exceeding type limits or defaults: nodes >20, edges >30 (stricter limits in type specs).

**SD-S-023** Legend if ≥4 palette slots or ≥3 non-default edge classes. **SD-S-024** Caption in delivery per naming table.

## Multi-diagram bundles

Review order: Domain Model / Capability Map → C4 L2 → Module Dependency → Data Flow. **SD-S-025** Consistent names across the set.

## Change policy

| Change | Action |
|--------|--------|
| New edge type | Update type spec + tokens + L1 checklist |
| New layout ID | Update layouts.md matrix only |
| Deprecated rule | Keep ID; mark Deprecated |
| Breaking change | New major spec version; tag old SVGs in caption |

---

## Glossary {#glossary}

Canonical English for labels, legends, and captions.

### Knowledge

| Term | Definition |
|------|------------|
| **Concept** | Named idea in a taxonomy (not deployable). |
| **Concept Tree** | Hierarchy of concepts (broader/narrower). |
| **Capability** | Outcome-oriented ability (not module/container). |
| **Capability Map** | Grouped capabilities by domain or level. |
| **Learning Unit** | Lesson, module, lab, or checkpoint. |
| **Learning Path** | Ordered learning units. |
| **Domain Model** | Aggregates, entities, value objects, domain links. |
| **Aggregate** | DDD consistency boundary. |
| **Entity** | Domain object with identity. |
| **Value Object** | Immutable, no identity (optional). |
| **Bounded Context** | Linguistic boundary as group frame. |

### Engineering

| Term | Definition |
|------|------------|
| **Module** | Package, library, or compile unit. |
| **Module Dependency** | Depends-on between modules. |
| **Data Flow** | Logical data movement (not physical network). |
| **Process** | Transforms or routes data. |
| **Data Store** | Holds data in a flow diagram. |
| **Container** | C4 deployable/runnable unit. |
| **C4 Level 2 Container** | Containers in one software system. |
| **Software System** | C4 system scope for one L2 diagram. |
| **External System** | Outside the system under design. |

### Shared

| Term | Definition |
|------|------------|
| **Diagram type** | One of six types or `generic`. |
| **Node role** / **Edge role** | Semantic class of shape or link. |
| **Layout ID** | Pattern from [layouts.md](layouts.md). |
| **L0 / L1 / L2** | Markup / per-type / publish checklists. |

### C4 / DDD

| Term | Diagram |
|------|---------|
| C4 Context (L1) | Out of scope v1 |
| C4 Component (L3) | Use Module Dependency |
| Aggregate, Entity, VO | Domain Model |
| Bounded Context | Domain Model or Capability Map band |
