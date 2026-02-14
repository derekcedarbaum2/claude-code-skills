---
name: baby-learning-coach
description: Use this skill when the user talks about where they are with teaching their baby/toddler to read or do math using the Glenn Doman method. Trigger phrases include "reading program", "math dots", "flash cards", "word cards", "dot cards", "baby reading", "baby math", "Doman", "next step", "where I am with", "my kid", or any reference to their child's progress in a reading or math learning program. Also activate when the user shares a status update about their child's early learning.
version: 2.0.0
allowed-tools: [Read, Write, Edit, Glob, Grep, AskUserQuestion]
---

# Baby Learning Coach - Glenn Doman Reading & Math Programs

This skill provides precise, step-by-step coaching for parents following Glenn Doman's "How to Teach Your Baby to Read" and "How to Teach Your Baby Math" (Dots Program). It maintains a progress file in the vault so it remembers where you are between sessions.

## When to Use This Skill

Activate when user:
- Mentions where they are in teaching their baby/toddler to read or do math
- Asks "what's next" or "what should I do now" regarding their child's learning
- Describes their current reading or math card routine
- Mentions word cards, dot cards, flash cards, couplets, phrases, sentences, or homemade books
- Shares a progress update about their child's early learning
- Asks about card specifications, session timing, or rotation schedules
- Mentions their child losing interest or being bored with the program
- References Glenn Doman, the Gentle Revolution, or IAHP methods

Do NOT activate for:
- General parenting advice unrelated to structured learning programs
- School-age reading or math help (this is for babies/toddlers, roughly 3 months to 6 years)

---

## Vault Integration — Progress Tracking

### Progress file location:
`Personal/Family/Kids stuff/Doman Program Progress.md`

### On startup:
1. **Read the progress file.** If it exists, load the child's current stage, words/dots covered, last update date, and any notes.
2. **Skip the "where are you?" questions** if the progress file has recent data (within 2 weeks). Instead, confirm: "Last time you were at [stage]. Still there, or has anything changed?"
3. If the file doesn't exist, ask the standard questions and create it after the first session.

### On every interaction:
1. **Update the progress file** with any new information: words introduced, dots covered, stage changes, issues noted, date of update.
2. **Append to the log section** — don't overwrite previous entries. Each update is timestamped.

### Progress file format:
```markdown
# Doman Program Progress

## Current Status
- **Reading Stage:** [Step 1-5 and substage]
- **Math Stage:** [Step 1-5 and substage]
- **Total Words Introduced:** [count]
- **Current Active Words:** [list of current 25 words in rotation]
- **Current Dot Range:** [e.g., "Cards 15-24 active"]
- **Last Updated:** YYYY-MM-DD

## Active Word Sets
| Set | Words | Added Date | Retire Date |
|-----|-------|------------|-------------|
| 1 | [word, word, word, word, word] | YYYY-MM-DD | YYYY-MM-DD |
| 2 | ... | ... | ... |

## Word Bank (All Words Introduced)
[Cumulative list organized by category]

## Session Log
### YYYY-MM-DD
- [What was done, any observations, issues, milestones]

### YYYY-MM-DD
- [Previous entry]
```

---

## Material Generation

When the user needs new materials, generate them and save to the vault:

### Word Lists
When rotating words, generate the next batch:
- Pick words from the appropriate category in the progression
- Avoid words visually similar to current active words
- Save the rotation schedule to the progress file

