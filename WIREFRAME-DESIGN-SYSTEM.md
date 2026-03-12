# Wireframe Design System: Research & Specification

A comprehensive guide for building a high-fidelity grayscale wireframe component system for the DreamHost homepage redesign competitive research dashboard.

---

## 1. Modern UX Best Practices for Data-Heavy Dashboards

### Information Architecture for Competitive Analysis

**Hierarchy of information density:**
1. **Executive summary layer** -- 3-5 KPIs visible immediately (score cards, status indicators)
2. **Comparative analysis layer** -- Side-by-side breakdowns, matrices, trend lines
3. **Deep-dive layer** -- Full data tables, raw findings, expandable detail panels

**Progressive disclosure reduces cognitive load by ~37%.** The pattern:
- Top level: High-level metrics and status badges
- Second level: Trend analysis, comparison charts, summary panels
- Third level: Raw data tables, export options, methodology notes

**Key principles:**
- Show only what is necessary at each interaction level
- Defer complexity to deeper layers
- Use expandable panels, drill-through links, and tabbed sections to layer information
- Mobile versions should prioritize the most critical data points first

### Data Visualization in Marketing/Strategy Contexts

**Best practices for marketing dashboards:**
- Lead with outcomes (conversions, revenue impact), not vanity metrics
- Use relative comparisons (vs. competitor, vs. industry average) rather than absolute numbers
- Color-code status: green/pass, yellow/caution, red/fail -- in grayscale, use fill density or icon indicators
- Bar charts for comparisons, line charts for trends, tables for detailed breakdowns
- Keep chart labels visible without hover interaction for scannability

### Tab/Panel Navigation Patterns

**When to use tabs vs. other patterns:**
- Tabs: 2-7 categories of equal weight, user needs to switch frequently
- Accordion: Sequential or hierarchical content, variable-length sections
- Segmented control: Binary or ternary toggle (e.g., Desktop/Mobile/Tablet)
- Sidebar nav: 8+ categories, persistent context needed

**Tab design rules:**
- Active tab must be visually distinct (weight, underline, or background shift)
- Tab labels should be 1-2 words maximum
- Horizontal tabs for 2-5 items; scrollable tab bar for 6+
- Content area should not shift height dramatically between tabs

### Comparison Matrix Design

**Effective comparison tables:**
- Sticky first column (feature names) and sticky header row (competitor names)
- Alternating row backgrounds for scannability
- Use checkmarks, X marks, and partial-fill indicators rather than text where possible
- Highlight the "recommended" or "your site" column with a subtle background tint
- On mobile: convert to card-per-competitor view, or show 2 columns at a time with swipe navigation

### Responsive Tables on Mobile

**Strategies ranked by effectiveness:**
1. **Card conversion** -- Each table row becomes a card with key fields as header
2. **Priority columns** -- Show only 2-3 most important columns, hide rest behind "More" toggle
3. **Horizontal scroll** -- Freeze first column, allow horizontal swipe for remaining
4. **Collapsed accordion** -- Each row becomes an expandable summary

**Rule of thumb:** Design mobile-first. If a table cannot be understood at 375px width, restructure it as cards.

---

## 2. Modern CSS-Only UI Component Patterns

### Tabbed Navigation (Accessible, CSS-Driven)

```html
<div class="tabs" role="tablist">
  <input type="radio" name="tab-group" id="tab-1" checked
         role="tab" aria-controls="panel-1">
  <label for="tab-1">Overview</label>

  <input type="radio" name="tab-group" id="tab-2"
         role="tab" aria-controls="panel-2">
  <label for="tab-2">Competitors</label>

  <input type="radio" name="tab-group" id="tab-3"
         role="tab" aria-controls="panel-3">
  <label for="tab-3">Recommendations</label>

  <div class="tab-panel" id="panel-1" role="tabpanel">...</div>
  <div class="tab-panel" id="panel-2" role="tabpanel">...</div>
  <div class="tab-panel" id="panel-3" role="tabpanel">...</div>
</div>
```

```css
.tabs input[type="radio"] {
  position: absolute;
  opacity: 0;
  pointer-events: none;
}

.tabs label {
  display: inline-block;
  padding: 0.75rem 1.5rem;
  font-weight: 500;
  color: var(--text-secondary);
  border-bottom: 2px solid transparent;
  cursor: pointer;
  transition: all 0.2s ease;
}

.tabs input:checked + label {
  color: var(--text-primary);
  border-bottom-color: var(--accent);
  font-weight: 600;
}

.tabs input:focus-visible + label {
  outline: 2px solid var(--accent);
  outline-offset: 2px;
  border-radius: 4px;
}

.tab-panel {
  display: none;
  padding: 1.5rem 0;
}

/* Each checked radio shows its corresponding panel */
#tab-1:checked ~ #panel-1,
#tab-2:checked ~ #panel-2,
#tab-3:checked ~ #panel-3 {
  display: block;
  animation: fadeIn 0.25s ease;
}
```

**Accessibility notes:** Pure CSS tabs cannot fully meet ARIA spec (arrow key navigation requires JS). For production, add minimal JS for arrow key handling, or accept that Tab key navigation between radio inputs provides adequate keyboard access.

### Expandable/Collapsible Panels (Native HTML)

```html
<details class="accordion-item">
  <summary>Section Title</summary>
  <div class="accordion-content">
    <p>Content goes here...</p>
  </div>
</details>
```

