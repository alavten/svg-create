# Design Tokens

Single source for SVG attribute values. Map to `fill`, `stroke`, `stop-color`, `font-*`, `rx`/`ry`, coordinates.

**Palette:** assign `hue-a` … `hue-f` by **semantic role**, not decoration. Same slot → same meaning in one file. ≤6 hues per file; legend if ≥4 slots used. Structural types: [knowledge-diagrams.md](knowledge-diagrams.md), [engineering-diagrams.md](engineering-diagrams.md).

## Semantic bindings

Map **node roles** and **edge roles** (from type specs) to visual classes below. Do not invent new stroke colors.

### Node roles → palette / shape

| Node role | Diagram types | Visual binding |
|-----------|---------------|----------------|
| `concept`, `concept-root` | Concept Tree | `hue-*` or `neutral` |
| `capability` | Capability Map | `hue-*` by domain |
| `capability-group` | Capability Map | `bg-group` frame |
| `learning-unit` | Learning Path | `hue-*` or `neutral` |
| `milestone` | Learning Path | `hue-e` or `neutral` |
| `aggregate`, `entity` | Domain Model | `hue-*`; aggregate may use `hue-a` accent |
| `value-object` | Domain Model | `neutral` |
| `bounded-context` | Domain Model | `bg-group` dashed |
| `module` | Module Dependency | `hue-*` or `neutral` |
| `module-group` | Module Dependency | `bg-group` |
| `process` | Data Flow | `hue-*` |
| `data-store` | Data Flow | `hue-d` or `neutral` |
| `external-actor` | Data Flow | `neutral`, dashed frame |
| `container` | C4 L2 | `hue-*` |
| `external-system`, `person` | C4 L2 | `neutral` |
| `software-system-boundary` | C4 L2 | `bg-group` solid frame |

### Edge roles → edge class

| Edge role | Edge class | Arrow |
|-----------|------------|-------|
| `is-a`, `contains`, `associates`, `uses` | `edge-default` or `edge-sync` | yes (unless noted) |
| `part-of`, `aggregates`, `depends-on`, `imports`, `requires` | `edge-dependency` | no |
| `precedes`, `enables`, `inherits` | `edge-sync` | yes |
| `optional-branch`, `references`, `triggers` | `edge-async` | yes |
| `flows-to`, `reads-writes` | `edge-data` | yes |

### Forbidden mappings (MUST NOT)

| Edge role | MUST NOT use |
|-----------|----------------|
| `precedes` (Learning Path) | `edge-data`, `edge-dependency` |
| `depends-on` (Module) | `edge-sync` as primary style |
| `requires` (Capability) | `edge-data` |
| `is-a` (Concept Tree) | `edge-data` |
| `uses` (C4) | `edge-dependency` |
| Pedagogical order | `flows-to` |

Violations: fix stroke class per table; see [checklists.md](checklists.md) L1.

## Radius

| Token | `rx` / `ry` |
|-------|-------------|
| sm | 8 |
| md | 12 |
| lg | 16 |
| xl | 20 |
| xxl | 24 |
| **node** | **18** |
| legend swatch | 2 |

**Left accent bar:** when a 3–4px vertical accent sits on the left, that edge and the panel body meeting it must be **square** (`rx=0` on accent; no left-side rounding on the fill). Round **only the right** corners of the body (use `<path>` or split shapes — a full `<rect rx="…">` rounds all four corners).

## Spacing (user units)

| Token | Value |
|-------|-------|
| xs | 4 |
| sm | 8 |
| md | 12 |
| lg | 16 |
| xl | 24 |
| xxl | 32 |
| xxxl | 48 |

Between major nodes: **≥ 24**.

## Typography

`font-family`: system-ui, sans-serif, "PingFang SC", "Microsoft YaHei", sans-serif.

| Role | `font-size` | `fill` | `font-weight` | Use for |
|------|-------------|--------|---------------|---------|
| Title | 16–18 | `rgba(255,255,255,0.92)` | 600 | Diagram title |
| Section | 14 | `rgba(255,255,255,0.92)` | 600 | Row / group title |
| Label | 12–13 | `rgba(255,255,255,0.92)` | 500–600 | Primary node text |
| Sub label | 10–12 | `rgba(255,255,255,0.78)` | 400–500 | Secondary line in node (required reading) |
| Body secondary | 12 | `rgba(255,255,255,0.72)` | 400 | In-layer supporting lines |
| Axis | 10–11 | `rgba(255,255,255,0.65)` | 500 | Side rails, rotated section markers |
| Muted | 10–11 | `rgba(255,255,255,0.52)` | 400 | Parentheticals, optional hints only |

### On tinted node fills (`node-hue-*`)

