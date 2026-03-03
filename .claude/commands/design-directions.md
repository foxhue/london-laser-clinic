# /design-directions — Generate homepage design directions from project.json

Read `project.json`, research the client's industry via Perplexity, then generate 3 mood-driven homepage concepts plus a wildcard direction — each as a self-contained `index.html` + `styles.css` pair inside `designs/design-{key}/`.

The 3 standard directions are driven by `designs[].mood` from `project.json`. The wildcard (Design D) is driven entirely by curated inspiration references — Dribbble shots, Webflow templates, and other visual references that push beyond industry conventions. Same content, radically different visual treatment.

**Run this after** `/scaffold` (which creates the `designs/index.html` hub) and `/brand-palette` (which proposes colour palettes). The hub already exists — this command generates the actual homepage concepts it links to.

## Steps

### 1. Read project.json
Extract:
- `client.name`, `client.short_name`, `client.tagline` — for page headings, hero copy, footer
- `client.slug` — for CSS variable prefixes (`--{slug}-primary`, etc.)
- `client.industry`, `client.location` — for Perplexity research queries and industry-specific copy
- `client.phone`, `client.email`, `client.website` — for CTA sections and footer contact info
- `brand.colors.*` — default palette (fallback when `designs[].palette` is null)
- `brand.fonts.heading`, `brand.fonts.body`, `brand.fonts.google_fonts_url` — for typography
- `designs[]` — array of `{ key, name, mood, palette }` (typically 3 entries, drives visual approach per direction)
- `pages[]` — array of `{ key, title, slug }` — service pages inform nav links and service cards
- `agency.name` — for code comments and footer attribution

### 2. Read inspiration/references.md

Check `inspiration/references.md` for two types of content:

**Direction references** (A/B/C): If the file has site references grouped by design direction (or ungrouped general references), extract:
- Reference sites, URLs, and descriptions
- "What's good" notes and "Borrow for this project" insights
- Visual patterns, layout approaches, and typography observations

Use these to inform the design decisions for the 3 standard directions in step 4.

If direction references are empty or template-only, skip them — Perplexity research in step 3 is sufficient for the standard directions.

**Wildcard references**: Look for a `## Wildcard` section (or similar heading). This section contains curated inspiration links — Dribbble shots, Webflow templates, Awwwards sites, or any visual references that push beyond the industry norm. Extract:
- Visual patterns: layout structure, grid breaking, whitespace treatment
- Colour approach: dark mode, high contrast, unexpected palettes
- Typography style: oversized, experimental, mixed weights
- Interaction feel: what makes these designs stand out
- Specific elements worth borrowing for the wildcard direction

The wildcard references are **required** — they are the sole brief for Design D. If the Wildcard section is empty, warn the user that wildcard inspiration is needed before generating Design D, and generate only the 3 standard directions.

### 3. Research via Perplexity

Use `mcp__perplexity__perplexity_search` — **two queries**:

**Query 1 — Competitor aesthetics**:
`"top {client.industry} websites {client.location} web design homepage layout style"`

**Query 2 — Industry trends**:
`"best {client.industry} website design 2026 homepage layout trends modern"`

Collect from both queries:
- Competitor homepage layouts (hero styles, service presentation, navigation patterns)
- Colour patterns and imagery styles common in this industry
- Typography approaches (serif vs sans-serif, weight contrasts, letter-spacing)
- What works well and what feels generic or dated
- Differentiation opportunities — gaps in what competitors are doing

This research informs design decisions but doesn't override the `mood` descriptions from `project.json`.

### 4. Plan 4 directions

#### Standard directions (A/B/C)

For each entry in `designs[]`, read its `mood` string and map it to concrete design decisions. The three designs must be **visually distinct** — different layouts and structural choices, not just colour swaps.

For each direction, decide:

| Decision | Options (vary per mood) |
|----------|------------------------|
| Nav style | centred logo with split links, left-aligned logo with right nav, overlay/transparent nav |
| Hero | full-bleed background image, split layout (image + text side by side), asymmetric offset, text-focused minimal |
| Services | 3-column flat cards, 6-card grid with image overlays, minimal list with hover reveals |
| About | 50/50 image-text split, full-width background with offset text, stacked with large stats |
| Testimonials | single large pull-quote, multi-card grid (2-3 cards), slider-style with pagination dots |
| CTA | minimal centred on blush/surface background, full-width dark band, integrated with footer |
| Footer | 4-column standard grid, minimal 2-column, expanded with large logo |
| Colour usage | which surfaces use which palette colours, contrast strategy, accent placement |
| Typography | heading scale (h1 size, letter-spacing), weight contrasts, body line-height |
| Border radius | sharp (0), subtle (2-4px), soft (8-12px) |
| Spacing | tight vertical rhythm, balanced, generous/airy |

#### Wildcard direction (D)

The wildcard has no `mood` string — its visual approach is derived entirely from the curated references in the Wildcard section of `references.md`. Analyse the collected references and extract:

1. **The dominant visual pattern** — what do the references have in common? (e.g., dark backgrounds, oversized type, broken grids, heavy imagery)
2. **How it contrasts with A/B/C** — the wildcard should feel like it comes from a different design universe, not a 4th variation on the same themes
3. **What to borrow literally** — specific layout structures, section treatments, or typographic approaches from the references
4. **A colour approach** — derive from the references. If `designs[]` has a 4th entry with a `palette`, use it. Otherwise, extract a palette from the reference aesthetics that contrasts with the other 3 directions. Fall back to `brand.colors` only as a last resort.

Map these observations to the same decision table above. The wildcard should make different choices from all 3 standard directions on at least nav style, hero layout, and spacing.

Document all decisions (including reference attribution) as comments in the generated CSS header block.

**Wildcard naming**: Use key `d`, name derived from the reference aesthetic (e.g., "Dark Editorial", "Brutalist Bold", "Studio Mono"). The name should capture the vibe of the curated references.

### 5. Generate homepage content

Write realistic, industry-specific copy that will be **shared across all 4 designs** (same words, different visual treatment). This is critical — the client must compare layouts, not copywriting.

Sections:

1. **Nav** — Logo (text-based: `{client.short_name}` main + tagline sub), links from `pages[]` (use `title` for link text), CTA button ("Book Now" or similar industry-appropriate label)

2. **Hero** — Headline (compelling, industry-specific), subheadline (1-2 sentences expanding on value proposition), 1-2 CTA buttons (primary + secondary), hero image reference (`../../website/images/`)

3. **Services** — 3-6 cards built from `pages[]` service pages. Each card: image (`../../website/images/`), `h3` title, 1-2 sentence description. Card count and layout vary per design but content is the same.

4. **About** — Section eyebrow, `h2` heading, 2 paragraphs about the business (industry-specific, professional), 2-3 stat blocks (e.g., "10+ Years", "5,000+ Clients"), image reference

5. **Testimonials** — 1-3 placeholder quotes marked as placeholders (e.g., `<!-- Placeholder testimonial — replace with real client quote -->`). Include client first name + initial, treatment type. Number of visible quotes varies per design layout.

6. **CTA** — Booking/contact section with `{client.phone}` and `{client.email}` from config. Eyebrow, heading, paragraph, CTA button.

7. **Footer** — 4 logical groups: brand (logo + tagline + brief description), services (links from `pages[]`), company (About, Contact, Privacy, Terms), contact (`{client.phone}`, `{client.email}`, `{client.location}`). Copyright line with `{client.name}`.

### 6. Generate files

For each of the 4 directions (3 from `designs[]` + the wildcard), generate two files:

#### `designs/design-{key}/index.html`

Full homepage concept (~400+ lines). Requirements:

**Document structure**:
- `<!DOCTYPE html>` with `lang="en"`
- `<meta charset="UTF-8">`, viewport meta, description meta using `{client.tagline}`
- `<title>{client.name} — {designs[].name}</title>`
- Google Fonts loaded from `brand.fonts.google_fonts_url` with `preconnect`
- Linked `styles.css` (same directory)
- `<body>` wraps content in `.page-wrapper`

**Navigation**:
- "← Design Directions" back-link to `../index.html` — small, muted, above the nav bar
- CSS-only mobile hamburger menu using checkbox toggle pattern (no JavaScript):
  ```html
  <input type="checkbox" id="nav-toggle" class="nav-toggle-input" aria-hidden="true">
  <label for="nav-toggle" class="nav-toggle" aria-label="Toggle menu">
    <span class="nav-toggle__bar"></span>
    <span class="nav-toggle__bar"></span>
    <span class="nav-toggle__bar"></span>
  </label>
  ```
