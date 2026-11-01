# Temple Door Platform — Navigation Architecture
**Canonical reference for every page type across all sites.**
Every new session that builds or edits any HTML page must read this document before writing a single link.

---

## 1. Canonical URLs (locked — never deviate)

| Site | Canonical URL | Notes |
|---|---|---|
| Temple Door (root) | `https://home.intelligencereport.info` | NOT intelligencereport.info — that domain is an unrelated third-party site |
| Romans Road Commentary | `https://commentary.intelligencereport.info` | |
| Spiritual Growth Lessons | `https://lessons.intelligencereport.info` | |
| Study Hall | `https://study.intelligencereport.info` | |
| Confrontations with Doctrine | `https://confrontations.intelligencereport.info` | |
| The Watchman | `https://watchman.intelligencereport.info` | |
| The Christian Life | `https://christianlife.intelligencereport.info` | |

> **Rule:** When in doubt about any URL, check this table. Never construct a URL from memory.

---

## 2. Site Inventory

| Site name | Subdomain | Repo | Content type |
|---|---|---|---|
| Temple Door | home | temple-door | Platform landing — card index to all sites |
| Romans Road Commentary | commentary | romans-road (or commentary) | Verse-by-verse Romans exegesis — per-lesson HTML pages, Illuminations, Greek Guide |
| Spiritual Growth Lessons | lessons | lessons | Shorter doctrinal curriculum lessons |
| Study Hall | study | study-hall | Doctrine library (45 pages), Scripture index, cross-site content index |
| Confrontations with Doctrine | confrontations | confrontations | Transcript-based doctrinal studies |
| The Watchman | watchman | the-watchman | Long-form analytical articles |
| The Christian Life | christianlife | christianlife | Doctrinal studies on Christian living — content units by topic/passage |

---

## 3. Page Level Taxonomy

Four levels. Every page in the platform falls into exactly one.

### Level 0 — Platform Root
**What it is:** The Temple Door index page. Entry point to all sites.
**URL:** `https://home.intelligencereport.info/`
**Page:** `temple-door/index.html`
**Nav:** None. No breadcrumb. No back link. The site mark "IntelligenceReport.info" is the identity, not a link. Cards do the navigation.
**Header links:** None.
**Footer:** Author attribution only.

---

### Level 1 — Site Landing Page
**What it is:** The index page of a subdomain site. Describes the site and lists its content units.
**URL pattern:** `https://[site].intelligencereport.info/`
**Examples:** `christianlife/index.html`, `watchman/index.html`, `confrontations/index.html`
**Nav:** Single back link only — no breadcrumb needed (only one level above).

**Header (top of page):**
```
← Temple Door     [right-aligned or below: site mark "IntelligenceReport.info"]
```
Rendered as a small-caps Cinzel link, gold-dim color, positioned above the page h1.

**Footer:** Author attribution only.
**In-body links:** None. Cards handle forward navigation.

---

### Level 2 — Content Unit Page
**What it is:** A page under a site landing — a study, article, lesson, or doctrine page. This is where the actual content lives.
**URL pattern:** `https://[site].intelligencereport.info/[slug].html`
**Examples:**
- `christianlife/dynamics-for-disaster.html`
- `watchman/[article-slug].html`
- `study/doctrines/[doctrine-slug].html`

**Nav:** Horizontal nav bar — site name left, cross-site links right.

**Header (top of page):**
```
[Site Name]                    Spiritual Growth Lessons  Study Hall  Romans Road  Temple Door
```
- Left: site name in gold Cinzel, links to that site's index (`https://[site].intelligencereport.info/`)
- Right: cross-site navigation links in small uppercase Cinzel — always include Temple Door; include other sites relevant to this content
- Single nav bar replaces both breadcrumb and secondary doc-nav

