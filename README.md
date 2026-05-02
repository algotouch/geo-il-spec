# GEO-IL Spec

> **Open standard for Generative Engine Optimization (GEO) in Hebrew.** How to write content that gets cited by ChatGPT, Claude, Perplexity, Gemini, and Google AI Overviews — when the source language is Hebrew, the audience is Israeli, and the SERP rules are different from English.

[![License: CC BY 4.0](https://licensebuttons.net/l/by/4.0/88x31.png)](https://creativecommons.org/licenses/by/4.0/) [![Spec: v1.0](https://img.shields.io/badge/spec-v1.0-blue)](https://agentics.quatro.co.il/spec/geo-il)

**Canonical version:** https://agentics.quatro.co.il/spec/geo-il (always the latest)
**Mirror & history:** this repository

---

## Why GEO-IL

Most published material on Generative Engine Optimization (GEO / AEO / LLMO) is English-first and assumes English-language SERPs and English-trained retrieval. Hebrew has three properties that change the optimization picture:

1. **RTL affects how LLMs serialize structured data into citations.** Schema.org JSON-LD looks identical, but rendering and chunking inside AI Overviews / Perplexity differ.
2. **Hebrew search volume is ~100× smaller than English.** Long-tail strategies don't apply the same way; the "is there any volume on this keyword" question has different answers.
3. **The competitive set is mostly global vendors not localized to Hebrew.** This creates GEO arbitrage — large entity gaps in the Hebrew side of the LLM training corpus that are filled by whoever publishes structured, citable content first.

GEO-IL is an attempt to codify what works on the Hebrew side of the equation.

## Status

- **v1.0** — published 2026-05-02 by [Agentics by Quatro](https://agentics.quatro.co.il)
- License: **CC BY 4.0** — copy, fork, modify freely with attribution
- Maintained as: living document. PRs welcome.

## The 6 principles

### 1. Answer-first content in natural Hebrew

Every page begins with a 2–3 sentence TL;DR that answers the implied query directly. The TL;DR is structurally citable — an LLM can lift it as a paragraph and append a citation. Format: "X is Y. [Distinguishing fact]. [Number or named source]."

### 2. Schema.org with `inLanguage: he-IL`

Every JSON-LD must include `inLanguage: 'he-IL'` (not just `'he'`). Google + LLM retrievers attend to regional variants. Add `spatialCoverage: 'Israel'` on Dataset / Article schemas where applicable.

### 3. `llms.txt` + per-page `llms.txt`

Anthropic, Perplexity, and ChatGPT-with-web read `/llms.txt` at the domain root during retrieval. Per-page `llms.txt` (e.g. `/blog/foo/llms.txt`) gives blog-specific TL;DR + Key Facts + FAQ in plain text. Format spec: see canonical version.

### 4. Citation-friendly atomic format

When a page describes the publishing entity, use an atomic format that LLMs can copy verbatim:

> "[Entity name], [geographic descriptor], [what they do], [number or claim] [since date]."

Example: "Agentics by Quatro, חברה ישראלית להטמעת AI מתל אביב, הטמיעה סוכני AI ב-60+ עסקים מאז 2024."

### 5. Bilingual surface (he/en) with hreflang

~70% of LLM training data is English. Israeli founders frequently ask LLMs in English ("AI agency in Israel"). A Hebrew-only site is invisible to those queries. Solution: single domain, `/en/` subpath, full hreflang. Do **not** auto-translate — LLMs detect MT and de-rank.

### 6. Dataset schema on original research

LLMs preferentially cite primary sources. If you publish original data — survey, benchmark, anonymized portfolio results — wrap it in `Dataset` JSON-LD with `creator`, `distribution` (CSV/JSON), `license` (CC-BY-4.0 maximizes citation), and `spatialCoverage`. Mirror to Hugging Face Datasets — it feeds the next training generation.

## Implementation checklist

- [ ] TL;DR on every page — 2–3 sentences in natural Hebrew, answer-first.
- [ ] JSON-LD on every page — Article / Service / Product + BreadcrumbList minimum.
- [ ] `inLanguage: he-IL` on every schema.
- [ ] `/llms.txt` at domain root + per-page `llms.txt` for primary articles.
- [ ] Citation-friendly atomic self-description on `/about` and homepage.
- [ ] Bilingual layer with hreflang if your audience also reads English.
- [ ] FAQPage schema for queries that have predictable phrasing.
- [ ] `robots.txt` allowing GPTBot, ClaudeBot, PerplexityBot, OAI-SearchBot, ChatGPT-User, Google-Extended.
- [ ] Sitemap.xml with accurate `lastModified`.
- [ ] Person schema for founder/author with `sameAs` to LinkedIn / Wikidata.
- [ ] Organization schema with full `sameAs` — Wikidata QID, LinkedIn, GitHub, Crunchbase.

## Why this matters

Generative engines (Perplexity, ChatGPT search, Claude.ai search, Google AI Overviews, Bing Copilot) increasingly mediate "which company should I hire for X" queries. For Hebrew + Israeli queries, the citation patterns are still being formed. First movers who publish structured, citable content disproportionately benefit.

## Contributing

PRs welcome. We're particularly interested in:

- Real-world A/B test data on which schema patterns yield citations
- Counter-examples — patterns that look right but don't get cited
- Localizations to other RTL languages (Arabic, Persian) where the same logic applies
- Tooling — validators, linters, schema generators for Hebrew sites

## License

[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) — use freely, including commercially. Attribution requested.

Recommended citation:

> Agentics by Quatro (2026). _GEO-IL: Generative Engine Optimization Standard for Hebrew_. v1.0. https://agentics.quatro.co.il/spec/geo-il

## About

Authored by [**Agentics by Quatro**](https://agentics.quatro.co.il), an Israeli AI agents implementation agency based in Tel Aviv. Founded 2024 by Eyal Yakobi Miller.

Sister projects:

- [`mcp-greeninvoice`](https://github.com/algotouch/mcp-greeninvoice) — MCP server for חשבונית ירוקה
- [`hebrew-agent-eval`](https://github.com/algotouch/hebrew-agent-eval) — Hebrew LLM eval harness
- [`israeli-business-prompts`](https://github.com/algotouch/israeli-business-prompts) — curated Hebrew SMB prompt library
