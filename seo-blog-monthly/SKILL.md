---
name: seo-blog-monthly
description: >
  Monthly SEO blog content generator. Generates 8 publication-ready blog articles per month
  for any brand, with full keyword strategy (Tier 1/2/3), SERP competition analysis, AI
  search visibility check (GEO/AEO), hub-and-spoke internal linking, and brand voice.
  Integrates SE Ranking + Google Search Console + GA4 for fully data-driven topic selection.
  Outputs a formatted DOCX to ~/Downloads. Use this skill whenever the user says things like
  "generate blog content", "monthly blog articles", "write 8 blog posts", "blog content
  strategy", "seo blog", "/seo-blog-monthly", or wants to produce a batch of SEO-optimized
  articles for a website. Also triggers when user provides a URL and asks for content
  generation, blog planning, or monthly content automation.
---

# SEO Blog Monthly Generator

Generates 8 SEO-optimised, interlinked English blog articles for any brand website.
Full pipeline: brand strategy → keyword research → SERP analysis → AI visibility check
→ content writing → DOCX output.

Reference files (read when needed):
- `references/brand-onboarding.md` — client questionnaire and saved profile format
- `references/data-sources.md` — SE Ranking + GSC + GA4 data pull guide and decision framework
- `references/keyword-strategy.md` — Tier system, hub-and-spoke, intent classification
- `references/serp-analysis.md` — what to check before writing each article
- `references/geo-aeo-strategy.md` — writing rules for AI search citation

---

## Step 0 — Parse inputs

| Argument | Example | Default |
|---|---|---|
| `URL` | https://stonedeart.com.my | required |
| `--brand` | "Premium marble supplier, KL" | auto-detected |
| `--month` | "August 2026" | next calendar month |
| `--output` | ~/Documents | ~/Downloads |
| `--format` | `two-column` or `single` | `two-column` |
| `--avoid` | "sintered stone, quartz" | from saved profile |

---

## Step 1 — Brand profile

Read `references/brand-onboarding.md` for the full onboarding process.

**Check for saved profile first:**
Look for `~/.claude/seo-blog-clients/[domain].json`. If it exists, load it and confirm:
> "Using saved brand profile for [domain]. Any updates before I start?"

**If no saved profile:**
- Fetch homepage + about page + product/service pages
- Run the onboarding questionnaire (see `references/brand-onboarding.md`)
- Save answers to `~/.claude/seo-blog-clients/[domain].json` for future runs

The brand profile drives everything: voice, avoid list, pillar pages, CTAs, audience.
A weak brand profile = generic content. Take time here.

---

## Step 2 — Connect data sources

Read `references/data-sources.md` for the full data pull guide and decision framework.

**SE Ranking (required):**
Check if SE Ranking MCP tools are available. If not:
> "This skill uses SE Ranking for live keyword data. Please connect the SE Ranking MCP
> in your Claude settings first, then try again."

If connected: call `PROJECT_listProjects` to find the project matching this domain.
If not found, ask the user which project to use.

**GSC (use if connected to SE Ranking project):**
Call `PROJECT_getGoogleSearchConsole` to pull:
- Top queries by impressions (last 28 days)
- Queries ranked #4–#30 (opportunity zone)
- Queries with > 100 impressions and CTR < 3%
- Queries with clicks but no matching page in sitemap

**GA4 (use if connected):**
Pull top 20 blog posts by sessions + top 5 by conversions + posts with engagement < 1 min.

If GSC or GA4 are not connected, note this and proceed with SE Ranking data only.
Do not stop — SE Ranking alone is sufficient, GSC and GA4 make decisions sharper.

---

## Step 3 — Audit existing content

Fetch `[URL]/post-sitemap.xml` (try `/sitemap_post.xml`, `/blog-sitemap.xml` if 404).
Extract all post URLs and titles. This is the "covered topics" list — never duplicate.

---

## Step 4 — Keyword strategy

Read `references/keyword-strategy.md` for the full Tier system and hub-and-spoke rules.
Read `references/data-sources.md` for the combined decision framework.

From SE Ranking + GSC + GA4 data, build three tiers:

**Tier 1 — Defend** (SE Ranking positions 1–10, or GA4 top traffic pages)
Write cluster content to reinforce, not compete. Link back to the ranking page.

**Tier 2 — Attack** (SE Ranking positions 11–50 + GSC queries with impressions but no page)
Priority: GSC queries with clicks but no dedicated URL → high volume + low KD → buying intent.

**Tier 3 — GEO/AEO** (zero/low volume, but high AI citation value)
Written to be cited by ChatGPT, Perplexity, Google AI Mode — not for organic traffic.
See `references/geo-aeo-strategy.md` for Tier 3 article format.

Check for cannibalization: no two articles share a primary keyword, and no article
targets a keyword already served by an existing post or a page ranking #1–5.

---

## Step 5 — AI visibility check

Read `references/geo-aeo-strategy.md` for the full AI search strategy.

Use SE Ranking AI tools if available:
- `DATA_getAiSearchBrand` — is the brand currently mentioned in AI responses?
- `DATA_getAiSearchPromptsByBrand` — which prompts trigger brand mentions?

Also check manually where needed:
- Which keywords trigger a Google AI Overview?
- Where are competitors getting cited in AI results instead of this brand?

This identifies:
1. Topics to reinforce (brand already appearing — write to strengthen)
2. Topics to attack (competitors appearing — write better content to displace them)
3. Question formats to model the FAQ sections after

---

## Step 6 — Select 8 topics + get confirmation

