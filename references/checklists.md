# Structural Diagram Checklists

**L0 markup:** complete [quality.md § L0](quality.md#l0--markup--export) (single source — do not duplicate here).

**Review target:** L2 in ≤15 minutes per file.

---

## L0 — Structural additions

After [quality.md § L0](quality.md#l0--markup--export):

- [ ] **L0-S-01** Caption in delivery: diagram type (or `generic`), scope, `spec v1`
- [ ] **L0-S-02** Labels use terms from [structural-spec.md § Glossary](structural-spec.md#glossary)

---

## L1 — Per diagram type

Run the appendix for the declared type after modeling, before final L0 pass.

### L1 Concept Tree {#l1-concept-tree}

- [ ] **L1-CT-01** Only `concept` / `concept-root` nodes
- [ ] **L1-CT-02** Only `is-a` / `part-of` edges
- [ ] **L1-CT-03** No `precedes`, `depends-on`, `uses`, `flows-to`
- [ ] **L1-CT-04** Layout per [layouts.md](layouts.md#diagram-type--layout-id) row Concept Tree
- [ ] **L1-CT-05** Abstraction span ≤2 levels
- [ ] **L1-CT-06** Node count ≤18; edges ≤24
- [ ] **L1-CT-07** No deployable service/module names as concepts
- [ ] **L1-CT-08** SD-K-CT-N1/N2 avoided

### L1 Capability Map {#l1-capability-map}

- [ ] **L1-CM-01** Only `capability` / `capability-group` nodes
- [ ] **L1-CM-02** Only `requires` / `contains` / `enables` edges
- [ ] **L1-CM-03** No module or container node roles
- [ ] **L1-CM-04** Layout per layouts row Capability Map
- [ ] **L1-CM-05** Abstraction span ≤2 levels
- [ ] **L1-CM-06** Node count ≤20; edges ≤28
- [ ] **L1-CM-07** Technology names justified in caption if used
- [ ] **L1-CM-08** SD-K-CM-N1/N2 avoided

### L1 Learning Path {#l1-learning-path}

- [ ] **L1-LP-01** Only `learning-unit` / `milestone` nodes
- [ ] **L1-LP-02** Only `precedes` / `optional-branch` edges
- [ ] **L1-LP-03** `precedes` uses `edge-sync`; not `edge-data`
- [ ] **L1-LP-04** Layout per layouts row Learning Path
- [ ] **L1-LP-05** Single primary path; branches ≤2
- [ ] **L1-LP-06** Node count ≤12; edges ≤14
- [ ] **L1-LP-07** No engineering node roles
- [ ] **L1-LP-08** SD-K-LP-N1/N2 avoided

### L1 Domain Model {#l1-domain-model}

- [ ] **L1-DM-01** Only domain node roles from spec
- [ ] **L1-DM-02** Only `associates` / `aggregates` / `references` / `inherits` edges
- [ ] **L1-DM-03** No Container/Service/API/Database on domain nodes
- [ ] **L1-DM-04** Layout per layouts row Domain Model
- [ ] **L1-DM-05** Abstraction span ≤2 levels
- [ ] **L1-DM-06** Node count ≤20; edges ≤30
- [ ] **L1-DM-07** Cross-context `references` in caption
- [ ] **L1-DM-08** SD-K-DM-N1/N2 avoided

### L1 Module Dependency {#l1-module-dependency}

- [ ] **L1-MD-01** Only `module` / `module-group` nodes
- [ ] **L1-MD-02** Only `depends-on` / `imports` with `edge-dependency`
- [ ] **L1-MD-03** Not used when all boxes are deployable containers
- [ ] **L1-MD-04** Layout per layouts row Module Dependency
- [ ] **L1-MD-05** Node count ≤20; edges ≤35
- [ ] **L1-MD-06** No capability or concept nodes
- [ ] **L1-MD-07** SD-E-MD-N1/N2 avoided
- [ ] **L1-MD-08** Separate file from C4 if both needed (SD-E-OV-002)

### L1 Data Flow {#l1-data-flow}

- [ ] **L1-DF-01** Only `process` / `data-store` / `external-actor` nodes
- [ ] **L1-DF-02** `flows-to` / `reads-writes` use `edge-data`
- [ ] **L1-DF-03** No `precedes` edges
- [ ] **L1-DF-04** Layout per layouts row Data Flow
- [ ] **L1-DF-05** Node count ≤18; edges ≤28
- [ ] **L1-DF-06** Data labels on flows or caption explains data
- [ ] **L1-DF-07** No network/deployment detail
- [ ] **L1-DF-08** SD-E-DF-N1/N2 avoided

### L1 C4 L2 Container {#l1-c4-l2-container}

- [ ] **L1-C4-01** `software-system-boundary` frame present
- [ ] **L1-C4-02** Only C4 L2 node roles
- [ ] **L1-C4-03** Only `uses` / high-level `reads-writes`
- [ ] **L1-C4-04** Layout per layouts row C4 L2 Container
- [ ] **L1-C4-05** Node count ≤15; edges ≤25
- [ ] **L1-C4-06** No domain aggregates as containers
- [ ] **L1-C4-07** No modules as top-level containers
- [ ] **L1-C4-08** SD-E-C4-N1/N2 avoided

---

## L2 — Pre-publish review

Assumes L1 + quality L0 passed.

- [ ] **L2-01** Type classified; not mixed knowledge/engineering canvas
- [ ] **L2-02** Scope matches title and caption
- [ ] **L2-03** Roles match closed enums in type spec
- [ ] **L2-04** Abstraction span within limit
- [ ] **L2-05** Split if density exceeded
- [ ] **L2-06** Bundle names consistent ([structural-spec.md](structural-spec.md#multi-diagram-bundles))
- [ ] **L2-07** No SD-S-010–SD-S-019 violations
- [ ] **L2-08** Legend matches hues and edge classes used
- [ ] **L2-09** Rule exceptions documented with IDs
- [ ] **L2-10** Layout matches [layouts.md](layouts.md#diagram-type--layout-id)
- [ ] **L2-11** One-sentence decision support for stakeholder
- [ ] **L2-12** Not duplicating another type in the doc set

---

## Multi-diagram bundle order

L1 + L2 per file, in order: Domain Model / Capability Map → C4 L2 → Module Dependency → Data Flow.
