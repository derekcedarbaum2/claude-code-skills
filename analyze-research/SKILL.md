---
name: analyze-research
description: Use this skill when the user wants to analyze multiple user interviews to identify patterns, prioritize requirements, or synthesize insights across research sessions. Reads Interview Snapshots, JTBD extractions, and raw transcripts to generate cross-interview pattern analysis and prioritized requirements.
version: 1.0.0
allowed-tools: [Read, Write, Edit, Glob, Grep, AskUserQuestion]
---

# Cross-Interview Research Analyzer

Analyze multiple user interviews to identify meaningful patterns, surface contradictions, and generate prioritized requirements. This skill works with outputs from the `synthesize-interviews` skill plus raw transcripts to provide evidence-based requirement prioritization.

## When to Use This Skill

Activate when user:
- Has multiple Interview Snapshots or synthesis outputs to analyze
- Wants to identify patterns across interviews
- Says "analyze research", "prioritize requirements", "find patterns"
- Needs to aggregate insights from multiple discovery sessions
- Wants to validate assumptions across user segments

Do NOT activate for:
- Single interview analysis (use synthesize-interviews)
- Writing PRDs (use write-prd after this skill)
- Meeting summaries (direct prompt)

## Core Philosophy

> **Patterns Over Anecdotes** - One user's opinion is a data point. Three users saying the same thing is a pattern. Patterns drive requirements.

> **Frequency ≠ Importance** - A single "this completely changed how I work" insight can outweigh five users mentioning a minor annoyance. Weight by severity × frequency × strategic fit.

> **Contradictions Are Signals** - When users disagree, it's often a segmentation opportunity, not noise. Surface contradictions, don't hide them.

> **Evidence Strength Matters** - P0 requires strong evidence (3+ users, high severity). P2 with weak evidence should be flagged for validation.

---

## Workflow Overview

```
1. GATHER
   ├── Read all Interview Snapshots
   ├── Read JTBD extractions (if separate)
   └── Read raw transcripts (for quote validation)

2. MAP
   ├── Extract all JTBDs across interviews
   ├── Normalize job statements
   └── Tag by user type, segment, product area

3. ANALYZE
   ├── Count frequency by job/theme
   ├── Assess severity (critical → nice-to-have)
   ├── Identify contradictions
   └── Segment by user type / platform

4. PRIORITIZE
   ├── Calculate Evidence Score
   ├── Apply strategic alignment (value pillars)
   └── Flag low-confidence items

5. OUTPUT
   ├── Pattern Report
   └── Prioritized Requirements
```

---

## Step 1: Gather Input

Read all research materials provided:

```
If user provides files/folders:
  1. Read all Interview Snapshots (look for "Interview Snapshot" in filename)
  2. Read JTBD extractions or synthesis reports
  3. Read raw transcripts (for quote validation)
  4. Count: N interviews, N participants, date range
  5. Note user types and segments represented

If files not provided:
  1. Ask user to provide folder path or file list
  2. Search common locations (project folder, Desktop)
```

**Expected Input Formats:**
- Interview Snapshots (from synthesize-interviews skill)
- Full Synthesis Reports (from synthesize-interviews skill)
- JTBD Extractions (from synthesize-interviews skill)
- Raw transcripts (for validation)

---

## Step 2: Understand Context

Use AskUserQuestion to confirm analysis parameters:

```yaml
questions:
  - question: "What product area does this research cover?"
    header: "Product"
    multiSelect: false
    options:
      - label: "Core product"
        description: "Primary product offering"
      - label: "New feature"
        description: "Feature being explored or developed"
      - label: "Adjacent product"
        description: "Related product or extension"
      - label: "Platform / infrastructure"
        description: "Underlying platform capabilities"
      - label: "Cross-product"
        description: "Research spans multiple products"

  - question: "What should drive prioritization?"
    header: "Priority Framework"
    multiSelect: true
    options:
      - label: "Evidence strength (Recommended)"
        description: "Frequency × Severity = higher priority"
      - label: "Value pillar alignment"
        description: "Acquisition / Engagement / Retention fit"
      - label: "Segment coverage"
        description: "Requirements that span multiple user segments"
      - label: "User type breadth"
        description: "Requirements from multiple user types (admin, power user, etc.)"
```

