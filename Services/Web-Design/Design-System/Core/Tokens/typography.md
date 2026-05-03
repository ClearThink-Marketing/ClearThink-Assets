# Typography

ClearThink Web-Design typography system. Two layers — primitives (raw values) and semantics (named tokens components reference). Components reference the semantic layer only, via utility classes.

Follows the same Token file structure as `colors.md` (§7.6 of `Web-Design_Design-System_Round-1_Resolutions.md`).

---

## 1. Philosophy

Type carries voice. ClearThink's brand voice (`Brand/guidelines.md`) is **clear, direct, grounded, confident** — type should read the same. Three principles drive the schema:

**Type is composite.** A heading isn't just a size — it's size + line-height + weight + letter-spacing + family acting together. The semantic layer bundles these into role-named utility classes (`text-h1`, `text-body`) so components don't have to coordinate four properties manually. Components consume these as classes, not as raw CSS variables via arbitrary syntax.

**Modular scale, no one-off sizes.** Sizes above 16px derive from a 1.25 modular ratio (locked per §7.1). Below 16px, sizes are pixel-tuned for readability rather than strict ratio — UI labels at 13px feel cramped against form inputs and button heights. This is convention, not compromise. If a design needs a size that isn't on the scale, the design is wrong, not the scale.

**Family is the override surface; scale is the system.** Clients override font families (`--font-sans`, optionally `--font-display`). The scale, weights, and line heights stay constant. This keeps rhythm consistent across clients while letting brand identity travel through type.

---

## 2. Primitive scale

Raw values. Components never reference these directly.

### Font families

| Token | Default | Notes |
|---|---|---|
| `--font-display` | `'Fraunces', Georgia, serif` | Headlines and display. Variable font with `opsz` and `wght` axes — dials warm-and-human at small sizes, crisp-and-authoritative at hero sizes. Free, Google Fonts. |
| `--font-sans` | `'Inter', system-ui, sans-serif` | Body, UI, h4 and below. Clean geometry, neutral-but-warm, large weight range, ubiquitous browser support. Free, Google Fonts. |
| `--font-mono` | `'JetBrains Mono', ui-monospace, monospace` | Code samples only. Not used in regular marketing copy. |

The Fraunces + Inter pairing gives ClearThink heritage/craftsmanship cues at headline sizes (where AEC-Commercial clients trade on it) without committing to a paid license. Inter handles all functional text where neutrality matters.

### Type scale — modular 1.25 above 16px, pixel-tuned below

Display, h1, and h2 use `clamp()` for fluid sizing — they compress smoothly on small screens without breakpoint hops. h3 and below stay static; reading body at varying sizes introduces measure problems (lines too short narrow, too long wide).

| Token | Computed | Min – Max | Sizing |
|---|---|---|---|
| `--font-size-5xl` | `clamp(2.5rem, 4vw + 1rem, 3.8125rem)` | 40 – 61 px | Fluid (display) |
| `--font-size-4xl` | `clamp(2rem, 3vw + 0.75rem, 3.0625rem)` | 32 – 49 px | Fluid (h1) |
| `--font-size-3xl` | `clamp(1.625rem, 2vw + 0.5rem, 2.4375rem)` | 26 – 39 px | Fluid (h2) |
| `--font-size-2xl` | `1.9375rem` | 31 px | Static (h3) |
| `--font-size-xl` | `1.5625rem` | 25 px | Static (h4) |
| `--font-size-lg` | `1.25rem` | 20 px | Static (body-lg) |
| `--font-size-base` | `1rem` | 16 px | Static (body) |
| `--font-size-sm` | `0.875rem` | 14 px | Static (body-sm, label, button) |
| `--font-size-xs` | `0.8125rem` | 13 px | Static (caption, overline) |
| `--font-size-2xs` | `0.75rem` | 12 px | Static (microcopy floor) |

Note for Frankee / Figma library: fluid tokens need min/max ranges shown in Figma, not just one value.

### Font weights

| Token | Weight | Use |
|---|---|---|
| `--font-weight-regular` | 400 | Body, default |
| `--font-weight-medium` | 500 | h4, buttons, labels, overlines |
| `--font-weight-semibold` | 600 | Display, h1, h2, h3 (Fraunces); inline emphasis (`<strong>`) within body copy (Inter) |

Three weights. Fraunces is variable — one file serves all weights. Inter loads three weight files (400/500/600). Single semibold concept across the system: 600 is the emphasized weight whether it's a Fraunces headline or an Inter `<strong>` in body copy.

### Line heights

| Token | Value | Use |
|---|---|---|
| `--line-height-tight` | 1.05 | Display |
| `--line-height-heading` | 1.1 | h1, h2 |
| `--line-height-snug` | 1.25 | h3, h4, UI labels, overline |
| `--line-height-normal` | 1.5 | Body copy |
| `--line-height-relaxed` | 1.7 | Long-form prose, callouts |

### Letter spacing

