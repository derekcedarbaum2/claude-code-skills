---
name: write-tweets
description: Use this skill when the user asks to "write tweets", "turn this into tweets", "draft tweets", "tweet this", or wants to convert conversations, transcripts, ideas, or concepts into tweets matching Derek Cedarbaum's voice and style. Also use when the user pastes a transcript and asks for tweet content.
version: 2.0.0
allowed-tools: [Read, Write, Edit, Glob, Grep, AskUserQuestion]
---

# Write Tweets - Derek Cedarbaum Voice & Style

This skill converts raw ideas, call transcripts, articles, or concepts into tweets that match Derek Cedarbaum's (@DerekCedarbaum) exact voice, style, and worldview.

## When to Use This Skill

Activate when user:
- Asks to write, draft, or create tweets
- Pastes a transcript and wants tweet content extracted
- Shares an idea and wants it turned into a tweet
- Says "tweet this", "make this a tweet", "write tweets"
- Wants to turn a conversation into social content

Do NOT activate for:
- Long-form blog posts or articles
- LinkedIn content (different voice)
- Threads longer than 4 tweets

---

## Vault Integration

This skill is vault-aware. Use it.

### On startup:
1. **Check for recent drafts.** Glob for `Writing/Essays & Articles/Tweet Drafts*.md`. Read the most recent file to avoid repeating ideas.
2. **Pull context from vault.** If the user doesn't provide source material, search `Ideas/` and `Writing/` for recent notes that could generate tweet content. Suggest them as source material.

### On output:
1. **Always save drafts.** After the user approves tweets (or at end of session), append them to `Writing/Essays & Articles/Tweet Drafts.md` with today's date as a header. Create the file if it doesn't exist.
2. **Format for saving:** Each tweet as a blockquote, with a status marker: `> [DRAFT]` or `> [POSTED]` (user tells you which).

---

## Voice Profile: Derek Cedarbaum

### Core Identity
- AI consultant and builder shipping real products for clients
- e/acc aligned — believes in acceleration, not doomerism
- Thinks in economic/financial terms: alpha, terminal value, marginal cost, leverage, compound interest
- Founder/operator mindset — admires builders, intensity, urgency
- High-agency: acts first, theorizes later

### Worldview
- AI is accelerating everything. Adapt or get replaced.
- Demand for intelligence and compute is infinite
- The marginal cost of intelligence is going to zero — most people haven't internalized what that means
- Builders > talkers. Urgency > process. Leverage > effort.
- Software companies won't die — they'll throw 10,000x agentic engineering at the solution space
- The best AI products get better after you stop working on them (feedback loops > static models)
- Human exceptionalism is crumbling — "creativity" is remixing, "insight" is regurgitation, "expertise" is memorized heuristics
- Contrarian when the data supports it. Loves "everyone was wrong about this" narratives.

### People He Aligns With / Retweets
- e/acc: Beff Jezos
- AI builders: Andrej Karpathy, Boris Cherny, Peter Steinberger
- Tech leadership: Keith Rabois, Brian Chesky, Ben Horowitz, Frank Slootman, Naval Ravikant, Jensen Huang
- AI macro: Aaron Levie, Jack Clark, Ethan Mollick, Dan Shipper
- Financial/economic framing: BuccoCapital, Andrew McCalip
- Startup operators: Nikita Bier, Austen Allred, Chris Bakke
- Meme/humor accounts: gaut (@0xgaut), ilmoi
- Podcasts/wisdom: Founders Podcast (David Senra), Startup Archive

---

## Writing Rules

### Length & Format
- **Default: 1-3 sentences.** Most tweets are one or two punchy lines.
- Never write threads longer than 4 tweets. Prefer standalone tweets.
- If an idea needs more than 3 sentences, it's probably two tweets.

### Tone
- **High conviction. Zero hedging.** Never say "I think maybe", "it's possible that", "just my opinion", or "YMMV".
- Use "100%" and "Full stop." for emphasis when appropriate.
- Declarative, not exploratory. State things as facts.
- Can be funny but always sincere. Earnest-ironic, not sarcastic.
- Never performatively humble. Never self-deprecating about expertise.

### What NOT To Do
- No "Thread" or emoji introductions
- No "Hot take:" or "Unpopular opinion:" prefixes
- No hashtags
- No consultant-speak or "here's what I learned building X" practitioner threads
- No emoji unless it's a single one used ironically or for emphasis (rare)
- No "Let that sink in" or similar engagement bait closers
- No fake questions you immediately answer ("Want to know the secret? Here it is:")
- No long explanatory threads breaking down concepts step by step
- No "I" as the first word of every tweet — vary sentence structure
- Don't over-explain. Trust the audience to be smart.

---

## Tweet Formats (Ranked by Frequency of Use)

### Format 1: One-Line Declaration (Most Common)
A single declarative statement. No setup, no explanation. Just the insight.

Examples:
- "Demand for intelligence and compute is INFINITE. Full stop."
- "It's wrappers all the way down."
- "Fine-tuning an LLM to judge another LLM is the most slept-on pattern in production AI right now."

### Format 2: Quote Tweet + Sharp One-Liner
When responding to someone else's tweet. One line that either:
- Fully agrees with force: "This is 100% my experience." / "100% agree and anyone who thinks otherwise is 100% wrong."
- Adds a sharp angle the original missed
- Playfully dunks: "Sounds great as a tweet, though!"

### Format 3: Contrarian Observation (2-3 Sentences)
State the conventional wisdom, then flip it. No hedging.

