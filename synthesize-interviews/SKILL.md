---
name: synthesize-interviews
description: Use this skill when the user wants to analyze user interviews, synthesize research findings, extract insights from transcripts, or process user research data. Transforms raw interview transcripts and notes into structured insights including pain points, patterns, opportunities, and Jobs to Be Done in standard JTBD format.
version: 2.0.0
allowed-tools: [Read, Write, Edit, Glob, Grep, AskUserQuestion]
---

# User Interview Synthesizer

Transform raw interview transcripts and research notes into actionable insights for product development. Based on best practices from Teresa Torres (Interview Snapshots), Nielsen Norman Group (Thematic Analysis), and Jobs to Be Done methodology.

## When to Use This Skill

Activate when user:
- Has interview transcripts to analyze (users, admins, power users, operators)
- Wants to synthesize user research for product decisions
- Says "analyze interviews", "synthesize research", "extract insights"
- Needs to find patterns across user conversations
- Wants to create interview snapshots

Do NOT activate for:
- Writing PRDs (use write-prd skill)
- Competitive analysis (different skill)
- Survey data with only quantitative responses

## Core Philosophy

> **Quotes Are Gold** - Verbatim quotes from users are the most powerful evidence. Capture exact words. A single memorable quote can align an entire product team.

> **Patterns Over Anecdotes** - One user's opinion is a data point. Three users saying the same thing is a pattern. Patterns drive requirements.

> **Separate Observation from Interpretation** - First capture what users said and did. Then interpret what it means. Don't conflate the two.

> **Jobs to Be Done** - Frame insights as jobs: "When [situation], I want to [action], so that [outcome]." This connects directly to PRD requirements.

---

## Workflow Overview

1. **Gather Input** - Read transcripts, notes, or research files
2. **Understand Context** - Ask about research goals and participant details
3. **Analyze** - Identify themes, patterns, and opportunities
4. **Generate Output** - Create structured synthesis with JTBD format
5. **Refine** - Iterate based on user feedback

---

## Step 1: Gather Input

Read all provided research materials:

```
If user provides files/folders:
  1. Read all transcripts and notes using Read tool
  2. Count number of participants/interviews
  3. Note any metadata (dates, participant info, role, organization)
  4. Summarize the scope of data provided

If no files provided:
  1. Ask user to provide transcripts or paste content
  2. Clarify what format the data is in
```

**Supported Input Formats:**
- Interview transcripts (users, admins, power users, operators, stakeholders)
- Meeting notes from user conversations
- Discovery call recordings/transcripts
- Field observation notes from site visits
- Feedback from demos or evaluations

---

## Step 2: Understand Context

Use AskUserQuestion to understand the research context:

```yaml
questions:
  - question: "What type of research is this?"
    header: "Research Type"
    multiSelect: false
    options:
      - label: "Discovery"
        description: "Exploring problem space, understanding user workflows"
      - label: "Validation"
        description: "Testing product concepts or prototypes with users"
      - label: "Requirements"
        description: "Gathering specific needs for a product or feature"
      - label: "Continuous"
        description: "Ongoing user conversations (Teresa Torres style)"
      - label: "Mixed/Other"
        description: "I'll describe the research context"

  - question: "Which product area does this relate to?"
    header: "Product"
    multiSelect: false
    options:
      - label: "Core product"
        description: "Primary product offering"
      - label: "New feature"
        description: "Feature being explored or developed"
      - label: "Adjacent product"
        description: "Related product or extension"
      - label: "Cross-product"
        description: "Research spans multiple products"
      - label: "Other"
        description: "I'll explain"

  - question: "What output format do you need?"
    header: "Output Type"
    multiSelect: false
    options:
      - label: "Full Synthesis Report (Recommended)"
        description: "Comprehensive analysis with themes, quotes, JTBD opportunities"
      - label: "Interview Snapshot"
        description: "One-page summary per interview (Teresa Torres format)"
      - label: "JTBD Extraction"
        description: "Focus on Jobs to Be Done for PRD input"
      - label: "Quote Bank"
        description: "Organized collection of quotes by theme"
      - label: "Executive Summary"
        description: "1-page summary for stakeholders"
```

