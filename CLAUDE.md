# CLAUDE.md

> Project context file for Claude Code. Keep this file updated as the project evolves.

---

## 0. Agent Workflow (MANDATORY — READ FIRST)

**Every request on this codebase MUST be executed through the agent chain. The main thread is a router and orchestrator only — it does NOT write code, edit files, or run tests directly for any task that touches the project domain.**

### The Locked Agent Chain

```
developer → frontend (if UI work) → qa → reviewer
```

This chain is non-negotiable. The main thread's job is to:

1. Identify the request type and entry agent
2. Delegate via the `Agent` tool with full context
3. Hand off between agents in the correct order
4. Surface the final reviewer summary back to the user

### Entry Agent Selection

| Request type | Entry agent |
|---|---|
| Any data file / TypeScript content / SEO logic / sitemap / robots / metadata / JSON-LD / structured data / analytics setup | `developer` |
| Frontend-only UI / React component / Next.js page / Tailwind / layout / accessibility / animation / breadcrumbs (no data change needed) | `frontend` |
| Writing or auditing tests for an existing feature | `qa` |
| Final review of completed work | `reviewer` |
| Commit and push completed, reviewed work | `git-commit-push` |
| Codebase exploration / research-only questions (no code change) | `Explore` |
| Implementation planning before a large change | `Plan` |

If the request involves both data and UI, **always start with `developer`** — `developer` will hand off to `frontend` when UI work is required.

### Mandatory Handoff Order

1. **`developer`** scaffolds/modifies data files, TypeScript types, SEO metadata, sitemap, robots, JSON-LD, API routes, or any non-UI logic.
2. **`frontend`** is invoked by `developer` (or main thread on UI-only work) when Next.js pages or React components are needed.
3. **`qa`** is invoked after every code change — writes/updates tests, runs targeted tests, never the full suite unless required.
4. **`reviewer`** is the final gate — performs senior-level review against the original requirement, delegates fixes back to `developer` / `frontend` if issues are found, and prints the formatted delivery summary.
5. **`git-commit-push`** runs only after `reviewer` approves AND the user explicitly asks to commit.

Skipping `qa` or `reviewer` is forbidden. Even for trivial changes, `qa` confirms correctness and `reviewer` confirms requirement match.

### When the Main Thread May Act Directly

The main thread may act WITHOUT delegating only for:

- Reading files purely to answer a user question (no code change)
- Updating `CLAUDE.md`, `MEMORY.md`, or other meta/config files
- Trivial single-line edits to non-domain files (typos, comments, formatting) where the agent chain clearly does not apply

For everything else, delegate. When in doubt, delegate.

---

## 1. Project Overview

**Name:** Hiran Nuwanpriya Portfolio
**URL:** https://hirannuwanpriya.com
**Type:** SEO-first professional portfolio website for a senior full stack software engineer.
**Goal:** Attract senior engineering job opportunities in Australia and New Zealand by showcasing real project delivery, technical depth, measurable outcomes, and professional credibility.

**Primary traffic source:** Organic SEO + direct recruiter / hiring manager visits.
**Primary audience:**
- Australian and New Zealand recruiters
- Hiring managers and software engineering managers
- CTOs and startup founders
- Technical leads looking for senior engineers

**Secondary audience:**
- Freelance clients
- SaaS founders needing contract development support
- Agencies needing Laravel / React support

**Target roles:**
- Senior Full Stack Engineer
- Senior Software Engineer
- Laravel Developer / PHP Developer
- React Developer / Vue.js Developer
- SaaS Developer
- Technical Lead
- Remote Full Stack Developer

---

## 2. Tech Stack

### Core Stack

| Area | Technology |
|---|---|
| Framework | Next.js (App Router) |
| Language | TypeScript |
| UI Library | React |
| Styling | Tailwind CSS v4 |
| Hosting | Vercel |
| Source Control | GitHub |
| Content | Static TypeScript data files |
| Analytics | Vercel Web Analytics + Google Analytics 4 |
| Performance | Vercel Speed Insights |
| SEO | Next.js Metadata API, sitemap.ts, robots.ts, JSON-LD structured data |

### Package Versions (keep current)

- next — latest stable
- react — v19
- typescript — latest stable
- tailwindcss — v4
- @vercel/analytics
- @vercel/speed-insights
- eslint — v9
- prettier — v3

### Why This Stack

Next.js App Router with TypeScript supports:
- SEO-friendly server-side rendering and static generation
- Metadata API for per-page SEO titles, descriptions, and Open Graph
- Built-in sitemap.ts and robots.ts generation
- JSON-LD structured data via server components
- Fast Core Web Vitals out of the box
- Seamless Vercel deployment with automatic GitHub integration

---

## 3. Brand Positioning

### Main Positioning Statement

> Senior Full Stack Engineer and Laravel Specialist based in Australia, building scalable SaaS platforms, enterprise systems, APIs, eCommerce solutions, and high-performance web applications using Laravel, React, Vue, TypeScript, DevOps, and AI-assisted engineering workflows.

