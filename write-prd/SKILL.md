---
name: write-prd
description: Use this skill when the user asks to "write a PRD", "create a PRD", "help me with a PRD", "product requirements document", or wants to document product requirements for a feature or product. This skill uses an interview-driven approach to gather requirements and generate a structured PRD.
version: 5.0.0
allowed-tools: [Read, Write, Edit, Glob, Grep, AskUserQuestion]
---

# Write PRD - Interview-Driven PRD Generator

This skill creates PRDs through a structured interview process. It's tuned for Derek's product domains — primarily AI products, agents, and infrastructure — but works for any product.

## When to Use This Skill

Activate when user:
- Asks to write, create, or help with a PRD
- Wants to document product requirements
- Says "PRD", "product requirements document"
- Needs to create requirements for a new feature or product

Do NOT activate for:
- Technical documentation or API docs
- Project status updates
- Bug reports or tickets

## Core Philosophy

- **Problem First, Solution Second** — Obsess over the problem before prescribing solutions. Engineers should have room to solve creatively.
- **Interview First, Write Second** — A 15-minute interview produces a better PRD than guessing.
- **Every Word Earns Its Place** — If a sentence doesn't help someone build or decide, cut it.
- **Quantify Everything** — "Users struggle" is useless. "40% abandon at checkout" creates urgency.

---

## Vault Integration

### On startup:
1. **Check for existing work.** Glob `Ideas/Product Ideas/` for files matching the product name or concept. Read any matches — build on existing specs, PRFAQs, or concepts rather than starting from scratch.
2. **Pull context.** If the user mentions a product idea by name, search `Ideas/` broadly for related notes.

### On output:
1. **Save to vault.** Write the PRD to `Ideas/Product Ideas/[Product Name] - PRD V1.md`.
2. If a file already exists for that product, ask whether to overwrite or create V2/V3.

---

## Workflow

### Step 1: Gather Context

Before asking questions:
1. Search `Ideas/Product Ideas/` for existing docs on this product.
2. If found, read them and summarize what's already known.
3. Skip interview questions already answered by existing docs.
4. If user provides files, read those too.

### Step 2: Discovery Interview

Use AskUserQuestion for structured discovery. 5 rounds. Adapt — skip what's already known, follow up when answers are vague.

#### Round 1: Problem Validation

```yaml
questions:
  - question: "How do users solve this problem today?"
    header: "Current State"
    multiSelect: false
    options:
      - label: "No solution exists"
        description: "Users can't do this — they give up or go without"
      - label: "Manual workarounds"
        description: "Spreadsheets, emails, manual processes cobbled together"
      - label: "Competitor products"
        description: "Other tools that don't fully meet their needs"
      - label: "Internal tools"
        description: "Something exists but it's inadequate"

  - question: "How do we know this is a real problem?"
    header: "Evidence"
    multiSelect: true
    options:
      - label: "User interviews/research"
        description: "Talked to users who describe this pain"
      - label: "Support tickets/complaints"
        description: "Users are actively asking for this"
      - label: "Usage data"
        description: "Analytics show users struggling or dropping off"
      - label: "Assumption - needs validation"
        description: "We believe this but haven't validated"
```

#### Round 2: User & Context

```yaml
questions:
  - question: "Who feels this pain most acutely? (Primary user for V1)"
    header: "Target User"
    multiSelect: false
    options:
      - label: "End user/consumer"
        description: "Individual people using the product directly"
      - label: "Business user"
        description: "Employees using it for their job (not technical)"
      - label: "Technical user"
        description: "Developers, engineers, or IT staff"
      - label: "Multiple personas"
        description: "Two or more user types with equal priority"

  - question: "What triggers the user to need this?"
    header: "Trigger"
    multiSelect: false
    options:
      - label: "Time-based"
        description: "Part of a regular workflow (daily, weekly)"
      - label: "Event-based"
        description: "Triggered by something happening"
      - label: "Goal-based"
        description: "Trying to achieve a specific outcome"
      - label: "Pain-based"
        description: "Frustrated and looking for relief"
```

#### Round 3: Strategic Fit & Timing