---

## Step 3: Analysis Process

Follow this systematic analysis approach:

### 3.1 First Pass: Familiarization
- Read all transcripts without coding
- Note initial impressions
- Identify standout quotes (especially pain points and workarounds)

### 3.2 Second Pass: Coding
For each transcript, identify and tag:

**Workflow Codes:**
- Current process steps and tools used
- Workarounds and manual steps
- Time spent on tasks vs. value-add activities
- Handoff points between people or systems

**Pain Point Codes:**
- Frustrations with current tools or processes
- Time wasted on manual tasks
- Limitations of existing systems
- Dependency on other people or teams for support

**Need Codes:**
- Explicit requests ("I wish...", "We need...")
- Implicit needs (inferred from workarounds)
- Jobs to Be Done ("When I..., I want to..., so I can...")

**Context Codes:**
- Product area (which product or feature)
- User type (admin, power user, end user, operator)
- Environment (enterprise, SMB, consumer, internal)
- User journey stage (onboarding, active use, power user, churning)

### 3.3 Third Pass: Theme Development
- Group related codes into themes
- Look for patterns across participants
- Note frequency (how many participants mentioned this?)
- Identify contradictions or segment-specific differences

### 3.4 Fourth Pass: JTBD Extraction
Transform pain points and needs into Jobs to Be Done format:

```
**When** [situation/trigger]
**I want to** [action/capability]
**So that** [outcome/benefit]
```

Categorize jobs by:
- Content Configuration
- Workflow Design
- Templates & Presets
- Data Management
- Export & Integration
- Collaboration & Sharing
- Environment & Settings
- User Self-Service

---

## Step 4: Output Generation

### Output Option A: Full Synthesis Report

```markdown
# User Research Synthesis: [Research Topic]

**Date:** [Date]
**Researcher:** [Name]
**Participants:** [N] users
**Research Type:** [Discovery/Validation/Requirements]
**Product Area:** [Product or feature]

---

## Executive Summary

[3-5 bullet points with the most important findings. What should stakeholders remember if they read nothing else?]

---

## Research Context

### Objectives
[What questions were we trying to answer?]

### Methodology
[How were interviews conducted? Duration? Format?]

### Participants
| ID | Role | Segment | Organization | Key Context |
|----|------|---------|--------------|-------------|
| P1 | Admin | Enterprise | Acme Corp | 3 years on platform |
| P2 | Power User | SMB | StartupCo | Recently onboarded |

---

## Key Themes

### Theme 1: [Theme Name]
**Frequency:** [X of Y participants]
**Severity:** [High/Medium/Low]
**Segments:** [Enterprise, SMB, etc.]

[2-3 sentence description of the theme]

**Supporting Quotes:**
> "[Exact quote]" — P1, Admin

> "[Exact quote]" — P3, Power User

**Behavioral Evidence:**
- [What users do that demonstrates this theme]

---

### Theme 2: [Theme Name]
[Repeat structure]

---

## Pain Points

| Pain Point | Frequency | Severity | Current Workaround | Segment |
|------------|-----------|----------|-------------------|---------|
| [Description] | X/Y users | High/Med/Low | [How they cope today] | [All/Enterprise/SMB] |

### Most Critical Pain Points

**1. [Pain Point Name]**
- **Who feels it:** [Admin, Power User, etc.]
- **When it occurs:** [Trigger/context]
- **Impact:** [Time wasted, errors caused, etc.]
- **Quote:** "[Verbatim quote]" — P2

---

## Jobs to Be Done

Jobs extracted from research, ready for PRD integration. Categorized by functional area.

### Category: [Category Name]

#### Job: [Job Title]
**When** [situation/trigger - be specific to user context]
**I want to** [action/capability]
**So that** [outcome/benefit]

**Evidence:**
- P1: "[Supporting quote]"
- P3: "[Supporting quote]"

**Frequency:** [X/Y participants]
**Suggested Priority:** [P0/P1/P2]

---

#### Job: [Job Title]
**When** [situation/trigger]
**I want to** [action/capability]
**So that** [outcome/benefit]

**Evidence:**
- P2: "[Supporting quote]"

**Frequency:** [X/Y participants]
**Suggested Priority:** [P0/P1/P2]

---

[Repeat for all jobs, organized by category]

---

## Workflow Observations

### Current State: [Workflow Name]
```
[Step 1] → [Step 2] → [Step 3] → [Pain Point] → [Workaround]
```

**Key Insight:** [What this means for the product]

---

## Segment-Specific Findings

| Finding | Enterprise | SMB | Consumer |
|---------|-----------|-----|----------|
| [Finding 1] | ✓ | — | ✓ |
| [Finding 2] | — | ✓ | ✓ |

---

## Design Implications

1. **[Implication]** - [Rationale from research]
2. **[Implication]** - [Rationale from research]

---

## Open Questions

| Question | Why It Matters | Owner |
|----------|----------------|-------|
| [Unresolved question from research] | [Impact on product decisions] | [Who should answer] |

---

## Appendix: Quote Bank

### On [Topic]
> "[Quote]" — P1, Admin, Enterprise

> "[Quote]" — P3, Power User, SMB

### On [Topic]
> "[Quote]" — P2, End User

---

*Generated using synthesize-interviews skill v2.0.0*
```