- `<nav>` with `aria-label="Main navigation"`

**Content sections**:
- Each section wrapped in `<section>` with `id`, `class`, and `aria-label`
- Section comments using box-drawing characters: design name + mood + section description
  ```html
  <!-- ═══════════════════════════════════════════════
       HERO — Design A: Full-Width Background Image
       Cinematic hero with dark overlay and centred text
       ═══════════════════════════════════════════════ -->
  ```
- Grid system: `.container` (max-width 1200px) / `.row` (flexbox) / `.col` with responsive column classes (`col-lg-*`, `col-md-*`, `col-sm-*`)
- Images reference `../../website/images/` with descriptive `alt` text
- Semantic heading hierarchy: one `h1` in hero, `h2` per section, `h3` for cards/items
- `loading="lazy"` on images below the fold

**Accessibility**:
- `aria-label` on all `<section>` and `<nav>` elements
- Proper heading hierarchy (h1 → h2 → h3)
- Descriptive `alt` text on all images
- `aria-label` on CTA links/buttons
- Skip-to-content link (hidden, visible on focus)

**Footer**:
- `<footer>` with 4-column grid
- `{client.name}` copyright with current year
- "Website by {agency.name}" credit line

#### `designs/design-{key}/styles.css`

Complete stylesheet (~600+ lines). Requirements:

**Header comment**:
```css
/* ═══════════════════════════════════════════════════════════════
   {client.name} — Design {KEY}: "{designs[].name}"
   Mood: {designs[].mood}
   Inspiration: [notes from research/references]
   ═══════════════════════════════════════════════════════════════ */
```

For the wildcard, replace `Mood:` with `Wildcard — inspired by:` and list the key reference sources:
```css
/* ═══════════════════════════════════════════════════════════════
   {client.name} — Design D: "{derived name}" ✦ WILDCARD
   Wildcard — inspired by: [Dribbble shot X, Webflow template Y, ...]
   Approach: [what makes this different from A/B/C]
   ═══════════════════════════════════════════════════════════════ */
```

**Section 1 — CSS Custom Properties** (`:root`):
- Brand colours with `--{slug}-` prefix:
  - If `designs[].palette` is set, use its values (`primary`, `accent`, `accent_hover`, `background`, `surface`)
  - If `designs[].palette` is null, use `brand.colors.*` values
- Functional colour aliases: `--{slug}-text`, `--{slug}-text-muted`, `--{slug}-border`, `--{slug}-border-strong`
- Hover/derived states
- Typography variables: `--{slug}-font-heading`, `--{slug}-font-body`, tracking, weight
- Spacing scale: `--sp-4` through `--sp-80`, plus design-specific extended values if needed
- Border radius tokens: `--r-none`, `--r-sm`, `--r-md`, `--r-lg` (values vary per design mood)
- Transition base: `--transition-base: 0.25s ease`
- Design-specific variables (e.g., hero overlay colour, hero min-height)

**Section 2 — Base**:
- CSS reset (`box-sizing`, margin/padding reset)
- Body styles using custom properties
- `.page-wrapper` flex column layout
- `.page-main` flex: 1
- `.section` padding using spacing scale
- `.container` max-width 1200px, auto margins, horizontal padding
- `.row` flexbox with negative margin gutter
- `.col` system: `-lg-*` (desktop), `-md-*` (tablet), `-sm-*` (mobile), `-shrink` (auto width)
- Row modifiers: `row-align-center`, `row-justify-center`, `row-justify-between`, `row-gap-sm`

**Section 3 — Typography**:
- Heading classes: `.h1` through `.h4` using heading font
- `.paragraph-sm`, `.paragraph-lg`, `.paragraph-xl`
- `.eyebrow` — small uppercase label
- Link styles

**Section 4 — Buttons**:
- `.btn` base with transition
- Modifier classes: `.cc-primary`, `.cc-light`, `.cc-outline`, `.cc-outline-light`
- Hover and focus states

