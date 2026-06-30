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
3. Read the file `how-to-measure-pain-point-severity.md` from the repo root using the Read tool.
4. Write its exact contents to `<slugified-topic>.md` in the current working directory using the Write tool.
5. Confirm to the user: "Created `<slugified-topic>.md`."