### Short Tagline (use on hero and meta)

**Senior Full Stack Engineer | Laravel, React, Vue & SaaS Specialist**

### Professional Identity

Present Hiran as:
- Senior full stack software engineer with 12+ years of experience
- Laravel and PHP specialist
- React, Vue, and TypeScript-capable frontend developer
- SaaS and enterprise application developer
- Technical lead and mentor
- Developer with international client experience (Europe, USA, Australia)
- Performance-focused and business-aware engineer
- Remote-ready, based in Hobart, Tasmania, Australia

---

## 4. SEO Strategy

### Primary Keywords

- Senior Full Stack Engineer Australia
- Laravel Developer Australia
- Laravel Developer Hobart
- Full Stack Developer Hobart
- React Developer Australia
- Vue Developer Australia
- SaaS Developer Australia
- PHP Developer Australia
- Technical Lead Software Engineer Australia
- Remote Full Stack Developer Australia
- Full Stack Engineer New Zealand
- Laravel React Developer

### Secondary Keywords

- Laravel SaaS developer
- Laravel performance optimisation
- Laravel enterprise application developer
- Laravel API developer
- React Native mobile app developer
- Vue.js Laravel developer
- Docker Laravel deployment
- Redis Laravel performance
- Laravel Nova developer
- Laravel Livewire developer
- AI-assisted software development
- software engineering portfolio Australia

### Location Keywords (use naturally, not excessively)

Australia, New Zealand, Hobart, Tasmania, Remote, Hybrid

---

## 5. Site Structure

```
/
├── about
├── skills
├── experience
├── projects
│   ├── booknordics-travel-booking-platform
│   ├── promsoc-brussels-education-platform
│   ├── werenewsneakers-ecommerce-mobile-app
│   ├── brusselslife-lifestyle-platform
│   └── irisnet-customer-care-billing-portal
├── services
├── blog
│   ├── laravel-performance-optimisation
│   ├── building-scalable-saas-platforms-with-laravel
│   └── ai-assisted-software-development
├── resume
└── contact
```

---

## 6. Folder Structure

```
hiran-portfolio/
├── app/
│   ├── layout.tsx                    # Root layout with Analytics, SpeedInsights, JSON-LD Person schema
│   ├── page.tsx                      # Homepage
│   ├── globals.css
│   ├── about/
│   │   └── page.tsx
│   ├── skills/
│   │   └── page.tsx
│   ├── experience/
│   │   └── page.tsx
│   ├── projects/
│   │   ├── page.tsx
│   │   └── [slug]/
│   │       └── page.tsx
│   ├── blog/
│   │   ├── page.tsx
│   │   └── [slug]/
│   │       └── page.tsx
│   ├── services/
│   │   └── page.tsx
│   ├── resume/
│   │   └── page.tsx
│   ├── contact/
│   │   └── page.tsx
│   ├── sitemap.ts
│   └── robots.ts
├── components/
│   ├── layout/
│   │   ├── Header.tsx
│   │   ├── Footer.tsx
│   │   └── MobileNav.tsx
│   ├── sections/
│   │   ├── Hero.tsx
│   │   ├── ProofCards.tsx
│   │   ├── AboutSummary.tsx
│   │   ├── SkillsGrid.tsx
│   │   ├── FeaturedProjects.tsx
│   │   ├── ResultsImpact.tsx
│   │   ├── BlogPreview.tsx
│   │   └── ContactCTA.tsx
│   ├── ui/
│   │   ├── Button.tsx
│   │   ├── Card.tsx
│   │   ├── Badge.tsx
│   │   ├── Container.tsx
│   │   ├── SectionHeading.tsx
│   │   ├── MetricCard.tsx
│   │   └── ProjectCard.tsx
│   └── seo/
│       ├── JsonLd.tsx
│       └── BreadcrumbJsonLd.tsx
├── data/
│   ├── profile.ts
│   ├── skills.ts
│   ├── experience.ts
│   ├── projects.ts
│   └── blog.ts
├── public/
│   ├── images/
│   │   ├── profile/
│   │   ├── projects/
│   │   └── og/
│   ├── resume/
│   │   └── hiran-nuwanpriya-resume.pdf
│   └── favicon.ico
├── types/
│   └── index.ts                      # Shared TypeScript interfaces
├── package.json
├── next.config.ts
├── tsconfig.json
├── tailwind.config.ts
└── README.md
```

---

## 7. Data Files

All content lives in `/data/` as TypeScript files. Never hardcode content in components. Always import from data files.

### `data/profile.ts`

```ts
export const profile = {
  name: "Hiran Nuwanpriya",
  title: "Senior Full Stack Engineer & Laravel Specialist",
  location: "Hobart, Tasmania, Australia",
  availability: "Open to remote roles and periodic on-site travel",
  email: "hirannuwanpriya@gmail.com",
  phone: "+61 478 001 862",
  linkedin: "https://www.linkedin.com/in/hirannuwanpriya/",
  github: "https://github.com/Hirannuwanpriya",
  summary:
    "Senior Full Stack Engineer and Technical Lead with 12+ years of experience building scalable SaaS, enterprise, eCommerce, API and mobile software solutions using Laravel, React, Vue, TypeScript and DevOps workflows.",
};
```

