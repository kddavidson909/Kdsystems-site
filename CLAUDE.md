# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Kevin Davidson's personal freelance landing page (`kdsystems.co`) plus 3 demo project pages used as portfolio samples. Built with pure HTML + CSS — no frameworks, no build step, no JavaScript libraries.

## Development Workflow

There is no build step. To preview changes, open the HTML file directly in a browser. Deployment is automatic:

```
git add . && git commit -m "..." && git push
```

Netlify auto-deploys from `main` within ~30 seconds. If push is rejected with "non-fast-forward," `git push origin main --force` is safe (personal repo).

## File Structure & Architecture

Each page is fully self-contained — all CSS lives in an inline `<style>` block in the `<head>`. There are no shared stylesheets.

| File | Purpose | Accent color |
|---|---|---|
| `index.html` | Main portfolio/landing page | Red `#dc2626` |
| `greencut.html` | Landscaping demo | Green `#22c55e` |
| `fastflow.html` | Plumbing demo | Blue `#0ea5e9` |
| `peakfitness.html` | Fitness studio demo | Orange `#ff5500` |

### CSS Variable Convention

Every file opens with a `:root` block defining the full color palette for that page. All colors are referenced via `var(--name)` throughout — never hardcoded inline. The standard variable names used across all files are:

```css
:root {
  --bg, --surface, --card, --border   /* background layers (darkest → lightest) */
  --[accent], --[accent]-d            /* primary accent + darker shade */
  --[accent]-g, --[accent]-gg         /* glow/alpha versions for shadows/glows */
  --text, --muted, --subtle           /* text hierarchy */
}
```

When adding a new page, define all these variables in `:root` first and use them exclusively.

### Section Structure

`index.html` sections (in order): nav → hero → services → portfolio → about → contact → footer

Demo pages follow a similar pattern but add industry-specific elements like a credential bar (greencut), promo bar (fastflow, peakfitness), or sticky CTA panel (fastflow hero uses a 2-column grid with a form panel on the right).

### Responsive Design

Mobile breakpoint is `@media (max-width: 768px)` in every file. At mobile: nav links hide, section padding drops from `64px` to `24px`, multi-column layouts stack vertically.

## Contact Form

The form in `index.html` posts to Web3Forms (`https://api.web3forms.com/submit`). The access key is stored in a `<input type="hidden" name="access_key">` field. All form fields **must** have `name` attributes or Web3Forms rejects the submission.

## Brand & Style Rules

- **Background layers:** `--bg` (body), `--surface` (alternate sections), `--card` (cards/inputs)
- **Accent on main site:** `#dc2626` (red) — each demo uses its own accent
- **Typography:** `'Segoe UI', system-ui, sans-serif` everywhere; no Google Fonts loaded
- **Interactive elements:** use CSS `transition` on hover; no JavaScript event listeners
- **Accordions/disclosure:** use native `<details>`/`<summary>` — no JS toggles
- **No JS** — if a feature needs interactivity, use native HTML elements or suggest a free third-party service

## Owner Preferences

- Ship working code fast; skip theory explanations unless asked
- No backend — static HTML only; for form/email needs use free services (Web3Forms, ImprovMX)
- When designing new demo pages, reference real competitor sites for layout ideas rather than inventing structure
- Commands should be Windows/PowerShell-friendly
