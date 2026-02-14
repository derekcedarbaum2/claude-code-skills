# Biographer - Interview Q&A

> **Purpose:** Stores all product discovery questions and Derek's answers across sessions. Used alongside the Product Memory file to build the product specification.

**Last Updated:** 2026-02-11

---

## Round 1: Core Experience & User Journey

**Q1: When you imagine opening the app for the very first time, what does that first session look like? Do you envision an onboarding questionnaire (name, family, life goals), or do you want to jump straight into your first entry?**

A1: Jump straight into the first entry — it's stickier. The onboarding questionnaire should come *after* the first entry. There should be a full profile covering: name, family, life goals, profession, age, interests, and other background questions/details.

**Q2: For the daily entry flow — do you see this as primarily voice-first (you hit record and talk), or do you want equal weight given to text, voice, video, and photo as entry types? What's your default mode?**

A2: Equal weight to all input types. Clean UI with a list of options — the voice button should be the most accessible (top/easiest thumb reach), video option higher up, text box at the bottom, and photo attachments as a small widget (standard photo attachment pattern).

**Q3: When you say "diary entry" — is each entry tied to a single day, or can you have multiple entries per day (e.g., morning thoughts, evening reflection)?**

A3: *(Not directly answered — implied multiple entries are fine given "any time that I want" from the transcript. Will confirm in a later round.)*

**Q4: After you submit an entry and the AI "interviews" you with follow-up questions — how deep should that go? 1-2 follow-ups? Or a full back-and-forth conversation that could last 10+ minutes?**

A4: Full back-and-forth, up to ~10 minutes. But after every few questions, the AI should ask if the user wants to continue or end the session — providing an easy out at natural breakpoints.

**Q5: Should the app ever surface past entries to you? Like "On this day 3 years ago, you wrote about..." — or do you only want to look back when you explicitly ask for a biographical generation?**

A5: Yes, the app should surface past entries and ask for follow-ups to close loops on events.

**Q6: How do you feel about the AI proactively reaching out with questions even when you haven't made an entry? For example: "You mentioned your daughter's first steps last week — how has she been doing since?"**

A6: Likes proactive outreach, but it must be toggleable. The app should ask the user if they want to be reached out to after the first or second proactive interaction. Key insight: following up on past entries is a strong differentiator. Many diary events happen in isolation and don't have natural follow-ups — but the *impact* of those events lingers. Example: you went on a great date and never saw the person again, but the app could ask how that date impacted you later. This is "a memory of a memory" — not just logging events, but capturing their emotional afterlife.

---

## Round 2: The AI Biographer Personality & Biographical Output

**Q7: When the AI interviews you after an entry, what tone should it have? Warm and empathetic like a therapist? Curious and probing like a journalist? Intellectual like a literary biographer? Some blend?**

A7: Intellectual, literary biographer tone — probing in an objective manner. Explicitly NOT overly empathetic, because empathy could solicit biased responses from the user. The biographer should be objective to preserve the integrity of the biographical record.

**Q8: For the biographical chapters it generates — do you imagine a specific writing style? Something literary like a Pulitzer-winning biography? More conversational like a memoir? Or do you want users to pick from style templates?**

A8: Users should pick from writing style templates. Examples given: "Write like Walter Isaacson," "Write like J.R.R. Tolkien," "Write in the style of Roosevelt's autobiography," "Write in the style of Lord of the Rings." The AI should access and emulate those writing styles. Additional curated templates should be provided so users don't have to think through it on their own — make the choices obvious.

**Q9: When you generate a biographical chapter, what's the unit of time? A year? A month? A "life chapter"? Or should the AI figure out the natural chapter breaks?**

A9: The AI should figure out the natural chapter breaks on its own. There are too many ways it could be broken out — let the AI determine the natural narrative arcs.

**Q10: Should the biography be written in first person ("I walked into the room...") or third person ("Derek walked into the room...")? Or user's choice?**

A10: User's choice. First person = autobiography, third person = biography. The user can choose which they want.

**Q11: Can you edit the generated chapters? Like, if the AI writes a chapter and gets the tone wrong or includes something you'd rather leave out — do you want a full editor, or more of a "regenerate with these notes" feedback loop?**

A11: Full editor. Can edit via text or via voice. In text mode, user can highlight a block of text to edit. In voice mode, user can reference specific passages verbally and dictate changes.

**Q12: How do you think about entries that are mundane vs. significant? Should the AI weight them differently?**

A12: Over time, the AI should inquire whether a daily entry or event was significant. It should ask for clarification from the contributor. When no explicit significance rating is provided, the AI should try to figure it out on its own. The user can always correct the AI's significance assessment after the fact.

---

## Round 3: Digital Legacy, Privacy & Data

