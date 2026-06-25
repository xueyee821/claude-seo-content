# claude-seo-content

Reusable Claude Code skills for SEO & content automation.

---

## Skills

### `/seo-blog-monthly` — Monthly Blog Content Generator

Generates 8 SEO-optimised, interlinked English blog articles per month for any brand website. Outputs a formatted DOCX to your Downloads folder.

**Features:**
- Auto-detects brand voice and products from the website
- Uses SE Ranking for live keyword data (Tier 1/2/3 architecture)
- Avoids duplicating existing blog posts (reads your sitemap)
- GEO/AEO optimised — answer-first structure for AI search citation
- Internal linking map — no orphan articles
- Two-column format (Content Frame + Blog Post) or single-column

**Requirements:**
- [Claude Code](https://claude.ai/code)
- SE Ranking account with MCP connected

**Install:**
```bash
claude install https://github.com/xueyee821/claude-seo-content/raw/main/seo-blog-monthly.skill
```

**Usage:**
```bash
# Basic
/seo-blog-monthly https://yourwebsite.com

# With options
/seo-blog-monthly https://yourwebsite.com --brand "Premium marble supplier, KL" --month "August 2026"

# Avoid certain topics
/seo-blog-monthly https://yourwebsite.com --avoid "sintered stone, engineered stone"

# Single-column output
/seo-blog-monthly https://yourwebsite.com --format single
```

---

## Coming Soon

- `/seo-content-brief` — Single article brief generator
- `/seo-cluster` — Topic cluster planner with pillar page mapping
- `/seo-monthly-report` — Monthly SE Ranking performance report

---

Made with [Claude Code](https://claude.ai/code)
