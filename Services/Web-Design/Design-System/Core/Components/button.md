# Button

ClearThink Web-Design button component. First entry in `Core/Components/`. Consumes the token system established in `Core/Tokens/`; doesn't define new design vocabulary.

Follows the §7.6 component file structure (per Round-1 Resolutions): Purpose → When to use / when not → Anatomy → Variants → States → Utility class definitions → Token usage → Code → ✅/❌ → Accessibility → Related components. The "Utility class definitions" section is new for component files — establishes the consumption pattern for every other component (`@utility btn { ... }`, consumed as `class="btn btn-primary"`).

---

## 1. Purpose

A button triggers an action. Submit a form. Schedule a call. Delete a record. Toggle visibility. The action lives **on the same page** — no navigation. Buttons that navigate are misnamed links and should be `<a>` instead.

---

## 2. When to use / when not to use

### ✅ Use a button for:
- Form submission (`Schedule a call`, `Submit`, `Send`)
- Triggering an action on the current page (`Add to list`, `Save changes`, `Delete`)
- Opening modals, drawers, or expanding states (`Open details`)
- Loading more content (`Show more`, `Load older`)

### ❌ Don't use a button for:
- **Navigation between pages.** Use `<a>` — links carry semantic meaning (URL, hover, middle-click, copy-link, search-engine indexability) that buttons don't.
- **External URLs.** Always `<a target="_blank" rel="noopener">`.
- **Anchor links** (jumping within a page). Use `<a href="#section">`.
- **File upload triggers.** Use `<input type="file">` — wrapping a button styled to look like an input is fragile and inaccessible.
- **State toggles (binary on/off).** Use a Toggle component — buttons don't communicate "currently on" state semantically.

The most common marketing-site failure mode: styling an `<a>` to look like a button and giving it `onClick` instead of `href`. The element should match its job. A button does, a link goes.

---

## 3. Anatomy

Four parts. Padding, border, and corner radius aren't anatomy — they're styling that flows from token usage.

```
┌─────────────────────────────────────────┐
│   [icon]   Schedule a call   [icon]     │
│     ↑           ↑               ↑       │
│  optional      label         optional   │
│   leading                    trailing   │
└─────────────────────────────────────────┘
              container

  In loading state:
┌─────────────────────────────────────────┐
│              [spinner]                  │
│                 ↑                       │
│   replaces label, preserves min-width   │
└─────────────────────────────────────────┘
```

| Part | Element | Notes |
|---|---|---|
| Container | `<button>` | Always a `<button>` element. Never `<div>`, never `<a>` styled to look like one. |
| Label | text content | The action verb. "Schedule a call" not "Click here." |
| Icon (optional) | `<svg>` or icon component | Leading, trailing, or icon-only (separate config). |
| Spinner (loading) | `<svg>` (animated) | Visible when `aria-busy="true"`. Replaces label, preserves button width. |

---

## 4. Variants

Four variants. Each maps to a role in the page's interaction hierarchy.

| Variant | Role | Bg | Text | Border |
|---|---|---|---|---|
| **primary** | The single most-important action on a page or section | `--color-bg-primary` | `--color-text-on-primary` | none |
| **secondary** | Supporting action paired with primary, or the most-important action when no primary exists | `--color-bg-surface` | `--color-text-strong` | `--color-border-strong` |
| **ghost** | Tertiary action, low visual weight (e.g., "Cancel" next to a primary "Save") | transparent | `--color-text` | none |
| **destructive** | Action with irreversible consequence (delete, remove, cancel-with-loss) | `--status-danger-text` | `--neutral-50` | none |

`destructive` re-uses `--status-danger-text` as a fill (the deep red used elsewhere as text on `--status-danger-bg`). This is a deliberate stretch of the status tone into a button context — a destructive button *is* a danger-status concept, and using the same red across the system reinforces that meaning.

No `link` variant. Style links as links; if a button needs to look like text, use `ghost`.

No `icon-only` as a variant — that's a configuration on any of the four variants (see §6 Utility classes for the `btn-icon` modifier).

---

## 5. States

Six states. Every variant supports every state.

