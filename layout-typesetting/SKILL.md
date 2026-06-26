---
name: layout-typesetting
description: "Frontend layout & typesetting design skill. Distilled from design terminology reference — covers layout basics, grid systems, layout patterns, responsive strategies, and CSS layout engineering. Use when building page layouts, designing responsive UIs, choosing layout patterns, setting up grids, or troubleshooting layout issues. Triggers: 'layout', 'typesetting', '排版', '布局', 'grid', '栅格', 'responsive layout', '响应式布局', 'flexbox', 'css grid', 'page structure', '页面结构', 'card grid', 'dashboard layout', 'master-detail', 'sidebar layout'."
---

# Layout & Typesetting Design — Frontend Layout Engineering

Comprehensive reference for designing and implementing page layouts. Covers design terminology, grid systems, layout patterns, responsive strategy, and CSS engineering — all aligned so AI agents produce structurally sound, visually coherent layouts.

---

## 1. Layout Basics & Spatial Relationships

### Layout (布局)
Decides WHERE interface elements sit on the page: navigation, body, sidebar, buttons, footer. Every element needs a stable position.

### Composition (构图)
Controls how elements relate VISUALLY after placement: where the eye lands first, which area carries weight, what recedes. Layout = structure. Composition = visual balance.

### Visual Hierarchy (视觉层级)
Use size, weight, color contrast, and whitespace to create clear priority levels:
- Titles > prices > buttons > captions — never make everything equally heavy.
- **CSS implication**: `font-size`, `font-weight`, `color`, `opacity`, `margin` all contribute to hierarchy.

### Reading Flow (阅读路径)
The path eyes follow across the page. Z-pattern (hero pages) and F-pattern (text-heavy pages) are common, but actual flow depends on content and task.

### Alignment (对齐)
Invisible axes that keep scattered elements stable:
- Left-align text blocks, center-align CTAs sparingly.
- Card edges, button groups, form fields should align to a shared reference line.
- Misaligned elements make pages feel "wobbly."

### Proximity (邻近)
Distance EXPRESSES relationships:
- Elements close together → perceived as one group.
- More distance → perceived as separate modules.
- Use spacing to signal grouping, not just `<hr>` dividers.

### Grouping (分组)
Achieved through spacing control, not necessarily borders or dividers. Form sections, settings groups, list items — adjust margin/gap to clarify groups.

### Whitespace (留白)
Space NOT occupied by content: padding, margin, gaps between sections.
- **Too little** → page feels cramped, users can't parse grouping.
- **Too much** → related info gets pulled apart.
- **CSS**: `padding`, `margin`, `gap` (flex/grid), `row-gap`, `column-gap`.

---

## 2. Grid Systems (栅格系统)

### Grid (栅格)
A reference line system of rows, columns, gutters, and margins. Grids are invisible but structure all content alignment.
- **12-column grid** is the web standard (divisible by 2, 3, 4, 6).
- **CSS**: `grid-template-columns: repeat(12, 1fr)`.

### Container (页面容器)
Outer wrapper holding main content. Typically has `max-width` + centered via `margin: 0 auto`.
- Without `max-width`, body text stretches too wide on large screens.
- Common widths: `1200px`, `1280px`, `1440px`.

### Margin (页面外边距)
Space from container edge to browser edge. Prevents content from touching screen edges on mobile.

### Row (行)
Horizontal layout band. One row might hold 3 metric cards; the next row holds a chart.

### Column / Col (栏)
Vertical division baseline. Content can span one or multiple columns.
- Too narrow → cards feel cramped.
- Too wide → lists and body text feel loose.

### Gutter (槽距)
Space BETWEEN adjacent columns or rows. Separates content, prevents visual merging.
- Common values: `16px`, `20px`, `24px`, `32px`.
- **CSS**: `gap` property in flex/grid, or explicit margin.

### Module (模块)
An actual content block placed on the grid. A product card, stat card, or chart area is a module. One module can span multiple columns.

### Baseline Grid (基线网格)
Vertical rhythm reference lines (like ruled notebook paper). Keeps line-height, paragraph spacing, and component heights on the same rhythm.
- **CSS**: `line-height` + consistent spacing multiples (e.g., all spacing in multiples of `4px` or `8px`).

### Modular Grid (模块化栅格)
Adds ROW constraints on top of column grid, forming a matrix. Used for dashboards, card matrices, magazine-style pages needing repeated comparison.

> **Distinction**: Modular Grid is a DESIGN reference (visual rhythm + alignment). CSS Grid is the ENGINEERING implementation (which rows/columns/areas elements occupy).

