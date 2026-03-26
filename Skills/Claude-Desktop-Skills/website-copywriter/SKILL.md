---
name: website-copywriter
description: "Write conversion-focused website copy for any page type — homepages, about pages, service pages, product pages, pricing, contact, FAQ, and more. Use this skill whenever the user wants website copy written, revised, or improved. Triggers include: 'write copy for', 'website copy', 'homepage copy', 'about page', 'service page copy', 'landing page', 'web copywriting', 'CTA copy', 'hero section', or any request to write or rewrite text that will appear on a website. Also trigger when the user provides a client profile and asks for copy to be written from it. This skill works hand-in-hand with the client-profile-generator (upstream) and content-brief-builder (downstream)."
---

# Website Copywriter

## What This Skill Does

This skill writes conversion-focused website copy — the actual words that go on each page of a client's website. It takes a client profile (from the Client Profile Generator skill) and produces polished, persuasive, page-specific copy in .docx format.

Each page gets its own document. The copy is ready for a designer to drop into wireframes or for the Content Brief Builder skill to organize into structured briefs.

## The Copywriting Philosophy

This skill draws on three proven frameworks and applies them with discernment — not mechanically, but as a practiced copywriter would:

### Sugarman (The Craft of Persuasive Writing)
- **The Slippery Slide**: Every sentence pulls readers to the next. Headlines pull to subheadings, subheadings to body, body to CTAs. No dead spots.
- **First Sentence Rule**: The sole purpose of the first sentence is to get them to read the second. Keep it short, emotional, and resonant.
- **Seeds of Curiosity**: Hint at a benefit you'll reveal further down. Keep them scrolling.
- **Sell on Emotion, Justify with Logic**: Lead with how it feels, then back it up with why it makes sense.
- **Harmony**: Get readers nodding "yes" from the first line. Statements they agree with build momentum toward action.
- **Sell the Concept, Not the Product**: Bundle features into emotionally compelling ideas. "Peace of mind" not "waterproof material."

### Cialdini (The Psychology of Persuasion)
- **Pre-Suasion**: What you present first shapes how everything after is received. Prime the right mental frame before the ask.
- **Attention = Importance**: Whatever visitors focus on gets elevated importance. Put your strongest benefit in the most visible position.
- **Trust Before Pitch**: Establish credibility before presenting the offer. Social proof, credentials, and empathy come first.
- **Single Focal Point**: Near the CTA, remove competing distractions. One clear action.
- **The Six Principles**: Use reciprocity (give value first), social proof (others chose this), authority (expertise signals), scarcity (limited availability), consistency (micro-commitments), and liking (shared identity) as natural persuasion layers — not as gimmicks.

### Hormozi (The Structure of Irresistible Offers)
- **Value Equation**: Dream Outcome × Perceived Likelihood ÷ Time Delay ÷ Effort = Value. Maximize the top, minimize the bottom.
- **Grand Slam Offer**: Make the offer so good they feel stupid saying no. Stack value visually.
- **Lead with Outcome, Not Process**: "Get [specific result] in [timeframe]" beats "Our methodology includes..."
- **Transformation Gap**: Show the distance between where they are now and where they'll be. Make the gap feel urgent and the bridge feel simple.
- **Guarantees Remove Risk**: Money-back guarantees, satisfaction promises, and trial periods convert fence-sitters.

### When to Use What

Not every page needs every framework. Use discernment:

| Page Type | Primary Framework | Why |
|-----------|------------------|-----|
| Homepage hero | Cialdini (pre-suasion) + Sugarman (slippery slide) | Prime the right frame, then pull them in |
| About page | Sugarman (storytelling + credibility) | Build trust through narrative |
| Service/product pages | Hormozi (value equation) + Sugarman (emotion → logic) | Make the offer irresistible |
| Pricing page | Hormozi (grand slam offer + value stacking) | Justify the price with visible value |
| Testimonials | Cialdini (social proof + authority) | Let others do the convincing |
| Contact/CTA | Cialdini (single focal point) + Hormozi (risk reversal) | Remove friction, remove risk |
| FAQ | Sugarman (objection resolution) | Anticipate and resolve every doubt |

## Process

### Step 1: Get Oriented

Before writing any copy, you need:

**Required:**
- Client profile (from the Client Profile Generator skill, or equivalent info)
- Which page(s) to write

