---
name: hypothesis
description: Use this skill when the user wants to generate a product hypothesis, explore a new concept, validate an opportunity, or needs to articulate and test an early-stage idea before user discovery. Outputs a structured hypothesis document with assumption mapping and interview guide.
version: 1.0.0
allowed-tools: [Read, Write, Edit, Glob, Grep, AskUserQuestion]
---

# Hypothesis Generator

Transform early-stage observations, feedback, or business problems into structured, testable product hypotheses with assumption mapping and validation plans.

## When to Use This Skill

Activate when user:
- Says "I have an idea", "explore this concept", "generate a hypothesis"
- Describes a market observation, customer signal, or business problem
- Wants to articulate an opportunity before committing resources
- Needs to structure fuzzy thinking into a testable hypothesis
- Mentions "top of funnel", "early stage", "concept exploration"

Do NOT activate for:
- Writing a PRD (use `/write-prd`)
- Analyzing an interview transcript (use `/user-discovery`)
- Tasks with engineering handoff (use `/prd-taskmaster`)
- Ideas that are already validated and ready for requirements

## Core Philosophy

> **Articulate Before You Build** - The cheapest way to test an idea is to write it down clearly enough that you can prove it wrong. A well-structured hypothesis saves weeks of building the wrong thing.

## Position in the PM Funnel

```
[Observation/Signal]
       |
       v
  /hypothesis  <-- YOU ARE HERE
       |
       v
  /user-discovery (validate with users)
       |
       v
  /write-prd (document requirements)
       |
       v
  /prd-taskmaster (engineering handoff)
```

## Workflow Overview

1. **Identify the Trigger** - What sparked this hypothesis?
2. **Discovery Interview** - 3 rounds of structured questions
3. **Generate Hypothesis** - Jobs-based statement with assumptions
4. **Map Assumptions** - Categorize by risk (desirability/feasibility/viability)
5. **Create Validation Plan** - Interview guide and kill criteria
6. **Output Document** - Complete hypothesis brief

---

## Step 1: Identify the Trigger

Ask what prompted this exploration:

```yaml
questions:
  - question: "What triggered this hypothesis? What did you observe or hear?"
    header: "Trigger Type"
    multiSelect: false
    options:
      - label: "Market observation"
        description: "Competitor move, industry trend, or market gap you noticed"
      - label: "Customer feedback"
        description: "Something users said, complained about, or requested"
      - label: "Business problem"
        description: "Leadership priority, strategic gap, or metric to improve"
      - label: "Technology opportunity"
        description: "New capability, integration, or technical possibility"
```

After selection, ask for details:

```
"Describe the trigger in 2-3 sentences. What specifically did you observe, hear, or identify?"
```

---

## Step 2: Discovery Interview

### Round 1: The Opportunity Space

```yaml
questions:
  - question: "Who might benefit from this? Who experiences the problem or need?"
    header: "Target User"
    multiSelect: false
    options:
      - label: "Existing user segment"
        description: "Current customers who have an unmet need"
      - label: "Adjacent user"
        description: "People similar to current users but not yet served"
      - label: "New market"
        description: "Entirely different user type we don't serve today"
      - label: "Internal team"
        description: "Employees, operators, or partners (not end customers)"

  - question: "What's the current state? How do these users handle this today?"
    header: "Current State"
    multiSelect: false
    options:
      - label: "Manual workaround"
        description: "They do it manually - spreadsheets, phone calls, sticky notes"
      - label: "Competitor solution"
        description: "They use a competitor or alternative product"
      - label: "Don't address it"
        description: "They live with the problem or ignore it"
      - label: "Internal tool"
        description: "They built something custom or use an internal system"
```

### Round 2: The Belief

```yaml
questions:
  - question: "What situation triggers the need? When does this problem become acute?"
    header: "Trigger Moment"
    multiSelect: false
    options:
      - label: "Time-based"
        description: "At a specific time (daily, weekly, quarterly)"
      - label: "Event-based"
        description: "When something happens (new customer, deadline, emergency)"
      - label: "Workflow-based"
        description: "During a specific task or process"
      - label: "Let me describe"
        description: "I'll explain the specific trigger"

  - question: "What outcome are users trying to achieve? What does success look like?"
    header: "Desired Outcome"
    multiSelect: false
    options:
      - label: "Save time"
        description: "Complete a task faster or with less effort"
      - label: "Reduce risk"
        description: "Avoid errors, failures, or negative outcomes"
      - label: "Enable capability"
        description: "Do something they couldn't do before"
      - label: "Improve quality"
        description: "Get better results from existing processes"
```

