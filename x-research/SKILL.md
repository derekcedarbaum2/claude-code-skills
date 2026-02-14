---
name: x-research
description: Use this skill when the user wants to research what people are saying on X/Twitter about a topic, company, product, person, or trend. Searches X for real-time discourse, expert opinions, competitive intel, and community sentiment. Trigger phrases include "search X for", "what's Twitter saying about", "X research", "check X for", "what are people saying about", or any request for social media sentiment/discourse analysis.
version: 1.0.0
allowed-tools: [Read, Write, Edit, Glob, Grep, WebSearch, WebFetch, AskUserQuestion, Bash]
---

# X/Twitter Research Agent

Agentic research over X/Twitter. Decomposes questions into targeted searches, follows threads, deep-dives linked resources, and synthesizes sourced briefings.

## When to Use This Skill

Activate when user:
- Asks "what are people saying about [topic]" or "search X for [topic]"
- Wants competitive intel from X discourse
- Needs expert/community perspectives on a product, company, technology, or trend
- Wants to find high-signal takes for content research
- Says "x research", "twitter research", "check X", "X discourse"

Do NOT activate for:
- Writing tweets (use write-tweets skill)
- Posting to X or account management
- General web research with no X/social media angle

---

## Research Methodology

Follow this loop for every research request:

### 1. Decompose the Question

Break the user's question into 3-5 targeted search queries. Use X-specific search patterns:

**Search operators to use in WebSearch queries:**
- `site:x.com` or `site:twitter.com` — restrict to X
- `"exact phrase"` — match exact wording
- Combine with topic keywords, company names, product names
- Add `2026` or recent date ranges for recency
- For specific people: include their X handle or full name

**Query construction examples:**
- Competitive intel: `site:x.com "[company name]" [product] review OR feedback OR opinion`
- Expert opinions: `site:x.com from:[handle] [topic]` or `site:x.com "[person name]" [topic]`
- Product discourse: `site:x.com "[product]" launch OR release OR update -giveaway -airdrop`
- Tech trends: `site:x.com "[technology]" developer OR engineer opinion OR experience`

### 2. Search and Extract

For each query:
1. Run `WebSearch` with the constructed query
2. For promising results, use `WebFetch` to pull the full tweet/thread content
3. Assess signal quality — prioritize:
   - High engagement (lots of likes/replies indicates resonance)
   - Domain experts and known voices
   - Substantive takes with reasoning, not just hot takes
   - Threads with linked resources (blog posts, demos, data)
4. Filter noise — skip:
   - Promotional/spam accounts
   - Crypto/airdrop spam
   - Pure retweets with no commentary
   - Bot-like engagement patterns

### 3. Follow Threads

When you find a high-signal tweet:
- Fetch the full thread if it's a thread starter
- Check replies for expert pushback or additional context
- Note if the original poster is a known voice in the domain

### 4. Deep-Dive Linked Resources

If multiple tweets reference the same blog post, GitHub repo, or article:
- Fetch the linked resource with `WebFetch`
- Extract key claims or data points
- Note that X discourse is reacting to this source

### 5. Synthesize by Theme

Group findings into themes. Don't just dump a list of tweets — tell the user what the discourse means.

### 6. Save Results

Always save research to the Obsidian vault (see Output section).

---

## Output Format

### Briefing Structure

