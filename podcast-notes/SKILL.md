---
name: podcast-notes
description: Use this skill when the user pastes podcast transcript quotes or excerpts and wants actionable notes. Trigger phrases include "podcast notes", "turn this into notes", "actionable advice", or when the user pastes transcript text and asks for practical takeaways. Also activate when the user uses /podcast-notes.
version: 2.0.0
allowed-tools: [Read, Write, Edit, Glob, Grep, AskUserQuestion]
---

# Podcast Notes - Transcript to Actionable Advice

This skill converts raw podcast transcript excerpts into clean, practical, bulleted advice. No fluff. No reinterpretation. Just what the speaker actually said, distilled into imperative bullets you can act on. Notes are saved to the vault with source metadata and cross-referenced against existing notes.

## When to Use This Skill

Activate when user:
- Pastes podcast transcript text and wants notes or advice
- Says "podcast notes", "turn this into notes", "actionable advice"
- Pastes a quote block and asks for practical takeaways
- Uses /podcast-notes

Do NOT activate for:
- Summarizing entire podcast episodes from a URL
- Writing tweets from transcripts (use write-tweets skill)
- Creating PRDs from podcast content (use write-prd skill)
- General note-taking unrelated to podcast/interview transcripts

---

## Vault Integration

### On startup:
1. Ask the user for the podcast name and episode (if not already stated). This is for your records only — it does NOT appear in the bullet output.

### On output:
1. **Display bullets clean** — no attribution, no source info, just the imperative bullets (same as before).
2. **Save to vault.** Write notes to `Ideas/Podcasts/[Podcast Name] - [Episode or Topic].md`. If a file for this podcast already exists, append under a new date header.
3. **File format:**
   ```markdown
   # [Podcast Name] - [Episode/Topic]
   **Date:** YYYY-MM-DD
   **Source:** [Podcast name, episode number/title if known]

   ---

   - [bullet 1]
   - [bullet 2]
   - ...
   ```

### Cross-referencing:
After generating bullets, Grep the vault (`Ideas/`, `Work/`, `Writing/`, `Personal/`) for concepts that connect to the advice. If you find relevant existing notes, append a `## Connections` section to the saved file:

```markdown
## Connections
- [[Note Name]] — [1-sentence explanation of why it connects]
```

Only include genuine connections. Don't force it.

---

## Core Rules

### 1. Faithfulness Over Creativity
Extract what was actually said. Do NOT:
- Add advice the speaker didn't give
- Infer meaning that isn't clearly stated
- Reframe the advice into a different philosophy or framework
- Embellish or dramatize the point
- Add qualifiers or caveats the speaker didn't include

### 2. Direct Imperative Tone
Every bullet starts with a verb. Command form. No hedging.

**Do this:**
- Define your North Star metric before building anything.
- Set guardrail metrics upfront so you know when to stop.

**Not this:**
- You should consider defining a North Star metric.
- It might be helpful to think about guardrail metrics.
- One approach is to set metrics before building.

### 3. Flat Bullet List
- One flat list of bullets. No headers, no grouping, no numbering.
- Each bullet is one actionable piece of advice.
- If a point has a sub-point that is a distinct action, make it its own bullet.
- Keep bullets to 1-2 sentences max. If it needs more, split it.

### 4. No Attribution in Display Output
- Strip all speaker names, podcast names, and links from the displayed bullets.
- Source info is saved in the vault file metadata only.

### 5. No Fluff
- No introductory text ("Here are the key takeaways...")
- No closing text ("Hope this helps!")
- No meta-commentary about the transcript
- Just the bullets. Nothing else.

---

## How to Process Transcript Text

### Step 1: Read the Transcript
Read the pasted text carefully. Identify every distinct piece of advice, recommendation, framework, or actionable insight.

### Step 2: Filter Out Non-Advice
Skip:
- Small talk, pleasantries, filler ("yeah", "right", "so basically")
- Self-promotion or plugs
- Storytelling that doesn't contain a transferable lesson
- Repetition of the same point (consolidate into one bullet)
- Questions posed by the interviewer (unless they contain advice)

### Step 3: Convert to Imperative Bullets
For each piece of advice:
1. Identify the core action or principle
2. Write it as a direct command starting with a verb
3. Preserve specificity — if the speaker named a specific metric, method, or framework, keep it
4. Keep the speaker's language where it's clear and direct; only rephrase when the transcript is rambling or unclear

### Step 4: Display Output
Print the bullets. Nothing else.

### Step 5: Save and Cross-Reference
1. Save to vault (see Vault Integration above).
2. Search for connections to existing notes.
3. Tell the user where the file was saved and any connections found.

---

## Examples

### Input:
"I think the strategy component, a couple other components I'd highlight, what is your hypothesis? Because we always want to be using the scientific method. What is your North Star metric, your guardrail metrics, your diagnostic metrics? Because we always want to set that out in advance so that we can then look at, you know, in a statistically significant way, whether things are working."

### Output:
- Start with a hypothesis before building anything.
- Apply the scientific method to product work.
- Define your North Star metric, guardrail metrics, and diagnostic metrics upfront.
- Set metrics in advance so you can measure results with statistical significance.

---

### Input:
"And what are the open questions? Like, what are we trying to test? What are we not trying to do with the feature? All those things, a prototype doesn't answer those questions. So really, the ideal unit of work for a PM right now is a prototype plus a PRD."

### Output:
- Document your open questions explicitly — what you're testing and what you're not trying to do.
- Recognize that prototypes alone don't answer strategic questions.
- Pair every prototype with a PRD — that's the ideal unit of PM work.

---

## Edge Cases

**If the transcript is too vague to extract actionable advice:**
Print what you can extract, then add a single line at the end:
`[Some points in this excerpt were too vague to convert to specific advice.]`

**If the transcript contains no actionable advice (pure storytelling/anecdote):**
State: `[This excerpt doesn't contain actionable advice to extract.]`

**If the user pastes multiple separate transcript excerpts:**
Process them all into one flat bullet list. Do not separate by excerpt.

---

## Quality Checklist

Before outputting, verify:
- [ ] Every bullet starts with an imperative verb
- [ ] No bullet adds meaning the speaker didn't express
- [ ] No introductory or closing text
- [ ] No attribution in displayed output
- [ ] No numbering or headers — just a flat bullet list
- [ ] Each bullet is 1-2 sentences max
- [ ] Filler and small talk have been stripped
- [ ] Specific terms/frameworks from the speaker are preserved
- [ ] Notes saved to vault with source metadata
- [ ] Cross-references checked and included if relevant