### `data/projects.ts`

Each project must include: `slug`, `title`, `subtitle`, `industry`, `client`, `region`, `role`, `duration`, `teamSize`, `stack`, `overview`, `problem`, `solution`, `keyFeatures`, `contribution`, `results`, `challenges`, `demonstrates`.

The five projects are:

1. **booknordics-travel-booking-platform** — Travel & Activities Booking Platform (Norway, Laravel + Statamic)
2. **promsoc-brussels-education-platform** — Adult Education Portal (Belgium, Laravel 9 + Nova + Livewire)
3. **werenewsneakers-ecommerce-mobile-app** — eCommerce Web & Mobile App (Belgium, Laravel 9 + React Native)
4. **brusselslife-lifestyle-platform** — Lifestyle Magazine Platform (Belgium, Laravel + Horizon)
5. **irisnet-customer-care-billing-portal** — Customer Care & Billing Portal (Belgium, CakePHP + SSO)

### `data/skills.ts`

Group skills into: Backend Engineering, Frontend Engineering, Database & Search, DevOps & Cloud, Mobile Development, Engineering Leadership.

### `data/experience.ts`

Work history in reverse chronological order:

1. Creative Software | Sri Lanka | 2025–present | Associate Technical Lead / Full Stack Engineer
2. BWS Brussels / Eurokom SPRL | Belgium | 2023–2025 | Team Lead / Full Stack Developer
3. Adlux Software (Pvt) Ltd | 2020–2023 | Senior Software Engineer / Full Stack Developer
4. Itelligence Services (Pvt) Ltd | 2017–2020 | Senior Software Engineer / Full Stack Developer
5. 247Techies (Pvt) Ltd | 2015–2017 | Software Engineer
6. Fidenz.com (Pvt) Ltd | 2013–2015 | Associate Software Engineer

### `data/blog.ts`

Initial blog articles (content can be stub or full MDX-ready):

1. `laravel-performance-optimisation` — How I Optimise Laravel Applications for Performance
2. `building-scalable-saas-platforms-with-laravel` — Building Scalable SaaS Platforms with Laravel, Redis and Queues
3. `ai-assisted-software-development` — How AI-Assisted Development Improves Software Delivery

---

## 8. Homepage Structure

The homepage (`app/page.tsx`) must include these sections in order:

### Section 1: Hero
- **H1:** Senior Full Stack Engineer & Laravel Specialist in Australia
- **Subheading:** I build scalable SaaS platforms, enterprise web applications, APIs, eCommerce systems, and mobile solutions using Laravel, React, Vue, TypeScript, Docker, DevOps, and AI-assisted engineering workflows.
- **CTA Buttons:** View My Projects · Download Resume · Contact Me

### Section 2: Proof Cards (4–6 cards)
- 12+ Years Software Engineering Experience
- Laravel, React, Vue & TypeScript
- SaaS, ERP, CRM, LMS & eCommerce Systems
- MSc in Software Engineering
- International Client Experience
- Team Lead & Mentor

### Section 3: About Summary
Brief paragraph positioning Hiran as a senior full stack engineer across travel, healthcare, education, eCommerce, and telecom industries.

### Section 4: Core Skills
Grouped skill badges by category (see `data/skills.ts`).

### Section 5: Featured Projects
5 project cards using `ProjectCard` component with: name, industry, summary, tech stack badges, key result, link to case study.

### Section 6: Results & Impact
Metric cards using real numbers from the CV:
- 66% reduction in website load time (12s → 4s)
- 50%+ improvement in response times
- 99.9% uptime maintained
- 50% reduction in time-to-market
- 30% improvement in operational efficiency
- 10,000+ user accounts and product records supported
- ~40% backend load time improvement
- ~30% increase in session duration
- ~25% reduction in bounce rate

### Section 7: Blog Preview
3 article cards linking to full blog posts.

### Section 8: Contact CTA
Headline + buttons: Contact Me · LinkedIn · GitHub · Download Resume

---

## 9. Project Case Study Page Structure

Each `app/projects/[slug]/page.tsx` must follow this structure:

```
Project Title
Industry & Client / Region
Role · Duration · Team Size
Technology Stack (badges)
Project Overview
Problem
Solution
Key Features
Technical Contribution
Performance / Business Impact (metric cards)
Challenges Solved
What This Project Demonstrates
Call to Action (Contact Me / View Other Projects)
```

---

## 10. SEO Rules

**Every page must have:**
- One clear H1
- Unique `metadata` export with `title`, `description`, `keywords`, `openGraph`, `twitter`
- `<link rel="canonical">` (use Next.js canonical metadata)
- Breadcrumb JSON-LD on all nested pages
- Correct heading hierarchy (H1 → H2 → H3, no skipping)
- Alt text on all meaningful images
- Internal links to related pages

