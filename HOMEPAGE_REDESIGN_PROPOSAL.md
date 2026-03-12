# DreamHost Homepage Redesign Proposal
## Content Hierarchy & Section Mapping

---

## Executive Summary

This proposal maps out a redesigned DreamHost homepage focused on clear product segmentation, performance credibility, and conversion. Based on competitive analysis of BlueHost, Hostinger, and SiteGround — plus DreamHost's own current site and internal performance data — the recommendation consolidates a currently scattered homepage (~15+ sections) into a focused, intentional flow of **10 sections**.

### Key Problems with Current Homepage
1. **No clear value proposition** — Hero leads with Remixer/Liftoff (naming confusion), but the page also pushes domains, flash sales, 5 hosting products, CDN, and pro services all at once
2. **Differentiators are buried** — Employee-owned, open source commitment, privacy stance, WordPress contributions are deep in the page
3. **No audience segmentation** — Beginners, developers, and growing businesses all see the same undifferentiated wall of content
4. **Discount-led messaging** — Flash sale banners and price anchors dominate over value and trust

### What Competitors Do Well
- **BlueHost**: Layered trust (WordPress.org endorsement, Trustpilot, 5M users), clear hosting type cards, third-party speed benchmarks
- **Hostinger**: AI-first positioning woven into every section, progressive product education (simple → complex), statistics bar for scale proof
- **SiteGround**: Platform positioning ("Web hosting & beyond"), no pricing on homepage (routes to subpages), support as a competitive moat with named staff photos

---

## Proposed Section Flow

```
┌─────────────────────────────────────────┐
│  1. ANNOUNCE BAR                        │
│  2. NAVIGATION                          │
│  3. HERO                                │
│  4. TRUST BAR                           │
│  5. HOSTING PLANS                       │
│  6. REMIXER (AI WEBSITE BUILDER)        │
│  7. WHY DREAMHOST                       │
│  8. GLOBAL CDN & PERFORMANCE            │
│  9. FAQ                                 │
│ 10. FOOTER                              │
└─────────────────────────────────────────┘
```

---

## Section 1: Announce Bar
**Purpose**: Timely promotion or news — rotatable, not permanent content

**Content**:
- Single promotional message (e.g., current hosting deal, new feature launch)
- Keep it short — one line with a CTA link
- Right-side: Support link / Knowledge Base

**Notes**: Current announce bar structure works well. Keep it lightweight. No countdown timers (that's Hostinger's playbook and reads as discount-brand).

---

## Section 2: Navigation
**Purpose**: Global wayfinding

**Content**:
- DreamHost logo
- Nav items: Hosting, Website Builder, Domains, Pro Services, Pricing
- Right: Login | Get Started (CTA button)

**Notes**: Already built and refined in our coded header. No changes needed to structure. The nav should remain clean with the placeholder bar approach we've established until final content is locked.

---

## Section 3: Hero
**Purpose**: Primary value proposition — the single most important message on the page

**Headline Direction**: Lead with what DreamHost IS, not a product feature.

**Content Hierarchy**:
1. **Eyebrow**: "Employee-Owned Since 1997" (immediately differentiates — no competitor can claim this)
2. **H1**: Value-driven headline about building/hosting with a company that puts customers first (not a product pitch)
3. **Subheadline**: Brief supporting copy — mention AI website builder, managed WordPress, VPS, and 100% uptime guarantee in one line
4. **Primary CTA**: "See Our Plans" (routes to Section 5)
5. **Secondary CTA**: "Try Remixer Free" (routes to builder)
6. **Hero Visual**: Product screenshot or illustration showing the Remixer builder interface or a hosting dashboard