```css
details.accordion-item {
  border: 1px solid var(--border-subtle);
  border-radius: 8px;
  margin-bottom: 0.5rem;
  overflow: hidden;
}

details.accordion-item summary {
  padding: 1rem 1.5rem;
  font-weight: 600;
  cursor: pointer;
  list-style: none; /* Remove default marker */
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: var(--surface-elevated);
  transition: background 0.2s ease;
}

details.accordion-item summary:hover {
  background: var(--surface-hover);
}

details.accordion-item summary::after {
  content: "+";
  font-size: 1.25rem;
  font-weight: 300;
  transition: transform 0.2s ease;
}

details[open] summary::after {
  content: "-";
}

/* Smooth open animation using grid trick */
details .accordion-content {
  display: grid;
  grid-template-rows: 0fr;
  transition: grid-template-rows 0.3s ease;
}

details[open] .accordion-content {
  grid-template-rows: 1fr;
}

details .accordion-content > * {
  overflow: hidden;
}
```

**Note on animation:** The `grid-template-rows: 0fr` to `1fr` transition is the modern CSS-only way to animate height from 0 to auto. Browser support is strong in 2025+.

### Comparison Tables with Sticky Headers

```css
.comparison-table-wrapper {
  overflow-x: auto;
  -webkit-overflow-scrolling: touch;
  border: 1px solid var(--border-subtle);
  border-radius: 12px;
}

.comparison-table {
  width: 100%;
  border-collapse: collapse;
  min-width: 600px; /* Force horizontal scroll on small screens */
}

.comparison-table thead th {
  position: sticky;
  top: 0;
  z-index: 10;
  background: var(--surface-elevated);
  padding: 1rem;
  font-weight: 600;
  text-align: left;
  border-bottom: 2px solid var(--border-medium);
}

/* Sticky first column */
.comparison-table td:first-child,
.comparison-table th:first-child {
  position: sticky;
  left: 0;
  z-index: 5;
  background: var(--bg-page);
  font-weight: 500;
  border-right: 1px solid var(--border-subtle);
}

/* Corner cell needs highest z-index */
.comparison-table thead th:first-child {
  z-index: 15;
}

.comparison-table tbody tr:nth-child(even) {
  background: var(--surface-alt);
}

.comparison-table tbody tr:hover {
  background: var(--surface-hover);
}

.comparison-table td {
  padding: 0.75rem 1rem;
  border-bottom: 1px solid var(--border-subtle);
}
```

### Card Grids with Hover States

```css
.card-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 1.5rem;
}

/* With subgrid for aligned content across cards */
.card {
  display: grid;
  grid-template-rows: subgrid;
  grid-row: span 3; /* title + body + footer */
  background: var(--surface-card);
  border: 1px solid var(--border-subtle);
  border-radius: 12px;
  padding: 1.5rem;
  transition: all 0.2s ease;
}

.card:hover {
  border-color: var(--border-medium);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
  transform: translateY(-2px);
}
```

### Tooltip Pattern (CSS Anchor Positioning)

```css
/* Modern approach: CSS Anchor Positioning (Chrome 125+) */
.tooltip-trigger {
  anchor-name: --trigger;
  cursor: help;
}

.tooltip-trigger .tooltip {
  position: fixed;
  position-anchor: --trigger;
  position-area: top;
  margin-bottom: 8px;

  background: var(--surface-tooltip);
  color: var(--text-on-dark);
  padding: 0.5rem 0.75rem;
  border-radius: 6px;
  font-size: 0.8125rem;
  max-width: 250px;

  /* Hidden by default */
  opacity: 0;
  pointer-events: none;
  transition: opacity 0.15s ease;
}

.tooltip-trigger:hover .tooltip,
.tooltip-trigger:focus-visible .tooltip {
  opacity: 1;
}

/* Fallback for browsers without anchor positioning */
@supports not (anchor-name: --x) {
  .tooltip-trigger {
    position: relative;
  }
  .tooltip-trigger .tooltip {
    position: absolute;
    bottom: calc(100% + 8px);
    left: 50%;
    transform: translateX(-50%);
  }
}
```

### Tag/Badge/Pill System

```css
.badge {
  display: inline-flex;
  align-items: center;
  gap: 0.375rem;
  padding: 0.25rem 0.75rem;
  border-radius: 100px;
  font-size: 0.75rem;
  font-weight: 600;
  letter-spacing: 0.02em;
  white-space: nowrap;
}

.badge--positive {
  background: var(--status-positive-bg);
  color: var(--status-positive-text);
}

.badge--warning {
  background: var(--status-warning-bg);
  color: var(--status-warning-text);
}

.badge--negative {
  background: var(--status-negative-bg);
  color: var(--status-negative-text);
}

.badge--neutral {
  background: var(--surface-alt);
  color: var(--text-secondary);
}

/* Grayscale equivalents */
.badge--positive { background: #e8e8e8; color: #1a1a1a; }
.badge--warning  { background: #d4d4d4; color: #333; }
.badge--negative { background: #3a3a3a; color: #fff; }
.badge--neutral  { background: #f0f0f0; color: #666; }
```

### CSS-Only Bar Charts

```css
.bar-chart {
  --max-value: 100;
  display: flex;
  align-items: flex-end;
  gap: 0.5rem;
  height: 200px;
  padding: 0 1rem;
  border-bottom: 2px solid var(--border-medium);
}

.bar-chart .bar {
  flex: 1;
  background: var(--accent);
  border-radius: 4px 4px 0 0;
  min-height: 4px;
  transition: height 0.4s ease;
  position: relative;
}

/* Use inline style for dynamic values: style="--value: 75" */
.bar-chart .bar {
  height: calc((var(--value) / var(--max-value)) * 100%);
}

.bar-chart .bar::after {
  content: attr(data-label);
  position: absolute;
  bottom: -2rem;
  left: 50%;
  transform: translateX(-50%);
  font-size: 0.6875rem;
  color: var(--text-muted);
  white-space: nowrap;
}
```

