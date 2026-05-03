# Components — Overview

Routing breadcrumb for `Core/Components/`. Locks the architectural patterns that every component file in this folder follows. Stubbed early (per chat decision) so the patterns are visible during component drafting; sections fill in as patterns harden.

This file is the source of truth for **how component files compose** — naming conventions, utility class structure, cross-component references. Individual component files (`button.md`, `input.md`, etc.) follow the §7.6 component file structure (per Round-1 Resolutions); this overview captures the connective tissue between them.

---

## 1. Components index

| Component | Status | File |
|---|---|---|
| Button | ✅ Built | [`button.md`](./button.md) |
| Input | ✅ Built | [`input.md`](./input.md) |
| Card | Pending | — |
| Modal | Pending | — |
| Accordion | Pending | — |
| Nav (primitive) | Pending | — |

---

## 2. Three utility categories

Every component file uses utility classes in one of three categories. The distinction is locked.

### Subcomponents — sibling DOM elements

`{component}-{part}` naming. Atomic — never bake state into the part name.

Each subcomponent is a separate DOM element with its own utility class. Subcomponents compose with the main component but have their own token consumption.

Examples (from `input.md`):
- `input-label` (the `<label>` element)
- `input-helper` (helper-text below the input)
- `input-error-text` (the error message element — distinct from the `input-error` *state* on the input itself)
- `input-prefix`, `input-suffix` (inline adornments)

**Anti-pattern:** `input-label-error` — error is a state, not a part of the label. Cross-variant states compose via separate utilities (see below), not by baking state into a subcomponent name.

### Modifiers — same DOM element, additional class

`{component}-{modifier}` naming. Modifies the main component's geometry, layout, or shape — but the modifier is on the same DOM node as the variant.

Examples:
- `btn-icon` (square padding via aspect-ratio for icon-only buttons)
- `btn-inline-end` (strips left-side border-radius for input + button pairings)
- `input-bare-sides` (strips border-radius and side-borders for prefix/suffix composition)

Modifiers don't change role; they adapt geometry for composition with other elements.

### Cross-variant states — same DOM element, behavior across all variants

`{component}-{state}` naming. State applies regardless of which variant is in use.

Examples (from `input.md`):
- `input-error` (error state on any input variant)
- `input-disabled` (disabled state on any input variant)
- `input-readonly` (read-only state on any input variant)

**Variant-specific states** (e.g., button hover changes per variant) live as nested pseudo-classes inside the variant utility — not as separate state utilities. The rule from `button.md` §6: pick the approach that matches how state actually varies. Variant-specific = nested; cross-variant = separate.

### Disambiguation summary

| Category | DOM | Naming | Composes with |
|---|---|---|---|
| Subcomponent | Sibling element | `{component}-{part}` | Variant + size on parent |
| Modifier | Same element | `{component}-{modifier}` | Variant + size + state |
| Cross-variant state | Same element | `{component}-{state}` | Variant + size + modifier |

---

## 3. Utility class consumption pattern

Components consume class composition: `class="{component} {component}-{variant} {component}-{size}"`. Locked from `button.md`.

```html
<!-- Buttons -->
<button class="btn btn-primary btn-md">Schedule a call</button>

<!-- Inputs -->
<input class="input input-default input-md" />

<!-- Future cards (illustrative) -->
<article class="card card-elevated card-md">…</article>
```

Tailwind v4 `@utility` declarations (or plain CSS class declarations) define each role. Components reference these as classes — never as raw CSS variables consumed via arbitrary syntax (`class="[font:var(--text-h1)]"` is banned per `button.md` §6 redline trail).

State-implementation rule from `button.md` §6:
- **Variant-specific states** use nested pseudo-classes inside each variant utility
- **Cross-variant states** use separate utilities

---

## 4. Cross-reference convention

Every component file's §12 Related components lists siblings — including ones that don't exist yet — with "*not built yet*" annotations. Future files cross-reference back symmetrically.