| State | Behavior | Token / treatment |
|---|---|---|
| **default** | Resting | Variant base colors |
| **hover** | Cursor over | Variant-specific. `primary` uses `--color-bg-primary-hover`; `secondary` gains a muted-surface fill (`--color-bg-surface-muted`); `ghost` gains a subtle text-tinted wash (`color-mix` of `--color-text` at 8%); `destructive` darkens via `color-mix()` against `--neutral-950`. |
| **focus** | Keyboard focus | Visible 2px ring in `--color-border-focus`, 2px offset from button |
| **pressed** | Active mouse-down or keyboard activation | Bg shifts to `--brand-primary-pressed` (computed); on destructive, darker mix |
| **disabled** | Action unavailable | `aria-disabled="true"`, `opacity: 0.5`, `cursor: not-allowed`, no hover/pressed transitions |
| **loading** | Async action in flight | `aria-busy="true"`, label replaced by spinner, `min-width` preserved (no layout shift), pointer events disabled while busy |

### State implementation notes

**Disabled uses `aria-disabled`, not the `disabled` HTML attribute.** The `disabled` attribute removes the button from the focus order and prevents events from firing — this kills the user's ability to discover *why* something is disabled (tooltips, helper text become unreachable). `aria-disabled="true"` keeps the button focusable and announces "disabled" to screen readers, while CSS handles the visual disabled state. Click handlers should check `aria-disabled` and short-circuit.

**Loading preserves width.** Without `min-width`, replacing "Schedule a call" with a spinner causes the button to shrink — the layout reflows, and the user feels uncertainty. Set `min-width` to the resting button's measured width (or use the Tailwind `min-w-[]` utility with a fixed value matching design intent).

**Ghost hover stays quieter than secondary hover.** Ghost uses a text-tinted wash (`color-mix` against `--color-text` at low alpha) rather than the muted-surface fill secondary uses. This preserves the visual hierarchy at hover — ghost is meant to be the lowest-weight variant, and hovered ghost shouldn't compete with hovered secondary.

**Focus rings are non-negotiable.** Don't set `outline: none` without replacing it with a visible custom ring. Keyboard users rely on it.

---

## 6. Utility class definitions

Components consume class composition: `class="btn btn-primary btn-md"`. Tailwind v4 `@utility` declarations (or plain CSS class declarations) define each role. This is the consumption pattern every component file in `Core/Components/` will follow.

**State implementation: nested vs. separate utilities.** Variant-specific states use nested pseudo-classes (the button pattern below — `btn-primary`, `btn-secondary`, `btn-ghost`, `btn-destructive` each have their own `&:hover` and `&:active` declarations). Component-wide states that apply across all variants use separate utilities (e.g., a future `@utility input-error` that styles error state globally across every input variant). Pick the approach that matches how the state actually varies — variant-specific = nested; cross-variant = separate utility. This precedent applies across `Core/Components/`.

```css
/* Base — applied to every button */
@utility btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: var(--space-inline-sm);
  border-radius: var(--radius-control);
  cursor: pointer;
  transition: background-color 150ms ease, color 150ms ease, box-shadow 150ms ease;
  white-space: nowrap;

  &:focus-visible {
    outline: 2px solid var(--color-border-focus);
    outline-offset: 2px;
  }

  &[aria-disabled="true"] {
    opacity: 0.5;
    cursor: not-allowed;
  }

  &[aria-busy="true"] {
    pointer-events: none;
  }
}

/* Sizes */
@utility btn-sm {
  font: var(--text-button-sm);
  padding: 0.5rem 0.75rem;
  min-height: 36px;
}

@utility btn-md {
  font: var(--text-button);
  padding: 0.75rem 1.25rem;
  min-height: 44px;
}

@utility btn-lg {
  font: var(--text-button-lg);
  padding: 0.875rem 1.5rem;
  min-height: 52px;
}

/* Variants */
@utility btn-primary {
  background-color: var(--color-bg-primary);
  color: var(--color-text-on-primary);

  &:hover:not([aria-disabled="true"]) {
    background-color: var(--color-bg-primary-hover);
  }
  &:active:not([aria-disabled="true"]) {
    background-color: var(--brand-primary-pressed);
  }
}

@utility btn-secondary {
  background-color: var(--color-bg-surface);
  color: var(--color-text-strong);
  border: 1px solid var(--color-border-strong);

  &:hover:not([aria-disabled="true"]) {
    background-color: var(--color-bg-surface-muted);
  }
}

@utility btn-ghost {
  background-color: transparent;
  color: var(--color-text);

  &:hover:not([aria-disabled="true"]) {
    background-color: color-mix(in oklch, transparent, var(--color-text) 8%);
  }
}

@utility btn-destructive {
  background-color: var(--status-danger-text);
  color: var(--neutral-50);

  &:hover:not([aria-disabled="true"]) {
    background-color: color-mix(in oklch, var(--status-danger-text), var(--neutral-950) 10%);
  }
}

/* Icon-only modifier — applies square padding via aspect-ratio rather than asymmetric padding */
@utility btn-icon {
  aspect-ratio: 1;
  padding-inline: 0;
}

/* Inline-end modifier — strips left-side border-radius for input-inline + button pairings */
@utility btn-inline-end {
  border-top-left-radius: 0;
  border-bottom-left-radius: 0;
}
```

