# New Project Reference — Single-File Multilingual Website

> Copy-paste this into your next session. Replace all [PLACEHOLDERS] with client-specific info.
> Based on the Sungai Revive build — bright, poster-style, 4-language static site.

---

## PART 1 — THE BRIEF TEMPLATE (paste this to start a new build)

```
Client: [CLIENT NAME / PROJECT NAME]
Audience: [e.g. schools, communities, corporates, NGOs — who is this for?]
Purpose: [e.g. movement awareness, toolkit distribution, ESG reporting, fundraising]

Site sections (in order):
1. Hero — [headline, tagline, CTA buttons]
2. Why It Matters — [3–5 pillar cards]
3. Journey/Roadmap — [3–4 timeline phases]
4. Toolkit/Resources — [4–6 resource cards]
5. Activities/Programme — [3–4 activity cards]
6. Science/Method — [3 tech cards + explainer grid]
7. Impact Stats — [4 stat counters]
8. ESG/Dashboard — [9 metric boxes + SDG alignment]
9. Get Involved — [4–5 involvement roles]
10. CTA Banner — [headline + 2 buttons]
11. Footer — [brand blurb + 3 link columns]

Languages required: English / Bahasa Malaysia / Chinese / Iban
(or replace Iban with another language if different client)

Tone: [bright, cheerful, poster-style / professional / playful / etc.]
Colors: [primary, accent, background — or attach reference images]
Must-haves: [e.g. 4-language toggle, ESG dashboard, animated counters]

Build a mockup first — show me the layout before I greenlight. Static HTML, no framework needed.
```

---

## PART 2 — THE SOP (workflow to follow every time)

**Step 1 — Rich brief, not interviews.**
Get positioning, site structure, hard constraints, and visual references in one shot. Images beat adjectives — ask for them.

**Step 2 — Build v1 fast, single HTML file.**
Full structure + content first, polish second. No build tools, no framework — just HTML/CSS/JS.

**Step 3 — Screenshot before greenlight.**
Always render locally (python3 -m http.server 8910) + Playwright screenshots of every major section. Never describe a layout in words — show it.

**Step 4 — Take revision notes literally.**
Each note is a hard rule to satisfy, not inspiration. Re-screenshot after changes.

**Step 5 — Bug-hunt via real rendering.**
Animation bugs and duplicate-attribute bugs are invisible in source. Screenshot catches them.

**Step 6 — Deploy only on explicit "proceed".**
Wait for clear approval, then deploy straight to live URL with no extra back-and-forth.

**Step 7 — Clean up.**
Gitignore tool-generated state (e.g. .netlify/), commit, push.

---

## PART 3 — THE COMPLETE BOILERPLATE HTML

> Replace all [PLACEHOLDERS] marked with brackets. The 4-language pattern (data-lang spans) is already wired in — just swap the content per language.

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>[PROJECT NAME] — [TAGLINE]</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Baloo+2:wght@500;600;700;800&family=Poppins:wght@300;400;500;600;700;800;900&display=swap" rel="stylesheet">
<style>
:root {
  --river: #0ea5e9;        /* primary accent — change to match client brand */
  --river-deep: #0284c7;
  --leaf: #22c55e;         /* secondary accent */
  --leaf-deep: #16a34a;
  --sun: #fbbf24;          /* tertiary / CTA accent */
  --sun-deep: #f59e0b;
  --coral: #fb7185;
  --ink: #0f3b2e;          /* dark text */
  --muted: #5b7570;
  --cream: #fbfdf9;        /* page background */
  --white: #ffffff;
  --paper: #f3fbf2;
  --sky: #eaf8ff;
}

* { margin: 0; padding: 0; box-sizing: border-box; }
html { scroll-behavior: smooth; }

body {
  font-family: 'Poppins', sans-serif;
  background: var(--cream);
  color: var(--ink);
  overflow-x: hidden;
}

h1, h2, h3, .display { font-family: 'Baloo 2', sans-serif; }

/* ─── NAV ─── */
nav {
  position: fixed;
  top: 0; left: 0; right: 0;
  z-index: 1000;
  padding: 0 2rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 76px;
  background: rgba(255,255,255,0.9);
  backdrop-filter: blur(16px);
  border-bottom: 1px solid rgba(34,197,94,0.12);
  transition: all 0.3s;
}

.nav-logo {
  display: flex;
  align-items: center;
  gap: 10px;
  text-decoration: none;
}

.nav-logo .drop {
  width: 40px; height: 40px;
  background: linear-gradient(140deg, var(--river), var(--leaf));
  border-radius: 50% 50% 50% 0;
  transform: rotate(-45deg);
  flex-shrink: 0;
  position: relative;
  box-shadow: 0 4px 14px rgba(34,197,94,0.35);
  animation: bob 3s ease-in-out infinite;
}

@keyframes bob {
  0%,100% { transform: rotate(-45deg) translateY(0); }
  50% { transform: rotate(-45deg) translateY(-4px); }
}

.nav-logo span {
  font-family: 'Baloo 2', sans-serif;
  font-size: 1.3rem;
  font-weight: 800;
  color: var(--ink);
}

.nav-logo span em {
  color: var(--leaf-deep);
  font-style: normal;
}

.nav-links {
  display: flex;
  align-items: center;
  gap: 1.8rem;
  list-style: none;
}

.nav-links a {
  color: var(--muted);
  text-decoration: none;
  font-size: 0.88rem;
  font-weight: 600;
  transition: color 0.2s;
}

.nav-links a:hover { color: var(--leaf-deep); }

.lang-toggle {
  display: flex;
  gap: 4px;
  background: var(--paper);
  border: 1px solid rgba(34,197,94,0.2);
  border-radius: 25px;
  padding: 4px;
}

.lang-btn {
  padding: 5px 11px;
  border-radius: 20px;
  border: none;
  background: transparent;
  color: var(--muted);
  font-size: 0.72rem;
  font-weight: 700;
  cursor: pointer;
  transition: all 0.2s;
}

.lang-btn.active {
  background: var(--leaf);
  color: white;
  box-shadow: 0 2px 8px rgba(34,197,94,0.4);
}

.nav-cta {
  background: linear-gradient(135deg, var(--sun), var(--sun-deep));
  color: white !important;
  padding: 10px 20px;
  border-radius: 25px;
  font-weight: 700 !important;
  font-size: 0.85rem !important;
  box-shadow: 0 4px 14px rgba(245,158,11,0.35);
  transition: transform 0.2s !important;
}

.nav-cta:hover { transform: translateY(-2px); color: white !important; }