```yaml
questions:
  - question: "Why build this now?"
    header: "Timing"
    multiSelect: false
    options:
      - label: "Customer commitment"
        description: "Promised to a customer or required for a deal"
      - label: "Competitive pressure"
        description: "Competitors have this or market is moving"
      - label: "Technical opportunity"
        description: "New capability makes this possible/easier now"
      - label: "Accumulated demand"
        description: "Requests have piled up — can't ignore anymore"
      - label: "No specific urgency"
        description: "Important but not time-sensitive"

  - question: "Painkiller or vitamin?"
    header: "Severity"
    multiSelect: false
    options:
      - label: "Painkiller (must-have)"
        description: "Solves acute pain — users desperately need this"
      - label: "Vitamin (nice-to-have)"
        description: "Makes things better but users can live without it"
      - label: "Strategic bet"
        description: "Unlocks future opportunity even if not urgent now"
```

#### Round 4: Success & Trade-offs

```yaml
questions:
  - question: "What does success look like? (Primary metric)"
    header: "Success"
    multiSelect: false
    options:
      - label: "Adoption/usage"
        description: "X users actively using this feature"
      - label: "Task completion"
        description: "Users can complete [workflow] successfully"
      - label: "Time savings"
        description: "Reduces time to do X from Y to Z"
      - label: "Revenue impact"
        description: "Increases conversion, retention, or deal size"
      - label: "Let me specify"
        description: "I have a specific metric in mind"

  - question: "What are we explicitly NOT doing in V1?"
    header: "Non-Goals"
    multiSelect: true
    options:
      - label: "Power-user features"
        description: "Advanced capabilities that can wait"
      - label: "Integrations"
        description: "Connections to other tools/systems"
      - label: "Additional platforms"
        description: "Focus on one surface first"
      - label: "Edge cases"
        description: "Handle the 80% case, not every scenario"
      - label: "Let me specify"
        description: "I'll list specific non-goals"
```

#### Round 5: AI-Specific & Risks

**This round adapts to the product domain.** For AI products (the default), use these questions. For non-AI products, skip the AI-specific questions and ask general risk questions instead.

```yaml
questions:
  - question: "What's the hardest or riskiest part?"
    header: "Key Risk"
    multiSelect: true
    options:
      - label: "Model quality/reliability"
        description: "LLM output quality, hallucinations, consistency"
      - label: "Eval strategy"
        description: "How do we know the AI is working correctly?"
      - label: "Data pipeline"
        description: "Getting the right data in the right format"
      - label: "User trust/adoption"
        description: "Will users trust AI-generated output?"
      - label: "Cost/latency"
        description: "Inference costs or response time constraints"
      - label: "Scope creep"
        description: "Could easily grow beyond what's manageable"
      - label: "Dependencies"
        description: "Relies on other teams, APIs, or model providers"

  - question: "What level of detail does this PRD need?"
    header: "Detail"
    multiSelect: false
    options:
      - label: "Problem-focused (Recommended)"
        description: "Define the problem and success criteria — let eng solve it"
      - label: "Solution-outlined"
        description: "Include high-level solution approach and key flows"
      - label: "Fully specified"
        description: "Detailed requirements, edge cases, acceptance criteria"
```

---

## Step 3: Identify Domain Standards

After the interview, before writing the PRD, identify which industry standards, regulations, and domain conventions govern each requirement area. This prevents vague AC like "use standard format" and ensures engineers get specific, implementable defaults.

### Process

1. **List each JTBD from the interview**
2. **For each JTBD, ask:** "Is there a standard, regulation, or domain convention that governs how this should work?"
3. **If yes:** Research the specific standard and resolve defaults (format, values, thresholds)
4. **If unknown:** Flag as Open Question — "Which standard governs [behavior]? Engineering to confirm."
5. **If no standard applies:** Focus AC on specific behaviors (response times, data validation, state management)

### What to Look For

| Category | Examples |
|----------|----------|
| **Data formats** | How must data be structured? (schemas, file formats, encoding, coordinate systems) |
| **Regulatory compliance** | What laws or regulations apply? (HIPAA, SOX, GDPR, PCI DSS, ADA/WCAG) |
| **Industry standards** | What bodies define the conventions? (ISO, IEEE, W3C, ACORD, HL7) |
| **Domain conventions** | What do practitioners expect by default? (unit systems, display formats, terminology) |
| **Interoperability** | What systems must this integrate with? What protocols/APIs do they use? |

### Examples Across Domains

