---
name: seo-blog-monthly
description: >
  Monthly SEO blog content generator. Generates 8 publication-ready blog articles per month
  for any brand, optimized for GEO/AEO (AI search citation), internal linking, and keyword
  clusters. Outputs a formatted DOCX to ~/Downloads. Use this skill whenever the user says
  things like "generate blog content", "monthly blog articles", "write 8 blog posts", "blog
  content strategy", "seo blog", "/seo-blog", or wants to produce a batch of SEO-optimized
  articles for a website. Also triggers when user provides a URL and asks for content generation,
  blog planning, or monthly content automation.
---

# SEO Blog Monthly Generator

Generates 8 SEO-optimised, interlinked English blog articles for any brand website. Output
is a DOCX file saved to ~/Downloads (or a path the user specifies).

---

## Step 0 — Parse inputs

Accept these arguments (all optional except URL):

| Argument | Example | Default |
|---|---|---|
| `URL` | https://stonedeart.com.my | required |
| `--brand` | "Premium marble supplier, KL" | auto-detected |
| `--month` | "August 2026" | next calendar month |
| `--output` | ~/Documents | ~/Downloads |
| `--format` | `two-column` or `single` | `two-column` |
| `--avoid` | "sintered stone, quartz" | none |

If `--brand` is not provided, fetch the homepage and about page to infer:
- What the company sells / specialises in
- Target audience
- Geographic market
- Brand tone (formal, warm, technical, lifestyle)
- Products or categories NOT sold (if detectable)

Summarise your brand inference and confirm with the user before proceeding if brand
information is ambiguous.

---

## Step 1 — Connect SE Ranking

This skill requires SE Ranking MCP to be connected for keyword data.

Check if SE Ranking MCP tools are available (look for `mcp__*seranking*` or similar tools
in your tool list). If they are not connected:

> "This skill uses SE Ranking for live keyword data. Please connect the SE Ranking MCP in
> your Claude settings first, then try again."

Stop here if SE Ranking is not connected.

If connected, find the project matching the user's URL:
- Call `PROJECT_listProjects` or equivalent to list available projects
- Match by domain name
- If no matching project found, ask the user: "I couldn't find a SE Ranking project for
  [domain]. Which project should I use?"

---

## Step 2 — Audit existing content

Fetch `[URL]/post-sitemap.xml` (try also `/sitemap_post.xml`, `/blog-sitemap.xml` if the
first 404s). Extract all existing post URLs and titles.

Build a "covered topics" list. Use this to filter out duplicates when selecting new topics.

---

## Step 3 — Keyword research

Pull keyword data from SE Ranking for this domain:

1. Get domain's tracked keywords and their current positions
2. Identify keyword gaps: real search volume + low difficulty + no dedicated existing content
3. Note which keywords the domain already ranks for (positions 1–10) — write cluster content
   to reinforce these, not compete with them
4. Note keywords ranked 11–50 — high-priority targets for new content

Group findings into:
- **Tier 1** — Already ranking well (defend with cluster content)
- **Tier 2** — Gap keywords with real search volume (attack)
- **Tier 3** — Zero/low volume, but valuable for AI citation (GEO/AEO content)

---

## Step 4 — Select 8 topics

Choose topics that:
- Are NOT already covered by existing posts
- Are NOT in the `--avoid` list (if provided)
- Represent a balanced monthly distribution:
  - **Material / Product deep-dive**: 2 articles
  - **Design & Lifestyle**: 2 articles
  - **Buyer's Guide / How-to**: 1 article
  - **FAQ / GEO (AI citation)**: 1 article
  - **Case Study or Project Story**: 2 articles

Priority order within each category:
1. Tier 2 keywords with clear buying intent
2. Tier 3 GEO topics (for AI visibility)
3. Brand voice / lifestyle content

Include the user's local market in at least 4 of the 8 primary keywords if the business
is geo-targeted.

Present the 8 selected topics with primary keyword and rationale before writing. Let the
user confirm or swap topics.

---

## Step 5 — Assign internal linking

For each article, define:
- **Pillar page link** — which key service/category page on the site this article supports
- **2–3 existing blog post links** — most thematically related from the sitemap
- **2 cross-links to other batch articles** — no article is an island

The FAQ/GEO article should reference all 7 other batch articles.

Anchor text must be descriptive (the destination's primary keyword where natural). No
"click here" or "read more". Max 1 link per 300 words.

---

## Step 6 — Write Content Frame + Blog Post

For each of the 8 articles, write:

### A. Content Frame (structured outline)

```
[Article Title]

Focus Keywords: [primary], [secondary 1], [secondary 2], [long-tail]
Target Keywords: [2–3 keywords]

Intro / Hook:
• Hook: [answer-first opening — lead with the key insight]
• Observation: [what the reader notices or struggles with]
• Lifestyle / Emotional Angle: [connect to reader's world]
• Transition: [bridge to body content]

---
Section 1 – [Title]
Target Keywords: [keywords]
Content Focus:
• [key point]
• [key point]
• [key point]
Internal Link → [Anchor text: /destination-url]

---
[Sections 2–5 in the same format]

CTA: [Specific call to action — e.g. visit showroom, request quote, view collection]
```

### B. Blog Post (full article)

Write in the brand's voice (inferred or provided). Structure:
- **H1**: Full article title
- **Answer-first opening**: 2–3 paragraphs that directly answer the core question (GEO
  optimised — AI systems cite pages that answer questions immediately)
- **H2 per section** matching the Content Frame
- 3–4 prose paragraphs per section
- At least one comparison table or structured list per article
- **FAQ section** at the end: 3–5 H3 questions with short, direct answers (AEO)
- Specific product/material names throughout (not generic references)
- Closing CTA

Target word counts by article type:
| Type | Words |
|---|---|
| Product / Material | 1,800–2,200 |
| Design / Lifestyle | 1,400–1,800 |
| Buyer's Guide | 1,800–2,200 |
| FAQ / GEO | 2,000–2,500 |
| Case Study | 1,200–1,500 |

---

## Step 7 — Generate DOCX

Use the `docx` skill to produce the output file.

**File name:** `[BrandName]_Blog_[MonthYear].docx`
Example: `StoneDéArt_Blog_August2026.docx`

**Save to:** `--output` path (default `~/Downloads/`)

### If `--format two-column` (default):

One table per article:
- Left column (40%): Content Frame
- Right column (60%): Blog Post
- H1 article title above the table (full width)
- Page break between articles

### If `--format single`:

Each article as a continuous section:
- H1: Article title
- `## Content Frame` subsection (the outline)
- `## Blog Post` subsection (the full article)
- Page break between articles

**DOCX formatting for both modes:**
- Font: Arial — 11pt body, 14pt H1, 12pt H2
- Page margins: 2cm all sides
- Document title header: "[Brand] | Blog Content [Month Year]"
- Internal links shown as: → [Anchor text: /url]

After generating, confirm the file path and size.

---

## Quality checklist (run before delivering)

- [ ] No topic overlaps with existing sitemap posts
- [ ] Every article has a primary keyword from SE Ranking data (or Tier 3 GEO rationale)
- [ ] Every article links to a relevant pillar/service page
- [ ] Every article links to 2–3 existing posts
- [ ] Every article cross-links to 2 other batch articles
- [ ] FAQ section in every article
- [ ] Answer-first opening in every article
- [ ] At least one table or structured list per article
- [ ] Local/market context present where relevant
- [ ] `--avoid` keywords only appear as foils if mentioned at all — never recommended
- [ ] Brand voice consistent throughout
- [ ] DOCX saved to correct path with correct filename
