# Shadows

ClearThink Web-Design elevation system. Two layers — primitives (5 outer levels + 1 inner, each a stacked sharp-close + soft-far pair for physical realism) and a small semantic layer of role-based elevation tokens.

Follows the §7.6 Token file structure (Philosophy → Primitive scale → Semantic layer → Override surface → Decision tree → Examples → Common mistakes), adapted for dimensional tokens. Inherits the scoped per-file override pattern from `spacing.md` and `radii.md`, with one deliberate vocabulary shift: the multiplier here is `--shadow-depth`, not `--shadow-density`.

---

## 1. Philosophy

Shadow is **presence, not decoration**. Elevation answers a single question: "is this above the surface, and how much?" Three principles drive the schema:

**Two-shadow physical realism, gentle alpha.** Each outer level pairs a sharp close shadow with a soft far shadow — the way real objects cast multi-layered light. Alpha curves stay gentle (0.05–0.12 at the close shadow) so surfaces lift without hovering. AEC-Commercial brands read grounded; theatrical drop-shadows undercut that.

**Role, not geometry.** The semantic layer encodes elevation roles (surface, raised, overlay, modal) — components reach for the role, not the geometry. A card and a tile share `--shadow-surface` because they share an elevation role; splitting them by component name is a coherence trap.

**Depth is the override surface, scoped per file.** A single `--shadow-depth` multiplier scales **alpha** across the semantic layer — flat (0.5×) for editorial / accessibility-focused brands, lifted (1.5×) for tactile / clickable layouts. Geometry (offset, blur, spread) stays constant; only visual weight shifts. The variable is `--shadow-depth` (not `density` like spacing/radii) because depth describes presence, not size.

---

## 2. Primitive scale

Six primitives — five outer elevation levels plus one inner. Outer levels are stacked pairs (sharp close + soft far). Inner is single-stop. All use `--neutral-950` with alpha (not pure black, not warm-tinted) for cohesion with the color system.

Shadows reference the channel-form variant of `--neutral-950` so alpha can flex via the `rgb(R G B / alpha)` syntax. The variant is defined in [`colors.md`](./colors.md):

```css
--neutral-950-rgb: 18 23 24;
```

| Primitive | Composition |
|---|---|
| `--shadow-none` | `none` |
| `--shadow-sm` | `0 1px 2px 0 rgb(var(--neutral-950-rgb) / calc(0.05 * var(--shadow-depth))), 0 1px 1px 0 rgb(var(--neutral-950-rgb) / calc(0.03 * var(--shadow-depth)))` |
| `--shadow-md` | `0 1px 3px 0 rgb(var(--neutral-950-rgb) / calc(0.08 * var(--shadow-depth))), 0 4px 6px -2px rgb(var(--neutral-950-rgb) / calc(0.05 * var(--shadow-depth)))` |
| `--shadow-lg` | `0 4px 6px -1px rgb(var(--neutral-950-rgb) / calc(0.10 * var(--shadow-depth))), 0 10px 15px -3px rgb(var(--neutral-950-rgb) / calc(0.06 * var(--shadow-depth)))` |
| `--shadow-xl` | `0 10px 15px -3px rgb(var(--neutral-950-rgb) / calc(0.12 * var(--shadow-depth))), 0 25px 50px -12px rgb(var(--neutral-950-rgb) / calc(0.08 * var(--shadow-depth)))` |
| `--shadow-inner` | `inset 0 2px 4px 0 rgb(var(--neutral-950-rgb) / calc(0.06 * var(--shadow-depth)))` |

The close-shadow alpha curve (0.05 / 0.08 / 0.10 / 0.12) is intentionally less aggressive than Tailwind's defaults. AEC-Commercial pages read subtle, not theatrical.

`--shadow-depth` flexes alpha values; offset, blur, and spread are fixed. See §4 for the override mechanism.

---

## 3. Semantic layer

Four role-based tokens. Each maps an elevation role to a primitive. Components reach for these — not the primitives directly.

| Token | Maps to | Use |
|---|---|---|
| `--shadow-surface` | `var(--shadow-sm)` | Cards / panels at rest. Default elevation for content surfaces. |
| `--shadow-raised` | `var(--shadow-md)` | Cards on hover, dropdowns, sticky navs, anything that's "lifted but not floating." |
| `--shadow-overlay` | `var(--shadow-lg)` | Popovers, tooltips, contextual menus. Floats above content. |
| `--shadow-modal` | `var(--shadow-xl)` | Modals, dialogs, full-screen overlays. Maximum elevation. |

**Total: 4 semantic tokens.** No semantic for inner shadow — rare enough that components reach for `--shadow-inner` directly when needed (typically inset form fields in compact UI, recessed surfaces).

### What's deliberately NOT a semantic token

