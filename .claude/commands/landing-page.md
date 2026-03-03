# /landing-page — Generate service/campaign landing page

Read `project.json` and generate a single-page landing for a specific service or campaign, built as self-contained section blocks for Webflow embeds.

## Usage

The user specifies which service or campaign the landing page is for:
- `/landing-page laser hair removal`
- `/landing-page summer promotion`
- `/landing-page [service name]`

If no service is specified, ask the user what the landing page should focus on.

## Steps

### 1. Read project.json
Extract:
- `client.name`, `client.short_name`, `client.tagline` — for page headings and copy
- `client.slug` — for CSS variable prefixes and BEM naming
- `client.industry`, `client.location`, `client.phone`, `client.email` — for CTAs and local context
- `brand.colors.*` — for section styling
- `brand.fonts.*` — for typography
- `agency.name` — for attribution comment in code

### 2. Plan landing page content

Based on the specified service/campaign and client industry, plan:
- Hero headline and sub-headline
- Key benefits (3-5 points)
- Service/product details
- Social proof approach (testimonials, reviews, stats)
- FAQ topics (5-8 questions)
- CTA strategy (primary and secondary calls to action)
- Visual section flow

### 3. Generate landing page files

#### Main page
**File**: `landing/index.html`

Complete landing page that includes all sections inline. Requirements:
- Title: `{client.name} — {service/campaign name}`
- Load Google Fonts from `brand.fonts.google_fonts_url`
- Link to `styles.css` for shared base styles
- Include all section HTML in order
- Responsive: 1200px, 991px, 767px, 478px breakpoints
- Images reference `../website/images/` (shared local files)

#### Shared styles
**File**: `landing/styles.css`

Base styles for the landing page:
- CSS custom properties from brand tokens with `--{slug}-` prefix
- Base reset and typography
- Shared responsive utilities
- Print styles

#### Section blocks
**Directory**: `landing/sections/`

Each section is a self-contained HTML file with its own `<style>` block — designed for independent Webflow custom code embeds. Generate these files:

**`01-header.html`** — Navigation bar
- Client logo placeholder
- Minimal nav (service name, CTA button)
- Sticky on scroll
- BEM: `{slug}-header`, `{slug}-header__logo`, `{slug}-header__cta`

**`02-hero.html`** — Hero section
- Large headline about the service
- Supporting sub-headline
- Primary CTA button
- Hero image placeholder
- BEM: `{slug}-hero`, `{slug}-hero__title`, `{slug}-hero__cta`

**`03-trust-bar.html`** — Trust indicators
- "As seen in" / certification badges / trust signals
- Placeholder slots for client-provided trust assets
- BEM: `{slug}-trust`

**`04-benefits.html`** — Key benefits
- 3-5 benefit cards with icon placeholders
- Benefit headline + short description
- BEM: `{slug}-benefits`, `{slug}-benefits__card`

**`05-about-service.html`** — Service details
- What the service involves
- Process steps or methodology
- Image placeholder
- BEM: `{slug}-service`

**`06-results.html`** — Results/outcomes
- Before/after or results showcase
- Statistics or metrics
- Image placeholders
- BEM: `{slug}-results`

**`07-testimonials.html`** — Social proof
- 2-3 testimonial cards with placeholder quotes
- Client name, treatment/service type
- Star ratings
- BEM: `{slug}-testimonials`, `{slug}-testimonials__card`

**`08-pricing.html`** — Pricing/packages
- 2-3 pricing tiers or service packages
- Feature lists per tier
- CTA per tier
- BEM: `{slug}-pricing`, `{slug}-pricing__tier`

**`09-process.html`** — How it works
- 3-4 step process
- Step number, title, description
- Visual connection between steps
- BEM: `{slug}-process`, `{slug}-process__step`

**`10-faq.html`** — Frequently asked questions
- 5-8 accordion-style FAQs
- Relevant to the specific service
- Pure CSS accordion (no JS)
- BEM: `{slug}-faq`, `{slug}-faq__item`

**`11-gallery.html`** — Image gallery
- Grid of image placeholders
- Lightbox optional (CSS-only)
- BEM: `{slug}-gallery`

**`12-cta-banner.html`** — Mid-page CTA
- Bold call-to-action banner
- Phone number and booking button
- BEM: `{slug}-cta-banner`

**`13-map-contact.html`** — Location/contact
- Embedded map placeholder
- Address, phone, email from config
- Opening hours placeholder
- BEM: `{slug}-map`

**`14-footer-cta.html`** — Footer with final CTA
- Final call to action
- Contact details from config
- Links placeholder
- BEM: `{slug}-footer`

### 4. Generate asset brief addendum

**File**: `landing/client-asset-brief.md`

Checklist of assets needed specifically for the landing page:
- Hero image (recommended dimensions)
- Benefit icons or illustrations
- Before/after photos (if applicable)
- Testimonial quotes with client names
- Trust badges / certifications
- Gallery images
- Pricing details
- FAQ answers (confirm/expand the drafted ones)

## Important
- ALL values come from `project.json` — no hardcoded client data
- BEM naming with `{client.slug}-` prefix throughout (e.g., `marr-hero__title`)
- Each section file must be self-contained: own `<style>` block, can be pasted into Webflow independently
- Responsive breakpoints: 1200px, 991px, 767px, 478px
- Images reference `../website/images/` (shared local files)
- CSS custom properties use `--{slug}-` prefix
- Write compelling, industry-appropriate copy — not lorem ipsum
- Copy should be specific to the service/campaign, not generic
- All sections should work independently but also flow together as a complete page
- Match the code quality from the MARR Laser landing page
- Include HTML comments at the top of each section file: `<!-- Section: {name} | {client.name} Landing Page -->`