**Q13: For the dead man's switch — should the designated recipients get everything (raw diary entries, unedited), or only the polished biographical/documentary output? Or should the user configure exactly what gets shared?**

A13: User should be able to configure exactly what gets shared. Users can go back and mark memories with different legacy statuses — include in legacy, exclude/destroy on death or departure.

**Q14: Some diary entries might be deeply private — things you'd never want anyone to read. Should there be a way to mark entries as "private/exclude from legacy" vs. "include in legacy"? Or even "destroy on death"?**

A14: Yes — covered in Q13. Users can mark entries to keep, exclude from legacy, or destroy on death/departure. This is a retroactive action — users can go back through their entries and tag them at any time.

**Q15: How do you feel about encryption? Should entries be end-to-end encrypted so that even the company running the app can't read them?**

A15: Trust is paramount — cannot let any user data leak. However, acknowledged that E2E encryption creates tension with the need for the company to exist and operate the AI processing. Data security is a top priority but the exact encryption model needs further exploration given the AI processing requirements.

**Q16: For the legacy trigger — "hasn't signed in for X years" feels risky. Would you prefer a more deliberate mechanism, like designating a "digital executor" who can request access with proof of death?**

A16: Hybrid approach — after 2 years of inactivity, the system sends an email to the designated executor to confirm. (Answered in Round 4.)

**Q17: Should recipients be able to interact with the AI biographer after receiving the legacy? For example, your children could ask the AI questions about your life based on all the entries — almost like talking to a version of you.**

A17: Yes — great idea. Took it further: this shouldn't only be a posthumous feature. Users should be able to **publish their AI biographer publicly while still living** as a feature. Others could interact with your AI biographer as a public-facing representation of your life story.

**Q18: Can you confirm — should users be able to make multiple entries per day, or is it one entry per day that they can keep adding to?**

A18: Confirmed — users can make as many entries per day as they want. They can just open the app, take a voice note, and it gets collated under that date/day.

---

## Round 4: Social Sharing, Stickiness & Daily Value

**Q19: You mentioned wanting shareable outputs for Twitter/Instagram/Substack. What if the app generated a "daily reflection" — a polished, short-form version of your entry? Like a beautifully written 2-3 sentence vignette from your day that's share-ready?**

A19: Likes the daily reflection concept. Platform-specific outputs: video entries can be posted to Instagram or TikTok. Text entries (or video converted to text) can go to Twitter or Facebook. Other socials can be added over time.

**Q20: Would you want the app to generate different formats for different platforms? For example: a tweet-length version, an Instagram caption + suggested photo, a longer Substack-style paragraph?**

A20: Yes to all three formats. Tweet-length version, Instagram caption + suggested photo, and at end of week — longer Substack-style posts compiled from the week's content when there's more material to work with.

**Q21: Should there be a "public journal" mode where selected entries (or AI-polished versions of them) are automatically published to a blog/feed — separate from the full biography?**

A21: Yes, there should be a public journal mode.

**Q22: For the legacy trigger — would you prefer a pure inactivity timer, a designated "digital executor" who submits proof of death, or a hybrid?**

A22: Hybrid — after 2 years of inactivity, the system sends an email to the designated executor to confirm.

**Q23: How do you think about the timeline/feed view of your entries? Chronological scroll? Calendar view? A "life map" visualization? Something else?**

A23: Likes the calendar view. Not sure what the chronological UI would look like — open to exploring options.

**Q24: Should the app track location data with entries? For example, auto-tagging "this entry was recorded in Central Park" — which could enrich the biography with sense of place?**

A24: Yes, track location data with entries.

---

## Round 5: Onboarding, Profile & The Interviewer

**Q25: For the profile questionnaire (after first entry) — how extensive should it be? Just basics (name, age, family, profession) or a deep biographical intake (childhood, where you grew up, formative experiences, values, what you want to be remembered for)?**

A25: Deep biographical intake. Must support save and exit at any time — user can return to it later since it could take considerable time. The intake itself should be multi-modal: user chooses video-based, voice-based, or text-based intake. Voice and video are transcribed to text. Important nuance: video intake content has added value because someone interacting with the user's AI biographer later might want to see them speaking, not just read text. So the video component of the profile intake is preserved and potentially surfaced.

**Q26: Should the profile be built through a conversational interview (AI asks questions one at a time) or a traditional form (fill in fields)?**

A26: Conversational interview — the AI asks questions one at a time, like a real biographer conducting an intake interview.

**Q27: For the voice avatar interviewer (future feature) — do you envision a single default avatar, or should users pick from a roster of interviewer personalities?**

A27: User's choice from a roster of interviewer personalities — e.g., "The Historian," "The Philosopher," "The Storyteller" — each with a distinct interviewing style.

**Q28: When the AI follows up on a past entry days or weeks later — should that feel like a push notification or appear when you next open the app?**

