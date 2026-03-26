---
name: content-brief-builder
description: "Build information architecture briefs that map finished copy to specific page sections. Use this skill whenever the user mentions 'content brief', 'page brief', 'IA brief', 'information architecture', 'content mapping', 'section mapping', or wants to organize completed website copy into a structured format showing what content goes where on each page. Also trigger when the user provides copy docs and a page structure screenshot and wants them combined into a single reference document. This skill works downstream of the website-copywriter skill — it takes the table-based copy docs as input and produces briefs that define the content structure of each page."
---

# Content Brief Builder

## What This Skill Does

This skill takes finished website copy (from the Website Copywriter skill) and organizes it into page-level information architecture briefs — documents that define what content goes where on each page, in what order, and with what structure.

The brief is focused purely on **information architecture**: section order, content elements per section, content hierarchy, and structural notes (e.g., "this section has 5 repeating cards" or "this is a 2-column split"). It does NOT include visual design direction (backgrounds, colors, animations, hover states, responsive behavior). Those decisions belong to the designer.

## Inputs

**Required:**
- Completed copy document(s) from the Website Copywriter skill (table-based .docx files in the client's Deliverables folder)
- Client profile (from the Client Profile Generator skill, for brand reference)

**Helpful but not required:**
- Page structure screenshot or reference site — a visual showing the section order the designer should follow. This could be a screenshot of a competitor site, a template, or a wireframe sketch.
- CMS or platform constraints (e.g., "this is a WordPress site using Elementor")

If no page structure screenshot is provided, use the copy document's section order as the default page flow.

## Process

### Step 0: Set Up Folders

If they don't already exist, create:
```
Clients/[Client Name]/Deliverables/Briefs/
```

### Step 1: Gather and Review Inputs

1. Read the client profile for brand context
2. Read the copy document(s) for the page(s) being briefed
3. If a page structure screenshot is provided, analyze it to understand:
   - Number of sections and their order on the page
   - What type of content each section contains
   - Navigation and footer structure

### Step 2: Map Copy to Page Structure

For each page section identified from the screenshot (or from the copy doc sections if no screenshot):

1. **Match copy sections to page sections** — align the copy doc's table sections with the screenshot's sections
2. **Identify gaps** — sections in the screenshot that have no corresponding copy, or copy sections that don't map to any visible structure
3. **Note structural patterns** — does a section have repeating items (cards, pillars, team members)? Is it a single block or a split?

### Step 3: Build the Brief

Create a .docx document using a **table-based format** (consistent with the copy docs). The brief should contain:

#### Page Header
- Page name, client name, date
- Reference to source copy doc
- Reference to structure screenshot (if provided)

#### Section Briefs (one per page section, in page order)

Each section gets:

**Section heading** — bold, with the section's position number (e.g., "Section 1: Hero", "Section 2: Social Proof Bar")

**A structure table** — describes what this section contains:

| Label | Content |
|-------|---------|
| **Section Type** | Hero / text block / card grid / split content / stats bar / testimonial / CTA / etc. |
| **Content Elements** | List of what goes in this section (e.g., "Headline, subheadline, 2 CTAs, background image") |
| **Repeating Items** | If applicable: "5 market cards, each with: name, description, image direction" |

**A content table** — the actual copy for this section, pulled verbatim from the copy doc:

| Label | Content |
|-------|---------|
| **Headline** | [The actual headline copy] |
| **Subheadline** | [The actual subheadline] |
| **Body Copy** | [The actual body text] |
| **Primary CTA** | [Button text] → [link destination] |
| **Secondary CTA** | [Button text] → [link destination] |
| **Image Direction** | [Direction from copy doc — what the image should convey, not how it should look] |

**Notes row** — any IA-relevant notes, like "This section references the same services shown on the Services page" or "Client needs to confirm these stats."

#### Repeating Element Briefs

For sections with repeating items (service cards, team members, portfolio items, testimonials):
- Show the **template** — what fields each card/item contains
- Show **all items** filled in with their actual copy
- Note the **count** (e.g., "5 cards total")

#### Navigation & Footer

Include a section for:
- **Navigation**: Menu items and their link destinations, CTA button text
- **Footer**: Link groups (what links go in which column), contact info, social links, legal links

#### Gap Flags

Carry forward any gap flags from the copy doc (yellow-highlighted rows) and add new ones:
- Missing content the client needs to provide (photos, testimonials, case studies, stats)
- Sections where copy exists but no structural reference was given
- Content that needs client review or verification before design proceeds

Consolidate all gaps into a **Gap Summary** table at the end of the brief so the designer and account manager can see everything that's outstanding in one place.

### Step 4: Format and Save

Save each brief to the client's Briefs folder:

```
Clients/[Client Name]/Deliverables/Briefs/[PageName]_Brief.docx
```

For example:
- `Clients/CSBD/Deliverables/Briefs/Homepage_Brief.docx`
- `Clients/CSBD/Deliverables/Briefs/About_Brief.docx`

**Document formatting:**
- US Letter, 1-inch margins, Arial font
- **Table-based layout throughout** — consistent with the copy docs
- Label cells use the client's brand color as a light tint background
- Section headings as styled headings between tables, with accent-colored divider lines
- Gap flags with yellow-highlighted rows
- Section numbers in headings to match page flow order

Use the docx skill (docx-js) for file creation. Reference the docx SKILL.md for technical details.

### Step 5: Present and Get Feedback

After completing the brief(s):
1. Provide computer:// links to each brief doc
2. Note any sections where the copy-to-structure mapping was ambiguous
3. Highlight gap flags that need client input before design can proceed
4. Ask if anything needs adjustment

## Important Notes

- **IA only, not design.** This brief defines what content goes where and in what order. It does NOT dictate visual design decisions (colors, backgrounds, animations, hover states, responsive behavior, spacing, typography choices). The designer uses their own creative discretion for all visual decisions.
- **The brief is the content source of truth.** The designer shouldn't need to cross-reference the copy doc — all copy should be reproduced in the brief alongside its structural context.
- **Match the copy doc exactly.** Don't paraphrase or edit the copy. Pull it verbatim from the copy document. The copywriter already approved it.
- **When no screenshot is provided**, use standard web conventions for section ordering, but note that the designer determines the final structure.
- **One brief per page.** Even if you're briefing an entire site, each page gets its own document.
