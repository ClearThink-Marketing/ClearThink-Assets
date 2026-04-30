# Brand Guidelines

ClearThink Marketing's visual and verbal identity. Source of truth for any file, deliverable, slide, or page produced by or on behalf of ClearThink.

See [`../Overview.md`](../Overview.md) for company-level positioning and mission.

---

## Brand essence

ClearThink cuts through the noise and gives small business owners a clear plan for growth.

The brand should feel: **clear, direct, grounded, and confident.** Not flashy. Not corporate. Not hyped. Someone who knows their craft talking plainly about what they do.

**Operating principle:** *diagnose before you prescribe.* This applies to the work and to the way we talk about the work.

---

## Colors

| Name | Hex | Role |
|---|---|---|
| **GREEN** | `#1B9B5E` | Primary brand color. Headlines, primary buttons, key accents. |
| **BRIGHT** | `#3BEB96` | Accent. Highlights, hover states, secondary callouts. Use sparingly. |
| **DARK** | `#121718` | Body text on light backgrounds. Dark surfaces. |
| **CREAM** | `#F6F3EF` | Light backgrounds, surfaces, cards. Replaces plain white. |

### Color rules
- **Backgrounds:** default to `CREAM` on light-mode surfaces, `DARK` on dark-mode surfaces. Avoid pure white (`#FFFFFF`) and pure black (`#000000`).
- **Primary actions:** `GREEN` fills with `CREAM` text.
- **Accents:** `BRIGHT` is a highlight color — use it to draw the eye, not to fill large areas.
- **Contrast:** always verify WCAG AA at minimum for any text/background pair.

---

## Typography

ClearThink's default type stack:

| Family | Use | License |
|---|---|---|
| **Fraunces** | Headlines and display | Free, Google Fonts (variable font) |
| **Inter** | Body, UI, h4 and below | Free, Google Fonts |
| **JetBrains Mono** | Code samples (rare in marketing copy) | Free, Google Fonts |

The Fraunces + Inter pairing gives ClearThink heritage and craftsmanship at headline sizes without committing to a paid license. Inter handles all functional text where neutrality matters.

### Pairing principles

- Fraunces for display, h1, h2, h3 — the moments where character matters
- Inter for h4 and everything below — body, UI, labels, captions, microcopy
- Single emphasized-weight concept: 600 (semibold). Fraunces headlines run at 600; inline `<strong>` in body copy also runs at Inter 600
- Don't mix more than two display weights on the same page

### Web design type system

Full token system, sizes, line heights, override mechanics, and consumption patterns live in [`../Services/Web-Design/Design-System/Core/Tokens/typography.md`](../Services/Web-Design/Design-System/Core/Tokens/typography.md). That doc is the source of truth for design system implementation. This section establishes the brand-level pairing decision; the design system implements it.

### Non-web deliverables

Until non-web typography is formalized (slide templates, document templates), keep using the fonts specified in each service's existing `.docx` / `.pptx` templates.

---

## Voice & tone

### The through-line
**Professional but down to earth.** Clear, direct, human.

### By context

| Context | Voice |
|---|---|
| `README.md`, founder-facing content | Slightly more personal. Terry's voice comes through in mission/origin framing. |
| `Overview.md`, reference docs, client deliverables | Corporate-crisp. Third person. Factual. |
| Differentiation sections, positioning statements | Punchier. More direct. Still no hype. |
| Social posts, email subject lines | Short, plainspoken, useful — not clever for the sake of clever. |

### Writing principles
- **Lead with the point.** Don't warm up. Don't set the scene. Say the thing.
- **Short sentences beat long ones.** If you can cut a word, cut it.
- **Concrete beats abstract.** "50-keyword landscape analysis" beats "comprehensive market research."
- **Own the stance.** ClearThink has a point of view (strategy before execution, diagnose before prescribe). Say it plainly.
- **No filler transitions.** Skip "that said," "with that in mind," "moving forward."

---

## Words and phrases to avoid

### Corporate jargon
*unlock, synergy, leverage, empower, robust, holistic, streamline*

### Overused marketing hype
*game-changing, cutting-edge, world-class, best-in-class, next-level, revolutionary, transformative*

### AI-tell phrases
*in today's fast-paced world, delve into, navigate the complexities of, at the end of the day, that said, it's worth noting, landscape (as filler), journey*

### Also avoid
- Excessive superlatives (*the most*, *the best*, *absolutely essential*)
- Sales-deck cadences (*"Imagine a world where..."*)
- Hedging that weakens the point (*"arguably,"* *"somewhat,"* *"kind of"*)
- Empty qualifiers (*really*, *very*, *truly*, *simply*)

---

## Usage notes for agents

Any Claude agent producing ClearThink-branded output — client deliverables, internal docs, marketing copy, code comments in repo files — must check every paragraph against the banned-words list above before shipping.

When in doubt: read it out loud. If it sounds like a sales pitch, a LinkedIn post, or an AI, rewrite it.

---

*Last updated: April 2026*