```markdown
# X Research: [Topic]

**Date:** [YYYY-MM-DD]
**Query:** [User's original question]
**Searches run:** [N]
**Signal quality:** [High/Medium/Low — honest assessment of what was found]

---

## TL;DR

[3-5 bullet points. The "if you read nothing else" summary. Be direct.]

---

## Key Findings

### Theme 1: [Theme Name]

[2-3 sentence summary of this theme]

**Top voices:**

> "[Tweet text]"
> — @username ([context: role/company if known]) | [engagement metrics if visible]
> [tweet URL]

> "[Tweet text]"
> — @username | [engagement]
> [tweet URL]

**What this means:** [1-2 sentence interpretation. Connect to user's question.]

---

### Theme 2: [Theme Name]

[Same structure]

---

## Contrarian / Minority Takes

[Important: Always include dissenting views. What are the skeptics saying? This is often the most valuable signal.]

> "[Contrarian tweet]"
> — @username
> [URL]

---

## Linked Resources Worth Reading

| Resource | Source | Why It Matters |
|----------|--------|---------------|
| [Title](URL) | Referenced by @user1, @user2 | [1-line reason] |

---

## Gaps and Limitations

- [What you couldn't find or assess]
- [Topics where X discourse was thin or low-quality]
- [Searches that returned mostly noise]

---

## Research Metadata

- **Queries used:**
  - `[query 1]`
  - `[query 2]`
  - `[query 3]`
- **Time window:** [What period the results cover]
- **Confidence:** [How confident you are in the synthesis]
```

---

## Vault Integration

### Save Location
Save all research briefings to the Obsidian vault:
- **Path:** `Research/X Research/[Topic] - X Research [YYYY-MM-DD].md`
- Create the directory if it doesn't exist
- Check for existing research on the same topic to avoid duplicate work and note what's new

### Cross-Reference
- If related notes exist in `Ideas/` or `Research/`, mention them in the briefing
- If findings are relevant to an active hypothesis or PRD, note the connection

---

## Use Case Playbooks

### Competitive Intel
When the user asks about a competitor or competing product:
1. Search for the company/product name + common reaction terms (review, feedback, switched to, left, migrated)
2. Search for the founders/leaders by name — what are they saying publicly?
3. Search for comparisons: "[product] vs [alternative]"
4. Look for customer complaints and praise patterns
5. Check for recent launches, pivots, or controversy

### Expert Opinions
When the user wants to know what experts think:
1. If specific experts are named, search their handles directly
2. If general, search the topic + filter for substantive takes (look for threads, not one-liners)
3. Prioritize people with domain credentials (engineers for tech, operators for business, researchers for science)
4. Note consensus vs. disagreement among experts

### Content Research
When the user wants takes to inform their own writing:
1. Find the most viral/resonant takes on the topic — what framing gets engagement?
2. Identify the angles that haven't been covered yet (content gaps)
3. Look for data points, stats, or examples being cited repeatedly
4. Note which takes align with and challenge the user's existing worldview
5. Flag quotes that could be referenced or riffed on

---

## Quality Checklist

Before presenting results:

- [ ] Every claim has a source (tweet URL or linked resource)
- [ ] Engagement context included where visible (helps gauge signal vs. noise)
- [ ] Contrarian/minority views included — not just confirmation bias
- [ ] Themes are genuine patterns, not forced groupings of 1-2 tweets
- [ ] Gaps and limitations honestly stated — don't oversell thin results
- [ ] Briefing answers the user's actual question, not just "here's what I found"
- [ ] Saved to vault

---

## Refinement Strategies

If initial results are noisy or thin:

- **Too much noise:** Add exclusion terms (-giveaway, -airdrop, -promotion), restrict to recent dates
- **Too few results:** Broaden search terms, try synonyms, remove restrictive filters
- **Wrong audience:** Add domain-specific terms or known expert handles
- **Stale results:** Tighten date range to last 24-48 hours
- **Crypto spam:** Add `-$ -airdrop -giveaway -whitelist -NFT`

Always tell the user when results are thin rather than padding with low-quality content.

---

## Future: CLI Mode

This skill currently uses Claude's native WebSearch. For higher-volume research with precise engagement filtering, sorting, and caching, a CLI tool (`x-search.ts`) can be added later that wraps the X API directly. The skill prompt and research methodology stay the same — only the search execution changes.

When CLI is available:
- `bun run x-search.ts search "<query>" --sort likes --min-likes 50`
- `bun run x-search.ts profile <username>`
- `bun run x-search.ts thread <tweet_id>`
- `bun run x-search.ts watchlist check`

This is not yet implemented. The prompt-based approach works for most use cases.
