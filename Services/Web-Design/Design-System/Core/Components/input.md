# Input

ClearThink Web-Design text input component. Second entry in `Core/Components/`. Inherits the utility class consumption pattern locked in `button.md` (`class="input input-default input-md"`), exercises the §6 nested-vs-separate utilities precedent, and parallels button's size scale so inputs and buttons compose visually in inline layouts.

Follows the §7.6 component file structure (per Round-1 Resolutions).

---

## 1. Purpose

A text input collects single-line typed input from the user — names, emails, phone numbers, search terms, URLs, passwords, numeric values. The input represents **one field, one line**. Multi-line text, structured selections, binary toggles, file pickers, and date pickers are separate component files.

**In scope (this file):**
- `<input type="text">`
- `<input type="email">`
- `<input type="tel">`
- `<input type="url">`
- `<input type="search">`
- `<input type="password">`
- `<input type="number">`

**Out of scope (separate files):**
- `<textarea>` → `[Textarea]` *not built yet*
- `<select>` → `[Select]` *not built yet*
- `<input type="checkbox">` → `[Checkbox]` *not built yet*
- `<input type="radio">` → `[Radio]` *not built yet*
- Toggle switches → `[Toggle]` *not built yet*
- `<input type="file">` → `[FileInput]` *not built yet*
- `<input type="date">` / date pickers → `[DatePicker]` *not built yet*

---

## 2. When to use / when not to use

### ✅ Use a text input for:
- Free-form single-line text capture (name, address line, search query)
- Structured single-line input where a typed value beats a picker (email, phone, URL)
- Numeric input where the range is open or large (price, quantity, percentage — though consider native steppers for very small ranges)
- Password capture (always `type="password"`, never `type="text"` for passwords)

### ❌ Don't use a text input for:
- **Multi-line text.** Use Textarea — single-line input wraps awkwardly when content overflows.
- **Choosing from a fixed list.** Use Select, Radio, or Checkbox — picking is faster and less error-prone than typing.
- **Yes/no decisions.** Use Toggle or Checkbox — text input invites unintended values.
- **Date or time entry.** Use DatePicker — date formats vary by locale and benefit from native UI.
- **Files.** Use FileInput.

---

## 3. Anatomy

Five parts. Three are always present (label, input element, helper or error text). Prefix and suffix are optional adornments.

```
Email *                                          ← input-label (with required asterisk)
┌─────┬─────────────────────────────────┬─────┐
│  @  │ you@example.com                  │  →  │  ← prefix + input element + suffix
└─────┴─────────────────────────────────┴─────┘
We won't share with third parties.                ← input-helper (default state)
⚠ Email is required to receive the proposal.    ← input-error-text (error state)
```

| Part | Element | Notes |
|---|---|---|
| Label | `<label>` | Always paired with the input via `for`/`id` or by wrapping. Contains the field name and optional required indicator. |
| Input element | `<input>` | The actual interactive control. Types per §1. |
| Helper text | `<p>` or `<span>` (with id linked via `aria-describedby`) | Default-state helper. Format hints, examples, optional context. Replaced by error text when input is in error state. |
| Error text | `<p>` (with id linked via `aria-describedby`) | Visible when input is in error state. Distinct utility (`input-error-text`) from the input's error state utility (`input-error`). |
| Prefix / Suffix (optional) | `<span>` | Inline adornment — currency symbols, units, action affordances. Visually attached to the input via shared border. |

---

## 4. Variants

Two variants. Both visually outlined; no filled-style alternative.

| Variant | Role | Notes |
|---|---|---|
| **default** | Stand-alone field. All four corners rounded via `--radius-control`. | Most form contexts. |
| **inline** | Field paired with an adjacent submit button (newsletter signup, search bar). Right-side border radius stripped to 0 so the button takes those corners. | Use when the input + button compose as a single visual unit. |

No `error` variant — error is a state (see §5). No `disabled` variant — disabled is a state. No outlined/filled split — outlined treatment only across both variants.

---

## 5. States

Six states. Every variant supports every state.