**Homepage metadata example:**

```ts
export const metadata: Metadata = {
  title: "Senior Full Stack Engineer Australia | Laravel, React, Vue & SaaS Developer",
  description:
    "Senior Full Stack Engineer based in Australia with 12+ years of experience building Laravel, React, Vue, SaaS, eCommerce, enterprise, API and mobile solutions.",
  keywords: [
    "Senior Full Stack Engineer Australia",
    "Laravel Developer Australia",
    "React Developer Australia",
    "Vue Developer Australia",
    "SaaS Developer Australia",
    "Full Stack Developer Hobart",
    "Technical Lead Software Engineer",
  ],
  openGraph: {
    title: "Hiran Nuwanpriya | Senior Full Stack Engineer",
    description:
      "Laravel, React, Vue and SaaS specialist building scalable software solutions for international clients.",
    url: "https://hirannuwanpriya.com",
    siteName: "Hiran Nuwanpriya Portfolio",
    images: [
      {
        url: "https://hirannuwanpriya.com/og-image.jpg",
        width: 1200,
        height: 630,
        alt: "Hiran Nuwanpriya Senior Full Stack Engineer Portfolio",
      },
    ],
    locale: "en_AU",
    type: "website",
  },
};
```

---

## 11. JSON-LD Structured Data

Use JSON-LD via server components for all schema types. Never use client-side injection for structured data.

### Person Schema (homepage + about page)

```json
{
  "@context": "https://schema.org",
  "@type": "Person",
  "name": "Hiran Nuwanpriya",
  "jobTitle": "Senior Full Stack Engineer",
  "url": "https://hirannuwanpriya.com",
  "sameAs": [
    "https://www.linkedin.com/in/hirannuwanpriya/",
    "https://github.com/Hirannuwanpriya"
  ],
  "address": {
    "@type": "PostalAddress",
    "addressLocality": "Hobart",
    "addressRegion": "Tasmania",
    "addressCountry": "Australia"
  },
  "knowsAbout": [
    "Laravel", "PHP", "React", "Vue.js", "TypeScript",
    "SaaS Development", "Enterprise Software", "DevOps", "API Development"
  ]
}
```

Also implement:
- **WebSite** schema on all major pages
- **Article** schema on all blog posts
- **BreadcrumbList** schema on all project and blog pages

---

## 12. Sitemap

`app/sitemap.ts` must include all static routes plus dynamic project and blog slugs from data files:

```ts
import type { MetadataRoute } from "next";
import { projects } from "@/data/projects";
import { blog } from "@/data/blog";

const siteUrl = process.env.NEXT_PUBLIC_SITE_URL || "https://hirannuwanpriya.com";

export default function sitemap(): MetadataRoute.Sitemap {
  const staticRoutes = [
    "", "/about", "/skills", "/experience",
    "/projects", "/services", "/blog", "/resume", "/contact",
  ];

  const projectRoutes = projects.map((p) => ({
    url: `${siteUrl}/projects/${p.slug}`,
    lastModified: new Date(),
    changeFrequency: "monthly" as const,
    priority: 0.9,
  }));

  const blogRoutes = blog.map((b) => ({
    url: `${siteUrl}/blog/${b.slug}`,
    lastModified: new Date(),
    changeFrequency: "monthly" as const,
    priority: 0.8,
  }));

  return [
    ...staticRoutes.map((route) => ({
      url: `${siteUrl}${route}`,
      lastModified: new Date(),
      changeFrequency: "monthly" as const,
      priority: route === "" ? 1 : 0.8,
    })),
    ...projectRoutes,
    ...blogRoutes,
  ];
}
```

---

## 13. Robots

`app/robots.ts`:

```ts
import type { MetadataRoute } from "next";

const siteUrl = process.env.NEXT_PUBLIC_SITE_URL || "https://hirannuwanpriya.com";

export default function robots(): MetadataRoute.Robots {
  return {
    rules: { userAgent: "*", allow: "/" },
    sitemap: `${siteUrl}/sitemap.xml`,
  };
}
```

---

## 14. Analytics Setup

### `app/layout.tsx`

```tsx
import { Analytics } from "@vercel/analytics/react";
import { SpeedInsights } from "@vercel/speed-insights/next";

export default function RootLayout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="en-AU">
      <body>
        {children}
        <Analytics />
        <SpeedInsights />
      </body>
    </html>
  );
}
```

### Environment Variables

```
NEXT_PUBLIC_SITE_URL=https://hirannuwanpriya.com
NEXT_PUBLIC_GA_ID=G-XXXXXXXXXX
```

---

## 15. Design System

> **Source of truth:** Brand Guidelines (brand_guideline.png). Every agent working on UI must follow this section exactly. Do not deviate from these values.

---

### 15.1 Brand Essence

The portfolio communicates these qualities in every design decision:

| Trait | Application |
|---|---|
| **Minimal** | Generous whitespace, no clutter, purposeful elements only |
| **Editorial** | Strong typographic hierarchy, magazine-quality layout rhythm |
| **Modern** | Clean geometry, sharp lines, contemporary spatial composition |
| **Confident** | Bold headlines, direct copy, no hedging or over-decoration |
| **Creative** | Unexpected layout moments, selective use of accent colour |
| **Premium** | Refined spacing, careful kerning, high-contrast card surfaces |

---

### 15.2 Colour Palette

Define these as CSS custom properties in `app/globals.css`. Use variable names consistently across all components — never hardcode hex values in components.

```css
:root {
  /* Primary & Neutrals */
  --color-deep-blue: #355CFF;       /* Primary action, CTAs, active states */
  --color-soft-blue: #AFC4FF;       /* Hover states, subtle highlights, tints */
  --color-charcoal: #161616;        /* Primary text, headings, dark surfaces */
  --color-warm-white: #F7F6F2;      /* Page background, section backgrounds */
  --color-cool-gray: #D0DCE3;       /* Borders, dividers, hairlines, card borders */
  --color-black: #000000;           /* Maximum contrast text, footer background */

  /* Accent Colors — use sparingly, one per page section maximum */
  --color-accent-yellow: #FFC83D;   /* Highlights, tags, small decorative marks */
  --color-accent-purple: #8B5CF6;   /* Secondary accent, skill category labels */
  --color-accent-green: #22C55E;    /* Success states, availability indicators */
  --color-accent-red: #EF4444;      /* Error states, urgent callouts only */

  /* Semantic Aliases */
  --color-bg: var(--color-warm-white);
  --color-bg-card: #FFFFFF;
  --color-text-primary: var(--color-charcoal);
  --color-text-secondary: #6B7280;
  --color-text-muted: #9CA3AF;
  --color-border: var(--color-cool-gray);
  --color-cta-bg: var(--color-deep-blue);
  --color-cta-text: #FFFFFF;
  --color-cta-hover-bg: #2347E8;
}
```

**Colour usage rules:**
- Page background: `--color-warm-white` (`#F7F6F2`) — **light theme, not dark**
- Primary headings and body text: `--color-charcoal` (`#161616`)
- All interactive CTAs and primary buttons: `--color-deep-blue` (`#355CFF`)
- Borders, dividers, hairlines: `--color-cool-gray` (`#D0DCE3`)
- Footer background: `--color-black` (`#000000`) with white text
- Accent colours are decorative only — dots, tags, small icons — never backgrounds of large areas

---

### 15.3 Typography

Install both fonts via Google Fonts or a self-hosted font loader in `app/layout.tsx`.

```
Playfair Display — Display headings (H1 only)
Satoshi — All other text (H2–H6, body, buttons, captions, labels)
```

#### Type Scale

| Element | Font | Weight | Size | Tracking | Line Height |
|---|---|---|---|---|---|
| **H1** | Playfair Display | Bold (700) | 72px | -1% | 1.1 |
| **H2** | Satoshi | Medium (500) | 36px | 0% | 1.2 |
| **Body** | Satoshi | Regular (400) | 16px | 0% | 1.7 |
| **Caption** | Satoshi | Regular (400) | 12px | 0% | 1.6 |
| **Button** | Satoshi | Medium (500) | 14px | +0.5px | — |

#### Tailwind font config (`tailwind.config.ts`)

```ts
fontFamily: {
  display: ['"Playfair Display"', 'Georgia', 'serif'],
  sans: ['Satoshi', 'Inter', 'system-ui', 'sans-serif'],
},
```

#### Font usage rules

- **H1 only** uses Playfair Display. Every other text element uses Satoshi.
- Never use Inter, Roboto, Arial, or system-ui as a primary font — Satoshi is always the fallback before system fonts.
- Maintain the exact size and tracking values from the scale above.
- Body text line-height must be 1.7 for readability.

---

### 15.4 Layout System

#### Grid
- **12-column grid** on desktop
- Full-width single column on mobile
- Max content width: `1280px` (use `Container` component)
- Horizontal padding: `24px` mobile / `48px` tablet / `64px` desktop

#### Spacing Scale (8pt system)
All spacing values must be multiples of 8px:

```
8px · 16px · 24px · 32px · 48px · 64px · 96px · 128px
```

Map to Tailwind: `p-2` (8px) · `p-4` (16px) · `p-6` (24px) · `p-8` (32px) · `p-12` (48px) · `p-16` (64px) · `p-24` (96px) · `p-32` (128px)

#### Border Radius
Use these values only — do not freestyle:

```
4px   → rounded-sm   (small tags, badges)
8px   → rounded      (buttons, inputs)
12px  → rounded-xl   (cards)
16px  → rounded-2xl  (large cards, hero elements)
24px  → rounded-3xl  (feature cards, CTA blocks)
```

#### Dividers & Lines
- **Hairline:** 1px solid `#D0DCE3` — section dividers, card borders
- **Dashed:** 1px dashed `#D0DCE3` — decorative separators only