**Rationale**: The current hero leads with "You describe it. Remixer builds it." — which buries the hosting business (DreamHost's core revenue) behind a website builder pitch. The hero should establish brand identity and trust FIRST, then let individual sections sell products. BlueHost and Hostinger both use their heroes for broad value propositions, not single-product pitches.

The "Employee-Owned" eyebrow is a strategic move — it immediately sets DreamHost apart from every competitor. BlueHost is owned by Newfold Digital (EIG). Hostinger is VC-backed. SiteGround was acquired by a private equity firm. DreamHost's independence IS the story.

---

## Section 4: Trust Bar
**Purpose**: Immediate credibility before the user scrolls into product content

**Content** (horizontal strip, 4-5 items):
- Trustpilot rating (star display + review count)
- "100% Uptime Guarantee"
- "WordPress.org Recommended"
- "25+ Years Hosting Experience"
- "Employee-Owned & Independent"

**Rationale**: Every top competitor places trust signals immediately after the hero. BlueHost uses a triple trust bar (money-back, WordPress.org, Trustpilot). Hostinger places Trustpilot + testimonials right after hero. DreamHost currently has NO dedicated trust bar — the Trustpilot reviews appear only on product subpages.

---

## Section 5: Hosting Plans
**Purpose**: Core product showcase — the primary conversion section

**Content Structure**: Three product cards, side by side

### Card 1: Web Hosting
- **Label**: "Getting Started"
- **Headline**: "Web Hosting"
- **Description**: Entry-level shared hosting for new websites and blogs
- **Starting Price**: From $X.XX/mo
- **Key Features** (3-4 bullets):
  - Free domain + SSL
  - 1-click WordPress install
  - NVMe SSD storage
  - 24/7 expert support
- **CTA**: "View Plans"

### Card 2: DreamPress
- **Label**: "Most Popular" (badge)
- **Headline**: "DreamPress"
- **Description**: Managed WordPress hosting with built-in CDN and staging
- **Starting Price**: From $XX.XX/mo
- **Key Features** (3-4 bullets):
  - Managed WordPress updates + security
  - Built-in Bunny CDN
  - 1-click staging environment
  - On-demand backups
- **CTA**: "View Plans"

### Card 3: VPS Hosting
- **Label**: "Power Users"
- **Headline**: "VPS Hosting"
- **Description**: Fully managed VPS with dedicated resources and Auto-Boost RAM
- **Starting Price**: From $XX/mo
- **Key Features** (3-4 bullets):
  - Dedicated CPU + RAM
  - Auto-Boost RAM protection
  - Full root access (or managed)
  - Built-in observability
- **CTA**: "View Plans"

**Design Notes**:
- DreamPress gets the center position and "Most Popular" badge (classic anchoring — BlueHost uses "RECOMMENDED" on their third tier, Hostinger uses "MOST POPULAR" on their middle tier)
- Cards should NOT show full pricing tables — just starting prices and key differentiators. Detailed comparison belongs on dedicated plan pages (SiteGround's approach)
- Each card routes to its respective product page for full plan comparison
- Do NOT mix product categories in one pricing table (the current hosting page puts shared, DreamPress, and VPS in one grid, which is confusing)

**Rationale**: DreamHost's current homepage buries hosting plans in a "Hosting Services" section that's the 6th or 7th section down the page, after deals, domains, and a flash sale banner. Hosting is the core business — it should be the first product content users see after the trust bar.

---

## Section 6: Remixer (AI Website Builder)
**Purpose**: Prominent product showcase for the AI builder — positioned as a capability ON TOP of hosting, not a replacement for it

**Content Hierarchy**:
1. **Eyebrow**: "AI Website Builder"
2. **H2**: Headline about building your website in seconds with AI
3. **Subheadline**: Describe the conversational AI builder experience — you describe your site, Remixer generates it, you customize with drag-and-drop
4. **Three Feature Pillars** (icon + short description each):
   - **AI-Powered Generation**: Describe your vision, get a complete site
   - **WordPress-Native**: Built on WordPress, not a proprietary locked-in builder (this is a key differentiator vs. Wix/Squarespace AND vs. Hostinger's builder)
   - **Included Free**: Bundled with hosting plans, not an upsell
5. **CTA**: "Try Remixer" or "Build Your Site"
6. **Visual**: Screenshot or animation of the Remixer builder interface

**Naming Note**: The current site uses both "Remixer" (homepage hero, nav) and "Liftoff" (builder page). This proposal uses "Remixer" per the user's brief. The naming needs to be consolidated site-wide.

**Rationale**: Hostinger dedicates ~3 full sections to their AI builder capabilities (Website Builder, Quick-start WordPress, Hostinger Horizons). BlueHost highlights "AI Site Creation Tools" across all plan features. DreamHost's builder deserves prominent placement, but as Section 6 (not the hero), because:
1. Hosting is the revenue engine — builder is the acquisition tool
2. Users who come to DreamHost.com already know it's a hosting company
3. The builder pitch is stronger AFTER the user understands the hosting foundation it sits on

---

## Section 7: Why DreamHost
**Purpose**: Brand differentiation — the section that answers "why should I choose DreamHost over BlueHost/Hostinger/SiteGround?"

**Content Structure**: H2 headline + 4-6 differentiator blocks (icon + headline + short description)

### Differentiator 1: Employee-Owned & Independent
- Not owned by a private equity firm or holding company
- Customer interests come first — no corporate parent extracting value
- Decisions made by people who use the product

### Differentiator 2: Open Source Champions
- Active WordPress core contributors
- Support and contribute to open-source projects
- Your site runs on open standards, never locked into proprietary tech

### Differentiator 3: Privacy by Default
- Domain privacy included free (many competitors charge extra)
- No upselling your data
- Committed to user privacy since 1997

### Differentiator 4: 100% Uptime Guarantee
- Industry-leading uptime SLA
- Credit-backed guarantee (not just marketing language)
- Redundant infrastructure across global data centers

### Differentiator 5: In-House Expert Support
- 100% in-house support team (no outsourcing)
- WordPress specialists — core contributors on staff
- 24/7 availability via chat and ticket

### Differentiator 6: Proven Track Record
- 25+ years in business
- 1.5M+ websites hosted
- Trusted by developers, businesses, and creators worldwide

**Rationale**: DreamHost's current homepage buries these differentiators in a "What Makes DreamHost So Different" section that's ~70% down the page. These are the most compelling reasons to choose DreamHost — especially "Employee-Owned" and "Open Source Champions," which NO competitor can match. BlueHost's "Why Bluehost is right for you" section focuses on generic features (CDN, security, auto-updates). Hostinger's differentiators are AI tools and price. SiteGround leans on support quality. DreamHost should lean into values and independence.

---

## Section 8: Global CDN & Performance
**Purpose**: Showcase the new Bunny CDN-powered global infrastructure with real performance data

**Content Hierarchy**:
1. **Eyebrow**: "Global Performance"
2. **H2**: Headline about worldwide speed powered by Bunny CDN
3. **Subheadline**: Brief explanation — content delivered from the nearest global edge location, dramatically reducing load times for visitors worldwide
4. **Performance Stats Display**: Visual presentation of the datacenter performance data

### Stats to Feature (from AMS1 and SIN1 data):

**Europe (Amsterdam Data Center)**:
| Metric | Before (US Only) | After (AMS1) | Improvement |
|--------|-------------------|--------------|-------------|
| TTFB (Frankfurt) | 270ms | 19ms | 93% faster |
| TTFB (London) | 239ms | 22ms | 91% faster |
| Page Load (Frankfurt) | 995ms | 460ms | 54% faster |
| Page Load (London) | 938ms | 470ms | 50% faster |

**Asia-Pacific (Singapore Data Center)**:
| Metric | Before (US Only) | After (SIN1) | Improvement |
|--------|-------------------|--------------|-------------|
| TTFB (Singapore) | 210ms | 9ms | 96% faster |
| FCP (Singapore) | 924ms | 374ms | 59% faster |
| Page Load (Singapore) | 917ms | 561ms | 39% faster |

5. **Visual**: World map with datacenter locations highlighted (Portland, Amsterdam, Singapore) showing edge network reach
6. **Supporting Copy**: Mention specific CDN benefits — automatic image optimization, DDoS protection, global edge caching
7. **CTA**: "Learn More About Our CDN" or "See All Plans with CDN"

### Load Testing / Competitive Benchmark (from ReviewSignals data):
Consider including a simplified competitive benchmark section showing DreamHost's load testing performance vs. competitors:
- DreamHost handled **800K+ successful requests** with sub-2s P95 response times on optimized configs
- Competitive with SiteGround (~610K requests, 1s P95) and ahead of WPEngine (~970K requests but 3.5s P95)
- Kinsta showed high throughput but also high failure rates (~89-92% failure rate in tests)

**Presentation Recommendation**: Use the AMS1/SIN1 CDN data as the PRIMARY performance story (it's cleaner, more dramatic, and directly tied to the Bunny CDN product feature). The ReviewSignals load testing data is more nuanced and better suited for a dedicated performance page or blog post rather than homepage real estate.

**Rationale**: BlueHost includes a speed comparison section citing WPShout benchmarks. Hostinger uses statistics bars (4M+ clients, 150+ countries). SiteGround relies on testimonials mentioning speed improvements. DreamHost has ACTUAL first-party performance data showing 90%+ TTFB improvements — this is far more compelling than any competitor's speed claims. This data should be presented visually (not in tables) with large, bold improvement percentages.

---

## Section 9: FAQ
**Purpose**: Address common questions, reduce support load, capture long-tail SEO

**Content**: Accordion-style expandable Q&A (6-8 questions)

### Recommended Questions:

1. **What type of hosting do I need?**
   - Guide beginners toward Web Hosting, growing sites toward DreamPress, power users toward VPS

2. **What is DreamPress?**
   - Explain managed WordPress hosting and how it differs from standard Web Hosting

3. **What is Remixer?**
   - Explain the AI website builder, that it's included with hosting, and that it builds on WordPress

4. **Does DreamHost offer a CDN?**
   - Explain Bunny CDN integration, global edge locations, and that it's included with DreamPress (or as an add-on for other plans)

5. **Can I migrate my existing website to DreamHost?**
   - Cover free migration tools and assisted migration

6. **What is the 100% Uptime Guarantee?**
   - Explain the SLA and credit policy

7. **What makes DreamHost different from other hosts?**
   - Employee-owned, open source, privacy-first, 25+ years

8. **What if I'm not satisfied?**
   - 97-day money-back guarantee (DreamHost's is industry-leading at 97 days vs. the standard 30 days — this should be highlighted more prominently)

**Rationale**: BlueHost has 7 FAQ questions. Hostinger has NO FAQ (uses AI chatbot instead). SiteGround has no homepage FAQ. A well-structured FAQ serves dual purpose: conversion support (answering objections) and SEO (long-tail keyword capture). DreamHost's current FAQ exists but is buried at the very bottom of a very long page.

---

## Section 10: Footer
**Purpose**: Navigation, legal, trust reinforcement

**Content**:
- Link columns: Products, Resources, Company, Support, Legal
- Payment method icons
- Social media links
- "Employee-Owned & Independent" badge or tagline
- Copyright

---

## Competitive Comparison Matrix

| Element | BlueHost | Hostinger | SiteGround | DreamHost (Current) | DreamHost (Proposed) |
|---------|----------|-----------|------------|--------------------|--------------------|
| Hero Focus | Broad trust + AI | Price discount + urgency | Platform positioning | Single product (Remixer) | Brand identity + values |
| Trust Bar | ✅ Triple (Trustpilot, WP.org, guarantee) | ✅ Trustpilot + testimonials | ✅ Trustpilot + domain count | ❌ None on homepage | ✅ Trustpilot + uptime + WP.org + years |
| Plan Presentation | 4-tier pricing table | 3-tier pricing cards | No pricing (routes to subpages) | Mixed products in one list | 3 product cards (Web/DreamPress/VPS) |
| AI Builder | Feature bullet in plans | 3 dedicated sections | 1 service card | Hero + mid-page section | Dedicated Section 6 |
| Differentiators | Generic features | AI + price | Support quality | Buried deep on page | Section 7 — prominent |
| Performance Data | Third-party benchmark | Statistics bar | Testimonial quotes | CDN section (buried) | Dedicated section with real data |
| FAQ | ✅ 7 questions | ❌ (AI chatbot) | ❌ | ✅ (buried) | ✅ 8 questions, prominent |
| Sections on Page | ~14 | ~14 | ~11 | ~15+ | **10** |

---

## Content Priorities (Ranked)

1. **Hero + Trust Bar** — Establish brand identity and credibility immediately
2. **Hosting Plans** — Core business, primary conversion path
3. **Remixer** — Key acquisition tool and differentiator
4. **Why DreamHost** — Brand values that no competitor can replicate
5. **Global CDN & Performance** — New capability with compelling data
6. **FAQ** — Conversion support + SEO

---

## What We're NOT Including (and Why)

- **Domain search bar**: BlueHost and Hostinger both feature domain search prominently. DreamHost's core business is hosting, not domain registration. Domain search belongs on a dedicated domains page, not eating homepage real estate.
- **Flash sale banners**: The current homepage has promotional sale banners. These train users to wait for deals and undermine brand value. Pricing should be confident, not desperate.
- **Pro Services section**: Currently on the homepage. Better suited for a nav dropdown or dedicated page. The homepage should focus on self-serve products.
- **Dedicated Hosting / Cloud Hosting cards**: These are niche products for specific audiences. They don't belong in the main homepage plan showcase. They can be mentioned in the FAQ or linked from the hosting plans page.
- **Customer testimonial carousel**: While every competitor has one, a trust bar with Trustpilot rating is more space-efficient on the homepage. Full testimonials can live on product pages where they're more contextually relevant.
- **Media logo bar**: DreamHost doesn't currently feature press logos. Unless there are recent notable press mentions, this section would feel forced.

---

## Next Steps

1. Review and approve this content hierarchy
2. Finalize actual copy/headlines for each section
3. Begin wireframing the approved section flow
4. Source/create visual assets (screenshots, illustrations, map)
5. Build out in the coded landing page
