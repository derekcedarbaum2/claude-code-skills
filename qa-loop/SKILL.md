---
name: qa-loop
description: Recursive self-improvement loop for PM artifacts. Evaluates, critiques, rewrites, and re-scores until quality threshold is met. Use when you want to polish a PRD, stakeholder update, interview synthesis, or hypothesis before shipping.
version: 1.0.0
allowed-tools: [Read, Write, Edit, Glob, Grep, AskUserQuestion]
---

# QA Loop - Recursive Quality Refinement

A brutal, iterative quality loop that evaluates your work, diagnoses weaknesses, rewrites, and re-evaluates until it actually hits the bar. No more shipping first drafts.

## When to Use This Skill

Activate when user:
- Says "qa loop", "polish this", "make this sharper", "review and improve"
- Wants to refine a PRD, stakeholder update, interview synthesis, or hypothesis
- Says "this isn't good enough yet" or "tighten this up"
- Invokes `/qa-loop` with or without a file path

Do NOT activate for:
- First-draft generation (use `/write-prd`, `/hypothesis`, etc. first)
- Code review (this is for PM artifacts, not code)
- Simple editing tasks (typos, formatting)

## Core Philosophy

> **Generate → Evaluate → Diagnose → Improve → Repeat**

Most artifacts ship at 70% quality. This skill doesn't stop until you hit 90%.

The loop runs three escalating passes:
1. **Constructive Coach** - Identify gaps, suggest fixes
2. **Skeptical Reviewer** - Challenge assumptions, push back on weak points
3. **Adversarial Attacker** - Actively try to break the argument

Each pass scores against criteria. Loop continues until ALL criteria score 9/10 or higher.

---

## Invocation

**File mode:**
```
/qa-loop /path/to/artifact.md
```

**Inline mode (on last generated artifact):**
```
/qa-loop
```

If no file path provided, look for the most recently written/edited file in the conversation context.

---

## Workflow Overview

1. **Detect Artifact Type** - PRD, stakeholder update, interview synthesis, or hypothesis
2. **Load Scoring Criteria** - Type-specific evaluation rubric (10 criteria)
3. **Initial Score** - Evaluate current state against all criteria
4. **Pass 1: Constructive** - Coach tone, identify gaps, rewrite weak sections
5. **Re-Score** - Check if 9/10 threshold met
6. **Pass 2: Skeptical** - Reviewer tone, challenge assumptions, tighten arguments
7. **Re-Score** - Check if 9/10 threshold met
8. **Pass 3: Adversarial** - Attacker tone, stress-test with hostile personas
9. **Final Score** - Confirm all criteria at 9/10
10. **Output** - Polished artifact + changelog

**Exit Criteria:** ALL criteria must score 9/10 or higher. Max 3 passes.

---

## Step 1: Detect Artifact Type

Read the artifact and classify it:

| Type | Detection Signals |
|------|-------------------|
| **PRD** | Contains "Requirements", "Acceptance Criteria", "User Stories", "Problem Statement", JTBD format |
| **Stakeholder Update** | Contains "Status", "Progress", "Update", "Summary", addressed to leadership/customers |
| **Interview Synthesis** | Contains "Key Insights", "Quotes", "JTBD", "Persona", references to interviews/discovery |
| **Hypothesis** | Contains "Assumption", "Validation", "Thesis", "Kill Criteria", early-stage framing |

If ambiguous, ask:

```yaml
questions:
  - question: "What type of artifact is this?"
    header: "Artifact Type"
    multiSelect: false
    options:
      - label: "PRD"
        description: "Product requirements document for engineering"
      - label: "Stakeholder update"
        description: "Status update, executive summary, or customer communication"
      - label: "Interview synthesis"
        description: "User discovery output, JTBD extraction, research analysis"
      - label: "Hypothesis"
        description: "Early-stage opportunity brief, assumption mapping"
```

---

## Step 2: Load Scoring Criteria

Each artifact type has 10 scoring criteria. Every criterion is scored 1-10.

### PRD Scoring Criteria

| # | Criterion | What 9/10 Looks Like | Common Failure |
|---|-----------|---------------------|----------------|
| 1 | **Problem Specificity** | Quantified pain ("45 min/session" not "takes too long") | Vague adjectives |
| 2 | **Evidence Quality** | Direct quotes, data, named sources | Claims without proof |
| 3 | **So-What Clarity** | Every fact has an implication stated | Facts without meaning |
| 4 | **Metric Precision** | Baseline → Target → Timeframe for every metric | "Improve X" without numbers |
| 5 | **Audience Fit** | Right detail level for engineers (testable, specific) | Too vague to implement |
| 6 | **Structure Logic** | Most important info first, logical flow | Buried lede, random order |
| 7 | **Word Economy** | No filler, every sentence earns its place | Bloat, redundancy |
| 8 | **Acceptance Criteria** | Specific enough to write tests against | "Should work well" |
| 9 | **Scope Clarity** | Crystal clear what's in/out, why deferred | Ambiguous boundaries |
| 10 | **Actionability** | Engineer could start tomorrow | Missing context to begin |

