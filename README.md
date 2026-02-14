# Claude Code Skills

Custom skills I have built for Claude Code to embed rigor, methodology, and repeatable workflows into my daily product management work. These are not prompt templates. They are structured systems that enforce quality gates, scoring rubrics, and iterative improvement loops so I do not have to rely on the model alone to get good output.

I am a product manager, not a software engineer. I built all of these using Claude Code itself.

## Why I Built These

I adopted Claude Code and quickly realized the default interaction model (type a prompt, get an answer) is not enough for serious PM work. The output quality depends entirely on the structure of the input. So I started building skills that encode the structure I would otherwise have to remember and apply manually every time: interview methodologies, scoring criteria, adversarial review passes, execution modes with rollback support.

The result is a system where Claude Code operates less like a chatbot and more like a junior PM who has been trained on my exact frameworks and standards.

## Skills

### Product Discovery and Requirements

| Skill | What It Does |
|-------|-------------|
| **write-prd** | Interview-driven PRD generator. Runs a 5-round discovery interview, maps to domain standards, generates engineer-ready requirements with acceptance criteria. Includes AI product-specific sections. |
| **hypothesis** | Turns fuzzy ideas into falsifiable hypotheses with assumption mapping, kill criteria, and interview guides. Forces you to define what would prove you wrong before you start building. |
| **synthesize-interviews** | Converts raw interview transcripts into structured JTBD outputs. 4 formats: full report, interview snapshots, JTBD extraction, executive summary. Built on Teresa Torres and Nielsen Norman methodologies. |
| **analyze-research** | Cross-interview pattern analysis. Frequency matrices, severity assessment, contradiction detection, evidence scoring. Generates prioritized requirements with confidence flags. |
| **user-discovery** | Interview analyzer that validates or challenges existing hypotheses against live research. Generates emerging theses and persona insights. |

### Quality Control and Execution

| Skill | What It Does |
|-------|-------------|
| **execute-prd** | PRD execution engine with TaskMaster integration. Detects existing PRDs and offers execute/update/replace workflows. 4 autonomous execution modes (sequential, parallel, full async) with git branching policies, datetime tracking, and rollback support. 928 lines. |
| **qa-loop** | Recursive self-improvement loop. 3 escalating passes: constructive coach, skeptical reviewer, adversarial attacker (with hostile personas). Scores against 10 criteria and iterates until all hit 9/10. Does not stop until the work is actually good. |

### Content and Communication

| Skill | What It Does |
|-------|-------------|
| **write-tweets** | My exact voice encoded as executable rules. 7 tweet formats, worldview mapping, anti-patterns checklist. Converts transcripts, ideas, or conversations into tweets that sound like me, not like AI. |
| **x-research** | Agentic X/Twitter research. Decomposes queries, filters signal from noise, follows threads, generates sourced briefings with evidence quality assessment. |
| **podcast-notes** | Converts podcast transcripts into actionable bullets with vault integration and cross-referencing to existing notes. |

### Personal

| Skill | What It Does |
|-------|-------------|
| **baby-learning-coach** | Glenn Doman methodology coach for early childhood reading and math programs. 5-step pathways with age-specific guidance, rotation systems, troubleshooting protocols, and progress tracking. |

## How These Work

Each skill is a single SKILL.md file that Claude Code loads when invoked. The file contains:

- **Trigger conditions**: when to activate and when not to
- **Workflow steps**: structured multi-step processes the model follows
- **Scoring rubrics**: criteria with explicit definitions of what good looks like
- **Quality gates**: conditions that must be met before output is delivered
- **Vault integration**: where to read from and write to in my Obsidian knowledge base
- **Tool permissions**: which Claude Code tools the skill is allowed to use

The model does not freelance. It follows the workflow, checks against the rubric, and iterates until the output meets the bar.

## Setup

These skills are designed for Claude Code's skill system. To use them:

1. Copy any skill folder into `~/.claude/skills/`
2. Each folder contains a single `SKILL.md` file
3. Invoke with `/skill-name` in Claude Code (e.g., `/qa-loop`, `/write-prd`)

Note: Some skills reference my Obsidian vault paths for file storage. You would need to update those paths for your own setup.

## Author

Derek Cedarbaum | [LinkedIn](https://www.linkedin.com/in/derek-cedarbaum)