### Round 3: Confidence & Evidence

```yaml
questions:
  - question: "How confident are you in this hypothesis?"
    header: "Confidence"
    multiSelect: false
    options:
      - label: "Strong signal"
        description: "Multiple data points, direct user feedback, clear pattern"
      - label: "Moderate signal"
        description: "Some evidence but need more validation"
      - label: "Weak signal / hunch"
        description: "Intuition or single data point - needs significant validation"
      - label: "Pure speculation"
        description: "Interesting idea but no evidence yet"

  - question: "What evidence do you already have?"
    header: "Existing Evidence"
    multiSelect: true
    options:
      - label: "User quotes"
        description: "Direct statements from users about this problem/need"
      - label: "Usage data"
        description: "Analytics showing behavior patterns"
      - label: "Market research"
        description: "Industry reports, competitor analysis"
      - label: "None yet"
        description: "This is the starting point - no evidence gathered"
```

---

## Step 3: Generate Hypothesis Document

After completing the interview, generate a markdown document with this structure:

### Document Template

```markdown
# Hypothesis Brief: [Descriptive Title]

**Created:** [Today's date]
**Author:** [User or "Product Team"]
**Status:** Draft - Needs Validation
**Confidence:** [Strong/Moderate/Weak/Speculative]

---

## The Trigger

**Type:** [Market observation / Customer feedback / Business problem / Technology opportunity]

[2-3 sentence description of what sparked this hypothesis]

---

## Hypothesis Statement

### Jobs-Based Format

> **When** [situation/trigger moment]
> **[Target user]** needs to [capability/action]
> **So that** [desired outcome/benefit]

### Plain Language
[1-2 sentence restatement in conversational language]

---

## Current State

### How Users Handle This Today
[Description of current workarounds, alternatives, or coping mechanisms]

### Pain Points in Current State
1. [Pain point 1]
2. [Pain point 2]
3. [Pain point 3]

### Why This Matters Now
[Why is this hypothesis worth exploring at this moment? What changed?]

---

## Assumption Map

### Desirability Assumptions (Do users want this?)

| # | Assumption | Risk Level | Evidence Needed |
|---|------------|------------|-----------------|
| D1 | [Users actually experience this problem] | High/Med/Low | [What would prove this true/false] |
| D2 | [Users would switch from current solution] | High/Med/Low | [What would prove this true/false] |
| D3 | [This is a top priority for users] | High/Med/Low | [What would prove this true/false] |

### Feasibility Assumptions (Can we build this?)

| # | Assumption | Risk Level | Evidence Needed |
|---|------------|------------|-----------------|
| F1 | [Technical capability exists or can be built] | High/Med/Low | [What would prove this true/false] |
| F2 | [We have the skills/resources to execute] | High/Med/Low | [What would prove this true/false] |
| F3 | [Timeline is realistic] | High/Med/Low | [What would prove this true/false] |

### Viability Assumptions (Should we build this?)

| # | Assumption | Risk Level | Evidence Needed |
|---|------------|------------|-----------------|
| V1 | [Aligns with company strategy] | High/Med/Low | [What would prove this true/false] |
| V2 | [Business model works] | High/Med/Low | [What would prove this true/false] |
| V3 | [Competitive advantage exists] | High/Med/Low | [What would prove this true/false] |

### Riskiest Assumption
**[Assumption ID]:** [Statement of the single riskiest assumption that could kill this hypothesis]

---

## Kill Criteria

This hypothesis should be abandoned if:

1. **User evidence says no:** [Specific threshold, e.g., "<3 of 10 users express this problem unprompted"]
2. **Technical blocker:** [What would make this impossible to build]
3. **Business misalignment:** [What would make this not worth pursuing]
4. **Competitive dynamics:** [What market condition would invalidate this]

---

## Validation Plan

### Phase 1: Quick Validation (1-2 weeks)

**Objective:** Test the riskiest assumption before investing more time

**Method:** [User interviews / Data analysis / Prototype testing / Expert consultation]

**Sample:** [Who to talk to, how many]

**Success Criteria:** [What would move this forward vs. kill it]

### Phase 2: Deeper Discovery (if Phase 1 passes)

**Objective:** Understand the full problem space and solution requirements

**Method:** `/user-discovery` interviews with [target users]

**Output:** Validated JTBD, persona refinement, PRD readiness assessment

---

## Interview Guide

### Screening Questions
1. [Question to confirm they're the right user type]
2. [Question to confirm they have context on this problem space]

### Discovery Questions (Open-ended, don't lead)

**Understanding the Current State:**
1. "Tell me about the last time you [relevant activity]. Walk me through it."
2. "What's the hardest part about [current process]?"
3. "How do you currently handle [problem area]?"

**Exploring the Pain:**
4. "When [trigger situation] happens, what do you do?"
5. "What have you tried to solve this? What worked? What didn't?"
6. "If you could wave a magic wand, what would be different?"

**Validating Importance:**
7. "How often does this come up? Daily? Weekly? Rarely?"
8. "On a scale of 1-10, how painful is this? What makes it a [X]?"
9. "What would it mean for you if this problem was solved?"

**Testing Assumptions:**
10. "[Assumption D1 question - specific to hypothesis]"
11. "[Assumption D2 question - specific to hypothesis]"

### What to Listen For
- **Positive signals:** [Specific phrases or reactions that would support the hypothesis]
- **Negative signals:** [Specific phrases or reactions that would challenge the hypothesis]
- **Surprises:** [Things that would reshape the hypothesis]

---

## Existing Evidence

[List any evidence gathered before this hypothesis was formalized]

| Source | Evidence | Supports/Challenges |
|--------|----------|---------------------|
| [Source 1] | [What was observed/said] | Supports / Challenges |

---

## Next Steps

1. [ ] Schedule [N] user interviews with [target persona]
2. [ ] Review existing [data source] for supporting evidence
3. [ ] Validate [riskiest assumption] within [timeframe]
4. [ ] Decision point: Continue to /user-discovery or kill

---

## Appendix: Related Context

### Company/Product Context
[Any relevant background about how this fits into current strategy, existing products, or ongoing initiatives]

### Competitive Landscape
[Quick notes on how competitors address this, if known]

### Open Questions
| Question | Who Can Answer | Priority |
|----------|----------------|----------|
| [Question 1] | [Stakeholder] | High/Med/Low |

---

*Generated with /hypothesis skill. Next step: Validate assumptions, then use /user-discovery to synthesize findings.*
```