Sub label inside colored rects: use **`0.78–0.85`** (not Muted). Prefer `0.82` when fill opacity ≥10%.

### Readability rules

- Text **&lt;11px**: opacity **≥ 0.55**; never use 0.38.
- **Axis / side labels**: never Muted tier; min **0.62**, prefer **0.65**.
- Aim for clear read at **100%** and acceptable at **50%** scale (no contrast check tool required; follow table above).

Divider: `stroke="rgba(255,255,255,0.08)"` `stroke-width="1"`.

## Canvas

| Token | Fill | Stroke |
|-------|------|--------|
| `bg-base` | `#0A0A0B` | — |
| `bg-canvas` | `#0E0E10` | `rgba(255,255,255,0.06)` |
| `bg-panel` | `#121214` | `rgba(255,255,255,0.08)` |
| `bg-elevated` | `#161618` / `#1C1C1F` | — |
| `bg-lane` | hue tint **6–8%** | hue **~22%**, 1px |
| `bg-group` | none | `rgba(255,255,255,0.10)` dashed |

```xml
<linearGradient id="canvasGrad" x1="0" y1="0" x2="0" y2="1">
  <stop offset="0%" stop-color="#111113"/>
  <stop offset="100%" stop-color="#0A0A0B"/>
</linearGradient>
```

## Palette slots (nodes)

Optional **4px left accent bar** using Accent hex. Node fill ~8–14% opacity; stroke ~35–55%.

| Slot | Fill | Stroke | Accent |
|------|------|--------|--------|
| `neutral` | `rgba(255,255,255,0.05)` | `rgba(255,255,255,0.14)` | — |
| `hue-a` | `rgba(79,140,255,0.12)` | `rgba(79,140,255,0.45)` | `#4F8CFF` |
| `hue-b` | `rgba(52,211,153,0.11)` | `rgba(52,211,153,0.42)` | `#34D399` |
| `hue-c` | `rgba(45,212,191,0.10)` | `rgba(45,212,191,0.40)` | `#2DD4BF` |
| `hue-d` | `rgba(167,139,250,0.11)` | `rgba(167,139,250,0.42)` | `#A78BFA` |
| `hue-e` | `rgba(251,191,36,0.10)` | `rgba(251,191,36,0.40)` | `#FBBF24` |
| `hue-f` | `rgba(34,211,238,0.10)` | `rgba(34,211,238,0.40)` | `#22D3EE` |

Lane backgrounds (optional): use matching hue at 7% fill, 22% stroke.

## Edge types

| Type | Stroke | Width | Style | Arrow |
|------|--------|-------|-------|-------|
| `default` | `rgba(255,255,255,0.20)` | 1.5 | solid | yes on directed down/forward |
| `sync` | `rgba(79,140,255,0.55)` | 1.5 | solid | yes |
| `async` | `rgba(167,139,250,0.50)` | 1.5 | `stroke-dasharray="6 4"` | yes |
| `data` | `rgba(251,191,36,0.55)` | 1.5 | solid | yes |
| `dependency` | `rgba(148,163,184,0.40)` | 1.2 | `stroke-dasharray="4 4"` | no |
| `critical` | `#4F8CFF` | 2 | solid; ≤1 glow | yes |
| `failure` | `rgba(251,113,133,0.50)` | 1.5 | dashed | optional |

≤3 non-default edge colors per diagram.

## Shadows

Prefer flat fills. Optional:

```xml
<feDropShadow dx="0" dy="2" stdDeviation="3" flood-color="#000" flood-opacity="0.25"/>
<filter id="accentGlow">
  <feDropShadow stdDeviation="3" flood-color="#4F8CFF" flood-opacity="0.35"/>
</filter>
```

## Legend

When ≥4 slots used — corner box `#161618`, swatch 8×8, label 10–11px; list slots present only.

## Palette budget

| Nodes | Max hues | Max edge types (+ default) |
|-------|----------|----------------------------|
| ≤8 | 4 | 2 |
| 9–20 | 5 | 3 |
| >20 | 6 | 3 |

## defs template

```xml
<defs>
  <style type="text/css"><![CDATA[
    .font { font-family: system-ui, sans-serif; }
    .node-hue-a { fill: rgba(79,140,255,0.12); stroke: rgba(79,140,255,0.45); }
    .node-hue-b { fill: rgba(52,211,153,0.11); stroke: rgba(52,211,153,0.42); }
    .edge-sync { fill: none; stroke: rgba(79,140,255,0.55); stroke-width: 1.5; }
    .edge-default { fill: none; stroke: rgba(255,255,255,0.20); stroke-width: 1.5; }
  ]]></style>
</defs>
```