---

### 15.5 UI Components Reference

All components must match these specifications:

#### Navigation Bar
- White/warm-white background
- Logo wordmark left-aligned: "Hiran Nuwanpriya" in Playfair Display or Satoshi Bold
- Nav links: Satoshi Medium 14px — Work · About · Experience · Contact
- Right end: `+` icon button (round, `--color-deep-blue` fill) as mobile trigger or CTA
- Sticky on scroll with a 1px bottom border in `--color-cool-gray`

#### Buttons

| Variant | Background | Text | Border | Hover |
|---|---|---|---|---|
| **Primary** | `#355CFF` | White | None | `#2347E8` bg |
| **Secondary** | White | `#161616` | 1px `#D0DCE3` | `#F7F6F2` bg |
| **Text Link** | Transparent | `#161616` | None | Underline |

All buttons use Satoshi Medium 14px, 0.5px letter-spacing, `border-radius: 8px`, padding `12px 24px`. Include a `→` arrow icon on Primary and Secondary, `↗` on Text Link.

#### Section Label Pattern
Before each major section heading, include a numbered label:
```
● 01 ABOUT ME    (small dot + number + uppercase category)
```
Font: Satoshi Regular 12px, `--color-deep-blue` dot, `--color-text-muted` text, uppercase, tracked.

#### Stats / Metric Cards
Display key metrics in a horizontal stats block:
```
1M+          80%          4.9★          12+
Projects   Repeat      Client       Years
Delivered  Clients     Rating      Experience
```
Number: Satoshi Bold 32px `--color-charcoal`. Label: Satoshi Regular 12px `--color-text-secondary`.

#### Project Card
- White background, `border-radius: 12px`, 1px `--color-cool-gray` border
- Project image top half (16:9 ratio)
- Title: Satoshi Medium 16px
- Category tag bottom-left
- Arrow `→` link bottom-right in `--color-deep-blue`
- Subtle box-shadow on hover: `0 8px 32px rgba(0,0,0,0.08)`

#### Testimonial Card
- White card, `border-radius: 16px`
- Large `❝` quote mark in `--color-deep-blue`, 48px
- Quote text: Satoshi Regular 16px, line-height 1.6
- Attribution: avatar + name (Satoshi Medium 14px) + role (Satoshi Regular 12px `--color-text-secondary`) + `●` accent dot

#### Contact CTA Block
- Full-width block, `background: #355CFF`, `border-radius: 24px`
- Headline: Satoshi Bold 28px white
- Subline: Satoshi Regular 16px white/80%
- Email and location: left-aligned, white
- "Schedule a Call →" text link: right-aligned, white
- Accent dots row below: Fast `●` · Collaborative `●` · Thoughtful `●` · Impactful `●`

---

### 15.6 Imagery Direction

All images and visual assets must follow these rules:

- **Profile photo:** Monochrome or desaturated portrait — honest, timeless, professional. No bright backgrounds.
- **Project visuals:** Clean creative compositions — minimal, intentional, high contrast. Think editorial product photography style.
- **Background accents:** High-contrast abstract or architectural photography where backgrounds are needed.
- **Selective blue accents:** Use `--color-soft-blue` (`#AFC4FF`) or `--color-deep-blue` as overlay tints on images to create visual cohesion.
- **No stock photo clichés:** No handshakes, laptops on desks, generic team photos.
- Aspect ratios: Hero `16:9`, Project cards `4:3`, Profile `1:1` (circular crop)

---

### 15.7 Page-by-Page Style Notes

These are the design intentions for each page type. Agents must implement these, not invent alternatives.

| Page | Design Intention |
|---|---|
| **Homepage** | Strong H1 in Playfair Display, clear value proposition in Satoshi, generous whitespace, bold typography. Lead with identity then work. |
| **About** | Share background, approach, and values. Pair text with key stats block and a personal narrative paragraph. Satoshi throughout. |
| **Projects / Portfolio** | Showcase work with context, process, and measurable impact. Card grid layout, clean, focused on the work. |
| **Experience** | Vertical timeline, clean and editorial. Company + role + dates left-aligned. Key achievements as bullet points. |
| **Contact** | Use the full-width `--color-deep-blue` CTA block pattern. Include email, LinkedIn, GitHub, location, availability. |
| **Footer** | Black background (`#000000`), white text. Essential links only: nav + socials. High contrast. "Clarity in design. Purpose in every detail." tagline. |

---

### 15.8 Animation & Motion

- **Entry animations:** Elements fade up (`translateY: 16px → 0`, `opacity: 0 → 1`) on scroll-into-view using CSS `@keyframes` or lightweight IntersectionObserver. Duration: `400ms`, easing: `ease-out`.
- **Stagger delay:** When revealing a list of cards, stagger by `80ms` per item.
- **Hover transitions:** All interactive elements use `transition: all 150ms ease` — no longer.
- **No:** parallax, auto-playing video, looping animations, heavy JS-driven motion.
- **Performance rule:** All animations must use only `transform` and `opacity` — never `width`, `height`, `top`, `left` (causes layout reflow).

