# Colors

ClearThink Web-Design color system. Two layers — primitives (raw values) and semantics (named tokens components reference). Components reference the semantic layer only.

This file is the working example for the Token file structure (§7.6 of `Web-Design_Design-System_Round-1_Resolutions.md`). Refinements made here propagate to `typography.md`, `spacing.md`, `radii.md`, and `shadows.md`.

---

## 1. Philosophy

Color is the most-overridden design token in marketing sites — every client has brand colors, and the design system has to consume them without breaking. Three principles drive the schema:

**Two layers, one direction of reference.** Primitives are raw values (hex codes). Semantic tokens are named slots (`--color-bg-primary`, `--color-text-muted`). Components reference semantic tokens — never primitives. The override mechanism swaps primitive values; semantics stay constant; components don't notice.

**Roles, not colors.** Brand primitives are named by role (`--brand-primary`, `--brand-accent`), not by hue. When a client overrides `--brand-primary` from green to navy, the token name still reads correctly — the meaning travels with the role. ClearThink's brand identity (GREEN / BRIGHT / DARK / CREAM) lives in `Brand/guidelines.md`; the design system consumes those values into role-based slots.

**Marketing scope, not product UI.** A marketing site has roughly five interaction states (default, hover, pressed, focus, disabled), one primary action, one optional accent. Building Figma-FPL-depth color semantics for marketing produces dead tokens. The schema covers what marketing sites actually use: surface, text, border, status — sized to be capture-able in a single brand-discovery conversation.

---

## 2. Primitive scale

Raw values. Components never reference these directly.

### Brand (sourced from `Brand/guidelines.md`)

| Token | Default value | Source |
|---|---|---|
| `--brand-primary` | `#1B9B5E` | ClearThink GREEN |
| `--brand-accent` | `#3BEB96` | ClearThink BRIGHT |

DARK and CREAM are no longer in the brand namespace — they anchor the neutral ramp below as `--neutral-950` and `--neutral-50`. They're still ClearThink's identity colors per `Brand/guidelines.md`; the design system just consumes them as ramp endpoints.

### Neutral ramp — Tailwind stone, anchored at DARK and CREAM

Warm-gray, perceptually uniform via OKLCH, WCAG-tested. Anchors preserve ClearThink's identity values; interior stops come from Tailwind's stone palette.

| Token | Hex | Source |
|---|---|---|
| `--neutral-950` | `#121718` | DARK (ClearThink anchor) |
| `--neutral-900` | `#1C1917` | stone-900 |
| `--neutral-800` | `#292524` | stone-800 |
| `--neutral-700` | `#44403C` | stone-700 |
| `--neutral-600` | `#57534E` | stone-600 |
| `--neutral-500` | `#78716C` | stone-500 |
| `--neutral-400` | `#A8A29E` | stone-400 |
| `--neutral-300` | `#D6D3D1` | stone-300 |
| `--neutral-200` | `#E7E5E4` | stone-200 |
| `--neutral-100` | `#F5F5F4` | stone-100 |
| `--neutral-50` | `#F6F3EF` | CREAM (ClearThink anchor) |

### Channel-form variant (for shadow alpha-modulation)

For use inside `rgb(R G B / alpha)` syntax — needed by shadow primitives in `shadows.md` that flex alpha via `var(--shadow-depth)`. Modern CSS Color Level 4 syntax can't slice the existing hex value at runtime, so the channel-separated form exists as a parallel primitive.

| Token | Value |
|---|---|
| `--neutral-950-rgb` | `18 23 24` |

**Bounded to `--neutral-950` only.** Other neutrals don't get parallel RGB forms ad-hoc — only `--neutral-950` is consumed inside `rgb()` for shadow color (per the shadow color decision in `shadows.md`). If a future token type needs a different anchor inside `rgb()`, that's a deliberate decision, not a pattern to replicate.

### Status — paired bg + text per status

Light bg / deep text pairs (Tailwind 100 / 800 convention). All pairs pass WCAG AA on cream and on each other. Borders use the deep text tone, not the bg tone.