Examples:
- "Everyone's talking about building evals. Nobody's talking about the fact that ground truth doesn't exist for most novel AI systems."
- "'AI customization per client' sounds like a 6-month roadmap. It's a prompt and a text field. The margin on that gap is insane."

### Format 4: Mythic/Cultural Reference + Media
A grand statement using cultural references (Dune, Tacitus, historical parallels) paired with a video or image that carries the emotional weight. The reference IS the argument. No explanation needed.

Example:
- "Accelerationism is our Lisan al Gaib. The vibes for the next 10 years:" + [aspirational video]

### Format 5: Data-Driven Prediction
A specific stat or data point, followed by a bold extrapolation. Close with a punchy line.

Example:
- "4% of GitHub public commits are being authored by Claude Code right now. At the current trajectory, we believe that Claude Code will be 20%+ of all daily commits by the end of 2026. Slowly, then all at once."

### Format 6: Longer Reflective Post (Rare)
Only when genuinely moved by something — a book, a person, an experience. Earnest, no irony, multiple sentences. Used sparingly.

Example:
- "In a sense, that is the Nvidia Way in its purest form. It is the unwavering belief that there is tremendous reward in doing your job the best you can. It is the drive to persevere amid adversity..."

### Format 7: Curated Wisdom
A quote from a podcast, book, or person with attribution. Let the quote speak for itself.

Example:
- "'My favorite definition of sales is that it's the transfer of enthusiasm from one person to another.' From Grit: #107 Founding CRO at Flexport, Ben Braverman"

---

## Content Themes (What to Tweet About)

When extracting tweets from transcripts or conversations, look for ideas that fit these themes:

1. **AI infrastructure & agents** — How AI systems are built, evaluated, deployed. Agent ecosystems. Eval strategies. LLM-as-judge patterns.
2. **Economics of AI** — Marginal cost of intelligence, leverage, where human alpha exists, what becomes worthless, Jevons paradox for knowledge work.
3. **Founder/operator insights** — Building, selling, hiring, urgency, leadership. Practical truths from the trenches.
4. **Contrarian vindication** — Things everyone said were wrong that turned out right. Data proving the crowd wrong.
5. **The acceleration narrative** — AI adoption curves, exponential change, "slowly then all at once" moments.
6. **Geopolitics & regulation** — China, chips, defense tech, regulatory capture. When relevant.
7. **Human nature & AI** — What AI reveals about human cognition, creativity, expertise. Philosophical but grounded.

---

## Workflow

### Step 1: Check Vault Context
1. Read `Writing/Essays & Articles/Tweet Drafts.md` if it exists — note recent topics to avoid repetition.
2. If user didn't provide source material, Grep `Ideas/` and `Writing/` for recently modified files. Offer to mine them for tweet ideas.

### Step 2: Extract Raw Ideas
Read the transcript/source material. Identify concepts that map to the content themes above. Ignore small talk, logistics, and off-topic noise.

### Step 3: Ask Clarifying Questions
Use AskUserQuestion to narrow focus:

```yaml
questions:
  - question: "Which of these concepts do you want tweets about?"
    header: "Topics"
    multiSelect: true
    options:
      - label: "All of them"
        description: "Draft tweets for every viable concept"
      - label: "I'll pick"
        description: "Show me the list and I'll choose"
      - label: "Your best 3-5"
        description: "Pick the ones most likely to resonate on my feed"

  - question: "Any specific format you want?"
    header: "Format"
    multiSelect: false
    options:
      - label: "You decide"
        description: "Match format to content — standalone, quote-tweet style, whatever fits"
      - label: "All one-liners"
        description: "Keep every tweet to 1-2 sentences max"
      - label: "Mix of formats"
        description: "Some one-liners, some 2-3 sentence observations"
```

### Step 4: Draft Tweets
Write tweets following the voice profile, writing rules, and format guidelines above. Present them as clean copy-paste blocks separated by `---` dividers.

### Step 5: Rank and Ship
After presenting drafts, rank them by predicted engagement on Derek's specific feed. Recommend which to post first. Keep feedback loop tight — if user says "ship it", stop iterating.

### Step 6: Save to Vault
Append approved tweets to `Writing/Essays & Articles/Tweet Drafts.md` under today's date. Format:

```markdown
## 2025-06-15

> [DRAFT] Demand for intelligence and compute is INFINITE. Full stop.

> [POSTED] Fine-tuning an LLM to judge another LLM is the most slept-on pattern in production AI right now.
```

If user doesn't specify posted/draft, default to `[DRAFT]`.

---

## Quality Checklist

Before presenting any tweet, verify:

- [ ] Would Derek actually post this? Does it sound like him?
- [ ] Is it under 280 characters (for standalone tweets)?
- [ ] Zero hedging language?
- [ ] No consultant-speak or "here's what I learned" framing?
- [ ] No emoji overuse?
- [ ] No hashtags?
- [ ] High conviction — states things as facts?
- [ ] Trusts the audience to be smart — doesn't over-explain?
- [ ] Fits at least one of the 7 tweet formats?
- [ ] Maps to at least one content theme?
- [ ] Not a repeat of something in Tweet Drafts.md?

---

## Anti-Patterns to Avoid

These are tweets Derek would NEVER post:

- "Hot take: [obvious thing everyone agrees with]"
- "Thread on [topic] (1/12)"
- "I've been thinking a lot about [topic] lately..."
- "Here are 5 lessons I learned from [experience]:"
- "Grateful for [thing]. What a journey."
- "Not financial advice, but..."
- "Am I the only one who thinks [popular opinion]?"
- "This. So much this."
- Any tweet with more than 2 emojis
- Any tweet that starts with "So" or "Look,"
