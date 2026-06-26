---
name: color-system
description: "Frontend color system design skill. Distilled from design terminology reference — covers color basics (Hue/Saturation/Lightness/Alpha), color spaces (RGB/Hex/HSL/OKLCH/sRGB/P3), color architecture & palettes (Primary/Semantic/Neutral/Color Scale), design tokens & theming (Primitive/Semantic Tokens, Light/Dark Mode), accessibility (WCAG contrast ratios, color blindness, forced colors), and visual effects (gradients, blending modes). Use when designing color systems, creating palettes, building design tokens, choosing color spaces, ensuring accessibility compliance, or setting up light/dark theming. Triggers: 'color', '色彩', 'palette', '调色盘', 'color system', '色彩系统', 'design tokens', 'dark mode', '深色模式', 'WCAG', 'contrast', '对比度', 'hex', 'HSL', 'OKLCH', 'gradient', '渐变色', 'brand color', '品牌色'."
---

# Color System Design — Frontend Color Engineering

Comprehensive reference for designing color systems. Covers color perception basics, color spaces & representation, palette architecture, design tokens & theming, accessibility standards, and visual effects — all aligned so AI agents produce visually coherent, accessible color schemes.

---

## 1. Color Basics & Perception

### Hue (色相)
What CATEGORY a color belongs to: red, yellow, green, blue, purple. In HSL/HSV, hue is placed on a 0°–360° circle (the color wheel). You're essentially choosing a direction on the wheel.

- **CSS**: `hsl(240, 100%, 50%)` — the `240` is the hue (blue).

### Saturation (饱和度)
How VIVID / intense a color is. High saturation = bright and eye-catching. Low saturation = muted, tending toward gray.
- **UI rule**: Primary buttons can be slightly more saturated. Backgrounds and large color blocks should be toned down to avoid eye strain.

### Chroma (彩度)
Also describes color intensity, but in PERCEPTUAL color models like OKLCH. Measures how far a color is from the gray axis.
- **Key benefit**: When building color scales, stable Chroma produces colors that feel like they "belong together."

### Lightness (明度)
How light/dark a color is in a given color model. In HSL: `0%` ≈ black, `100%` ≈ white, `50%` is usually the most saturated version of that hue.

### Luminance (亮度)
PERCEIVED brightness to the human eye. The same numeric lightness value looks different across hues — yellow appears brighter than blue even at the same HSL L value.
- **Critical for**: contrast ratio calculations, accessibility.

### Alpha (透明通道)
Controls how much a color REVEALS what's behind it. `Alpha = 1` → fully opaque. Lower alpha → background shows through.
- **CSS**: `rgba(0, 0, 0, 0.5)` — last value is alpha.

### Opacity (不透明度)
How opaque the ENTIRE element is. `100%` = fully opaque, `0%` = fully transparent.
- **Key distinction**: CSS `opacity` affects the WHOLE element (text, icons, children). Alpha on a color value only affects that specific color.
- Design tools use checkerboard patterns to indicate transparency.

### Warm Color (暖色)
Colors with warm associations: red, orange, yellow. Perceived as "closer" and "hotter."
- **UI use**: warnings, promotions, high-energy CTAs, sale tags.

### Cool Color (冷色)
Colors with cool associations: blue, cyan, purple. Perceived as "farther" and "calmer."
- **UI use**: information areas, backgrounds, data panels, interfaces needing reduced stimulation.

---

## 2. Color Representation & Color Spaces

### RGB (Red, Green, Blue)
Mixes red, green, blue light channels to create screen colors. Each channel: 0–255. All 0 = black. All 255 = white.
- **CSS**: `rgb(59, 130, 246)`.

### RGBA (Red, Green, Blue, Alpha)
RGB + Alpha channel for transparency.
- **CSS**: `rgba(59, 130, 246, 0.5)`.

### Hex Code (十六进制颜色码)
Web standard color format. `#` followed by 6 hex digits (RRGGBB). Each pair controls one channel: `00`–`FF` (0–255).
- 8-digit hex adds alpha: `#FF573380` — last two `80` is alpha (`FF` = opaque, `00` = transparent).
- **CSS**: `#3B82F6`, `#FF573380`.

### HSL (Hue, Saturation, Lightness)
Describes color in human-friendly terms: "change hue, make it more vivid, make it lighter."
- More intuitive than RGB for manual adjustments.
- **CSS**: `hsl(217, 91%, 60%)`.

### HSLA (Hue, Saturation, Lightness, Alpha)
HSL + Alpha channel.
- Best for: overlays, floating elements, semi-transparent states while keeping HSL's intuitive adjustment model.

### OKLCH (Oklab Lightness, Chroma, Hue)
Perceptually uniform color model. The `L` in OKLCH more accurately reflects what the human eye perceives as brightness.
- **HSL problem**: Yellow `L=50%` and blue `L=50%` — yellow still looks brighter, blue darker.
- **OKLCH solves this**: Same L = same perceived brightness across hues.
- **Use cases**: color scales, theme switching, accessibility-conscious design systems.
- **CSS**: `oklch(62.8% 0.26 255)` — modern CSS support, with `@supports` fallback.

