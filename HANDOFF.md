# HANDOFF — Dr. Ahmed Awad personal-brand demo

Client: **Dr. Ahmed Awad (د.أحمد عوض)** — Consultant Plastic & Reconstructive Surgeon, Jeddah, KSA.
This is a **personal professional-brand site**, not a clinic site. He does not own a clinic, has no
fixed address, and has no in-house team — every section is built around that fact deliberately.

Repo: `github.com/Aymean/ahmedawad-demo` (public). Single self-contained `index.html`, no framework,
no external CDN requests — fonts self-hosted in `fonts/`, real photo/video self-hosted in `media/`.

---

## VERSION 2 — real photo/video added (this pass)

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
