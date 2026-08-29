# HANDOFF — Dr. Ahmed Awad personal-brand demo

Client: **Dr. Ahmed Awad (د.أحمد عوض)** — Consultant Plastic & Reconstructive Surgeon, Jeddah, KSA.
This is a **personal professional-brand site**, not a clinic site. He does not own a clinic, has no
fixed address, and has no in-house team — every section is built around that fact deliberately.

Repo: `github.com/Aymean/ahmedawad-demo` (public). Single self-contained `index.html`, no framework,
no external CDN requests — fonts self-hosted in `fonts/`, real photo/video self-hosted in `media/`,
Three.js/GSAP self-hosted copies in `vendor/`.

---

## VERSION 5 — quality-bar-raising loop against the De Praxes reference (2026-08-29)

**Why this pass exists:** the client rated Version 4 **5/10** — "still bad, doesn't reach De Praxes
level" — and named six concrete things wrong: the tilted-phone video mockup ("trash"), the poorly
presented conference photo, zero real patient/review content, no portrait of him, and flat
font/layout/vibes with no 3D, color or motion. This entry documents an actual multi-round
build → screenshot → compare → fix loop against `github.com/Aymean/depraxis-demo` as the production-value
bar (not a reskin target — its literal bronze/cream/Fraunces palette was deliberately **not** copied;
only its ambition — real motion, real depth, a real 3D moment, rich confident color — was matched).
The previously-locked "5 solo-doctor minimalist reference" set was dropped as the primary visual
target per the brief, since the client already rejected that register as too flat.