---

## 16. Component Rules

- **Every component must be TypeScript** with explicit prop types.
- **No hardcoded content in components.** All text, data, and links come from `/data/` files or props.
- **Use server components by default.** Only use `"use client"` when interactivity requires it (e.g. mobile nav toggle, contact form).
- **Use Next.js `<Image />`** for all images — never raw `<img>` tags.
- **Use Next.js `<Link />`** for all internal navigation — never `<a href>` for internal links.
- **Accessible markup:** correct heading order, alt text on meaningful images, descriptive link text, visible focus states, semantic HTML.

### Core Components to Build

| Component | Location | Notes |
|---|---|---|
| `Header` | `components/layout/` | Responsive nav, mobile hamburger |
| `Footer` | `components/layout/` | Links, social, copyright |
| `MobileNav` | `components/layout/` | Client component |
| `Hero` | `components/sections/` | H1, subheading, CTA buttons |
| `ProofCards` | `components/sections/` | 4–6 stat/proof cards |
| `SkillsGrid` | `components/sections/` | Grouped badges by category |
| `FeaturedProjects` | `components/sections/` | 5 project cards |
| `ResultsImpact` | `components/sections/` | Metric cards with numbers |
| `BlogPreview` | `components/sections/` | 3 article cards |
| `ContactCTA` | `components/sections/` | Headline + button row |
| `ExperienceTimeline` | `components/sections/` | Vertical timeline |
| `Button` | `components/ui/` | Primary / secondary / ghost variants |
| `Card` | `components/ui/` | Generic card wrapper |
| `Badge` | `components/ui/` | Tech stack / skill badge |
| `MetricCard` | `components/ui/` | Number + label stat card |
| `ProjectCard` | `components/ui/` | Project preview card |
| `SectionHeading` | `components/ui/` | Consistent H2 + subtitle |
| `Container` | `components/ui/` | Max-width layout wrapper |
| `JsonLd` | `components/seo/` | Generic JSON-LD injector |
| `BreadcrumbJsonLd` | `components/seo/` | Breadcrumb schema |

---

## 17. Coding Conventions

### General

- Use TypeScript everywhere. No `any` types.
- Use explicit return types on all functions and components.
- Use `const` by default; `let` only when reassignment is needed.
- Use descriptive names: `isMobileNavOpen`, not `open`.
- Prefer early returns to deeply nested conditionals.
- Group imports: React → Next.js → third-party → internal (`@/`)

### Naming

- **Components:** PascalCase (`ProjectCard`, `ContactCTA`)
- **Files:** PascalCase for components, camelCase for utilities and data files
- **CSS classes:** Tailwind utilities only — no custom class names unless absolutely necessary
- **Types/interfaces:** PascalCase (`ProjectData`, `SkillGroup`)
- **Data exports:** camelCase named exports (`export const projects = [...]`)

### File Structure Rules

- One component per file
- Co-locate component-specific types at the top of the component file or in `types/index.ts` if shared
- No barrel index files unless the folder has 5+ exports

---

## 18. Performance Rules

- Use `next/image` with correct `width`, `height`, and `alt` on every image.
- Compress all images before committing. Use WebP or AVIF.
- Use server components by default — only add `"use client"` when necessary.
- Lazy-load non-critical sections with `React.lazy` or Next.js dynamic imports where appropriate.
- Keep JavaScript bundle minimal — avoid heavy third-party libraries.
- No heavy CSS animations — use `transition` and `transform` only.
- Target Lighthouse score: 95+ on all pages.
- Monitor Core Web Vitals via Vercel Speed Insights after deployment.

---

## 19. Vercel Deployment

### Setup Commands

```bash
npx create-next-app@latest hiran-portfolio
# TypeScript: Yes | ESLint: Yes | Tailwind CSS: Yes | App Router: Yes | Turbopack: Yes

git init
git add .
git commit -m "Initial portfolio setup"
git branch -M main
git remote add origin https://github.com/Hirannuwanpriya/hiran-portfolio.git
git push -u origin main
```

### Vercel Settings

| Setting | Value |
|---|---|
| Framework Preset | Next.js |
| Build Command | `next build` |
| Install Command | `npm ci` |
| Production Branch | `main` |
| Node.js Version | 20.x |

### Custom Domain

Add to Vercel after first deployment:
```
hirannuwanpriya.com
www.hirannuwanpriya.com
```

### Post-Deploy Checklist

- [ ] Custom domain configured and DNS propagated
- [ ] Vercel Analytics enabled
- [ ] Vercel Speed Insights enabled
- [ ] Google Analytics 4 tag added
- [ ] Google Search Console domain verified
- [ ] Sitemap submitted: `https://hirannuwanpriya.com/sitemap.xml`
- [ ] All pages return 200 in production
- [ ] Mobile responsiveness verified
- [ ] Core Web Vitals passing in Speed Insights
- [ ] Resume PDF accessible at `/resume/hiran-nuwanpriya-resume.pdf`

