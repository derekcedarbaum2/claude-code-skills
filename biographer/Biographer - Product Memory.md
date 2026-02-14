# Biographer - Product Memory

> **Purpose:** This file is the persistent memory for all planning sessions on the Biographer product. If a session is interrupted, provide this file and the companion Q&A file to resume with full context.

**Last Updated:** 2026-02-12

---

## Product Vision

An AI-powered biographical diary app that captures a user's life through daily entries (voice, video, text, photos) and uses AI to synthesize those entries into biographical chapters, memoirs, and eventually documentary-style content. The app acts as a personal biographer — interviewing the user, asking follow-up questions, and curating a rich narrative of their life over years and decades.

## Origin & Motivation

- Derek has a 2.5-year-old son, 11-month-old daughter, and 8-year-old stepdaughter
- Birth of his daughter prompted deeper thinking about legacy, life, death, and what to leave behind
- Inspired by movie/TV scenes of parents leaving video messages for children
- A single video felt insufficient — wants a comprehensive account of his life
- Loves reading biographies; aspires to have his own biographical record
- Has tried physical diaries multiple times but always abandons them — believes an app-based approach with AI engagement would be stickier
- Not an engineer or designer; relying on AI coding agents to build this

## Core Concepts

### Daily Diary Entries
- Multi-modal input: voice notes, video recordings, text, photos
- **Atomic unit**: one entry = everything captured in a single session (voice + photos + text bundled together)
- **Entries are threaded**: if the AI asks a follow-up about a past entry and the user responds, the response is linked to the original. AI understands relationship chains across entries.
- Any time, any day — not forced to be daily but encouraged
- Entries are the raw material for everything else
- App should follow up on past entries to "close loops" — many life events happen in isolation but their emotional impact lingers
- Core concept: **"memory of a memory"** — capturing not just what happened, but how past events continue to affect you over time

### AI Biographer / Interviewer
- **"Done for the day" trigger**: AI interviewer engages after the user signals they're finished for the day, NOT after every individual recording. Batched, not per-entry.
- After the batch trigger, AI analyzes and asks follow-up questions (like a real biographer would)
- Pokes holes, asks for clarification, enriches the entry
- **Tone: intellectual, literary, objective** — probes like a biographer, NOT a therapist. Deliberately avoids over-empathy to prevent soliciting biased responses
- Acts as both interviewer and coach
- Asks users to rate significance of entries/events over time; infers significance when user doesn't rate; user can correct after the fact
- **Interviewer personality roster**: user picks from archetypes — "The Historian," "The Philosopher," "The Storyteller" — each with a distinct style
- Future vision: voice avatar (ElevenLabs, Google/Gemini voice models) for conversational interview experience
- Goal: videos should feel like there's an off-screen interviewer asking questions
- **Follow-up delivery**: push notification first → if dismissed, appears as prompt on next app open (never lost)

### "Interview Me" Mode (Standalone)
- Dedicated entry point separate from diary entries
- User taps "Interview Me" and the avatar begins asking questions (text or voice)
- Available any time — even on days when diary entries are also made
- Guided prompts queue: biographer questions, historian questions, guided journaling prompts for days when user doesn't know what to talk about
- **Two core app modes**: (1) Record a diary entry, (2) Be interviewed by your biographer

### Biographical Generation
- User can request AI to generate biographical chapters from their entries
- **Writing style templates**: curated library of styles (e.g., "Walter Isaacson," "J.R.R. Tolkien," "Roosevelt's autobiography," "Lord of the Rings"). Templates should be obvious/easy to pick — user shouldn't have to think hard
- **POV choice**: first person (autobiography) or third person (biography) — user selects
- **AI determines natural chapter breaks** — no forced time units (year/month). AI finds the narrative arcs
- Can include/exclude certain events or time periods
- **Full editor** for generated chapters — edit via text (highlight blocks) or voice (reference passages verbally)
- AI ingests all entry types (video, voice, text, image) for synthesis
- **External context enrichment**: AI pulls in public/historical context when relevant (e.g., "the day the election happened") to enrich the narrative
- **Contradiction flagging**: AI surfaces contradictions between entries for user to address — doesn't silently reconcile
- **Flexible date range generation**: user selects specific life periods (childhood, 40s, etc.), combines multiple ranges, or generates across whole life
- **Version persistence**: nothing gets overwritten — all generated versions coexist and are browsable

