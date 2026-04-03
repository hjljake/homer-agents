---
name: website-platforms
display_name: Website Platforms
description: Platform comparison knowledge for website recommendations — covers WordPress, Squarespace, Wix, Webflow, Shopify, and Contentful with pricing, pros/cons, technical requirements, and Amiara integration readiness
category: planning
---

# Website Platforms

When recommending a website platform, evaluate each option against the user's business type, technical skill level, budget, and future integration needs. Always prioritize platforms that the user can manage independently without developer help.

## Platform Profiles

### WordPress.org (Self-Hosted)

- **Best for:** Businesses that want full control, plan to scale content marketing, or need extensive customization
- **Technical level required:** Low-Medium (managed hosting handles the hard parts)
- **Monthly cost:** $10-50/mo (hosting) + $0-100/yr (theme/plugins). Managed hosts: SiteGround ($3-15/mo), Cloudways ($14+/mo), WP Engine ($20+/mo)
- **Blog capability:** Native and excellent — WordPress was built as a blogging platform. Best-in-class blog architecture, categories, tags, RSS, SEO plugins (Yoast/RankMath)
- **E-commerce:** Via WooCommerce plugin (free, powerful, but adds complexity)
- **SEO:** Excellent with plugins. Full control over meta tags, sitemaps, schema markup, URL structure
- **Strengths:** 40%+ market share, massive ecosystem (60,000+ plugins), any design possible, full data ownership, huge freelancer pool for help
- **Weaknesses:** Requires updates/maintenance, security is your responsibility on self-hosted, plugin conflicts happen, can be overwhelming for beginners
- **Amiara integration readiness:** HIGH — Full REST API built in, Application Passwords for auth (no plugins needed), existing MCP servers available. Easiest platform for Amiara to draft and manage blog posts programmatically.

### WordPress.com (Managed)

- **Best for:** Users who want WordPress without managing hosting/updates
- **Technical level required:** Low
- **Monthly cost:** Free (very limited) / $4/mo (Personal) / $8/mo (Premium) / $25/mo (Business) / $45/mo (Commerce)
- **Blog capability:** Same core WordPress engine. Business plan+ required for plugins and full REST API access.
- **Strengths:** Zero maintenance, automatic updates, built-in CDN and security
- **Weaknesses:** Limited customization on lower plans, plugins only on Business+, more expensive than self-hosted for equivalent functionality
- **Amiara integration readiness:** MEDIUM — REST API available on Business+ plans. Lower plans have restricted API access. Automattic exploring MCP integrations.

### Squarespace

- **Best for:** Service businesses, creatives, portfolios, restaurants — anyone who values design and simplicity over flexibility
- **Technical level required:** Low
- **Monthly cost:** $16/mo (Personal) / $23/mo (Business) / $27/mo (Basic Commerce) / $49/mo (Advanced Commerce)
- **Blog capability:** Good built-in blogging with categories, tags, and scheduling. Clean URLs. Limited compared to WordPress (no plugins for advanced SEO, limited taxonomy)
- **E-commerce:** Built-in on Business+ plans. Good for physical products, less flexible than Shopify for complex catalogs
- **SEO:** Decent basics (meta titles, descriptions, auto-sitemap). No advanced schema markup control. Limited URL customization.
- **Strengths:** Beautiful templates out of the box, all-in-one (hosting + domain + email + analytics), excellent for non-technical users, reliable uptime
- **Weaknesses:** Limited customization beyond templates, no plugin ecosystem, slower page load times than optimized WordPress, vendor lock-in
- **Amiara integration readiness:** LOW — No public write API for blog content. Content creation is UI-only. Would require browser automation or Squarespace to release a content API. Not recommended if Amiara integration is a priority.

### Wix

