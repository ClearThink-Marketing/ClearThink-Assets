---
name: context-builder
description: Build a CLAUDE.md file by interviewing the user with 7 questions, then generate a complete ready-to-use file from their answers.
allowed-tools:
  - Read
  - Write
---

Build a CLAUDE.md file by interviewing the user. Sub-command: $ARGUMENTS

## PURPOSE

Interview the user with simple questions one at a time and generate a complete, ready-to-use CLAUDE.md file from their answers. This removes the blank-page problem — the user never has to figure out what to write.

Use this when:
- A user is setting up Claude Cowork for the first time
- A user wants to improve their existing CLAUDE.md
- A user's business has changed and their file is stale

---

## WORKFLOW

### STEP 1: INTRODUCE YOURSELF

Start with exactly this message (friendly, no jargon):

---

Hey! I'm going to ask you 7 quick questions and build your CLAUDE.md file from your answers.

This file tells Claude everything it needs to know about you — so every answer it gives is specific to your work, not generic advice.

Answer however feels natural. Short answers are fine.

**Question 1 of 7: What do you do? Describe your job or business in one or two sentences.**

---

### STEP 2: ASK QUESTIONS ONE AT A TIME

Wait for the user to answer each question before asking the next. Do NOT ask multiple questions at once. After each answer, acknowledge it briefly (one sentence max) then ask the next question.

**The 7 questions in order:**

1. What do you do? Describe your job or business in one or two sentences.
2. Who is your audience? Who are you trying to reach or help?
3. What tone do you use? (examples: casual and friendly / professional / direct and no-nonsense / educational)
4. What is your business context? How does your work connect — platforms, products, funnels, team? (e.g. YouTube → email list → paid course)
5. What are your rules for Claude? What should Claude always do when working with you?
6. What should Claude never do? What mistakes or bad habits do you want it to avoid?
7. What are your goals right now? What are you working toward in the next 3-6 months?

### STEP 3: GENERATE THE CLAUDE.MD FILE

After all 7 answers, say:

"Got everything I need. Here's your CLAUDE.md file:"

Then generate the file using this exact structure, filled in from their answers. Write it as a proper markdown code block so they can copy it directly.

---

**CLAUDE.MD TEMPLATE:**

```markdown
# CLAUDE.md
# Last updated: [today's date]

## Who I am
[1-3 sentences from their answer to Q1. Plain English, no jargon.]

## My audience
[1-3 sentences from their answer to Q2. Who they are, what they struggle with, what they want.]

## My tone
[Their answer to Q3, expanded into 2-3 concrete style rules. Example: "Casual and friendly — like explaining to a friend over coffee. No jargon. Short sentences. Encouraging, not preachy."]

## My business context
[Their answer to Q4. Map out the full picture — platforms, products, funnel, anything Claude needs to understand the ecosystem.]

## My rules for Claude
[Bullet list from Q5. Each rule gets its own line. Start each with "Always" or a direct verb.]

## What to avoid
[Bullet list from Q6. Each item gets its own line. Start each with "Never" or "Don't".]

## My goals
[Their answer to Q7. 2-4 bullet points describing what they're working toward.]
```

---

### STEP 4: TELL THEM WHAT TO DO NEXT

After delivering the file, say exactly this:

---

**To use this file:**

1. Copy everything above
2. Open a text editor and paste it
3. Save it as `CLAUDE.md`
4. In Claude Cowork, open your Project → Project Settings → upload the file

Claude will read it at the start of every conversation in that Project. You'll notice the difference immediately.

**Want to update it later?** Just say `/context-builder update` and I'll ask you what changed.

---

## RULES

- Ask questions one at a time. Never stack two questions together.
- Keep your between-question acknowledgments short. One sentence. Don't repeat their answer back to them.
- If an answer is vague, ask one follow-up before moving on: "Can you give me a quick example?"
- Write the final CLAUDE.md in plain English — no corporate speak, no filler phrases
- The "My rules" and "What to avoid" sections should be specific and actionable, not vague ("Always research before writing" not "Be accurate")
- If the user says `/context-builder update` — ask what changed in their business, then regenerate only the sections that need updating
