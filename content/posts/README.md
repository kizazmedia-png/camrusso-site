# Insights — Post Authoring Guide

This directory holds the markdown source files for the blog at `/insights.html`.

The HTML pages under `/insights/` and the post list inside `insights.html` are
generated from these files by Claude Code on demand. There is no SSG, no build
tool, and no Node/Python toolchain to install — when you've added or edited a
post, ask Claude Code to **"regenerate the blog"** (or run the prompt you used
the first time) and it will rebuild `insights.html` and the per-post HTML files
from whatever lives here.

---

## File naming

One markdown file per post. The filename (minus the `.md`) becomes the URL slug.

  `content/posts/geo-vs-seo-2026.md`  →  `/insights/geo-vs-seo-2026.html`

Use lowercase, hyphenated slugs. No spaces, no underscores, no capital letters.

## Required front matter

Each file must start with a YAML front matter block delimited by `---`:

```markdown
---
title: "The Post Title"
date: 2026-05-21
excerpt: "A 1–2 sentence summary shown on the blog index."
cover_image: cover.jpg     # optional, relative to assets/insights/
---
```

Fields:

- **title** (required) — string. The post title. Wrap in quotes if it contains
  punctuation like colons.
- **date** (required) — ISO date (`YYYY-MM-DD`). Posts on `insights.html` are
  sorted newest first by this field.
- **excerpt** (required) — 1–2 sentence summary shown on the blog index. Keep
  it tight; long excerpts are clamped to two lines visually.
- **cover_image** (optional) — filename inside `assets/insights/`. If omitted,
  the post renders without a hero image. Drop the image file into
  `assets/insights/` before regenerating.

If front matter is missing or malformed, the build will skip that file and warn
in the regeneration output. It will not break the rest of the blog.

## Body format

Standard GitHub-flavored markdown, including:

- Headings: use `##` for section headings and `###` for sub-sections. (Do not
  use `#` — that's reserved for the post title from front matter.)
- Bold (`**…**`), italic (`*…*`), and inline `code`.
- Fenced code blocks with language hints (` ```js `, ` ```bash `, etc.).
- Lists, blockquotes, tables, and strikethrough.
- Bare URLs auto-link.

Em-dashes (`—`) are preserved verbatim. Quote characters are not auto-converted
to smart quotes — type the curly quote directly if you want curly quotes.

## Images inside a post

Reference images with standard markdown:

```markdown
![Descriptive alt text](../assets/insights/my-chart.png)
```

Store images in `assets/insights/`. If you provide alt text, it will render as
a `<figcaption>` underneath the image with the site's editorial styling.

## Publishing checklist

1. Write the post as `content/posts/[slug].md` with valid front matter.
2. Drop any images into `assets/insights/`.
3. Ask Claude Code to regenerate the blog.
4. Verify `insights.html` shows the new post and `insights/[slug].html` exists.