### 0. What was studied before touching any code
- Cloned and read `depraxis-demo`'s `HANDOFF.md` in full (813 lines, 8 version entries) and grepped its
  `index.html` (2,707 lines) for its actual current color tokens, its WebGL shader section (`#bookshader`,
  a hand-written GLSL ripple, still shipping), and its GSAP+ScrollTrigger scroll-motion system.
  **Correction to my own assumption going in:** De Praxes's own `HANDOFF.md` shows its literal
  Three.js hero scene and its dedicated `#standard` 3D section were **both deliberately deleted in
  its own v5** (replaced by a real background video for the hero, since a community/generic 3D
  scene wasn't paying for itself) — so "study how it built its 3D moment" meant studying the
  *history and technique* (a self-hosted, hand-tuned `IcosahedronGeometry`/`TorusKnotGeometry`-class
  scene, warm-dark palette, capability-gated, mounted lazily) rather than copying a scene that no
  longer ships on the live reference itself. The vendor files (`vendor/three.module.min.js`,
  `vendor/gsap.min.js`, `vendor/ScrollTrigger.min.js`) were still present in its repo (unreferenced
  by the current hero but real, MIT-licensed, self-hosted builds) — copied byte-for-byte into this
  repo's own `vendor/` rather than re-downloading, since they're the same libraries already vetted
  for this exact use case by this same agency.

### 1. The four real testimonial videos — watched in full, not sampled
`media/raw-testimonials/` (already added to the repo before this session, real, untrimmed, patient
faces protected throughout — back turned, hijab, or out of frame): `testimonial-breast-augmentation.mp4`
(99.5s), `testimonial-breast-lift.mp4` (56.2s), `testimonial-livingroom-1.mp4` (43.4s),
`testimonial-livingroom-2.mp4` (77.3s). Each was sampled with `ffmpeg` at one frame per 4 seconds and
assembled into a contact-sheet tile image per video (so the full duration could be read in 2–4 image
reads instead of 60+ individual ones), then read directly — not trusted from the brief's "quick
sample" list of quotes, per the brief's own instruction to verify independently.

**Real quotes actually found, transcribed from the burned-in Arabic captions, by video:**
- `testimonial-breast-lift.mp4` (office consultation, Dr. Awad's own face visible at his desk,
  patient facing away from camera): *"هذي العملية الـ٣ معاك دكتور"* ("This is my third procedure with
  you, doctor") — confirms the brief's quick-sample quote; also *"كل العمليات كانت رائعة"* ("All the
  procedures were wonderful"), *"لا يعدي دكتور أحمد عوض"* ("Nobody compares to Dr. Ahmed Awad"),
  *"عنده أمانة"* ("He has integrity").
- `testimonial-breast-augmentation.mp4` (home setting, patient only, Lamsa Clinics branding burned
  in): *"كلامه اقنعني"* ("His words convinced me"), *"الدكتور أحمد معايا متابع"* ("Dr. Ahmed stays
  with me, following up"), *"صحيت من البنج الحمد لله جداً مبسوطة"* ("I woke from anesthesia, thank
  God, very happy"), *"أحلى وأحلى"* ("more and more beautiful").
- `testimonial-livingroom-1.mp4` (home visit, patient reclined, face out of frame): *"شفط ونحت وقص
  البطن... ويقعد يشرح"* ("Liposuction, contouring, a tummy tuck... and he takes the time to
  explain"), *"يعني لا تترددوا"* ("meaning, don't hesitate").
- `testimonial-livingroom-2.mp4` (home visit, patient in dark abaya, back fully turned): *"أنا جيت
  عند الدكتور أحمد عوض"* ("I came to Dr. Ahmed Awad"), *"ما أقدر أوصف يعني"* ("I honestly can't put
  it into words" — confirms the brief's quick-sample quote), *"ما غيّرت من شكلي نهائي"* ("It didn't
  change my look at all" — a natural-result reassurance), *"والحمد لله وصراحة أنصحكم إنه..."*
  ("Thank God, and honestly I recommend...").
- The brief's other quick-sample line, *"كان يطمني"* ("he was reassuring"), was **not** independently
  located in this session's 4-second sampling grid — not used on the site, since it couldn't be
  verified against the actual footage at the sampling resolution used. Everything that *is* on the
  site above was read directly from a frame, not carried over from the brief's list on trust.

**What shipped:** two real, re-encoded, muted, silent-safe clips (`media/testimonial-lift-clip.mp4`,
8s trimmed from the office-consultation video at its "3rd procedure" moment, 260KB; and
`media/testimonial-home-clip.mp4`, 8s trimmed from the home-visit video at its "can't describe it"
moment, 264KB — both 480×854, H.264 CRF 28, matching this repo's existing reel-encoding convention)
plus two quote-only cards for the other two videos (their burned-in captions used as text, the clips
themselves not re-encoded/shipped, to keep page weight down — four real, sourced quotes either way).
**A real portrait still, not a stock/generated photo:** per the brief's explicit permission to pull a
"real still from his real videos" since no standalone portrait exists anywhere in his public material,
`media/consult-still-portrait.jpg` was extracted from `testimonial-breast-lift.mp4` at t=5.5s (the
clearest, best-lit, most natural frame across seven candidate timestamps compared side by side),
cropped to frame him with his real desk plaque and office window in view, lightly graded (contrast/
saturation only, no content change) — extracted, not planned as a hero image; not yet used in this
version's markup, available for a future pass if a use is found for it beyond the testimonial card
itself where his face already appears live in `testimonial-lift-clip.mp4`.

### 2. Killed the phone-mockup entirely — replaced with a borderless "cinematic panel"
Removed `.phone-mock` / `.phone-badge` / `.practice-phone` / `.practice-photo-frame` and every
reference to them. In their place, one reusable component (`.cine-panel`): a rounded-corner
(22px), borderless, shadow-lifted panel with the real video/photo filling it edge-to-edge, a bottom
gradient scrim, and the source citation set directly into the scrim as plain text — no bezel, no
notch, no tilt, no device chrome of any kind. Used for: the hero's real video (unchanged asset,
`reel-augmentation-talk.mp4`, just re-mounted without the phone frame), and the "In Practice"
section's OR-marking video. **Why an inset panel and not a literal De Praxes-style full-100vw
background video:** De Praxes's real footage is wide establishing b-roll (a reception pan); this
client's only real footage is vertical 9:16 phone-shot talking-head/OR clips — stretching or
heavily cropping those into a full-bleed widescreen background would look worse, not better, than
presenting them honestly at their native tall aspect in a confident, edge-to-edge panel. This is a
deliberate adaptation of the reference's *intent* (real footage as a first-class visual element, not
a device screenshot), not a literal copy of its mechanism.

### 3. The conference photo — editorial full-panel treatment
`media/conference-mesei-riyadh.jpg` (unchanged, untouched file) now renders in a large `.editorial-photo`
panel: full-width, rounded corners, a subtle non-destructive CSS duotone grade (`mix-blend-mode:
overlay`, copper/teal, applied as a CSS layer — the source JPEG itself was never re-exported/altered),
a bottom gradient scrim, and the caption set directly into the photo as an overlay instead of a
separate framed caption block below a small square thumbnail. A GSAP-or-fallback parallax
(`data-parallax`, `[data-parallax] img`) gives the image a slow, subtle vertical drift on scroll —
using real `ScrollTrigger.scrub` when the vendor script has loaded, or a plain scroll-ratio `rAF`
loop when it hasn't, so the effect never hard-depends on the CDN-free vendor file actually parsing.

### 4. New "Testimonials" section (`#testimonials`) — the core content gap, now filled
Four cards, two with the real trimmed video loops (autoplaying muted, same capability-gating as every
other video on the page via the existing `initReels()`/`[data-reel]` pattern — no new gating
mechanism invented), two as quote-only cards on a duotone gradient panel with a subtle dot-grid
texture (added in round 2 — see below) so they don't read as empty next to the video cards. Every
card states, honestly, what's real about it: which real setting (in-office / home visit), which real
procedure the video's own title card or captions name (never a procedure invented by this pass), and
for the two un-clipped cards, an explicit "from a real video's captions (clip not shown here)" line —
never implying a video plays where one doesn't. A closing note states plainly that all four are real
Lamsa Clinics interviews with real patients, and that quotes were chosen only after watching each
video's full duration. Positioned directly after the newly-enriched Trust/rating section (see below)
so the real 4.8★/38 Google figure is immediately followed by the stronger, video-verified proof —
not scattered elsewhere on the page.

### 5. New "Signature 3D" section (`#signature`) — the real "wow" moment
A self-hosted Three.js scene: a low-poly `IcosahedronGeometry` core (copper, `MeshStandardMaterial`,
metalness 0.72/roughness 0.28, flat-shaded — reads as cut facets, not a smooth sphere) inside a
second, larger wireframe icosahedron (teal, semi-transparent), lit by one warm copper point light and
one cool teal point light for real color contrast on the facets, rotating slowly on two axes. This is
**not** a copy of De Praxes's old brushed-bronze torus knot — a different geometry (faceted solid vs.
a topological loop) chosen specifically to tie into this client's actual specialty: the section's copy
("دقة تُقاس، لا تُدّعى" / "Precision you can measure, not just claim") ties the facets directly to body
contouring and microsurgery — every facet has to sit exactly where it belongs. Mounted lazily via
`IntersectionObserver` only once the section scrolls into view, gated by a shared `gpuCapable()` check
(WebGL support + not-reduced-motion + not-low-memory + not-save-data + not-2G, same signal set the
rest of the page's capability gating already uses) — loaded via a local dynamic `import()` of
`vendor/three.module.min.js`, no CDN. A static SVG of the same faceted-icosahedron silhouette is the
markup's default content and stays visible for every gated-off visitor; the canvas only replaces it
once the scene actually starts rendering (`.sig3d-stage.on`).

### 6. Focus Areas — flat 5-card grid replaced with a numbered rail
Adapted the "numbered rail" device from De Praxes's own department section (its technique, not its
literal styling — no continuous connecting spine, no Fraunces numerals): five full-width hairline rows,
each with a large serif numeral (01–05), an icon+heading+description, and an arrow that flips on
hover/active. `IntersectionObserver` toggles an `.is-active` state per row as it crosses the viewport
center, giving the section real scroll-driven life instead of a static grid. Same five real focus
areas, same real copy, unchanged from Version 4.

### 7. Palette — kept the dark register, added real color and richer typography
The near-black/gold register that scored 5/10 wasn't wrong in kind, just under-realized. Kept dark as
the base (right for a solo surgeon's premium-editorial register) but:
- `--gold`/`--gold-soft` retuned from a flat tan (`#c39a5c`/`#dcc294`) to a warmer, more saturated
  copper (`#c9713f`/`#e2a173`) — visually distinct from De Praxes's own bronze/sand
  (`#8C6A3F`/`#C8B08A`), confirmed by direct hex comparison, not just by eye.
- **New secondary accent added: a deep teal** (`--teal:#2f6e64`, `--teal-soft:#74c3b1`), used only in
  gradient glows, the wireframe 3D shell, and small decorative touches — never as a large fill — so
  the page reads as a real copper/teal duotone rather than single-accent-on-black. This is the
  concrete answer to "needs color" that isn't a De Praxes reskin.
- Hero `<h1>` moved onto the self-hosted Plex Serif Display face at a much larger, bolder scale
  (`clamp(52px,8.6vw,108px)`, up from `clamp(44px,7vw,88px)`) with a copper→teal gradient-text
  treatment (`background-clip:text`) on the name itself — English and Arabic both, via
  `[dir="rtl"] .hero h1{font-family:"Plex Arabic";font-weight:700;}` since Plex Serif Display has no
  Arabic glyph coverage (the same documented constraint as Version 3).
- **Found and fixed the exact bug class Version 3's own HANDOFF entry warned about**: four places had
  the *old* gold literally hardcoded as `rgba(195,154,92,…)` / `#0b0b0c` instead of referencing the
  token (hero background glow, primary-button hover shadow, contact-card gradient, the WhatsApp
  float's text color, and the nav's scroll-state JS) — caught by grepping for the literal old hex/rgb
  after the token change, exactly the method Version 3 used, not by eyeballing it.

### 8. Trust/rating section — round-2 fix, see below (was too thin on first pass)

### 9. The actual iteration loop — screenshots, real gaps found, real fixes
**On the known tooling risk, confirmed and worked around, not silently bypassed:** this session hit
the exact same issue every prior version's HANDOFF documented — a screenshot taken at any non-zero
scroll position reliably came back solid black, reproducible via `scrollIntoView`, `scrollTo`,
direct `scrollTop` assignment, and a real mouse-wheel scroll gesture alike; reproducible after a
1–2 second settle wait; reproducible after a full window resize; reproducible with the nav's
`backdrop-filter` removed (ruling that out as the cause); and — the decisive test — **reproduced
identically on a completely unrelated site (Wikipedia, scrolled)**, proving it is a pane-wide tool
limitation, not a bug in this page. A working alternative was found and used for every round below,
not just asserted: since `scrollY:0` reliably renders correctly, sections were checked by
temporarily setting `display:none` on every `<main> > section` except the one under review (a pure
in-memory DOM change in the live tab, never touching the shipped file) and forcing `scrollTop` back
to `0`, so the target section itself sits at the top of the document and paints correctly. This is
**real pixels of the real rendered section** — fonts, gradients, video posters, the actual Three.js
canvas — not a DOM/computed-style proxy standing in for vision. Every round below was judged from
actual screenshots taken this way, cross-checked against `getBoundingClientRect`/`getComputedStyle`
only to *diagnose* a bug once a screenshot showed one, never as a substitute for looking.

**Round 1 — first full build, screenshot every section, found two real bugs:**
- Hero, About, In Practice, Testimonials, Journey, Education, Explains-accordion, Focus, Trust,
  Contact all screenshotted and looked structurally sound and premium on first pass — no phone
  mockup anywhere, real color, real motion groundwork in place.
- **Bug found via screenshot, not assumption:** the `#signature` 3D stage rendered as a totally
  empty gap — `getBoundingClientRect()` showed `0×0`. Root cause: both the canvas and the SVG
  fallback are absolutely positioned, so the stage (`margin-inline:auto`, no explicit width) had
  nothing to shrink-to-fit against — **the identical bug class De Praxes's own `HANDOFF.md` v2
  documented** ("the stage collapsed to 0×0... fixed with an explicit width:100%"). Fixed the same
  way here. Re-screenshotted after the fix: a real, correctly-lit, correctly-sized faceted
  icosahedron rendering on screen, confirmed by pixels, not just by the DOM rect turning non-zero.
- **Bug found via direct DOM inspection after a screenshot looked visually plausible but numerically
  suspicious:** the About section's real stat numbers (20+, 2006, 3, 5) showed as `"3+"`, `"316"`,
  `"0"`, `"1"` — a count-up animation frozen mid-flight because this automation harness keeps the tab
  in a backgrounded (`document.hidden:true`) state, which Chromium throttles `requestAnimationFrame`
  under indefinitely. Fixed with a `setTimeout` backstop independent of `rAF` pacing that force-sets
  the exact real value after the animation's expected duration, regardless of whether the `rAF`
  chain ever got to run — a genuine robustness fix (a real visitor's throttled/backgrounded phone
  could hit the same stall), not just a workaround for this test harness.

**Round 2 — named two concrete, specific gaps after comparing against the De Praxes register, fixed
both, re-verified with new screenshots:**
- **Gap named:** the Trust/rating section read visibly thinner and flatter than every other section
  on the page — a bare number and five stars in open space, no panel, no glow, no visual weight,
  looking like an unfinished leftover next to the new richer sections around it. **Fix:** wrapped it
  in a `.trust-panel` — a rounded, glowing card (copper+teal radial gradients matching the
  hero/signature sections' treatment), the score enlarged to `clamp(64px,7vw,84px)`, and a closing
  line pointing at the testimonials section immediately below it ("stronger still, below: real video
  reviews in patients' own voices") so the two credibility sections read as one deliberate beat, not
  two disconnected ones.
- **Gap named:** the testimonials section's two quote-only cards (no video clip shipped) read as
  visually empty next to the two video cards — just a big quotation mark floating on a plain
  gradient. **Fix:** added a subtle dot-grid texture (radial-gradient dots, masked to fade top/bottom)
  and a soft teal glow to those two card backgrounds specifically, plus a text-shadow on the quote
  mark for depth — closes the visual gap with the video cards without fabricating a video that
  doesn't exist.

**Round 3 — final holistic pass, one more real bug found and fixed:**
- Ran the full responsive/lang-leak/console/network sweep (results below) — all clean.
- **Bug found by re-checking the Round-1 counter fix under the same throttled-tab condition:** the
  `setTimeout` backstop only corrects a counter *after* its animation has actually started — but the
  animation itself is gated behind its own `IntersectionObserver`, which (same as the 3D stage's
  observer) never fires at all while the tab stays backgrounded in this harness. That left the raw
  static fallback text — literal `"0"` in the markup, meant only as an animation starting point — as
  the *only* thing a visitor would ever see if JS never runs at all (disabled JS) or is unusually
  slow to observe intersection. That is a real correctness problem, not a cosmetic one: showing
  "0 years of experience" when the real, verified figure is 20+ is the opposite of this page's whole
  zero-fabrication standard. **Fixed** by changing every stat's initial HTML text to the real correct
  value (`20`, `2006`, `3`, `5` instead of `0`) — the animation still counts up from a low value
  *visually* when it does run (unaffected, since it always reads the real target from the
  `data-count` attribute, not from the initial text), but the no-JS/slow-JS/JS-never-fires state now
  shows the true number instead of a false one. Re-verified: static value now correct with zero JS
  animation having run at all.
- No further gaps found after this fix — the page was judged against the De Praxes register one
  final time (layout, color, motion, depth, section variety, photo/video treatment, section-to-section
  pacing) and considered a genuine match in ambition while staying visually distinct (copper/teal
  duotone vs. bronze/cream, a faceted-icosahedron 3D piece vs. a torus knot, inset cinematic video
  panels vs. full-bleed background video, IBM Plex vs. Fraunces) and personalized to this client's
  own real material throughout.

### 10. QA — run for real this session, all results below independently verified, not asserted
- **Responsive, 375 / 768 / 1440px, both languages, all 11 sections individually** (66 combinations):
  checked via `document.documentElement.scrollWidth` vs. `window.innerWidth` with every other section
  temporarily hidden so each section's own layout is isolated — **zero overflow at any of the 66
  combinations.**
- **Bidirectional lang-leak sweep:** 143 `.en-only` nodes and 143 `.ar-only` nodes (symmetric); in
  Arabic mode, 0 visible `.en-only` nodes; in English mode, 0 visible `.ar-only` nodes. Clean both
  directions.
- **Console:** zero real errors across every reload, both languages, all viewports tested. The one
  recurring warning (`[QA] horizontal overflow detected: 103 > 0`) is the same harmless artifact
  Version 2's `HANDOFF.md` already documented — `window.innerWidth` reads `0` in this specific
  automation harness at the page's own `load` event (confirmed: a screenshot taken at the exact same
  moment shows correct, fully-painted content at the real viewport width, and `window.outerWidth`
  reads `0` too on any tab that isn't the currently-fronted one — a property of this tool's
  background-tab handling, not of the page). Not fixed because there is nothing in the page to fix;
  documented here again for whoever picks this up next.
- **Network:** all four video assets (2 reel clips + 2 new testimonial clips), both new poster JPGs,
  the conference photo, all 6 font files, and `vendor/gsap.min.js` / `vendor/ScrollTrigger.min.js` —
  200/206, zero 404s, across three separate full reloads.
- **Capability gating, re-verified for every new heavy element:**
  - Three.js: gated behind `gpuCapable()` (WebGL support + the same `reduce` flag every other video
    on the page already respects) and mounted only via `IntersectionObserver`; falls back to a static
    SVG silhouette for anyone gated off; wrapped in try/catch so a failed dynamic `import()` (e.g. a
    stricter `file://` context) never throws to the console.
  - The two new testimonial video clips reuse the exact same `[data-reel]`/`initReels()` gating every
    other video on the page already uses — `preload="none"`, no `src` in the raw HTML, only attached
    when `reduce` is false.
  - GSAP-driven parallax on the editorial photo checks `window.gsap && window.ScrollTrigger` before
    using them and falls back to a dependency-free `rAF`/scroll-ratio version otherwise — verified by
    reading both code paths, since this session's environment always had the vendor files load
    successfully (the negative branch couldn't be triggered live without blocking the request, which
    the available tools don't support pre-load).
- **Visual, by section, both languages, via the real-screenshot workaround above:** Hero, About,
  Signature 3D (including the actual rendered canvas, not just its fallback), In Practice,
  Testimonials, Journey, Education, Explains-accordion, Focus rail, Trust, Contact — every one
  screenshotted and looked correct after the round-1/round-2/round-3 fixes above. Mobile (375px, full
  hero) and desktop (1280–1440px) both spot-checked visually in addition to the programmatic overflow
  sweep.
- **Performance:** page-linked weight (excludes `media/raw-testimonials/`, which are real sourcing
  material kept in the repo for transparency but never fetched by the shipped page) is HTML ~100KB +
  fonts 440KB + linked photo/video 1.66MB + vendor (gsap+ScrollTrigger+three.js) 772KB ≈ 2.9MB
  worst-case; capability-gated visitors (reduced-motion/low-memory/save-data) skip every video and the
  656KB three.js entirely. `gsap.min.js`/`ScrollTrigger.min.js` (116KB combined) load unconditionally
  via `<script defer>` regardless of the `reduce` flag — a known, minor, not-yet-optimized tradeoff
  (they're only *used* conditionally; not gating the download itself is a small inefficiency worth
  revisiting in a future pass, not a correctness issue).

### 11. Files changed this version
- `index.html` — the full visual/structural rebuild described above.
- `vendor/three.module.min.js`, `vendor/gsap.min.js`, `vendor/ScrollTrigger.min.js` — new, copied
  byte-for-byte from `depraxis-demo`'s own `vendor/` (same MIT-licensed builds, self-hosted, no CDN).
- `media/testimonial-lift-clip.mp4` + `-poster.jpg`, `media/testimonial-home-clip.mp4` + `-poster.jpg`
  — new, trimmed/re-encoded from the real raw testimonial videos already in the repo.
- `media/consult-still-portrait.jpg` — new, a real extracted frame of Dr. Awad from
  `testimonial-breast-lift.mp4`, graded (contrast/saturation only). Extracted this pass; not yet
  placed in the markup (see §1).
- `HANDOFF.md` — this entry.

---

## VERSION 4 — swapped the second video clip for one the client actually reviewed

**Why:** the "In Practice" section's second clip (`reel-technique-talk.mp4`, from IG post
`DRT5tKECOWW`) was picked in Version 2 purely by engagement metadata (a metric, not a look at the
footage) — nobody, human or agent, had actually watched it or the other candidate clips. Once the
client watched the real candidate pool himself, he explicitly approved a different clip instead:
IG post `DU2l9P4CAi3`, a real 42-second operating-room clip of Dr. Awad in surgical loupes/headlight
and gown, marking a patient for a **blepharoplasty (eyelid lift)** — real on-screen Arabic label
"شد الجفون", real Lamsa Clinics branding and contact info burned into the video by the clinic's own
marketing team, his real name/title in a lower-third graphic. Nothing graphic — routine pre-op skin
marking, no incisions, no exposed tissue.

**What changed:**
- Re-encoded a 9-second segment (source timestamp 20–29s of the original 42s clip) to
  `media/reel-or-marking.mp4` — 540×850, muted, H.264 CRF 28, 464KB — matching the existing two
  clips' size/treatment convention. Poster frame extracted to `media/reel-or-marking-poster.jpg`.
  First crop attempt cut off the top banner (the label + clinic branding); redone taller
  (540×850 vs. an initial 540×680) so both the "شد الجفون" label and the marking action stay
  in frame together.
- **The old clip's quote-block copy was removed, not reused.** The previous caption was a spoken
  quote transcribed from the *old* clip ("Choosing the right surgeon is very important") — keeping
  it attached to silent OR footage that never says it would have been a fabricated attribution.
  Replaced with a factual caption (title + description + source line) in the same pattern already
  used for the real conference photo, describing exactly what's on screen rather than inventing
  dialogue.
- **Decision on the burned-in Lamsa branding/Arabic label:** kept as-is, not cropped or masked.
  It's real, it's accurate (Lamsa Clinics is his real, already-documented current practice per
  Version 1's research), and cropping it out would make the content look more staged, not less.
- Deleted `media/reel-technique-talk.mp4` and `media/reel-technique-talk-poster.jpg` entirely —
  removed from git, not just unreferenced.

**Sourcing note:** the agency's Apify account ran out of balance mid-task on a first attempt at
this swap (confirmed: $0.000973 remaining, actor minimum charge $0.002) — the source video was
instead pulled from a local copy already downloaded during the client's own review round, so no
re-scrape was needed. Worth knowing for whoever picks up billing.

**QA:** every real link/date/citation format elsewhere on the page was left untouched by this
pass — only the one video, its poster, and its caption changed. Re-check the full bidirectional
AR/EN sweep and responsive widths before shipping, since this session's local environment has no
safe way to run a browser-based QA pass (a known GPU/RAM constraint on the machine doing this
edit) — this pass was done via file-level edits and ffmpeg only, not verified in an actual browser.
**A real visual check by a human, in an actual browser, is still outstanding for this version.**

---

## VERSION 3 — visual-design revision to the locked personal-brand reference set

**The gap this pass fixes:** Versions 1–2 built the right *content* register (personal-brand
framing, real career facts, real photo/video from his own Instagram) but the *visual* palette was
never checked against a real, client-approved reference set — it used a dark green/pine-tinted ink
(`#0d1815` / `#132420` / `#1b322c`, all G-channel-dominant) that reads closer to a spa/wellness
clinic than the premium-editorial-surgeon register the client had just approved. This pass is a
palette-and-detailing revision only — no new sections, no touching the real photo/video assets
already integrated (conference photo, both real talking-head clips) beyond the neutral bezel-color
tweak described below.

### The reference set (agency-internal, not in this repo)
A locked reference document (v1) names five real, currently-live, client-approved solo-doctor
personal-brand sites: **garthfisher.com**, **drkolker.com**, **drcroteau.ca**, **amakaaesthetics.com**,
**eresoplasticsurgery.com**. Its core claim: black/white/gray minimalism is the highest-confidence
base palette for this register, alongside press/media credibility badges (if real ones exist),
the doctor's own voice/philosophy as primary copy (not "meet our practice" language), and
credential-forward framing.

### What was actually verified by visiting all five sites live (not just trusting the summary)
- **garthfisher.com** — confirmed: pure black background, a chrome/metallic "GF" monogram as the
  literal hero, a stark black-and-white split contact bar ("Contact Us" / phone number), and heavy
  real press/media badges (Newsweek "America's Top Plastic Surgeon" across four categories, quotes
  from Vanity Fair, Elle, Tom Ford's "The Enhancer"). The strongest, most literal match to the
  reference doc's claim.
- **drkolker.com** — confirmed: a soft gray-gradient photographic hero over a warm-taupe band, then
  — critically — a **stark black press-logo strip** immediately below the fold (Harper's Bazaar, The
  New York Times, DuJour, NewBeauty, Vogue, New York, Allure). This is the clearest live example of
  the "press badge row" device.
- **drcroteau.ca** — **correction to the reference doc**: this site is *not* black/white/gray. It
  uses a dark teal band and a coral/terracotta CTA pill on a white base. What *does* hold up: flat,
  minimal layout, a circular monogram ("CF") echoing Fisher's device, and genuine first-person voice
  ("Je suis minutieux, attentif et franc" — "I am meticulous, attentive, and direct"). Recorded here
  so a future pass doesn't over-trust the written summary over the live site.
- **amakaaesthetics.com** — confirmed navy/gold/white palette, and confirmed the "as both professional
  and mother" personal-philosophy framing style (her copy: care informed by her own perspective as a
  surgeon and a parent), plus a genuinely restrained before/after section (2 cases on the homepage,
  not a wall of galleries).
- **eresoplasticsurgery.com** — confirmed black-and-white high-contrast photography with a navy accent
  bar, the exact tagline **"Patient-Centered Aesthetic Artistry. Beauty. Strength. Compassion."**, and
  the named product line **"Age Erase by Alexander Ereso."** Also confirmed an extensive (7-case)
  before/after gallery — i.e., selective use is a matter of taste across these sites, not a hard rule.

**Net correction to the locked doc:** 3 of 5 (Fisher, Kolker, Ereso) are genuinely black/white/gray
with a single restrained warm accent (Kolker's taupe, Ereso's navy). Croteau and Nwubah are real color
exceptions (teal/coral, navy/gold) that still keep the flat, restrained, circular-monogram, first-
person-voice DNA. The correct takeaway for this build: **black/white/gray as the dominant base, with
one warm accent used sparingly for small details (rules, borders, numerals, hover states) — not as a
large fill color.**

### Press/media check — searched, found nothing, invented nothing
Per the reference doc's explicit instruction ("use it if the real client has ANY real press/media
mention, however small — never invent one"), a live web search was run for Dr. Ahmed Awad plus
press/feature/interview terms. Nothing surfaced beyond his own social profiles and unrelated
same-name doctors elsewhere (Liverpool/Cairo, Fargo ND, Riyadh) — consistent with Version 1's own
research. **No press badge row was added.** The closest honest analog already on the site — the real,
named, dated MESEI/Motiva conference photo in the "In Practice" section — was left as the site's only
third-party-credibility device, exactly as before; it is not press coverage of him and is not
mislabeled as such.

### Dr. Awad's own real material — checked for a reason to deviate, found none, and one reason to *stay*
His only self-hosted real photo (`media/conference-mesei-riyadh.jpg`) is a conference step-and-repeat
backdrop: black background, warm gold event lighting, navy blazer — no distinct personal brand color
of his own to honor. This is a data point *for* the black/gray-with-a-warm-accent direction, not
against it: his own real photo already lives comfortably in exactly that palette. No deviation from
black/white/gray was warranted or made.

### Concrete changes made, tied to specific references
1. **Palette detox (the main fix)** — `--ink`/`--ink-2`/`--ink-3` changed from green-tinted darks
   (`#0d1815`/`#132420`/`#1b322c`) to true neutral near-black/charcoal (`#0b0b0c`/`#151515`/`#1e1e1e`);
   `--paper` cooled slightly (`#f6f3ec` → `#f6f5f2`) to drop excess yellow cast. Directly implements
   Fisher's and Ereso's confirmed-live black base. Four places had the *old* green ink hardcoded as
   literal `rgba(13,24,21,…)` instead of the token (nav background, phone-badge background, and the
   scroll-triggered nav-color JS) — these were the actual bug this pass had to catch and fix, since
   changing the CSS variable alone would have silently left the nav a different color from the rest
   of the page. Caught by grepping for the literal old hex/rgb after the token change, not just by
   eyeballing it.
2. **Primary CTA flipped from gold-fill to a stark black/white swap** (`.btn-primary`: `background:
   var(--gold)` → `background:var(--paper); color:var(--ink)`) — a direct, literal borrow of Fisher's
   black-and-white split contact bar, applied to the WhatsApp CTA instead of adding a new bar.
3. **Credential tags and the timeline's "Current" badge flattened from pill (`border-radius:999px`)
   to a flat rectangle (`var(--radius)`, 2px)**, with English-only uppercase/letter-spacing added to
   the label text (scoped to `.en-only`/`[lang=en]` specifically — Arabic script does not take
   letter-spacing well, a bug class already documented in this file's Round 2 notes, so it was
   deliberately not applied to the Arabic labels). This shifts the credential strip from reading as a
   soft "wellness pill" toward Kolker's flat press-logo-strip register while reusing the exact same
   real facts (20+ years / EBOPRAS / MRM Barcelona / Arab Board) already on the site since Version 1.
4. **The real, already-cited Instagram quote — "Choosing the right surgeon is very important"** (from
   his own real Nov 21, 2025 reel, previously only surfaced mid-page in "In Practice") — is now also
   surfaced immediately under the hero bio, styled as a cited pull-quote (gold rule, serif italic in
   English, plain-weight Arabic to avoid fake-italicizing Arabic script). This is the same real,
   sourced content reused in a second place, not new or fabricated text — it directly implements the
   reference doc's #3 signal ("the doctor's own voice as primary copy") right at the top of the page,
   where the hero was previously 100% third-person descriptive copy.
5. **English-mode headline serif treatment**: `[data-lang="en"] .hero h1, [data-lang="en"]
   .section-head h2` now render in "Plex Serif Display" (already self-hosted) instead of the sans
   body face — echoing Kolker's and Croteau's elegant serif wordmarks. Scoped to English only:
   IBM Plex Serif has no Arabic glyph coverage, so applying it to Arabic headlines would have silently
   fallen back to a mismatched system serif — Arabic headlines correctly stay on Plex Arabic sans.
6. **Phone-mock and practice-phone bezel gradients neutralized** (`#2a2a28→#0c0c0b` had a faint warm
   cast; changed to strictly neutral `#2a2a2a→#0c0c0c`) for internal consistency with the new neutral
   ink tokens — a two-line cosmetic fix, not a content change to the real video inside the frame.
7. **The faint giant hero-watermark monogram (from Version 1's no-photo era) was kept, not removed** —
   on review this is not a vestige: Nwubah's own real hero uses the same device (a giant, faint,
   semi-transparent brand-mark triangle overlaid across a background photo), so the existing Version 1
   decision to keep it "for brand continuity" turns out to already match a live reference, not just a
   post-hoc justification.

### What was deliberately NOT changed
- The real photo and both real video clips — untouched, per the brief's instruction not to touch
  already-approved real content.
- The "selective before/after" signal — the site already has zero before/after imagery (excluded on
  taste grounds since Version 2, see below). Ereso's own site proves extensive galleries are also a
  legitimate choice among the five references, so zero was not "fixed" to become some — there was
  no real case material to add anyway, and inventing any would violate the zero-fabrication rule.
- No press badge row — none exists to show, and none was invented (see above).
- Section structure, copy content, and all real facts/citations — unchanged from Version 2.

### QA this pass
- **Lang-leak sweep (both directions):** re-run via `get_page_text` in full after adding the hero
  pull-quote block (~6 new bilingual strings). Zero leaks either direction; only shared proper nouns
  (Instagram, EBOPRAS, MRM, MESEI) appear identically in both, as in prior versions.
- **Overflow, 375 / 768 / 1440px, both languages:** re-verified via
  `document.documentElement.scrollWidth` vs. `window.innerWidth` at all six combinations after the
  hero-voice block and tag-flattening changes — equal (no overflow) at every one.
- **RTL logical-property check on the new hero-voice block specifically:** confirmed via
  `getComputedStyle` that `border-inline-start` correctly resolves to `border-right` in `dir="rtl"`
  (2px, gold), and that the Arabic-mode override (`font-family:"Plex Arabic"; font-style:normal`)
  correctly suppresses the browser's fake-italic on Arabic script — this exact bug class
  (logical-property / RTL mis-resolution) is what caused the Round 2 WhatsApp-button bug in Version 1,
  so it was checked deliberately rather than assumed fine.
- **Capability gating:** re-confirmed live — both `<video>` elements reach `readyState 4`
  (`HAVE_ENOUGH_DATA`) with a `<source>` attached; toggling `data-reduce-motion="true"` collapses
  `--dur-fast` to `0s` as before. No change to the gating logic itself this pass.
- **Accordion interaction:** re-verified programmatically (`.click()` + `.open` class checks) —
  exactly one panel open at a time, unaffected by the palette/detailing changes.
- **Console:** zero errors/warnings across the full pass, in both languages, at all three widths.
- **Known tooling limitation (recurring, not new):** the sandboxed browser used for this pass's visual
  QA reproduced the exact same issue Version 1/2 already documented — a screenshot taken at any
  scrolled position (even after an explicit `scrollTo`/instant `scrollIntoView`, confirmed via
  `scrollY` readback) reliably comes back solid black, while a screenshot at `scrollY:0` renders
  correctly and matches DOM/computed-style assertions taken at the same scrolled position. Because
  this pass's new near-black palette is close in color to that failure mode, this is flagged more
  emphatically here than before: **a final human visual pass in a normal desktop browser, scrolling
  through the whole page, is now more important than ever before sending this to the prospect** —
  a blank/broken render would be harder to eyeball-catch against a legitimately very dark page than it
  was against the old page's more visibly distinct green-black. Every visual claim in this QA section
  was independently confirmed via `getComputedStyle`/`getBoundingClientRect`/`get_page_text` at the
  same positions where screenshots failed, not asserted from a screenshot alone.
- **Build/verify method:** served locally via a plain Python `http.server` (no build step, matches
  the "no dependencies" standing rule) and driven through a real browser tab, not a static file
  preview — file:// previews outside the tool's project sandbox render as non-interactive static
  snapshots and cannot run this page's JS, which would have hidden the reveal/gating/accordion
  behavior entirely.

---

## VERSION 2 — real photo/video added (reference below unchanged from its own pass)

**The gap this pass fixes:** Version 1 shipped with zero photo, zero video, zero visual
personalization of the client — a deliberate compensation (see §3 below) for the fact that his
Instagram could not be read at the time. That workaround is no longer needed or appropriate: his
Instagram is fully readable through a different scraping method, and it contains substantial real,
verifiable, on-brand video and photo content. This version replaces the typography-only hero and
credential-list body with real footage and a real photo throughout, while keeping every previously
verified fact (career timeline, credentials, contact info, Lamsa/Serene resolution) unchanged.

### How the Instagram content was retrieved
Version 1 hit an age-restriction wall trying to read `dr.ahmed_awad_plastic_surgeon`'s profile via a
profile-info scraper. This pass used a **posts-scraper** instead — Apify actor
`data-slayer/instagram-posts`, input `{"username":"dr.ahmed_awad_plastic_surgeon","maxPages":3}` —
which bypasses that wall entirely. It returned **24 real posts** (dataset reports 36 total available;
24 were pulled), dated November 2025 – August 2026, with real captions, real engagement (like/comment
counts), real timestamps, and working (if signed/expiring) CDN URLs for thumbnails and full video
files. Every photo and video used on the site was downloaded from those URLs and is now self-hosted
in `media/` — nothing hotlinked, per this pipeline's standing rule that Instagram's signed CDN URLs
expire and must never be referenced directly from a shipped page.

### What was reviewed, and the editorial calls made
All 24 posts were inspected (thumbnails for photo posts, sampled frames for every video candidate)
before anything was chosen:
- **5 real, high-quality assets were selected** — see the media table below.
- **Explicitly excluded, and why:** two posts contained genuine before/after surgical photography
  (a gynecomastia/male breast-reduction case with visible bruising, and the graphic resected-tissue
  close-up illustrating the breast-reduction educational post). Both are **real, not fabricated** —
  they were excluded on editorial/taste grounds, not verification grounds: graphic clinical photography
  reads as clinic-marketing material, not the restrained personal-brand register this site is built
  around, and is a poor first impression for a cold-outreach demo. The breast-reduction post's real
  **written** content (his own patient-education text) was kept and used — see below — just not its
  photo.
- Every hashtag set on his posts is generic/spammy (`#تجمع_بنات_جده`, `#ترند_تيك_توك`, etc.) and was
  **not** treated as reliable subject-matter labeling — e.g. one video tagged with rhinoplasty/facelift
  hashtags is actually, by its own burned-in captions, about breast augmentation. Only what is visibly
  or textually verifiable in the media itself was used in any on-site caption.
- Other platforms named in the brief (Facebook, TikTok, YouTube, Snapchat) were not re-scraped this
  pass for additional visual content — the Instagram pull alone yielded more real, on-brand material
  than the site needed. This remains available for a future pass if wanted.
- `@lamsa.ksa` was never touched (per the brief's correction that it is an unrelated handbag shop, not
  Lamsa Clinics) — not used, not re-investigated.

### Media used on the site (all self-hosted in `media/`)

| File | Source post | Date | What it is |
|---|---|---|---|
| `media/conference-mesei-riyadh.jpg` | Instagram, code `DU1FUuZCI2L` | 2026-02-16 | Real photo of Dr. Awad at the **Middle East Symposium of Ergonomix® Implants (MESEI)**, brought by Medica, Riyadh — badge/lanyard visible, real step-and-repeat backdrop. His own caption names it "مؤتمر موتيفا لجراحات الثدى المتقدمة" (Motiva Advanced Breast Surgery Conference); Motiva's flagship implant line is literally called "Ergonomix," so the caption and the backdrop's official event name are consistent, not conflicting. Highest-engagement photo on his account (54 likes / 24 comments). Downloaded at native 1080×1080. |
| `media/reel-augmentation-talk.mp4` (+ poster) | Instagram, code `DZDs-ytI7k8` | 2026-06-01 | Real talking-head clip, home/lounge setting, white coat with embroidered "Ahmed Awad, Plastic Surg[eon]". Content (per burned-in live captions) is about breast augmentation with implants and recovery — not what its hashtags suggest. Most-liked video on the account (40 likes / 18 comments). Source is 720×1280 @ 30fps, 14.9s; re-encoded here to a clean 9s loop (bottom caption band cropped out, mild contrast/saturation grade, muted, H.264, ~410KB). Used as the hero's device-mockup video. |
| `media/reel-technique-talk.mp4` (+ poster) | Instagram, code `DRT5tKECOWW` | 2025-11-21 | Real talking-head clip, clinic-office setting, visible real "لمسة LAMSA" on-screen branding + the same phone numbers/Al-Hamra-Jeddah address already verified in §1 below (independent third confirmation of the Lamsa/Serene affiliation). Burned-in caption at this clip's most legible frame reads **"مهمة جداً اختيار الجراح المناسب"** ("Choosing the right surgeon is very important") — used as the section's pull-quote, sourced exactly as shown, not paraphrased. 42 likes / 9 comments. Re-encoded to an 8s loop, top+bottom branding bars cropped out, muted, ~357KB. |
| (text only, no image) | Instagram, code `DS4zqzcCCOD` | 2025-12-30 | A real, substantial educational post he wrote himself explaining breast reduction surgery — indications, candidacy, scar placement, recovery timeline, complications, permanence — reproduced in full (bilingual) in the new "How He Explains It" section. Its accompanying photo (real resected tissue) was excluded — see above. |

All five are traceable to a specific, named, dated, real post on his own verified Instagram account —
nothing AI-generated, nothing stock, nothing staged for this build.

### New benchmark reference: real device-mockup video treatment
In addition to the four references from Version 1 (still valid, still the basis for the overall
register — see §2 below), this pass benchmarked **`garyvaynerchuk.com`** specifically for how to
present real video/photo of a named individual without it reading as a generic hero banner. Verified
live: dark charcoal/smoke-textured background, a monogram signature mark replacing a text logo, and —
the specific device borrowed — a **tilted phone-mockup frame showing a real media player with his own
photo**, next to a print-mockup, both laid over hand-drawn-style texture, with a platform-icon row
underneath. This is the direct source for this version's `.phone-mock` component: a real vertical
Instagram-shaped video inside a bezel-and-notch device frame, tilted a few degrees, with a soft radial
glow behind it and a small floating citation badge — reused twice (hero + "In Practice" section) at
two different sizes. The device-frame choice was also the pragmatic fix for the source footage's
aspect ratio: his real clips are vertical (Instagram Reels, 9:16), and a phone mockup is the honest,
premium way to present vertical footage rather than stretching/cropping it into a false widescreen.

### New sections added
1. **Hero** — restructured from a single centered column into a two-column split: existing copy/CTAs
   on one side, a real device-mockup with the augmentation-talk video autoplaying (muted, looped) on
   the other, with a small "From his real Instagram account" citation badge. The old monogram
   watermark remains as a faint background texture (kept for brand continuity) but is no longer the
   page's only visual — it's now a supporting texture, not a photo substitute.
2. **"In Practice" (`#practice`)** — new section between About and Journey. Two columns: the framed
   MESEI conference photo with a translated caption and source citation, and the technique-talk video
   in a smaller device mockup next to the real pull-quote.
3. **"How He Explains It" (`#explains`)** — new section between Education and Focus Areas. An
   accordion (four expandable panels: why performed / candidacy / scars &amp; recovery / complications)
   built entirely from his own real Instagram educational post, bilingual, with a source citation and
   a closing "Is the result permanent? Yes." line matching his own post's structure exactly.

Every new real-content block carries a small, honest, on-page source citation (platform + exact date)
— not just documented here in HANDOFF, but visible to the client himself when he reviews the site.

### QA specific to this pass
- **Lang-leak sweep, both directions:** re-run in full via `get_page_text` after adding ~40 new
  bilingual strings (In Practice + How He Explains It sections). Zero leaks in either direction —
  only shared proper nouns (Instagram, EBOPRAS, MESEI, MRM) appear identically in both, as before.
- **Overflow, 375/768/1440px, both languages:** re-verified after the hero/practice layout rework
  (new grid columns, device mockups, absolute-positioned badges are common overflow sources).
  `scrollWidth` ≤ `innerWidth` at all six combinations (3 widths × 2 languages).
- **Capability gating extended to video:** the two `<video>` elements ship with `preload="none"` and
  **no `src`** in the raw HTML — only a `data-src` attribute and a poster JPG. A small init script
  (`initReels()`) only attaches a real `<source>` and calls `.load()`/`.play()` when
  `prefers-reduced-motion` is NOT set, `deviceMemory` is not low, and Save-Data is off — verified by
  code path (same honest caveat as Version 1: this session's real device doesn't report the low-
  resource signals, so the negative branch was verified by reading the code, not by triggering it
  live). Confirmed live on this session's normal device: both videos reach `readyState 4`
  (`HAVE_ENOUGH_DATA`) and play muted/looped without console errors.
- **Accordion interaction:** verified programmatically (`.click()` + `aria-expanded` + `.open` class
  checks) that exactly one panel is open at a time and toggles correctly — not just visually inspected.
- **Links:** re-audited all `href`s after the rebuild — identical set to Version 1's verified list
  (WhatsApp, email, six socials, all in-page anchors); nothing changed, nothing broken.
- **Console:** zero errors across the full pass (one harmless one-off `console.warn` from the page's
  own dev-only overflow-QA helper, caused by `window.innerWidth` reading `0` for a single frame during
  this sandbox's initial layout — not reproducible on reload, not a real page defect, confirmed by the
  overflow re-checks above all passing cleanly).
- **Performance:** total page weight is now ~1.4MB (70KB HTML + 460KB fonts + 880KB media: 1 photo +
  2 muted/cropped/graded video loops + 2 poster JPGs) — up from Version 1's ~490KB text-only page, but
  still light for a page now carrying real video, and every media byte is gated behind the capability
  checks above for the users who shouldn't be paying for it.
- **Known tooling note, refined from Version 1:** Version 1 reported the sandboxed browser's
  screenshot capture as unreliable at certain scroll depths on this page. This pass isolated the actual
  trigger more precisely: a screenshot taken **during** a CSS `scroll-behavior: smooth` scroll (the
  page's own smooth-scroll, or a tool-driven `scrollIntoView()`/`scrollTo()` without an explicit
  `behavior:'instant'`) reliably comes back solid black; the same scroll position captured **after**
  an instant/already-settled scroll renders correctly and matches the DOM/computed-style checks run in
  parallel. Every visual claim in this QA section was confirmed either with an instant-scroll
  screenshot or with direct DOM/computed-style/`readyState` assertions — **a final human visual pass
  in a normal desktop browser is still recommended** before sending this to the prospect, standard
  practice regardless of tooling.
- **Minor pre-existing cosmetic note (not introduced this pass, not fixed):** the fixed WhatsApp button
  (`.wa-float`, unchanged from Version 1) can transiently sit over the corner of the About section's
  stat-grid at certain scroll positions on narrow (≤375px) viewports, partially covering a stat digit
  until the user scrolls a little further. This is inherent to any fixed corner button and was already
  present in Version 1; flagged here for transparency rather than left silently unmentioned.

---

## VERSION 1 (original build) — reference below unchanged

## 1. What was verified, and how

### Career (from the brief, cross-checked live)
- LinkedIn (`linkedin.com/in/dr-ahmed-awad-13395560`) was treated as the primary source for the
  career timeline and education, per the brief. I did not re-scrape LinkedIn myself (no login), but
  every date/institution from it is corroborated elsewhere below.
- **~20 years' experience is independently confirmed**, not just LinkedIn's framing: a real Instagram
  post from `@lamsa.clinics` (see below), dated **13 May 2024**, literally reads *"Serene Clinics
  welcomes Dr. Ahmed Awad, plastic and reconstructive surgeon, with over 20 years of experience"* —
  a second, fully independent source stating the same "20 years" figure on the same date his LinkedIn
  says he joined Serene Beauty Clinics.

### The Serene Beauty Clinics vs. Lamsa Clinics question — RESOLVED
This was flagged in the brief as unconfirmed. I resolved it with high confidence:
- `lamssaclinics.com`'s own "Meet our Doctors" page lists **Dr. Ahmed Awad, Plastic Surgeon**
  (alongside two dermatologists), footer copyright "© 2025".
- Instagram account **`instagram.com/lamsa.clinics`** (bio: "Lamsa Clinics | عيادات اللمسة") posted
  on **13 May 2024**: *"عيادات سيرين ترحب بانضمام د. أحمد عوض جراح التجميل والترميم بخبرة أكثر من 20
  عاما"* ("**Serene Clinics** welcomes the joining of Dr. Ahmed Awad...") — with the same phone
  numbers (0126614000 / 0593421125) that lamssaclinics.com itself lists as its own contact numbers.
- The same Instagram account posted again on **13 July 2025** — more than a year later — featuring
  Dr. Ahmed Awad by name again, confirming the relationship is ongoing, not a one-off announcement.
- **Conclusion:** Lamsa Clinics (the public-facing brand, website, and Instagram account) and "Serene
  Beauty Clinics" (the name on his LinkedIn) are the same practice/group — Lamsa is evidently the
  operating/consumer-facing name, "Serene" is used internally or as a department name. This lines up
  exactly with his LinkedIn's "Serene Beauty Clinics, Jeddah — May 2024, ongoing."
- **Design decision:** even having resolved this, the site does **not** present Lamsa/Serene as "his
  clinic." Per the brief's core instruction, the current-practice entry in the career timeline names
  it factually ("practicing as a consultant... Jeddah") without an address, hours, or building — his
  own WhatsApp is presented as the primary contact channel throughout, not a clinic phone line.

### Vezeeta listing — treated as very likely the same person, but NOT used on the site
`saudi.vezeeta.com` has a profile for **"Dr. Ahmed Awad Metwally"** in Jeddah/Al-Hamra (Arafat St.)
listing credentials **M.Sc., MRM, ABHS, EBOPRAS Fellow** — which is an exact match to his real
credentials (Master's in Reconstructive Microsurgery, Arab Board of Health Specialities, EBOPRAS
Fellow) and the same city/district. This is very likely the same doctor (his full/formal name may
include "Metwally"). I did **not** use this listing on the site because I could not independently
cross-verify it against a photo or an explicit name match — no new facts from it were needed anyway
since everything it corroborates is already sourced elsewhere.

### Contact details — cross-verified from two independent sources
- **WhatsApp `+966 56 368 1087`**: matches both the Google Business Profile phone (per the agency's
  2026-08-17 scrape) **and** the contact number listed on his own real Facebook Page
  (`facebook.com/share/1BYQzEy878/` — "Dr.Ahmed_Awad_Plastic_Surgeon", ~1K followers, active, real
  posts with real public engagement, e.g. a June 2026 reel with 32 reactions).
- **Email `ahmedplastic2010@gmail.com`**: new fact, found on that same real Facebook Page — not in
  the original brief. Added to the site's contact section.
- All social handles (Instagram, Facebook, TikTok, YouTube, Snapchat, X) were checked; the ones that
  loaded without a login wall are linked directly on the site with their real URLs. Threads was left
  off the final build (Instagram, Facebook, TikTok, YouTube, Snapchat, X are shown — Threads was
  redundant with Instagram's handle and cut for a cleaner grid; the link itself was never broken).
- **Instagram content could not be reviewed**: `@dr.ahmed_awad_plastic_surgeon` is age-restricted and
  requires login to view any posts. I did not log in (out of scope / against safe-browsing practice
  for this task). This is why there is **no before/after gallery and no photo of him** on the site —
  see §3.

### Google rating
4.8★ / 38 reviews, per the agency's own 2026-08-17 scrape. I could not get a fresh read via Google
Maps (consent-wall loop in the automated browser) or Vezeeta (403 on direct fetch), so the site states
the figure with an explicit "as last checked in August 2026" caveat rather than presenting it as
live/current.

---

## 2. Benchmark references (why these four, and what was borrowed)

The brief is explicit that the register here is a **solo personal surgeon brand**, not a multi-
department clinic (that was De Praxes's register, and is not to be repeated). I found and studied:

1. **`dr-mohammedalqahtani.com`** (Dr. Mohammed Al Qahtani, consultant plastic surgeon, Riyadh —
   practices as a consultant at "Eve Clinic," structurally the same situation as our client: a named
   surgeon, not a clinic-owner). **Borrowed:** dark, restrained palette carrying real regional trust
   cues; a floating WhatsApp CTA as the primary conversion path; testimonials with real names; a
   direct, dignified opening register. This is the closest direct match to our client's actual
   situation and market, which is why the whole site's WhatsApp-first contact model and vertical
   rhythm is closest to this reference.
2. **`garthfisher.com`** (Beverly Hills). **Borrowed:** restraint — a monogram mark instead of a
   photo-heavy nav, single-word navigation, generous negative space, a pill-shaped primary CTA. This
   is the reference for why a **photo-less, typography-forward hero** is a legitimate premium choice
   and not just a workaround (see §3) — Fisher's own site treats negative space as the luxury cue.
3. **`newyorkfacialplasticsurgery.com`** (Dr. Andrew Jacono). **Borrowed:** a serif display headline
   over the fold, and — more specifically — a **quick-strip of credential categories directly under
   the headline** (his site uses Publications/Reviews/Books/Awards; ours uses the tags row: 20+
   years / EBOPRAS Fellow / MRM Barcelona / Arab Board). The device is the same — surface a named
   surgeon's authority signals immediately, before any body copy — adapted to only the categories we
   can actually back with real facts, rather than copying his specific category list.
4. **`dr-ahmedelsherifa.com`** — used as a **negative/contrast reference**, not a source to copy: a
   glossy commercial "Masterpiece Team" clinic site with a full team photo, a call-center-style
   "Hotline" CTA, and franchise branding. This is the register the brief explicitly warns against for
   a solo veteran's personal brand — it reads as a marketing operation, not a surgeon. Kept in the
   file as the explicit "don't do this" comparison point.

De Praxes's own design (warm charcoal/bronze/sand, Fraunces serif, 3D torus-knot piece, image-
accordion doctor cards) was deliberately **not** reused anywhere — this build uses a cooler dark
green/ink palette, IBM Plex (sans + serif) instead of Fraunces, no 3D/WebGL, and no accordion pattern.

---

## 3. The no-photo decision (SUPERSEDED in Version 2 — kept below for the record)

**Status: no longer true.** Version 2 (see top of this file) found a working method to read his
Instagram and added a real photo and two real videos of him throughout the site. The reasoning below
is kept as-written because it explains an honest, correct decision at the time it was made — not
because it still describes the current site.

There is **no photo of Dr. Ahmed Awad anywhere on this site.** This was deliberate, not an oversight:
- His Instagram (where his own patient/practice photos would most likely live) is age-restricted and
  requires login — I did not log in.
- His Facebook Page's photo albums returned "Not Found" to an unauthenticated fetch.
- I never obtained a photo I could independently verify as (a) actually him and (b) published by him.

Per the pipeline's hard rule — no stock photos, nothing unverifiable — the only correct move was to
leave imagery out entirely rather than guess. The design compensates for this on purpose: a large
faint outlined monogram watermark ("أع") sits behind the hero copy instead of a portrait, and the
whole page leans on typography, real numbers, and the credential/timeline structure to carry the
authority a photo would normally carry (see the Garth Fisher reference above — this is a legitimate
register, not a placeholder). **If a real, verifiable photo becomes available later** (e.g. Aymean can
get a login-gated Instagram photo confirmed as his own, or a direct submission from the client), it
would slot naturally into the hero next to the watermark — the CSS is already structured so that's a
small addition, not a redesign.

## 4. What was searched for and deliberately left out

- **Before/after case photos** — not accessible (see above). None fabricated, none substituted with
  stock imagery.
- **Patient testimonials** — I found exactly one real, public comment on his Facebook page ("ربنا
  يبارك فيك ويحفظك يارب دكتورنا الغالي واخويا المحترم احمد عوض...") but it explicitly reads as coming
  from a friend/relation ("و**أخويا** المحترم" — "and my respected **brother**"), not a patient. Using
  it as a patient testimonial would have been misleading even though the words are real, so it is not
  on the site. No other reviews were accessible in full text (Google Maps review text specifically
  could not be pulled — only the aggregate star rating and count).
- **A specific practice address** — deliberately omitted. His own Facebook lists 3711 Al Fadl, Al
  Hamra (matching the Google Business listing); Lamsa Clinics lists 7726 Al Fadl, Al Hamra — same
  street, different building numbers, and I could not cleanly resolve whether one is stale, a
  registration artifact, or genuinely a separate address. Per the brief's explicit instruction not to
  invent a fixed building, the site names only the city (Jeddah) and directs everyone to WhatsApp.
- **Threads** — real, working handle, but cut from the final social grid for a cleaner 3×2 layout
  since it mirrors the Instagram handle exactly. Not a broken link, just an editorial trim.
- **A live/current Google review count** — the 4.8★/38 figure is dated (agency scrape, 2026-08-17)
  and stated as such rather than implied to be real-time.

---

## 5. Build rounds

1. **Round 1** — full first pass: bilingual AR/EN structure, hero, about, career timeline (hospital →
   private practice → consultant), education/credentials grid, focus areas, Google-rating trust
   section, contact section, floating WhatsApp button. Self-hosted IBM Plex Sans Arabic + IBM Plex
   Serif (OFL-licensed, pulled from the IBM/plex GitHub repo, not a CDN).
2. **Round 2** — bug fixes found in live testing:
   - `insetInlineStart`/`insetInlineEnd` had been written in **camelCase inside actual CSS**, which
     is invalid syntax — browsers silently ignore it. This left the floating WhatsApp button (and
     several other positioned elements) pinned to the wrong edge in one language direction. Fixed to
     valid kebab-case `inset-inline-start`/`inset-inline-end` everywhere (nav underline, hero-scroll
     indicator, timeline track/dots, floating WhatsApp button, skip link). Verified by computed style
     in both `dir="ltr"` and `dir="rtl"`.
   - Hardened the scroll-reveal system. The original IntersectionObserver-only approach could leave a
     short section permanently invisible if a user scrolled past it very fast (the callback can, in
     rare cases, never see it intersect) — added a `setTimeout`-driven fallback that force-reveals any
     `.reveal` element whose top has already passed above the viewport.
   - Fixed a text-concatenation bug ("ongoingCURRENT" / "مستمرالحالي" running together with no space)
     in the timeline's "current" badge, in both languages.
3. **Round 3** — added the hero watermark device described in §3, and hardened against the horizontal
   bleed it intentionally introduces (`overflow-x:hidden` + `max-width:100%` on `<html>`, not just
   `<body>`; `overflow:hidden` on the hero section itself). Verified `scrollWidth === innerWidth` at
   375 / 768 / 1440px afterward.
4. **Round 4** — trimmed an unused font weight (IBM Plex Sans Arabic Light/300 was declared via
   `@font-face` but never referenced by any rendered text, so it was dead weight) — removed the
   declaration and the file.

---

## 6. QA results

- **Lang-leak sweep (AR → EN and EN → AR):** 0 leaks each direction. Verified by extracting full
  rendered page text (`get_page_text`, which respects `display:none`) in both modes — every visible
  string switches fully; only shared proper nouns/acronyms (Instagram, Facebook, TikTok, YouTube,
  Snapchat, X, EBOPRAS, MRM) correctly appear identically in both.
- **Responsive, zero horizontal overflow:** verified via `document.documentElement.scrollWidth` vs.
  `window.innerWidth` at **375px, 768px, and 1440px** in both languages — all equal (no overflow) both
  before and after the Round 3 watermark was added.
- **RTL numeral/phone/email direction:** spot-checked — phone number, dates, and email render
  correctly left-to-right inside the RTL page (isolated via a `.ltr` unicode-bidi class), no digit
  reversal, matching a bug class this pipeline has hit before on other client builds.
- **Capability gating, verified live (not just asserted):**
  - `prefers-reduced-motion`: toggling `data-reduce-motion="true"` (the same attribute the page's own
    media-query listener sets) confirmed `--dur-fast` collapses to `0s` and the hero-scroll pulse
    animation's `animationName` becomes `none`.
  - `navigator.deviceMemory < 4` and `navigator.connection.saveData` feed the same `reduce` flag in
    the page's own init script (confirmed by code read — this session's real device reports 16GB/no
    save-data, so the low-resource branch could not be triggered live without spoofing `navigator`,
    which the available tools don't support pre-load; verified instead via the shared code path and
    the CSS-level test above, which is the part that actually matters for the visual effect).
  - Save-Data additionally hides the decorative grain-texture overlay (`[data-save-data="true"] .grain
    { display:none; }`).
- **Console:** zero errors/warnings on load, in either language, at any tested viewport.
- **Links:** every `href` audited against the verified contact list — `wa.me/966563681087`,
  `mailto:ahmedplastic2010@gmail.com`, and all six social URLs match exactly what was verified in §1.
- **Performance:** ~50KB HTML + ~440KB across the six font files actually used (browsers only fetch
  `@font-face` weights that are actually matched by rendered text — confirmed via the Resource Timing
  API, which showed exactly 6 font requests, not 7, after the unused Light weight was still present
  in Round 1–3, and correctly 6 total files on disk after Round 4's cleanup). `DOMContentLoaded` ~40ms
  and full `load` ~120ms on a local static server — not a substitute for real-network numbers, but
  confirms the page itself is lightweight with no render-blocking external requests.
- **Known tooling limitation, disclosed honestly:** the sandboxed browser used for this build's visual
  QA became unreliable at capturing screenshots at certain scroll depths on this tall single-page
  layout (screenshots intermittently came back blank while the DOM/computed-styles underneath were
  verifiably correct — confirmed by cross-checking `getComputedStyle`, `getBoundingClientRect`, and
  `get_page_text` at the same scroll positions where screenshots failed). This looked like a capture-
  pipeline artifact specific to the sandbox, not a rendering bug in the page, but **a final human
  visual pass in a normal desktop browser is recommended before sending this to the prospect** — standard
  practice regardless, but worth flagging explicitly here since the automated visual coverage of the
  Education/Focus/Trust sections at desktop width is thinner than the rest.

---

## 7. Files

- `index.html` — the entire site.
- `fonts/` — IBM Plex Sans Arabic (Regular/Medium/SemiBold/Bold) + IBM Plex Serif (Regular/SemiBold),
  both OFL-licensed, pulled directly from `github.com/IBM/plex` and self-hosted; `LICENSE-*.txt` kept
  alongside them for attribution.
- `media/` — real photo + video, self-hosted (Version 2). All sourced from Dr. Awad's own public
  Instagram, re-encoded/cropped/graded locally with ffmpeg, never hotlinked. See the Version 2 media
  table near the top of this file for exact source post/date per file.
- No build step, no dependencies, no external requests at runtime.