### Stakeholder Update Scoring Criteria

| # | Criterion | What 9/10 Looks Like | Common Failure |
|---|-----------|---------------------|----------------|
| 1 | **Executive Summary** | Key message in first 2 sentences | Buried lede |
| 2 | **So-What Clarity** | Clear implications for the reader | Status without meaning |
| 3 | **Ask Clarity** | Explicit request (decision, resources, awareness) | Unclear what you want |
| 4 | **Progress Honesty** | Real status, not spin | Hiding problems |
| 5 | **Risk Visibility** | Blockers surfaced with mitigation | Surprises later |
| 6 | **Metric Specificity** | Numbers, not adjectives | "Going well" |
| 7 | **Time Orientation** | Clear what happened, what's next, by when | Missing timeline |
| 8 | **Audience Calibration** | Right altitude for the reader | Too detailed or too vague |
| 9 | **Word Economy** | Respects reader's time, no fluff | Could be half the length |
| 10 | **Action Items** | Clear owners and deadlines | Vague next steps |

### Interview Synthesis Scoring Criteria

| # | Criterion | What 9/10 Looks Like | Common Failure |
|---|-----------|---------------------|----------------|
| 1 | **Quote Selection** | Quotes reveal unmet needs, not just confirm beliefs | Cherry-picked agreement |
| 2 | **Insight Specificity** | Concrete observations, not generalizations | "Users want better UX" |
| 3 | **JTBD Format** | Proper When/Want/So-that with real triggers | Vague job statements |
| 4 | **Evidence Linking** | Every insight traced to specific quote | Unsupported conclusions |
| 5 | **Contradiction Surfacing** | Notes where data conflicts | Only confirming evidence |
| 6 | **Participant Voice** | Preserves user's language, not PM-speak | Over-sanitized |
| 7 | **Implication Clarity** | What this means for product decisions | Facts without so-what |
| 8 | **Sample Honesty** | Acknowledges n=1 limitations | Overgeneralizing |
| 9 | **Question Quality** | Open questions are specific and answerable | Vague "needs more research" |
| 10 | **Actionability** | Clear what to do with this information | Interesting but useless |

### Hypothesis Scoring Criteria

| # | Criterion | What 9/10 Looks Like | Common Failure |
|---|-----------|---------------------|----------------|
| 1 | **Falsifiability** | Specific enough to prove wrong | Unfalsifiable belief |
| 2 | **Assumption Clarity** | Each assumption explicit and testable | Hidden assumptions |
| 3 | **Evidence Baseline** | Honest about what's known vs. guessed | Overconfident |
| 4 | **User Specificity** | Named persona, not "users" | Generic audience |
| 5 | **Trigger Clarity** | Specific situation when need arises | Vague context |
| 6 | **Outcome Precision** | Measurable success, not "better" | Fuzzy goals |
| 7 | **Risk Prioritization** | Riskiest assumption identified | All risks equal |
| 8 | **Kill Criteria** | Specific conditions to abandon | No exit ramp |
| 9 | **Validation Plan** | Concrete next steps to test | "Do more research" |
| 10 | **Word Economy** | Tight, no hedge words | Weasel words everywhere |

---

## Step 3: Initial Scoring

Score the artifact against all 10 criteria. For each criterion:

```
[Criterion Name]: [Score]/10
  Current: "[Quote from artifact showing current state]"
  Gap: [What's missing or weak]
```

**Output format:**

```markdown
## Initial Assessment

**Artifact:** [filename or "inline"]
**Type:** [PRD / Stakeholder Update / Interview Synthesis / Hypothesis]
**Overall Score:** [sum/100] ([percentage]%)

### Scores by Criterion

| # | Criterion | Score | Gap |
|---|-----------|-------|-----|
| 1 | [Name] | X/10 | [Brief gap description] |
| 2 | [Name] | X/10 | [Brief gap description] |
...

### Criteria Below Threshold (<9)
[List criteria that need improvement, ordered by severity]

### Pass 1 Focus
[Top 3-4 criteria to address in constructive pass]
```

---

## Step 4: Pass 1 - Constructive Coach

**Tone:** Helpful mentor. "Here's how to strengthen this."

**Focus:** Address the 3-4 lowest-scoring criteria identified in initial assessment.

