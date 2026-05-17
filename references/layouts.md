# Layout Patterns

Geometric arrangements for SVG diagrams. Values: [tokens](tokens.md). Markup rules: [quality](quality.md). Structural types: [structural-spec.md](structural-spec.md).

## Diagram-type selection

### Decision tree

```text
Structural diagram?
├─ No  → use "Graph shape" matrix below (generic)
└─ Yes → pick diagram type
    ├─ Concept Tree        → layered-stack (alt: nested-groups)
    ├─ Capability Map      → layered-stack (alt: swimlane, nested-groups)
    ├─ Learning Path       → horizontal-pipeline (alt: layered-stack phases)
    ├─ Domain Model        → nested-groups (alt: hub-spoke)
    ├─ Module Dependency   → nested-groups (alt: hub-spoke)
    ├─ Data Flow           → swimlane (alt: horizontal-pipeline)
    └─ C4 L2 Container     → nested-groups (alt: layered-stack)
```

### Diagram type → Layout ID {#diagram-type--layout-id}

| Diagram type | Primary | Alternates | Avoid |
|--------------|---------|------------|-------|
| Concept Tree | `layered-stack` | `nested-groups` | `horizontal-pipeline` |
| Capability Map | `layered-stack` | `swimlane`, `nested-groups` | `hub-spoke` |
| Learning Path | `horizontal-pipeline` | `layered-stack` (phases) | `hub-spoke` |
| Domain Model | `nested-groups` | `hub-spoke` | `layered-stack` (except context tiers) |
| Module Dependency | `nested-groups` | `hub-spoke` | `horizontal-pipeline` |
| Data Flow | `swimlane` | `horizontal-pipeline` | `hub-spoke` |
| C4 L2 Container | `nested-groups` | `layered-stack` | deployment/network detail |

One layout idiom per file. Type-aware mixing: [structural-spec.md](structural-spec.md#layout-and-density).

## Selection matrix (generic / graph shape)

| Graph shape | Layout ID | Typical node count |
|-------------|-----------|-------------------|
| Several rows stacked vertically | `layered-stack` | Medium |
| Single left-to-right chain | `horizontal-pipeline` | Small–medium |
| Parallel horizontal bands | `swimlane` | Medium–large |
| One center, many around | `hub-spoke` | Medium |
| Boxes inside labeled frames | `nested-groups` | Small–medium |

If unclear, ask once: vertical tiers vs horizontal chain vs lanes.

---

## layered-stack

**Sketch**

```text
[A] [B] [C]     ← top row
 \   |   /
  `--+--'       ← bus
     |
 [ wide row ]
     |
 [ band ]
 - - - - - -
 [ → → → → ]   ← inner sequence
```

**Use when:** Multiple tiers collapse into one lower block; top row fans into a bus.

**Avoid when:** Simple A→B→C only (use `horizontal-pipeline`).

**`<g id>`**

- `row-{n}` or `layer-{n}` — `transform="translate(x,y)"`
- `connectors-bus` — shared horizontal segment
- `row-{n}-cells` — chips inside a wide row
- `legend` — if ≥4 palette slots

**viewBox**

- Scale to content; margin 24–40; panel inset optional ~20px

**Nodes**

- Top: 2–4 columns, gap ≥ 24
- Wide row: equal-width cells ~115–120, gap ~10
- Sequence row: 4–8 cells, horizontal `edge-sync`

**Connectors**

- **Upper row → bus:** one vertical per top box to shared bus Y; `marker-end` on each drop
- **Bus:** single horizontal segment linking all column X at bus Y
- **Bus → next wide row (merge):** **one** vertical from bus (usually center X) into the row below; `marker-end` on that trunk — do **not** draw separate verticals from every column unless user asks for a fan-out
- Trunk may use `edge-critical` + optional glow; upper drops use `edge-default`
- **Next row → row below:** one vertical with `marker-end` (e.g. L4→L5)
- Section break: `edge-dependency` dashed (no arrow)
- In-row sequence: `edge-sync` with `marker-end` between cells

---

## horizontal-pipeline

**Sketch**

```text
[N1] --> [N2] --> [N3] --> [N4]
```

**Use when:** 3–8 steps in one direction.

**Avoid when:** Multiple vertical tiers or many cross-links.

**`<g id>`**

- `pipeline`; `node-{id}` per step; `connectors`

**viewBox**

- ~140–160 width per step; height ~200–280; margin 32

**Nodes**

- One row; equal cell size; gap ≥ 24

**Connectors**

- `edge-sync` between adjacent nodes
- Branch: optional `edge-data` below main line

---

## swimlane

**Sketch**

```text
Lane1 | [A] ----> [B]
Lane2 |      [C] ----> [D]
Lane3 | [E] ---------------->
```

**Use when:** ≥2 parallel rows with cross-row links.

**Avoid when:** Single row only.

**`<g id>`**

- `lane-{n}` — background `<rect>` + nodes
- `connectors`

**viewBox**

- Lane height ≥ 80–100; gap between lanes ≥ 16; margin 40

**Nodes**

- Stay inside lane rect; column-align across lanes
- Lane fill: `bg-lane` tints in [tokens](tokens.md)

**Connectors**

- Same lane: orthogonal `edge-sync`
- Cross lane: `edge-async` or `edge-default`; minimize crossings

---

## hub-spoke

**Sketch**

```text
      [S1]
[S4]--[C]--[S2]
      [S3]
```

**Use when:** One central node, 4–8 peripherals.

**Avoid when:** No hub or full mesh.

**`<g id>`**

- `hub-center`; `spoke-{id}`

**viewBox**

- Square or 4:3; hub at center; radius 180–240 to spokes

**Nodes**

- Center ~1.2× spoke size; spokes uniform

**Connectors**

- Hub–spoke: `edge-sync` (bezier or straight)
- Spoke–spoke: rare; use `edge-dependency` if needed

---

## nested-groups

**Sketch**

```text
+-- group-1 ----------------+
|  [a]  [b]  [c]            |
+---------------------------+
+-- group-2 ----------------+
|  [d]  [e]                 |
+---------------------------+
```

**Use when:** Nodes belong to named containers.

**Avoid when:** Flat list with no grouping.

**`<g id>`**

- `group-{id}` — frame + title
- `node-{id}` inside group

**viewBox**

- Stack groups vertically or 2-column; padding 16–20 inside frame

**Nodes**

- 2–5 per group; groups spaced ≥ 32

**Connectors**

- Inside group: `edge-default` or `edge-sync`
- Across groups: enter/exit at frame edge, not through title

---

## Shared rules

- Stable `id`s on groups and nodes (for `edit`)
- Snap positions to 4 or 8 px grid
- Legend if ≥4 palette slots ([tokens](tokens.md))
- One layout idiom per file unless user requests mix (structural: [structural-spec.md](structural-spec.md#layout-and-density))

### Connector notes by diagram type

| Diagram type | Layout | Note |
|--------------|--------|------|
| Data Flow | `swimlane` | Cross-lane: `edge-async` or `edge-default`; minimize crossings |
| C4 L2 Container | `nested-groups` | Externals outside `software-system-boundary` frame |
| Concept Tree | `layered-stack` | Child→parent links: bus merge optional for many children |
| Learning Path | `horizontal-pipeline` | Adjacent `learning-unit` nodes: `edge-sync` between cells |