| Status | `--status-{name}-bg` | `--status-{name}-text` |
|---|---|---|
| success | `#DCFCE7` | `#166534` |
| warning | `#FEF3C7` | `#854D0E` |
| danger | `#FEE2E2` | `#991B1B` |
| info | `#DBEAFE` | `#1E40AF` |

### Runtime-computed values (CSS only, not in JSON)

Hover and pressed shades are not stored as primitives. The build pipeline writes them into `:root` as `color-mix()` declarations, so they survive arbitrary client primary colors (yellow, pastel, magenta) without re-tuning by hand:

```css
:root {
  --brand-primary: #1B9B5E;
  --brand-primary-hover:   color-mix(in oklch, var(--brand-primary), var(--neutral-950) 10%);
  --brand-primary-pressed: color-mix(in oklch, var(--brand-primary), var(--neutral-950) 20%);
  --brand-accent-hover:    color-mix(in oklch, var(--brand-accent), var(--neutral-950) 10%);
}
```

`color-mix()` has full modern-browser support since 2023. The semantic layer references these as if they were primitives.

**Total stored primitives: 22** (2 brand + 11 neutral + 1 channel-form variant + 8 status). Plus 3 runtime-computed values.

---

## 3. Semantic layer

Named slots. Components reference these. Override mechanism swaps which primitive each slot points to.

### Surface (background) — 8 tokens

| Semantic token | Default → primitive | Use |
|---|---|---|
| `--color-bg-page` | `--neutral-50` | Page background |
| `--color-bg-surface` | `--neutral-50` | Card, modal, panel background |
| `--color-bg-surface-muted` | `--neutral-100` | Secondary card, alt section background |
| `--color-bg-primary` | `--brand-primary` | Primary buttons, key accents |
| `--color-bg-primary-hover` | `--brand-primary-hover` (computed) | Primary button hover |
| `--color-bg-inverse` | `--neutral-950` | Dark sections, inverse cards |
| `--color-bg-accent` | `--neutral-100` (no override) → `--brand-accent` (with override) | Highlight blocks. Falls back to a soft neutral so accent regions stay visible without a client accent. |
| `--color-bg-accent-hover` | `--neutral-200` (no override) → `--brand-accent-hover` (computed, with override) | Accent hover |

### Text — 9 tokens

| Semantic token | Default → primitive | Use |
|---|---|---|
| `--color-text` | `--neutral-700` | Default body text on light surfaces |
| `--color-text-strong` | `--neutral-800` | Headlines, emphasized text |
| `--color-text-muted` | `--neutral-600` | Secondary text |
| `--color-text-subtle` | `--neutral-500` | Captions, hint text, metadata |
| `--color-text-on-primary` | `--neutral-50` | Text on `--brand-primary` surfaces |
| `--color-text-on-inverse` | `--neutral-50` | Text on `--neutral-950` surfaces |
| `--color-text-on-accent` | `--neutral-700` | Text on accent surfaces (no override) or accent override |
| `--color-text-link` | `--brand-primary` | Inline links |
| `--color-text-link-hover` | `--brand-primary-hover` (computed) | Link hover |

### Border — 3 tokens

| Semantic token | Default → primitive | Use |
|---|---|---|
| `--color-border` | `--neutral-200` | Default borders, dividers |
| `--color-border-strong` | `--neutral-300` | Emphasized borders, input outlines |
| `--color-border-focus` | `--brand-primary` | Focus ring |

### Status — 12 tokens

For each of `success`, `warning`, `danger`, `info`:

| Semantic token | Maps to |
|---|---|
| `--color-bg-{status}` | `--status-{status}-bg` |
| `--color-text-{status}` | `--status-{status}-text` |
| `--color-border-{status}` | `--status-{status}-text` (border uses the deep tone, not the bg tone) |

**Total: 32 semantic tokens** (8 surface + 9 text + 3 border + 12 status). Slightly over the ~25–30 target; `--color-text-strong` retained per review (AEC-Commercial sites lean heavy-headline).