**Standard right-side links (use all that apply to the content):**
- Spiritual Growth Lessons → `https://lessons.intelligencereport.info`
- Study Hall → `https://study.intelligencereport.info`
- Romans Road → `https://commentary.intelligencereport.info`
- The Watchman → `https://watchman.intelligencereport.info`
- Temple Door → `https://home.intelligencereport.info` *(always last)*

**Footer:**
- Author attribution
- `← [Site Name]` back link
- Mirror key cross-site links from the nav bar

**In-body links:** Depends on document type — see Section 5.

---

### Level 3 — Sub-Page
**What it is:** A page nested under a content unit. Currently rare — would apply if a content unit grows large enough to be split into sub-pages.
**URL pattern:** `https://[site].intelligencereport.info/[unit]/[sub]/`
**Nav:** Full four-segment breadcrumb.

**Header:**
```
Temple Door  ›  [Site Name]  ›  [Unit Title]  ›  [Sub-page Title]
```
- First three segments are links; last segment is plain text.

**Footer:** Author attribution + `← [Unit Title]` back link.

---

## 4. Study Hall — Special Case

Study Hall has its own internal nav that replaces the simple breadcrumb on non-landing pages. It is a cross-functional reference library, and readers navigate laterally within it as much as vertically.

**Study Hall nav bar (Level 2 and 3 pages):**
```
Temple Door  |  Study Hall  |  Doctrine Library  |  Scripture Index
```
- "Temple Door" → `https://home.intelligencereport.info`
- "Study Hall" → `https://study.intelligencereport.info`
- "Doctrine Library" → `https://study.intelligencereport.info/doctrines/` (or `doctrine-library.html` — confirm path)
- "Scripture Index" → `https://study.intelligencereport.info/scripture-index.html` (confirm path)

Active page is plain text in the nav bar, not a link.

**Individual doctrine pages additionally get:**
- Action buttons top-right (PDF, Link, Copy, Image, HTML, Embed — Phosphor icons)
- These are already standardized; do not add breadcrumb on top of the Study Hall nav bar

---

## 5. Document Handling

**Document handling** = the action button set that appears on every content page (Level 2 and 3), giving the reader tools to use the content: print, link, embed, copy HTML. These are utility actions, not navigation. They are separate from the breadcrumb (location) and from semantic/related-content links.

**Standard document handling buttons (Phosphor icons, matching Study Hall implementation):**

| Button | Icon | Action |
|---|---|---|
| PDF | pdf icon | Print section/page as PDF |
| Copy Link | chain link icon | Copy URL (with anchor) to clipboard |
| Embed | embed/frame icon | Copy `<iframe>` embed snippet to clipboard |
| Copy HTML | `</>` icon | Copy section HTML to clipboard |

**Placement:**

- **Short pages (Type A/B):** Fixed floating panel, top-right of viewport. Buttons operate on the whole page.
- **Long-form documents (Type C, 20+ chapters):** Buttons appear per chapter, right-aligned below or beside the chapter heading. Each button operates on that chapter's content: PDF prints that section, Copy Link copies the anchor URL for that chapter, Copy HTML copies that chapter's section HTML, Embed copies an iframe pointing to that anchor.

**Per-chapter button behavior (Type C):**
- PDF: collects HTML from the chapter heading to the next chapter heading; opens a minimal print window with that content
- Copy Link: copies `[page URL]#[chapter-anchor-id]` to clipboard
- Copy HTML: copies the `outerHTML` of the chapter section to clipboard
- Embed: copies `<iframe src="[page URL]#[chapter-anchor-id]" ...></iframe>` to clipboard

**Icon library:** Phosphor Icons (already in use across the platform — load from CDN, consistent with Study Hall)

**Tooltip:** Each button shows a tooltip on hover naming the action.

---

## 5b. Related Content Nav (secondary nav)

Distinct from document handling. Links to related content elsewhere on the platform — other sites or pages the reader might want based on this content's subject.

