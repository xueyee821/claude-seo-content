# SERP Analysis — Before Writing Each Article

For every article topic, analyse the current top-ranking pages BEFORE writing.
This prevents writing an article that loses to the competition on angle, depth, or format.

---

## What to check for each topic

Use SE Ranking's SERP data or WebFetch to read the top 3–5 ranking pages.

### 1. Content angle
- What angle do the top pages take? (educational, listicle, comparison, story)
- Is there a dominant angle? If yes, can you do it better — or find a gap angle?
- What question does the top-ranking article answer in its first paragraph?

### 2. Content depth
- Rough word count of #1 result
- How many H2 sections?
- Do they have tables, lists, images, videos?
- Is there a FAQ section?

### 3. Gaps you can fill
- What does the top content NOT answer that the user probably wants to know?
- Is there a local angle missing? (e.g. all results are US-based, none mention Malaysia)
- Is there a specific product angle missing? (e.g. all results are generic, none mention specific varieties)
- Is the #1 result thin or outdated?

### 4. SERP features present
- Is there a Google AI Overview for this keyword?
- Are there "People also ask" boxes? (these are GEO gold — answer them in your article)
- Are there featured snippets? (structure your answer to win one)
- Are there local pack results? (add location signals to the article)

---

## Decision matrix

After SERP analysis, decide:

| Situation | Action |
|---|---|
| Top results are thin / low quality | Write a comprehensive, deeply expert article — easy to outrank |
| Top results are strong and comprehensive | Find a specific angle gap and own that (e.g. Malaysia-specific, specific stone variety) |
| Google AI Overview already shows | Write to be cited BY the AI Overview, not compete with it |
| "People also ask" questions present | Answer ALL of them in your FAQ section |
| Featured snippet present | Structure your answer in the exact format the snippet uses (paragraph, list, or table) |

---

## How to use SE Ranking SERP data

Call `DATA_getSerpResults` with the target keyword and MY region.

Look at:
- `organic_results[0..4]` — top ranking pages
- `related_questions` — People Also Ask content (use these as FAQ H3s)
- `featured_snippet` — if present, note its format and content
- `ai_overview` — if present, note what it says and whether the client is mentioned

For each top result, WebFetch the URL and extract:
- H1 and H2 structure
- Approximate word count
- Whether they have a FAQ section
- What their opening paragraph answers