---

## 4. Override surface

Which primitives a client can override. The override mechanism (per resolved §7.2 / §7.3) swaps primitive *values*; semantic slots never change.

### Always overridable

- `--brand-primary` → client primary brand color. Hover and pressed shades recompute at runtime via `color-mix()`.

### Conditionally overridable

- `--brand-accent` → client accent. **If absent, accent semantic tokens fall back to neutrals** (`--neutral-100` for bg, `--neutral-200` for hover) so accent regions still have visible presence.

### Anchors — rarely overridden

- `--neutral-950` and `--neutral-50` (DARK and CREAM equivalents). Technically swap-able for clients with strong custom dark/light surface colors, but most clients keep ClearThink defaults. Interior neutral stops are not individually overridable — the ramp comes as a unit.

### Never overridable

- Status colors (success / warning / danger / info) — keep meaning consistent across clients. A red "danger" state isn't a brand decision.

---

## 5. Decision tree — picking the right token

When writing a component, walk the tree in order:

```
Is this color carrying meaning (status)?
├─ Yes → use --color-{bg|text|border}-{status}
└─ No → continue

Is it a brand-primary action or surface?
├─ Yes → --color-bg-primary + --color-text-on-primary
└─ No → continue

What role does this color serve?
├─ Text → text token tree
│         (text / text-strong / text-muted / text-subtle / text-on-primary /
│          text-on-inverse / text-on-accent / text-link / text-link-hover)
├─ Surface → surface token tree
│         (bg-page / bg-surface / bg-surface-muted / bg-inverse /
│          bg-accent / bg-accent-hover)
└─ Border → border token tree
          (border / border-strong / border-focus)
```

---

## 6. Examples used together

### Primary CTA on cream page

```html
<button class="bg-[var(--color-bg-primary)] text-[var(--color-text-on-primary)] hover:bg-[var(--color-bg-primary-hover)]">
  Schedule a call
</button>
```

### Card with body and metadata

```html
<article class="bg-[var(--color-bg-surface)] border border-[var(--color-border)] p-6">
  <h3 class="text-[var(--color-text-strong)]">ClearLaunch</h3>
  <p class="text-[var(--color-text)]">8-week GTM strategy sprint.</p>
  <span class="text-[var(--color-text-subtle)]">$1,200 flat</span>
</article>
```

### Inverse section (dark)

```html
<section class="bg-[var(--color-bg-inverse)] text-[var(--color-text-on-inverse)]">
  <h2>What it costs to skip strategy</h2>
</section>
```

### Status banner (success)

```html
<div class="bg-[var(--color-bg-success)] border border-[var(--color-border-success)] text-[var(--color-text-success)] px-4 py-3">
  Your form was submitted.
</div>
```

---

## 7. ❌ Common mistakes

**Referencing a primitive directly in a component.**
```html
<!-- ❌ Breaks the override mechanism -->
<button class="bg-[#1B9B5E]">

<!-- ✅ -->
<button class="bg-[var(--color-bg-primary)]">
```

**Using a Tailwind utility for what should be a semantic token.**
```html
<!-- ❌ Won't respond to client overrides -->
<p class="text-stone-700">

<!-- ✅ -->
<p class="text-[var(--color-text)]">
```

**Putting brand colors into status tokens.**
```html
<!-- ❌ A primary-colored "danger" state confuses meaning -->
--color-bg-danger: var(--brand-primary);

<!-- ✅ -->
--color-bg-danger: var(--status-danger-bg);
```

**Inventing a new semantic token in a component file.**
If you reach for a color that doesn't exist in the semantic layer, the answer is to add it here in `colors.md` (with rationale), not to one-off it in the component. The whole point of the schema is constraint.

**Pure white or pure black anywhere.**
Per `Brand/guidelines.md`: surfaces use CREAM (= `--neutral-50`), text uses DARK (= `--neutral-950`) or a neutral. `#FFFFFF` and `#000000` are banned at every layer.