---

## 20. Build Phases

### Phase 1: Foundation
- Create Next.js TypeScript project with Tailwind v4
- Configure ESLint + Prettier
- Create folder structure
- Create all data files (`profile.ts`, `skills.ts`, `experience.ts`, `projects.ts`, `blog.ts`)
- Build `Header`, `Footer`, `Container`, `Button`, `Badge` components
- Set up global SEO metadata in `app/layout.tsx`

### Phase 2: Main Pages
- Homepage (all 8 sections)
- About page
- Skills page
- Experience page
- Projects listing page
- Resume page
- Contact page
- Services page

### Phase 3: Case Studies
Detailed pages for:
- BookNordics
- Promsoc.Brussels
- Werenewsneakers
- BrusselsLife
- IRISnet

### Phase 4: SEO & Structured Data
- Metadata on all pages
- Open Graph images
- `sitemap.ts`
- `robots.ts`
- JSON-LD Person schema
- JSON-LD Article schema on blog posts
- Breadcrumb schema on project and blog pages
- Canonical URLs

### Phase 5: Analytics & Deployment
- Push to GitHub
- Deploy to Vercel
- Add custom domain
- Enable Vercel Analytics + Speed Insights
- Add Google Analytics 4
- Submit to Google Search Console

### Phase 6: Content Growth
Publish blog articles targeting:
- Laravel performance optimisation
- SaaS architecture with Laravel
- Legacy system migration
- AI-assisted software engineering
- Laravel + React project architecture
- DevOps for Laravel applications

---

## 21. Key Content Data (source of truth)

All content below must be accurately reflected in data files. Do not invent or embellish.

### Metrics to Use (from CV)
- 66% reduction in website load time (12s → 4s) — BookNordics
- 50%+ improvement in response times — BWS Brussels
- 99.9% uptime maintained — BWS Brussels
- 50% reduction in time-to-market — BWS Brussels
- 30% improvement in operational efficiency — BWS Brussels
- 10,000+ user accounts — Promsoc.Brussels
- 10,000+ products synced — BookNordics
- ~40% backend load time improvement — Promsoc.Brussels
- ~30% increase in session duration — Promsoc.Brussels
- ~25% reduction in bounce rate — Promsoc.Brussels
- 250+ active courses — Promsoc.Brussels
- 20+ admin staff — Promsoc.Brussels
- 12,000+ addresses and events — BrusselsLife
- 200+ companies, 1,000+ user accounts — IRISnet
- 15+ dynamic report templates — IRISnet

### Education
- MSc in Software Engineering — Kingston University, London, UK (2020–2022)
- BSc in Information Technology — SLIIT, Sri Lanka (2010–2013)

### Contact
- Email: hirannuwanpriya@gmail.com
- Phone: +61 478 001 862
- LinkedIn: https://www.linkedin.com/in/hirannuwanpriya/
- GitHub: https://github.com/Hirannuwanpriya
- Location: Hobart, TAS, Australia
- Availability: Open to remote roles | Available for periodic on-site travel

---

## 22. Critical Reminders for Claude

When working on this codebase:

1. **Never hardcode content in components.** All copy, data, and links must come from `/data/` files.
2. **Use server components by default.** Add `"use client"` only when React state or browser APIs are required.
3. **Every public page must have a unique `metadata` export** with title, description, and Open Graph fields.
4. **Sitemap must include all project and blog slugs** dynamically from data files — not a static list.
5. **JSON-LD structured data must be rendered server-side** via script tags in server components, not injected via `useEffect`.
6. **Resume PDF must be in `public/resume/`** and linked from the resume page and hero CTA.
7. **All metrics and claims must match the CV exactly.** Do not inflate or invent numbers.
8. **Mobile-first layout is mandatory.** Test all components at 375px before 1440px.
9. **Use `next/image` for every image.** No raw `<img>` tags.
10. **Use `next/link` for every internal link.** No `<a href>` for internal navigation.
11. **Run ESLint and TypeScript type-check before marking any task complete.**
12. **The five case study projects are the core proof-of-work.** They must be detailed, metrics-driven, and recruiter-readable.
13. **Brand guidelines (Section 15) are the single source of truth for all visual decisions.** Never use dark backgrounds — the site is light theme (`#F7F6F2` warm white). Never use fonts other than Playfair Display (H1 only) and Satoshi (everything else).
14. **Colour hex values must always come from CSS variables** defined in `globals.css`. Never hardcode hex values like `#355CFF` in component styles — use `var(--color-deep-blue)`.
15. **All spacing must use the 8pt scale** — only values from: 8, 16, 24, 32, 48, 64, 96, 128px. No arbitrary spacing.
16. **Section labels follow the numbered dot pattern** (`● 01 ABOUT ME`) before every major section heading. This is a brand-mandated pattern.
17. **Buttons always include directional arrows** — `→` on Primary/Secondary, `↗` on Text Links. This is a brand requirement, not optional.