| State | Behavior | Token / treatment |
|---|---|---|
| **default** | Resting | `--color-border-strong` border, `--color-bg-surface` fill |
| **hover** | Cursor over | Border darkens to `--color-text` (variant-specific — uses nested pseudo-class on each variant utility) |
| **focus** | Keyboard focus | 2px ring in `--color-border-focus`, 2px offset (matches button) |
| **disabled** | User can't interact, value is **NOT** submitted with the form | `aria-disabled="true"` + `input-disabled` utility, `opacity: 0.5`, `cursor: not-allowed`, surface-muted bg |
| **error** | Validation failed | `--status-danger-text` border + outline, `aria-invalid="true"` for screen readers, `input-error-text` element rendered below |
| **read-only** | User can see but can't edit, value **IS** submitted with the form | HTML `readonly` attribute, surface-muted bg, `cursor: default`, no hover/focus interaction styling |

### State implementation notes

**Cross-variant states use separate utilities** — `input-error`, `input-disabled`, `input-readonly` apply to any variant (default or inline). This exercises the architectural precedent set in button.md §6: variant-specific states (hover, focus) use nested pseudo-classes inside each variant utility; cross-variant states use separate utilities. Error is the cleanest example — error styling is identical regardless of whether the input is `input-default` or `input-inline`.

**Disabled vs. read-only is a submission-semantic difference, not just a styling difference.** A disabled field's value is not included when the form submits. A read-only field's value IS submitted but the user can't change it. Marketing forms use disabled for fields gated behind a prerequisite (you can't enter "phone" until you've confirmed "I want to be called"). Read-only is for confirmation pages and server-supplied values the user is reviewing. Don't confuse them — see §10 Common mistakes.

**Disabled uses `aria-disabled="true"` + `input-disabled` utility.** Same pattern as button — preserves focus order so screen readers can announce "disabled," and keeps helper text reachable. Click handlers and form submission logic must check `aria-disabled` and short-circuit. The HTML `disabled` attribute is a separate submission-exclusion mechanism documented in `[Form]` (when built), not in `input.md` as a visual state.

**`required` attribute pairs with visual asterisk and `aria-required`.** The HTML `required` attribute provides browser validation; the visual asterisk in the label tells sighted users; `aria-required="true"` tells screen readers. All three are needed.

**No success state.** Marketing forms either submit successfully or surface an error. Field-by-field green-checkmark validation is product UI. Don't add it here.

---

## 6. Utility class definitions

Components consume class composition: `class="input input-default input-md"`. Cross-variant states (`input-error`, `input-disabled`, `input-readonly`) and modifiers (`input-bare-sides`) compose with any variant.

Architecture per `button.md` §6:
- **Variant-specific states (hover, focus)** use nested pseudo-classes inside each variant utility
- **Cross-variant states (error, disabled, read-only)** use separate utilities — error styling is identical across `input-default` and `input-inline`, so the utility lives once

Subcomponent utilities (`input-label`, `input-helper`, `input-error-text`, `input-prefix`, `input-suffix`) are siblings of the input itself and consume their own tokens. **Note the naming distinction:** `input-error` is a state utility on the input element; `input-error-text` is the message element below the input. Different responsibilities, different utilities.