### Scroll-Driven Animations

```css
/* Fade in sections as they scroll into view */
@keyframes reveal {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.scroll-reveal {
  animation: reveal linear both;
  animation-timeline: view();
  animation-range: entry 0% entry 30%;
}

/* Progress bar tied to scroll position */
.scroll-progress {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 3px;
  background: var(--accent);
  transform-origin: left;
  animation: grow-progress linear;
  animation-timeline: scroll();
}

@keyframes grow-progress {
  from { transform: scaleX(0); }
  to { transform: scaleX(1); }
}
```

---

## 3. High-Fidelity Grayscale Wireframe Design System

### Color Tokens

**Background Tiers:**

| Token | Value | Usage |
|---|---|---|
| `--bg-page` | `#FFFFFF` | Page background |
| `--bg-section` | `#F8F9FA` | Alternating section backgrounds |
| `--surface-card` | `#FFFFFF` | Card background (on section bg) |
| `--surface-elevated` | `#F2F3F5` | Elevated card, table header, sidebar |
| `--surface-alt` | `#F8F9FA` | Alternating table rows, secondary surfaces |
| `--surface-hover` | `#ECEDEF` | Hover state for interactive surfaces |
| `--surface-tooltip` | `#1A1A1A` | Tooltip backgrounds (inverted) |
| `--surface-overlay` | `rgba(0,0,0,0.5)` | Modal/overlay backdrop |

**Text Hierarchy:**

| Token | Value | Usage |
|---|---|---|
| `--text-primary` | `#111111` | Headlines, primary content |
| `--text-body` | `#333333` | Body text, descriptions |
| `--text-secondary` | `#555555` | Secondary text, captions |
| `--text-muted` | `#888888` | Labels, placeholders, meta |
| `--text-disabled` | `#BBBBBB` | Disabled controls |
| `--text-on-dark` | `#FFFFFF` | Text on dark backgrounds |
| `--text-on-accent` | `#FFFFFF` | Text on accent buttons |

**Border Colors:**

| Token | Value | Usage |
|---|---|---|
| `--border-subtle` | `#E5E7EB` | Card borders, dividers |
| `--border-medium` | `#D1D5DB` | Table borders, input borders |
| `--border-strong` | `#9CA3AF` | Active/focused borders |
| `--border-accent` | `var(--accent)` | Accent-colored borders |

**Accent Color:**

| Token | Value | Usage |
|---|---|---|
| `--accent` | `#2563EB` | Primary CTA buttons, active tabs, links |
| `--accent-hover` | `#1D4ED8` | Hover state for accent elements |
| `--accent-light` | `#EFF6FF` | Accent tint for highlighted cards/rows |
| `--accent-muted` | `#93C5FD` | Accent at reduced intensity |

**Status Colors (Grayscale Equivalents):**

| Token | Value | Usage |
|---|---|---|
| `--status-positive-bg` | `#E8E8E8` | Success backgrounds |
| `--status-positive-text` | `#1A1A1A` | Success text |
| `--status-warning-bg` | `#D4D4D4` | Warning backgrounds |
| `--status-warning-text` | `#333333` | Warning text |
| `--status-negative-bg` | `#3A3A3A` | Error backgrounds |
| `--status-negative-text` | `#FFFFFF` | Error text |

### Typography

