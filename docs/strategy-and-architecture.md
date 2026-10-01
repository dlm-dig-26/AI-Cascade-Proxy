# Strategy & Architecture — Assisted Short-Form Content Brand

**Status:** draft for decision · **Owner:** dlm.digid · **Last updated:** 2026-10-01

This is the founding document. It converts the original brief into a buildable
system and states plainly where the original brief would have killed the project.
Read the [Decisions locked](#1-decisions-locked) and
[Blind spots, risks, assumptions](#2-blind-spots-risks-and-assumptions) sections
before anything else — the rest of the doc depends on them.

---

## 1. Decisions locked

These four choices were made explicitly and shape every downstream decision.

| # | Decision | Chosen | Consequence |
|---|----------|--------|-------------|
| 1 | **Content source** | Transformative commentary on submitted links | Every piece must add substantial original value. A human review gate + fair-use checklist is a hard compliance control, not a formality. |
| 2 | **Automation level** | Assisted — pipeline produces, human reviews + uploads | No posting APIs, no ToS/audit exposure on publishing. Throughput is gated by human review + upload time. |
| 3 | **Branding** | Undecided — recommendation requested | See [§4](#4-branding-recommendation). Recommendation: **"Socket"** name + glitch/"reality has bugs" templated visual system. |
| 4 | **First deliverable** | This strategy + architecture doc | Code follows once [§11 open decisions](#11-open-decisions-before-code) are closed. |

### What "assisted only" actually means — read this

You originally asked for "little to no human intervention except guidelines."
You then chose **assisted**. Those two statements are in direct tension, and the
chosen one wins. Be clear-eyed:

- The pipeline *can* generate your target volume (2–5+ pieces/day/platform).
- A human **must** review each piece against the fair-use checklist **and**
  perform each upload.
- Realistic daily human load with good tooling: **~20–40 minutes/day** (batch
  review in a dashboard, then batch upload). This is the floor, not zero.
- This is the correct trade. The review gate *is* your legal defense and your
  brand-safety control. Removing it is what gets accounts terminated.

---

## 2. Blind spots, risks, and assumptions

Stated bluntly, because you asked for them.

### R1 — "Transformative" is not an automatic safe harbor
Genuine commentary improves your legal footing; it does **not** stop automated
Content ID / DMCA claims from firing. You will still receive false or
aggressive claims and must dispute them. Fair use is a defense argued
after the fact, not a shield that prevents the strike. **Mitigation:** source
whitelist (ingest preferentially from sources with clearer footing or explicit
permission), conservative clip-length limits, substantial added commentary,
and a dispute playbook.

### R2 — Originality demotion ≠ legal fair use
Clearing the *legal* transformative bar does not clear the *algorithmic*
originality bar. As of 2025 all four platforms demote "reaction slop" and
reposted/aggregated content. Your commentary must be the center of gravity of
the video, not a thin frame around someone else's clip. **Mitigation:** enforce
a minimum original-content ratio (see [§7](#7-guardrails-the-human-authored-layer)).

### R3 — Consistent AI visual identity is hard
Keeping a mascot visually consistent across hundreds of auto-generated videos is
an unsolved-enough problem to be a production risk. A **templated motion-graphics
/ glitch aesthetic** is far more reliable to automate than a character that must
look identical every time. This is the main driver of the branding recommendation.

### R4 — The "build volume, then mold sentiment" assumption is fragile
The brief assumes you can acquire an audience with absurdist humor and *later*
steer it toward "a desired content sentiment." Audiences punish bait-and-switch
with churn and backlash. **You must define the end-state sentiment now**, before
acquisition, and acquire against it — not acquire a generic crowd and pivot. If
"mold what's uploaded" means something closer to *merchandising / product / a
point of view you already hold*, say so now so the content ladders toward it from
day one.

### R5 — Cross-posting footprint can still look inauthentic
Even with manual uploads, mechanically identical cross-posts to four platforms
trip "coordinated/inauthentic" heuristics. **Mitigation:** platform-native
variants (aspect ratio, hook, caption, length, trending-audio hooks) rather than
one file posted four times.

### R6 — Per-piece cost compounds
TTS + render + multiple LLM calls per piece × 2–5/day × 4 platforms adds up.
**Mitigation:** set a hard per-piece cost ceiling and track it; cache/reuse
LLM analysis across platform variants of the same piece.

### R7 — One strike cascades
A single copyright strike can nuke a channel and, by association, your operating
pattern. **Mitigation:** per-platform account hygiene, no shared fingerprints
where avoidable, render-pack + source archival so any piece can be defended or
reproduced, and a kill-switch to pull a piece from all platforms fast.

### Assumptions this plan makes (flag if any are wrong)
- A1: You will operate the review + upload step daily (or delegate it). The
  pipeline assumes a reliable human in the loop.
- A2: Submitted source links are things you have *some* basis to comment on
  (public posts, news, viral clips) — not private or paywalled content.
- A3: Budget exists for cloud compute, TTS, and LLM calls at volume (order of
  low-hundreds USD/month at the target cadence; firm number depends on §11).
- A4: The end goal is an owned, monetizable, steerable audience — not vanity
  view counts. Content ladders toward a defined sentiment/offer.

---

## 3. The viable reframe (one paragraph)

An **AI content factory** that turns a submitted source link into original,
transformative short-form commentary in a sharp "everyday logic is broken" niche
— irreverent, funny, absurdist. It auto-produces platform-native variants for
TikTok, Reels, Shorts, and X, queues them behind a human review gate wired to a
fair-use checklist, and exports ready-to-upload render packs. A human approves
and uploads. An analytics loop reads what lands and steers future prompts and
guardrails. Volume + consistency + a defined sentiment = an owned audience you
can actually convert.

---

## 4. Branding recommendation

The brief's "Pepe Socke-t" has two concrete problems: **Pepe the Frog is Matt
Furie's IP** (he has won/settled infringement suits) and it carries
**hate-symbol brand-safety flags** that throttle ad revenue and reach — directly
undercutting a monetization goal. Below are three legally clear, brand-safe
directions that keep the irreverent energy.

### Direction A — "Socket" (continuity pick)
Keep the name energy you already gravitated toward; drop Pepe entirely. Original
mascot: a frayed wall-socket / plug character (or a sock-puppet pun on "sock-et")
that "plugs into" everyday absurdities. **Pros:** ownable, trademark-able,
continuity with your instinct. **Cons:** a recurring character still demands
visual consistency (see R3).

### Direction B — "Logic Gremlin"
A gremlin that sabotages the "common sense" we pretend governs daily life.
**Pros:** strong character + merch potential, clear thematic hook. **Cons:** same
character-consistency cost as A; more crowded naming space.

### Direction C — "Reality Has Bugs" / "Reality.exe"
Frame daily life as buggy software: error popups, glitch overlays, "patch notes
for real life," blue-screen gags. **Pros:** the *cheapest and most reliable
aesthetic to automate* — templated UI/motion-graphics instead of a character that
must render identically every time (directly answers R3). Infinitely extensible
format. **Cons:** less of a cuddly mascot for merch.

### Recommendation
**Name: "Socket." Visual system: Direction C (glitch / "reality has bugs"),**
with a minimal recurring mascot sting from A used sparingly as a brand bumper.

Rationale: "Socket" preserves your naming instinct and is ownable; the
Direction-C visual language is the single biggest lever on production
scalability and cost because it sidesteps character-consistency failure. The
light mascot sting gives you a recognizable brand bumper without betting the
pipeline on perfect character rendering. Revisit once we see real production
output — if the mascot renders reliably, lean harder into A.

> **Decision needed:** confirm name + visual direction, or counter. Everything
> visual in the pipeline (templates, fonts, motion presets) keys off this.

---

## 5. Content strategy

- **Niche:** the gap between how daily life / events / systems *claim* to work
  and how they actually work. Logical flaws, absurd incentives, "why is this
  like this" — exposed with humor.
- **Tone spec (the guardrail input):** irreverent, dry, punchy; punches at
  systems and absurdity, **not** at protected groups or individuals. Humor by
  itself or layered over the observation. No cruelty, no slurs, no targeting.
- **Formats (rotate):**
  1. *Patch notes for real life* — "Reality v2026.10 changelog."
  2. *Logic autopsy* — take a submitted clip, dissect the broken reasoning.
  3. *The absurd incentive* — why a dumb outcome is actually rational for someone.
  4. *Everyday bug report* — a daily annoyance filed as a software bug.
  5. *Overheard / caption-flip* — recontextualize a mundane source into absurdity.
- **Cadence:** pipeline targets ≥2/day/platform, aiming for 5+. Human review
  gate is the real rate limiter — size the daily batch to the review budget.
- **Platform-native variants:** one *idea* → N renders, differing by aspect
  ratio, hook, caption, length, and trending-audio slot. Never one file ×4.

---

## 6. System architecture — the cascade

Each stage is an independent, resumable job. State + queue in a database; media
in object storage. Named for the repo: a **cascade** of transforms sitting as a
**proxy** between raw source and published output.

```
[ Ingest ]    link submitted via dedicated channel  → job row created
     │
[ Acquire ]   fetch source + metadata; record license/source; archive
     │
[ Analyze ]   transcribe (speech-to-text); extract claims/beats; find the
     │        "logical flaw / absurdity" angle
     │
[ Ideate ]    LLM generates transformative angle + hook options, per brand
     │        guidelines; proposes which SHORT source clips (if any) to cite
     │
[ Script ]    VO script + on-screen text + b-roll plan + original-content ratio
     │        check; platform variant specs
     │
[ Produce ]   TTS voice; assemble video (captions, motion graphics, variants);
     │        thumbnails; per-platform caption/hashtags/title
     │
[ REVIEW ]    ← HUMAN GATE. Dashboard. Fair-use checklist. Approve/edit/reject.
     │
[ Package ]   export render pack per platform (file + copy + thumb + suggested
     │        post time) to a folder / Drive
     │
[ Publish ]   ← HUMAN. Manual upload. Log what went where + when.
     │
[ Measure ]   pull/record analytics (manual or read-only APIs)
     │
[ Learn ]     aggregate performance → suggest guideline/prompt updates
```

**Why this shape:** stages are isolated so a failure (e.g. a render error)
retries without re-running analysis; LLM analysis is cached and reused across
platform variants (cost control, R6); the human gate sits at exactly one place;
and publishing is deliberately outside the system (assisted-only, R-free on ToS).

### Proposed stack (for discussion, not locked)
- **Queue + state:** Supabase (Postgres + storage) — jobs, assets, decisions, metrics.
- **Compute:** stage workers (Node/Python). Video assembly via ffmpeg or Remotion.
- **AI:** LLM for analyze/ideate/script; speech-to-text for transcription; TTS for VO.
- **Review dashboard:** lightweight web app (Vercel) reading the queue.
- **Ingest channel:** pick one in §11 (email via Gmail, a web form, or a bot).
- **Packaging target:** Google Drive folder per day (you have Drive access), or
  direct dashboard download.

---

## 7. Guardrails — the human-authored layer

This is the "guidelines and guardrails" layer you said you'd own. It is config,
not code, so it can change without redeploys. Two files drive the pipeline:

### 7a. Fair-use / transformative checklist (blocks packaging until all pass)
- [ ] Original commentary is the **center of gravity** of the piece, not a frame.
- [ ] Source clips used are **short** and **necessary** to the point being made.
- [ ] The piece **adds meaning** the source did not have (critique, analysis, joke).
- [ ] Source is credited where appropriate; not passed off as our footage.
- [ ] Source is **not** private, paywalled, or someone's personal/sensitive content.
- [ ] No targeting of a private individual; punches at systems/absurdity only.
- [ ] Original-content ratio ≥ threshold (default: original ≥ 60% of runtime).
- [ ] Nothing that violates a platform's community guidelines (hate, harassment,
      graphic content, misinformation presented as fact).

### 7b. Brand/tone spec (feeds Ideate + Script prompts)
- Voice, do/don't phrasing, banned topics, the defined end-state sentiment (R4),
  formats in rotation, and the content→offer ladder.

---

## 8. Analytics & sentiment feedback loop

- **Collect:** per-piece metrics (views, retention, saves, shares, comments
  sentiment) — manual entry at first, read-only platform analytics later.
- **Attribute:** tie metrics back to the idea, format, hook, and angle.
- **Learn:** rank formats/hooks; surface what the acquired audience actually
  rewards; propose guideline updates (never auto-apply — human confirms, per R4).
- **Guard against drift:** watch comment sentiment vs. the *defined* end-state
  sentiment, not just raw engagement, so volume doesn't quietly pull the brand
  somewhere you can't monetize.

---

## 9. Repository structure (proposed)

```
AI-Cascade-Proxy/
├─ README.md
├─ docs/
│  └─ strategy-and-architecture.md   ← this file
│  └─ guardrails/                    ← fair-use checklist + brand/tone spec (next)
├─ pipeline/                         ← stage workers (ingest…learn)
├─ dashboard/                        ← review gate web app
└─ shared/                           ← db schema, types, config
```

---

## 10. Phased roadmap

- **Phase 0 — Decisions (now):** close §11. Lock brand, ingest channel, stack, budget.
- **Phase 1 — Manual spine:** DB schema + ingest + a dead-simple review dashboard.
  Produce 1 piece end-to-end *mostly by hand* to validate the format and the
  fair-use checklist on real content before automating.
- **Phase 2 — Automate the cascade:** analyze → ideate → script → produce, with
  caching and per-piece cost tracking. Target one platform first, then fan out.
- **Phase 3 — Volume + variants:** platform-native variants, daily batch review,
  render packs to Drive.
- **Phase 4 — Learn:** analytics ingestion + the feedback loop; guideline tuning.

Ship Phase 1 before trusting any automation — the checklist and the format need
to survive contact with real source material first.

---

## 11. Open decisions (before code)

1. **Brand:** confirm "Socket" + Direction C, or counter ([§4](#4-branding-recommendation)).
2. **End-state sentiment / goal (R4):** what is the audience *for*? Define the
   offer/POV now so content ladders toward it.
3. **Ingest channel:** email (Gmail), web form, or a bot (e.g. Telegram)? Who
   submits links — just you, or a wider feed?
4. **Stack confirmation:** Supabase + Vercel + ffmpeg/Remotine acceptable? Any
   existing accounts/preferences?
5. **AI providers:** which LLM / TTS / speech-to-text, and the **per-piece cost
   ceiling** (R6).
6. **Source policy (R1):** define the source whitelist and clip-length limits.
7. **Daily human budget:** how many minutes/day for review + upload? This sizes
   the batch and the realistic cadence.

---

*Nothing in this document is legal advice. The fair-use checklist is an
operational risk-reduction control, not a guarantee of non-infringement.
Confirm your approach with a qualified attorney before operating at scale.*