The size utilities (`btn-sm`, `btn-md`, `btn-lg`) reference `--text-button-sm`, `--text-button`, and `--text-button-lg`. All three are defined in `typography.md`.

---

## 7. Token usage

Every token this component reads. Cross-reference for impact-analysis when a token changes.

| Token | Source | Usage |
|---|---|---|
| `--text-button` | typography.md | Default (md) size label |
| `--text-button-sm` | typography.md | sm size label |
| `--text-button-lg` | typography.md | lg size label |
| `--color-bg-primary` | colors.md | primary variant fill |
| `--color-bg-primary-hover` | colors.md (computed) | primary hover fill |
| `--brand-primary-pressed` | colors.md (computed) | primary pressed fill |
| `--color-text-on-primary` | colors.md | primary variant label |
| `--color-bg-surface` | colors.md | secondary variant fill |
| `--color-bg-surface-muted` | colors.md | secondary hover fill |
| `--color-text-strong` | colors.md | secondary variant label |
| `--color-text` | colors.md | ghost variant label and hover tint base (via `color-mix`) |
| `--color-border-strong` | colors.md | secondary variant border |
| `--color-border-focus` | colors.md | focus ring color |
| `--status-danger-text` | colors.md | destructive variant fill |
| `--neutral-50` | colors.md | destructive variant label |
| `--neutral-950` | colors.md | hover-shade computation for destructive |
| `--radius-control` | radii.md | corner radius (density-aware) |
| `--space-inline-sm` | spacing.md | gap between icon and label |

No shadow token — buttons don't have elevation. (If a button needs visual lift, use `--shadow-surface` in component-level overrides, but document the deviation.)

---

## 8. Variants × sizes × states matrix

Every combination is valid. All four variants support all three sizes; all twelve variant-size pairs support all six states.

| Variant | sm | md | lg | default | hover | focus | pressed | disabled | loading |
|---|---|---|---|---|---|---|---|---|---|
| primary | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| secondary | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| ghost | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| destructive | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |

Icon configurations (leading / trailing / icon-only) work on every cell.

---

## 9. Code

### Primary, default size

```html
<button class="btn btn-primary btn-md">
  Schedule a call
</button>
```

### Secondary with leading icon

```html
<button class="btn btn-secondary btn-md">
  <svg class="size-4" aria-hidden="true">...</svg>
  Download proposal
</button>
```

### Ghost, small

```html
<button class="btn btn-ghost btn-sm">
  Cancel
</button>
```

### Destructive, large with trailing icon

```html
<button class="btn btn-destructive btn-lg">
  Delete project
  <svg class="size-5" aria-hidden="true">...</svg>
</button>
```

### Icon-only (requires `aria-label`)

```html
<button class="btn btn-ghost btn-icon btn-md" aria-label="Close dialog">
  <svg class="size-4" aria-hidden="true">...</svg>
</button>
```

### Loading state

```html
<button class="btn btn-primary btn-md" aria-busy="true" style="min-width: 180px;">
  <svg class="size-4 animate-spin" aria-hidden="true">...</svg>
  <span class="sr-only">Submitting</span>
</button>
```

### Disabled state

```html
<button class="btn btn-primary btn-md" aria-disabled="true">
  Schedule a call
</button>
```

(Click handlers must check `aria-disabled` and return early. The HTML `disabled` attribute is deliberately not used — see §5 for rationale.)

---

## 10. ❌ Common mistakes

**Hardcoding colors instead of tokens.**
```html
<!-- ❌ Bypasses the system; doesn't pick up density/depth overrides or color updates -->
<button class="btn" style="background-color: #1B9B5E; color: #F6F3EF;">

<!-- ❌ Tailwind utilities skip the role layer -->
<button class="btn bg-emerald-600 text-white">

<!-- ✅ Use the variant utility -->
<button class="btn btn-primary btn-md">
```

The variant utility carries semantic meaning (this is the primary action). Hardcoded colors carry only geometry — and break when a client overrides `--brand-primary`.

**Inconsistent button sizes within a CTA group.**
```html
<!-- ❌ Two CTAs at different sizes — visual noise, breaks visual hierarchy -->
<div class="flex gap-3">
  <button class="btn btn-primary btn-lg">Schedule a call</button>
  <button class="btn btn-ghost btn-md">Learn more</button>
</div>

<!-- ✅ Same size, different variants — hierarchy reads through variant, not size -->
<div class="flex gap-3">
  <button class="btn btn-primary btn-md">Schedule a call</button>
  <button class="btn btn-ghost btn-md">Learn more</button>
</div>
```