---

## Step 3: Analysis Process

### 3.1 Job Extraction and Normalization

For each Interview Snapshot or synthesis, extract:

```
Job Statement: {When/I want to/So that}
Source: {Participant ID, e.g., "Sarah Chen"}
User Type: {Admin, Power User, End User, Operator, Stakeholder}
Segment: {Enterprise, SMB, Consumer, Internal}
Product Area: {Core, Feature, Adjacent}
Key Quote: {Supporting evidence}
Suggested Priority: {From original synthesis}
```

**Normalization Rules:**
- Merge near-duplicate jobs (same intent, different wording)
- Preserve distinct jobs even if similar (note nuance)
- Tag segment-specific variants

### 3.2 Frequency Analysis

Create a frequency matrix:

| Job | Total Mentions | By User Type | By Segment |
|-----|----------------|--------------|------------|
| Load preset templates | 4/5 | Admin: 3, Power User: 1 | Enterprise: 2, SMB: 2 |
| Configure custom workflows | 3/5 | Admin: 2, Operator: 1 | Enterprise: 2, SMB: 1 |

**Frequency Thresholds:**
- **Strong pattern:** 3+ users (or 60%+ of sample)
- **Emerging pattern:** 2 users (40%+ of sample)
- **Anecdote:** 1 user (flag for validation)

### 3.3 Severity Assessment

For each job, assess severity based on evidence:

| Severity | Indicators |
|----------|------------|
| **Critical** | "I can't do my job without this", blocks workflow, causes errors |
| **High** | Significant time waste, frequent frustration, workaround required |
| **Medium** | Noticeable friction, occasional frustration |
| **Low** | Minor inconvenience, "would be nice" |

**Evidence for Severity:**
- Emotional language in quotes ("frustrating", "waste of time", "impossible")
- Workaround complexity (manual process, dependency on other teams)
- Frequency of occurrence (daily vs. occasionally)

### 3.4 Contradiction Analysis

Surface conflicting needs:

```markdown
### Contradiction: Templates vs. Flexibility

**User Group A (New Users / SMB):**
> "I'd want it all pre-built and ready to go... there's not a whole lot of customization needed. Just give me the template." — P1, SMB Admin

**User Group B (Power Users / Enterprise):**
> "We need to build custom workflows on the fly for every client engagement" — P4, Enterprise Power User

**Interpretation:**
This is a segmentation signal, not a conflict. New/SMB users prioritize templates. Enterprise power users need flexibility. V1 can target one segment.

**Recommendation:**
Target template-first users first ("Start Lean"). Add flexibility in V2.
```

### 3.5 Strategic Alignment

Map each job to value pillars:

| Job | Acquisition | Engagement | Retention |
|-----|------------|------------|-----------|
| Load preset templates | ✓ | ✓ | |
| Reduce setup time | | ✓ | |
| Advanced customization | | | ✓ |

---

## Step 4: Prioritization Framework

### Evidence Score Calculation

```
Evidence Score = (Frequency × Severity) + Strategic Alignment Bonus

Where:
- Frequency: 1 (anecdote) / 2 (emerging) / 3 (strong pattern)
- Severity: 1 (low) / 2 (medium) / 3 (high) / 4 (critical)
- Strategic Bonus: +1 if aligns with current quarter's value pillar focus
```

### Priority Assignment

| Priority | Evidence Score | Confidence |
|----------|----------------|------------|
| **P0** | 9+ | High - multiple users, critical/high severity |
| **P1** | 5-8 | Medium - pattern exists, moderate severity |
| **P2** | 3-4 | Low - emerging signal, needs validation |
| **Needs Validation** | 1-2 | Anecdote - interesting but unvalidated |

### Confidence Flags

Flag items with:
- **[Low N]** - Based on 1 user only
- **[Single Segment]** - Only validated in one user segment
- **[Contradicted]** - Other users expressed opposite need
- **[Assumed]** - Inferred from behavior, not explicitly stated

---

## Step 5: Output Generation

Generate two outputs:

### Output A: Pattern Report