### Color Gamut (色域)
How many colors a device or color system can display. Screens, wide-gamut displays, and printers all have different gamuts.

### Color Space (色彩空间)
An agreed-upon "color map" so design tools, browsers, and devices interpret the same value consistently.

### sRGB (Standard RGB)
The DEFAULT color space for web and standard displays. Narrowest gamut but best compatibility. Use sRGB for maximum reach.

### Adobe RGB
Wider gamut than sRGB, especially in cyan-green range. Used in professional photography and print workflows.

### Display P3
Wide-gamut color space supported by modern phones and laptops. Can display more vivid reds, yellows, greens than sRGB.
- Great for modern-device visuals, but plan sRGB fallback for older screens.

### Rec. 2020 (BT.2020)
Very wide gamut, targeting 4K/8K, HDR video, and high-end projection. Most consumer screens can't fully display its range. Not a daily web UI target.

### Color Space Decision Table
| Use Case | Space |
|----------|-------|
| General web UI, maximum compatibility | sRGB |
| Modern devices, vivid brand visuals | Display P3 (with sRGB fallback) |
| Print-to-screen workflow | Adobe RGB |
| HDR video, cinema | Rec. 2020 |

---

## 3. Color Architecture & Palettes

### Palette (调色盘 / 色板)
A project's ALLOWED set of colors. Prevents every page from independently choosing its own blue. Enables teams to say "THIS blue" unambiguously.

### Color Scale (色阶)
A single base color expanded into a ladder of light-to-dark variants.
- Light scales → backgrounds, borders.
- Mid scales → buttons, interactive elements.
- Dark scales → hover states, dark text.
- Naming convention: Tailwind (50–950), Material Design (50–900).

### Tint (加白)
Adding WHITE to a color → lighter, softer. Used for light backgrounds, hint backgrounds, lightweight labels.
- **CSS technique**: `color-mix(in srgb, base 70%, white)` or precomputed scale.

### Shade (加黑)
Adding BLACK to a color → darker, heavier. Used for dark text, pressed states, dark backgrounds.

### Tone (加灰)
Adding GRAY to a color → less vivid, quieter. Used for large backgrounds, illustrations, subdued interfaces.

### Primary Color (主色 / 品牌色)
The most-used, most MEMORABLE color. Appears on: primary buttons, selected items, key links, brand areas.

### Secondary Color (辅助色)
COMPLEMENTS the primary color. Appears on: secondary buttons, auxiliary entry points, brand extensions. Must not compete with primary for visual priority.

### Accent Color (强调色)
Creates LOCAL emphasis. SMALL-AREA use only: promo tags, VIP badges, notification dots, special highlights.
- **Warning**: Overusing accent color steals attention from primary.

### Semantic Color (语义色)
Colors carrying MEANING: green = success, red = danger/error, yellow = warning. Best paired with text or icons — never rely on color alone.

### Status Color (状态色)
Expresses CURRENT state: success, error, warning, info, disabled. Very close to Semantic Color but emphasizes what STATE a component/object is in.

### Foreground Color (前景色)
Text, icons, borders. Must maintain sufficient contrast against background.

### Background Color (背景色)
The surface beneath text, icons, buttons, cards. Determines overall lightness/darkness and affects foreground readability.

### Neutral Color (中性色 / 无彩色)
Black, white, grays (sometimes with slight warm/cool bias). Handles the most common, least glamorous parts: body text, secondary text, dividers, borders, disabled states, backgrounds.

---

## 4. Color Engineering & Tokens

### Design Tokens (设计令牌)
Design decisions stored as VARIABLES. Colors, spacing, fonts, radii can all be tokens. Benefit: design files and code use the SAME names instead of guessing hex values.

### CSS Custom Properties (CSS 变量)
CSS variables like `--color-primary`. Can be reused and overridden by themes. Web color tokens typically map to these.
```css
:root {
  --color-primary: #3B82F6;
  --color-primary-hover: #2563EB;
}
.dark {
  --color-primary: #60A5FA;
}
```

### Primitive Token (原始令牌)
Stores CONCRETE colors: `blue-500`, `red-300`. These are the "raw materials" — describe what the color IS objectively.

### Semantic Token (语义令牌)
Stores PURPOSE: `text-primary`, `danger-bg`, `button-primary-bg`. Components should use semantic tokens, so theme changes only require remapping, not touching every component.

```
Primitive:              Semantic:
blue-500: #3B82F6  →    button-primary-bg: blue-500
                        link-color: blue-500
red-500: #EF4444   →    danger-text: red-500
                        error-border: red-500
```