```css
/* Base — applied to every input */
@utility input {
  display: block;
  width: 100%;
  border-radius: var(--radius-control);
  border: 1px solid var(--color-border-strong);
  background-color: var(--color-bg-surface);
  color: var(--color-text);
  transition: border-color 150ms ease, box-shadow 150ms ease;

  &::placeholder {
    color: var(--color-text-subtle);
  }

  &:focus-visible {
    outline: 2px solid var(--color-border-focus);
    outline-offset: 2px;
  }
}

/* Sizes */
@utility input-sm {
  font: var(--text-input-sm);
  padding: 0.5rem 0.75rem;
  min-height: 36px;
}

@utility input-md {
  font: var(--text-input);                  /* 16px floor — iOS zoom prevention */
  padding: 0.75rem 1rem;
  min-height: 44px;
}

@utility input-lg {
  font: var(--text-input-lg);
  padding: 0.875rem 1.25rem;
  min-height: 52px;
}

/* Variants */
@utility input-default {
  /* All four corners rounded — base radius from @utility input */

  &:hover:not([readonly]):not([aria-disabled="true"]) {
    border-color: var(--color-text);
  }
}

@utility input-inline {
  /* Right-side radius stripped so adjacent button takes those corners */
  border-top-right-radius: 0;
  border-bottom-right-radius: 0;

  &:hover:not([readonly]):not([aria-disabled="true"]) {
    border-color: var(--color-text);
  }
}

/* Cross-variant state utilities */
@utility input-error {
  border-color: var(--status-danger-text);

  &:focus-visible {
    outline-color: var(--status-danger-text);
  }
}

@utility input-disabled {
  opacity: 0.5;
  cursor: not-allowed;
  background-color: var(--color-bg-surface-muted);
}

@utility input-readonly {
  background-color: var(--color-bg-surface-muted);
  cursor: default;
}

/* Modifier — strips border-radius and side-borders so input attaches cleanly to adjacent elements (typically prefix/suffix) */
@utility input-bare-sides {
  border-radius: 0;
  border-left: none;
  border-right: none;
}

/* Subcomponents */
@utility input-label {
  display: block;
  font: var(--text-label);
  color: var(--color-text);
  margin-bottom: var(--space-stack-sm);
}

@utility input-helper {
  font: var(--text-caption);
  color: var(--color-text-subtle);
  margin-top: var(--space-stack-sm);
}

@utility input-error-text {
  font: var(--text-caption);
  color: var(--status-danger-text);
  margin-top: var(--space-stack-sm);
}

@utility input-prefix {
  display: inline-flex;
  align-items: center;
  padding-inline: 0.75rem;
  background-color: var(--color-bg-surface-muted);
  border: 1px solid var(--color-border-strong);
  border-right: none;
  border-top-left-radius: var(--radius-control);
  border-bottom-left-radius: var(--radius-control);
  color: var(--color-text-subtle);
  font: var(--text-input);
}

@utility input-suffix {
  display: inline-flex;
  align-items: center;
  padding-inline: 0.75rem;
  background-color: var(--color-bg-surface-muted);
  border: 1px solid var(--color-border-strong);
  border-left: none;
  border-top-right-radius: var(--radius-control);
  border-bottom-right-radius: var(--radius-control);
  color: var(--color-text-subtle);
  font: var(--text-input);
}
```

When `input-prefix` or `input-suffix` is used, pair the input with the `input-bare-sides` modifier so its border-radius and adjacent borders collapse — the adornment and input then read as a single visual unit. Show this in §9 Code.

The size utilities reference `--text-input-sm`, `--text-input`, `--text-input-lg`, defined in `typography.md` (commit `14718f9`). **`--text-input` (16px) is non-negotiable on default (md) — anything smaller triggers iOS Safari zoom-on-focus, which is a UX regression.**

---

## 7. Token usage

Every token this component reads.

| Token | Source | Usage |
|---|---|---|
| `--text-input` | typography.md | md size input + prefix/suffix font (16px iOS zoom floor) |
| `--text-input-sm` | typography.md | sm size input font |
| `--text-input-lg` | typography.md | lg size input font |
| `--text-label` | typography.md | input-label font |
| `--text-caption` | typography.md | input-helper, input-error-text font |
| `--color-bg-surface` | colors.md | input fill (default state) |
| `--color-bg-surface-muted` | colors.md | input-disabled, input-readonly, input-prefix, input-suffix fill |
| `--color-text` | colors.md | input value text, input-label text, hover border |
| `--color-text-subtle` | colors.md | placeholder, input-helper, input-prefix/suffix text |
| `--color-border-strong` | colors.md | input border (default), prefix/suffix border |
| `--color-border-focus` | colors.md | focus ring |
| `--status-danger-text` | colors.md | input-error border + outline + input-error-text |
| `--radius-control` | radii.md | input + prefix/suffix corner radius (density-aware) |
| `--space-stack-sm` | spacing.md | label-to-input gap, input-to-helper gap, input-to-error-text gap |

No shadow token — inputs don't have elevation.

---

## 8. Variants × sizes × states matrix

Every combination is valid. All 36 cells (2 variants × 3 sizes × 6 states) are supported.

| Variant | sm | md | lg | default | hover | focus | disabled | error | read-only |
|---|---|---|---|---|---|---|---|---|---|
| default | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| inline | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |

Cross-variant states (`input-error`, `input-disabled`, `input-readonly`) compose with any variant:

```html
<input class="input input-default input-md input-error" aria-invalid="true">
```

Prefix and suffix work on every cell.

---

## 9. Code

### Default, md size, with label and helper

```html
<div>
  <label for="email" class="input-label">
    Email <span aria-hidden="true">*</span>
  </label>
  <input
    id="email"
    type="email"
    name="email"
    class="input input-default input-md"
    autocomplete="email"
    aria-describedby="email-helper"
    required
    aria-required="true"
  />
  <p id="email-helper" class="input-helper">
    We'll send the proposal here. We won't share with third parties.
  </p>
</div>
```