---

## 3. Page Layout Patterns

### Single-column (单栏)
Content in one centered narrow column. Ideal for articles, docs, reading-heavy pages.

### Sidebar (侧边栏)
Navigation/filters on one side, main content on the other. Common in admin panels, docs, settings pages.
- **CSS tip**: `grid-template-columns: 250px 1fr` or flexbox with fixed sidebar width.

### Split (分栏)
Screen divided into two main zones. Login pages (brand image + form), comparison views (left vs right).

### Multi-column (多栏)
Multiple horizontal columns for peer content. Index pages, resource lists, category entries — let users scan more items quickly.

### Card Grid (卡片网格)
Independent cards in a matrix. Products, video thumbnails, template lists. Cards have clear boundaries for easy scanning and comparison.
- **CSS**: `grid-template-columns: repeat(auto-fill, minmax(280px, 1fr))`.

### Masonry (瀑布流)
Fixed column width, variable heights, staggered vertical flow. Good for image galleries and UGC where each item has different height.
- **NOT** for: lists needing strict comparison of price/status/metrics.
- **CSS**: `columns` property or JS-assisted layout. Native `grid` with `masonry` is experimental.

### Dashboard (仪表盘)
Charts, metric cards, lists, and filters on one screen. Multiple dimensions at a glance.
- **Key challenge**: Curation — the most important metric must be seen FIRST, even on a dense screen.

### Master-detail (主从布局)
List on one side, detail on the other. Email clients, settings pages, admin panels. Best for frequent item-switching workflows.
- **CSS**: `grid-template-columns: 300px 1fr` or flexbox with scrollable list panel.

---

## 4. Responsive Layout Strategy

### Breakpoint (断点)
Width position where layout rules change. Typically based on viewport width.
- **Golden rule**: Breakpoints should match CONTENT failure points, not device sizes. "When does this layout break?" → that's the breakpoint.
- Common ranges: `640px`, `768px`, `1024px`, `1280px`.

### Responsive Design (响应式布局)
Layout continuously adjusts as available space changes. Elements compress, wrap, then breakpoints switch structure. Ideally, the page tightens step by step — never breaks suddenly.

### Adaptive Design (适配式布局)
Pre-prepared fixed layouts for specific widths. Cross a breakpoint → switch to another design. More like "several fixed schemes" than continuous flow.

| Approach | Behavior | Best for |
|----------|----------|----------|
| Responsive | Fluid, continuous adjustment | Content-driven sites |
| Adaptive | Snaps between fixed layouts | Complex apps with distinct mobile/desktop UX |

### Fixed (固定)
Explicit dimensions: `width: 300px`. OK for icons, avatars, fixed-width buttons.
- **Danger**: Long text, tables, narrow screens — fixed sizes easily overflow.

### Fluid (流体)
Elements follow parent: `width: 100%`, `flex: 1`. Fills available space.
- **Required guardrails**: `max-width` (prevents stretched body text) and `min-width` (prevents crushed cards).

### Intrinsic (内在布局)
Content-DRIVEN sizing: `max-content`, `min-content`, `fit-content`.
- Labels, buttons, menu items with variable text length.
- Short content doesn't take too much space; long content has boundaries.

### Viewport (视口)
The browser's visible area. Basis for breakpoints, `vw`/`vh` units, and above-the-fold content.
- Mobile: collapse sidebar. Desktop: expand multi-column.

### Container Query (容器查询)
Component responds to its OWN container size, not the viewport. Same card might appear in a wide main column OR a narrow sidebar — Container Query lets it adapt locally.
- **CSS**: `@container` + `container-type: inline-size`.

### Safe Area (安全区域)
Mobile edge area safe for content placement. Notches, rounded corners, gesture bars consume edge space.
- Fixed bottom bars, back buttons, full-screen images must avoid these areas.
- **CSS**: `env(safe-area-inset-top)`, `env(safe-area-inset-bottom)`, etc.

---

## 5. CSS Layout Engineering

### Normal Flow (文档流)
Browser's DEFAULT layout. No `position`, `float`, `flex`, or `grid` applied → elements flow in HTML order.
- Block elements: top to bottom.
- Inline content: left to right, auto-wraps when space runs out.
- **Always understand normal flow FIRST** before reaching for positioning hacks.

### Box Model (盒模型)
How an element occupies space: `content` → `padding` → `border` → `margin`.
- Debugging tip: check actual box size (content + padding + border), not just `width`/`height`.
- **CSS**: `box-sizing: border-box` makes `width` include padding + border (use this globally).