**Process:**
1. For each weak criterion, explain the gap clearly
2. Show a specific fix (rewrite the section, don't just describe)
3. Preserve author's voice while tightening

**Rewrite Rules:**
- Replace vague adjectives with numbers
- Add "This means..." after every fact
- Move most important information to the top
- Cut words that don't add meaning
- Add evidence where claims are unsupported

**Output:**

```markdown
## Pass 1: Constructive Coach

### Changes Made

**[Criterion 1]: [Score before] → [Score after]**
- Before: "[Original text]"
- After: "[Rewritten text]"
- Why: [Explanation of improvement]

**[Criterion 2]: [Score before] → [Score after]**
...

### Structural Changes
- [Any reordering, section moves, deletions]

### Updated Artifact
[Full rewritten artifact]
```

---

## Step 5: Re-Score After Pass 1

Re-evaluate all 10 criteria on the updated artifact.

**If all criteria ≥ 9/10:** Skip to Step 10 (Output)

**If any criteria < 9/10:** Continue to Pass 2

---

## Step 6: Pass 2 - Skeptical Reviewer

**Tone:** Constructively critical. "I'm not convinced. Prove it."

**Focus:** Challenge the argument, not just the writing.

**Skeptical Questions to Ask:**
- "How do we know this is true?"
- "What's the evidence for this claim?"
- "Who says? When? In what context?"
- "What would someone who disagrees say?"
- "Is this the most important thing, or just the first thing?"

**Rewrite Rules:**
- Every claim needs a source or gets qualified with "We believe..."
- Every "should" needs a "because"
- Every recommendation needs a "measured by"
- Remove anything that can't be defended

**Output:**

```markdown
## Pass 2: Skeptical Reviewer

### Challenges Raised

**Challenge 1:** [Weak claim or assumption]
- Original: "[Text that doesn't hold up]"
- Problem: [Why this is weak]
- Resolution: "[Strengthened or removed]"

**Challenge 2:** ...

### Scores After Pass 2

| # | Criterion | Before | After | Change |
|---|-----------|--------|-------|--------|
...

### Updated Artifact
[Full rewritten artifact]
```

---

## Step 7: Re-Score After Pass 2

**If all criteria ≥ 9/10:** Skip to Step 10 (Output)

**If any criteria < 9/10:** Continue to Pass 3

---

## Step 8: Pass 3 - Adversarial Attacker

**Tone:** Hostile. Actively trying to break the argument.

**Personas:** Rotate through these adversarial readers:

### Persona 1: Impatient Executive
> "I have 3 minutes. Why should I care? What's the ask? Get to the point."

**Attacks:**
- Is the key message in the first 2 sentences?
- Can I understand the ask without reading everything?
- Is there anything I can skip?
- Am I being asked to do something or just FYI'd?

### Persona 2: Skeptical Customer
> "Why would I buy this? What's the ROI? Prove it works. My budget is tight."

**Attacks:**
- Where's the evidence this solves my problem?
- What's the specific benefit I'll see?
- How does this compare to doing nothing?
- What's the risk if this doesn't work?

### Persona 3: Overloaded End User
> "I'm slammed. Will this actually help me or just add work?"

**Attacks:**
- Is this solving my problem or your problem?
- How much of my time does this take?
- What happens if I ignore this?
- Did anyone actually ask me what I need?

**Process:**
1. Read artifact as each persona
2. Note where each persona would disengage, object, or dismiss
3. Strengthen those sections to survive the attack
4. If a section can't survive attack, remove or qualify it

**Output:**

```markdown
## Pass 3: Adversarial Attack

### Persona Attacks

**Impatient Executive:**
- Attack: "[What they'd say]"
- Vulnerable section: "[Text that fails]"
- Defense: "[How we strengthened it]"

**Skeptical Customer:**
- Attack: "[What they'd say]"
- Vulnerable section: "[Text that fails]"
- Defense: "[How we strengthened it]"

**Overloaded End User:**
- Attack: "[What they'd say]"
- Vulnerable section: "[Text that fails]"
- Defense: "[How we strengthened it]"

### Final Scores

| # | Criterion | Final Score |
|---|-----------|-------------|
...

**Overall: [sum]/100 ([percentage]%)**

### Updated Artifact
[Full rewritten artifact]
```

---

## Step 9: Final Validation

If after 3 passes any criterion is still below 9/10:

```markdown
## Quality Gate: NOT PASSED

**Criteria still below threshold:**
| Criterion | Score | Blocker |
|-----------|-------|---------|
| [Name] | X/10 | [Why it can't be fixed without more input] |

**Recommendation:**
[What the user needs to provide to fix remaining gaps - more evidence, clarification, decision, etc.]

**Ship anyway?**
[Assessment of whether it's good enough despite gaps]
```

Use AskUserQuestion:

```yaml
questions:
  - question: "Some criteria are still below 9/10. How do you want to proceed?"
    header: "Quality Gate"
    multiSelect: false
    options:
      - label: "Ship as-is"
        description: "Good enough, I'll address gaps later"
      - label: "Provide more input"
        description: "I'll give you what's missing to fix the gaps"
      - label: "Lower threshold"
        description: "Accept 8/10 as passing for remaining criteria"
```

---

## Step 10: Output

**Final deliverable:**

```markdown
# QA Loop Complete

**Artifact:** [filename]
**Type:** [type]
**Passes Required:** [1/2/3]

## Score Progression

| Criterion | Initial | Pass 1 | Pass 2 | Pass 3 | Final |
|-----------|---------|--------|--------|--------|-------|
| 1. [Name] | X | X | X | X | ✅ 9+ |
...

**Initial Score:** [X]/100 → **Final Score:** [Y]/100

## Changelog

### What Changed

1. **[Section/Criterion]:** [Before → After summary]
2. **[Section/Criterion]:** [Before → After summary]
...

### Why It's Better

- [Key improvement 1]
- [Key improvement 2]
- [Key improvement 3]

### What Survived Unchanged

- [Sections that were already strong]

---

## Polished Artifact

[FULL FINAL ARTIFACT HERE]
```

**File handling:**
- If input was a file path: Ask if user wants to overwrite or save as new file
- If inline: Output the polished artifact in the conversation

---

## Quality Standards Reference

### Vagueness Fixes

| Vague | Specific |
|-------|----------|
| "fast" | "< 200ms p95" |
| "improve" | "increase from X to Y" |
| "better UX" | "reduce clicks from 5 to 2" |
| "soon" | "by March 15" |
| "many users" | "73% of interviewed users" |
| "should work well" | "passes all acceptance criteria in test plan" |

### Structure Principles

1. **Most important first** - Don't bury the lede
2. **One idea per paragraph** - No compound paragraphs
3. **Topic sentences** - First sentence states the point
4. **So-what follows what** - Every fact has an implication
5. **Specific before general** - Example, then principle

### Word Economy Rules

**Cut:**
- "very", "really", "quite", "basically", "actually", "just"
- "in order to" → "to"
- "due to the fact that" → "because"
- "at this point in time" → "now"
- "it is important to note that" → [delete entirely]
- Sentences that repeat previous sentences

**Keep:**
- Specific numbers
- Direct quotes
- Named sources
- Concrete examples

---

## Edge Cases

### Artifact Too Short
If artifact is < 200 words, likely missing substance. Flag:
```
This artifact may be too brief to evaluate fully.
Missing sections that would typically appear:
- [Expected section 1]
- [Expected section 2]

Proceed with QA loop on existing content, or expand first?
```

### Artifact Too Long
If artifact is > 3000 words, may need restructuring not just editing. Flag:
```
This artifact is [X] words. Consider:
- Is this one document or several?
- What could be moved to an appendix?
- What's the 500-word version?

Proceed with full QA loop, or restructure first?
```

### Missing Evidence
If artifact makes claims but provides no quotes/data:
```
This artifact lacks evidence for key claims.
Either:
1. Add evidence (quotes, data, sources)
2. Qualify claims as assumptions ("We believe..." / "Hypothesis:")
3. Remove claims that can't be supported

Cannot reach 9/10 on Evidence Quality without #1 or #2.
```

---

## Example Invocations

**Polish a PRD:**
```
/qa-loop /path/to/my-feature-prd.md

Run the full loop and make this sharper before I share with engineering.
```

**Inline on just-generated synthesis:**
```
/user-discovery /path/to/transcript.docx
[... synthesis generated ...]

/qa-loop

Polish this before I share with the team.
```

**Quick stakeholder update:**
```
Here's my draft update for the quarterly review:

[draft text]

/qa-loop

Make this executive-ready.
```

---

## Tips for Best Results

**Before running /qa-loop:**
- Have a complete first draft (this polishes, doesn't create)
- Know your audience (affects scoring calibration)
- Accept that content may get cut

**During the loop:**
- Trust the process - it will feel aggressive
- The adversarial personas are intentionally harsh
- Good writing survives attacks; weak writing gets exposed

**After the loop:**
- Review the changelog to understand what changed
- The final artifact should feel tighter, not longer
- If something important got cut, add it back with evidence

---

## Skill Integration

**Typical workflow:**
```
/write-prd           → First draft PRD
/qa-loop             → Polish to 9/10

/hypothesis          → First draft hypothesis
/qa-loop             → Stress-test assumptions

/user-discovery      → Interview synthesis
/qa-loop             → Sharpen insights before sharing
```

**This skill does NOT:**
- Generate content from scratch (use other skills)
- Add missing sections (flags them, doesn't invent)
- Change your core argument (tightens expression of it)
- Make things longer (almost always makes things shorter)

---

*This skill implements the recursive self-improvement pattern: Generate → Evaluate → Diagnose → Improve → Repeat. It doesn't stop until the work actually hits the bar.*
