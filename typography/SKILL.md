---
name: typography
description: "Frontend typography design skill. Distilled from design terminology reference — covers font classifications (Serif/Sans-Serif/Monospace/Proportional), text layout & spacing (Tracking/Kerning/Leading/Alignment), type anatomy (Baseline/X-height/Ascender/Descender/Cap Height), CSS units (PX/PT/EM/REM/CH), and rendering engineering (Anti-aliasing/Font Hinting/FOIT/FOUT/Font Fallback/Ligature). Use when choosing fonts, setting type scales, configuring text spacing, building font stacks, optimizing font loading, or troubleshooting text rendering. Triggers: 'typography', '文字排版', 'font', '字体', 'typeface', 'letter-spacing', 'line-height', 'font stack', 'font loading', 'FOIT', 'FOUT', 'serif', 'sans-serif', 'monospace', 'ligature', 'anti-aliasing', 'font hinting'."
---

# Typography Design — Frontend Type Engineering

Comprehensive reference for designing and implementing text typography. Covers font classifications, text spacing, type anatomy, CSS units, and rendering engineering — all aligned so AI agents produce readable, well-spaced, professionally typeset text.

---

## 1. Font Classifications & Basics

### Typography (文字排版)
Font selection, spacing adjustment, layout, and how text ultimately reads on screen or paper. Good typography gives readers an entry point, signals where to scan, and where to stop and read.

### Font (字体)
A collection of glyphs in a specific style, weight, and size. In digital development, typically a binary file (`.ttf`, `.otf`, `.woff2`). Fonts determine text's fundamental shape and affect the interface's tone, information density, and recognition efficiency.

### Serif (衬线体)
Fonts with decorative strokes ("feet") at stroke ends. Traditional, formal visual style. Good for long-form reading or classic aesthetics. Watch clarity at small sizes in UIs.

**Example**: `font-family: 'Georgia', 'Times New Roman', serif;`

### Sans-Serif (无衬线体)
Fonts with smooth stroke ends, no decoration. Clean, modern, clear — the default choice for digital interfaces. Stable at small sizes. **Use for**: buttons, navigation, forms, body text on screens.

**Example**: `font-family: 'Inter', 'Helvetica Neue', 'Arial', sans-serif;`

### Proportional Font (比例字体)
Each character occupies different horizontal width based on its shape (`W` vs `i`). More compact, natural rhythm. **Use for**: body text, labels, most UI text.

### Monospace (等宽字体)
Every character occupies the SAME horizontal width. **Use for**: code editors, terminals, data tables, logs, any content needing stable vertical alignment.

**Example**: `font-family: 'JetBrains Mono', 'Fira Code', 'Consolas', monospace;`

### Font Classification Decision Table

| Need | Font Type | CSS Example |
|------|-----------|-------------|
| Body text, UI labels | Sans-Serif | `'Inter', sans-serif` |
| Long-form reading, editorial | Serif | `'Georgia', serif` |
| Code, data, logs | Monospace | `'JetBrains Mono', monospace` |
| Compact UI labels | Proportional Sans-Serif | Most UI fonts |

---

## 2. Text Layout & Spacing

### Tracking (字间距 / Letter-spacing)
Uniform horizontal spacing applied across ALL characters in a word or text block. **CSS**: `letter-spacing`.
- Headings: slightly negative tracking tightens impact.
- All-caps text: increase tracking for legibility.
- Body text: default is usually best.

**Guidelines**:
- Headings: `-0.02em` to `-0.01em`
- All-caps labels: `0.05em` to `0.1em`
- Body: `0` (default)

### Kerning (字距微调)
Adjusting spacing between SPECIFIC letter PAIRS (e.g., A-V) to fix visual gaps from letter shapes. Local glyph-pair balance, not uniform spacing. Most well-designed fonts have built-in kerning tables — rarely manually adjusted in web typography. **CSS**: `font-kerning: normal | auto | none`.

### Leading (行间距 / Line-height)
Vertical distance between text lines. **CSS**: `line-height`.
- Too tight → text feels cramped, hard to follow.
- Too loose → lines feel disconnected.