- **`--shadow-card` / `--shadow-tile`** — same role, same token (`--shadow-surface`). Splitting by component name fragments the system without adding clarity.
- **`--shadow-popover` / `--shadow-tooltip`** — both `--shadow-overlay`. Same elevation, same token.
- **Hover-state shadows on individual components** — components transition between `--shadow-surface` and `--shadow-raised` directly. No separate "hover shadow" token.
- **Inner shadow at a semantic level** — used rarely enough (recessed inputs, pressed-state UI) that the primitive `--shadow-inner` is the right consumption surface.

---

## 4. Override surface

Shadows' override surface is a single multiplier — same architecture as `spacing.md` and `radii.md`, with one deliberate vocabulary shift.

### Depth (the multiplier)

A single CSS variable scales the **alpha** values across all shadow primitives. Default is `1`. Two named alternates:

```css
:root                              { --shadow-depth: 1; }      /* default — ClearThink standard */
[data-shadow-depth="flat"]         { --shadow-depth: 0.5; }    /* 50% alpha — recedes */
[data-shadow-depth="lifted"]       { --shadow-depth: 1.5; }    /* 150% alpha — pronounced */
```

Set on `<html>` for site-wide override, or on a single `<section>` for scoped override:

```html
<!-- Site-wide -->
<html data-shadow-depth="flat">

<!-- Just this section -->
<section data-shadow-depth="lifted">
```

### Why depth, not density

Spacing and radii multiply geometry — actual pixel sizes flex with the multiplier. Shadows don't: only **alpha** changes. Multiplying offset/blur/spread would shift element positions and visual layout; multiplying alpha keeps geometry constant and only changes visual weight. The vocabulary shift (`depth` instead of `density`) signals this — depth is about presence, not size.

### Use cases (independent of radii density)

- **Default** — most clients. ClearThink standard elevation feel.
- **Flat** — editorial / hero-image-led / accessibility-focused clients. Sites that lean on photography and typography for hierarchy; shadows recede to let imagery carry. Also fits clients with formal accessibility requirements where reduced visual weight is preferred.
- **Lifted** — marketing-forward / tactile / clickable layouts. Sites that want CTAs to feel pressable, cards to feel pickable, components to feel material. Common for AEC-Commercial brands targeting end-consumers (custom residential builders, design-build firms with retail-style sales motions).

Shadow depth is **independent of radii density**. A traditional/heritage client (`data-radius-density="sharp"`) might still want lifted shadows if their UX is conversion-focused; an editorial soft-radii brand might want flat shadows. Different brand levers, independently selectable.

### What's not overridable

- Individual semantic tokens (`--shadow-surface`, etc.) — clients don't reach in. Depth flexes the layer uniformly.
- The 5-primitive scale — clients don't redefine `--shadow-md` to mean a different geometry.
- The shadow color — `--neutral-950` with alpha is the system anchor.

### Override cascade

A depth override on `<html>` cascades to every primitive (and therefore every semantic) automatically through CSS variable inheritance. A scoped override on a section overrides only within that section's subtree. No build-pipeline regeneration required.

### Composing with spacing and radii multipliers

A single page can carry `data-space-density="comfortable"`, `data-radius-density="soft"`, AND `data-shadow-depth="lifted"` without collision. Three independent multipliers, three independent brand levers.

---

## 5. Decision tree — picking the right token

Three branches, role-based, mirrors radii's tree shape:

```
Is this a modal, dialog, or full-screen overlay?
├─ Yes → --shadow-modal
└─ No → continue

Is this a popover, tooltip, or contextual menu?
├─ Yes → --shadow-overlay
└─ No → continue

Is this a content surface (card, panel, tile)?
├─ At rest → --shadow-surface
└─ On hover / sticky / dropdown trigger → --shadow-raised
```

