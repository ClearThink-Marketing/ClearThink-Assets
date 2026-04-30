# Spacing

ClearThink Web-Design spacing system. Two layers — primitives (Tailwind's 4px scale, used directly via utilities) and a small semantic layer of system-level rhythm tokens (section padding, page gutters, stack gaps, inline gaps).

Follows the §7.6 Token file structure (Philosophy → Primitive scale → Semantic layer → Override surface → Decision tree → Examples → Common mistakes), adapted for **dimensional** rather than role-based decisions.

---

## 1. Philosophy

Type creates voice; **spacing creates pacing**. A page with consistent rhythm reads coherent. A page with inconsistent rhythm reads anxious. Three principles drive the schema:

**Tokens for system rhythm, primitives for component internals.** Section padding, page gutters, stack gaps, and inline gaps are system-level decisions — they govern how the page breathes across sections, components, and viewports. Component-internal spacing (the padding inside a button, the gap between a card's title and body) is a component-level decision. Reach for Tailwind utilities (`p-3`, `gap-2`, `mt-4`) directly when you're spacing inside a component. The semantic layer stays small (7 tokens) on purpose.

**The scale is Tailwind's.** Primitives mirror Tailwind's 4px-based scale verbatim — no parallel naming, no custom multiples. AI tools (Claude Design, Figma Make) recognize the scale natively, and any web developer reading the system already knows it. Adding a custom primitive layer for spacing would create translation friction with no upside.

**Density is the override surface, scoped per file.** Brand identity lives in the rhythm — clients don't reach in and override individual gap values. They override one **density multiplier** (default / comfortable / compact) that scales the content-rhythm tokens uniformly. The variable is scoped to this file (`--space-density`, `data-space-density`) so future "feel" tokens (`radii.md`, etc.) can introduce their own multipliers without collision.

---

## 2. Primitive scale

**Tailwind's 4px-based spacing scale, used directly.** Base unit is 4px (0.25rem). Each step is one base unit; common stops follow Tailwind's defaults.

| Tailwind utility | rem | px | Common use |
|---|---|---|---|
| `p-1` / `gap-1` | 0.25 | 4 | Hairline gaps |
| `p-2` / `gap-2` | 0.5 | 8 | Tight inline gaps, label-to-input |
| `p-3` / `gap-3` | 0.75 | 12 | Default inline gaps, button padding |
| `p-4` / `gap-4` | 1 | 16 | Default content padding |
| `p-6` / `gap-6` | 1.5 | 24 | Default vertical stack gap |
| `p-8` / `gap-8` | 2 | 32 | Card body padding, section internal |
| `p-12` / `gap-12` | 3 | 48 | Large stack gap |
| `p-16` / `gap-16` | 4 | 64 | Section block separator |
| `p-24` / `gap-24` | 6 | 96 | Section vertical padding (medium) |
| `p-32` / `gap-32` | 8 | 128 | Section vertical padding (large) |

The full Tailwind scale is available — these are the stops you'll actually use. If you reach for a value not on the scale (15px, 22px, 35px), the design is wrong, not the scale.

No custom CSS variables for primitives. The semantic layer references Tailwind's `--spacing` calc base (`calc(<n> * var(--spacing))`) where needed.

---

## 3. Semantic layer

Seven tokens. System-level rhythm only. Static tokens multiply by `--space-density` (see §4); fluid tokens do not — see the explicit note in §4 for why.

### Section rhythm — 2 tokens (fluid, NOT density-multiplied)

| Token | Value | Use |
|---|---|---|
| `--space-section-y` | `clamp(3rem, 6vw + 1rem, 8rem)` | Vertical padding inside a section (top + bottom). Fluid, 48–128 px. Compresses on small screens without breakpoint hops. |
| `--space-container-x` | `clamp(1rem, 4vw, 4rem)` | Horizontal padding on the max-width container. Fluid, 16–64 px. Keeps content off the viewport edge. |

### Stack gaps (vertical) — 3 tokens (density-multiplied)

| Token | Value | Use |
|---|---|---|
| `--space-stack-lg` | `calc(3rem * var(--space-density))` | 48 px before density. Between cards in a grid; between distinct content blocks within a section. |
| `--space-stack` | `calc(1.5rem * var(--space-density))` | 24 px before density. Default stack rhythm — between paragraphs, list items, headline-to-body. |
| `--space-stack-sm` | `calc(0.5rem * var(--space-density))` | 8 px before density. Tight stack — label-to-input, headline-to-eyebrow, caption-to-image. |

### Inline gaps (horizontal) — 2 tokens (density-multiplied)

| Token | Value | Use |
|---|---|---|
| `--space-inline` | `calc(0.75rem * var(--space-density))` | 12 px before density. Default horizontal gap — button group items, icon-plus-label inside a button, nav items. |
| `--space-inline-sm` | `calc(0.5rem * var(--space-density))` | 8 px before density. Tight horizontal gap — icon hugging text in a tight pill or chip. |

`--space-inline-sm` and `--space-stack-sm` share the same numeric value (8 px). That's intentional — they serve different axes (horizontal vs. vertical) and at the same value they read differently due to typographic weighting on each axis.

**Total: 7 semantic tokens.** Section padding (1) + container padding (1) + stack gaps (3) + inline gaps (2). Two axes × two scales = four naming roots: `space-section-y` / `space-container-x` / `space-stack-*` / `space-inline-*`.

### What's deliberately NOT a semantic token

Component-internal spacing — the padding inside a button, the gap between a card's title and body, the spacing between an input's edge and its placeholder text — uses Tailwind utilities directly. Those decisions belong to the component, not the system. The semantic layer governs **how components and sections relate to each other**, not how they're built internally.

If a component needs unusual internal rhythm, it lives in the component file (e.g., `Core/Components/button.md`), not here.

---

## 4. Override surface

Spacing's override surface is intentionally thin. Brand identity is encoded in the rhythm; per-client value tweaks would dissolve that identity. One override exists.

### Density (the multiplier)

A single CSS variable controls the multiplier applied to the **content-rhythm tokens** (stack and inline gaps). Default is `1` (ClearThink's standard rhythm). Two named alternates:

```css
:root                                { --space-density: 1; }      /* default — ClearThink standard */
[data-space-density="comfortable"]   { --space-density: 1.25; }   /* +25% breathing room */
[data-space-density="compact"]       { --space-density: 0.85; }   /* −15% tighter */
```

Set on `<html>` for site-wide override, or on a single `<section>` for scoped override:

```html
<!-- Site-wide -->
<html data-space-density="comfortable">

<!-- Just this section -->
<section data-space-density="compact">
```

Use cases:
- **Comfortable** — verbose, content-heavy clients (long-form services, in-depth case studies). Extra breathing room makes dense copy more digestible.
- **Compact** — info-dense pages (data tables, dashboards inside marketing sites, technical specs — mechanical schedules, finish specs, project deliverables lists for AEC-Commercial). Tighter rhythm fits more on-screen.
- **Default** — every other client.

### Density does NOT apply to fluid tokens

`--space-section-y` and `--space-container-x` use `clamp()` formulas pre-tuned for the responsive curve. Multiplying those by density would distort the section-padding ceiling on desktop (160px is excessive even for verbose content) and break the small-screen floor (sections lose their "this is a new chapter" effect below ~48px). **Density affects content rhythm (stacks, inline gaps), not page architecture (section padding, container padding).**

### What's not overridable

- Individual semantic tokens (`--space-section-y`, `--space-stack`, etc.) — clients don't reach in. Density flexes the content-rhythm layer.
- The 4px primitive base — it's Tailwind's, and changing it breaks every utility class.
- Stack and inline gap *ratios* to each other — they tune the system's internal coherence.

### Override cascade

A density override on `<html>` cascades to every density-multiplied semantic token automatically through CSS variable inheritance. A scoped override on a section overrides only within that section's subtree. No build-pipeline regeneration required — the override propagates through the cascade.

### Scoped naming pattern (architectural precedent)

`--space-density` and `data-space-density` are deliberately scoped to this file. `radii.md` will follow the same pattern with `--radius-density` and `data-radius-density="sharp"` / `"soft"`. Future "feel" files do the same. Each multiplier is self-documenting and prevents collision when multiple `data-*-density` attributes coexist on `<html>` or `<section>`.

---

## 5. Decision tree — picking the right approach

Spacing decisions are dimensional, not role-based. Walk these questions in order:

```
Is this padding INSIDE a single component (button, card body, input)?
├─ Yes → use Tailwind utility directly (p-3, p-4, p-6, gap-2, etc.)
│        Don't reach for a semantic token.
└─ No → continue

Where does the spacing sit dimensionally?

  Vertical between sections?
  ├─ Yes → padding-block on the section element → --space-section-y
  └─ No → continue

  Horizontal page edge to content?
  ├─ Yes → padding-inline on the max-width container → --space-container-x
  └─ No → continue

  Vertical stack within a content block?
  ├─ Between distinct blocks (cards, large groups) → --space-stack-lg
  ├─ Between paragraphs / list items / headline-to-body → --space-stack
  └─ Tight (label-to-input, eyebrow-to-headline) → --space-stack-sm

  Horizontal inline (flex/grid row)?
  ├─ Default (button groups, nav items, icon + label) → --space-inline
  └─ Tight (icon hugging text in a pill/chip) → --space-inline-sm
```

---

## 6. Examples used together

Spacing is invisible until shown in layout. These examples demonstrate breathing patterns — section-to-section rhythm, card-internal rhythm, form-field rhythm — not individual values.

### Section-to-section rhythm (page-level)

```html
<main>
  <section class="py-[var(--space-section-y)]">
    <div class="mx-auto max-w-screen-xl px-[var(--space-container-x)]">
      <h1 class="text-display text-[var(--color-text-strong)]">A clear plan for growth.</h1>
      <p class="text-body-lg text-[var(--color-text-muted)] mt-[var(--space-stack)] max-w-prose">
        8-week sprint that gives you the strategy before you spend on execution.
      </p>
    </div>
  </section>

  <section class="py-[var(--space-section-y)] bg-[var(--color-bg-surface-muted)]">
    <div class="mx-auto max-w-screen-xl px-[var(--space-container-x)]">
      <p class="text-overline text-[var(--color-text-link)]">Services</p>
      <h2 class="text-h2 text-[var(--color-text-strong)] mt-[var(--space-stack-sm)]">Three ways we work.</h2>
      <div class="grid grid-cols-3 gap-[var(--space-stack-lg)] mt-[var(--space-stack-lg)]">
        <!-- service cards -->
      </div>
    </div>
  </section>
</main>
```

Same `--space-section-y` on every section keeps the page reading coherent. Same container padding on every container keeps the horizontal frame steady.

### Card-internal rhythm

```html
<article class="bg-[var(--color-bg-surface)] border border-[var(--color-border)] p-8">
  <p class="text-overline text-[var(--color-text-link)]">Sprint</p>
  <h3 class="text-h3 text-[var(--color-text-strong)] mt-[var(--space-stack-sm)]">ClearLaunch</h3>
  <p class="text-body text-[var(--color-text)] mt-[var(--space-stack)]">
    8-week GTM strategy sprint that gives small business owners a clear plan before they spend.
  </p>
  <span class="text-caption text-[var(--color-text-subtle)] mt-[var(--space-stack)] block">
    $1,200 flat
  </span>
</article>
```

`p-8` is component-internal padding (Tailwind utility, not semantic). The vertical rhythm between elements inside the card uses semantic stack tokens — same rhythm rules as sections.

### Form-field rhythm

```html
<form class="flex flex-col gap-[var(--space-stack)]">
  <div class="flex flex-col gap-[var(--space-stack-sm)]">
    <label class="text-label text-[var(--color-text)]">Name</label>
    <input class="text-body text-[var(--color-text)] border border-[var(--color-border-strong)] px-3 py-2" />
    <p class="text-caption text-[var(--color-text-subtle)]">
      How should we address you in the proposal?
    </p>
  </div>

  <div class="flex flex-col gap-[var(--space-stack-sm)]">
    <label class="text-label text-[var(--color-text)]">Email</label>
    <input class="text-body text-[var(--color-text)] border border-[var(--color-border-strong)] px-3 py-2" />
  </div>

  <button class="text-button bg-[var(--color-bg-primary)] text-[var(--color-text-on-primary)] px-5 py-3 mt-[var(--space-stack-sm)]">
    Schedule a call
  </button>
</form>
```

Stack-sm binds label / input / helper-text into a single field unit. Stack-default separates field units from each other. Different rhythm tiers, same vocabulary.

### Density override (scoped)

```html
<!-- Default density on the rest of the site -->
<section class="py-[var(--space-section-y)]">
  <!-- standard ClearThink rhythm -->
</section>

<!-- Compact section for an info-dense table -->
<section class="py-[var(--space-section-y)]" data-space-density="compact">
  <!-- 85% spacing on stacks and inline gaps; section-y unchanged (fluid) -->
</section>
```

A single attribute on the section's root element flexes the content-rhythm tokens (stacks and inline gaps) inside. Section padding and container padding remain on their fluid curves regardless of density — page architecture stays intact.

---

## 7. ❌ Common mistakes

**Inventing off-scale values.**
```html
<!-- ❌ 22px isn't on the 4px scale -->
<div class="mt-[22px]">

<!-- ✅ Pick the nearest stop -->
<div class="mt-5">  <!-- 20px -->
<!-- or -->
<div class="mt-6">  <!-- 24px -->
```

If a design specifies an off-scale value, push back on the design before adding a one-off utility. The scale is the system.

**Inconsistent rhythm within a section.**
```html
<!-- ❌ Three different gap rhythms inside one section — reads anxious -->
<section class="py-24">
  <h2>Services</h2>
  <p class="mt-3">Intro copy</p>
  <div class="grid gap-7 mt-9">
    <Card />
  </div>
</section>

<!-- ✅ One stack rhythm tier per visual relationship -->
<section class="py-[var(--space-section-y)]">
  <h2>Services</h2>
  <p class="mt-[var(--space-stack)]">Intro copy</p>
  <div class="grid gap-[var(--space-stack-lg)] mt-[var(--space-stack-lg)]">
    <Card />
  </div>
</section>
```

**Hardcoded margins on reusable components.**
```html
<!-- ❌ Card commits to a margin its parent might not want -->
<article class="mt-8 p-8">
  <h3>...</h3>
</article>

<!-- ✅ Card has internal padding only; spacing between cards belongs to the parent -->
<article class="p-8">
  <h3>...</h3>
</article>

<!-- Parent owns the gap -->
<div class="grid gap-[var(--space-stack-lg)]">
  <Card />
  <Card />
</div>
```

A component is responsible for its **internals**, not its relationship to siblings. The parent layout owns gaps between children.

**Padding/margin confusion — using one for the other's job.**
- **Padding** = spacing *inside* an element's border (between its border and its content). Use for component-internals.
- **Margin** = spacing *outside* an element (between it and its neighbors). Use for stack/inline gaps.
- **`gap` (flex / grid)** = spacing between flex/grid items. Prefer over margins on children when the parent is a flex/grid container.

```html
<!-- ❌ Margin on the child to space it from siblings — works but fragile -->
<div>
  <Card class="mb-12" />
  <Card class="mb-12" />
  <Card />  <!-- last child shouldn't have margin -->
</div>

<!-- ✅ Gap on the flex/grid parent — consistent, no last-child carve-outs -->
<div class="grid gap-[var(--space-stack-lg)]">
  <Card />
  <Card />
  <Card />
</div>
```

**Asymmetric section padding.**
```html
<!-- ❌ Different top and bottom — visual "tilt" between sections -->
<section class="pt-32 pb-16">

<!-- ✅ Symmetric vertical padding — same rhythm above and below -->
<section class="py-[var(--space-section-y)]">
```

Asymmetry occasionally serves a design (a hero with extra top space to clear the nav), but it should be a deliberate exception, not the default. Symmetric `py` keeps the page rhythm steady.