---

## Step 4: Review & Refine

After generating the document:

```yaml
questions:
  - question: "Would you like to refine any section?"
    header: "Refinement"
    multiSelect: true
    options:
      - label: "Sharpen the hypothesis statement"
        description: "Make the JTBD more specific or compelling"
      - label: "Add more assumptions"
        description: "Identify additional risks to test"
      - label: "Expand interview guide"
        description: "Add more discovery questions"
      - label: "Looks good - save it"
        description: "Document is ready"
```

---

## Output Location

Save the hypothesis brief to the user's specified location, or suggest:
- `hypotheses/[descriptive-slug]-hypothesis.md` if a `hypotheses/` folder exists
- `[descriptive-slug]-hypothesis.md` in current directory otherwise

---

## Tips for Best Results

**During Discovery:**
- Push for specificity - vague hypotheses can't be tested
- Listen for the user's own language to incorporate into the JTBD
- If they say "users" generically, push for which users specifically
- Note when confidence is low - that shapes the validation plan

**During Generation:**
- The riskiest assumption is the one that, if wrong, makes everything else irrelevant
- Kill criteria should be specific enough to actually trigger a decision
- Interview questions should NOT mention the solution - stay problem-focused

**Connecting to Other Skills:**
- After validation interviews, use `/user-discovery` to synthesize findings
- If hypothesis is validated, use `/write-prd` to document requirements
- This skill outputs a hypothesis; other skills consume it

---

## Example Invocations

**From a customer signal:**
```
/hypothesis

I keep hearing from power users that they want to share their configurations
with other teams. Three different customers mentioned this in the last month.
```

**From a business problem:**
```
/hypothesis

Leadership wants us to improve user retention. We think onboarding quality
might be a factor but we're not sure what specifically.
```

**From a market observation:**
```
/hypothesis

I noticed that [competitor] added a template marketplace and their community
engagement spiked. Could we do something similar?
```

**From a technology opportunity:**
```
/hypothesis

Engineering says we could now do real-time collaboration via WebSocket sync.
Not sure if that's actually valuable to users or just technically cool.
```

---

*This skill generates hypothesis documents for early-stage exploration. It does not validate hypotheses - that requires user research via `/user-discovery`.*