| Domain | Requirement Area | Vague AC | Standards-Backed AC |
|--------|-----------------|----------|-------------------|
| Healthcare | Patient records | "Industry-standard format" | "HL7 FHIR R4, HIPAA-compliant PHI handling" |
| Finance | Transaction reporting | "Regulatory compliance" | "ISO 20022 message format, SOX audit trail requirements" |
| E-commerce | Payment processing | "Secure payment handling" | "PCI DSS Level 1, 3D Secure 2.0 for card-not-present" |
| Insurance | Claims processing | "Compliant data format" | "ACORD XML standard, form ACORD 125 for commercial lines" |
| AI products | Model outputs | "Accurate responses" | "BLEU score >0.7 for translation, <5% hallucination rate per eval suite" |

**The principle:** If a standard, regulation, or industry convention governs a behavior, the AC must name it and specify the default — never leave it as "standard" or "compliant."

---

## Step 4: Generate PRD

After the interview and standards mapping, generate using this template. Scale sections to the detail level requested — not every project needs every section filled out.

```markdown
# [Product Name] - Product Requirements Document

**Version:** 1.0
**Date:** [Today's date]
**Author:** Derek Cedarbaum
**Status:** Draft

---

## TL;DR

[3-5 bullets. The problem, the approach, the primary success metric, target timeline.]

---

## 1. Problem Statement

### The Problem
[2-3 sentences. Quantify the pain. No solutions here.]

### How Users Solve This Today
[Current workarounds, competitor products, or why they go without]

### Why This Matters Now
[Strategic urgency. Cost of waiting.]

### Evidence
[User research, support data, analytics. How do we KNOW this is real?]

---

## 2. Goals & Success Metrics

### Primary Goal
[One sentence.]

### Success Metrics
| Metric | Current | Target | Timeframe |
|--------|---------|--------|-----------|
| [Primary] | [Baseline] | [Target] | [When] |
| [Leading indicator] | [Baseline] | [Target] | [When] |

### Kill Criteria
[What signals tell us to stop?]

---

## 3. Target User

### Primary Persona: [Name/Role]
**Who:** [Specific role and context]
**Trigger:** "When [situation], I need to [action], so I can [outcome]."
**Today:** [Current workflow]
**Quote:** *"[Representative frustration quote]"*

---

## 4. Solution Overview

### Approach
[High-level direction. The concept, not a feature list.]

### Design Principles
| Principle | Implication |
|-----------|-------------|
| [e.g., "Speed over completeness"] | [e.g., "Ship MVP, iterate on usage data"] |

---

## 5. Requirements

| Priority | Meaning |
|----------|---------|
| **P0** | Must have — blocks launch |
| **P1** | Should have — launch is weaker without it |
| **P2** | Nice to have — not critical |

### [Category]

**[Requirement]** (P0/P1/P2)
*Story:* As a [role], I want to [action] so that [benefit].
*Acceptance Criteria:*
- [ ] [Specific, testable]
- [ ] [Specific, testable]

---

## 6. User Flows

> High-level only. Design owns detailed interactions.

### Flow: [Name]
1. User [trigger] → [Screen]
2. User [action] → [Response]
3. [Decision point] →
   ├─ Yes: [Next step]
   └─ No: [Alternative]

---

## 7. Non-Goals

| Item | Why Deferred |
|------|--------------|
| [Feature] | [Specific rationale] |

---

## 8. Assumptions & Risks

### Assumptions
| Assumption | If Wrong | Validation |
|------------|----------|------------|
| [Belief] | [Impact] | [How to test] |

### Risks
| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| [Risk] | H/M/L | H/M/L | [Plan] |

---

## 9. Open Questions

| Question | Owner | Decide By |
|----------|-------|-----------|
| [Unresolved item] | [Who] | [Date] |
```

### AI Product Sections (Include When Relevant)

For AI products, add these sections after Requirements:

```markdown
## AI Architecture (High-Level)

### Model Strategy
[Which models, why, hosted vs. API, fine-tuned vs. prompted]

### Eval Strategy
[How do we measure AI output quality? What's ground truth? Human eval, LLM-as-judge, automated metrics?]

### Data Requirements
[What data does the system need? Where does it come from? Privacy/compliance constraints?]

### Feedback Loops
[How does the product get better over time? User corrections, implicit signals, active learning?]

### Failure Modes
[What happens when the AI is wrong? How does the user recover? What's the blast radius?]
```