A28: Both, in sequence. First, send a push notification ("Your biographer has a question for you"). If the user dismisses the notification without opening the app, it should appear as a prompt on next app open before they start a new entry. Ensures follow-ups are never lost.

**Q29: You mentioned wanting the app to check audio/video quality and flag garbled words. Should this happen in real-time during recording or after you finish recording?**

A29: After the recording is finished. Can be fully async — if the user closes the app after recording, they can get a notification later alerting them to a quality issue with the audio or video. No need to block the recording flow.

**Q30: How do you feel about the app suggesting "prompts" on days when you don't know what to talk about? Like guided journaling questions or questions a biographer would ask?**

A30: Yes — guided journaling prompts, historian/biographer-style questions should all be in the queue. Key addition: even on days when a user DOES make a diary entry, there should be a standalone **"Interview Me"** option. The user taps it and the avatar begins asking questions — either via text or voice. This is a separate entry point from diary entries. The app has two core modes: (1) record a diary entry, (2) be interviewed by your biographer.

---

## Round 6: Business Model, Technical & Scope

**Q31: Monetization — what are you leaning toward? Subscription? Freemium? One-time purchase?**

A31: Not worrying about pricing yet. Single-user build for now (just Derek). **BYOK model (Bring Your Own Key)** — user connects their own AI API key (e.g., Anthropic, OpenAI). User manages their own API spend. If tokens run out, the app sends a notification: "Out of access tokens — please check with your AI service provider." No payment system needed for MVP.

**Q32: How much are you willing to spend on AI API costs per user?**

A32: N/A — paying his own API costs directly via BYOK. No per-user pricing model needed yet.

**Q33: For the MVP — what's the minimum feature set you'd want before using it yourself daily? If you had to pick 5 features to ship first, which matter most?**

A33: Wants to build **everything** discussed — no MVP cut. Will refine the spec until it's right, then build the full vision. Not interested in a stripped-down MVP.

**Q34: Do you have any budget in mind for initial development and hosting costs?**

A34: No budget in mind. Managed services preferred since he's not an engineer and can't manage infrastructure.

**Q35: Timeline — do you have a target for when you'd want a working prototype?**

A35: No timeline pressure. Can keep working on the spec and product as long as needed.

**Q36: Have you looked at any existing apps in this space (Day One, Rosebud, Captions, etc.)?**

A36: Has NOT looked at existing apps. **This is as much about Derek learning to make an app** as it is about the product itself. The process of building is part of the goal.

---

## Round 7: Content Architecture & The Biographer's Intelligence

**Q37: When the AI generates a biographical chapter, should it only draw from your diary entries, or should it also incorporate external context? For example, if you mention "the day the election happened," should it pull in what actually happened that day from public sources to enrich the narrative?**

A37: Yes — the AI should incorporate external context from public sources to enrich the narrative alongside personal entries.

**Q38: How should the app handle contradictions? If you say "that was the best day of my life" in March and then say "actually, the worst year of my life" in December about the same period — should the AI flag that, reconcile it, or preserve both perspectives?**

A38: The AI should flag contradictions. Don't silently reconcile or ignore them — surface them to the user.

**Q39: Should entries be taggable? For example, tagging entries with themes like "family," "career," "health," "travel" — so you can later generate a biography chapter focused on just one theme?**

A39: Yes, entries should be taggable with themes.

**Q40: When you think about the biography spanning 20-30 years, how do you imagine versioning? Should you be able to generate at age 40, then again at 50, and compare? Or does each generation replace the previous?**

A40: Nothing gets overwritten — all versions coexist. User can select flexible date ranges for generation: specific life periods (childhood, 40s, 50s), combine multiple ranges (e.g., childhood + 50s), or generate across the whole life. Each generation is its own version that persists.

**Q41: Should the app understand relationships between people you mention? Like building a character map — "Sarah = wife," "Marcus = business partner" — so the biography can reference people consistently?**

A41: Yes — build a character map. Users should be able to build a profile for each person mentioned in their entries.

**Q42: How do you feel about the app detecting emotional patterns over time? For example: "You've mentioned feeling anxious about work 15 times in the last 3 months — would you like to explore that?"**

A42: No — that crosses into therapist territory. Stay away from emotional pattern detection/analysis. Keep the biographer objective.

---

## Round 8: The Public Biographer, Sharing & Output Formats

**Q43: When someone interacts with your public AI biographer, what should the experience be? A chat interface? A voice conversation? Or more of a "browse chapters" experience with a chat layer?**

A43: Multiple interaction modes: (1) Voice conversation with the AI biographer, (2) Browse chapters by flipping through a calendar, (3) Chat layer to ask questions. All three should coexist in the public biographer experience.