**Top:** Nav row immediately below the breadcrumb header.
**Bottom:** Same links mirrored in the footer, so the reader can navigate out after finishing.

```html
<nav class="doc-nav">
  <a href="https://lessons.intelligencereport.info">Spiritual Growth Lessons</a>
  <!-- add further related links as content is published -->
</nav>
```

**Rule:** Every link in the top doc-nav must also appear in the footer. Top and footer always in sync.

---

## 6. Document Type Rules — In-Body Link Placement

Not all Level 2 pages are the same length or structure. Three document types:

---

### Type A — Short Page (< ~1,500 words, no sections)
**Examples:** Most Watchman articles, shorter Spiritual Growth Lessons, some Confrontations transcripts.

**Header:** Level 2 breadcrumb (as above).
**In-body:** No internal navigation needed. Content is read start to finish.
**Footer:** Author attribution. Optional: `← [Site Name]` back link.

---

### Type B — Sectioned Page (multi-section, single scroll)
**Examples:** Medium-length doctrinal lessons, some Watchman articles, doctrine pages.

**Header:** Level 2 breadcrumb.
**In-body:** TOC at top if more than ~5 named sections. No back-to-top links needed unless very long.
**Footer:** Author attribution. `← [Site Name]` back link.

---

### Type C — Long-Form Document (multi-chapter, 10,000+ words)
**Examples:** `dynamics-for-disaster/index.html` (20 chapters, ~110 pages). Any future content unit of comparable length.

**Header:** Level 2 breadcrumb.

**Page-level TOC:** Immediately below the forward/intro section, before Chapter 1. Links anchor to each chapter heading. Already implemented in dynamics-for-disaster.

**Chapter-level navigation:** At the bottom of each chapter section (after Chapter Conclusions), a small back-to-top link:
```
↑ Back to contents
```
Links to `#top` or the TOC anchor. Rendered in small Cinzel, gold-dim, right-aligned or centered.

**Footer:**
- Author attribution
- `← [Site Name]` back link — important on long pages because the reader finishes far from the header

**Optional (not required on first build):** Prev/Next chapter links at the bottom of each chapter. Implement only when content is stable and chapters are not being reorganized.

---

## 6. Romans Road Commentary — Special Case

The Romans Road Commentary is the largest site on the platform. It has its own internal structure that may need its own extended nav spec. Notes for now:

- Lesson pages are Level 2 but may link laterally to adjacent lessons (prev/next)
- Illuminations pages live under the Commentary subdomain but are a distinct content type — closer to Type A/B documents
- Greek Guide (`greek-guide.html`) is a reference tool, not a lesson — treat as Type B, no lesson prev/next links

**Commentary lesson header:**
```
Temple Door  ›  Romans Road Commentary  ›  [Lesson title or reference]
```

**Commentary lesson footer:**
- Author attribution
- `← Romans Road Commentary` back link
- Optionally: `← Previous Lesson` / `Next Lesson →` (when the lesson series is ordered and stable)

---

## 7. Page Analysis — Known Pages

Independent analysis of each known page type.

---

### home.intelligencereport.info/index.html
**Level:** 0
**Purpose:** Central landing for the whole platform. Reader orientation.
**Inbound:** Direct URL, search, shared links from all sub-sites.
**Reader wants:** Find the right site and click into it.
**Header links:** None.
**Body links:** Cards only.
**Footer:** Author attribution.
**Back-to-top:** Not needed.
**Notes:** The site mark "IntelligenceReport.info" is visual identity, not a link. Do not add a nav bar to this page.

---

### christianlife.intelligencereport.info/index.html
**Level:** 1
**Purpose:** Landing page for The Christian Life. Lists content units.
**Inbound:** Temple Door card click, direct URL.
**Reader wants:** Find a study and click into it.
**Header links:** `← Temple Door` (above the h1, small Cinzel, gold-dim).
**Body links:** Content unit cards.
**Footer:** Author attribution.
**Back-to-top:** Not needed.

