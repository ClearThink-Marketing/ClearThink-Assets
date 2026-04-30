# Radii

ClearThink Web-Design corner-radius system. Two layers — primitives (5 stops via Tailwind utilities, theme-configured) and a small semantic layer of role-based tokens (default surfaces, controls, pills).

Follows the §7.6 Token file structure (Philosophy → Primitive scale → Semantic layer → Override surface → Decision tree → Examples → Common mistakes), adapted for dimensional tokens. Mirrors `spacing.md`'s scoped-density pattern.

---

## 1. Philosophy

Corner radius is a **feel** decision more than a layout one. Sharp corners read traditional, architectural, institutional. Soft corners read friendly, approachable, modern. Three principles drive the schema:

**Three semantic tokens cover marketing-site needs.** Default (surfaces — cards, modals, panels), control (interactive elements — buttons, inputs, selects), and pill (fully rounded — toggles, tags-as-pills). Splitting control into separate button and input tokens is a trap: buttons and inputs should always share the same radius for visual coherence. One token, one decision.

**The primitive scale is bumped one stop.** Tailwind's default radii (`rounded-sm` 2px, `rounded-md` 6px) sit too tight for AEC-Commercial render scale. 2px reads accidental, 6px reads timid. ClearThink's primitives are 4px / 8px / 12px — same 5-stop shape, scaled up.

**Density is the override surface, scoped per file.** A single `--radius-density` multiplier flexes the whole semantic layer: sharp (0.5×) for traditional/heritage clients, default (1×) for ClearThink standard, soft (1.5×) for friendly/approachable brands. Same scoped-naming pattern as `spacing.md` — the variable is `--radius-density`, the attribute is `data-radius-density`. Multiple "feel" multipliers compose without collision.

---

## 2. Primitive scale

Five stops, configured via Tailwind theme override. Tailwind's default radii are bumped one stop up across the board so corner shapes read deliberate at the sizes AEC-Commercial marketing components actually use.

| Tailwind utility | ClearThink px | Tailwind default | Notes |
|---|---|---|---|
| `rounded-none` | 0 | 0 | Hard corners — heritage / institutional contexts |
| `rounded-sm` | 4 | 2 | Controls — buttons, inputs, selects |
| `rounded-md` | 8 | 6 | Surfaces — cards, modals, panels |
| `rounded-lg` | 12 | 8 | Larger surfaces — feature blocks, hero containers |
| `rounded-full` | 9999 | 9999 | Pills — toggles, tags, circular avatars |

`xl` / `2xl` / `3xl` deliberately omitted. Marketing components rarely need radii above 12px; when they do (a one-off feature card with deliberate softness), use arbitrary values (`rounded-[16px]`) sparingly rather than expanding the scale.

The theme override is part of the design system's Tailwind config; consumers don't see "Tailwind defaults" — they see ClearThink's values when they use `rounded-md`.

---

## 3. Semantic layer

Three tokens. Each maps a role to a primitive value, with density applied (except pill).

| Token | Value | Use |
|---|---|---|
| `--radius-default` | `calc(0.5rem * var(--radius-density))` | 8 px before density. **Surfaces** — cards, modals, panels, image containers, alert boxes. |
| `--radius-control` | `calc(0.25rem * var(--radius-density))` | 4 px before density. **Interactive controls** — buttons, inputs, selects, badges, chips. Buttons and inputs always match. |
| `--radius-pill` | `9999px` | **Pills** — toggles, tags-as-pills, status indicators, segmented controls. |

`--radius-pill` resolves to 9999px regardless of density — multiplying a value already at "infinity" by 0.5 or 1.5 still reads as a pill at any element size. Don't bother density-scaling something already saturated.

**Total: 3 semantic tokens.** That's it. No `--radius-button` separate from `--radius-input`, no `--radius-card` separate from `--radius-modal`. Coherence is the point.

### What's deliberately NOT a semantic token

- **Image-specific radii** — handled by the component (`Core/Components/image.md` once it exists). If a component needs a non-standard radius, the decision lives there, not here.
- **Hover / pressed radii changes** — controls don't change radius on interaction. That's a state animation pattern, not a token decision.
- **Asymmetric radii** (`rounded-tl-lg`, etc.) — Tailwind utilities handle these directly when needed. No semantic token wraps them.

