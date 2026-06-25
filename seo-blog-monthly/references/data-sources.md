# Data Sources — SE Ranking + GSC + GA4

This skill uses three data sources together to make content decisions.
Pull all three before selecting topics — they tell different parts of the story.

---

## SE Ranking

**What it tells you:** Rankings, keyword difficulty, SERP structure, competitor data, AI visibility

**Key calls:**
- `PROJECT_listProjects` — find the client's project
- `PROJECT_listKeywords` — all tracked keywords with current positions
- `DATA_getDomainKeywords` — full keyword universe for the domain
- `DATA_getSerpResults` — SERP data for a specific keyword (top results, PAA, AI Overview)
- `DATA_getAiSearchBrand` — brand mentions in AI search responses
- `DATA_getAiSearchPromptsByBrand` — which AI prompts trigger brand mentions
- `DATA_getSimilarKeywords` / `DATA_getLongTailKeywords` — expand keyword universe
- `DATA_getKeywordsMetrics` — volume, KD, CPC for specific keywords

**Use for:** Keyword tiers, SERP gap analysis, AI visibility, competitor keyword gaps

---

## Google Search Console (GSC)

**What it tells you:** What users are ACTUALLY searching to find the site right now

**Key data to pull:**
- **Queries with impressions but low CTR** — you're showing up but not getting clicked
  → These are title/meta description problems, not content problems
  → Or the content angle doesn't match search intent
- **Queries with clicks but no dedicated page** — people finding you for keywords you haven't targeted
  → Immediate Tier 2 content opportunities
- **Queries ranked #4–#20** — close to page 1, a cluster article could push them up
- **Pages with declining impressions** — existing content that needs a refresh or cluster support

**GSC integration via SE Ranking:**
Use `PROJECT_getGoogleSearchConsole` if GSC is connected to the SE Ranking project.

**What to look for specifically:**
```
High impressions + low CTR (< 3%) + position 1-10 → Fix title/meta
High impressions + low CTR + position 11-30 → Write cluster article to push to page 1
Queries with clicks → existing pages you haven't officially "targeted" → formalise these
Zero-click queries → informational queries being answered in SERP → write for AI citation
```

**Cross-reference with sitemap:** If GSC shows traffic for a URL but the topic isn't in
your content plan, add it to Tier 1 (defend) immediately.

---

## Google Analytics 4 (GA4)

**What it tells you:** How visitors actually BEHAVE after landing — what content works

**Key metrics to pull for existing blog posts:**
- **Sessions + Engaged sessions** — which posts drive real traffic
- **Average engagement time** — is the content holding attention? (target > 2 min for blog)
- **Scroll depth** — are people reading to the end or bouncing?
- **Conversions / key events** — which posts lead to contact form fills, WhatsApp clicks, etc.
- **Traffic source** — which posts get organic search vs social vs referral

**GA4 integration:** Use `PROJECT_getGoogleSearchConsole` or direct GA4 MCP if connected.

**What to look for specifically:**
```
High traffic + low engagement time → Content doesn't match intent → refresh angle
High engagement + low traffic → Good content, weak keyword targeting → optimise on-page
High traffic + high conversions → Your best performing content → write more like this
High traffic + zero conversions → Informational traffic → add stronger CTA or internal links
Low traffic + high engagement (from referrals) → Content people share → write more of this type
```

---

## Combined Decision Framework

Use all three sources together to make topic decisions:

### Finding Tier 2 topics (attack keywords)

| Signal | Source | Action |
|---|---|---|
| Ranking #11–30 with 100+ impressions/month | GSC + SE Ranking | Write cluster article to push to page 1 |
| Keyword tracked in SE Ranking, no dedicated page | SE Ranking | Write dedicated article |
| GSC query with clicks but no matching page | GSC | Create the page |
| Competitor ranking #1, client not in top 10 | SE Ranking | Outwrite the competitor |

### Finding content to refresh (not new articles)

| Signal | Source | Action |
|---|---|---|
| Page with declining impressions last 3 months | GSC | Refresh + add cluster support |
| Post with high traffic but low engagement time | GA4 | Rewrite with better intent match |
| Post ranking #4–#10 with low CTR | GSC | Fix title/meta description |

### Validating article types to write

Before writing a Case Study or Lifestyle article, check GA4:
- Do existing case studies on the site drive traffic and conversions?
- If yes, write more. If no, reconsider the format.

### Finding GEO/Tier 3 topics

| Signal | Source | Action |
|---|---|---|
| Query appearing in GSC with zero clicks (position 1 but no click) | GSC | AI is answering it — write to be cited |
| Brand NOT mentioned in AI search for a key topic | SE Ranking AI tools | Write Tier 3 article targeting that topic |
| "People Also Ask" questions appearing for your keywords | SE Ranking SERP | Answer them in FAQ sections |

---

## Data pull checklist (run at start of every monthly cycle)

- [ ] SE Ranking: pull all tracked keywords + positions
- [ ] SE Ranking: pull AI search brand mentions
- [ ] GSC: pull top 50 queries by impressions (last 28 days)
- [ ] GSC: pull queries ranked #4–#30 (opportunity zone)
- [ ] GSC: pull queries with > 100 impressions and CTR < 3%
- [ ] GA4: pull top 20 blog posts by sessions (last 28 days)
- [ ] GA4: pull top 5 posts by conversions
- [ ] GA4: flag posts with engagement time < 1 min (content quality issues)
- [ ] Cross-reference: GSC queries with no matching URL on sitemap = new content opportunities