**Q44: Should you be able to control what the public biographer can talk about? For example: "Don't discuss my health" or "Only discuss my career and family."**

A44: Yes — user should be able to scope what the public biographer can and cannot discuss. Topic-level controls for what's public vs. private.

**Q45: For the weekly Substack-style digest — should you review and approve it before it publishes, or should it auto-publish?**

A45: Review and approve ALL items before publishing. No auto-publish. User must approve everything that goes out.

**Q46: Should the app generate a "year in review" — an annual biographical summary more substantial than a weekly digest but shorter than a full biography chapter?**

A46: Yes — the app should generate a year in review.

**Q47: When the app converts a video entry into a shareable TikTok/Instagram clip — should it edit the video or just post the raw recording?**

A47: Edit the video — add captions, trim dead air, and add music. Not raw footage.

**Q48: Should there be a way to export your entire biography as a PDF, ePub, or printed book?**

A48: Yes — export as PDF, ePub, or printed book. A physical artifact to hand to your children.

---

## Round 9: Remaining Gaps & Edge Cases

**Q49: The productivity/coaching angle — you mentioned weekly reviews and the biographer acting as a coach. Do you want to keep this in the product, or does it feel like it muddies the biographer identity now that we've drawn a clear line against therapist behavior?**

A49: Drop it — muddies the biographer identity. The product is a biographer, not a productivity tool or coach.

**Q50: Product name — any new thoughts? "Biographer" is clean and literal. Some other directions: "Chronicle," "Memoir," "Epilogue," "Narrator," "My Chapter." Or brainstorm later?**

A50: Sticking with **Biographer**. Clean and literal.

**Q51: Should the app have a search function? Like "find all entries where I mentioned Tokyo" or "show me entries about my daughter's milestones"?**

A51: Yes — the app should have a search function across all entries.

**Q52: What happens if you delete an entry? Hard delete (gone forever) or soft delete (recoverable for 30 days)?**

A52: Soft delete — recoverable.

**Q53: Should there be a "highlights reel" — the AI picks your most significant entries from the past month/year and presents them as a curated collection?**

A53: Yes — and it should be social sharing-oriented. The highlights reel is a shareable output, not just an internal feature.

**Q54: Should the app support multiple languages? For example, if someone journals in Spanish some days and English others?**

A54: No — English only.

---

## Round 10: PM Spec Review — Gaps That Would Block Development

**Q55: What is an "entry"? If you record a voice note, attach 3 photos, and type a caption — is that one entry or three?**

A55: One entry. All content captured in a single session (voice + photos + text) is bundled as one atomic entry.

**Q56: When does the AI interview trigger? After each individual recording, or batched?**

A56: Batched. There should be a "done for the day" action that signals the AI to engage. The AI interviewer triggers after the user indicates they're finished for the day, not after every individual recording.

**Q57: BYOK routing — one key or many? Or should we move to a company API subscription with usage-based pricing + margin instead?**

A57: Reconsidering the BYOK model. Two options on the table: (1) BYOK where user manages their own keys and accounts, or (2) company API subscription with usage-based pricing, margin on top, and users just pay Biographer directly. Leaning toward whatever is easiest for the user. If company subscription: users pay a monthly fee, get a token allotment, and can buy more if they exceed it. **Decision deferred — needs further discussion.**

**Q58: Tagging and character map — manual, automatic, or both?**

A58: Both, with manual as primary. User manually tags entries day-to-day. Once a month, the backend runs an auto-tag sweep looking for patterns to improve tag accuracy. User can always confirm or correct auto-generated tags after the fact.

**Q59: Public biographer vs. public journal — how do these relate?**

A59: Two tabs on the same public page. One page, two experiences.

**Q60: What do legacy recipients actually receive?**

A60: Recipients get: (1) a downloadable zip file, and (2) read-only access to the app. "Destroy on death" entries are purged AFTER the executor confirms — so the system waits for confirmation, then purges, then grants access to what remains.

**Q61: How does social posting actually work? Direct API or manual?**

A61: Manual copy/paste for now. No direct API integrations with Twitter/IG/TikTok/Substack. App generates the content in platform-specific formats, user copies and posts themselves. Keeps engineering lift much lower.

**Q62: Are entries threaded or flat?**

A62: Threaded. If the AI asks a follow-up about a past entry and the user responds, that response is linked/threaded to the original. The AI should understand that Entry #47 was a follow-up to Entry #12. This threading informs biographical generation.

**Q63: Video storage — comfortable with the cost implications of storing all original video indefinitely?**

A63: Yes. Storage costs will continue to drop. This is not meant to be an inexpensive tool. Store everything at full quality indefinitely.

**Q64: Biographical intake completion — can users skip it?**

A64: Strongly prefers users NOT skip the biographical intake. Should be treated as required (or at minimum, heavily nudged/gated).