/* ─── HERO ─── */
.hero {
  min-height: 100vh;
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  padding: 110px 2rem 4rem;
  background: linear-gradient(180deg, #eafdf3 0%, #e3f7ff 45%, #fef9e7 100%);
}

.blob { position: absolute; border-radius: 50%; filter: blur(5px); opacity: 0.5; }
.blob-1 { width: 340px; height: 340px; background: radial-gradient(circle, #bbf7d0, transparent 70%); top: -80px; left: -80px; }
.blob-2 { width: 420px; height: 420px; background: radial-gradient(circle, #bae6fd, transparent 70%); bottom: -120px; right: -100px; }
.blob-3 { width: 260px; height: 260px; background: radial-gradient(circle, #fde68a, transparent 70%); top: 40%; right: 6%; }

.float-icon {
  position: absolute;
  font-size: 2.2rem;
  animation: floaty 6s ease-in-out infinite;
  opacity: 0.85;
  filter: drop-shadow(0 6px 10px rgba(0,0,0,0.08));
}

@keyframes floaty {
  0%,100% { transform: translateY(0) rotate(-4deg); }
  50% { transform: translateY(-18px) rotate(4deg); }
}

.hero-content { position: relative; z-index: 5; max-width: 900px; text-align: center; }

.hero-badge {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  background: white;
  border: 2px dashed var(--leaf);
  border-radius: 30px;
  padding: 8px 20px;
  font-size: 0.8rem;
  font-weight: 700;
  color: var(--leaf-deep);
  margin-bottom: 1.8rem;
  box-shadow: 0 4px 14px rgba(34,197,94,0.15);
}

.hero h1 {
  font-size: clamp(2.6rem, 6.5vw, 5rem);
  font-weight: 800;
  line-height: 1.08;
  margin-bottom: 1.2rem;
  color: var(--ink);
}

.hero h1 .highlight {
  background: linear-gradient(135deg, var(--river), var(--leaf-deep));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.hero-tagline {
  font-size: 1.15rem;
  color: var(--muted);
  margin: 0 auto 1rem;
  line-height: 1.7;
  max-width: 640px;
  font-weight: 500;
}

.hero-bm-badge {
  display: inline-block;
  background: linear-gradient(135deg, var(--sun), var(--coral));
  color: white;
  font-weight: 700;
  font-size: 0.95rem;
  padding: 10px 26px;
  border-radius: 40px;
  margin: 0.5rem 0 2rem;
  box-shadow: 0 6px 18px rgba(251,113,133,0.3);
  transform: rotate(-2deg);
}

.hero-btns { display: flex; gap: 1rem; flex-wrap: wrap; justify-content: center; }

.btn-primary {
  background: linear-gradient(135deg, var(--leaf), var(--leaf-deep));
  color: white;
  padding: 16px 32px;
  border-radius: 50px;
  text-decoration: none;
  font-weight: 700;
  font-size: 0.95rem;
  display: inline-flex;
  align-items: center;
  gap: 8px;
  transition: all 0.3s;
  box-shadow: 0 8px 24px rgba(34,197,94,0.35);
}

.btn-primary:hover { transform: translateY(-3px) scale(1.02); box-shadow: 0 12px 30px rgba(34,197,94,0.45); }

.btn-secondary {
  background: white;
  color: var(--ink);
  padding: 16px 32px;
  border-radius: 50px;
  text-decoration: none;
  font-weight: 700;
  font-size: 0.95rem;
  border: 2px solid var(--river);
  display: inline-flex;
  align-items: center;
  gap: 8px;
  transition: all 0.3s;
}

.btn-secondary:hover { background: var(--sky); transform: translateY(-3px); }

.hero-mascots { display: flex; justify-content: center; gap: 0.6rem; margin-top: 2.5rem; }

.mascot-pill {
  background: white;
  border-radius: 30px;
  padding: 8px 16px;
  box-shadow: 0 4px 14px rgba(0,0,0,0.06);
  font-size: 0.78rem;
  font-weight: 700;
  color: var(--ink);
  display: flex;
  align-items: center;
  gap: 6px;
}

.scroll-indicator {
  position: absolute;
  bottom: 28px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 4px;
  opacity: 0.6;
  animation: bounce 2s infinite;
  z-index: 10;
}

@keyframes bounce {
  0%,100% { transform: translateX(-50%) translateY(0); }
  50% { transform: translateX(-50%) translateY(8px); }
}

.scroll-indicator span { font-size: 0.68rem; letter-spacing: 2px; text-transform: uppercase; color: var(--muted); font-weight: 700; }
.scroll-arrow { font-size: 1.2rem; color: var(--leaf-deep); }

/* ─── PARTNERS STRIP ─── */
.partners-strip {
  background: white;
  border-top: 1px solid rgba(34,197,94,0.1);
  border-bottom: 1px solid rgba(34,197,94,0.1);
  padding: 1.6rem 2rem;
  text-align: center;
}

.partners-strip p {
  font-size: 0.72rem;
  font-weight: 800;
  letter-spacing: 2px;
  color: var(--muted);
  text-transform: uppercase;
  margin-bottom: 1rem;
}

.partners-logos { display: flex; justify-content: center; gap: 1rem; flex-wrap: wrap; align-items: center; }

.partner-logo-pill {
  background: var(--paper);
  border: 1px solid rgba(34,197,94,0.2);
  border-radius: 30px;
  padding: 8px 20px;
  font-size: 0.85rem;
  font-weight: 700;
  color: var(--ink);
}

/* ─── SECTION COMMONS ─── */
section { padding: 5.5rem 2rem; }
.container { max-width: 1200px; margin: 0 auto; }

.section-label {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  background: var(--paper);
  color: var(--leaf-deep);
  font-size: 0.75rem;
  font-weight: 800;
  letter-spacing: 1.5px;
  text-transform: uppercase;
  margin-bottom: 1.2rem;
  padding: 6px 16px;
  border-radius: 20px;
}

.section-title { font-size: clamp(1.9rem, 4vw, 2.9rem); font-weight: 800; line-height: 1.2; margin-bottom: 1rem; color: var(--ink); }
.section-sub { color: var(--muted); font-size: 1.02rem; line-height: 1.75; max-width: 620px; font-weight: 500; }
.center { text-align: center; margin-left: auto; margin-right: auto; }
.text-river { color: var(--river-deep); }
.text-leaf { color: var(--leaf-deep); }
.text-sun { color: var(--sun-deep); }
.text-coral { color: var(--coral); }

/* ─── PILLAR CARDS ─── */
.why-rivers { background: var(--white); }

.pillars-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 1.5rem; margin-top: 3rem; }

.pillar-card {
  background: var(--paper);
  border: 2px solid transparent;
  border-radius: 24px;
  padding: 2.2rem 1.6rem;
  text-align: center;
  transition: all 0.35s;
  cursor: default;
}

.pillar-card:hover { border-color: var(--leaf); transform: translateY(-8px) rotate(-1deg); box-shadow: 0 20px 40px rgba(34,197,94,0.18); background: white; }

.pillar-icon { width: 76px; height: 76px; border-radius: 26px; display: flex; align-items: center; justify-content: center; font-size: 2.1rem; margin: 0 auto 1.2rem; }

.pillar-card h3 { font-size: 1.1rem; font-weight: 700; margin-bottom: 0.6rem; color: var(--ink); }
.pillar-card p { font-size: 0.85rem; color: var(--muted); line-height: 1.65; }

/* ─── STATS ─── */
.stats-strip { background: linear-gradient(135deg, #0ea5e9, #16a34a); padding: 4rem 2rem; }
.stats-strip .section-label { background: rgba(255,255,255,0.2); color: white; }
.stats-strip .section-title { color: white; }
.stats-strip .section-sub { color: rgba(255,255,255,0.85); }

.stats-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(180px, 1fr)); gap: 1.2rem; margin-top: 2.5rem; }

.stat-card {
  background: rgba(255,255,255,0.15);
  border: 1px solid rgba(255,255,255,0.3);
  border-radius: 20px;
  padding: 1.8rem 1rem;
  text-align: center;
  backdrop-filter: blur(8px);
  transition: all 0.3s;
}

.stat-card:hover { transform: translateY(-6px); background: rgba(255,255,255,0.25); }
.stat-icon { font-size: 2rem; margin-bottom: 0.5rem; }
.stat-num { font-size: 2.3rem; font-weight: 800; color: white; line-height: 1; margin-bottom: 0.3rem; font-family: 'Baloo 2', sans-serif; }
.stat-label { font-size: 0.8rem; color: rgba(255,255,255,0.9); font-weight: 600; }

/* ─── TIMELINE ─── */
.journey { background: var(--sky); }
.timeline { position: relative; margin-top: 3rem; }
.timeline::before { content: ''; position: absolute; left: 50%; top: 0; bottom: 0; width: 4px; background: repeating-linear-gradient(180deg, var(--river) 0 14px, transparent 14px 24px); transform: translateX(-50%); border-radius: 4px; }
.timeline-item { display: grid; grid-template-columns: 1fr 70px 1fr; gap: 1rem; margin-bottom: 2.5rem; align-items: center; }
.timeline-item:nth-child(even) .tl-content { grid-column: 3; text-align: left; }
.timeline-item:nth-child(odd) .tl-content { grid-column: 1; text-align: right; }
.timeline-item .tl-dot { grid-column: 2; }
.tl-content { background: white; border-radius: 20px; padding: 1.6rem; box-shadow: 0 6px 20px rgba(14,165,233,0.1); transition: all 0.3s; }
.tl-content:hover { box-shadow: 0 12px 30px rgba(14,165,233,0.2); transform: translateY(-4px); }
.tl-dot { width: 60px; height: 60px; background: linear-gradient(135deg, var(--river), var(--leaf)); border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 1.5rem; margin: 0 auto; box-shadow: 0 0 0 6px white, 0 0 0 9px rgba(34,197,94,0.2); }
.tl-phase { font-size: 0.72rem; font-weight: 800; letter-spacing: 1.5px; color: var(--leaf-deep); text-transform: uppercase; margin-bottom: 0.4rem; }
.tl-content h3 { font-size: 1.1rem; font-weight: 700; margin-bottom: 0.5rem; color: var(--ink); }
.tl-content p { font-size: 0.85rem; color: var(--muted); line-height: 1.65; }

/* ─── TOOLKIT ─── */
.toolkit { background: white; }
.toolkit-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 1.5rem; margin-top: 3rem; }
.toolkit-card { border-radius: 24px; padding: 2.2rem; text-decoration: none; color: var(--ink); transition: all 0.35s; display: block; border: 2px solid transparent; }
.toolkit-card:hover { transform: translateY(-8px) rotate(-0.5deg); box-shadow: 0 20px 40px rgba(0,0,0,0.1); }
.tk-blue { background: #eaf8ff; } .tk-green { background: #effdf2; } .tk-amber { background: #fff8e6; }
.tk-teal { background: #e6fbf8; } .tk-coral { background: #fff0f1; } .tk-purple { background: #f4f0ff; }
.tk-icon { font-size: 2.6rem; margin-bottom: 1rem; display: block; }
.toolkit-card h3 { font-size: 1.15rem; font-weight: 700; margin-bottom: 0.5rem; }
.toolkit-card p { font-size: 0.85rem; color: var(--muted); line-height: 1.65; margin-bottom: 1.2rem; }
.tk-tags { display: flex; flex-wrap: wrap; gap: 6px; }
.tk-tag { background: white; border-radius: 20px; padding: 4px 12px; font-size: 0.72rem; font-weight: 700; color: var(--ink); box-shadow: 0 2px 6px rgba(0,0,0,0.06); }

/* ─── ACTIVITIES ─── */
.activities { background: var(--paper); }
.activities-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 1.5rem; margin-top: 3rem; }
.activity-card { border-radius: 24px; overflow: hidden; background: white; box-shadow: 0 6px 20px rgba(0,0,0,0.06); transition: all 0.35s; }
.activity-card:hover { transform: translateY(-8px); box-shadow: 0 20px 40px rgba(34,197,94,0.18); }
.activity-img { height: 170px; display: flex; align-items: center; justify-content: center; font-size: 4.2rem; }
.ai-blue { background: linear-gradient(135deg, #bae6fd, #eaf8ff); } .ai-green { background: linear-gradient(135deg, #bbf7d0, #effdf2); }
.ai-amber { background: linear-gradient(135deg, #fde68a, #fff8e6); } .ai-teal { background: linear-gradient(135deg, #99f6e4, #e6fbf8); }
.activity-body { padding: 1.6rem; }
.activity-type { font-size: 0.7rem; font-weight: 800; letter-spacing: 1.5px; text-transform: uppercase; color: var(--river-deep); margin-bottom: 0.5rem; }
.activity-card h3 { font-size: 1.05rem; font-weight: 700; margin-bottom: 0.6rem; line-height: 1.3; color: var(--ink); }
.activity-card p { font-size: 0.83rem; color: var(--muted); line-height: 1.6; }
.activity-footer { display: flex; justify-content: space-between; align-items: center; margin-top: 1rem; padding-top: 1rem; border-top: 1px solid #eee; }
.activity-age { font-size: 0.74rem; color: var(--muted); font-weight: 500; }
.activity-link { font-size: 0.8rem; font-weight: 700; color: var(--leaf-deep); text-decoration: none; }

/* ─── SCIENCE ─── */
.science { background: white; }
.tech-cards { display: grid; grid-template-columns: repeat(3, 1fr); gap: 2rem; margin-top: 3rem; }
.tech-card { text-align: center; padding: 2.5rem 1.6rem; border-radius: 28px; background: var(--paper); transition: all 0.35s; }
.tech-card:hover { transform: translateY(-8px); box-shadow: 0 20px 40px rgba(34,197,94,0.15); background: white; }
.tech-visual { width: 100px; height: 100px; border-radius: 50%; margin: 0 auto 1.5rem; display: flex; align-items: center; justify-content: center; font-size: 3rem; }
.tv-blue { background: linear-gradient(135deg, #bae6fd, #eaf8ff); } .tv-green { background: linear-gradient(135deg, #bbf7d0, #effdf2); } .tv-amber { background: linear-gradient(135deg, #fde68a, #fff8e6); }
.tech-card h3 { font-size: 1.2rem; font-weight: 700; margin-bottom: 0.8rem; color: var(--ink); }
.tech-card p { font-size: 0.85rem; color: var(--muted); line-height: 1.7; }
.tech-metrics { display: flex; justify-content: center; gap: 1.5rem; margin-top: 1.5rem; padding-top: 1.5rem; border-top: 1px solid rgba(0,0,0,0.08); }
.tech-metric { text-align: center; }
.tech-metric .num { font-size: 1.2rem; font-weight: 800; color: var(--river-deep); }
.tech-metric .lbl { font-size: 0.68rem; color: var(--muted); }
.wq-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(180px, 1fr)); gap: 1.2rem; margin-top: 2rem; }
.wq-card { background: var(--paper); border-radius: 18px; padding: 1.3rem; }
.wq-name { font-size: 0.72rem; font-weight: 800; letter-spacing: 1px; color: var(--muted); text-transform: uppercase; margin-bottom: 0.3rem; }
.wq-label { font-size: 0.98rem; font-weight: 700; margin-bottom: 0.8rem; color: var(--ink); }
.wq-bar { height: 7px; background: rgba(0,0,0,0.08); border-radius: 4px; overflow: hidden; margin-bottom: 0.5rem; }
.wq-fill { height: 100%; border-radius: 4px; }
.wq-desc { font-size: 0.76rem; color: var(--muted); line-height: 1.55; }

/* ─── ESG DASHBOARD ─── */
.esg { background: var(--sky); }
.esg-dashboard { background: white; border-radius: 28px; padding: 2.5rem; margin-top: 3rem; box-shadow: 0 10px 40px rgba(14,165,233,0.1); }
.esg-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 2rem; flex-wrap: wrap; gap: 1rem; }
.esg-title-block h3 { font-size: 1.3rem; font-weight: 700; color: var(--ink); }
.esg-title-block p { font-size: 0.85rem; color: var(--muted); }
.live-badge { display: flex; align-items: center; gap: 6px; background: #effdf2; border: 1px solid rgba(34,197,94,0.3); border-radius: 20px; padding: 6px 14px; font-size: 0.78rem; font-weight: 700; color: var(--leaf-deep); }
.live-dot { width: 6px; height: 6px; background: var(--leaf); border-radius: 50%; animation: blink 1.5s infinite; }
@keyframes blink { 0%,100% { opacity: 1; } 50% { opacity: 0.2; } }
.metrics-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(160px, 1fr)); gap: 1rem; margin-bottom: 2rem; }
.metric-box { background: var(--paper); border-radius: 18px; padding: 1.3rem; text-align: center; transition: all 0.3s; }
.metric-box:hover { background: #eaf8ff; transform: translateY(-4px); }
.metric-box .icon { font-size: 1.6rem; margin-bottom: 0.4rem; }
.metric-box .number { font-size: 1.9rem; font-weight: 800; line-height: 1; margin-bottom: 0.2rem; font-family: 'Baloo 2', sans-serif; }
.metric-box .label { font-size: 0.75rem; color: var(--muted); font-weight: 600; }
.sdg-row { display: flex; flex-wrap: wrap; gap: 0.8rem; margin-top: 1.5rem; padding-top: 1.5rem; border-top: 1px solid #eee; }
.sdg-badge { padding: 7px 16px; border-radius: 20px; font-size: 0.74rem; font-weight: 800; border: none; }

/* ─── GET INVOLVED ─── */
.get-involved { background: white; }
.involve-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 1.2rem; margin-top: 3rem; }
.involve-card { padding: 2.2rem 1.6rem; border-radius: 22px; text-align: center; text-decoration: none; color: var(--ink); transition: all 0.35s; background: var(--paper); display: block; }
.involve-card:hover { transform: translateY(-8px) rotate(-1deg); box-shadow: 0 16px 36px rgba(34,197,94,0.2); background: white; }
.involve-icon { font-size: 2.6rem; margin-bottom: 1rem; }
.involve-card h3 { font-size: 1.05rem; font-weight: 700; margin-bottom: 0.4rem; }
.involve-card p { font-size: 0.8rem; color: var(--muted); line-height: 1.55; }

/* ─── CTA BANNER ─── */
.cta-banner { background: linear-gradient(135deg, #fde68a 0%, #bbf7d0 50%, #bae6fd 100%); text-align: center; padding: 5rem 2rem; }
.cta-banner h2 { font-size: clamp(2rem, 4vw, 3rem); font-weight: 800; margin-bottom: 1rem; color: var(--ink); }
.cta-banner p { font-size: 1.05rem; color: var(--ink); opacity: 0.75; margin-bottom: 2rem; font-weight: 500; }
.cta-banner .btns { display: flex; gap: 1rem; justify-content: center; flex-wrap: wrap; }

/* ─── FOOTER ─── */
footer { background: var(--ink); padding: 4rem 2rem 2rem; color: white; }
.footer-grid { max-width: 1200px; margin: 0 auto; display: grid; grid-template-columns: 2fr 1fr 1fr 1fr; gap: 3rem; margin-bottom: 3rem; }
.footer-brand p { font-size: 0.85rem; color: rgba(255,255,255,0.65); line-height: 1.7; margin: 1rem 0; }
.footer-tagline { font-size: 0.8rem; color: var(--sun); font-weight: 700; }
.footer-col h4 { font-size: 0.8rem; font-weight: 800; letter-spacing: 1px; text-transform: uppercase; color: rgba(255,255,255,0.5); margin-bottom: 1rem; }
.footer-col ul { list-style: none; display: flex; flex-direction: column; gap: 0.7rem; }
.footer-col a { color: rgba(255,255,255,0.75); text-decoration: none; font-size: 0.86rem; transition: color 0.2s; }
.footer-col a:hover { color: var(--leaf); }
.footer-bottom { max-width: 1200px; margin: 0 auto; display: flex; justify-content: space-between; align-items: center; padding-top: 2rem; border-top: 1px solid rgba(255,255,255,0.1); flex-wrap: wrap; gap: 1rem; }
.footer-bottom p { font-size: 0.78rem; color: rgba(255,255,255,0.4); }
.footer-partners { display: flex; gap: 1rem; align-items: center; }
.partner-pill { background: rgba(255,255,255,0.08); border-radius: 20px; padding: 4px 14px; font-size: 0.74rem; font-weight: 700; color: rgba(255,255,255,0.7); }

/* ─── SCROLL ANIMATIONS ─── */
.fade-up { opacity: 0; transform: translateY(24px); transition: opacity 0.5s ease, transform 0.5s ease; }
.fade-up.visible { opacity: 1; transform: translateY(0); }

/* ─── RESPONSIVE ─── */
@media (max-width: 1024px) {
  .toolkit-grid { grid-template-columns: repeat(2, 1fr); }
  .tech-cards { grid-template-columns: repeat(2, 1fr); }
}

@media (max-width: 768px) {
  .timeline::before { left: 30px; }
  .timeline-item { grid-template-columns: 60px 1fr; }
  .timeline-item:nth-child(odd) .tl-content,
  .timeline-item:nth-child(even) .tl-content { grid-column: 2; text-align: left; }
  .timeline-item .tl-dot { grid-column: 1; }
  .toolkit-grid { grid-template-columns: 1fr; }
  .tech-cards { grid-template-columns: 1fr; }
  .footer-grid { grid-template-columns: 1fr 1fr; }
  .nav-links { display: none; }
  .stats-grid { grid-template-columns: repeat(2, 1fr); }
}

/* ─── LANGUAGE TOGGLE ─── */
[data-lang] { display: none; }
[data-lang].lang-active { display: inline; }
div[data-lang].lang-active, p[data-lang].lang-active { display: block; }
</style>
</head>
<body>

<!-- NAV -->
<nav>
  <a href="#" class="nav-logo">
    <div class="drop"></div>
    <span>[PROJECT <em>NAME</em>]</span>
  </a>

  <ul class="nav-links">
    <li><a href="#about"><span data-lang="en" class="lang-active">About</span><span data-lang="bm">Tentang</span><span data-lang="zh">[ZH]</span><span data-lang="ib">[IB]</span></a></li>
    <li><a href="#toolkit"><span data-lang="en" class="lang-active">Toolkit</span><span data-lang="bm">Toolkit</span><span data-lang="zh">[ZH]</span><span data-lang="ib">[IB]</span></a></li>
    <li><a href="#activities"><span data-lang="en" class="lang-active">Activities</span><span data-lang="bm">Aktiviti</span><span data-lang="zh">[ZH]</span><span data-lang="ib">[IB]</span></a></li>
    <li><a href="#science"><span data-lang="en" class="lang-active">Science</span><span data-lang="bm">Sains</span><span data-lang="zh">[ZH]</span><span data-lang="ib">[IB]</span></a></li>
    <li><a href="#esg"><span data-lang="en" class="lang-active">ESG</span><span data-lang="bm">ESG</span><span data-lang="zh">ESG</span><span data-lang="ib">ESG</span></a></li>
    <li><a href="#involve" class="nav-cta"><span data-lang="en" class="lang-active">[Join CTA] 🌱</span><span data-lang="bm">[BM CTA] 🌱</span><span data-lang="zh">[ZH CTA] 🌱</span><span data-lang="ib">[IB CTA] 🌱</span></a></li>
  </ul>

  <div class="lang-toggle">
    <button class="lang-btn active" onclick="setLang('en')">EN</button>
    <button class="lang-btn" onclick="setLang('bm')">BM</button>
    <button class="lang-btn" onclick="setLang('zh')">中文</button>
    <button class="lang-btn" onclick="setLang('ib')">Iban</button>
  </div>
</nav>

<!-- HERO -->
<section class="hero" id="home">
  <div class="blob blob-1"></div>
  <div class="blob blob-2"></div>
  <div class="blob blob-3"></div>
  <div class="float-icon" style="top:18%; left:8%;">[EMOJI]</div>
  <div class="float-icon" style="top:62%; left:6%; animation-delay:1s;">[EMOJI]</div>
  <div class="float-icon" style="top:24%; right:9%; animation-delay:2s;">[EMOJI]</div>
  <div class="float-icon" style="top:70%; right:10%; animation-delay:1.5s;">[EMOJI]</div>
  <div class="float-icon" style="top:46%; left:14%; animation-delay:0.5s;">[EMOJI]</div>

  <div class="hero-content">
    <div class="hero-badge">
      <span data-lang="en" class="lang-active">[BADGE TEXT EN]</span>
      <span data-lang="bm">[BADGE TEXT BM]</span>
      <span data-lang="zh">[BADGE TEXT ZH]</span>
      <span data-lang="ib">[BADGE TEXT IB]</span>
    </div>

    <h1>
      <span data-lang="en" class="lang-active">[HERO HEADLINE EN] <span class="highlight">[KEYWORD]</span>!</span>
      <span data-lang="bm">[HERO HEADLINE BM] <span class="highlight">[KEYWORD BM]</span>!</span>
      <span data-lang="zh">[HERO HEADLINE ZH]<span class="highlight">[KEYWORD ZH]</span>！</span>
      <span data-lang="ib">[HERO HEADLINE IB] <span class="highlight">[KEYWORD IB]</span>!</span>
    </h1>

    <p class="hero-tagline lang-active" data-lang="en">[TAGLINE EN]</p>
    <p class="hero-tagline" data-lang="bm">[TAGLINE BM]</p>
    <p class="hero-tagline" data-lang="zh">[TAGLINE ZH]</p>
    <p class="hero-tagline" data-lang="ib">[TAGLINE IB]</p>

    <div>
      <span class="hero-bm-badge">✨ [BRANDED MALAY SLOGAN]</span>
    </div>

    <div class="hero-btns">
      <a href="#toolkit" class="btn-primary">
        <span data-lang="en" class="lang-active">[CTA 1 EN]</span>
        <span data-lang="bm">[CTA 1 BM]</span>
        <span data-lang="zh">[CTA 1 ZH]</span>
        <span data-lang="ib">[CTA 1 IB]</span>
      </a>
      <a href="#involve" class="btn-secondary">
        <span data-lang="en" class="lang-active">[CTA 2 EN]</span>
        <span data-lang="bm">[CTA 2 BM]</span>
        <span data-lang="zh">[CTA 2 ZH]</span>
        <span data-lang="ib">[CTA 2 IB]</span>
      </a>
    </div>

    <div class="hero-mascots">
      <span class="mascot-pill">[EMOJI] [AUDIENCE 1]</span>
      <span class="mascot-pill">[EMOJI] [AUDIENCE 2]</span>
      <span class="mascot-pill">[EMOJI] [AUDIENCE 3]</span>
    </div>
  </div>

  <div class="scroll-indicator">
    <span>Scroll to Explore</span>
    <div class="scroll-arrow">↓</div>
  </div>
</section>

<!-- PARTNERS STRIP -->
<div class="partners-strip">
  <p>
    <span data-lang="en" class="lang-active">Proudly powered by</span>
    <span data-lang="bm">Dengan bangga disokong oleh</span>
    <span data-lang="zh">荣幸支持单位</span>
    <span data-lang="ib">Dikuasaka enggau ati ati</span>
  </p>
  <div class="partners-logos">
    <div class="partner-logo-pill">[PARTNER 1]</div>
    <div class="partner-logo-pill">[PARTNER 2]</div>
    <div class="partner-logo-pill">[PARTNER 3]</div>
  </div>
</div>

<!-- WHY IT MATTERS — 5 PILLAR CARDS -->
<section class="why-rivers" id="about">
  <div class="container center" style="max-width:700px;">
    <div class="section-label">Why It Matters</div>
    <h2 class="section-title">
      <span data-lang="en" class="lang-active">[SECTION TITLE EN] 💙</span>
      <span data-lang="bm">[SECTION TITLE BM] 💙</span>
      <span data-lang="zh">[SECTION TITLE ZH] 💙</span>
      <span data-lang="ib">[SECTION TITLE IB] 💙</span>
    </h2>
    <p class="section-sub center">
      <span data-lang="en" class="lang-active">[SECTION SUB EN]</span>
      <span data-lang="bm">[SECTION SUB BM]</span>
      <span data-lang="zh">[SECTION SUB ZH]</span>
      <span data-lang="ib">[SECTION SUB IB]</span>
    </p>
  </div>
  <div class="container">
    <div class="pillars-grid">
      <!-- Repeat this block for each pillar (3–5 total) -->
      <div class="pillar-card fade-up">
        <div class="pillar-icon" style="background:#eaf8ff;">[EMOJI]</div>
        <h3>
          <span data-lang="en" class="lang-active">[PILLAR TITLE EN]</span>
          <span data-lang="bm">[PILLAR TITLE BM]</span>
          <span data-lang="zh">[PILLAR TITLE ZH]</span>
          <span data-lang="ib">[PILLAR TITLE IB]</span>
        </h3>
        <p>
          <span data-lang="en" class="lang-active">[PILLAR DESC EN]</span>
          <span data-lang="bm">[PILLAR DESC BM]</span>
          <span data-lang="zh">[PILLAR DESC ZH]</span>
          <span data-lang="ib">[PILLAR DESC IB]</span>
        </p>
      </div>
    </div>
  </div>
</section>

<!-- JOURNEY / TIMELINE — 4 PHASES -->
<section class="journey" id="journey">
  <div class="container center" style="max-width:700px;">
    <div class="section-label">
      <span data-lang="en" class="lang-active">Programme Journey</span>
      <span data-lang="bm">Perjalanan Program</span>
      <span data-lang="zh">计划历程</span>
      <span data-lang="ib">Pejalai Program</span>
    </div>
    <h2 class="section-title">
      <span data-lang="en" class="lang-active">The Roadmap 🗺️</span>
      <span data-lang="bm">Pelan Hala Tuju 🗺️</span>
      <span data-lang="zh">路线图 🗺️</span>
      <span data-lang="ib">Jalai 🗺️</span>
    </h2>
  </div>
  <div class="container">
    <div class="timeline">
      <!-- Repeat this block for each phase -->
      <div class="timeline-item">
        <div class="tl-content fade-up">
          <div class="tl-phase">
            <span data-lang="en" class="lang-active">Phase 1 · [NAME]</span>
            <span data-lang="bm">Fasa 1 · [NAME BM]</span>
            <span data-lang="zh">第一阶段 · [NAME ZH]</span>
            <span data-lang="ib">Tahap 1 · [NAME IB]</span>
          </div>
          <h3>
            <span data-lang="en" class="lang-active">[EMOJI] [PHASE TITLE EN]</span>
            <span data-lang="bm">[EMOJI] [PHASE TITLE BM]</span>
            <span data-lang="zh">[EMOJI] [PHASE TITLE ZH]</span>
            <span data-lang="ib">[EMOJI] [PHASE TITLE IB]</span>
          </h3>
          <p>
            <span data-lang="en" class="lang-active">[PHASE DESC EN]</span>
            <span data-lang="bm">[PHASE DESC BM]</span>
            <span data-lang="zh">[PHASE DESC ZH]</span>
            <span data-lang="ib">[PHASE DESC IB]</span>
          </p>
        </div>
        <div class="tl-dot">[EMOJI]</div>
      </div>
    </div>
  </div>
</section>

<!-- TOOLKIT — 6 CARDS -->
<section class="toolkit" id="toolkit">
  <div class="container center" style="max-width:700px;">
    <div class="section-label">
      <span data-lang="en" class="lang-active">[TOOLKIT LABEL EN]</span>
      <span data-lang="bm">[TOOLKIT LABEL BM]</span>
      <span data-lang="zh">[TOOLKIT LABEL ZH]</span>
      <span data-lang="ib">[TOOLKIT LABEL IB]</span>
    </div>
    <h2 class="section-title">
      <span data-lang="en" class="lang-active">[TITLE EN] 🧰</span>
      <span data-lang="bm">[TITLE BM] 🧰</span>
      <span data-lang="zh">[TITLE ZH] 🧰</span>
      <span data-lang="ib">[TITLE IB] 🧰</span>
    </h2>
  </div>
  <div class="container">
    <div class="toolkit-grid">
      <!-- Repeat for each toolkit card; use tk-blue/green/amber/teal/coral/purple classes -->
      <div class="toolkit-card tk-blue fade-up">
        <span class="tk-icon">[EMOJI]</span>
        <h3>
          <span data-lang="en" class="lang-active">[CARD TITLE EN]</span>
          <span data-lang="bm">[CARD TITLE BM]</span>
          <span data-lang="zh">[CARD TITLE ZH]</span>
          <span data-lang="ib">[CARD TITLE IB]</span>
        </h3>
        <p>
          <span data-lang="en" class="lang-active">[CARD DESC EN]</span>
          <span data-lang="bm">[CARD DESC BM]</span>
          <span data-lang="zh">[CARD DESC ZH]</span>
          <span data-lang="ib">[CARD DESC IB]</span>
        </p>
        <div class="tk-tags">
          <span class="tk-tag">[TAG 1]</span>
          <span class="tk-tag">[TAG 2]</span>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ACTIVITIES — 4 CARDS -->
<section class="activities" id="activities">
  <div class="container center" style="max-width:700px;">
    <div class="section-label">
      <span data-lang="en" class="lang-active">[LABEL EN]</span>
      <span data-lang="bm">[LABEL BM]</span>
      <span data-lang="zh">[LABEL ZH]</span>
      <span data-lang="ib">[LABEL IB]</span>
    </div>
    <h2 class="section-title">
      <span data-lang="en" class="lang-active">[TITLE EN] 🧱</span>
      <span data-lang="bm">[TITLE BM] 🧱</span>
      <span data-lang="zh">[TITLE ZH] 🧱</span>
      <span data-lang="ib">[TITLE IB] 🧱</span>
    </h2>
  </div>
  <div class="container">
    <div class="activities-grid">
      <!-- Repeat; use ai-blue/green/amber/teal for image backgrounds -->
      <div class="activity-card fade-up">
        <div class="activity-img ai-blue">[EMOJI]</div>
        <div class="activity-body">
          <div class="activity-type">
            <span data-lang="en" class="lang-active">[TYPE EN]</span>
            <span data-lang="bm">[TYPE BM]</span>
            <span data-lang="zh">[TYPE ZH]</span>
            <span data-lang="ib">[TYPE IB]</span>
          </div>
          <h3>
            <span data-lang="en" class="lang-active">[TITLE EN]</span>
            <span data-lang="bm">[TITLE BM]</span>
            <span data-lang="zh">[TITLE ZH]</span>
            <span data-lang="ib">[TITLE IB]</span>
          </h3>
          <p>
            <span data-lang="en" class="lang-active">[DESC EN]</span>
            <span data-lang="bm">[DESC BM]</span>
            <span data-lang="zh">[DESC ZH]</span>
            <span data-lang="ib">[DESC IB]</span>
          </p>
          <div class="activity-footer">
            <span class="activity-age">[AGE/DURATION]</span>
            <a href="#" class="activity-link">Register →</a>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- STATS STRIP — 4 COUNTERS -->
<section class="stats-strip" id="impact">
  <div class="container center" style="max-width:700px;">
    <div class="section-label">
      <span data-lang="en" class="lang-active">Our Impact So Far</span>
      <span data-lang="bm">Impak Kami Setakat Ini</span>
      <span data-lang="zh">迄今为止的成果</span>
      <span data-lang="ib">Pengeruan Kami Datai Diatu</span>
    </div>
    <h2 class="section-title">
      <span data-lang="en" class="lang-active">[TITLE EN] 📈</span>
      <span data-lang="bm">[TITLE BM] 📈</span>
      <span data-lang="zh">[TITLE ZH] 📈</span>
      <span data-lang="ib">[TITLE IB] 📈</span>
    </h2>
  </div>
  <div class="container">
    <div class="stats-grid">
      <!-- Repeat; data-target = the number to count up to -->
      <div class="stat-card fade-up"><div class="stat-icon">[EMOJI]</div><div class="stat-num count-num" data-target="[NUMBER]">0</div><div class="stat-label">
        <span data-lang="en" class="lang-active">[LABEL EN]</span>
        <span data-lang="bm">[LABEL BM]</span>
        <span data-lang="zh">[LABEL ZH]</span>
        <span data-lang="ib">[LABEL IB]</span>
      </div></div>
    </div>
  </div>
</section>

<!-- ESG DASHBOARD -->
<section class="esg" id="esg">
  <div class="container center" style="max-width:700px;">
    <div class="section-label">
      <span data-lang="en" class="lang-active">ESG Impact</span>
      <span data-lang="bm">Impak ESG</span>
      <span data-lang="zh">ESG 影响力</span>
      <span data-lang="ib">Pengeruan ESG</span>
    </div>
    <h2 class="section-title">
      <span data-lang="en" class="lang-active">[TITLE EN] 📊</span>
      <span data-lang="bm">[TITLE BM] 📊</span>
      <span data-lang="zh">[TITLE ZH] 📊</span>
      <span data-lang="ib">[TITLE IB] 📊</span>
    </h2>
  </div>
  <div class="container">
    <div class="esg-dashboard fade-up">
      <div class="esg-header">
        <div class="esg-title-block">
          <h3>📊 ESG Impact Dashboard</h3>
          <p>
            <span data-lang="en" class="lang-active">Programme metrics · Updated in real-time</span>
            <span data-lang="bm">Metrik program · Dikemas kini masa nyata</span>
            <span data-lang="zh">计划指标 · 实时更新</span>
            <span data-lang="ib">Metrik program · Dibaharu masa tulin</span>
          </p>
        </div>
        <div class="live-badge"><div class="live-dot"></div>
          <span data-lang="en" class="lang-active">LIVE DATA</span>
          <span data-lang="bm">DATA LANGSUNG</span>
          <span data-lang="zh">实时数据</span>
          <span data-lang="ib">DATA TULIN</span>
        </div>
      </div>
      <div class="metrics-grid">
        <!-- Repeat metric-box for each KPI -->
        <div class="metric-box"><div class="icon">[EMOJI]</div><div class="number text-river">[VALUE]</div><div class="label">
          <span data-lang="en" class="lang-active">[LABEL EN]</span>
          <span data-lang="bm">[LABEL BM]</span>
          <span data-lang="zh">[LABEL ZH]</span>
          <span data-lang="ib">[LABEL IB]</span>
        </div></div>
      </div>
      <div>
        <p style="font-size:0.78rem; font-weight:800; letter-spacing:1px; color:var(--muted); text-transform:uppercase; margin-bottom:0.8rem;">
          <span data-lang="en" class="lang-active">UN Sustainable Development Goals Alignment</span>
          <span data-lang="bm">Penjajaran Matlamat Pembangunan Mampan PBB</span>
          <span data-lang="zh">联合国可持续发展目标对齐</span>
          <span data-lang="ib">Sejajar enggau Tujuan Pemansang Bertahan PBB</span>
        </p>
        <div class="sdg-row">
          <span class="sdg-badge" style="background:#dbf3fc;color:#0c7ea8;">SDG 6 · Clean Water</span>
          <span class="sdg-badge" style="background:#e3f3da;color:#3d7a2c;">SDG 13 · Climate Action</span>
          <!-- Add/remove SDG badges as relevant -->
        </div>
      </div>
    </div>
  </div>
</section>

<!-- GET INVOLVED — 5 ROLES -->
<section class="get-involved" id="involve">
  <div class="container center" style="max-width:700px;">
    <div class="section-label">Join the Movement</div>
    <h2 class="section-title">
      <span data-lang="en" class="lang-active">[TITLE EN] 🦸</span>
      <span data-lang="bm">[TITLE BM] 🦸</span>
      <span data-lang="zh">[TITLE ZH] 🦸</span>
      <span data-lang="ib">[TITLE IB] 🦸</span>
    </h2>
    <p class="section-sub center">
      <span data-lang="en" class="lang-active">[SUB EN]</span>
      <span data-lang="bm">[SUB BM]</span>
      <span data-lang="zh">[SUB ZH]</span>
      <span data-lang="ib">[SUB IB]</span>
    </p>
  </div>
  <div class="container">
    <div class="involve-grid">
      <!-- Repeat for each role card -->
      <a href="#" class="involve-card fade-up">
        <div class="involve-icon">[EMOJI]</div>
        <h3>
          <span data-lang="en" class="lang-active">[ROLE EN]</span>
          <span data-lang="bm">[ROLE BM]</span>
          <span data-lang="zh">[ROLE ZH]</span>
          <span data-lang="ib">[ROLE IB]</span>
        </h3>
        <p>
          <span data-lang="en" class="lang-active">[DESC EN]</span>
          <span data-lang="bm">[DESC BM]</span>
          <span data-lang="zh">[DESC ZH]</span>
          <span data-lang="ib">[DESC IB]</span>
        </p>
      </a>
    </div>
  </div>
</section>

<!-- CTA BANNER -->
<div class="cta-banner">
  <div class="container">
    <h2>
      <span data-lang="en" class="lang-active">[HEADLINE EN] <span class="text-river">[SUBLINE EN]</span> 💚</span>
      <span data-lang="bm">[HEADLINE BM] <span class="text-river">[SUBLINE BM]</span> 💚</span>
      <span data-lang="zh">[HEADLINE ZH]<span class="text-river">[SUBLINE ZH]</span> 💚</span>
      <span data-lang="ib">[HEADLINE IB] <span class="text-river">[SUBLINE IB]</span> 💚</span>
    </h2>
    <p>
      <span data-lang="en" class="lang-active">[CTA PARA EN]</span>
      <span data-lang="bm">[CTA PARA BM]</span>
      <span data-lang="zh">[CTA PARA ZH]</span>
      <span data-lang="ib">[CTA PARA IB]</span>
    </p>
    <div class="btns">
      <a href="#" class="btn-primary">
        <span data-lang="en" class="lang-active">⬇️ [BTN 1 EN]</span>
        <span data-lang="bm">⬇️ [BTN 1 BM]</span>
        <span data-lang="zh">⬇️ [BTN 1 ZH]</span>
        <span data-lang="ib">⬇️ [BTN 1 IB]</span>
      </a>
      <a href="#" class="btn-secondary">
        <span data-lang="en" class="lang-active">📩 [BTN 2 EN]</span>
        <span data-lang="bm">📩 [BTN 2 BM]</span>
        <span data-lang="zh">📩 [BTN 2 ZH]</span>
        <span data-lang="ib">📩 [BTN 2 IB]</span>
      </a>
    </div>
  </div>
</div>

<!-- FOOTER -->
<footer>
  <div class="footer-grid">
    <div class="footer-brand">
      <a href="#" style="text-decoration:none;display:inline-flex;align-items:center;gap:10px;">
        <div class="drop"></div>
        <span style="font-family:'Baloo 2',sans-serif; font-size:1.2rem;font-weight:800;color:#fff;">[PROJECT <em style="color:#4ade80;font-style:normal;">NAME</em>]</span>
      </a>
      <p>
        <span data-lang="en" class="lang-active">[BRAND DESC EN]</span>
        <span data-lang="bm">[BRAND DESC BM]</span>
        <span data-lang="zh">[BRAND DESC ZH]</span>
        <span data-lang="ib">[BRAND DESC IB]</span>
      </p>
      <p class="footer-tagline">✨ [MALAY SLOGAN]</p>
    </div>

    <div class="footer-col">
      <h4>
        <span data-lang="en" class="lang-active">Programme</span>
        <span data-lang="bm">Program</span>
        <span data-lang="zh">计划</span>
        <span data-lang="ib">Program</span>
      </h4>
      <ul>
        <li><a href="#about"><span data-lang="en" class="lang-active">About</span><span data-lang="bm">Tentang</span><span data-lang="zh">关于</span><span data-lang="ib">Pasal</span></a></li>
        <li><a href="#journey"><span data-lang="en" class="lang-active">Journey</span><span data-lang="bm">Perjalanan</span><span data-lang="zh">历程</span><span data-lang="ib">Pejalai</span></a></li>
        <li><a href="#toolkit"><span data-lang="en" class="lang-active">Toolkit</span><span data-lang="bm">Toolkit</span><span data-lang="zh">工具包</span><span data-lang="ib">Toolkit</span></a></li>
        <li><a href="#activities"><span data-lang="en" class="lang-active">Activities</span><span data-lang="bm">Aktiviti</span><span data-lang="zh">活动</span><span data-lang="ib">Aktiviti</span></a></li>
        <li><a href="#science"><span data-lang="en" class="lang-active">Science</span><span data-lang="bm">Sains</span><span data-lang="zh">科学</span><span data-lang="ib">Sains</span></a></li>
      </ul>
    </div>

    <div class="footer-col">
      <h4>
        <span data-lang="en" class="lang-active">Resources</span>
        <span data-lang="bm">Sumber</span>
        <span data-lang="zh">资源</span>
        <span data-lang="ib">Sumber</span>
      </h4>
      <ul>
        <li><a href="#"><span data-lang="en" class="lang-active">Download Centre</span><span data-lang="bm">Pusat Muat Turun</span><span data-lang="zh">下载中心</span><span data-lang="ib">Pusat Download</span></a></li>
        <li><a href="#"><span data-lang="en" class="lang-active">Worksheets</span><span data-lang="bm">Lembaran Kerja</span><span data-lang="zh">学习单</span><span data-lang="ib">Kertas Pengawa</span></a></li>
        <li><a href="#"><span data-lang="en" class="lang-active">Gallery</span><span data-lang="bm">Galeri</span><span data-lang="zh">图库</span><span data-lang="ib">Galeri</span></a></li>
      </ul>
    </div>

    <div class="footer-col">
      <h4>
        <span data-lang="en" class="lang-active">Get Involved</span>
        <span data-lang="bm">Sertai Kami</span>
        <span data-lang="zh">参与其中</span>
        <span data-lang="ib">Nyampul Kami</span>
      </h4>
      <ul>
        <li><a href="#"><span data-lang="en" class="lang-active">Volunteer</span><span data-lang="bm">Sukarelawan</span><span data-lang="zh">志愿者</span><span data-lang="ib">Sukarelawan</span></a></li>
        <li><a href="#"><span data-lang="en" class="lang-active">Partner</span><span data-lang="bm">Rakan</span><span data-lang="zh">合作伙伴</span><span data-lang="ib">Rakan</span></a></li>
        <li><a href="#"><span data-lang="en" class="lang-active">Contact Us</span><span data-lang="bm">Hubungi Kami</span><span data-lang="zh">联系我们</span><span data-lang="ib">Hubung Kami</span></a></li>
      </ul>
    </div>
  </div>

  <div class="footer-bottom">
    <p>
      <span data-lang="en" class="lang-active">© [YEAR] [PROJECT NAME] · [POWERED BY] · [LOCATION]</span>
      <span data-lang="bm">© [YEAR] [PROJECT NAME] · Dikuasakan oleh [PARTNER] · [LOCATION]</span>
      <span data-lang="zh">© [YEAR] [PROJECT NAME] · 由 [PARTNER] 支持 · [LOCATION]</span>
      <span data-lang="ib">© [YEAR] [PROJECT NAME] · Dikuasaka olih [PARTNER] · [LOCATION]</span>
    </p>
    <div class="footer-partners">
      <span class="partner-pill">[PARTNER 1]</span>
      <span class="partner-pill">[PARTNER 2]</span>
    </div>
  </div>
</footer>

<!-- JAVASCRIPT -->
<script>
let currentLang = 'en';

function setLang(lang) {
  currentLang = lang;
  document.querySelectorAll('.lang-btn').forEach(b => b.classList.remove('active'));
  document.querySelector(`.lang-btn[onclick="setLang('${lang}')"]`).classList.add('active');
  document.querySelectorAll('[data-lang]').forEach(el => {
    el.classList.toggle('lang-active', el.getAttribute('data-lang') === lang);
  });
}

const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) entry.target.classList.add('visible');
  });
}, { threshold: 0.05, rootMargin: '0px 0px -50px 0px' });

document.querySelectorAll('.fade-up').forEach(el => observer.observe(el));

function animateCounter(el) {
  const target = parseInt(el.getAttribute('data-target'));
  const duration = 1600;
  const step = target / (duration / 16);
  let current = 0;
  const timer = setInterval(() => {
    current += step;
    if (current >= target) { current = target; clearInterval(timer); }
    el.textContent = Math.floor(current).toLocaleString() + (target > 100 ? '+' : '');
  }, 16);
}

const counterObserver = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting && !entry.target.classList.contains('counted')) {
      entry.target.classList.add('counted');
      animateCounter(entry.target);
    }
  });
}, { threshold: 0.3 });

document.querySelectorAll('.count-num').forEach(el => counterObserver.observe(el));

window.addEventListener('scroll', () => {
  const nav = document.querySelector('nav');
  nav.style.background = window.scrollY > 50 ? 'rgba(255,255,255,0.98)' : 'rgba(255,255,255,0.9)';
});

document.querySelectorAll('.pillar-card, .toolkit-card, .activity-card, .involve-card, .stat-card, .tl-content').forEach((el, i) => {
  el.style.transitionDelay = `${(i % 4) * 0.06}s`;
});
</script>
</body>
</html>
```

---

## PART 4 — THE LANGUAGE TOGGLE PATTERN (KEY RULE)

The 4-language pattern is simple but must be followed precisely:

```html
<!-- For inline text (spans inside h1, h2, h3, li, a, etc.) -->
<span data-lang="en" class="lang-active">English text</span>
<span data-lang="bm">Bahasa Malaysia text</span>
<span data-lang="zh">中文文本</span>
<span data-lang="ib">Teks Iban</span>

<!-- For block-level elements (taglines, paragraphs) use <p> directly -->
<p class="hero-tagline lang-active" data-lang="en">English paragraph.</p>
<p class="hero-tagline" data-lang="bm">BM paragraph.</p>
<p class="hero-tagline" data-lang="zh">中文段落。</p>
<p class="hero-tagline" data-lang="ib">Iban paragraph.</p>
```

**Rules:**
- Default language = `en` — must have `class="lang-active"` on all `en` elements
- Every translatable element needs EXACTLY 4 sibling spans (en/bm/zh/ib)
- Block-level elements (p, div) need: `div[data-lang].lang-active { display: block; }` — already in CSS
- The JS `setLang()` function handles everything — don't manually add/remove display styles

**Verification (run this after completion to check balance):**
```python
import re
s = open('index.html').read()
for l in ['en','bm','zh','ib']:
    print(f'{l}: {len(re.findall(f"data-lang=\"{l}\"", s))}')
# All 4 should show the same count
```

---

## PART 5 — DEPLOYMENT CHECKLIST

**Before deploy:**
- [ ] Screenshot every section in all 4 languages (local server + Playwright)
- [ ] Run Python regex check — all 4 language counts must match
- [ ] Get explicit "proceed" from client

**Deploy to Netlify:**
```bash
# Start local server for testing
python3 -m http.server 8910 --directory ./

# Screenshot check (Playwright)
node -e "
const { chromium } = require('playwright');
(async () => {
  const b = await chromium.launch({ executablePath: '/opt/pw-browsers/chromium' });
  const p = await b.newPage();
  await p.setViewportSize({ width: 1280, height: 900 });
  await p.goto('http://localhost:8910');
  // switch language
  await p.click('button[onclick=\"setLang(\'zh\')\"]');
  await p.screenshot({ path: '/tmp/check_zh.png', fullPage: false });
  await b.close();
})();
"
```

**After deploy:**
- [ ] Verify live URL returns 200: `curl -s -o /dev/null -w "%{http_code}\n" https://[SITE].netlify.app`
- [ ] Commit & push final state to git branch
- [ ] Gitignore `.netlify/` to avoid untracked file issues

---

## PART 6 — THE 3-MESSAGE CLIENT ARC

> Brief → Visual Revision → Approve+Ship

**Message 1 (client gives you):**
> "[Audience + positioning]. Site structure: [list]. Must-have: [constraints]. Style reference: [images]. Build mockup first — show me layout before I greenlight."

**Message 2 (after client sees mockup):**
> "[Rule-like revision notes]. Refer to [images] for direction."

**Message 3 (client approves):**
> "Proceed. Share the link once done."

This 3-message arc is the shape that makes builds fast. Protect it.