- **Best for:** Very small businesses, personal sites, local businesses that need something quick and cheap
- **Technical level required:** Very Low (drag-and-drop)
- **Monthly cost:** Free (Wix-branded) / $17/mo (Light) / $29/mo (Core) / $36/mo (Business) / $159/mo (Business Elite)
- **Blog capability:** Built-in blog module. Basic categories and tags. Adequate for simple blogs, limited for content-heavy strategies.
- **E-commerce:** Built-in on Business+ plans
- **SEO:** Improved significantly (was historically weak). Now has meta tags, canonical URLs, sitemaps. Still lacks advanced schema control.
- **Strengths:** Easiest drag-and-drop builder, AI site generator, fast to launch, good for non-technical users who want visual control
- **Weaknesses:** Page speed often poor, hard to migrate away, limited export options, template lock-in (can't switch templates without rebuilding)
- **Amiara integration readiness:** LOW-MEDIUM — Wix has a Content Management API (Velo) that supports creating blog posts programmatically, but it's more complex than WordPress. No known MCP servers. Limited compared to WordPress REST API.

### Webflow

- **Best for:** Design-focused businesses, marketing teams that want visual control with clean code output, agencies
- **Technical level required:** Medium (visual builder but has a learning curve)
- **Monthly cost:** Free (staging only) / $14/mo (Basic) / $23/mo (CMS) / $39/mo (Business) / $212/mo (Enterprise). CMS plan required for blog.
- **Blog capability:** Good via Webflow CMS Collections. Clean URL structure, full control over blog layout. Requires CMS plan ($23+/mo).
- **E-commerce:** Built-in on Business+ plans. Limited compared to Shopify.
- **SEO:** Excellent — clean semantic HTML output, full meta tag control, auto-sitemap, Open Graph tags, fast page speeds
- **Strengths:** Designer-quality output without code, excellent performance, clean HTML/CSS, visual CMS, good SEO defaults
- **Weaknesses:** Steeper learning curve than Squarespace/Wix, CMS item limits on lower plans (10K on CMS plan), expensive at scale, smaller freelancer pool
- **Amiara integration readiness:** MEDIUM-HIGH — Webflow has a CMS API that supports creating, updating, and publishing collection items (blog posts). REST-based, API key auth. Could be integrated as an Amiara tool. No official MCP server but API is clean enough for a custom integration.

### Shopify

- **Best for:** E-commerce first businesses. If you sell products, this is the default choice.
- **Technical level required:** Low
- **Monthly cost:** $5/mo (Starter) / $39/mo (Basic) / $105/mo (Shopify) / $399/mo (Advanced)
- **Blog capability:** Built-in but basic. Functional for supporting product marketing. Not designed as a content-first platform — limited categorization (tags only, no categories), no native RSS, basic editor.
- **E-commerce:** Best-in-class. This is what Shopify does.
- **SEO:** Good for product pages. Blog SEO is limited (auto-generated URLs include /blogs/news/ prefix, limited schema control).
- **Strengths:** Unmatched e-commerce features, massive app ecosystem, handles payments/shipping/inventory, scales well
- **Weaknesses:** Blog is an afterthought, limited content customization without Liquid theme editing, expensive apps for basic features
- **Amiara integration readiness:** MEDIUM — Has REST and GraphQL Admin APIs that support creating blog articles. API key auth. Blog article creation is straightforward. No dedicated MCP server but API is well-documented.

### Contentful + Vercel/Netlify (Headless)

- **Best for:** Tech-savvy teams that want complete control over frontend and content model. Developer-led projects.
- **Technical level required:** HIGH — requires a developer to build the frontend
- **Monthly cost:** Contentful free tier (5 users, 25K records) / $300/mo (Team). Plus hosting: Vercel free tier / $20/mo (Pro). Total: $0-320+/mo
- **Blog capability:** Excellent content modeling — define exactly the fields you need. But you must build the blog frontend yourself (Next.js, Gatsby, etc.)
- **E-commerce:** Not built-in. Pair with Shopify/Snipcart/Stripe for commerce.
- **SEO:** Full control since you own the frontend. As good as your implementation.
- **Strengths:** Best-in-class content API, official MCP server, complete flexibility, multi-channel content delivery, excellent developer experience
- **Weaknesses:** Requires a developer, not self-service for non-technical users to set up, expensive at scale, content preview requires frontend work
- **Amiara integration readiness:** HIGHEST — Official MCP server (`@contentful/mcp-server`), excellent Content Management API, `rich-text-from-markdown` converter. Best API surface of any CMS. But only practical if the user has developer resources.

## Recommendation Matrix

| Scenario | Primary Rec | Runner-up | Avoid |
|---|---|---|---|
| Non-technical, needs blog, tight budget | WordPress.com Business | Squarespace | Contentful |
| Non-technical, needs blog, flexible budget | WordPress.org (managed host) | Squarespace | Contentful |
| Non-technical, e-commerce + blog | Shopify + WordPress.org | Shopify (blog built-in) | Wix |
| Design-focused, marketing team | Webflow | Squarespace | Wix |
| Wants Amiara integration (top priority) | WordPress.org | Webflow | Squarespace |
| Has developers on team | Contentful + Vercel | WordPress.org | Wix |
| Local business, just needs something fast | Squarespace | Wix | Contentful |
| Already has Shopify store, needs blog | Add WordPress.org on subdomain | Shopify built-in blog | — |

## Amiara Integration Tier List

| Tier | Platforms | Why |
|---|---|---|
| **Tier 1 — Ready now** | WordPress.org | Full REST API, built-in auth, existing MCP servers, drafts native |
| **Tier 2 — Feasible** | Contentful, Webflow | Good APIs, official/clean MCP paths, but require more setup |
| **Tier 3 — Possible** | Shopify, Wix, WordPress.com | APIs exist but are limited or require higher-tier plans |
| **Tier 4 — Not feasible** | Squarespace | No content write API |