Choose topics across this distribution:
- **Product / Material deep-dive**: 2 articles (Tier 1 or 2)
- **Design & Lifestyle**: 2 articles (Tier 2 or brand voice)
- **Buyer's Guide / How-to**: 1 article (Tier 2, commercial intent)
- **FAQ / GEO hub article**: 1 article (Tier 3, links to all 7 others)
- **Case Study or Project Story**: 2 articles (E-E-A-T, brand authority)

Rules:
- No topic from the "covered topics" list
- No topic from the `--avoid` list or brand profile avoid list
- Include local market in at least 4 of the 8 primary keywords (if geo-targeted)
- Run intent classification for each topic (see `references/keyword-strategy.md`)

**Present to user before writing:**
Show the 8 topics with: primary keyword, intent type, Tier, rationale.
Wait for confirmation or swaps before proceeding.

---

## Step 7 — SERP analysis (per article)

Read `references/serp-analysis.md` for what to check.

For each of the 8 topics, before writing:
1. Pull SERP data from SE Ranking (`DATA_getSerpResults`, MY region)
2. Check top 3 results: angle, depth, gaps, "People Also Ask"
3. Check for AI Overview, featured snippets
4. Note gaps the client can own (local angle, specific variety, deeper expertise)

This takes time but it's what separates generic content from content that actually ranks.
Document the gap finding for each article — it becomes the writing brief.

---

## Step 8 — Internal linking map

Read `references/keyword-strategy.md` for hub-and-spoke rules.

For each article, define:
- **Pillar page** from brand profile (mandatory link)
- **2–3 existing posts** from sitemap (most thematically related)
- **2 batch cross-links** (to other articles in this month's batch)
- **Contact page** (at least 1 article in the batch)

The FAQ/GEO hub article links to all 7 other batch articles.

Anchor text: descriptive, natural, never "click here". Max 1 link per 300 words.

---

## Step 9 — Write Content Frame + Blog Post

Read `references/geo-aeo-strategy.md` for answer-first structure and quotable sentence rules.

For each of the 8 articles, write both:

### A. Content Frame

```
[Article Title]

Primary Keyword: [keyword] | Search Vol: [X]/mo | Intent: [informational/commercial/transactional]
Secondary Keywords: [kw1], [kw2], [kw3]
SERP Gap to Own: [what the current top results miss that this article will cover]

Intro / Hook:
• Hook: [answer-first — lead with the core insight in 1 sentence]
• Observation: [what the reader is struggling with or noticing]
• Lifestyle / Emotional Angle: [connect to their world — local context]
• Transition: [bridge to body]

---
Section 1 – [Title]
Target Keywords: [keywords]
SERP insight: [what top results say / what gap we fill]
Content Focus:
• [key point]
• [key point — include a quotable statistic or specific fact]
• [key point]
Internal Link → [Anchor text: /destination-url]

---
[Sections 2–5 same format]

FAQ Section (3–5 questions from People Also Ask / AI search prompts):
• Q: [exact question as users ask it]
• Q: [exact question]
• Q: [exact question]

CTA: [Specific action — match brand profile cta_style and cta_location]
```

### B. Blog Post (full article)

Write in brand voice from the saved profile. Structure:

- **H1**: Full title (matches search intent)
- **Answer-first opening**: 2–3 paragraphs answering the core question directly
  (AI systems cite pages that answer immediately — see `references/geo-aeo-strategy.md`)
- **H2 per section** matching Content Frame structure
- 3–4 prose paragraphs per section
- At least 3 quotable statements per article (specific, factual, citable)
- At least one comparison table or structured list
- **FAQ section**: 3–5 H3 questions with direct 2–4 sentence answers
- Specific product/variety names (not generic references)
- Closing CTA from brand profile

Word counts:
| Type | Words |
|---|---|
| Product / Material | 1,800–2,200 |
| Design / Lifestyle | 1,400–1,800 |
| Buyer's Guide | 1,800–2,200 |
| FAQ / GEO hub | 2,000–2,500 |
| Case Study | 1,200–1,500 |

`--avoid` keywords: may appear ONLY as a foil ("unlike sintered stone, natural marble...").
Never explain their benefits. Never recommend them. The article must always conclude in
favour of the client's product.

---

## Step 10 — Generate DOCX

Use the `docx` skill.

**File name:** `[BrandName]_Blog_[MonthYear].docx`
**Save to:** `--output` path (default `~/Downloads/`)

### `--format two-column` (default):
- H1 article title above table (full width)
- Two-column table: Left 40% = Content Frame | Right 60% = Blog Post
- Page break between articles

### `--format single`:
- H1: Article title
- `## Content Frame` then `## Blog Post` sections
- Page break between articles

**Formatting:** Arial 11pt body / 14pt H1 / 12pt H2. Margins 2cm.
Document header: "[Brand] | Blog Content [Month Year]"
Internal links: → [Anchor text: /url]

After saving, confirm file path and size.

---

## Quality checklist

- [ ] Brand profile loaded or completed
- [ ] SE Ranking project identified and keywords pulled
- [ ] GSC data pulled (or noted as not connected)
- [ ] GA4 data pulled (or noted as not connected)
- [ ] Existing posts audited — no topic duplicates
- [ ] Keyword tiers assigned (Tier 1/2/3) for all 8 topics
- [ ] AI visibility checked — gaps and strengths identified
- [ ] Topics confirmed by user before writing
- [ ] SERP analysis done per article — gap identified for each
- [ ] Intent classified for each article (informational / commercial / transactional)
- [ ] Internal linking map complete — no orphan articles
- [ ] Answer-first opening in every article
- [ ] At least 3 quotable statements per article
- [ ] At least one table or list per article
- [ ] FAQ section in every article (questions from PAA / AI search prompts)
- [ ] `--avoid` keywords only as foils — never recommended
- [ ] Brand voice consistent with saved profile
- [ ] DOCX saved with correct filename and path