If you reach for a shadow that isn't on this list, you're either reinventing the system or the component genuinely needs no shadow (most components don't). Default to no shadow when in doubt — over-shadowing is the more common failure mode.

---

## 6. Examples used together

### Same card, three depths

The clearest way to feel the system is one component across all three depth modes. Same card, same content, same colors — only shadow alpha shifts:

```html
<!-- Flat: editorial / hero-image-led -->
<section data-shadow-depth="flat">
  <article class="rounded-[var(--radius-default)] bg-[var(--color-bg-surface)] shadow-[var(--shadow-surface)] p-8">
    <!-- shadow-surface alpha resolves to 0.025 close, 0.015 far — barely there -->
    <h3 class="text-h3">ClearLaunch</h3>
  </article>
</section>

<!-- Default: ClearThink standard -->
<article class="rounded-[var(--radius-default)] bg-[var(--color-bg-surface)] shadow-[var(--shadow-surface)] p-8">
  <!-- alpha resolves to 0.05 close, 0.03 far — present, grounded -->
  <h3 class="text-h3">ClearLaunch</h3>
</article>

<!-- Lifted: marketing-forward / tactile -->
<section data-shadow-depth="lifted">
  <article class="rounded-[var(--radius-default)] bg-[var(--color-bg-surface)] shadow-[var(--shadow-surface)] p-8">
    <!-- alpha resolves to 0.075 close, 0.045 far — pickable, material -->
    <h3 class="text-h3">ClearLaunch</h3>
  </article>
</section>
```

Render side-by-side to feel the difference. Flat recedes; default grounds; lifted lifts. Same card, three brand voices.

### Standard elevation hierarchy

Surface → raised → overlay → modal, working together on a page:

```html
<!-- Surface: card at rest -->
<article class="rounded-[var(--radius-default)] bg-[var(--color-bg-surface)] shadow-[var(--shadow-surface)] p-8">
  <h3 class="text-h3 text-[var(--color-text-strong)]">ClearLaunch</h3>
  <p class="text-body text-[var(--color-text)] mt-[var(--space-stack)]">
    8-week GTM strategy sprint.
  </p>
</article>

<!-- Raised: dropdown trigger / sticky nav -->
<nav class="sticky top-0 bg-[var(--color-bg-surface)] shadow-[var(--shadow-raised)] px-[var(--space-container-x)] py-3">
  <!-- nav content -->
</nav>

<!-- Overlay: popover -->
<div role="tooltip" class="rounded-[var(--radius-default)] bg-[var(--color-bg-surface)] shadow-[var(--shadow-overlay)] p-3">
  <p class="text-caption">$1,200 flat — no surprises.</p>
</div>

<!-- Modal: dialog -->
<div role="dialog" class="rounded-[var(--radius-default)] bg-[var(--color-bg-surface)] shadow-[var(--shadow-modal)] p-8 max-w-md">
  <h2 class="text-h2 text-[var(--color-text-strong)]">Schedule a call</h2>
  <!-- modal content -->
</div>
```

Each role has a clear elevation step. Skipping a step (jumping surface → modal) breaks the hierarchy; using each step at the right role keeps it readable.

### Inner shadow in a form field

Inner shadows are rare — typically reserved for recessed-feeling inputs in compact UI. Use the primitive directly:

```html
<input
  class="w-full rounded-[var(--radius-control)] bg-[var(--color-bg-surface-muted)] shadow-[var(--shadow-inner)] border border-[var(--color-border)] px-3 py-2 text-body text-[var(--color-text)]"
  placeholder="Email"
/>
```

The inset shadow gives the input a "scooped into the surface" feel against `--color-bg-surface-muted`. Pair with no outer shadow — combining inner and outer shadows on the same element reads visually noisy.

---

## 7. ❌ Common mistakes

**Hardcoding shadow values.**
```html
<!-- ❌ Bypasses the system; doesn't pick up depth override or color-system updates -->
<article class="shadow-[0_4px_12px_rgba(0,0,0,0.1)]">

<!-- ❌ Even Tailwind's named utility skips the role layer -->
<article class="shadow-md">

<!-- ✅ Use the role token -->
<article class="shadow-[var(--shadow-surface)]">
```

The semantic token communicates intent (this is a surface — at-rest elevation). The hardcoded value or Tailwind utility communicates only geometry. Pick the one that documents the why.

**Over-shadowing — every element doesn't need elevation.**
```html
<!-- ❌ Every block carries a shadow; nothing reads above anything else -->
<section>
  <h2 class="shadow-[var(--shadow-surface)]">Services</h2>
  <p class="shadow-[var(--shadow-surface)]">Our offerings...</p>
  <article class="shadow-[var(--shadow-surface)]"></article>
</section>

<!-- ✅ Surfaces get elevation; copy and headlines stay flat -->
<section>
  <h2>Services</h2>
  <p>Our offerings...</p>
  <article class="shadow-[var(--shadow-surface)]"></article>
</section>
```

Elevation is information — it communicates "this thing is above the page." If everything is elevated, nothing is. Default to no shadow; add one only when the role demands it (a card, a popover, a modal).

**Mismatched shadows on sibling elements.**
```html
<!-- ❌ Three cards in a grid, three different elevations — reads broken -->
<div class="grid grid-cols-3 gap-[var(--space-stack-lg)]">
  <article class="shadow-[var(--shadow-surface)]">Card A</article>
  <article class="shadow-[var(--shadow-raised)]">Card B</article>
  <article class="shadow-[var(--shadow-md)]">Card C</article>
</div>

<!-- ✅ Sibling elements at the same role share the same token -->
<div class="grid grid-cols-3 gap-[var(--space-stack-lg)]">
  <article class="shadow-[var(--shadow-surface)]">Card A</article>
  <article class="shadow-[var(--shadow-surface)]">Card B</article>
  <article class="shadow-[var(--shadow-surface)]">Card C</article>
</div>
```

Adjacent components in the same role match on every visual property — radii, elevation, spacing. If one card lifts higher than its siblings, the page reads broken. The semantic layer's whole purpose is preventing that drift.