### Error state

```html
<div>
  <label for="email" class="input-label">Email</label>
  <input
    id="email"
    type="email"
    class="input input-default input-md input-error"
    aria-invalid="true"
    aria-describedby="email-error"
    value="not-an-email"
  />
  <p id="email-error" class="input-error-text">
    ⚠ Enter a valid email address.
  </p>
</div>
```

### Inline variant (input + adjacent submit button)

```html
<form class="flex">
  <label for="newsletter-email" class="sr-only">Email</label>
  <input
    id="newsletter-email"
    type="email"
    name="email"
    class="input input-inline input-md"
    placeholder="you@example.com"
    autocomplete="email"
    aria-label="Email"
  />
  <button class="btn btn-primary btn-md btn-inline-end">
    Subscribe
  </button>
</form>
```

**Note:** `btn-inline-end` is forthcoming — a follow-up commit to `button.md` will add the modifier (3-line addition: `border-top-left-radius: 0; border-bottom-left-radius: 0`). Until that ships, callers using this pattern can apply inline border-radius overrides as a temporary measure.

### Prefix + suffix

```html
<div>
  <label for="price" class="input-label">Price</label>
  <div class="flex">
    <span class="input-prefix">$</span>
    <input
      id="price"
      type="number"
      class="input input-default input-md input-bare-sides"
      placeholder="0"
    />
    <span class="input-suffix">USD</span>
  </div>
</div>
```

When prefix and suffix wrap an input, the `input-bare-sides` modifier collapses the input's border-radius and adjacent borders so the three elements read as one visual unit.

### Disabled

```html
<input
  id="phone"
  type="tel"
  class="input input-default input-md input-disabled"
  aria-disabled="true"
  value="(unavailable until address confirmed)"
/>
```

(Click handlers and form submission must check `aria-disabled` and exclude the value. Form-level submission exclusion via HTML `disabled` is documented in `[Form]`.)

### Read-only

```html
<input
  id="confirmation-id"
  type="text"
  class="input input-default input-md input-readonly"
  value="CT-2026-04-30-1247"
  readonly
/>
```

The HTML `readonly` attribute is correct here — it preserves submission while preventing user edits. Pair with the `input-readonly` utility for visual consistency.

### Required field

```html
<label for="name" class="input-label">
  Name <span aria-hidden="true">*</span>
</label>
<input
  id="name"
  type="text"
  class="input input-default input-md"
  autocomplete="name"
  required
  aria-required="true"
/>
```

Three signals together: visual asterisk in the label (sighted users), `required` attribute (browser validation), `aria-required="true"` (screen readers).

---

## 10. ❌ Common mistakes

**Missing `<label>` — using placeholder as label.**
```html
<!-- ❌ Placeholder disappears on focus; screen readers don't announce reliably; field is unreadable when empty after navigating away -->
<input type="email" placeholder="Email" class="input input-default input-md" />

<!-- ✅ Real label paired via for/id -->
<label for="email" class="input-label">Email</label>
<input id="email" type="email" class="input input-default input-md" />
```

The most common form mistake. Placeholders are hint text, not labels — they vanish the moment the user starts typing, and they're unreliable for assistive tech. Always pair a `<label>` with every `<input>`.

**Font size below 16px on mobile-primary inputs — triggers iOS zoom.**
```html
<!-- ❌ btn-sm and input-sm at 14px cause iOS Safari to zoom in on focus, jolting the user -->
<input class="input input-default input-sm" />

<!-- ✅ Default to md (16px) for any input a mobile user will touch -->
<input class="input input-default input-md" />
```

iOS Safari triggers automatic zoom-on-focus when an input's font-size is below 16px. The page zooms, the user has to manually zoom out, the form feels broken. `--text-input` is locked at 16px to prevent this. `input-sm` (14px) is a deliberate exception for compact UI contexts only — toolbar search, dense data-entry tables. **Never use `input-sm` for primary mobile form fields.**

**Hardcoding error colors instead of using `input-error`.**
```html
<!-- ❌ Bypasses the system; doesn't pick up status-color updates; aria-invalid is missing -->
<input type="email" class="input input-default input-md" style="border-color: red;" />

<!-- ✅ Use the state utility, which carries the right border + outline styling AND signals the right semantics via aria-invalid -->
<input type="email" class="input input-default input-md input-error" aria-invalid="true" />
```