### Entry Tagging & Character Map
- **Taggable entries**: users manually tag entries with themes (family, career, health, travel, etc.) day-to-day. **Monthly auto-tag sweep**: backend runs once a month to detect patterns and suggest tags the user missed. User confirms or corrects auto-generated tags.
- **Character map**: app builds profiles for people mentioned in entries — relationships, roles, context. Biography references people consistently. Interviewer can ask about specific people.

### Anti-Patterns (What the App is NOT)
- **NOT a therapist**: no emotional pattern detection, no mood tracking, no wellness suggestions. The biographer stays objective and intellectual. This is a firm boundary.

### Documentary Generation (Future)
- As video AI models become cheaper, generate documentary-style chapters from photos, videos, voice recordings
- Storable chapters that build over time

### Digital Legacy ("Dead Man's Switch")
- If user doesn't sign in for a configurable period (1-2 years), trigger legacy protocol
- Sends email to designated recipients (spouse, children, etc.)
- **User configures exactly what gets shared** — can go back and mark any entry with a legacy status:
  - Include in legacy
  - Exclude from legacy
  - **Destroy on death/departure** (permanently deleted upon trigger)
- **Hybrid trigger**: after 2 years of inactivity, system emails the designated executor to confirm
- **Execution sequence**: executor confirms → "destroy on death" entries are purged → remaining content packaged
- **Recipients receive**: (1) downloadable zip file, (2) read-only access to the app

### Public AI Biographer
- Users can **publish their AI biographer publicly while still living**
- Others can interact with the published AI biographer — ask it questions about the user's life
- Also available posthumously to legacy recipients
- Acts as a living, queryable representation of someone's life story
- **Multi-mode interaction**: (1) Voice conversation with AI biographer, (2) Browse chapters via calendar-style flipping, (3) Chat layer to ask questions
- **Topic scoping**: user controls what the public biographer can/cannot discuss (e.g., "don't discuss health," "only career and family")
- **Public page structure**: Public biographer and public journal are **two tabs on the same public page** — one URL, two experiences

### Social Sharing / Stickiness
- **Daily outputs** — AI generates a polished "daily reflection" from entries
- **Platform-specific formats**:
  - **Twitter/Facebook**: tweet-length text version (video entries converted to text if needed)
  - **Instagram/TikTok**: video entries **edited** (captions added, dead air trimmed, music added) — not raw footage; Instagram caption + suggested photo for non-video
  - **Substack**: end-of-week longer-form post compiled from the week's content
- Other social platforms can be added over time
- **Year in review**: annual biographical summary — more substantial than weekly digest, shorter than full chapter
- **Review & approve everything**: all shareable content must be approved by user before publishing. No auto-publish.
- **Manual posting for now**: app generates platform-specific content, user manually copy/pastes. No direct API integrations with social platforms. Keeps engineering lift lower.
- Goal: make the app sticky by providing daily value beyond just storage

### Export & Physical Artifacts
- Export entire biography as **PDF, ePub, or printed book**
- Physical artifact you can hand to your children

### Public Journal Mode
- Selected entries (or AI-polished versions) automatically published to a blog/feed
- Separate from the full biography — this is the lighter, shareable layer

### ~~Productivity / Coaching~~ — DROPPED
- Muddies the biographer identity. Product is a biographer, not a productivity tool or coach.

## Platforms

- **iOS app** (primary mobile experience)
- **Web app** (same database, for desktop use — diary entries, configuration, camera/mic access)
- Shared database between iOS and web

## Technical Context