| Token | Value | Use |
|---|---|---|
| `--letter-spacing-tight` | `-0.02em` | Large headings (counters apparent looseness at size) |
| `--letter-spacing-normal` | `0` | Default |
| `--letter-spacing-wide` | `0.05em` | Overlines / small caps / eyebrows |

---

## 3. Semantic layer

Composite utility classes. Each bundles size + line-height + weight + family + (where applicable) letter-spacing and text-transform for a single role. Components reference these as class names — never as raw CSS variables consumed via arbitrary syntax.

In Tailwind v4 the semantic layer emits as `@utility` declarations. In plain CSS it's class declarations. Same outcome either way:

```css
@utility text-h1 {
  font: 600 var(--font-size-4xl) / 1.1 var(--font-display);
  letter-spacing: -0.02em;
}

@utility text-overline {
  font: 500 var(--font-size-xs) / 1.25 var(--font-sans);
  letter-spacing: 0.05em;
  text-transform: uppercase;
}
```

Components reference these as classes:

```html
<h1 class="text-h1">A clear plan for growth.</h1>
<p class="text-overline">For service-based businesses</p>
```

Not as arbitrary-value syntax (`class="[font:var(--text-h1)]"`) — that pattern can't bundle `text-transform` for overline and reads awkwardly.

### Display / hero — 1 token

| Class | Size | Line-height | Weight | Family | Tracking |
|---|---|---|---|---|---|
| `text-display` | `5xl` (40–61) | 1.05 | 600 | display | −0.02em |

### Headings — 4 tokens

| Class | Size | Line-height | Weight | Family | Tracking | HTML |
|---|---|---|---|---|---|---|
| `text-h1` | `4xl` (32–49) | 1.1 | 600 | display | −0.02em | `<h1>` |
| `text-h2` | `3xl` (26–39) | 1.1 | 600 | display | −0.02em | `<h2>` |
| `text-h3` | `2xl` (31) | 1.25 | 600 | display | normal | `<h3>` |
| `text-h4` | `xl` (25) | 1.25 | 500 | sans | normal | `<h4>` |

h5 and h6 deliberately omitted — marketing pages rarely need them. If a deeper hierarchy is needed, use `text-overline` or styled body weight.

### Body — 3 tokens

| Class | Size | Line-height | Weight | Family |
|---|---|---|---|---|
| `text-body-lg` | `lg` (20) | 1.5 | 400 | sans |
| `text-body` | `base` (16) | 1.5 | 400 | sans |
| `text-body-sm` | `sm` (14) | 1.5 | 400 | sans |

Inline `<strong>` within body copy renders at weight 600 (Inter semibold) — same emphasized-weight concept as Fraunces headings.

### UI — 9 tokens

| Class | Size | Line-height | Weight | Family | Extras |
|---|---|---|---|---|---|
| `text-button-sm` | `xs` (13) | 1.1 | 500 | sans | — |
| `text-button` | `sm` (14) | 1.1 | 500 | sans | — |
| `text-button-lg` | `base` (16) | 1.1 | 500 | sans | — |
| `text-input-sm` | `sm` (14) | 1.4 | 400 | sans | — |
| `text-input` | `base` (16) | 1.5 | 400 | sans | **iOS zoom floor — never below 16px** |
| `text-input-lg` | `lg` (20) | 1.5 | 400 | sans | — |
| `text-label` | `sm` (14) | 1.25 | 500 | sans | — |
| `text-caption` | `xs` (13) | 1.25 | 400 | sans | — |
| `text-overline` | `xs` (13) | 1.25 | 500 | sans | tracking 0.05em, `text-transform: uppercase` |

Button and input both have three size variants (sm / md-default / lg) because their component files have three sizes. Input line-heights (1.4 / 1.5 / 1.5) are looser than button's (1.1 across sizes) — buttons render labels in a tight inline area; inputs render typed content that needs reading rhythm. `--text-input` (16px) is non-negotiable on default — anything smaller triggers iOS Safari zoom-on-focus, a UX regression. Other UI tokens (label, caption, overline) have a single size since the components that consume them don't size-vary.

### Microcopy — 1 token

| Class | Size | Line-height | Weight | Family |
|---|---|---|---|---|
| `text-micro` | `2xs` (12) | 1.25 | 400 | sans |

12px is the accessibility floor. Anything below fails Section 508 audits and high-DPI rendering tests; 12px is conventional minimum across modern systems.

**Total: 18 semantic tokens.** (1 display + 4 headings + 3 body + 9 UI + 1 microcopy.)

---

## 4. Override surface

Which primitives a client can override.

### Always overridable

- `--font-sans` → client primary typeface. Propagates to body, UI, h4, microcopy.

### Conditionally overridable

- `--font-display` → client display typeface. If absent, falls back to `--font-sans` (same model as `--brand-accent` in `colors.md` falling back to neutrals).
- `--font-mono` → rarely changed; client may override if they have a brand monospace.

### Not overridable

