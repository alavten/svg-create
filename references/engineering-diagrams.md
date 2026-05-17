# Engineering Diagrams

Three engineering-family types. Cross-type rules: [structural-spec.md](structural-spec.md). Layout matrix: [layouts.md](layouts.md#diagram-type--layout-id). Visual bindings: [tokens.md](tokens.md#semantic-bindings). Checklists: [checklists.md](checklists.md#l1--per-diagram-type).

---

## Module Dependency

**Purpose:** Package/module depends-on graph. **Audience:** Developers. **Forbidden when:** All boxes are deployable containers (C4 L2) or capabilities (Capability Map).

**Nodes:** `module`, `module-group` (optional). **Edges:** `depends-on`, `imports` (pick one label per file).

**Abstraction:** ≤2 levels; container name as `nested-groups` frame if needed. **Density:** nodes ≤20, edges ≤35.

**Layout / tokens:** [layouts.md](layouts.md#diagram-type--layout-id) row **Module Dependency**; [tokens.md](tokens.md#semantic-bindings).

**Caption:** `Module Dependency — {scope} — spec v1`.

**SD-E-MD-001** MUST use only module node roles. **SD-E-MD-002** `depends-on` / `imports` with `edge-dependency`. **SD-E-MD-003** MUST NOT use knowledge node roles. **SD-E-MD-004** Deployable units → C4 L2, not modules.

| ID | MUST NOT | Fix |
|----|----------|-----|
| SD-E-MD-N1 | Microservices as modules only | C4 L2 |
| SD-E-MD-N2 | Payload labels on dependency edges | Data Flow |

---

## Data Flow

**Purpose:** Logical data movement. **Audience:** Developers, integration. **Forbidden when:** Container-only links without data semantics (C4 L2) or curriculum order (Learning Path).

**Nodes:** `process`, `data-store`, `external-actor` (optional). **Edges:** `flows-to`, `reads-writes`, `triggers` (optional).

**Abstraction:** ≤2 levels; no packet/protocol detail. **Density:** nodes ≤18, edges ≤28.

**Layout / tokens:** [layouts.md](layouts.md#diagram-type--layout-id) row **Data Flow**; [tokens.md](tokens.md#semantic-bindings). Cross-lane: see [layouts.md](layouts.md) swimlane connector notes.

**Caption:** `Data Flow — {scope} — spec v1`. Legend if all three edge roles appear.

**SD-E-DF-001** MUST use only data-flow node roles. **SD-E-DF-002** `flows-to` / `reads-writes` use `edge-data`. **SD-E-DF-003** MUST NOT use `precedes`. **SD-E-DF-004** MUST NOT show network/deployment detail.

| ID | MUST NOT | Fix |
|----|----------|-----|
| SD-E-DF-N1 | Service→Service without data label | Label data or use C4 L2 `uses` |
| SD-E-DF-N2 | Full module graph | Module Dependency + Data Flow |

---

## C4 Level 2 Container

**Purpose:** Containers in one **software system**. **Audience:** Architects. **Forbidden when:** Sub-module graph only (Module Dependency) or domain aggregates (Domain Model).

**Nodes:** `container`, `external-system`, `person` (optional), `software-system-boundary` (frame). **Edges:** `uses`; `reads-writes` sparingly.

**Abstraction:** 2 levels (boundary + containers); no L3 components. **Density:** nodes ≤15, edges ≤25.

**Layout / tokens:** [layouts.md](layouts.md#diagram-type--layout-id) row **C4 L2 Container**; [tokens.md](tokens.md#semantic-bindings).

**Caption:** `C4 L2 Container — {system name} — spec v1`.

**SD-E-C4-001** MUST include `software-system-boundary`. **SD-E-C4-002** MUST use only C4 L2 node roles. **SD-E-C4-003** MUST NOT show modules as top-level containers. **SD-E-C4-004** MUST NOT use domain entity/aggregate roles. **SD-E-C4-005** Container-level links only; no field/API lists on canvas.

| ID | MUST NOT | Fix |
|----|----------|-----|
| SD-E-C4-N1 | Domain aggregate as container | Domain Model + named service container |
| SD-E-C4-N2 | JSON on every link | Data Flow or API spec |

---

## Module Dependency vs C4 L2

| Question | Yes → | No → |
|----------|-------|------|
| Every box deployable? | C4 L2 | Module Dependency |
| Inside one container's code? | Module Dependency | C4 L2 |
| Maven/npm imports? | Module Dependency | C4 L2 |
| Service "uses" links? | C4 L2 | Module Dependency |

**SD-E-OV-001** MUST NOT mix both semantics on one canvas. **SD-E-OV-002** Use two SVGs + cross-reference in captions.

---

## Type index

| Type | Prefix | L1 |
|------|--------|-----|
| Module Dependency | SD-E-MD | [checklists.md#l1-module-dependency](checklists.md#l1-module-dependency) |
| Data Flow | SD-E-DF | [checklists.md#l1-data-flow](checklists.md#l1-data-flow) |
| C4 L2 Container | SD-E-C4 | [checklists.md#l1-c4-l2-container](checklists.md#l1-c4-l2-container) |