Size communicates context (compact UI = sm; default page = md; hero CTA = lg). Use one size per visual context. Hierarchy comes from variant.

**Using `<div>` instead of `<button>`.**
```html
<!-- ❌ Not focusable, not keyboard-activatable, screen readers don't announce as button -->
<div class="btn btn-primary btn-md" onclick="schedule()">Schedule a call</div>

<!-- ✅ Real button element — keyboard, focus, screen reader, all work -->
<button class="btn btn-primary btn-md" onclick="schedule()">Schedule a call</button>
```

If you find yourself reaching for `<div onclick>`, you're either re-implementing what `<button>` already does correctly, or the element should be a link.

**Primary + destructive competing in the same flow.**
```html
<!-- ❌ "Save" and "Delete" both pull the eye — user can't tell what's primary -->
<div class="flex gap-3">
  <button class="btn btn-destructive btn-md">Delete project</button>
  <button class="btn btn-primary btn-md">Save changes</button>
</div>

<!-- ✅ Destructive sits next to ghost or secondary, not primary — destruction is rarely the primary action -->
<div class="flex gap-3">
  <button class="btn btn-ghost btn-md">Delete project</button>
  <button class="btn btn-primary btn-md">Save changes</button>
</div>
```

A primary and a destructive button on the same screen are both screaming for attention. Move destructive to a confirmation dialog, a context menu, or a separate "danger zone" section.

**Using a button when a link is correct.**
```html
<!-- ❌ Marketing-site footer "About" as a button — no URL, no middle-click, no SEO -->
<button onclick="window.location='/about'" class="btn btn-ghost btn-sm">About</button>

<!-- ✅ Real link — works with keyboard, copy-link, search engines, all of it -->
<a href="/about" class="text-link">About</a>
```

The most common marketing-site mistake. Buttons styled to look like links (or vice versa) break the user's mental model and degrade accessibility/SEO.

---

## 11. Accessibility

Five non-negotiable requirements.

| Requirement | Rule |
|---|---|
| **Hit target ≥ 44×44 px** | `btn-md` (44px) and `btn-lg` (52px) hit this floor. `btn-sm` (36px) is a deliberate exception for compact UI contexts (toolbar buttons, dense data tables) — only use sm where the user is unlikely to be on touch and the layout requires density. Never use sm in primary mobile CTAs. |
| **Visible focus ring** | 2px solid ring in `--color-border-focus` with 2px offset, applied via `:focus-visible`. Never `outline: none` without replacement. |
| **`aria-disabled`, not `disabled`** | Disabled buttons stay focusable so screen readers announce "disabled" and users can reach helper-text explaining why. `disabled` HTML attribute hides the button from accessibility tree. |
| **`aria-label` on icon-only buttons** | An icon button without a text label is unreadable to screen readers. `aria-label="Close dialog"` is mandatory. The visible icon's `<svg>` should have `aria-hidden="true"` so it's not double-announced. |
| **`aria-busy="true"` on loading state** | Communicates async state to assistive tech. Pair with `<span class="sr-only">{action verb}</span>` so screen readers hear the action being performed. |

---

## 12. Related components

The component system is navigable — each file cross-references siblings, even ones that don't exist yet, so the relationships are documented as the system grows.

- **[Input]** — *built* (`input.md`). Pairs with `btn-inline-end` for newsletter signup, search bar, and other input + submit-button compositions. Input's `input-inline` variant strips right-side radius; `btn-inline-end` strips this button's left-side radius so they read as a single unit.
- **[IconButton]** — *not built yet*. When the icon-only pattern grows beyond a `btn-icon` modifier (e.g., needs its own size scale, accessibility pattern), it splits into its own component file.
- **[Link]** — *not built yet*. The element to use when the action is navigation. `<a>` styled with `text-link` token usage; never use a button for navigation.
- **[ButtonGroup]** — *not built yet*. Joined or spaced groups of related buttons (filter selectors, segmented controls). When ButtonGroup exists, it'll set the rule for sibling-button visual coherence.
- **[Form]** — *not built yet*. Buttons that submit forms have additional accessibility and state requirements (e.g., the button label should describe the action: "Send proposal" not "Submit"). Form will document the pattern.

The cross-reference convention: list related components even when they don't exist yet. Future component files reference back to button.md the same way. Builds a navigable system instead of isolated files.