- Type scale (the modular ratio is the system)
- Font weights (the 3-weight set is the system)
- Line heights and letter spacing (these tune the rhythm; clients shouldn't reach in)
- Composite semantic tokens — overrides happen at the family level and propagate

### Override cascade

When a client overrides `--font-sans`, every composite class referencing it (`text-h4`, `text-body`, `text-button`, etc.) automatically inherits the new family because the reference goes through the CSS cascade. The build pipeline does **not** need to re-emit composite classes per-client.

The same applies to `--font-display` overrides — composites referencing `--font-display` (`text-display`, `text-h1`, `text-h2`, `text-h3`) resolve correctly without intervention.

A client adding both an `--font-sans` and `--font-display` override gets a fully re-typed site from a token swap alone — no component edits required.

---

## 5. Decision tree — picking the right token

When writing a component, walk the tree in order:

```
Is this the page's primary headline / hero copy?
├─ Yes → text-display (large) or text-h1 (standard)
└─ No → continue

Is it a section heading?
├─ Major section → text-h2
├─ Sub-section → text-h3
├─ Minor heading → text-h4
└─ No → continue

What role does this text serve?
├─ Body copy
│   ├─ Lead / intro paragraph → text-body-lg
│   ├─ Standard paragraph → text-body
│   └─ Tight UI body → text-body-sm
├─ UI element
│   ├─ Button label → text-button
│   ├─ Form/UI label → text-label
│   ├─ Caption / metadata / helper → text-caption
│   └─ Section eyebrow / overline → text-overline
└─ Legal / footnote → text-micro
```

---

## 6. Examples used together

### Hero section

```html
<section class="bg-[var(--color-bg-page)] py-24">
  <p class="text-overline text-[var(--color-text-link)]">For service-based businesses</p>
  <h1 class="text-display text-[var(--color-text-strong)]">A clear plan for growth.</h1>
  <p class="text-body-lg text-[var(--color-text-muted)] mt-6 max-w-prose">
    8-week sprint that gives you the strategy before you spend on execution.
  </p>
</section>
```

### Service card

```html
<article class="bg-[var(--color-bg-surface)] border border-[var(--color-border)] p-6">
  <h3 class="text-h3 text-[var(--color-text-strong)]">ClearLaunch</h3>
  <p class="text-body text-[var(--color-text)] mt-3">
    8-week GTM strategy sprint.
  </p>
  <span class="text-caption text-[var(--color-text-subtle)] mt-2 block">
    $1,200 flat
  </span>
</article>
```

### Form field

```html
<label class="text-label text-[var(--color-text)]">Email</label>
<input class="text-body text-[var(--color-text)] border border-[var(--color-border-strong)] px-3 py-2" />
<p class="text-caption text-[var(--color-text-subtle)] mt-1">
  We'll only use this to send the proposal.
</p>
```

### Button

```html
<button class="text-button bg-[var(--color-bg-primary)] text-[var(--color-text-on-primary)] px-5 py-3 hover:bg-[var(--color-bg-primary-hover)]">
  Schedule a call
</button>
```

### Body with inline emphasis

```html
<p class="text-body text-[var(--color-text)]">
  ClearLaunch replaces guesswork with a <strong>data-backed strategic foundation</strong> before a single dollar lands on campaigns.
</p>
```

---

## 7. ❌ Common mistakes

**Hard-coding font properties in components.**
```html
<!-- ❌ Disconnected from the scale; won't respond to system updates -->
<h1 style="font-size: 48px; line-height: 1.1; font-weight: 700;">

<!-- ✅ -->
<h1 class="text-h1">
```

**Overriding what the composite class already sets.**
```html
<!-- ❌ leading-tight defeats the composite — text-h2 already sets line-height -->
<h2 class="text-h2 leading-tight">

<!-- ✅ Trust the composite -->
<h2 class="text-h2">
```

**Reaching into composite tokens via arbitrary syntax.**
```html
<!-- ❌ Pre-utility-class pattern; can't bundle text-transform for overline -->
<p class="[font:var(--text-overline)]">

<!-- ✅ Use the utility class -->
<p class="text-overline">
```

**Using HTML heading tags for visual sizing rather than document structure.**
```html
<!-- ❌ <h1> used for visual size, breaks document outline -->
<h1 class="text-h3">Subsection title</h1>

<!-- ✅ Right tag for structure, right class for visual treatment -->
<h3 class="text-h3">Subsection title</h3>
```

**Reaching for a font size that isn't on the scale.**
If a design specifies 22px and the scale offers 20px (`--font-size-lg`) or 25px (`--font-size-xl`), pick one — don't add a one-off. The scale is the system.

**Loading too many font weights.**
Each Inter weight file is ~30 KB; Fraunces variable is ~150 KB but covers all weights. The 3-weight set (Inter 400/500/600 + Fraunces variable at 600) covers marketing needs. Don't load Inter 100/200/300/700/800/900 unless a specific design requirement justifies the page-speed cost.

**Pure `font-family` overrides at the component level.**
```html
<!-- ❌ Bypasses the override mechanism -->
<p style="font-family: Helvetica;">

<!-- ✅ Propagated automatically through --font-sans override -->
<p class="text-body">
```