**Guidelines**:
- Body text: `1.5`–`1.6`
- Headings: `1.2`–`1.3`
- Dense UIs (tables, lists): `1.35`–`1.45`
- Avoid unitless values below `1.2` for multiline text

### Alignment (对齐方式)
Horizontal alignment of text along a reference edge:
- **Left** (`text-align: left`): default for LTR languages, most readable for body text.
- **Right** (`text-align: right`): numbers, secondary info in tables.
- **Center** (`text-align: center`): short headings, CTAs — avoid for long body text.
- **Justify** (`text-align: justify`): even edges, but can create "rivers" of whitespace — use with `hyphens: auto`.

---

## 3. Type Anatomy

Understanding why the same `font-size` looks different across fonts — and how icons, text, and components align vertically.

### Baseline (基线)
The invisible horizontal line most letters sit on. The vertical alignment REFERENCE for all text.
- Buttons, inputs, icons, mixed-font text all depend on baseline for visual stability.
- **CSS**: `vertical-align: baseline` (default).

### X-height (x 字高)
The height of lowercase letter bodies (`x`, `a`, `e`), excluding ascenders/descenders. Two fonts at the same `font-size` can look different sizes — x-height is the main reason.
- Higher x-height → font appears larger, more legible at small sizes.
- Lower x-height → more elegant, traditional feel.

### Ascender (升部)
Upward strokes extending above x-height (`b`, `d`, `h`, `l`). Affects line-height and vertical spacing between text rows.

### Descender (降部)
Downward strokes extending below baseline (`g`, `j`, `p`, `q`). Must reserve enough space in line-height to avoid crowding adjacent lines.

### Cap Height (大写字高)
Height from baseline to top of capital letters (`H`, `I`). Together with x-height, determines visual proportions. Important for: English headings, button text, icon alignment.

---

## 4. CSS & Digital Typography Units

### PX (像素 / Pixel)
Screen display base unit. In CSS, a logical pixel — actual physical pixels depend on device pixel ratio (DPR).
- **Best for**: `font-size`, borders, icon sizes, component spacing — most explicit boundaries.
- Not user-scalable in the same way relative units are.

### PT (点 / Point)
Physical length unit: `1pt = 1/72 inch`. Used in iOS as logical measurement, mapped to physical pixels via scale factor. Common in OS-level typography, mobile UI, and print contexts.

### EM (相对单位)
Relative unit: `1em` = current element's `font-size`. COMPOUNDS with nesting depth.
- **Best for**: component-internal padding, icon sizes that should scale with local text.
- **Watch for**: nesting accumulation — a nested `0.8em` inside `0.8em` compounds.

### REM (根相对单位 / Root EM)
Relative unit: `1rem` = root `<html>` element's `font-size`. Always consistent regardless of nesting depth.
- **Best for**: design system type scales, global spacing, breakpoints.
- **Standard**: `html { font-size: 16px }` → `1rem = 16px`.

```
html { font-size: 16px; }       /* 1rem baseline */
h1   { font-size: 2rem; }       /* 32px — consistent everywhere */
p    { font-size: 1rem; }       /* 16px */
small { font-size: 0.875rem; }  /* 14px */
```

### CH (字符单位 / Character Unit)
Relative unit: `1ch` = width of the `0` character in the current font. In monospace, `1ch` = exact width of any character.
- **Best for**: input field widths (`width: 30ch` for ~30 characters), code block line lengths, table column widths.

### Unit Decision Table
| Goal | Unit | Why |
|------|------|-----|
| Global type scale, spacing | `rem` | Consistent, no nesting issues |
| Component-local scaling | `em` | Scales with component font-size |
| Fixed sizes (borders, icons) | `px` | Explicit, predictable |
| Character-count-based width | `ch` | Maps to text content length |
| Mobile/iOS designs | `pt` | Platform-native measurement |

---

## 5. Rendering & Advanced Engineering

### Anti-aliasing (抗锯齿 / 字体平滑)
Smooths font edges on screen by filling edge pixels with varying-opacity transition pixels, reducing stair-step aliasing. Directly affects visual comfort for small text and high-contrast text.
- **CSS**: `-webkit-font-smoothing: antialiased` (macOS/iOS), `-moz-osx-font-smoothing: grayscale` (macOS Firefox).

