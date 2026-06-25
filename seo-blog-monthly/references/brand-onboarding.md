# Brand Onboarding — One-Time Setup

Run this questionnaire the FIRST time this skill is used for a new client.
Save answers to `~/.claude/seo-blog-clients/[domain].json` for future runs.

If a saved profile already exists for the domain, load it and skip this section
(just confirm with user: "Using saved brand profile for [domain]. Any updates?")

---

## Questions to ask the client

### 1. Business basics
- What do you sell / what service do you provide?
- What do you NOT sell? (important for --avoid logic)
- Where are your customers located? (city, country, language)
- How long have you been in business?

### 2. Target audience
- Who is your ideal customer? (homeowner, designer, contractor, etc.)
- What is their biggest pain point when looking for your product/service?
- What questions do they always ask before buying?

### 3. Brand voice
- 3 words that describe your brand personality
- 3 words you want to AVOID
- Any competitor you admire for their content (to understand tone benchmark)
- Do you use formal or casual language with customers?

### 4. Content rules
- Any topics that are sensitive or off-limits?
- Any competitor products/materials you don't want to recommend?
- Any claims you cannot legally make?
- Any certifications or awards to mention?

### 5. SEO context
- What are your most important pages? (pillar pages to link to)
- Do you have a Google AI Overview appearance? For which keywords?
- Any keywords you're currently running paid ads on? (avoid cannibalising)

### 6. Showroom / contact info
- Physical location(s) to mention in CTAs
- Preferred CTA style (visit showroom / request quote / WhatsApp us / etc.)
- Contact page URL

---

## Saved profile format

Save to `~/.claude/seo-blog-clients/[domain].json`:

```json
{
  "domain": "stonedeart.com.my",
  "brand_name": "Stone De Art",
  "tagline": "Inspired by nature. Designed for you.",
  "sells": ["marble", "granite", "quartzite", "onyx", "travertine"],
  "does_not_sell": ["sintered stone", "engineered stone", "quartz", "porcelain"],
  "avoid_topics": ["sintered stone benefits", "engineered stone guide"],
  "market": "Klang Valley, Malaysia",
  "audience": ["homeowners", "interior designers", "architects", "contractors"],
  "pain_points": ["not knowing which stone suits their lifestyle", "worried about maintenance"],
  "voice": ["sophisticated", "warm", "knowledgeable"],
  "avoid_tone": ["salesy", "generic", "corporate"],
  "pillar_pages": [
    {"name": "Marble", "url": "/marble/"},
    {"name": "Granite", "url": "/granite/"},
    {"name": "Flooring", "url": "/flooring/"},
    {"name": "Bathroom", "url": "/bathroom/"}
  ],
  "ai_overview_keywords": ["marble malaysia", "quartzite", "granite flooring", "marble walls"],
  "cta_style": "visit showroom",
  "cta_location": "Seri Kembangan, Selangor",
  "contact_url": "/contact-us/",
  "last_updated": "2026-06-25"
}
```