```markdown
# Cross-Interview Pattern Analysis: [Product Area]

**Date:** [Generated date]
**Source:** [N] interviews, [date range]
**Participants:** [List with user types and segments]
**Product Area:** [Product or feature]

---

## Executive Summary

[3-5 bullets: Strongest patterns, key contradictions, strategic implications]

---

## Research Coverage

### Participants
| ID | Name | User Type | Segment | Interview Date |
|----|------|-----------|---------|----------------|
| P1 | [Name] | Admin | Enterprise | [Date] |
| P2 | [Name] | Power User | SMB | [Date] |

### Coverage Gaps
- [ ] No consumer users interviewed
- [ ] Enterprise perspective limited to 1 participant
- [ ] No operator interviews

---

## Pattern Analysis

### Strong Patterns (3+ users)

#### Pattern: [Pattern Name]
**Frequency:** [X/Y users] | **Severity:** [Critical/High/Medium/Low]
**User Types:** [Admin, Power User, etc.] | **Segments:** [Enterprise, SMB, etc.]

**Evidence:**
> "[Quote]" — P1, [Name]
> "[Quote]" — P2, [Name]
> "[Quote]" — P3, [Name]

**Interpretation:** [What this means for product]

---

### Emerging Patterns (2 users)

#### Pattern: [Pattern Name]
**Frequency:** [X/Y users] | **Needs Validation:** Yes
...

---

### Contradictions

#### [Contradiction Title]
**Group A says:** [Summary with quote]
**Group B says:** [Summary with quote]
**Segmentation Insight:** [What this reveals about user segments]
**Recommendation:** [How to handle in product]

---

## Segment-Specific Findings

| Finding | Enterprise | SMB | Consumer |
|---------|-----------|-----|----------|
| Templates preferred | ✓ | ✓ | ? |
| Custom workflows needed | ✓ | — | — |

---

## User Type Findings

| Finding | Admin | Power User | End User | Operator |
|---------|-------|------------|----------|----------|
| Time-constrained | ✓ | — | — | ✓ |
| Needs customization | — | ✓ | — | — |

---

## Quote Bank by Theme

### On [Theme 1]
> "[Quote]" — P1, [Context]
> "[Quote]" — P2, [Context]

### On [Theme 2]
> "[Quote]" — P3, [Context]

---

## Open Questions for Follow-Up

| Question | Why It Matters | Suggested Source |
|----------|----------------|------------------|
| [Question from research] | [Impact] | [Who to ask] |

---

*Generated using analyze-research skill v1.0.0*
```

---

### Output B: Prioritized Requirements

```markdown
# Prioritized Requirements: [Product Area]

**Date:** [Generated date]
**Source:** [N] interviews
**Ready for PRD:** Yes (P0/P1) / Partial (needs validation)

---

## Evidence Score Legend

| Score | Meaning |
|-------|---------|
| 9+ | P0 - Strong evidence, must have |
| 5-8 | P1 - Pattern exists, should have |
| 3-4 | P2 - Emerging signal, nice to have |
| 1-2 | Needs validation before prioritizing |

---

## P0 Requirements (Strong Evidence)

### Job: [Job Title]
**Evidence Score:** [X] (Frequency: [X/Y], Severity: [Critical/High])

**When** [situation/trigger]
**I want to** [action/capability]
**So that** [outcome/benefit]

**Evidence:**
| Source | User Type | Segment | Quote |
|--------|-----------|---------|-------|
| [Name] | Admin | Enterprise | "[Quote]" |
| [Name] | Power User | SMB | "[Quote]" |
| [Name] | Admin | SMB | "[Quote]" |

**Value Pillar:** [Acquisition / Engagement / Retention]

**Acceptance Criteria (Suggested):**
- [ ] [Criterion with specific boundary]
- [ ] [Criterion with specific boundary]

**Confidence:** High
**Segments:** Enterprise, SMB (validated)

---

### Job: [Job Title]
[Repeat structure]

---

## P1 Requirements (Moderate Evidence)

### Job: [Job Title]
**Evidence Score:** [X] (Frequency: [X/Y], Severity: [Medium/High])
**Confidence:** Medium [Single Segment]

[Same structure as P0]

---

## P2 Requirements (Emerging Signal)

### Job: [Job Title]
**Evidence Score:** [X] (Frequency: [X/Y], Severity: [Low/Medium])
**Confidence:** Low [Low N]

[Same structure]

---

## Needs Validation

These requirements are interesting but lack sufficient evidence:

### Job: [Job Title]
**Evidence Score:** [X] | **Flag:** [Low N / Contradicted / Assumed]
**Source:** [Single participant]
**Why It's Interesting:** [Rationale]
**Validation Needed:** [What to ask, who to ask]

---

## Requirements NOT Validated

These hypotheses were not supported by research:

| Hypothesis | Evidence | Conclusion |
|------------|----------|------------|
| "Users want to customize every workflow" | 0/5 users | Invalidated - templates preferred |
| [Hypothesis] | [Evidence] | [Conclusion] |

---

## Summary

| Priority | Count | Confidence |
|----------|-------|------------|
| P0 | [X] | High |
| P1 | [X] | Medium |
| P2 | [X] | Low |
| Needs Validation | [X] | — |

---

## Next Steps

1. **For PRD:** Import P0 and P1 requirements directly
2. **For Validation:** Schedule interviews to validate P2 and flagged items
3. **Coverage Gaps:** [List user types or segments not yet interviewed]

---

*Generated using analyze-research skill v1.0.0*
```

