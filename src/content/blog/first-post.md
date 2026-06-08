---
title: 'Hello, world'
description: 'A first post — what this blog is and how it is built.'
pubDate: 'Jun 08 2026'
---

This is the first post on my new blog. I set it up as a static site so writing is
just editing Markdown files in a folder — no database, no CMS, nothing to log into.
Each `.md` file in the posts directory becomes a page, and the build turns the whole
thing into plain HTML I can host anywhere.

## Why static

Static sites are fast, cheap, and durable. There is no server to keep running and
nothing to patch at 2am. The trade-off is that anything dynamic has to happen at
build time or in the browser, which for a personal blog is no trade-off at all.

The toolchain here is [Astro](https://astro.build/), which renders Markdown to HTML
and ships almost no JavaScript by default. It also wires up an RSS feed and a sitemap
out of the box, so the SEO basics are covered without extra work.

## Writing a post

A post is a Markdown file with a small frontmatter block at the top — a title, a
description, and a publish date:

```yaml
---
title: 'Hello, world'
description: 'A first post — what this blog is and how it is built.'
pubDate: 'Jun 08 2026'
---
```

Everything below the frontmatter is the body. Headings, links, lists, and fenced
code blocks all render the way you would expect. That is the whole workflow: write
Markdown, save, and the post shows up.

More to come.