**Helpful but not required:**
- SEO keywords for the page
- Page structure screenshots or template reference
- Competitor websites for positioning context

If the user just says "write copy for Demarciano" without specifying pages, ask which pages they want. If they say "all of them," write them in this order:
1. Homepage
2. About Us
3. Services/Products Overview
4. Individual Service/Product Pages
5. Pricing (if applicable)
6. Case Studies/Portfolio (if applicable)
7. Contact
8. FAQ

### Step 2: Write the Copy

For each page, produce a .docx document using a **table-based format**. Every content element gets its own labeled row in a table — no prose blocks, no ambiguity about what goes where.

**Page header** — the page name and client name at the top of the document

**Section-by-section copy** — organized by page section (Hero, Value Prop, Social Proof, CTA, etc.). Each section should include:
- **Section name** as a heading (e.g., "Hero Section," "About Preview," "Services Grid")
- **A 2-column table** with labeled rows. The left column is the label (e.g., "Headline," "Subheadline," "Body Copy," "Primary CTA," "Image Direction"), the right column is the actual content. Use the client's brand color as a light tint on the label cells.
- For sections with repeating items (e.g., service cards, market segments, team members), use **sub-tables** — one per item, each with a bold name heading above its own label/value table.
- **Guidance notes** can be included as a "Notes" row within the table when helpful.

**Stats/numbers sections** — use a multi-column table (e.g., 4 columns for 4 stats) with a dark branded background and white text.

**Gap flags** — if real data is missing (e.g., no testimonials yet, no case studies), add a flagged row with a yellow background clearly noting what's needed from the client.

**SEO metadata** — at the end of each page doc, in its own labeled table:
- Title tag (60 chars max)
- Meta description (160 chars max, includes CTA)
- URL slug
- Primary keyword and where it's placed

**Strategic notes** — a final table with 2-3 sentences explaining the copywriting approach for this page

### Step 3: Writing Guidelines

These rules apply to ALL copy produced by this skill:

**Lead with benefits, not features.**
- Bad: "We use advanced CRM software"
- Good: "Never lose track of a lead — automated follow-ups keep your pipeline full"

**Be specific and concrete.**
- Bad: "We provide solutions for businesses"
- Good: "We handle [specific service] for [specific audience] in [specific context]"

**Address objections before they form.**
- Price → lead with value and ROI
- Trust → lead with proof and credentials
- Risk → lead with guarantees and track record
- Time → lead with speed and simplicity

**Use numbers over vague claims.**
- "Over 500 clients served" beats "many satisfied clients"
- "Average 30-day turnaround" beats "fast delivery"
- "94% satisfaction rate" beats "high satisfaction"

**Write for scannability.**
- Short paragraphs (2-4 sentences max)
- Descriptive subheadings that tell a story even if you only read them
- Bullet points for feature/benefit lists
- Bold key phrases sparingly

**Match the client's tone.** Pull tone direction from the client profile (Section 7: Brand Voice & Tone). The profile specifies tone descriptors, personality traits, and words to use/avoid. Follow those.

**BANNED WORDS — Never use these:**
Comprehensive, Robust, Leverage, Synergy, Facilitate, Methodology, Cutting-edge, Innovative, Groundbreaking, Seamless, Next-generation, Transformative, Best-in-class, Intriguing, Noteworthy, Remarkable, Extensive, Harness, Revolutionize

Always prefer: specific, concrete, benefit-oriented, human, clear, direct language.

### Step 4: Page-Specific Strategy

#### Homepage
The homepage is the most important page. It must:
- Pass the **5-second test** — visitors understand what you do, who you serve, and why it matters within 5 seconds
- **Pre-suade** with the right mental frame before asking for action (Cialdini)
- Create a **slippery slide** from hero to CTA (Sugarman)
- Include both **high-commitment** ("Get a quote") and **low-commitment** ("Learn more") CTAs

**Typical homepage sections:**
1. Hero (headline + subheadline + CTA + image direction)
2. Social proof bar (logos, stats, or trust signals)
3. Value proposition or brand statement
4. Services/products preview (benefit-focused, not just names)
5. Featured work or testimonials
6. Secondary CTA

#### About Page
This page builds trust and humanizes the brand. It must:
- **Connect the founder's story to the customer's pain** — not just "here's our history"
- **Establish authority** through credentials, years in business, and track record
- **Show values in action** — not generic platitudes
- Make it about what the customer gets from who you are