### Display (显示类型)
Defines how an element participates in layout:
- `block` — full width, new line.
- `inline` — flows with text, no width/height.
- `inline-block` — inline but accepts width/height.
- `flex` / `grid` — creates NEW layout context for children.

> `display` affects BOTH how the element itself lays out AND how its children are arranged.

### Flexbox (弹性布局)
**1D layout model** — handles arrangement, distribution, alignment on ONE axis:
- Main axis (row or column) for primary flow.
- Cross axis for perpendicular alignment.
- Perfect for: nav bars, button groups, toolbars, form rows, card internal layout.
- **NOT** for: full-page grids (use CSS Grid).

### CSS Grid (CSS 栅格)
**2D layout model** — simultaneous row AND column control:
- Define tracks: `grid-template-columns`, `grid-template-rows`.
- Place items: `grid-column`, `grid-row`, `grid-area`.
- Perfect for: page skeletons, card matrices, dashboards, form layouts.

### Positioning (定位)
- `static` — normal flow (default).
- `relative` — keeps space, offset from self.
- `absolute` — removed from flow, positioned relative to nearest positioned ancestor.
- `fixed` — relative to viewport. Floating buttons, fixed nav, bottom action bars.
- `sticky` — scrolls in flow until threshold, then sticks. Section headers, table headers.

> **Principle**: Positioning is for overlays and fixed zones. Don't use it to replace normal layout.

### Z-index (层级)
Controls visual stacking order of overlapping elements. Higher number = on top.
- Only meaningful WITHIN a stacking context.
- **Constraint**: Keep z-index values disciplined. Nav, overlay, modal, tooltip each get a fixed tier. Avoid random `z-index: 9999` patches.

### Stacking Context (层叠上下文)
A self-contained stacking environment. An element creates a stacking context, and its children stack internally first; then the whole context participates in external stacking.
- Common triggers: `position` + `z-index`, `opacity < 1`, `transform`, `filter`, `isolation`.
- **Debugging**: Child's `z-index` may be "capped" by parent's stacking context — this is the root cause of many z-index bugs.

### Overflow (溢出)
How to handle content exceeding box boundaries:
- `visible` — content spills out (default).
- `hidden` / `clip` — cut off.
- `auto` / `scroll` — provide scrollbars.
- **Decision tree**: Should content wrap? → Should container grow? → Or should it clip/scroll?

### Scroll Container (滚动容器)
Any element that accepts scrolling via `overflow`. Becomes the scroll boundary for its children.
- Affects: sticky elements, scroll shadows, internal lists, fixed headers, overlay positioning.
- Many scroll problems originate from INNER scroll containers, not the page itself.

---

## Quick Decision Cheatsheet

### Choosing a Layout Pattern
| Need | Use |
|------|-----|
| Reading-heavy (articles, docs) | Single-column |
| Navigation + content | Sidebar |
| Two parallel zones (login, comparison) | Split |
| Dense scanning (product list, gallery) | Card Grid or Multi-column |
| Variable-height content (images, UGC) | Masonry |
| Monitoring + comparison | Dashboard |
| List-inspect workflow (email, settings) | Master-detail |

### Choosing CSS Layout
| Need | Use |
|------|-----|
| One row/column of items | Flexbox |
| Row + Column grid simultaneously | CSS Grid |
| Full-page structure | CSS Grid |
| Overlay, fixed element, sticky header | Positioning |
| Content-driven sizing | Intrinsic (`fit-content`, `min-content`) |

### Responsive Strategy
| Content type | Strategy |
|------|-----|
| Content-driven, flexible | Responsive (fluid + breakpoints) |
| Distinct mobile/desktop UX | Adaptive (layout snap at breakpoints) |
| Component adapting to its container | Container Queries |

### Spacing Rhythm
- Base unit: `4px` or `8px`
- Gutters: `16px`–`32px`
- Section gaps: `48px`–`80px`
- Container max-width: `1200px`–`1440px`
- Line-height: `1.5`–`1.6` for body, `1.2`–`1.3` for headings

### Z-index Tier Convention
| Tier | Value | Usage |
|------|-------|-------|
| Page content | `0`–`100` | Cards, sections |
| Sticky headers | `100`–`200` | `position: sticky` nav |
| Dropdowns/popovers | `200`–`500` | Select menus, tooltips |
| Modals/overlays | `500`–`800` | Modal dialogs |
| Notifications/toasts | `800`–`1000` | Top-level alerts |