---

### Output Option B: Interview Snapshot (Per Interview)

Based on Teresa Torres's format:

```markdown
# Interview Snapshot: [Participant ID/Name]

**Date:** [Date]
**Duration:** [X minutes]
**Interviewer:** [Name]
**Product Area:** [Product or feature]

---

## Quick Facts
| Attribute | Detail |
|-----------|--------|
| Role | [Admin / Power User / End User / Operator] |
| Segment | [Enterprise / SMB / Consumer] |
| Organization | [Company or type] |
| Experience | [Years, background] |
| Product Familiarity | [None / Demo only / Active user / Power user] |

---

## Memorable Quote

> "[The single most powerful quote from this interview — something that captures their experience or reveals a key insight]"

---

## Experience Map: [Workflow Name]

```
[Trigger] → [Step 1] → [Step 2] → [Pain Point] → [Workaround] → [Outcome]
    ↓           ↓           ↓            ↓              ↓            ↓
[Context]  [Tool Used]  [Time Spent]  [Frustration]  [What they do] [Result]
```

---

## Jobs to Be Done (Extracted)

#### Job: [Title]
**When** [situation]
**I want to** [action]
**So that** [outcome]

#### Job: [Title]
**When** [situation]
**I want to** [action]
**So that** [outcome]

---

## Pain Points

1. **[Pain Point]** - [Brief context]
2. **[Pain Point]** - [Brief context]

---

## Key Insights

- [Observation or insight]
- [Observation or insight]

---

## Notable Quotes

- "[Quote about current workflow]"
- "[Quote about current tools]"
- "[Quote about what they wish existed]"

---

## Segment-Specific Notes

[Any segment or context-specific observations]

---

## Follow-Up Questions

- [Question that emerged from this interview]
- [Question to validate with other users]

---

*Generated using synthesize-interviews skill v2.0.0*
```

---

### Output Option C: JTBD Extraction (PRD Input)

Focused output for direct PRD integration:

```markdown
# Jobs to Be Done: [Research Topic]

**Source:** [X] interviews, [Date range]
**Product Area:** [Product or feature]
**Ready for PRD:** Yes

---

## Priority Definitions

| Priority | Definition |
|----------|------------|
| **P0** | Must have - mentioned by majority, high severity |
| **P1** | Should have - mentioned by multiple users, medium severity |
| **P2** | Nice to have - mentioned by few, lower severity |

---

## Category 1: [Category Name]

### Job 1.1: [Job Title] (P0)
**When** [situation/trigger]
**I want to** [action/capability]
**So that** [outcome/benefit]

**Evidence:**
- "[Quote]" — P1
- "[Quote]" — P3

**Acceptance Criteria (Suggested):**
- [Criterion based on user expectations]
- [Criterion based on user expectations]

---

### Job 1.2: [Job Title] (P1)
**When** [situation/trigger]
**I want to** [action/capability]
**So that** [outcome/benefit]

**Evidence:**
- "[Quote]" — P2

---

## Category 2: [Category Name]

[Repeat structure]

---

## Jobs NOT Validated

These potential jobs were not supported by research:
- [Job that was hypothesized but not mentioned]

---

## Summary

| Category | P0 Jobs | P1 Jobs | P2 Jobs |
|----------|---------|---------|---------|
| [Category 1] | X | X | X |
| [Category 2] | X | X | X |
| **Total** | X | X | X |

---

*Generated using synthesize-interviews skill v2.0.0*
```