---

### Writing Acceptance Criteria (For Engineers & Designers)

AC are the contract between PM, engineering, and design. Great criteria answer: "How do we know when this is done?"

**What Engineers Need:**
- Specific boundaries (numbers, not adjectives: "< 3 seconds" not "fast")
- Edge cases called out (what happens when X fails? when list is empty?)
- Data requirements (inputs, formats, required vs. optional)
- System interactions (triggers, downstream effects)
- Testable conditions (can write an automated test against it)
- Standards references (when a standard governs behavior, cite it by name)

**What Designers Need:**
- User context (what state is the user in?)
- Visual requirements (what's visible, hierarchy)
- Interaction model (click, drag, hover, keyboard)
- Feedback requirements (loading, success, error, empty states)
- Accessibility (screen reader, keyboard nav, color contrast)

**Two Formats:**

**Format 1: Rule-Based (for discrete behaviors)**
```
- [ ] Upload accepts: PNG, JPG, WebP (max 10MB)
- [ ] Preview generates in <2 seconds
- [ ] Maximum 20 items per workspace (show warning at 15)
- [ ] Delete requires confirmation modal
```

**Format 2: Scenario-Based (for workflows)**
```
GIVEN I have an unsaved draft with 5 items
WHEN I click "Save"
THEN I see a modal with: name field (required), description (optional)
AND name field is auto-focused
AND I cannot save until name is 3+ characters
AND saving shows spinner, then success toast, then returns to editor
```

**Standards-Backed Criteria:**
```
Bad:  "Data is handled securely"
Good: "PHI display follows HIPAA minimum necessary; lab results use HL7 FHIR R4"

Bad:  "Payment processing is secure"
Good: "Card data per PCI DSS Level 1; no PAN stored post-authorization; 3D Secure 2.0 for CNP"

Bad:  "Accessible to all users"
Good: "WCAG 2.1 AA; all interactive elements keyboard-navigable; color contrast ratio ≥4.5:1"
```

---

## Step 5: Review & Refine

```yaml
questions:
  - question: "What would you like me to refine?"
    header: "Feedback"
    multiSelect: true
    options:
      - label: "Sharpen problem statement"
        description: "Make the problem more specific or compelling"
      - label: "Clarify success metrics"
        description: "Make metrics more specific or add targets"
      - label: "Add/change requirements"
        description: "More features or adjust priorities"
      - label: "Expand AI architecture"
        description: "More detail on model, eval, or data strategy"
      - label: "Expand risks/assumptions"
        description: "Document more unknowns"
      - label: "Looks good"
        description: "Ready for review"
```

---

## Quality Checklist

### Content
- [ ] Problem is quantified with specific numbers
- [ ] Evidence proves this is real (not assumed)
- [ ] Success metrics have baseline → target → timeframe
- [ ] Kill criteria defined
- [ ] Non-goals include things stakeholders might expect
- [ ] Risks have mitigation plans

### Writing
- [ ] TL;DR is ≤5 bullets
- [ ] Problem statement ≤4 sentences
- [ ] No solutions in the problem section
- [ ] Personas use specific roles (not "users")
- [ ] Acceptance criteria are testable (pass/fail)
- [ ] No filler words ("very", "really", "quite", "basically")

### Acceptance Criteria Quality
- [ ] Every criterion has specific boundaries (numbers, not adjectives)
- [ ] Edge cases called out (empty states, errors, max limits)
- [ ] Data requirements specified (inputs, formats, required vs. optional)
- [ ] An engineer could write a test against each criterion
- [ ] A designer could create mockups without asking questions
- [ ] Where a standard governs behavior, it's cited by name with defaults
- [ ] Domain standards research was performed (Step 3)

### Alignment Test
- [ ] Could an engineer start building from this tomorrow?
- [ ] Could a designer start wireframing from this tomorrow?
- [ ] Would two engineers reading this build the same thing?
- [ ] If requirements conflict, does the PRD help prioritize?

### AI-Specific (when applicable)
- [ ] Eval strategy defined — how do we know the AI works?
- [ ] Failure modes documented — what happens when AI is wrong?
- [ ] Feedback loops described — how does it improve over time?
- [ ] Model/data requirements clear enough for eng to estimate