---

## Output Location

Save outputs to:
- **Pattern Report:** `[Product] - Pattern Analysis [Date].md`
- **Prioritized Requirements:** `[Product] - Prioritized Requirements [Date].md`

Suggest saving in the product folder or research folder.

---

## Step 6: Review & Refine

After generating outputs:

```yaml
questions:
  - question: "What would you like me to refine?"
    header: "Feedback"
    multiSelect: true
    options:
      - label: "Adjust priority scores"
        description: "Change weighting or thresholds"
      - label: "Expand contradiction analysis"
        description: "Go deeper on conflicting needs"
      - label: "Add segment breakdown"
        description: "More detail by user segment"
      - label: "Add user type breakdown"
        description: "More detail by user type"
      - label: "Simplify for stakeholders"
        description: "Executive summary version"
      - label: "Looks good"
        description: "Ready to use for PRD"
```

---

## Quality Checklist

### Evidence Quality
- [ ] Every P0 has 3+ user sources
- [ ] Quotes are verbatim with attribution
- [ ] User type and segment noted for each source
- [ ] Contradictions surfaced, not hidden

### Prioritization Quality
- [ ] Evidence scores are justified
- [ ] Severity based on user language, not assumption
- [ ] Low-confidence items flagged
- [ ] Strategic alignment considered

### Coverage
- [ ] Noted which user types are represented
- [ ] Noted which segments are represented
- [ ] Identified coverage gaps for future research

### Actionability
- [ ] P0/P1 ready for PRD import
- [ ] P2 has validation plan
- [ ] Contradictions have recommendations

---

## Domain Reference

### User Types
| Type | Description | Typical Needs |
|------|-------------|---------------|
| **Admin** | Manages settings, team access, configuration | Efficiency, control, templates |
| **Power User** | Daily heavy user, builds complex workflows | Flexibility, customization, speed |
| **End User** | Regular user, consumes outputs | Simplicity, reliability, guidance |
| **Operator** | Manages ongoing operations | Monitoring, quick actions, automation |
| **Stakeholder** | Reviews outputs, makes decisions | Summaries, metrics, clarity |

### Value Pillars
| Pillar | Description |
|--------|-------------|
| **Acquisition** | Attract and convert new users |
| **Engagement** | Increase active usage and depth |
| **Retention** | Keep users and reduce churn |

### JTBD Categories
1. Content Configuration
2. Workflow Design
3. Templates & Presets
4. Data Management
5. Export & Integration
6. Collaboration & Sharing
7. Environment & Settings
8. User Self-Service

---

## Integration with Other Skills

This skill's output feeds into:
- **write-prd** - Import prioritized requirements directly into PRD
- **synthesize-interviews** - When new interviews are conducted, re-run analysis

---

## Tips for Better Analysis

1. **Include coverage gaps** - Note which user types and segments are missing
2. **Preserve nuance** - Don't over-merge jobs that have subtle differences
3. **Contradiction ≠ conflict** - Contradictions reveal segments
4. **Validate before P0** - If you only have 1-2 users, flag for validation
5. **Strategic fit matters** - A P2 job that aligns perfectly with company strategy may deserve P1