- Derek has no engineering background — needs guidance on tech stack, hosting, databases, auth, payments, deployment
- **This is also a learning project** — Derek wants to learn how to build an app through this process. Education is part of the goal, not just shipping.
- **Single-user build for now** — no multi-user auth or payments needed for MVP
- **AI billing model — DECIDED**: Phase 1 (single-user): hardcoded API keys in backend config, Derek pays API bills directly. Phase 2 (multi-user): company subscription with usage-based pricing + margin. All AI calls proxied through backend. User never sees API keys, tokens, or model names.
- App monitors usage and notifies when approaching limits
- **Managed services preferred** — Derek can't manage raw infrastructure
- Will need: database, file storage (for video/audio/photos), managed hosting
- **Store all video at full quality indefinitely** — not meant to be an inexpensive tool. Storage costs expected to drop over time.
- **Biographical intake is required** — not skippable. User must complete it (with save & resume support).
- No budget constraints defined; no timeline pressure

## Key Features List

1. Multi-modal diary entries (voice, video, text, photo)
2. AI interview/follow-up after entries
3. Biographical chapter generation (configurable writing style)
4. Documentary chapter generation (future)
5. Digital legacy / dead man's switch
6. Configurable notification reminders (time of day)
7. Audio/video quality analysis with transcript correction prompts
8. Recording guidance (lighting, quality settings)
9. Social sharing outputs (format TBD)
10. Onboarding interview / questionnaire
11. Voice avatar interviewer (ElevenLabs, Google voice models — future)
12. Web-based system configuration (interviewer questions, avatars, voice models)
13. ~~User auth, payments, multi-user support~~ → Deferred. Single-user for now.
14. ~~Productivity/coaching features~~ → DROPPED. Muddies biographer identity.
15. Public AI biographer — publish a queryable version of your life story for others to interact with
16. Entry legacy tagging (include / exclude / destroy on death)
17. Public journal mode — auto-publish polished entries to a blog/feed
18. Platform-specific social sharing (Twitter, Instagram, TikTok, Facebook, Substack)
19. Weekly Substack-style digest from the week's entries
20. Calendar view for browsing entries
21. Location auto-tagging on entries
22. "Interview Me" standalone mode — on-demand biographer interview, separate from diary entries
23. Guided journaling prompts for days without inspiration
24. Interviewer personality roster (Historian, Philosopher, Storyteller)
25. Deep biographical intake — conversational, multi-modal, save & resume
26. Async audio/video quality checking with delayed notifications
27. ~~BYOK~~ → DROPPED. Phased billing: hardcoded keys (Phase 1), company subscription + usage pricing (Phase 2)
28. Usage monitoring with limit notifications
29. External context enrichment — AI pulls public/historical context into biography
30. Contradiction flagging between entries
31. Entry tagging by theme (family, career, health, travel, etc.)
32. Flexible date range generation with version persistence
33. Character map — profiles for people mentioned in entries
34. Public biographer: voice conversation + chapter browsing (calendar) + chat layer
35. Public biographer topic scoping (control what it can/can't discuss)
36. Approval workflow — all shareable content reviewed before publishing
37. Year in review — annual biographical summary
38. Video editing for social clips (captions, trim dead air, add music)
39. Export biography as PDF, ePub, or printed book
40. Search across all entries (people, places, themes, keywords)
41. Soft delete for entries (recoverable)
42. Highlights reel — AI-curated significant entries, social sharing-oriented

## Decisions Made

| Decision | Detail | Date |
|----------|--------|------|
| First-entry-first onboarding | User jumps straight into first diary entry before any profile/questionnaire. Deep biographical intake follows — conversational interview format (not a form). Multi-modal: video, voice, or text. Save & exit anytime, resume later. Video intake is preserved for public biographer interactions. | 2026-02-11 |
| Equal-weight input UI | All input types (voice, video, text, photo) given equal weight. Voice button = most thumb-accessible, video higher up, text box at bottom, photo as small widget. | 2026-02-11 |
| Interview depth | Full back-and-forth (~10 min), with opt-out checkpoints every few questions. | 2026-02-11 |
| Past entry surfacing | App proactively surfaces past entries and asks for follow-ups to close loops. | 2026-02-11 |
| Proactive outreach | AI can reach out even without a new entry, but feature is toggleable. App asks user if they want this after 1-2 occurrences. | 2026-02-11 |
| Objective AI tone | Intellectual, literary biographer — deliberately not empathetic to avoid soliciting biased responses. | 2026-02-11 |
| Writing style templates | Curated library of famous styles (Isaacson, Tolkien, Roosevelt, etc.) — users pick from templates, not free-form. | 2026-02-11 |
| AI-determined chapter breaks | No forced time units — AI finds natural narrative arcs for chapter structure. | 2026-02-11 |
| First/third person choice | User chooses: first person = autobiography, third person = biography. | 2026-02-11 |
| Full chapter editor | Edit generated chapters via text (highlight blocks) or voice (reference passages verbally). | 2026-02-11 |
| Significance tracking | AI asks about event significance over time; infers when user doesn't rate; user can always correct. | 2026-02-11 |
| Configurable legacy sharing | User marks each entry: include in legacy, exclude, or destroy on death. Retroactive tagging at any time. | 2026-02-11 |
| Public AI biographer | Users can publish their AI biographer publicly while still living. Others can interact with it. Also available posthumously. | 2026-02-11 |
| Multiple entries per day | Unlimited entries per day — open app, record, gets collated under that date. | 2026-02-11 |
| Data trust is paramount | Zero tolerance for data leaks. Exact encryption model TBD but security is a non-negotiable top priority. | 2026-02-11 |
| Platform-specific social outputs | Tweet-length for Twitter/FB, video for IG/TikTok, weekly Substack-style longer posts. | 2026-02-11 |
| Public journal mode | AI-polished entries auto-published to a blog/feed, separate from full biography. | 2026-02-11 |
| Legacy trigger: hybrid | 2 years inactivity → system emails designated executor to confirm. | 2026-02-11 |
| Calendar view for entries | Primary entry browsing UI is calendar-based. Chronological scroll TBD. | 2026-02-11 |
| Location tracking | Auto-tag entries with location data to enrich biography with sense of place. | 2026-02-11 |
| Deep biographical intake | Conversational AI interview (not a form). Multi-modal (video/voice/text). Save & exit anytime. Video preserved for biographer interactions. | 2026-02-11 |
| Interviewer personality roster | User picks from archetypes: Historian, Philosopher, Storyteller — each with distinct style. | 2026-02-11 |
| Follow-up delivery | Push notification first → if dismissed, prompt on next app open. Never lost. | 2026-02-11 |
| Async quality check | Audio/video quality checked after recording. Notification sent later if issues found. Doesn't block recording flow. | 2026-02-11 |
| "Interview Me" standalone mode | Dedicated button separate from diary entries. Avatar asks questions via text or voice. Always available. | 2026-02-11 |
| Guided prompts | Biographer/historian questions + guided journaling prompts queued for days user doesn't know what to talk about. | 2026-02-11 |
| BYOK model | User connects own AI API key. No payment system needed. App monitors tokens and notifies on exhaustion. | 2026-02-11 |
| Single-user MVP | No multi-user auth or payments. Build for Derek first. | 2026-02-11 |
| Managed services | Prefer managed hosting/infra since Derek is not an engineer. | 2026-02-11 |
| Full feature build | No MVP cut — build everything discussed. Refine spec until right, then build the full vision. | 2026-02-11 |
| Learning project | This is as much about Derek learning to build an app as it is about the product. Education is part of the goal. | 2026-02-11 |
| External context enrichment | AI pulls public/historical context into biographical chapters when relevant. | 2026-02-11 |
| Contradiction flagging | AI surfaces contradictions between entries — doesn't silently reconcile or ignore. | 2026-02-11 |
| Entry tagging | Entries taggable by theme (family, career, health, travel, etc.) for theme-based chapter generation. | 2026-02-11 |
| Version persistence | All generated biography versions coexist. Nothing overwritten. Flexible date range selection. | 2026-02-11 |
| Character map | App builds profiles for people mentioned. Tracks relationships, roles, context. | 2026-02-11 |
| No therapist behavior | Firm boundary: no emotional pattern detection, mood tracking, or wellness suggestions. Biographer stays objective. | 2026-02-11 |
| Public biographer multi-mode | Voice conversation + calendar chapter browsing + chat layer. All three coexist. | 2026-02-11 |
| Public biographer topic scoping | User controls what public biographer can/cannot discuss (e.g., "don't discuss health"). | 2026-02-11 |
| Approval before publish | All shareable content (social posts, weekly digests, etc.) must be reviewed and approved. No auto-publish. | 2026-02-11 |
| Year in review | App generates annual biographical summary — between weekly digest and full chapter in depth. | 2026-02-11 |
| Video editing for social | Videos edited with captions, dead air trimmed, music added before posting to IG/TikTok. Not raw. | 2026-02-11 |
| Book export | Export biography as PDF, ePub, or printed book — physical artifact for family. | 2026-02-11 |
| Product name: Biographer | Clean and literal. No rename needed. | 2026-02-12 |
| Drop productivity/coaching | Muddies the biographer identity. Product is a biographer, not a coach. | 2026-02-12 |
| Search function | Full search across all entries — people, places, themes, keywords. | 2026-02-12 |
| Soft delete | Deleted entries are recoverable, not permanently destroyed. | 2026-02-12 |
| Highlights reel | AI-curated collection of most significant entries. Social sharing-oriented — a shareable output, not just internal. | 2026-02-12 |
| English only | No multi-language support. English only. | 2026-02-12 |
| Entry = atomic bundle | One entry = everything captured in a single session (voice + photos + text bundled). | 2026-02-12 |
| "Done for the day" trigger | AI interviewer triggers after user signals they're done for the day, not after every recording. Batched. | 2026-02-12 |
| Manual tagging + monthly auto-sweep | User tags manually day-to-day. Backend auto-tags monthly for patterns. User confirms/corrects. | 2026-02-12 |
| Public page: two tabs | Public biographer + public journal = two tabs on same public page. One URL. | 2026-02-12 |
| Legacy delivery | Zip file + read-only app access. Destroy-on-death entries purged after executor confirms, before access granted. | 2026-02-12 |
| Manual social posting | App generates platform-specific content, user copy/pastes. No API integrations for now. | 2026-02-12 |
| Threaded entries | Follow-up responses linked to original entries. AI understands relationship chains. | 2026-02-12 |
| Full-quality video storage | Store all video indefinitely at full quality. Not a cheap tool. | 2026-02-12 |
| Biographical intake required | Not skippable. User must complete it (save & resume supported). | 2026-02-12 |
| Drop BYOK, phased billing | Phase 1: hardcoded API keys, Derek pays directly. Phase 2: company subscription + usage-based pricing + margin. User never touches API keys. | 2026-02-12 |

## Open Questions

- ~~What should the shareable social output look like?~~ RESOLVED: platform-specific formats (tweet, IG caption+photo, weekly Substack)
- ~~How does the productivity/coaching feature coexist with the biographer theme?~~ RESOLVED: dropped — muddies identity
- ~~Product name — "Biographer" or something catchier?~~ RESOLVED: sticking with Biographer
- ~~Monetization model~~ DEFERRED: single-user BYOK for now. Revisit when opening to other users.
- Data privacy/encryption approach — trust is paramount, but E2E encryption conflicts with AI processing needs. Need to find the right model.
- ~~AI billing model~~ RESOLVED: Drop BYOK. Phase 1 hardcoded keys, Phase 2 company subscription + usage pricing.
- ~~How to handle the legacy trigger confirmation reliably~~ RESOLVED: hybrid — 2 years inactivity then executor confirmation
- ~~How does the public AI biographer work?~~ RESOLVED: multi-mode (voice, calendar browse, chat), topic scoping controls, approval before publish

## Session Log

### Session 1 — 2026-02-11
- Transcribed initial voice memo (14:44 duration)
- Captured product vision, core concepts, and feature list
- Started user interview process (Round 1 questions posed, awaiting answers)
- Created persistent memory file and Q&A tracking file
- Round 1 answers received — 5 key decisions locked in
- Core insight emerged: "memory of a memory" concept — the app's value isn't just logging events but tracking their emotional afterlife over time
- Confirmed: Q3 (multiple entries per day) still needs explicit confirmation
- Moving to Round 2
- Round 2 answers received — 6 more decisions locked in (AI tone, writing styles, chapter structure, POV, editing, significance)
- Key design principle: objectivity over empathy in the AI persona to preserve biographical integrity
- Moving to Round 3
- Round 3 answers received — 4 more decisions locked in (legacy config, public biographer, multiple entries/day, data trust)
- New feature emerged: **Public AI Biographer** — publish a living, queryable version of your life story while still alive. Major differentiator.
- Q16 (legacy trigger mechanism) still unanswered — will revisit
- Moving to Round 4
- Round 4 answers received — 6 more decisions locked in (social formats, public journal, legacy trigger, calendar view, location tracking)
- Q16 (legacy trigger) finally resolved: hybrid model — 2 years inactivity → executor email
- Social sharing strategy now fully defined across platforms with weekly Substack digest
- 21 features now on the list, 20 decisions locked in
- Moving to Round 5
- Round 5 answers received — 6 more decisions locked in (deep intake, interviewer personalities, follow-up delivery, async quality check, Interview Me mode, guided prompts)
- Major architectural insight: the app has **two core modes** — (1) Record a diary entry, (2) Be interviewed by your biographer. This shapes the entire home screen and navigation.
- Video content from profile intake is preserved and surfaceable — people interacting with the public AI biographer can see the user speaking, not just read text
- 26 features, 26 decisions locked in
- Moving to Round 6
- Round 6 answers received — 5 more decisions locked in (BYOK, single-user, managed services, full build, learning project)
- Critical reframe: **this is a learning project** — Derek wants to learn to build an app, not just ship one. Guides how we explain tech decisions.
- Monetization deferred. Multi-user auth deferred. BYOK simplifies AI integration significantly.
- 28 features, 31 decisions locked in
- Moving to Round 7
- Round 7 answers received — 6 more decisions locked in (external context, contradictions, tagging, versioning, character map, no therapist)
- Established firm **anti-pattern**: no therapist behavior. Reinforces the objective biographer identity.
- Character map is a powerful feature — turns the biography into a rich narrative with consistent characters
- 33 features, 37 decisions locked in
- Moving to Round 8
- Round 8 answers received — 6 more decisions locked in (public biographer UX, topic scoping, approval workflow, year in review, video editing, book export)
- Public biographer UX now fully defined: voice + calendar browse + chat
- Physical book export = emotionally powerful output format
- 39 features, 43 decisions locked in
- Moving to Round 9
- Round 9 answers received — 6 more decisions locked in (drop coaching, name = Biographer, search, soft delete, highlights reel, English only)
- Productivity/coaching officially dropped — product identity is now clean and singular
- **Product name confirmed: Biographer**
- Highlights reel as a social sharing-oriented output adds another sticky daily-value layer
- 42 features, 49 decisions locked in
- **Interview phase complete** — all major product questions answered across 9 rounds (54 questions total)

### Session 2 — 2026-02-12
- Resumed from terminal saved output
- Round 9 answers captured (6 decisions)
- PM spec review conducted — identified 10 structural gaps
- Round 10 answers received — 10 more decisions locked in (entry data model, batch trigger, tagging model, public page structure, legacy delivery, manual social posting, threaded entries, video storage, required intake, BYOK under review)
- **BYOK dropped** — replaced with phased billing: hardcoded keys (Phase 1), company subscription + usage pricing (Phase 2). Consumer product, not a developer tool.
- Manual social posting locks in significantly reduced engineering scope
- Entry threading established — fundamentally shapes the data model
- BYOK billing resolved: phased approach locked in
- 42 features, 60 decisions locked in — no open blockers remaining except encryption model
