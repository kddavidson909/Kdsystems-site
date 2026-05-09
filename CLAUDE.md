# KD Systems — Portfolio Site

## Project Overview

This is Kevin Davidson's personal freelance landing page (`kdsystems.co`). Live site for selling landing-page and automation services to small businesses. Built from scratch as Kevin's first web project — he's self-teaching HTML/CSS via AI-assisted development.

The repo also contains 3 demo project pages (landscaping, plumbing, bakery) used as portfolio samples to show prospects.

## Files

- `index.html` — main portfolio/landing page
- `greencut.html` — landscaping demo (green theme)
- `fastflow.html` — plumbing demo (blue theme)
- `peakfitness.html` — bakery demo, Hearth Bakery (orange theme)
- `headshot.jpg` — Kevin's photo for the about section

## Tech & Style

- **Pure HTML + CSS only.** No frameworks, no build step, no JavaScript libraries. Don't suggest React, Tailwind, etc.
- Inline `<style>` blocks per file (no separate CSS files)
- Dark theme everywhere: black background, red accent on the main site (`#dc2626`); each demo page uses its own accent color
- Mobile-first responsive via CSS media queries
- Native HTML where possible (e.g., `<details>` for FAQ accordions — no JS)

## Brand

- **Name:** KD Systems
- **Domain:** kdsystems.co
- **Email:** kevin@kdsystems.co
- **Tagline:** Modern Websites. Smarter Systems.
- **Positioning:** Industrial-maintenance background; practical, reliable systems for small businesses

## Deployment

- Hosted on **Netlify** (auto-deploys from GitHub `main` branch)
- Repo: `github.com/kddavidson909/Kdsystems-site`
- DNS managed by Netlify (nameservers pointed there from Namecheap)
- Free Netlify SSL handles HTTPS

**Workflow:** edit locally → `git add . && git commit -m "..." && git push` → Netlify rebuilds in ~30s.

If push gets rejected with "non-fast-forward," use `git push origin main --force` (it's a personal repo, safe).

## Contact Form

- Uses **Web3Forms** (free, no submission limit) — submissions email straight to `kevin@kdsystems.co`
- Access key is in the form's hidden input
- All form fields require `name` attributes or Web3Forms rejects the submission

## Email Setup

- `kevin@kdsystems.co` runs through **ImprovMX** (free forwarding) into Kevin's personal Gmail
- Sending uses Gmail "Send mail as" with an app password — replies show the kdsystems.co address
- MX records and SPF TXT live in Netlify DNS

## How Kevin Wants to Work

- **Build first, learn as we go.** Don't lecture on theory. Ship code, then explain the parts he encounters.
- **Speed over perfection.** Don't over-polish; get to working output fast.
- **No backend.** This is static HTML. If a feature needs server logic, suggest a free third-party service (Web3Forms, ImprovMX, etc.) instead of building one.
- **Practical references.** When designing demo pages, fetch real competitor sites (e.g., Rooter Hero, Flores Artscape) and adapt their structure rather than inventing layouts.
- He's working in **PowerShell on Windows** — give Windows-friendly commands.