The error state has both visual and accessibility components. The `input-error` utility carries the visual treatment; `aria-invalid="true"` carries the screen-reader semantic. Both are needed.

**Disabled vs. read-only confusion — different submission semantics.**
```html
<!-- ❌ Order summary that "disables" the line-item names — but the values won't be in the form payload, so the order can't be reconstructed server-side -->
<input class="input ... input-disabled" aria-disabled="true" value="ClearLaunch — $1,200" />

<!-- ✅ Read-only: user can't edit, but the value IS submitted -->
<input class="input ... input-readonly" readonly value="ClearLaunch — $1,200" />
```

**Disabled** = user can't interact, value is **not submitted** when the form posts. Use for fields gated behind a prerequisite (e.g., "Phone number" disabled until "I want to be called by phone" is checked).

**Read-only** = user can't edit, but value **IS submitted**. Use for confirmation pages, server-supplied values the user is reviewing, identifiers that must round-trip without modification.

Picking the wrong one breaks form submission semantics — disabled fields silently drop out of the payload.

**Missing `autocomplete` attribute on common field types.**
```html
<!-- ❌ Forces the user to manually type their email even though the browser knows it; major conversion drag on lead-gen forms -->
<input type="email" name="email" class="input input-default input-md" />

<!-- ✅ Browser autofills from the user's saved profile, dropping form completion time substantially -->
<input
  type="email"
  name="email"
  class="input input-default input-md"
  autocomplete="email"
/>
```

Common values: `email`, `tel`, `name`, `given-name`, `family-name`, `street-address`, `postal-code`, `country`, `organization`, `bday`, `current-password`, `new-password`. The full spec lives at [WHATWG autofill](https://html.spec.whatwg.org/multipage/form-control-infrastructure.html#autofill).

For ClearThink lead-gen forms (email + name + company are most fields), missing autocomplete is a measurable conversion drag.

---

## 11. Accessibility

Six non-negotiable requirements.

| Requirement | Rule |
|---|---|
| **`<label>` paired with every `<input>`** | Either via `<label for="X">` + `<input id="X">`, or by wrapping `<label><span>Field</span><input/></label>`. Visually-hidden labels acceptable (`<label class="sr-only">`) when context makes the label redundant — e.g., a single search input next to a "Search" button — but the label must still exist in the DOM. |
| **`aria-describedby` linking helper / error text to input** | The id of the helper-text or error-text element goes in the input's `aria-describedby`. Screen readers announce the description after the field name. When error replaces helper, swap the id reference. |
| **`aria-invalid="true"` on error state** | Always pairs with `input-error` utility class. Class handles visual; aria handles semantic. |
| **`required` + visual asterisk + `aria-required`** | Required fields need all three signals. The HTML `required` attribute does browser validation; the visible asterisk in the label tells sighted users; `aria-required="true"` tells screen readers. |
| **Visible focus ring** | 2px solid ring in `--color-border-focus` with 2px offset, applied via `:focus-visible`. Same pattern as button. Never `outline: none` without replacement. |
| **AA contrast on error text — 4.5:1** | `--status-danger-text` (#991B1B) on `--color-bg-page` (#F6F3EF) measures 6.4:1, comfortably above the 4.5:1 floor. Verify if a client overrides backgrounds. |

---

## 12. Related components

- **[Textarea]** — *not built yet*. Multi-line text input. Inherits this file's label / helper / error-text / state pattern; size scale and behavior diverge (auto-resize, max-rows, etc.).
- **[Select]** — *not built yet*. Single or multi-value selection from a fixed list. Use when the value space is finite and known.
- **[Checkbox]** — *not built yet*. Independent boolean choices.
- **[Radio]** — *not built yet*. Mutually exclusive choice from a small set.
- **[Toggle]** — *not built yet*. Binary on/off (preference setting). Distinct from Checkbox (form value).
- **[FileInput]** — *not built yet*. File uploads.
- **[DatePicker]** — *not built yet*. Date and time entry.
- **[Form]** — *not built yet*. Container for input groups, validation patterns, submission lifecycle. Will document the full label-input-helper-error-button composition pattern, including HTML-`disabled` form-level submission exclusion.
- **[Button]** — *built* (`button.md`). Pairs with `input-inline` for newsletter signup, search bar, and other input + submit-button compositions. The `input-inline` variant strips right-side radius; the adjacent button uses the forthcoming `btn-inline-end` modifier to strip left-side radius.
