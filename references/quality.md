# SVG Quality (L0)

**L0 — Markup and export** rules for all svg-create output. Semantic rules: [checklists.md](checklists.md) L1/L2. Values: [tokens](tokens.md). Geometry: [layouts](layouts.md).

Structural diagrams: [structural-spec.md](structural-spec.md). Layout mixing: [structural-spec.md#layout-and-density](structural-spec.md#layout-and-density).

## Document

- Root: `<svg xmlns="http://www.w3.org/2000/svg" viewBox="min-x min-y width height">`
- UTF-8 encoding; `<?xml version="1.0" encoding="UTF-8"?>` required for non-ASCII text; write file as UTF-8 (do not corrupt multibyte labels)
- Explicit `viewBox` always; `width`/`height` optional for embed

## Nodes

- Primary shape: `<rect rx="18">` unless user needs other primitives
- Group: `<g id="node-{id}">`; optional 4px accent `<rect>` per [tokens](tokens.md)
- **Left accent:** accent bar square; body **flat left**, rounded right only — see [tokens](tokens.md) Radius
- Text: `<text>` with `fill` from [tokens](tokens.md) typography table; `text-anchor` as needed
- Secondary node line → **Sub label** tier; side / rail text → **Axis** tier; only de-emphasized hints → **Muted**
- Do not put readable structure labels at opacity 0.38 or on Muted tier
- Equal cell size within one row or group
- **Legend:** place in a footer band below the diagram bounds; never overlap lanes/nodes (extend `viewBox` height if needed)

```xml
<g id="node-a">
  <rect x="0" y="0" width="4" height="56" fill="#4F8CFF"/>
  <path class="node-hue-a" stroke-width="1"
    d="M 4 0 H 112 Q 120 0 120 12 V 44 Q 120 56 112 56 H 4 Z"/>
  <text class="font" x="62" y="32" text-anchor="middle"
    fill="rgba(255,255,255,0.92)" font-size="13">Label</text>
</g>
```

## Paths (edges)

- `<path fill="none" …>` or `<line>`; stroke from tokens edge table
- Routing: orthogonal polylines or cubic bezier (`C`/`S`)
- **Arrows:** `<marker id="arrow-…">` in `<defs>`; `marker-end="url(#arrow-…)"` on directed segments; `markerWidth` ≤8; fill matches stroke
- **Layered / stacked layouts:** upper columns → horizontal bus → **one** trunk into next band (`marker-end` on trunk); see [layouts](layouts.md) `layered-stack`
- **Z-order:** draw merge/trunk connectors **after** the target layer’s filled shape, or place the trunk **inside** that layer’s `<g>` (local coords from bus `y` to a few px inside the band); trunk must cross the layer top edge visibly
- `dependency` dashed dividers: no arrow
- Static output only—no SMIL/CSS animation unless requested
- Avoid: stroke-width >2 except one `critical` edge; sharp 90° without intent
- Avoid: multiple trunks from bus to next band when design is merge-to-one (three separate drops = wrong)
- Avoid: upper columns without vertical to bus (incomplete merge)

## Groups

- Layers: `<g id="row-1">` etc. per [layouts](layouts.md)
- Position with `transform="translate(x,y)"`; avoid redundant nesting
- Stable `id`s required for edit workflows

## Rendering

- No `foreignObject` (no HTML/CSS in SVG)
- Minimize `<filter>` count; no long `feGaussianBlur` chains
- No embedded raster `<image>` unless user supplies assets
- Avoid invalid or self-closing mistakes on non-void elements

## Anti-patterns (markup and visual)

**Markup**

- Missing `xmlns` or `viewBox`
- Duplicate `id`s
- Hard-coded pixel canvas with no `viewBox` scaling

**Visual (in SVG)**

- Overlapping text unreadable at 100%
- Sub label or axis text at opacity <0.55, or 9px text at ≤0.38
- Using Muted fill for chip subtitles, side rails, or lane annotations
- >6 distinct fill hues without legend
- Connector stroke unrelated to declared edge type
- Saturated fills (`#3B82F6` as node background)

**Layout (L0)**

- Major nodes closer than `spacing.xl` (24)

Mixed layout patterns: [structural-spec.md](structural-spec.md#layout-and-density).

## L0 — Markup & export

Quick pass before delivery; full list: [checklists.md](checklists.md#l0--universal-all-svg).

- [ ] Well-formed SVG; `viewBox` set; UTF-8 text intact
- [ ] Layout ID matches [layouts](layouts.md)
- [ ] Colors from [tokens](tokens.md); legend if ≥4 hues
- [ ] ≤1 `critical` glow; filters minimal
- [ ] Directed edges have `marker-end`; layered bus: columns → bus → **one** trunk (not per-column fans)
- [ ] Typography tiers correct (Sub label ≥0.78 on tinted nodes; Axis ≥0.65; Muted only for hints)
- [ ] Labels readable at 100% and ~50% scale
- [ ] `edit` mode: topology and `id`s preserved unless restructure requested
- [ ] No React/HTML output

For structural diagrams, also complete **L1** (type) and optionally **L2** (publish) in [checklists.md](checklists.md).