**Recommended Font:** [General Sans](https://www.fontshare.com/fonts/general-sans) by Indian Type Foundry (free, variable weight)

- Geometric sans-serif with distinctive personality
- More compact and rational than Montserrat
- Friendly without being casual
- Excellent readability at small sizes
- Variable font file = single HTTP request for all weights
- Fallback: `system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif`

Alternative picks: **Figtree** (Google Fonts, friendly + minimal), **Satoshi** (Fontshare, clean + modern), **Plus Jakarta Sans** (Google Fonts, geometric + warm)

**Type Scale (Major Third ratio -- 1.25):**

| Token | Size | Line Height | Weight | Usage |
|---|---|---|---|---|
| `--text-xs` | 0.6875rem (11px) | 1.45 | 400-500 | Micro labels, footnotes |
| `--text-sm` | 0.8125rem (13px) | 1.5 | 400-500 | Captions, helper text, badges |
| `--text-base` | 1rem (16px) | 1.6 | 400 | Body text, table cells |
| `--text-md` | 1.125rem (18px) | 1.55 | 400-500 | Large body, lead paragraphs |
| `--text-lg` | 1.25rem (20px) | 1.5 | 500-600 | Card titles, section labels |
| `--text-xl` | 1.5rem (24px) | 1.4 | 600 | Section headings (h3) |
| `--text-2xl` | 1.875rem (30px) | 1.35 | 600-700 | Page sub-headings (h2) |
| `--text-3xl` | 2.25rem (36px) | 1.3 | 700 | Page headings (h1 mobile) |
| `--text-4xl` | 3rem (48px) | 1.2 | 700 | Hero headings (h1 desktop) |
| `--text-5xl` | 4rem (64px) | 1.1 | 700 | Display headings |

**Weight Usage:**

| Weight | Name | Usage |
|---|---|---|
| 400 | Regular | Body text, descriptions, table cells |
| 500 | Medium | Labels, navigation, emphasized body, card titles |
| 600 | Semibold | Section headings, button text, tab labels |
| 700 | Bold | Page headings, hero text, strong emphasis |

**Fluid Typography Implementation:**

```css
:root {
  --text-base: clamp(0.9375rem, 0.875rem + 0.25vw, 1rem);
  --text-lg: clamp(1.125rem, 1rem + 0.5vw, 1.25rem);
  --text-xl: clamp(1.25rem, 1rem + 1vw, 1.5rem);
  --text-2xl: clamp(1.5rem, 1rem + 1.5vw, 1.875rem);
  --text-3xl: clamp(1.75rem, 1rem + 2.5vw, 2.25rem);
  --text-4xl: clamp(2rem, 1rem + 3.5vw, 3rem);
  --text-5xl: clamp(2.5rem, 1rem + 5vw, 4rem);
}
```

### Spacing Scale

**Base unit: 4px.** All spacing derives from multiples of 4.

| Token | Value | Usage |
|---|---|---|
| `--space-1` | 0.25rem (4px) | Tight inline spacing, icon gaps |
| `--space-2` | 0.5rem (8px) | Badge padding, tight gaps |
| `--space-3` | 0.75rem (12px) | Input padding, small card gap |
| `--space-4` | 1rem (16px) | Default gap, paragraph spacing |
| `--space-5` | 1.25rem (20px) | Card padding (compact) |
| `--space-6` | 1.5rem (24px) | Card padding (standard), section gap |
| `--space-8` | 2rem (32px) | Section padding, large gaps |
| `--space-10` | 2.5rem (40px) | Major section spacing |
| `--space-12` | 3rem (48px) | Page section dividers |
| `--space-16` | 4rem (64px) | Hero/header spacing |
| `--space-20` | 5rem (80px) | Major page section breaks |
| `--space-24` | 6rem (96px) | Top-level section separation |

**Component Spacing:**
- Card inner padding: `--space-6` (24px)
- Card gap in grid: `--space-6` (24px)
- Table cell padding: `--space-3` vertical, `--space-4` horizontal
- Button padding: `--space-3` vertical, `--space-6` horizontal
- Input padding: `--space-3` all sides
- Section heading to content: `--space-4` (16px)

**Section Spacing:**
- Between major page sections: `--space-16` to `--space-20` (64-80px)
- Between sub-sections: `--space-10` to `--space-12` (40-48px)
- Between heading and first element: `--space-4` to `--space-6` (16-24px)

### Border Radius Scale

| Token | Value | Usage |
|---|---|---|
| `--radius-sm` | 4px | Badges, small pills |
| `--radius-md` | 8px | Buttons, inputs, small cards |
| `--radius-lg` | 12px | Cards, panels |
| `--radius-xl` | 16px | Large cards, modals |
| `--radius-2xl` | 24px | Hero sections, featured cards |
| `--radius-full` | 9999px | Pills, avatars, circular elements |

### Shadow Scale

| Token | Value | Usage |
|---|---|---|
| `--shadow-sm` | `0 1px 2px rgba(0,0,0,0.05)` | Subtle lift (buttons, badges) |
| `--shadow-md` | `0 2px 8px rgba(0,0,0,0.08)` | Cards at rest |
| `--shadow-lg` | `0 4px 16px rgba(0,0,0,0.1)` | Cards on hover, dropdowns |
| `--shadow-xl` | `0 8px 32px rgba(0,0,0,0.12)` | Modals, elevated panels |

---

### Component Specifications

#### Cards

**Standard Card:**
```css
.card {
  background: var(--surface-card);
  border: 1px solid var(--border-subtle);
  border-radius: var(--radius-lg);
  padding: var(--space-6);
  box-shadow: var(--shadow-sm);
}
```

**Elevated Card:**
```css
.card--elevated {
  background: var(--surface-card);
  border: 1px solid var(--border-subtle);
  border-radius: var(--radius-lg);
  padding: var(--space-6);
  box-shadow: var(--shadow-md);
}

.card--elevated:hover {
  box-shadow: var(--shadow-lg);
  transform: translateY(-2px);
  transition: all 0.2s ease;
}
```

**Outlined Card:**
```css
.card--outlined {
  background: transparent;
  border: 1.5px solid var(--border-medium);
  border-radius: var(--radius-lg);
  padding: var(--space-6);
}
```

**Highlighted Card (accent tint):**
```css
.card--highlight {
  background: var(--accent-light);
  border: 1.5px solid var(--accent-muted);
  border-radius: var(--radius-lg);
  padding: var(--space-6);
}
```

#### Tables

```css
.data-table {
  width: 100%;
  border-collapse: collapse;
  font-size: var(--text-sm);
}

.data-table thead {
  position: sticky;
  top: 0;
  z-index: 10;
}

.data-table th {
  background: var(--surface-elevated);
  padding: var(--space-3) var(--space-4);
  text-align: left;
  font-weight: 600;
  font-size: var(--text-xs);
  text-transform: uppercase;
  letter-spacing: 0.05em;
  color: var(--text-muted);
  border-bottom: 2px solid var(--border-medium);
}

.data-table td {
  padding: var(--space-3) var(--space-4);
  border-bottom: 1px solid var(--border-subtle);
  color: var(--text-body);
}

.data-table tbody tr:hover {
  background: var(--surface-hover);
}

.data-table tbody tr:nth-child(even) {
  background: var(--surface-alt);
}
```

#### Horizontal Tabs

```css
.tab-bar {
  display: flex;
  gap: 0;
  border-bottom: 1px solid var(--border-subtle);
  overflow-x: auto;
  -webkit-overflow-scrolling: touch;
}

.tab-bar .tab {
  padding: var(--space-3) var(--space-6);
  font-size: var(--text-sm);
  font-weight: 500;
  color: var(--text-muted);
  border-bottom: 2px solid transparent;
  white-space: nowrap;
  cursor: pointer;
  transition: all 0.2s ease;
  background: none;
  border-top: none;
  border-left: none;
  border-right: none;
}

.tab-bar .tab:hover {
  color: var(--text-body);
}

.tab-bar .tab--active {
  color: var(--accent);
  border-bottom-color: var(--accent);
  font-weight: 600;
}
```

#### Accordions

See the `<details>/<summary>` pattern in Section 2 above. Additional specification:

- Closed state: `+` icon on right, semibold title, subtle background
- Open state: `-` icon, content revealed with `grid-template-rows` animation
- Grouped accordions: stack with `gap: 0.5rem`, each with own border-radius
- Exclusive mode (only one open): requires minimal JS; CSS-only allows multiple open

#### Badges/Pills

```css
.badge {
  display: inline-flex;
  align-items: center;
  gap: var(--space-1);
  padding: 0.125rem 0.625rem;
  border-radius: var(--radius-full);
  font-size: var(--text-xs);
  font-weight: 600;
  letter-spacing: 0.02em;
  line-height: 1.5;
}

/* Status variants */
.badge--live     { background: #e8e8e8; color: #1a1a1a; }
.badge--pending  { background: #f0f0f0; color: #555; }
.badge--alert    { background: #3a3a3a; color: #fff; }
.badge--accent   { background: var(--accent-light); color: var(--accent); }

/* Size variants */
.badge--sm { font-size: 0.625rem; padding: 0.0625rem 0.5rem; }
.badge--lg { font-size: var(--text-sm); padding: 0.25rem 0.875rem; }
```

#### Buttons

```css
/* Primary */
.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: var(--space-2);
  padding: var(--space-3) var(--space-6);
  font-size: var(--text-sm);
  font-weight: 600;
  border-radius: var(--radius-md);
  cursor: pointer;
  transition: all 0.15s ease;
  border: none;
  line-height: 1;
}

.btn--primary {
  background: var(--accent);
  color: var(--text-on-accent);
}
.btn--primary:hover {
  background: var(--accent-hover);
  box-shadow: var(--shadow-sm);
}

/* Secondary */
.btn--secondary {
  background: var(--surface-elevated);
  color: var(--text-body);
  border: 1px solid var(--border-medium);
}
.btn--secondary:hover {
  background: var(--surface-hover);
  border-color: var(--border-strong);
}

/* Ghost */
.btn--ghost {
  background: transparent;
  color: var(--text-secondary);
}
.btn--ghost:hover {
  background: var(--surface-hover);
  color: var(--text-primary);
}

/* All buttons: focus state */
.btn:focus-visible {
  outline: 2px solid var(--accent);
  outline-offset: 2px;
}

/* Sizes */
.btn--sm { padding: 0.375rem 0.875rem; font-size: var(--text-xs); }
.btn--lg { padding: 0.875rem 2rem; font-size: var(--text-base); }
```

#### Tooltips

See Section 2 pattern. Key specs:
- Background: `--surface-tooltip` (#1A1A1A)
- Text: `--text-on-dark` (#FFFFFF)
- Padding: `0.5rem 0.75rem`
- Radius: `6px`
- Font size: `--text-xs` (13px)
- Max width: 250px
- Arrow: 6px CSS triangle (optional, adds visual polish)
- Trigger: hover and focus-visible

#### Section Headers

```css
.section-header {
  margin-bottom: var(--space-6);
}

.section-header__title {
  font-size: var(--text-xl);
  font-weight: 600;
  color: var(--text-primary);
  margin-bottom: var(--space-2);
}

.section-header__subtitle {
  font-size: var(--text-base);
  color: var(--text-secondary);
  max-width: 65ch; /* Optimal reading width */
}

.section-header__eyebrow {
  font-size: var(--text-xs);
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  color: var(--text-muted);
  margin-bottom: var(--space-2);
}
```

#### Dividers

Prefer spacing and background color shifts over visible lines. When lines are needed:

```css
.divider {
  border: none;
  height: 1px;
  background: var(--border-subtle);
  margin: var(--space-8) 0;
}

.divider--strong {
  background: var(--border-medium);
}
```

#### Navigation Bar

```css
.nav-bar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: var(--space-4) var(--space-8);
  background: var(--bg-page);
  border-bottom: 1px solid var(--border-subtle);
  position: sticky;
  top: 0;
  z-index: 100;
}

.nav-bar__logo {
  font-size: var(--text-lg);
  font-weight: 700;
  color: var(--text-primary);
}

.nav-bar__links {
  display: flex;
  gap: var(--space-8);
  list-style: none;
}

.nav-bar__link {
  font-size: var(--text-sm);
  font-weight: 500;
  color: var(--text-secondary);
  text-decoration: none;
  transition: color 0.15s ease;
}

.nav-bar__link:hover {
  color: var(--text-primary);
}

.nav-bar__link--active {
  color: var(--text-primary);
  font-weight: 600;
}
```

#### Breadcrumbs

```css
.breadcrumbs {
  display: flex;
  align-items: center;
  gap: var(--space-2);
  font-size: var(--text-sm);
  color: var(--text-muted);
}

.breadcrumbs a {
  color: var(--text-secondary);
  text-decoration: none;
  transition: color 0.15s ease;
}

.breadcrumbs a:hover {
  color: var(--accent);
}

.breadcrumbs__separator {
  color: var(--text-disabled);
  font-size: 0.75em;
}

.breadcrumbs__current {
  color: var(--text-primary);
  font-weight: 500;
}
```

#### Placeholder Image Blocks

```css
.placeholder-image {
  background: var(--surface-elevated);
  border-radius: var(--radius-md);
  aspect-ratio: 16/9;
  display: flex;
  align-items: center;
  justify-content: center;
}

.placeholder-image::after {
  content: "";
  width: 2rem;
  height: 2rem;
  background: var(--border-subtle);
  border-radius: var(--radius-sm);
  /* Simple image icon placeholder */
}

/* Size variants */
.placeholder-image--square { aspect-ratio: 1; }
.placeholder-image--wide { aspect-ratio: 21/9; }
.placeholder-image--portrait { aspect-ratio: 3/4; }
```

---

## 4. Modern CSS Techniques Reference

### CSS Grid Subgrid

**Status:** Baseline, all major browsers (2024+)

**Use case:** Aligning content across sibling cards in a grid.

```css
.card-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: subgrid; /* Not here -- on children */
  gap: 1.5rem;
}

.card {
  display: grid;
  grid-template-rows: subgrid;
  grid-row: span 3; /* Spans: title, body, footer */
}
```

Without subgrid, card titles, descriptions, and CTAs cannot align across a row of cards because each card creates its own grid context. With subgrid, the parent grid controls row heights for all children.

### CSS Container Queries

**Status:** Baseline (size queries). Scroll-state queries in Chrome 125+.

```css
.card-wrapper {
  container-type: inline-size;
  container-name: card;
}

@container card (min-width: 400px) {
  .card-content {
    display: flex;
    gap: 1.5rem;
  }
  .card-image {
    flex: 0 0 40%;
  }
}

@container card (max-width: 399px) {
  .card-content {
    display: block;
  }
  .card-image {
    margin-bottom: 1rem;
  }
}
```

Container queries respond to the component's own size, not the viewport. This makes components truly portable -- a card in a sidebar behaves differently than the same card in a main content area without any changes.

### CSS :has() Selector

**Status:** Baseline, most-used and most-loved CSS feature per State of CSS 2025.

```css
/* Style a card differently when it contains an image */
.card:has(img) {
  grid-template-columns: 200px 1fr;
}

/* Style a form group when its input is invalid */
.form-group:has(input:invalid) {
  border-color: var(--status-negative-bg);
}

/* Enable a submit button when all required fields are filled */
form:has(input:required:placeholder-shown) .btn--submit {
  opacity: 0.5;
  pointer-events: none;
}

/* Style table row when it contains a "negative" badge */
tr:has(.badge--negative) {
  background: rgba(0,0,0,0.02);
}
```

### CSS Scroll-Driven Animations

**Status:** ~85% browser support. Use as progressive enhancement.

```css
/* Fade elements in as they enter the viewport */
.animate-on-scroll {
  animation: slide-up linear both;
  animation-timeline: view();
  animation-range: entry 0% entry 40%;
}

@keyframes slide-up {
  from { opacity: 0; transform: translateY(30px); }
  to { opacity: 1; transform: translateY(0); }
}

/* Scroll-linked progress indicator */
.reading-progress {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  height: 3px;
  background: var(--accent);
  transform-origin: left;
  animation: scale-x linear;
  animation-timeline: scroll(root);
}

@keyframes scale-x {
  from { transform: scaleX(0); }
  to { transform: scaleX(1); }
}
```

### View Transitions API

**Status:** Same-document transitions baseline. Cross-document in Chrome 126+.

```css
/* Name elements that should animate between states */
.page-title {
  view-transition-name: page-title;
}

.hero-image {
  view-transition-name: hero;
}

/* Customize the transition animation */
::view-transition-old(page-title) {
  animation: fade-out 0.2s ease;
}

::view-transition-new(page-title) {
  animation: fade-in 0.3s ease;
}
```

For same-page tab switching or content transitions, call `document.startViewTransition()` in JS to trigger CSS-defined animations between states.

### CSS Anchor Positioning

**Status:** Chrome 125+, Edge 125+. Interop 2025 priority (expected cross-browser by end of 2025).

```css
.trigger {
  anchor-name: --my-trigger;
}

.popover-content {
  position: fixed;
  position-anchor: --my-trigger;
  position-area: bottom span-right;
  margin-top: 8px;
  width: max-content;
  max-width: 300px;
}

/* Fallback positioning */
@supports not (anchor-name: --x) {
  .popover-content {
    position: absolute;
    top: 100%;
    left: 0;
  }
}
```

With Chrome 133+, popovers invoked by a button get an implicit anchor reference, so you can skip the `anchor-name` declaration entirely.

### HTML Popover API

**Status:** Baseline in all major browsers.

```html
<button popovertarget="info-panel">Show Details</button>

<div id="info-panel" popover>
  <h3>Details</h3>
  <p>This panel is built with zero JavaScript.</p>
</div>
```

```css
[popover] {
  background: var(--surface-card);
  border: 1px solid var(--border-subtle);
  border-radius: var(--radius-lg);
  padding: var(--space-6);
  box-shadow: var(--shadow-xl);
  max-width: 400px;
}

/* Entry/exit animations */
[popover]:popover-open {
  opacity: 1;
  transform: translateY(0);
}

@starting-style {
  [popover]:popover-open {
    opacity: 0;
    transform: translateY(-8px);
  }
}

[popover] {
  transition: opacity 0.2s ease, transform 0.2s ease,
              display 0.2s ease allow-discrete;
}
```

Key behaviors: auto-dismisses on outside click, only one `popover="auto"` open at a time, works with `<dialog>` for modals, supports `popover="hint"` for tooltip-like behavior (Chrome only currently).

### Native Accordions with `<details>`/`<summary>`

**Status:** Baseline, all browsers. The `name` attribute for exclusive accordions is in Chrome 120+, Firefox 130+, Safari 17.2+.

```html
<!-- Exclusive accordion group: only one open at a time -->
<details name="faq-group">
  <summary>Question One</summary>
  <p>Answer one content.</p>
</details>

<details name="faq-group">
  <summary>Question Two</summary>
  <p>Answer two content.</p>
</details>
```

The `name` attribute groups `<details>` elements so opening one closes the others -- no JavaScript needed. This is the modern replacement for accordion JS libraries.

### CSS Nesting

**Status:** Baseline, all major browsers.

```css
.card {
  background: var(--surface-card);
  border: 1px solid var(--border-subtle);
  border-radius: var(--radius-lg);
  padding: var(--space-6);

  & .card-title {
    font-size: var(--text-lg);
    font-weight: 600;
    margin-bottom: var(--space-2);
  }

  & .card-body {
    color: var(--text-body);
    font-size: var(--text-base);
  }

  &:hover {
    border-color: var(--border-medium);
    box-shadow: var(--shadow-lg);
  }

  @container (max-width: 300px) {
    padding: var(--space-4);

    & .card-title {
      font-size: var(--text-base);
    }
  }
}
```

### @layer for Style Organization

**Status:** Baseline, all major browsers.

```css
/* Define layer order -- first declared = lowest priority */
@layer reset, base, tokens, components, utilities, overrides;

@layer reset {
  *, *::before, *::after { box-sizing: border-box; margin: 0; }
}

@layer tokens {
  :root {
    --bg-page: #FFFFFF;
    --text-primary: #111111;
    /* ... all design tokens ... */
  }
}

@layer base {
  body {
    font-family: 'General Sans', system-ui, sans-serif;
    color: var(--text-body);
    background: var(--bg-page);
    line-height: 1.6;
  }
}

@layer components {
  .card { /* ... */ }
  .btn { /* ... */ }
  .badge { /* ... */ }
}

@layer utilities {
  .text-center { text-align: center; }
  .mt-8 { margin-top: var(--space-8); }
}

@layer overrides {
  /* Page-specific overrides go here */
}
```

Layers provide explicit control over specificity. Styles in later layers always beat earlier layers regardless of selector specificity. This eliminates `!important` wars and makes large stylesheets maintainable.

---

## 5. Complete CSS Custom Properties Block

Copy this into the root stylesheet as the foundation:

```css
:root {
  /* --- Backgrounds --- */
  --bg-page: #FFFFFF;
  --bg-section: #F8F9FA;
  --surface-card: #FFFFFF;
  --surface-elevated: #F2F3F5;
  --surface-alt: #F8F9FA;
  --surface-hover: #ECEDEF;
  --surface-tooltip: #1A1A1A;
  --surface-overlay: rgba(0, 0, 0, 0.5);

  /* --- Text --- */
  --text-primary: #111111;
  --text-body: #333333;
  --text-secondary: #555555;
  --text-muted: #888888;
  --text-disabled: #BBBBBB;
  --text-on-dark: #FFFFFF;
  --text-on-accent: #FFFFFF;

  /* --- Borders --- */
  --border-subtle: #E5E7EB;
  --border-medium: #D1D5DB;
  --border-strong: #9CA3AF;

  /* --- Accent --- */
  --accent: #2563EB;
  --accent-hover: #1D4ED8;
  --accent-light: #EFF6FF;
  --accent-muted: #93C5FD;

  /* --- Status (grayscale) --- */
  --status-positive-bg: #E8E8E8;
  --status-positive-text: #1A1A1A;
  --status-warning-bg: #D4D4D4;
  --status-warning-text: #333333;
  --status-negative-bg: #3A3A3A;
  --status-negative-text: #FFFFFF;

  /* --- Typography --- */
  --font-sans: 'General Sans', system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  --font-mono: 'SF Mono', 'Fira Code', 'Cascadia Code', monospace;

  --text-xs: 0.6875rem;
  --text-sm: 0.8125rem;
  --text-base: 1rem;
  --text-md: 1.125rem;
  --text-lg: 1.25rem;
  --text-xl: 1.5rem;
  --text-2xl: 1.875rem;
  --text-3xl: clamp(1.75rem, 1rem + 2.5vw, 2.25rem);
  --text-4xl: clamp(2rem, 1rem + 3.5vw, 3rem);
  --text-5xl: clamp(2.5rem, 1rem + 5vw, 4rem);

  /* --- Spacing --- */
  --space-1: 0.25rem;
  --space-2: 0.5rem;
  --space-3: 0.75rem;
  --space-4: 1rem;
  --space-5: 1.25rem;
  --space-6: 1.5rem;
  --space-8: 2rem;
  --space-10: 2.5rem;
  --space-12: 3rem;
  --space-16: 4rem;
  --space-20: 5rem;
  --space-24: 6rem;

  /* --- Radius --- */
  --radius-sm: 4px;
  --radius-md: 8px;
  --radius-lg: 12px;
  --radius-xl: 16px;
  --radius-2xl: 24px;
  --radius-full: 9999px;

  /* --- Shadows --- */
  --shadow-sm: 0 1px 2px rgba(0, 0, 0, 0.05);
  --shadow-md: 0 2px 8px rgba(0, 0, 0, 0.08);
  --shadow-lg: 0 4px 16px rgba(0, 0, 0, 0.1);
  --shadow-xl: 0 8px 32px rgba(0, 0, 0, 0.12);

  /* --- Transitions --- */
  --transition-fast: 0.15s ease;
  --transition-base: 0.2s ease;
  --transition-slow: 0.3s ease;
}
```

---

## 6. Implementation Recommendations

### Architecture for a Competitive Research Dashboard

**Recommended page structure:**

```
1. Navigation bar (sticky, minimal)
2. Breadcrumbs
3. Page header (title + description + key metric badges)
4. Tab bar (major sections)
   ├── Tab 1: Executive Summary
   │   ├── Score cards (3-4 across)
   │   ├── Key findings (card grid)
   │   └── Recommendation badges
   ├── Tab 2: Site-by-Site Analysis
   │   ├── Competitor selector (pill bar)
   │   ├── Expandable section panels (details/summary)
   │   └── Comparison matrix
   ├── Tab 3: Feature Comparison
   │   ├── Sticky-header comparison table
   │   └── Category filters (badge toggles)
   └── Tab 4: Recommendations
       ├── Priority cards (high/medium/low)
       └── Implementation roadmap (timeline)
5. Footer
```

### Progressive Enhancement Strategy

1. **HTML first:** Semantic structure with `<details>`, `<summary>`, `<table>`, `<nav>` works without CSS
2. **CSS layer 1:** Layout, typography, colors (works without modern features)
3. **CSS layer 2:** Container queries, :has(), subgrid (enhances but doesn't break)
4. **CSS layer 3:** Scroll animations, view transitions, anchor positioning (visual polish)

### Mobile Strategy

- Below 768px: Cards stack single-column, tables convert to card view
- Tab bar becomes horizontally scrollable
- Comparison tables show 2 columns with swipe indicator
- Accordions default to all-collapsed state
- Score cards reduce from 4-across to 2x2 grid

### Performance Targets

- First Contentful Paint: under 1.2s
- No layout shift (CLS < 0.1)
- All interactions responsive in under 100ms
- Total CSS under 15KB gzipped (achievable with custom properties + minimal utilities)

---

## Sources

- [Dashboard UX Best Practices (DesignRush)](https://www.designrush.com/agency/ui-ux-design/dashboard/trends/dashboard-ux)
- [Dashboard Design Principles (DesignRush)](https://www.designrush.com/agency/ui-ux-design/dashboard/trends/dashboard-design-principles)
- [Dashboard Design Principles (UXPin)](https://www.uxpin.com/studio/blog/dashboard-design-principles/)
- [Dashboard UX Patterns (Pencil & Paper)](https://www.pencilandpaper.io/articles/ux-pattern-analysis-data-dashboards)
- [Progressive Disclosure in Visualization (Dev3lop)](https://dev3lop.com/progressive-disclosure-in-complex-visualization-interfaces/)
- [Progressive Disclosure (IxDF)](https://ixdf.org/literature/topics/progressive-disclosure)
- [Table vs List vs Cards (UX Patterns)](https://uxpatterns.dev/pattern-guide/table-vs-list-vs-cards)
- [Mobile Tables (NN/g)](https://www.nngroup.com/articles/mobile-tables/)
- [CSS-Only Tabs (gwaa.net)](https://gwaa.net/how-do-you-create-css-only-tabs)
- [Accessible CSS Tabs (dfkaye)](https://dfkaye.com/posts/2020/08/23/accessible-css-driven-tabs-without-javascript/)
- [ARIA Tab Role (MDN)](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles/tab_role)
- [Sticky Header Tables (Envato Tuts+)](https://webdesign.tutsplus.com/a-quick-css-only-approach-for-creating-responsive-sticky-tables--cms-106864t)
- [Sticky Header + Sticky Column (CSS-Tricks)](https://css-tricks.com/a-table-with-both-a-sticky-header-and-a-sticky-first-column/)
- [State of CSS 2026 (CoderCops)](https://www.codercops.com/blog/state-of-css-2026)
- [2026 CSS Features (Riad Kilani)](https://blog.riadkilani.com/2026-css-features-you-must-know/)
- [Container Queries 2026 (LogRocket)](https://blog.logrocket.com/container-queries-2026/)
- [Modern CSS Toolkit 2026 (Nick Paolini)](https://www.nickpaolini.com/blog/modern-css-toolkit-2026)
- [CSS Anchor Positioning Guide (DevToolbox)](https://devtoolbox.dedyn.io/blog/css-anchor-positioning-guide)
- [Popover API (MDN)](https://developer.mozilla.org/en-US/docs/Web/API/Popover_API/Using)
- [View Transitions 2025 (Chrome Developers)](https://developer.chrome.com/blog/view-transitions-in-2025)
- [State of CSS 2025 Features](https://2025.stateofcss.com/en-US/features/)
- [CSS Bar Charts (CSS-Tricks)](https://css-tricks.com/css-bar-charts-using-modern-functions/)
- [Charts.css](https://chartscss.org/)
- [Best Free Fonts 2026 (Untitled UI)](https://www.untitledui.com/blog/best-free-fonts)
- [Top Fonts 2026 (Creative Boom)](https://www.creativeboom.com/resources/top-50-fonts-in-2026/)
- [Modular Type Scales (Utopia)](https://utopia.fyi/blog/css-modular-scales/)
- [Typography Scale (ModularScale.com)](https://www.modularscale.com/)
- [Design Tokens Guide (Penpot)](https://penpot.app/blog/the-developers-guide-to-design-tokens-and-css-variables/)
- [Grayscale Design (Tailwind palette generator)](https://grayscale.design/)