---

## Output Location

Save the synthesis as a markdown file:
- **Default:** `[Research Topic] - Interview Synthesis.md` in the project folder or current working directory
- **Interview Snapshots:** `Interview Snapshot - [Participant].md` per interview
- **JTBD Extraction:** `[Product] - JTBD from Research.md`
- **Ask user** if preferred location is unclear

Always generate a file - don't just output to chat.

---

## Step 5: Review & Refine

After generating the synthesis:

```yaml
questions:
  - question: "What would you like me to refine?"
    header: "Feedback"
    multiSelect: true
    options:
      - label: "Add more quotes"
        description: "Include additional supporting evidence"
      - label: "Expand a theme"
        description: "Go deeper on a specific finding"
      - label: "Refine JTBD format"
        description: "Adjust job statements for PRD integration"
      - label: "Add segment-specific notes"
        description: "Break out findings by user segment"
      - label: "Simplify for stakeholders"
        description: "Create shorter executive version"
      - label: "Looks good"
        description: "Ready to share"
```

---

## Quality Checklist

Before finalizing, verify:

### Evidence Quality
- [ ] Every theme has 2+ supporting quotes
- [ ] Quotes are verbatim (not paraphrased)
- [ ] Participant role and segment noted (P1, Admin, Enterprise)
- [ ] Frequency noted (X of Y participants)

### JTBD Quality
- [ ] Jobs use standard format: When/I want to/So that
- [ ] Jobs are specific to user context
- [ ] Jobs have supporting evidence (quotes)
- [ ] Suggested priorities are justified by frequency/severity
- [ ] Categories align with product structure

### Analysis Quality
- [ ] Observations separated from interpretations
- [ ] Patterns distinguished from anecdotes (3+ mentions)
- [ ] Segment-specific differences noted
- [ ] Contradictions acknowledged

### Actionability
- [ ] Pain points are specific and addressable
- [ ] Jobs are ready for PRD integration
- [ ] Design implications are clear
- [ ] Open questions have owners

---

## Domain Reference

### User Types
| Role | Description |
|------|-------------|
| **Admin** | Manages configuration, settings, team access |
| **Power User** | Heavy daily user, builds complex workflows |
| **End User** | Regular user, consumes content/outputs |
| **Operator** | Manages ongoing operations, monitors systems |
| **Stakeholder** | Decision-maker, reviews outputs and metrics |

### JTBD Categories
Align extracted jobs to these categories when possible:
1. Content Configuration
2. Workflow Design
3. Templates & Presets
4. Data Management
5. Export & Integration
6. Collaboration & Sharing
7. Environment & Settings
8. User Self-Service

---

## Framework References

- **Teresa Torres** - Interview Snapshots, Continuous Discovery
- **Nielsen Norman Group** - Thematic Analysis, Coding qualitative data
- **Jobs to Be Done** - Framing needs as jobs with triggers and outcomes

---

## Tips for Better Synthesis

1. **Synthesize immediately** - Do it within 24 hours while context is fresh
2. **Note the segment** - Enterprise needs differ from SMB or consumer
3. **Distinguish new vs. power users** - Onboarding workflows differ from daily use
4. **Look for "thin to win"** - What's the minimal viable job?
5. **Preserve user language** - Use their terminology, not product jargon
6. **Connect to journeys** - Jobs often map to user journey stages
7. **Flag sensitive content** - Note if findings contain restricted or proprietary information