---

## 4. Override surface

Radii's override surface is intentionally thin. One override exists.

### Density (the multiplier)

A single CSS variable controls the multiplier applied to the **density-aware semantic tokens** (default and control). Default is `1`. Two named alternates:

```css
:root                                 { --radius-density: 1; }      /* default — ClearThink standard */
[data-radius-density="sharp"]         { --radius-density: 0.5; }    /* 50% — traditional / heritage */
[data-radius-density="soft"]          { --radius-density: 1.5; }    /* 150% — friendly / approachable */
```

Set on `<html>` for site-wide override, or on a single `<section>` for scoped override:

```html
<!-- Site-wide -->
<html data-radius-density="sharp">

<!-- Just this section -->
<section data-radius-density="soft">
```

### Use cases (AEC-Commercial framing)

- **Default** — most AEC-Commercial clients. General contractors, design-build firms, mainstream commercial AEC practices. ClearThink's standard feel.
- **Sharp** — traditional / heritage clients. Multi-generation general contractors with legacy positioning, classical architecture practices, restoration specialists, custom builders trading on craftsmanship-since-19xx. The hard corners signal continuity and substance.
- **Soft** — friendly / approachable clients. Custom residential builders pivoting toward homeowner relationships, design-forward studios, AEC firms with modern-warm brand voices. The softer corners signal accessibility without going full-tech-startup.

Default is the safe call when in doubt — neither sharp nor soft has a runaway aesthetic.

### Pill stays pill

`--radius-pill` is exempt from density. A pill at sharp density is still a pill; a pill at soft density is still a pill. Density affects feel where there's a meaningful range of corner shapes; a fully-rounded element has no range to flex.

### What's not overridable

- Individual semantic tokens (`--radius-default`, `--radius-control`) — clients don't reach in. Density flexes the whole content layer.
- The 5-stop primitive scale — clients don't redefine `rounded-md` to mean 16px.
- The mapping from semantic to primitive — clients don't reroute `--radius-default` to something other than 8px-base.

### Override cascade

A density override on `<html>` cascades to every density-aware semantic token automatically through CSS variable inheritance. A scoped override on a section overrides only within that section's subtree. No build-pipeline regeneration required.

### Scoped naming pattern

`--radius-density` and `data-radius-density` are scoped to this file, mirroring `spacing.md`'s `--space-density` / `data-space-density` pattern. Future "feel" files do the same. A single page can carry both `data-space-density="comfortable"` and `data-radius-density="soft"` without collision — the multipliers are independent.

---

## 5. Decision tree — picking the right token

Three branches, no nesting:

```
Is this an interactive control (button, input, select, badge, chip)?
├─ Yes → --radius-control
└─ No → continue

Is this a pill / fully-rounded element (toggle, tag-as-pill, status pip)?
├─ Yes → --radius-pill
└─ No → --radius-default
```

If you reach for a radius that isn't on this list, you're either reinventing the system or the component genuinely needs a one-off — in which case use `rounded-[<value>]` sparingly and document why in the component file.

---

## 6. Examples used together

### Same component, three densities

The clearest way to feel the system is to see one component across all three density modes. Same button, same content, same colors — only the radius shifts:

```html
<!-- Sharp: traditional / heritage -->
<section data-radius-density="sharp">
  <button class="rounded-[var(--radius-control)] bg-[var(--color-bg-primary)] text-[var(--color-text-on-primary)] text-button px-5 py-3">
    Schedule a call
  </button>
  <!-- --radius-control resolves to 2px — corners read architectural -->
</section>

<!-- Default: ClearThink standard -->
<button class="rounded-[var(--radius-control)] bg-[var(--color-bg-primary)] text-[var(--color-text-on-primary)] text-button px-5 py-3">
  Schedule a call
</button>
<!-- --radius-control resolves to 4px — corners read deliberate, professional -->

<!-- Soft: friendly / approachable -->
<section data-radius-density="soft">
  <button class="rounded-[var(--radius-control)] bg-[var(--color-bg-primary)] text-[var(--color-text-on-primary)] text-button px-5 py-3">
    Schedule a call
  </button>
  <!-- --radius-control resolves to 6px — corners read warm, accessible -->
</section>
```

