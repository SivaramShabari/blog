# CLAUDE.md

This is a **personal project** (a static Astro blog). It is separate from any work setup on this machine.

## Memory & context policy — read first

- **Never** write memory, notes, or context about this project to the central/global user memory (anything under `~/.claude/...`). The global Claude configuration on this machine is reserved for work; this blog must not leak into it.
- All Claude memory and context for this blog lives **in this repository**, under `.claude/memory/`.
- When you learn a durable fact worth remembering, write it as a file in `.claude/memory/` and add a one-line pointer to `.claude/memory/MEMORY.md` (the index). Do not put it anywhere under `~/.claude`.
- `.claude/` is gitignored, so these notes stay local to this checkout and are never pushed. (If you'd rather version them, remove the `.claude/` line from `.gitignore`.)

## Project quick facts

- Astro `blog` template, TypeScript strict. Markdown posts in `src/content/blog/`.
- Keep it minimal: no CMS, auth, analytics, or dependencies beyond what the template ships. Sitemap, RSS, and MDX stay on (SEO baseline).
- Title: **Quack Overflow**. Live site: **https://writing.sivaramshabari.me**.
- Hosting / deploy details are in `.claude/memory/`.
