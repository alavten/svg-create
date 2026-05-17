# Knowledge Diagrams

Four knowledge-family types. Cross-type rules: [structural-spec.md](structural-spec.md). Layout matrix: [layouts.md](layouts.md#diagram-type--layout-id). Visual bindings: [tokens.md](tokens.md#semantic-bindings). Checklists: [checklists.md](checklists.md#l1--per-diagram-type).

---

## Concept Tree

**Purpose:** Hierarchical taxonomy of ideas. **Audience:** Analysts, curriculum designers. **Forbidden when:** Ordered steps (Learning Path) or capabilities (Capability Map).

**Nodes:** `concept`, `concept-root` (optional). **Edges:** `is-a`, `part-of` (optional).

**Abstraction:** ≤2 levels; split deeper trees by branch. **Density:** nodes ≤18, edges ≤24.

**Layout / tokens:** [layouts.md](layouts.md#diagram-type--layout-id) row **Concept Tree**; [tokens.md](tokens.md#semantic-bindings).

**Caption:** `Concept Tree — {scope} — spec v1`. Legend if ≥3 branch hues.

**SD-K-CT-001** MUST use only concept node roles. **SD-K-CT-002** Consistent `is-a` direction (note in caption). **SD-K-CT-003** MUST NOT use `precedes`, `depends-on`, `uses`, `flows-to`. **SD-K-CT-004** MUST NOT use deployable service/module names as concepts.

| ID | MUST NOT | Fix |
|----|----------|-----|
| SD-K-CT-N1 | Linear chain as "steps" | Learning Path + `precedes` |
| SD-K-CT-N2 | Capability outcomes in tree | Capability Map |

---

## Capability Map

**Purpose:** Outcome-oriented abilities by domain. **Audience:** Product, enterprise architecture. **Forbidden when:** Modules or containers (engineering types).

**Nodes:** `capability`, `capability-group`. **Edges:** `requires`, `contains` (optional), `enables` (optional).

**Abstraction:** ≤2 levels. **Density:** nodes ≤20, edges ≤28.

**Layout / tokens:** [layouts.md](layouts.md#diagram-type--layout-id) row **Capability Map** (`swimlane` when parallel domains with cross-links); [tokens.md](tokens.md#semantic-bindings).

**Caption:** `Capability Map — {scope} — spec v1`. Legend if ≥4 domain hues or both `requires` and `enables`.

**SD-K-CM-001** MUST use only capability node roles. **SD-K-CM-002** MUST NOT use module/container/process roles. **SD-K-CM-003** Technology as capability only with caption note. **SD-K-CM-004** Document any `requires` cycles in caption.

| ID | MUST NOT | Fix |
|----|----------|-----|
| SD-K-CM-N1 | Microservices as capabilities | C4 L2; keep capabilities tech-agnostic |
| SD-K-CM-N2 | Curriculum order between capabilities | Learning Path |

---

## Learning Path

**Purpose:** Ordered learning units. **Audience:** L&D, tech leads. **Forbidden when:** Runtime data flow (Data Flow) or concept taxonomy (Concept Tree).

**Nodes:** `learning-unit`, `milestone` (optional). **Edges:** `precedes`, `optional-branch` (optional).

**Abstraction:** 1 primary path; ≤2 branches, 1 decision depth. **Density:** nodes ≤12, edges ≤14.

**Layout / tokens:** [layouts.md](layouts.md#diagram-type--layout-id) row **Learning Path**; [tokens.md](tokens.md#semantic-bindings).

**Caption:** `Learning Path — {topic} — spec v1`. Legend if `optional-branch` used.

**SD-K-LP-001** MUST use only learning node roles. **SD-K-LP-002** `precedes` via `edge-sync`; not `edge-data`. **SD-K-LP-003** MUST NOT use `depends-on`, `uses`, `reads-writes`. **SD-K-LP-004** MUST NOT mix engineering roles.

| ID | MUST NOT | Fix |
|----|----------|-----|
| SD-K-LP-N1 | API calls between lessons | Learning order only |
| SD-K-LP-N2 | Full concept hierarchy in path | Concept Tree + Learning Path |

---

## Domain Model

**Purpose:** DDD structure (aggregates, entities, links). **Audience:** Domain experts, developers. **Forbidden when:** Deployable containers or modules (engineering).

**Nodes:** `aggregate`, `entity`, `value-object` (optional), `bounded-context` (frame). **Edges:** `associates`, `aggregates`, `references`, `inherits` (optional).

**Abstraction:** ≤2 levels. **Density:** nodes ≤20, edges ≤30.

**Layout / tokens:** [layouts.md](layouts.md#diagram-type--layout-id) row **Domain Model**; [tokens.md](tokens.md#semantic-bindings).

**Caption:** `Domain Model — {bounded context} — spec v1`. Legend if cross-context `references` or ≥4 entity hues.

**SD-K-DM-001** MUST use only domain node roles above. **SD-K-DM-002** MUST NOT label Container/Service/API/Database on domain nodes. **SD-K-DM-003** MUST NOT use C4 `uses` on entities. **SD-K-DM-004** Cross-context `references` visible and in caption.

| ID | MUST NOT | Fix |
|----|----------|-----|
| SD-K-DM-N1 | Microservices as aggregates | Domain language + C4 L2 for services |
| SD-K-DM-N2 | Curriculum order on entities | Learning Path |

---

## Type index

| Type | Prefix | L1 |
|------|--------|-----|
| Concept Tree | SD-K-CT | [checklists.md#l1-concept-tree](checklists.md#l1-concept-tree) |
| Capability Map | SD-K-CM | [checklists.md#l1-capability-map](checklists.md#l1-capability-map) |
| Learning Path | SD-K-LP | [checklists.md#l1-learning-path](checklists.md#l1-learning-path) |
| Domain Model | SD-K-DM | [checklists.md#l1-domain-model](checklists.md#l1-domain-model) |