**Section 5 — Navigation**:
- Nav layout matching the design's chosen nav style
- Logo text styling
- Nav link styles with hover
- Mobile nav: hidden checkbox input, toggle bars, slide/fade menu
- Desktop/mobile visibility utilities: `.u-sm-d-none`, `.u-d-none`, `.u-sm-d-block`

**Section 6 — Back link**:
- `.back-link` — small, muted, positioned above nav

**Sections 7-12 — Component styles**:
- Hero (background, overlay, content layout — unique per design)
- Services cards (layout, image treatment, hover states)
- About (image/text split, stat blocks)
- Testimonials (quote styling, author, pagination if applicable)
- CTA section (background, button placement)
- Footer (column grid, link styles, copyright)

**Section 13 — Media queries**:
- `@media (max-width: 992px)` — tablet adjustments, column overrides
- `@media (max-width: 767px)` — mobile layout, stacked columns, reduced spacing, mobile nav active
- `@media (max-width: 477px)` — small mobile fine-tuning, font size reductions

### 7. Update designs hub

The `designs/index.html` hub (created by `/scaffold`) links to the 3 standard directions. After generating Design D, append a 4th card to the hub with a subtle "Wildcard" badge. The badge should be a small styled label (e.g., uppercase, accent background, small font) next to or below the direction name — making it clear this is the intentionally different option without being visually dominant.

If the wildcard was skipped (empty references), leave the hub unchanged at 3 cards.

### 8. Verify output

After generating all files, confirm:
- [ ] Each design has both `index.html` and `styles.css` in `designs/design-{key}/`
- [ ] All 4 directions generated (3 standard + wildcard), or 3 if wildcard references were empty
- [ ] All client values pulled from `project.json` — zero hardcoded names, colours, or contact details
- [ ] CSS prefix uses `{client.slug}` throughout (e.g., `--marr-primary`)
- [ ] Each design is self-contained (own HTML + own CSS, no shared dependencies)
- [ ] Designs are visually distinct — different nav style, hero layout, service presentation, spacing
- [ ] Wildcard feels like a different design universe from the 3 standard directions
- [ ] Same content (copy) across all 4 directions
- [ ] Images reference `../../website/images/` with descriptive alt text
- [ ] CSS-only mobile nav works (checkbox toggle, no JavaScript)
- [ ] Responsive at 992px, 767px, 477px breakpoints
- [ ] `designs[].palette` used where set, `brand.colors` used where palette is null
- [ ] Testimonials clearly marked as placeholders
- [ ] Back-link to `../index.html` present on each page
- [ ] Heading hierarchy correct (one h1, h2 per section, h3 for items)
- [ ] Designs hub updated with wildcard card + badge

## Important
- ALL values come from `project.json` — no hardcoded client data
- CSS variable prefix uses `client.slug` (e.g., `--marr-primary` for slug "marr")
- Each design must be fully self-contained: own HTML + own CSS, no shared stylesheet
- Designs must be **visually distinct** — different layouts, structural choices, and spatial treatment, not just colour or font swaps
- The wildcard must feel like it comes from a **different design universe** — not a 4th variation on the same themes
- Same content across all directions — the client compares visual treatment, not copy
- Images reference `../../website/images/` (shared local files from website directory)
- Production-quality code, not scaffolding or stubs — match MARR Laser design direction quality
- Responsive at 992px, 767px, 477px breakpoints
- No JavaScript — CSS-only mobile nav using checkbox toggle pattern
- If `designs[].palette` is set, use it for that direction's colours; if null, fall back to `brand.colors`
- Wildcard palette: derive from curated references; use a 4th `designs[]` palette entry if present, otherwise extract from reference aesthetics, falling back to `brand.colors` only as last resort
- Copy must be industry-specific and professional — not lorem ipsum or generic filler
- Placeholder testimonials must be clearly marked with HTML comments
- Direction references empty in `references.md` → proceed with Perplexity research alone for A/B/C
- Wildcard references empty in `references.md` → skip Design D, warn user, generate only A/B/C
- Grid system uses `.container` / `.row` / `.col` pattern with responsive column classes
- HTML comments use box-drawing characters for section dividers (matching MARR pattern)
- Footer includes "Website by {agency.name}" credit
- Designs hub gets a 4th card with "Wildcard" badge when Design D is generated
