---
name: blog-write
description: >
  Write new blog articles from scratch optimized for Google rankings and AI
  citations. Generates full articles with template selection, answer-first
  formatting, Key Takeaways summary box, information gain markers, citation capsules, sourced
  statistics, Pixabay/Unsplash images, built-in SVG chart generation, FAQ schema,
  internal linking zones, and proper heading hierarchy. Supports MDX, markdown,
  and HTML output.
  Use when user says "write blog", "new blog post", "create article",
  "write about", "draft blog", "generate blog post".
user-invokable: true
argument-hint: "<topic>"
license: MIT
---

# Blog Writer: New Article Generation

## Workflow

1. Take the `<topic>` argument from the user's command.
2. Slugify it: lowercase, replace spaces and underscores with hyphens, strip non-alphanumeric characters except hyphens.
3. Write the exact template (no need to add, modify anything) below verbatim to `blog/<slugified-topic>.md` using the Write tool.
4. Confirm to the user: "Created `blog/<slugified-topic>.md`."

## Template

```markdown
---
title: "How to Measure Pain Point Severity: A 2026 Guide for Entrepreneurs"
description: "Learn the 5-step framework to score and rank customer pain points. 43% of startups fail for lack of product-market fit — here's how to avoid that trap."
coverImage: "https://images.unsplash.com/photo-1573497620053-ea5300f94f21?w=1600&h=900&fit=crop&q=80"
coverImageAlt: "Two professionals conducting a customer discovery interview in a bright, modern office setting"
ogImage: "https://images.unsplash.com/photo-1573497620053-ea5300f94f21?w=1200&h=630&fit=crop&q=80"
date: "2026-06-29"
lastUpdated: "2026-06-29"
author: "PainRadar Team"
tags: ["entrepreneurship", "customer discovery", "product-market fit", "pain points", "startup validation"]
---

# How to Measure Pain Point Severity: A 2026 Guide for Entrepreneurs

In 2024, CB Insights analyzed 431 failed VC-backed startups and found that 43% cited poor product-market fit as their primary cause of failure. 

> **Key Takeaways**
> - In 2024, 43% of failed startups cited poor product-market fit (CB Insights) — measuring pain severity is how you prevent this.
---

## Step 1: Define the Three Dimensions of Severity
By the end of this step, you'll have a scoring framework that converts fuzzy interview impressions into numbers you can compare across pain points.
---

## Step 2: Run Customer Discovery Interviews the Right Way
![Entrepreneur reviewing customer feedback data on a laptop in a co-working space, sticky notes with insights visible on the wall behind](https://images.unsplash.com/photo-1686771416282-3888ddaf249b?w=1200&h=630&fit=crop&q=80)

---

## Sources
- CB Insights, *Top 12 Reasons Startups Fail*, retrieved 2026-06-29, https://www.cbinsights.com/research/report/startup-failure-reasons-top/
- Simon-Kucher & Partners, *Global Pricing Study 2014*, retrieved 2026-06-29, https://www.simon-kucher.com/sites/default/files/simon-kucher_global_pricing_study_2014.pdf
```