#### Service/Product Pages
These pages convert browsers into buyers. They must:
- **Apply the Value Equation** — Dream Outcome × Likelihood ÷ Time ÷ Effort (Hormozi)
- **Lead with the transformation** — where they are now vs. where they'll be
- **Resolve the top 3 objections** specific to this service/product
- Include specific deliverables, timelines, or specifications
- End with a clear, single CTA

#### Pricing Page
If the client has a pricing page, it must:
- **Stack value visually** — show what's included at each tier (Hormozi)
- **Anchor high** — present the premium option first or show the total value before the price
- **Include a guarantee** or risk-reversal element
- Make the preferred option obvious through visual emphasis

#### Contact Page
Keep it simple:
- 3-5 form fields max
- State response time expectations
- Provide alternative contact methods
- Address pre-contact hesitations ("Not sure if we're the right fit? Here's what to expect.")

#### FAQ Page
This is an objection-resolution machine:
- Organize by concern type (pricing, process, results, logistics)
- Write answers that sell, not just inform
- Each answer should resolve the doubt AND reinforce a benefit

### Step 5: Industry Adaptation

While the frameworks are universal, adapt language and emphasis by business type:

| Business Type | Copy Emphasis | Language Style |
|---------------|--------------|----------------|
| B2B Services | ROI, process, expertise | Professional, consultative |
| B2C Services | Outcomes, experience | Warmer, benefit-focused |
| E-commerce/Apparel | Identity, community, visuals | Bold, direct, aspirational |
| Professional Services | Credentials, results, methodology | Authoritative, trustworthy |
| Creative Services | Portfolio, vision, process | Strategic, collaborative |
| Healthcare/Wellness | Care, outcomes, compassion | Compassionate, reassuring |
| Technology/SaaS | Efficiency, solutions, integration | Clear, precise |
| Home Services | Reliability, reviews, local trust | Straightforward, community-focused |

### Step 6: Format and Save

Each page gets its own .docx file saved to the client's Deliverables folder:

```
Clients/[Client Name]/Deliverables/[PageName]_Copy.docx
```

For example:
- `Clients/Demarciano/Deliverables/Homepage_Copy.docx`
- `Clients/Demarciano/Deliverables/About_Copy.docx`
- `Clients/Demarciano/Deliverables/Services_Overview_Copy.docx`

**Document formatting:**
- US Letter, 1-inch margins, Arial font
- **Table-based layout throughout** — every content element in labeled 2-column tables
- Label cells use the client's brand color as a light tint background
- Section headings as styled headings between tables, with a thin accent-colored divider line
- Stats/numbers sections as multi-column branded tables
- SEO metadata in its own labeled table at the end
- Strategic notes in a final table at the very end
- Gap flags with yellow-highlighted rows for missing content

Use the docx skill (docx-js) for file creation. Reference the docx SKILL.md for technical details.

### Step 7: Present and Get Feedback

After completing each page (or all pages):
1. Provide computer:// links to each doc
2. Briefly note any strategic choices worth flagging
3. Ask if revisions are needed before moving on

If the user asks "why did you write it this way?" — explain:
- Which pain point you're addressing
- Which framework informed the approach (Sugarman, Cialdini, or Hormozi)
- How it connects to the ideal customer from the profile
- Why this approach converts better than the alternative

## Important Notes

- **Never use placeholder copy.** Every line should be actual, strategic, polished copy ready to go live.
- **Pull directly from the client profile.** The profile's target audience, UVP, differentiators, and voice guidelines are your raw materials. Don't write generic copy when you have specific client data.
- **The client's voice matters.** If the profile captured direct quotes or specific language the client uses, weave that in. It should sound like THEIR brand, not a template.
- **CTAs should vary.** Don't use "Contact Us" on every page. Tailor CTAs to the page context: "Shop the Collection," "See Our Work," "Get Your Free Quote," "Start Your Project."
- **Don't keyword stuff.** If SEO keywords are provided, integrate them naturally at 1-2% density max. The copy should read like a human wrote it, not an algorithm.
- **E-commerce is different.** For product-based businesses, copy is more concise. Images do heavy lifting. The copy's job is to frame the brand story and guide navigation — not to write essays.