Builds a navigable system instead of isolated files. When `card.md` ships, `button.md` and `input.md` get updated to reference it back where relevant.

---

## 5. Token-additive commit pattern

When a component needs primitive tokens that don't yet exist in the token files (`colors.md` / `typography.md` / `spacing.md` / `radii.md` / `shadows.md`), the pattern is:

1. **Sequential commit to the token file** adding the new primitive(s) — purely additive, no existing consumers affected
2. **Component file commit** referencing the new primitive

Established by:
- `--neutral-950-rgb` added to `colors.md` (commit `222c52c`) before `shadows.md` shipped
- `--text-button-sm` / `--text-button-lg` added to `typography.md` (commit `2e65f98`) before `button.md` shipped
- `--text-input` / `-sm` / `-lg` added to `typography.md` (commit `14718f9`) before `input.md` shipped

Forward: `--color-bg-overlay-scrim` will be added to `colors.md` before `card.md` drafts (per chat's consolidated additive survey).

Predictable component-file dependencies on token files should be front-loaded as consolidated additive commits when possible (one survey per token file, not one per component) to reduce sequencing friction.

---

## 6. No inline-style overrides in canonical examples

Code examples in component files (§9 of each file) compose utility classes only. Inline-style overrides (e.g., `style="border-top-left-radius: 0"`) are a signal that a missing utility should be added — either in the same file or as a small follow-up commit to the dependent component.

Established when `input.md` round 2 redlined the prefix/suffix and inline-form code examples. Two new utilities resulted: `input-bare-sides` (added to `input.md`) and `btn-inline-end` (added to `button.md` as follow-up commit `ffa9bc9`).

If a code example *must* show an inline override (e.g., a temporary measure while a follow-up utility is in flight), annotate explicitly — see `input.md` §9 inline-form note pattern.

---

## 7. Variant × sizes × states matrix

Components with multiple variants × sizes × states should include a matrix table (§8 in component files) showing valid combinations. Default to "every cell is valid" unless documented otherwise.

Pattern from `button.md` and `input.md` — both 4-variant × 3-size × 6-state matrices with all cells valid. Convention: state column extends from variant × size base, each cross-variant state composable.

---

## 8. When to split a variant into a separate component

**Locked rule (TBD content — pattern not yet hardened):** A configuration is a separate component file (not a variant) when it has materially different anatomy, accessibility requirements, or state model. Otherwise it's a variant.

Examples observed so far:
- `<a>` styled as a link — separate from button (different element, different a11y, navigation vs action)
- `<textarea>` — separate from input (different element, different size model — auto-resize, max-rows)
- `<select>` — separate from input (different a11y, different state model — open/closed dropdown)

**Section content TBD** — fill in when card.md / modal.md / accordion.md surface more decisions about variant-vs-component splits.

---

## 9. File structure for component files

Reference: §7.6 of `Web-Design_Design-System_Round-1_Resolutions.md`.

Twelve sections, in order:
1. Purpose
2. When to use / when not to use
3. Anatomy
4. Variants
5. States
6. Utility class definitions
7. Token usage
8. Variants × sizes × states matrix
9. Code
10. ❌ Common mistakes
11. Accessibility
12. Related components

The matrix table (§8) is structurally optional — used when component has multiple variants × sizes × states. Components with only a single variant or no states (rare) skip it.

---

## 10. Deferred to Form.md

`[Form]` — not built yet. Several decisions defer to Form's eventual scope:

- HTML `disabled` attribute as form-level submission exclusion (vs `aria-disabled` for visual disabled state on individual inputs)
- Validation patterns and lifecycle
- Submission behavior (full label-input-helper-error-button composition)
- `autocomplete` attribute conventions on common field types
- Form-button labeling convention ("Send proposal" not "Submit")

Tracked in `CLEANUP.md` under "Deferred to Form.md."

---

*Stub committed 2026-05-03. Sections fill in as component patterns harden. Update this file when new components ship if they introduce conventions worth elevating to overview level.*
