# SOP: Fast, Beautiful Mockup Website Builds
*(based on the Sungai Revive build — brief → layout review → revamp → deploy, all in one session)*

## Why this run worked

1. **One rich brief, not a back-and-forth interview.** The client gave positioning, site structure, audience, future roadmap, and even internal "exec review" commentary in a single message. That let the build start immediately instead of stalling on clarifying questions.
2. **A "show me before you greenlight" checkpoint.** Asking to see the layout before approving caught the wrong tone (dark/tech) early — cheap to fix at mockup stage, expensive to fix after "final."
3. **Reference images did the heavy lifting for visual direction.** Four poster/branding images said more than paragraphs of style guidance could. The revamp matched tone, palette, and energy in one pass because the direction was visual, not verbal.
4. **Constraints stated as rules, not vibes.** "No numbers in the hero, push them lower," "bright/white/green," "must include 4-language toggle" — each was a testable constraint, not a mood. Easy to verify against, easy to satisfy precisely.
5. **Built as a single static file.** No build step, no framework, no deploy pipeline complexity — just HTML/CSS/JS. This kept iteration cycles (edit → reload → screenshot) seconds long.
6. **Visually verified before claiming done, every time.** Local server + headless browser screenshots of every section caught two real bugs (a CSS animation timing issue hiding cards, and a duplicate `class` attribute silently dropping the hero tagline) that code review alone would have missed.
7. **Deploy was a single clear "proceed" instruction.** Once the client said "nice, proceed, share the link," deployment ran straight through — no scope creep, no extra questions, just ship the approved thing.

## The repeatable workflow (SOP)

**Step 1 — Brief intake**
Ask the client for (or accept in one shot): positioning/audience, site structure/sections, any explicit must-haves (e.g. language toggle, specific integrations), and tone/style references (images > adjectives). The more concrete the constraints, the less guessing later.

**Step 2 — Build v1 fast, single file**
Static HTML/CSS/JS, no tooling. Get full structure and content in first, styling second. Speed at this stage matters more than polish — it's a draft to react to.

**Step 3 — Visual proof before greenlight**
Always screenshot every major section (local server + headless browser) and show the client the actual rendered layout before asking for sign-off. Never describe a layout in words and ask for approval — show it.

**Step 4 — Take revamp direction literally**
When given new constraints (palette, tone, audience, "move X lower"), treat each as a hard rule to satisfy, not just inspiration. Re-screenshot after the revamp to confirm every rule was actually met, not just attempted.

**Step 5 — Bug-hunt via real rendering, not just reading code**
Animation timing bugs and attribute bugs (like duplicate `class=""`) are invisible in source review but obvious in a screenshot. Budget time for this pass — it's where real defects surface.

**Step 6 — Deploy only on explicit "proceed"**
Don't deploy speculatively. Wait for clear approval language, then go straight to a live URL with no extra back-and-forth — check for an existing site/project first (never assume "create new" silently), then deploy and verify the URL returns 200 before sharing it.

**Step 7 — Clean up after deploy**
Gitignore any tool-generated local state (e.g. `.netlify/`), commit, push. Don't leave stray untracked files in the repo.

## Tips to keep this smooth next time

- **Lead with reference images** whenever there's a target aesthetic — they compress a paragraph of adjectives into one unambiguous artifact.
- **Phrase revisions as rules** ("don't put numbers in the hero," "must include X") rather than general mood — rules are checkable, vibes aren't.
- **Insist on a visual checkpoint before any greenlight** — for both you and the client. It catches misreads early and cheaply.
- **Stay single-file/no-build for mockups.** Add tooling only once the client is committed past the mockup stage — it slows iteration for no payoff this early.
- **Always re-render and re-screenshot after every meaningful revision**, not just the first build — regressions hide in CSS easily (timing, specificity, duplicate attributes).
- **Don't deploy until you hear an explicit "proceed/ship it."** Build appetite for showing work, not shipping unapproved iterations.
- **Verify the live URL actually returns 200** before handing it over — don't assume the deploy tool succeeded just because it returned without error.

## Reusable prompt pattern (for the client to reuse)

> "[Audience + positioning in 1-2 sentences]. Site structure: [list sections]. Must-have: [hard constraints, e.g. language toggle]. Style reference: [attach images]. Build a mockup first — show me the layout before I greenlight. Static HTML is fine, no need for a framework yet."

Then after reviewing:
> "[Specific, rule-like revision notes]. Refer to [images] for direction."

Then to ship:
> "Proceed. Share the link once done."

This three-message arc (brief → visual revision → approve+ship) is the shape that made this build fast — it's worth keeping as the default pattern for future mockup requests.
