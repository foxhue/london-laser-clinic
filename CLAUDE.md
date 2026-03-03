# London Laser Clinic — Foxhue Studio Project

## Overview
Website project for London Laser Clinic, built using the Foxhue Studio template.

**GitHub Pages**: https://foxhue.github.io/london-laser-clinic/
**Design Hub**: https://foxhue.github.io/london-laser-clinic/designs/
**Layout Variants**: https://foxhue.github.io/london-laser-clinic/website/variants/

## Repo Structure
```
london-laser-clinic/
├── CLAUDE.md
├── project.json              ← client config
├── .gitignore
├── .claude/commands/
│   ├── scaffold.md
│   ├── seo-report.md
│   ├── social-audit.md
│   ├── creative-process.md
│   └── landing-page.md
├── index.html                ← Foxhue Project Hub (4-card layout)
├── designs/
│   ├── index.html            ← design direction hub
│   ├── styles.css            ← shared design styles
│   ├── design-a/
│   ├── design-b/
│   └── design-c/
├── website/
│   ├── styles.css            ← brand tokens stylesheet
│   ├── images/
│   └── variants/
│       ├── index.html        ← client review hub
│       └── thank-you.html    ← form confirmation
├── docs/
│   ├── client-asset-brief.md
│   ├── project-status.md
│   ├── creative-process.html
│   └── seo-competitor-report.html
└── inspiration/
    └── references.md
```

## Brand Tokens
| Token | Value |
|-------|-------|
| Primary | `#333333` |
| Accent | `#888888` |
| Accent hover | `#666666` |
| Background | `#F5F5F5` |
| Surface | `#E0E0E0` |
| Heading font | Cormorant Garamond, serif |
| Body font | Noto Sans, sans-serif |

```css
--london-laser-clinic-primary: #333333;
--london-laser-clinic-accent: #888888;
--london-laser-clinic-accent-hover: #666666;
--london-laser-clinic-bg: #F5F5F5;
--london-laser-clinic-surface: #E0E0E0;
--london-laser-clinic-text: #333333;
--london-laser-clinic-light: #ffffff;
--london-laser-clinic-font-heading: 'Cormorant Garamond', serif;
--london-laser-clinic-font-body: 'Noto Sans', sans-serif;
```

### Font Loading
```html
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:wght@300;400;500;600&family=Noto+Sans:wght@300;400;500;600&display=swap" rel="stylesheet">
```

## Client Details
- **Name**: London Laser Clinic
- **Location**: London (7 locations)
- **Phone**: 07503 834611
- **Website**: http://www.londonlaser.co.uk/
- **Google Business**: https://maps.google.com/?cid=3775228527920774244

## Pages
| Key | Title | Slug |
|-----|-------|------|
| homepage | Homepage | index |
| about | About | about |
| contact | Contact | contact |

## Deliverables
| Deliverable | Enabled |
|------------|---------|
| SEO Report | Yes |
| Creative Process | Yes |
| Social Audit | No |
| Landing Page | No |

## Commands
- `/scaffold` — Generate project infrastructure from project.json
- `/seo-report` — Research competitors and generate SEO report
- `/creative-process` — Generate client-facing creative process page
- `/social-audit` — Social media landscape analysis (disabled)
- `/landing-page {service}` — Campaign landing page (disabled)
- `/brand-palette` — Explore and generate brand color palette options
- `/design-directions` — Generate design direction concepts for client review
## Architecture Notes
- All generated files read from `project.json`
- CSS variable prefix: `--london-laser-clinic-`
- Review hub uses AJAX form submission via Formsubmit.co
- Website breakpoints: 992px, 767px, 477px
- Deploy to GitHub Pages from `main` branch