---

### christianlife.intelligencereport.info/dynamics-for-disaster.html
**Level:** 2
**Document type:** C — Long-form
**Purpose:** Full doctrinal study — 20 chapters on Matthew 8:18–27, Luke 9:57–62, 2 Peter 1.
**Inbound:** The Christian Life landing card click, direct URL or search.
**Reader wants:** Study the content; navigate between chapters; return to The Christian Life.
**Header:** Breadcrumb — `Temple Door  ›  The Christian Life  ›  Dynamics for Disaster` (current page = plain text, not a link)
**Document handling top:** `Spiritual Growth Lessons` → `https://lessons.intelligencereport.info` · Add Romans Road Commentary link when Romans 9 lessons are published
**Page TOC:** Yes — `id="contents"` on TOC div, immediately after the Forward block, before Chapter 1. ✓
**Back-to-contents links:** `↑ Back to contents` before each chapter heading (after the first) and after the last chapter. ✓
**Footer:** Author attribution + `← The Christian Life` + `Spiritual Growth Lessons` (mirrors doc-nav top). ✓
**Pending:** Romans 9 link — add to both doc-nav top and footer once Romans 9 lessons are published at their URL.

---

### watchman.intelligencereport.info/index.html
**Level:** 1
**Purpose:** Landing for The Watchman. Lists articles.
**Header links:** `← Temple Door`
**Body links:** Article cards.
**Footer:** Author attribution.

---

### watchman.intelligencereport.info/[article-slug].html
**Level:** 2
**Document type:** A or B depending on length.
**Header:** Breadcrumb — `Temple Door  ›  The Watchman  ›  [Article Title]`
**Footer:** Author attribution + `← The Watchman`
**Notes:** Action buttons (PDF, Link, Copy, Image, HTML, Embed) top-right — already standardized on Watchman articles, carry forward.

---

### study.intelligencereport.info/index.html
**Level:** 1
**Purpose:** Study Hall landing.
**Header links:** `← Temple Door`
**Body links:** Internal tool cards (Doctrine Library, Scripture Index, etc.)
**Footer:** Author attribution.

---

### study.intelligencereport.info/doctrines/[doctrine].html
**Level:** 2
**Document type:** B (sectioned)
**Header:** Study Hall nav bar (NOT simple breadcrumb — see Section 4).
**Action buttons:** PDF, Link, Copy, Image, HTML, Embed — top-right. Already standardized.
**Footer:** Author attribution.
**Notes:** Do not add a breadcrumb bar to doctrine pages — the Study Hall nav bar is the standard.

---

### commentary.intelligencereport.info/index.html
**Level:** 1
**Purpose:** Romans Road Commentary landing.
**Header links:** `← Temple Door`
**Footer:** Author attribution.

---

### commentary.intelligencereport.info/[lesson-slug].html (or lesson pages)
**Level:** 2
**Document type:** B or C depending on lesson length.
**Header:** Breadcrumb — `Temple Door  ›  Romans Road Commentary  ›  [Lesson Ref/Title]`
**Footer:** Author attribution + `← Romans Road Commentary` + optional prev/next lesson links.

---

### commentary.intelligencereport.info/illuminations/illuminations.html
**Level:** 2
**Document type:** B (or index to individual illuminations)
**Header:** Breadcrumb — `Temple Door  ›  Romans Road Commentary  ›  Illuminations`
**Footer:** Author attribution + `← Romans Road Commentary`
**Notes:** Individual illumination articles use the same pattern. Illuminations nav was previously standardized as: `Temple Door | Study Hall | Home | Guide to the Greek NT | Search` — this needs to be revisited for consistency with the breadcrumb standard. Flag for review.

---

### commentary.intelligencereport.info/greek-guide.html
**Level:** 2
**Document type:** B (reference tool)
**Header:** Breadcrumb — `Temple Door  ›  Romans Road Commentary  ›  Guide to the Greek New Testament`
**Footer:** Author attribution + `← Romans Road Commentary`

