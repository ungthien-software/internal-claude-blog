---

## name: blog-write
description: >
  Write new blog articles from scratch optimized for Google rankings and AI
  citations. Generates full articles with template selection, answer-first
  formatting, Key Takeaways summary box, information gain markers, citation
  capsules, sourced statistics, Pixabay/Unsplash images, FAQ schema, internal
  linking zones, and proper heading hierarchy. Supports MDX, markdown, and HTML
  output.
  Use when user says "write blog", "new blog post", "create article",
  "write about", "draft blog", "generate blog post".
user-invokable: true
argument-hint: ""
license: MIT



# Blog Writer: New Article Generation

Writes complete blog articles from a topic, brief, or outline, optimized for
Google rankings and AI citations.

**Key references** (paths relative to repo root; references live in the
main `blog` skill's references directory, not in `blog-write/`):

- `skills/blog/references/synthesis-contract.md`: 6 LAWs for synthesis output (applies whenever the article embeds research-synthesis prose)
- `skills/blog/references/content-templates.md`: Template selection guide and usage
- `skills/blog/references/quality-scoring.md`: 5-category scoring (Content 30, SEO 25, E-E-A-T 15, Technical 15, AI Citation 15)
- `skills/blog/references/eeat-signals.md`: Experience, expertise, authority, trust markers
- `skills/blog/references/internal-linking.md`: Linking strategy and anchor text rules



## Workflow



### Phase 0: Surface Targeting

By default, target three surfaces: (1) owned-site organic Google ranking,
(2) SERP including AI Overviews, and (3) AI-assistant citations (ChatGPT,
Perplexity, Claude, Gemini, Copilot). This shapes structure, citation density,
and answer-first formatting throughout.

### Phase 1: Topic Understanding

This skill runs autonomously from start to finish. Do NOT stop to ask the user
questions. Infer all inputs from the topic and any project context:

- **Target audience / search intent** - Infer from the topic and primary keyword.
- **Primary keyword** - Derive from the topic phrasing.
- **Word count** - Default to 2,000-2,500 words unless the topic implies otherwise.
- **Platform/format** - Auto-detect from the project (MDX, markdown, HTML); default
  to markdown if none is detected.
- **If a brief exists** - Load it and use it as the source of truth.



### Phase 1.5: Template Selection

Select the appropriate content template from the 12 templates in
`skills/blog/templates/` (the main `blog` skill owns the templates directory).

1. **Auto-detect content type** from the topic and search intent:

  | Signal                                    | Template             |
  | ----------------------------------------- | -------------------- |
  | "How to...", process, steps               | `how-to-guide`       |
  | "Best X", "Top N", list format            | `listicle`           |
  | Client result, before/after, metrics      | `case-study`         |
  | "X vs Y", comparison, alternatives        | `comparison`         |
  | Broad topic, comprehensive guide          | `pillar-page`        |
  | "Is X worth it", product evaluation       | `product-review`     |
  | Opinion, prediction, industry take        | `thought-leadership` |
  | Expert quotes, multi-source collection    | `roundup`            |
  | Code walkthrough, tool demo, technical    | `tutorial`           |
  | Breaking news, algorithm update, event    | `news-analysis`      |
  | Survey results, experiment, original data | `data-research`      |
  | Q&A, knowledge base, "What is X"          | `faq-knowledge`      |

2. **Load the matching template**: Read from `skills/blog/templates/<type>.md`
3. **Adapt the outline** - Use the template's section structure, heading patterns,
  and word count guidance to shape Phase 3's outline
4. **Fallback** - If no template clearly fits, use the generic outline structure
  in Phase 3 below. Inform the user which template was selected (or that none matched).

See `skills/blog/references/content-templates.md` for detailed selection criteria.

### Phase 2: Research

Spawn a `blog-researcher` agent (or do inline research with web_search):

1. **Find 8-12 current statistics** (2025-2026 data preferred)
  - Search: `[topic] study 2025 2026 data statistics`
  - Prioritize tier 1-3 sources (see `skills/blog/references/quality-scoring.md`)
  - Record: statistic, source name, URL, date, methodology
2. **Find a cover image** (wide, high-quality, topic-relevant, 1200x630 OG-compatible):
  - Search `site:pixabay.com [topic] wide banner` (preferred), then
   `site:unsplash.com [topic] wide`, then `site:pexels.com [topic] wide` as fallback
3. **Find 3-5 inline images** from open-source platforms:
  - **Pixabay** (preferred): `site:pixabay.com [topic keywords]`, verify a direct
   CDN URL returns HTTP 200 via `curl -sI "<url>" | head -1`
  - **Unsplash** (alternative): `https://images.unsplash.com/photo-<id>?w=1200&h=630&fit=crop&q=80`
  - **Pexels** (fallback): `site:pexels.com [topic keywords]`



### Phase 3: Outline Generation

Create a structured outline before writing. If a template was loaded in Phase 1.5,
adapt this skeleton to match the template's section structure:

```
# [Title as Question - Include Primary Keyword]

## Introduction (100-150 words)
- Hook with surprising statistic
- Problem/opportunity statement
- What the reader will learn

> **Key Takeaways**
> - [Core finding with statistic and source]
> - [Second key insight or recommendation]
> - [Third actionable takeaway]
> (3-5 bullets, 40-60 words combined)

## H2: [Question Format] (300-400 words)
- Answer-first paragraph (40-60 words with stat + source)
- Supporting evidence
- [Image placement]
- Practical advice
- [CITATION CAPSULE placeholder]
- [INTERNAL-LINK: anchor text → target description]

## H2: [Question Format] (300-400 words)
- Answer-first paragraph
- Analysis and implications
- [CITATION CAPSULE placeholder]
- [INTERNAL-LINK: anchor text → target description]

## H2: [Statement for Variety] (300-400 words)
- Answer-first paragraph
- Real-world example or case study
- [Image placement]
- [CITATION CAPSULE placeholder]

## H2: [Question Format] (300-400 words)
- Answer-first paragraph
- Step-by-step guidance
- [CITATION CAPSULE placeholder]
- [INTERNAL-LINK: anchor text → target description]

## H2: [Question Format] (200-300 words)
- Answer-first paragraph
- Forward-looking analysis

## [CTA Section or Inline Placement]
- See `skills/blog/references/cta-placement.md` for placement rules by content type
- Place CTA after value delivery, not at arbitrary positions
- Single focused CTA per post (266% more conversions)
- [CTA: contextual call-to-action matching article topic]

## FAQ Section (3-5 questions, 40-60 words each answer)
- [INTERNAL-LINK: anchor text → detailed content]

## Conclusion (100-150 words)
- Key takeaways (bulleted)
- Call to action
- [INTERNAL-LINK: anchor text → next logical content]
```

Build the outline internally and proceed directly to writing - do not pause for
user approval.

**Visual element pacing**: Insert `[IMAGE]` or `[CALLOUT]` markers every 300-500
words, alternating types. See `skills/blog/references/cta-placement.md` for CTA
positioning.

### Phase 4: Content Writing

**Output file (REQUIRED):** Write the finished article to `blog/<slug>.md` relative
to the current working directory, where `<slug>` is the slugified topic:

- Lowercase the topic.
- Replace every run of non-alphanumeric characters (spaces, punctuation) with a
  single hyphen `-`.
- Strip leading/trailing hyphens.
- Example: topic `"How AI Overviews Change SEO in 2026!"` -> `blog/how-ai-overviews-change-seo-in-2026.md`.

Use exactly this path and filename - do not add dates, subfolders, or other
prefixes. A downstream program parses the printed path (see Phase 6), so it must be
correct and match the file actually written.

Write the full article following these rules:

#### 4a. Frontmatter

```yaml
---
title: "[Question-format title with primary keyword]"
description: "[Fact-dense, 150-160 chars, includes 1 statistic]"
coverImage: "[URL from Pixabay/Unsplash/Pexels]"
coverImageAlt: "[Descriptive sentence about the cover image]"
ogImage: "[Same as coverImage, or custom OG image URL]"
date: "YYYY-MM-DD"
lastUpdated: "YYYY-MM-DD"
author: "[Author name]"
tags: ["keyword1", "keyword2", "keyword3"]
---
```

If the platform uses a different field name (e.g., `image`, `hero`, `thumbnail`),
adapt to match the project's existing frontmatter convention.

#### 4b. Summary Box (Key Takeaways)

Immediately after the introduction (before the first H2 body section), add a summary box:

```markdown
> **Key Takeaways**
> - [Core finding with statistic] ([Source], year)
> - [Second key insight or recommendation]
> - [Third actionable takeaway]
```

Requirements:

- 3-5 bullet points, 40-60 words combined
- Must be self-contained - understandable without reading the article
- Include 1 specific statistic with source name
- State the key finding, recommendation, or answer
- Default label: "Key Takeaways". If a persona is active, use the persona's summary_label
- Backward compatible: accept existing TL;DR boxes during rewrites



#### 4c. Answer-First Formatting (Critical)

Every H2 section MUST open with a 40-60 word paragraph containing:

- At least one specific statistic with source attribution
- A direct answer to the heading's implicit question

Pattern:

```markdown
## How Does X Impact Y in 2026?

[Stat from source] ([Source Name](url), year). [Direct answer to the heading
question in 1-2 more sentences, explaining the implication and what this means
for the reader.]
```

**FLOW evidence triple (drafting requirement, not just audit):**

Every public statistic must carry three components AT DRAFTING TIME:

1. **Year anchor in prose.** Write "In 2026," or "As of Q1 2026," BEFORE
  the statistic, in the sentence body. Year buried inside parentheses
   does not count. Example:
  - GOOD: "In 2026, Ahrefs found a 58% lower CTR for position one when
  an AI Overview was present."
  - WEAK: "Position-one CTR dropped 58% (Ahrefs, 2026)."
2. **Inline citation with publisher and title.** Name both the publisher
  and the document title (or report name), not just a brand. Example:
  - GOOD: "Ahrefs, AI Overviews CTR update, December 2025"
  - WEAK: "Ahrefs reported..."
3. **URL plus retrieval date in the source block at the bottom of the post.**
  Provenance discipline lets future readers and AI crawlers verify the
   source still says what was claimed. Format:
  - "[Publisher], [Title], retrieved YYYY-MM-DD, [full URL]"

**FLOW quality bar (drop or replace):**
Public claims must use verified sources OR stay qualitative. If a statistic
cannot be verified, drop it. If it is contradicted by a more recent source,
replace it with the verified alternative. Do not soften vague language to
keep an unsourceable number.

For evidence-led optimization prompts (CTR audit, AI detector test, schema,
PAA rewording, ChatGPT visibility), see `/blog flow optimize`.

#### 4d. Information Gain Markers

Distribute at least 2-3 information gain markers throughout the article. These
signal to search engines and AI systems that the content contains original value
not available elsewhere.

Tag each with a comment or visible marker:

- `[ORIGINAL DATA]` - Proprietary surveys, experiments, A/B test results, case
study metrics the author collected first-hand
- `[PERSONAL EXPERIENCE]` - First-hand observations, lessons learned from direct
involvement, "when we tried X, Y happened" narratives
- `[UNIQUE INSIGHT]` - Analysis others haven't made, contrarian perspectives
backed by data, novel connections between existing research

Placement:

- Weave into the body text naturally
- Use as inline comments: `<!-- [ORIGINAL DATA] -->` before the relevant paragraph
- Or as visible callouts if the format supports it:
  ```markdown
  > **Our finding:** [original observation backed by specific data]
  ```
- Minimum 2 per post, target 3 for comprehensive articles

These markers map directly to the "Originality/unique value markers" criterion
in the Content Quality scoring category (see `skills/blog/references/quality-scoring.md`).

#### 4e. Citation Capsules

For each major H2 section, generate a citation capsule - a 40-60 word self-contained
passage designed so AI systems can extract and quote it directly.

Requirements per capsule:

- 40-60 words, self-contained (makes sense in isolation)
- Contains: one specific claim + one data point + source attribution
- Written in a declarative, quotable style
- Placed within the H2 section body (not as a separate block)

Example:

```markdown
According to a 2026 Gartner study, 58% of enterprise buyers now consult AI
assistants before contacting a vendor ([Gartner](https://www.gartner.com), 2026).
This shift means B2B content must answer specific questions concisely enough
for AI systems to extract and cite in their responses.
```

Capsules map to the "AI Citation Readiness" scoring category (15 points) in
`skills/blog/references/quality-scoring.md`.

#### 4f. Internal Linking Zones

Mark internal linking opportunities throughout the article using placeholder
notation. The user (or a follow-up pass) will resolve these to actual URLs.

Zone placement:

- **Introduction** - Link to related pillar content or topic hub
- **Each H2 section** - Link to supporting articles, deeper dives, related tools
- **FAQ section** - Link answers to detailed content that expands on the answer
- **Conclusion** - Link to the next logical piece of content the reader should consume

Format:

```markdown
[INTERNAL-LINK: anchor text → target description]
```

Example:

```markdown
For a deeper dive into keyword clustering, see our
[INTERNAL-LINK: complete guide to keyword clustering → pillar page on keyword research methodology].
```

Target 5-10 internal link zones per 2,000-word post. Use descriptive anchor text
(never "click here" or "read more"). See `skills/blog/references/internal-linking.md` for
anchor text rules and linking strategy.

#### 4g. Paragraph Rules

- Every paragraph: 40-80 words (never exceed 150)
- Every sentence: max 15-20 words
- Start each paragraph with the most important information
- Target Flesch Reading Ease: 60-70



#### 4h. Heading Rules

- One H1 (title only)
- H2s for main sections (60-70% as questions)
- H3s for subsections only - never skip levels
- Include primary keyword naturally in 2-3 headings



#### 4i. Image Embedding

```markdown
![Descriptive alt text - topic keywords naturally](https://cdn.pixabay.com/photo/...)
```

- Place images after H2 headings, before body text
- Space evenly throughout the post (not clustered)
- Alt text should be a full descriptive sentence



#### 4j. Citation Format

Inline attribution (always):

```markdown
Organic CTR declined 61% with AI Overviews ([Seer Interactive](https://www.seerinteractive.com/), 2025).
```



#### 4k. FAQ Section

Add 3-5 FAQ items with 40-60 word answers. Each answer must contain a statistic.

For MDX with FAQSchema component:

```mdx
<FAQSchema faqs={[
  { question: "Question?", answer: "40-60 word answer with statistic and source." },
]} />
```

For standard markdown:

```markdown
## Frequently Asked Questions

### Question text here?

Answer with statistic and source attribution (40-60 words).
```



### Phase 5: Quality Check

Before delivering, verify:

#### Structure and Content

1. Every H2 opens with a statistic + source
2. No paragraph exceeds 150 words
3. All statistics have named tier 1-3 sources
4. 3-5 inline images with descriptive alt text
5. Cover image present in frontmatter (coverImage + ogImage)
6. FAQ section present with 3-5 items
7. Heading hierarchy is clean (H1 -> H2 -> H3)
8. Meta description is 150-160 chars with a stat



#### New Element Verification

1. TL;DR box present after introduction (40-60 words, contains statistic + source)
2. At least 2-3 information gain markers (`[ORIGINAL DATA]`, `[PERSONAL EXPERIENCE]`, or `[UNIQUE INSIGHT]`)
3. Citation capsules present in major H2 sections (40-60 words, self-contained, quotable)
4. Internal linking zones marked in introduction, H2 sections, FAQ, and conclusion
5. No AI-detectable phrases from banned list (see `agents/blog-writer.md`)



#### Burstiness and Naturalness Check

1. **Sentence length variance** - Verify a mix of short (8-word) and long (25-word) sentences. Uniform sentence length signals AI authorship.
2. **Banned AI phrase scan** - Check for and remove:
  - "in today's digital landscape", "it's important to note", "dive into"
    - "game-changer", "navigate the landscape", "revolutionize", "seamlessly"
    - "cutting-edge", "harness the power of", "leverage" (as verb)
    - "delve", "crucial", "elevate", "foster", "landscape" (overused)
    - "multifaceted", "robust", "tapestry", "embark"
    - Full list in `agents/blog-writer.md`
3. **Contractions** - Verify natural use of contractions ("it's", "we've", "don't", "isn't"). Formal AI prose avoids contractions; natural writing uses them.
4. **Rhetorical questions** - Verify at least one rhetorical question every 200-300 words to break up declarative patterns.



### Phase 5.5: Delivery Contract Enforcement (simplified)

Before Phase 6, run a lightweight subset of the delivery contract
(`skills/blog/references/blog-delivery-contract.md`). The user is never the first
reviewer; the gates are.

Steps:

1. **Hero image**: if `nanobanana-mcp` is loaded, generate the hero via the MCP tool.
  Otherwise run `python scripts/generate_hero.py --topic "<title>" --tags "<tags>" --out <folder>`
   (uses the Gemini, Unsplash, Pexels, Pixabay, Openverse ladder). The hero is the
   cover/OG image.
2. **Content review (blocking)**: dispatch the `blog-reviewer` agent (Task tool)
  against the canonical `.md`. The agent emits its scorecard to `<folder>/review.md`
   ending with `BLOCKING: true|false (reason)`. Threshold: overall score 90/100 or
   higher AND zero P0 issues per `editorial-heuristics.md`.
3. **Asset + link integrity**: run `python scripts/blog_preflight.py --draft <folder>`
  to check assets and links (Gate 5). Exit 0 = ship; exit 1 = block.
   (PDF rendering and multi-viewport visual verification are intentionally skipped
   in this simplified flow.)
4. **Iteration**: on any block, capture the failure diagnostic from
  `<folder>/preflight-report.json`, re-dispatch the blog-writer agent with the
   diagnostic as input, and re-run from step 1. Maximum 3 iterations. On the 3rd
   failure, STOP and present the failure diagnostic instead of the draft.

The orchestrator holds the loop counter; this sub-skill never loops itself.

### Phase 6: Delivery

Present the completed article ONLY after Phase 5.5 returns all gates passing.

Summary template:

```
## Blog Post Complete: [Title]

### Template Used
- [Template name] (or "generic outline - no template matched")

### Statistics
- [N] sourced statistics from tier 1-3 sources
- [N] unique sources cited

### Visual Elements
- Cover image: [source - Pixabay/Unsplash/Pexels]
- [N] inline images (Pixabay/Unsplash/Pexels)

### Dual-Optimization Elements
- TL;DR box: present (N words)
- Information gain markers: [N] ([types used])
- Citation capsules: [N] across H2 sections
- Internal linking zones: [N] marked

### Structure
- [N] H2 sections with answer-first formatting
- [N] FAQ items with schema
- Word count: ~[N] words
- Estimated reading time: [N] min

### Naturalness
- Sentence length variance: [pass/fail]
- AI phrase scan: [pass/fail]
- Contractions used: [yes/no]
- Rhetorical questions: [N] (target: 1 per 200-300 words)

### Next Steps
- Review and customize for your brand voice
- Resolve [INTERNAL-LINK] placeholders with actual URLs
- Add internal links to your existing content
- Run `/blog analyze <file>` to verify quality score
- Generate schema markup: `/blog schema <file>`
```

**Final step (MUST DO - IMPORTANT):** The article must be saved to
`blog/<slug>.md` if not saved yet. Then print the output path to stdout on its own
line, in exactly this format so a downstream program can parse it:

```
BLOG_FILE: blog/<slug>.md
```

Rules for this line:
- Print the literal prefix `BLOG_FILE: ` followed by the exact path written in Phase 4.
- One path only, on its own line, with no surrounding quotes, backticks, or extra text.
- The printed path MUST match the file that was actually written - the program uses
  this line to locate the file, so any mismatch breaks it.