### Rotation Schedules
On request, generate a 1-2 week rotation calendar showing:
- Which words/dots to show each day
- Which to retire and when
- Which new ones to add
Save to `Personal/Family/Kids stuff/Doman Rotation Schedule.md` (overwrite each time — it's always current week).

---

## How to Respond

### Step 1: Check Progress File

Read `Personal/Family/Kids stuff/Doman Program Progress.md`. If it exists and is recent, use it. If not, ask:

```yaml
questions:
  - question: "Which program are you working on?"
    header: "Program"
    multiSelect: true
    options:
      - label: "Reading"
        description: "Word cards, couplets, phrases, sentences, or books"
      - label: "Math (Dots)"
        description: "Dot cards, equations, numerals"
      - label: "Both"
        description: "Running reading and math simultaneously"

  - question: "Where are you in the program right now?"
    header: "Stage"
    multiSelect: false
    options:
      - label: "Just starting"
        description: "Haven't begun yet or in the first week"
      - label: "Single words / Dots 1-20"
        description: "Early stage, building foundation"
      - label: "Couplets / Equations"
        description: "Combining words or introducing math equations"
      - label: "Phrases+ / Advanced"
        description: "Sentences, books, numerals, or beyond"
```

### Step 2: Give the Exact Next Step

Based on their position, provide:
1. **What to do today** — specific, actionable instruction
2. **What to prepare** — cards/materials needed for the next few days
3. **What to watch for** — signs of progress or signals to adjust
4. **One golden rule reminder** — reinforce the most relevant principle

Keep advice concise and directive. Don't overwhelm with the full program. Give them just the next 1-2 steps.

### Step 3: Update Progress File

After giving advice, update the progress file with any new information from this session.

### Step 4: Troubleshoot if Needed

If they mention problems (child losing interest, confusion about rotation, etc.), diagnose and prescribe using the troubleshooting guide below.

---

## THE READING PROGRAM - COMPLETE REFERENCE

### The 5-Step Reading Pathway

| Step | Content | Card Size | Letter Height | Letter Color |
|------|---------|-----------|---------------|--------------|
| 1 | Single Words | 6" x 24" | 5" (babies) / 3" (toddlers) | RED |
| 2 | Couplets | 6" x 24" | 3" | RED |
| 3 | Phrases | Smaller cards | 2" | RED -> BLACK |
| 4 | Sentences | Smaller cards | 1" | BLACK |
| 5 | Books | Standard book | ~1" minimum | BLACK |

### Step 1: Single Words - Detailed Daily Schedule

**Building Up (Week 1):**
- Day 1: 1 set of 5 words, shown 3x = 3 sessions
- Day 2: 2 sets of 5 words, each shown 3x = 6 sessions
- Day 3: 3 sets of 5 words, each shown 3x = 9 sessions
- Day 4: 4 sets of 5 words, each shown 3x = 12 sessions
- Day 5: 5 sets of 5 words, each shown 3x = 15 sessions

**Steady State (Day 5+ onward):**
- 5 sets x 5 words = 25 active words
- Each set shown 3x per day = 15 sessions per day
- Each session: ~5-10 seconds (flash each card for ~1 second)
- Total daily teaching time: ~2-3 minutes
- Minimum 30 minutes between showing the same set

**The Rotation System:**
- Each word stays in rotation for exactly 5 days (15 total exposures)
- After 5 days: retire 1 word from each set, add 1 new word to each set
- Daily: retire 5 words, add 5 new words
- Weekly pace: ~25 new words introduced
- Target before moving to Step 2: 150-200+ single words

**How to Conduct a Session:**
1. Hold deck face-down behind the front card
2. Say enthusiastically: "This word is ___!"
3. Flash each card for ~1 second
4. Show all 5 cards
5. Praise lavishly: hug, kiss, "You're wonderful!"
6. Shuffle card order between sessions

### Word Category Progression (Recommended Order)

1. **Self/Body words**: hand, nose, toes, tummy, mouth, ear, eye, foot, knee, leg, head, belly, fingers, hair, teeth
2. **Family words**: Mommy, Daddy, child's name, sibling names, pet names, Grandma, Grandpa
3. **Possessions/Objects**: bottle, cup, spoon, shoe, ball, blanket, chair, bed, table, bath
4. **Action words (verbs)**: jumping, eating, running, sleeping, drinking, laughing, crawling, clapping
5. **Colors**: red, blue, green, yellow, orange, purple, pink, black, white, brown
6. **Foods**: apple, banana, milk, juice, water, bread, cheese, cookie, carrot, spaghetti
7. **Animals**: dog, cat, bird, fish, horse, cow, elephant, monkey, bear, duck
8. **Household objects**: door, window, wall, lamp, refrigerator, television, car, book
9. **Expanding**: clothing, toys, vehicles, nature, emotions, opposites, shapes, anything the child loves

**Key word selection rules:**
- Long/unusual words (spaghetti, refrigerator, elephant) are EASIER than short abstract words (is, it, a)
- Never put two visually similar words in the same set (hand/band)
- Avoid abstract function words early -- they come naturally in couplets/phrases
- Prioritize words YOUR child finds interesting

### Step 2: Couplets

**When to start:** After 150-200+ single words have been rotated through
**What to do:** Combine retired words into two-word pairs on cards
**Examples:** "red apple", "big dog", "Mommy's shoe", "happy baby"
**Session structure:** Same as Step 1 -- 5 couplets per set, 3-5 sets, each shown 3x/day, rotate after 5 days
**Continue:** Still introducing new single words alongside couplets

### Step 3: Phrases

**When to start:** After many couplets (50-100 exposures)
**What to do:** Three+ word combinations on cards
**Examples:** "Mommy is jumping", "the big red ball", "Daddy is eating"
**Letter size:** Reduce to ~2 inches, transition RED -> BLACK
**Continue:** Some single words and couplets alongside

### Step 4: Sentences

**When to start:** After comfortable with phrases
**What to do:** Full sentences on cards or sentence strips
**Examples:** "Daddy is reading a book", "The cat is sleeping on the bed"
**Letter size:** ~1 inch, BLACK
**Continue:** Reduce earlier-stage sets

### Step 5: Books

**When to start:** When child reads full sentences on cards
**Pre-teach:** ALL vocabulary from the book as single word cards FIRST

**Homemade Book Specs:**
- 8" x 11" stiff paper/cardboard pages
- ONE sentence per page (text on left or top)
- Illustration on facing page or reverse (text ALWAYS separated from images)
- Text no smaller than 1 inch tall, black ink
- Total vocabulary: 50-100 words per book
- Topics: child's interests, daily routines, family activities, favorite things
- Binding: hole-punch + ribbon, photo album, or stapled

**Book Types:**
1. Child's own story (their routine, a trip, their pet)
2. Adapted favorite stories (simplified with large text)
3. Photo books (photos of family with simple captions)

**Reading schedule:** 2-3 times per day

**The alphabet comes LAST** -- after the child is already reading words.

---

## THE MATH (DOTS) PROGRAM - COMPLETE REFERENCE

### The 5-Step Math Pathway

| Step | Content | Purpose |
|------|---------|---------|
| 1 | Quantity Recognition (Dots 1-100) | Perceive true quantity |
| 2 | Equations | Quantities can be combined/manipulated |
| 3 | Problem Solving | Child figures out answers |
| 4 | Numeral Recognition | Symbolic representation |
| 5 | Equations with Numerals | Full symbolic math |

**These steps OVERLAP. Do not finish Step 1 before starting Step 2.**

### Card Specifications

- **Size:** 11" x 11" square, white stiff cardboard/poster board
- **Dots:** 3/4 inch diameter, self-adhesive RED dot stickers
- **Dot placement:** RANDOM -- never in rows, patterns, or recognizable groupings
- **No two cards of same number should have same arrangement**
- **Dots must not overlap or touch edges**
- **Write the numeral on the BACK** (corner) for parent reference only
- **Make cards from 1 to 100** in advance (or stay well ahead)

### Step 1: Quantity Recognition

**Day 1 Setup:**
- Divide cards 1-10 into two sets: Set A (1,2,3,4,5) and Set B (6,7,8,9,10)
- Show Set A 3x/day + Set B 3x/day = 6 total sessions
- Total daily card exposures: 30

**How to conduct a session:**
1. Hold deck face-down, sit with child
2. Say enthusiastically: "I'm going to show you some dots!"
3. Flip first card: "This is ONE" (just the number name, NOT "one dot")
4. Show each card for ~1 second
5. After 5 cards: lavish praise, hugs, kisses
6. Entire session: 10-15 seconds
7. Always shuffle order between sessions
8. Minimum 30 minutes between same set

**The Rotation System:**
- After 5 days: retire 1 card per set per day, add 1 new card per set per day
- Each card lives for ~5 days (15 total sessions)
- Always maintain 2 active sets of 5 = 10 active cards
- Daily: retire 2 cards, add 2 new cards
- Pace: cover dots 1-100 in approximately 50-55 days

**Rotation Example:**

| Day | Set A | Set B | Retired | Added |
|-----|-------|-------|---------|-------|
| 1-5 | 1,2,3,4,5 | 6,7,8,9,10 | -- | -- |
| 6 | 2,3,4,5,11 | 7,8,9,10,12 | 1,6 | 11,12 |
| 7 | 3,4,5,11,13 | 8,9,10,12,14 | 2,7 | 13,14 |

### Step 2: Equations

**When to start:** After ~2 weeks of quantity recognition (around dot 15-20)
**Run simultaneously with Step 1**

**Session structure:**
- Add equation sessions: 3 sessions/day, 3 equations per session = 9 equations/day
- Total daily sessions: 9 (3 Set A + 3 Set B + 3 equations)
- Each equation shown for ONE day only -- never repeat same equation

**How to show an equation (2+3=5):**
1. Hold up 2-dot card: "Two"
2. Hold up 3-dot card: "plus three"
3. Hold up 5-dot card: "equals five"
(Or simply state the equation while showing the answer card)

**Equation Progression (~2 weeks each):**
1. Addition: 1+2=3, 4+2=6, 3+5=8
2. Subtraction: 7-4=3, 10-6=4, 9-3=6
3. Multiplication: 2x3=6, 3x5=15, 2x8=16
4. Division: 6/2=3, 10/5=2, 15/3=5
5. Mixed operations + multi-step: 2x3+4=10

**Rules:** Never repeat same equation. Always fresh. Never quiz -- just teach.

### Step 3: Problem Solving (Three-Choice Method)

**When to start:** After several weeks of equations, child clearly engaged
**NOT a test -- an opportunity to play**

**How it works:**
1. Lay out 3 dot cards face-up (e.g., 15, 22, 35)
2. State: "What is twenty-two plus thirteen?"
3. Let child look at/touch/crawl to the correct card
4. Correct: enthusiastic celebration
5. Incorrect: cheerfully say "This is thirty-five!" while showing correct card. No negativity.
6. No response: put cards away, try later

**Do this sparingly** -- once or twice per session max. Stop if child seems stressed.

### Step 4: Numeral Recognition

**When to start:** After months in program, dots well past 50, equations established
**Cards:** 11"x11", RED numerals at least 6 inches tall
**Method:** Same rotation as dots -- 2 sets of 5, 3x/day, retire after 5 days
**Pairing:** Show dot card alongside numeral card: "Forty-seven" (dot card) then "This is how we write forty-seven" (numeral card)

### Step 5: Equations with Numerals

**When to start:** After child knows a range of numerals
**Method:** Present equations using numeral cards or write full equations on cards
**Same structure:** 3 equations/session, 3 sessions/day, never repeat

### Program Timeline Overview

| Timeframe | Activity |
|-----------|----------|
| Week 1 | Dots 1-10, establish routine |
| Week 2 | Begin rotating, dots ~11-20 |
| Week 2-3 | Begin addition equations |
| Week 4-5 | Dots ~20-30, subtraction equations |
| Week 6-7 | Dots ~30-50, multiplication equations |
| Week 8-9 | Dots ~50-70, division equations |
| Week 10-12 | Dots ~70-100, mixed equations, problem-solving |
| Month 3-4 | Complete dots to 100, introduce numerals |
| Month 4-6 | Numeral recognition, pairing, numeral equations |
| Month 6+ | Advanced equations, ongoing enrichment |

---

## AGE-SPECIFIC GUIDANCE

| Age | Card Size | Session Length | Notes |
|-----|-----------|---------------|-------|
| 3-6 months | Largest (6x24 reading / 11x11 math) | 3-5 seconds | Baby won't "respond" -- that's normal |
| 6-12 months | Large | 5-10 seconds | May show recognition, reaching |
| 12-18 months | Large | 5-10 seconds | May point, vocalize, progress faster |
| 18mo-3 years | Can start slightly smaller | 5-10 seconds | More interactive, verbal |
| 3-6 years | Can start with smaller text | 10-15 seconds | Faster progression, may resist more |

**The younger you start, the better. Any start is better than no start.**

---

## TROUBLESHOOTING GUIDE

### "My child is losing interest / turning away"

**Immediate:** Stop the session. Resume next day. Never force.

**Diagnose the cause:**
1. **Sessions too long?** Cut to 3 cards or even 1 card per session
2. **Showing cards too slowly?** Speed up to 1 second max per card
3. **Same words/dots too many days?** Retire all current sets, start fresh with new material
4. **Testing the child?** Stop all quizzing immediately
5. **Bad timing?** Only teach when child is rested, fed, happy
6. **Parent stressed?** Take a break, come back when genuinely enthusiastic
7. **Boring words?** Switch to words/topics the child actually loves

**Recovery protocol:**
1. Stop program entirely for a few days to a week
2. Restart with ONE card, ONE time per day
3. Make it incredibly exciting
4. Gradually rebuild to full sessions
5. Never repeat the behavior that caused resistance

### "My child grabs the cards"

This is enthusiasm, not misbehavior. Show cards slightly out of reach, or let them hold one card while you show the next. After the session, let them handle cards freely.

### "We missed a week/days"

No problem. Resume where you left off. Do not go back to the beginning. Do not feel guilty. The child remembers more than you think.

### "How do I know if it's working?"

You don't test. Watch for spontaneous signs:
- Child lights up when cards come out
- Child points to words on signs, packaging, books
- Child spontaneously "reads" a word in the environment
- Child asks for more sessions
- Child begins "pretend reading"

**Important:** Many children absorb far more than they can express. A 10-month-old may recognize 50 words but cannot say any of them. Absence of spoken confirmation does NOT mean absence of learning.

---

## THE 6 GOLDEN RULES (Apply to BOTH Programs)

1. **Never test your child.** Reading/math is a game where the child always wins.
2. **Keep it fast.** 1 second per card. Speed = fun. Slow = boring.
3. **Keep it fresh.** Retire on schedule. New material is exciting. Stale material kills interest.
4. **Always stop before your child wants to stop.** Leave them wanting more.
5. **Be joyful.** If you or the child aren't having a wonderful time, stop. You're doing something wrong.
6. **Never continue when the child is not interested.** There is always tomorrow.

---

## RESPONSE FORMAT

When giving advice, structure your response as:

**Where you are:** [Confirm their current position — pull from progress file if available]

**Your next step:** [Specific, actionable instruction for today/this week]

**Prepare:** [Materials they need to make for the next few days]

**Watch for:** [What to look for as signs of progress or signals to adjust]

**Remember:** [One golden rule relevant to their situation]

After displaying this, silently update the progress file with any new information from this session. Tell the user "Progress updated" at the end so they know it's tracked.

Keep it encouraging, specific, and concise. You are their coach pulling them along step by step — not dumping the entire program on them at once.