---

### lessons.intelligencereport.info/index.html
**Level:** 1
**Purpose:** Spiritual Growth Lessons landing.
**Header links:** `← Temple Door`
**Footer:** Author attribution.

---

### lessons.intelligencereport.info/[lesson].html
**Level:** 2
**Document type:** A or B.
**Header:** Breadcrumb — `Temple Door  ›  Spiritual Growth Lessons  ›  [Lesson Title]`
**Footer:** Author attribution + `← Spiritual Growth Lessons`

---

### confrontations.intelligencereport.info/index.html
**Level:** 1
**Purpose:** Confrontations with Doctrine landing.
**Header links:** `← Temple Door`
**Footer:** Author attribution.

---

### confrontations.intelligencereport.info/[episode].html
**Level:** 2
**Document type:** B or C depending on transcript length.
**Header:** Breadcrumb — `Temple Door  ›  Confrontations with Doctrine  ›  [Episode Title]`
**Footer:** Author attribution + `← Confrontations with Doctrine`

---

## 8. Implementation Notes

**Nav bar HTML pattern (Level 2):**
```html
<nav class="site-nav">
  <a class="nav-site" href="https://[site].intelligencereport.info/">[Site Name]</a>
  <div class="nav-links">
    <a href="https://lessons.intelligencereport.info">Spiritual Growth Lessons</a>
    <a href="https://study.intelligencereport.info">Study Hall</a>
    <a href="https://commentary.intelligencereport.info">Romans Road</a>
    <a href="https://home.intelligencereport.info">Temple Door</a>
  </div>
</nav>
```
Include only the right-side links relevant to this content. Temple Door is always last.

**Nav bar CSS:**
```css
.site-nav {
  background: var(--parchment);
  border-bottom: 1px solid var(--border);
  padding: 0.8rem 2rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.site-nav .nav-site {
  font-family: 'Cinzel', serif;
  font-size: 0.82rem;
  font-weight: 600;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: var(--gold);
  text-decoration: none;
}
.site-nav .nav-links {
  display: flex;
  gap: 2rem;
}
.site-nav .nav-links a {
  font-family: 'Cinzel', serif;
  font-size: 0.72rem;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: var(--ink);
  text-decoration: none;
  opacity: 0.65;
}
.site-nav .nav-links a:hover { opacity: 1; color: var(--gold); }
```

**Level 1 back link pattern:**
```html
<a class="back" href="https://home.intelligencereport.info">← Temple Door</a>
```
Placed above the h1. Styled: small Cinzel, gold-dim color, uppercase, letter-spaced.

**Back-to-contents link pattern (Type C documents):**
```html
<p class="chapter-return"><a href="#contents">↑ Back to contents</a></p>
```
Placed after each `.conclusions-heading` section. Give the TOC wrapper an `id="contents"`.

**Footer back link pattern:**
```html
<footer>
  JohnDavid Wilbourn &nbsp;·&nbsp; IntelligenceReport.info
  &nbsp;&nbsp;|&nbsp;&nbsp;
  <a href="https://[site].intelligencereport.info">← [Site Name]</a>
</footer>
```

---

## 9. Known Issues Requiring Remediation

| Page | Issue | Priority |
|---|---|---|
| Illuminations pages | Nav pattern uses old Study Hall nav — may conflict with breadcrumb standard | Review |
| Study Hall nav bar | Confirm exact file paths for Doctrine Library and Scripture Index links | Confirm |
| All content pages | Document handling action buttons not yet implemented on existing pages (SGL lessons, Romans Road lessons, Confrontations, Watchman articles) — standard is defined in Section 5; apply on next edit of each page | Ongoing |

---

*Last updated: 2026-10-31. Update this file whenever a new page type is built or a nav decision is made.*
