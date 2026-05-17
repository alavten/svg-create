# svg-create

面向「生成、编辑、换肤独立 `.svg` 文件」的矢量图技能。由 Agent 按 `SKILL.md` 路由，并在各参考契约（`references/*.md`）下执行。支持 **六种结构型图**（知识 4 类 + 工程 3 类）与 **通用流程图 / 节点图**。

## 适用场景

适合说法例如：画架构图、概念树、能力地图、学习路径、领域模型、模块依赖、数据流、C4 容器图、流程图、节点图、改 SVG、换配色、导出可嵌入矢量图等。技能产出 **独立、可校验的 `.svg`**，而非 React/HTML 画布组件。

**在范围内：** 新建 / 编辑 / 换肤 `.svg`；六种结构型图；暗色极简风格。  
**不在范围内：** React/TSX、React Flow、HTML canvas、纯 CSS 图形、动效 Web UI。

## 你将经历的一次协作

- **结构型图**：先选定 **一种** 图类型（每文件一种，不混用知识/工程角色），再列节点与边角色、选布局 ID、套 token、绘制并通过检查清单。
- **通用图**：由你描述节点与关系，Agent 从 `layouts.md` 选布局，再套用 `tokens.md` 与 `quality.md`。
- **编辑 / 换色**：保留拓扑、`viewBox` 与 `id`；仅换色时只改 `fill`/`stroke`。
- **交付**：除文件路径外，应附带图类型、结构摘要、布局 ID、满足的 rule ID 与检查项（见 `SKILL.md` § Delivery format）。

## 七种产出怎么选

用你的说法对照目标类型（详细规则见对应 `references/*.md`）：

| 你想做的事 | 类型 | 契约文件 |
| ---------- | ---- | -------- |
| 概念分层、taxonomy | Concept Tree | `references/knowledge-diagrams.md` |
| 业务能力划分 | Capability Map | `references/knowledge-diagrams.md` |
| 课程 / 上手路径 | Learning Path | `references/knowledge-diagrams.md` |
| DDD 领域结构 | Domain Model | `references/knowledge-diagrams.md` |
| 模块依赖关系 | Module Dependency | `references/engineering-diagrams.md` |
| 逻辑数据流向 | Data Flow | `references/engineering-diagrams.md` |
| C4 二级容器视图 | C4 Level 2 Container | `references/engineering-diagrams.md` |
| 通用流程图、节点图 | generic | `layouts.md` + `tokens.md` + `quality.md` |
| 改图、换肤、保留结构 | edit | `SKILL.md` Guardrails + `quality.md` |

路由习惯：

1. 意图不清（要概念树还是能力图？）→ 先对照 `SKILL.md` 意图表或 `structural-spec.md` 选型。
2. 结构型图 → 严格一种类型 per file；跨类型需求请拆文件或说明「派生视图」。
3. 绘制前不擅自增加用户未暗示的节点/边；闭合枚举内的角色才可用。

## 标准工作流（结构型）

1. **选型** → [structural-spec.md](references/structural-spec.md#diagram-type-selection)
2. **建模** → [knowledge-diagrams.md](references/knowledge-diagrams.md) 或 [engineering-diagrams.md](references/engineering-diagrams.md)
3. **布局** → [layouts.md](references/layouts.md#diagram-type--layout-id)
4. **视觉 token** → [tokens.md](references/tokens.md#semantic-bindings)
5. **实现与校验** → [quality.md](references/quality.md)；[checklists.md](references/checklists.md) L1 → L0

七步 SOP 详见 [structural-spec.md § Seven-step SOP](references/structural-spec.md#seven-step-sop)。

## 各参考文件职责

| 文件 | 作用 |
| ---- | ---- |
| `structural-spec.md` | 选型、SOP、边界、术语 |
| `knowledge-diagrams.md` | 四种知识型图节点/边规范 |
| `engineering-diagrams.md` | 三种工程型图节点/边规范 |
| `layouts.md` | 布局 ID 与类型矩阵 |
| `tokens.md` | 颜色、线型等语义绑定 |
| `checklists.md` | L1/L2 语义检查；L0 见 quality |
| `quality.md` | L0 标记与导出规则 |

## SKILL 下载与使用说明

如果你只想拿到技能说明文件（`SKILL.md`）做阅读或二次集成，可用以下方式：

- 通过 skills CLI 直接安装到当前代理环境：

```bash
npx skills add alavten/svg-create
```

- 克隆完整仓库

```bash
git clone https://github.com/alavten/svg-create.git
```

## 进一步阅读

- 总路由与意图表：**`SKILL.md`**
- 结构型选型与全局规则：**`references/structural-spec.md`**
- 各图类型字段与约束：**`references/knowledge-diagrams.md`**、**`references/engineering-diagrams.md`**