### Font Hinting (字体提示 / 字体微调)
At small sizes, aligns key strokes (horizontal/vertical) to pixel boundaries for crispness. More noticeable on low-resolution screens and information-dense UIs.
- Quality varies by font file — well-hinted fonts look sharper at small sizes.

### FOIT (Flash of Invisible Text / 无形文本闪烁)
Browser hides text while web font downloads, then reveals it. Content is briefly invisible → hurts perceived performance and reading continuity.
- **Solution**: Use `font-display: swap` to favor FOUT over FOIT.

### FOUT (Flash of Unstyled Text / 无样式文本闪烁)
Browser renders text in fallback font while web font downloads, then swaps. Shows content faster than FOIT, but causes layout shift.
- **Solution**: Match fallback font metrics to web font using `size-adjust`, `ascent-override`, `descent-override` in `@font-face`.

### Font Fallback (字体回退机制 / 字体栈)
Browser iterates through `font-family` list until it finds an available font. A good font stack reduces risk from loading failures, missing glyphs, and cross-platform differences.

**Example stack**:
```css
font-family: 'Inter', 'SF Pro Text', 'Helvetica Neue', 'Arial', sans-serif;
```

### Ligature (连字 / 合体字)
Merging two+ adjacent letters/symbols into one glyph. Resolves stroke collisions (`fi`, `fl`) and can display multi-char symbols as one continuous symbol (`=>`, `!=`).
- **Caution in code**: looks smoother but may reduce clarity for some developers.
- **CSS**: `font-variant-ligatures: common-ligatures | no-common-ligatures`.

---

## Quick Decision Cheatsheet

### Type Scale (8px baseline, 16px root)
| Element | `rem` | `px` (at 16px root) | Notes |
|---------|-------|---------------------|-------|
| Caption / tiny | `0.75rem` | 12px | Legal, footnotes |
| Body small | `0.875rem` | 14px | Secondary text |
| Body | `1rem` | 16px | Primary reading |
| Body large / H6 | `1.125rem` | 18px | Lead paragraph |
| H5 | `1.25rem` | 20px | Section subhead |
| H4 | `1.5rem` | 24px | Section heading |
| H3 | `1.875rem` | 30px | Major heading |
| H2 | `2.25rem` | 36px | Page heading |
| H1 | `3rem` | 48px | Hero / page title |

### Font Stack Template
```css
/* Sans-serif system stack */
--font-sans: 'Inter', 'SF Pro Text', -apple-system, BlinkMacSystemFont,
             'Segoe UI', 'Helvetica Neue', 'Arial', sans-serif;

/* Serif system stack */
--font-serif: 'Georgia', 'Times New Roman', 'Noto Serif SC', serif;

/* Monospace system stack */
--font-mono: 'JetBrains Mono', 'Fira Code', 'SF Mono', 'Consolas',
             'Liberation Mono', 'Courier New', monospace;
```

### Font Loading Best Practices
```css
@font-face {
  font-family: 'MyWebFont';
  src: url('/fonts/myfont.woff2') format('woff2');
  font-display: swap;           /* FOUT over FOIT */
  font-weight: 400;
  font-style: normal;
}
```

| Strategy | Pros | Cons |
|----------|------|------|
| `font-display: swap` | Content visible immediately | Layout shift on swap |
| `font-display: block` | No layout shift | Short invisible period |
| `font-display: optional` | No repaint after load | Font may never show |
| `font-display: fallback` | Short block, then fallback | Rare swap |

**Recommended**: `swap` + match fallback metrics with `size-adjust` to minimize layout shift.

### CJK Typography Considerations
- Chinese/Japanese/Korean text typically needs larger `line-height` (1.6–1.8) for readability.
- CJK characters are naturally monospaced-like in width — proportional tracking feels wrong.
- `letter-spacing` should rarely be applied to CJK body text.
- `text-align: justify` works well for CJK due to uniform character widths.
- Plan for larger font files — subset with `unicode-range` in `@font-face`.