### Theming (主题化)
Switching the interface between different appearances. Component structure stays the same; semantic tokens point to different primitives.
- `text-primary` → dark gray (light mode) / light gray (dark mode).

### Light Mode (浅色模式)
Light background, dark text. Like reading on paper. Suits bright environments. Most websites' default.

### Dark Mode (深色模式)
Dark background, light text. Reduces overall brightness for low-light environments. May save power on OLED screens.
- **Critical**: NEVER simply invert light mode colors. Dark backgrounds change color perception — primary/accent colors need luminosity and saturation re-adjustment to avoid feeling muddy or harsh.

---

## 5. Accessibility & Readability

### Relative Luminance (相对亮度)
How bright a color appears to the human eye. Different hues have different perceived brightness: green > red > blue at the same numeric value.
- The sRGB relative luminance formula accounts for this perceptual difference.

### Contrast Ratio (对比度)
The brightness difference between foreground and background. White-on-white = `1:1` (invisible). Black-on-white = up to `21:1`.

### WCAG Standards
Web Content Accessibility Guidelines — the standard for web accessibility.

**AA (minimum)**: Normal text ≥ `4.5:1`, large text (≥18pt or ≥14pt bold) ≥ `3:1`.
**AAA (enhanced)**: Normal text ≥ `7:1`, large text ≥ `4.5:1`.

> Always target AA at minimum for body text. AAA is aspirational for most UIs.

### Color Blindness (色盲/色弱适配)
Users with color vision deficiency may not distinguish certain hues, especially red-green. **Never** convey state through color alone.
- ✅ Good: Red text + ❌ icon + "Error: Invalid email"
- ❌ Bad: Only red border to indicate error
- Add text, icons, or shape differences alongside color coding.

### Forced Colors / High Contrast Mode (强制色 / 高对比模式)
Windows High Contrast Mode and assistive tools override page colors with system-specified high-contrast themes.
- Shadows, gradient backgrounds, and decorative colors may be ignored/replaced.
- Buttons, links, and borders rely on system colors instead.
- **CSS**: Use `forced-colors: active` media query to adjust styles for this mode.

---

## 6. Rendering & Visual Effects

### Gradient (渐变色)
Smooth transition between two or more colors. The browser/design tool calculates intermediate colors between start and end points.
- **Linear gradient**: along a direction (`linear-gradient(to right, blue, purple)`).
- **Radial gradient**: from center outward (`radial-gradient(circle, white, gray)`).

### Blending Mode (混合模式)
How upper-layer colors mix with lower-layer colors. Photoshop's Multiply, Screen — CSS `mix-blend-mode` and `background-blend-mode`.
- Different modes use different algorithms to compute the color where layers meet.
- Common CSS values: `multiply`, `screen`, `overlay`, `darken`, `lighten`, `color-dodge`, `color-burn`.

---

## Quick Decision Cheatsheet

### Color Space Selection
| Goal | Space |
|------|-------|
| Max compatibility, web UI | sRGB + Hex |
| Human-friendly manual adjustment | HSL |
| Perceptually uniform scales, theming | OKLCH |
| Vivid modern devices | Display P3 (fallback sRGB) |

### Token Architecture
```
Layer 1: Primitive Tokens
  blue-500: #3B82F6
  red-500: #EF4444
  gray-100: #F3F4F6
  gray-900: #111827

Layer 2: Semantic Tokens    ← USE THESE IN COMPONENTS
  --color-primary: blue-500
  --color-primary-hover: blue-600
  --color-danger: red-500
  --bg-surface: gray-100
  --text-primary: gray-900
  --text-secondary: gray-500

Layer 3: Theme Overrides
  .dark {
    --bg-surface: gray-900;
    --text-primary: gray-100;
    --text-secondary: gray-400;
  }
```

### WCAG Compliance Checklist
- [ ] Body text ≥ 4.5:1 contrast (AA)
- [ ] Large text ≥ 3:1 contrast (AA)
- [ ] States not conveyed by color alone (icons + text alongside color)
- [ ] Focus indicators visible
- [ ] Test with forced-colors mode

### Semantic Color Convention
| Meaning | Typical Hue | Example Use |
|---------|-------------|-------------|
| Success | Green | Confirmation, completion badges |
| Danger / Error | Red | Error messages, destructive buttons |
| Warning | Yellow / Orange | Alerts, caution notices |
| Info | Blue | Informational banners, tips |
| Disabled | Gray | Inactive controls, unavailable options |

### Dark Mode Adjustment Rules
- [ ] Background: dark gray (`#111`–`#1A1A2E`), not pure black
- [ ] Text: light gray (`#E5E5E5`), not pure white
- [ ] Primary color: INCREASE lightness, slightly REDUCE saturation
- [ ] Semantic colors: recheck all contrast ratios
- [ ] Shadows: use lighter, more subtle shadows (or eliminate)
- [ ] Borders: use rgba white at low alpha instead of dark borders