Render these three side-by-side to feel the difference. Sharp is institutional; default is professional; soft is approachable. Same button, three brand voices.

### Standard component patterns

Cards, controls, and pills working together inside a section:

```html
<section class="py-[var(--space-section-y)]">
  <div class="mx-auto max-w-screen-xl px-[var(--space-container-x)]">
    <article class="rounded-[var(--radius-default)] bg-[var(--color-bg-surface)] border border-[var(--color-border)] p-8">
      <h3 class="text-h3 text-[var(--color-text-strong)]">ClearLaunch</h3>
      <p class="text-body text-[var(--color-text)] mt-[var(--space-stack)]">
        8-week GTM strategy sprint.
      </p>
      <div class="flex gap-[var(--space-inline)] mt-[var(--space-stack)]">
        <span class="rounded-[var(--radius-pill)] bg-[var(--color-bg-success)] text-[var(--color-text-success)] text-caption px-3 py-1">
          Available
        </span>
        <button class="rounded-[var(--radius-control)] bg-[var(--color-bg-primary)] text-[var(--color-text-on-primary)] text-button px-5 py-2">
          Learn more
        </button>
      </div>
    </article>
  </div>
</section>
```

Three different radii, three different roles — card surface, status pill, action control. The hierarchy reads cleanly because each role is unambiguous.

### Pill in context

Status indicators, tags, and segmented controls all share `--radius-pill`:

```html
<!-- Status pill -->
<span class="rounded-[var(--radius-pill)] bg-[var(--color-bg-success)] text-[var(--color-text-success)] text-caption px-3 py-1">
  In progress
</span>

<!-- Tag -->
<span class="rounded-[var(--radius-pill)] bg-[var(--color-bg-surface-muted)] text-[var(--color-text-muted)] text-caption px-3 py-1">
  AEC-Commercial
</span>

<!-- Toggle (segmented control item) -->
<button class="rounded-[var(--radius-pill)] bg-[var(--color-bg-primary)] text-[var(--color-text-on-primary)] text-button px-4 py-2">
  All
</button>
```

All three use the same token because the pill *role* is consistent — full rounding signals "this is a discrete labeled atom," whether it's status, classification, or selection.

---

## 7. ❌ Common mistakes

**Mismatched radii on adjacent elements.**
```html
<!-- ❌ Card uses default (8px), button inside uses lg (12px) — corners fight each other -->
<article class="rounded-[var(--radius-default)] p-8">
  <button class="rounded-lg ...">Action</button>
</article>

<!-- ✅ Card and button radii belong to different roles, so they can differ — but radii of the same role on adjacent elements should always match -->
<article class="rounded-[var(--radius-default)] p-8">
  <button class="rounded-[var(--radius-control)] ...">Action</button>
</article>
```

The principle: radii within the same role match. A button next to an input matches (both `--radius-control`). Two cards stacked match (both `--radius-default`). A button on a card differs (different roles, different tokens) — but neither should drift to a one-off.

**Hardcoding 9999px for pills.**
```html
<!-- ❌ Bypasses the system; doesn't pick up future pill behavior changes -->
<span class="rounded-[9999px] ...">Available</span>

<!-- ❌ Even worse — `rounded-full` works but skips the role layer -->
<span class="rounded-full ...">Available</span>

<!-- ✅ Use the role token -->
<span class="rounded-[var(--radius-pill)] ...">Available</span>
```

The semantic token communicates intent (this is a pill — a discrete labeled atom). The Tailwind utility communicates only shape (this happens to be fully rounded). Pick the one that documents the why.

**Reaching for a Tailwind primitive when a semantic token exists.**
```html
<!-- ❌ Loses density override — sharp/soft modes won't flex this corner -->
<button class="rounded-md ...">Schedule</button>

<!-- ✅ Goes through the semantic layer — density-aware -->
<button class="rounded-[var(--radius-control)] ...">Schedule</button>
```

Tailwind primitives (`rounded-sm`, `rounded-md`, `rounded-lg`) are still available and still configured to ClearThink's bumped values. They're for cases where no semantic token fits (image-specific radii in a custom component, intentional one-offs). For controls, surfaces, and pills, always use the semantic.
