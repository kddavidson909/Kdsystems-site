# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Kevin Davidson's freelance site for KD Systems (`kdsystems.co`): a main landing page, three service pages, and a thank-you page. The portfolio section is a "coming soon" placeholder until a new demo project is built. Pure HTML and CSS. No frameworks, no build step, no JavaScript libraries.

## Hosting and Deployment

The site is hosted on **GitHub Pages** from the `main` branch of `kddavidson909/Kdsystems-site`, with the custom domain set by the `CNAME` file. It is no longer on Netlify, so nothing in a `netlify/` folder or `netlify.toml` will run.

There is no build step. To preview, open the HTML file in a browser. To deploy:

```
git pull
git add .
git commit -m "..."
git push
```

GitHub Pages usually updates within a minute or two.

Kevin edits this site from more than one computer. Always `git pull` before starting work. **Never force push** (`git push --force`). If a push is rejected as non-fast-forward, run `git pull`, resolve any conflicts, and push again. A force push would erase commits made from the other computer.

## Editing Rules (important)

Several pages have been published with their endings cut off, losing FAQ items, the CTA band, the footer, and the closing tags. To keep that from happening again:

- Make targeted edits to the part of the file that changes. Do not rewrite or regenerate a whole HTML file.
- After editing any HTML file, confirm it still ends with `</footer>`, `</body>`, and `</html>` before committing.
- Before committing, review `git diff --stat`. A large number of deleted lines from a small change is a sign something was truncated.

## File Structure

Each page is self-contained. All CSS lives in an inline `<style>` block in the `<head>`. There are no shared stylesheets.

| File | Purpose |
|---|---|
| `index.html` | Main landing page (dark theme, red `#dc2626` accent) |
| `automation.html` | Business Automation service page |
| `ai-tools.html` | AI-Powered Tools service page |
| `landing-pages.html` | Websites and Landing Pages service page |
| `crm-integrations.html` | Redirect to `automation.html` (CRM work was folded into automation) |
| `thanks.html` | Thank-you page the contact form redirects to |
| `sitemap.xml`, `robots.txt`, `googleb2b4515427ab4fed.html` | SEO and Google Search Console verification |
| `favicon.svg`, `kd_systems_logo.png` | Favicon and social share image |

Images live in `assets/images/`.

`KD_sys_logo.html` is a logo design file, not a page. It is listed in `.gitignore` but is still tracked, so it is publicly reachable until it is removed with `git rm --cached KD_sys_logo.html`.

### CSS Variable Convention

Every page opens with a `:root` block defining its color palette. Colors are referenced with `var(--name)` rather than hardcoded. Standard names:

```css
:root {
  --bg, --surface, --card, --border   /* background layers */
  --[accent], --[accent]-d            /* primary accent and a darker shade */
  --[accent]-g, --[accent]-gg         /* glow and alpha versions for shadows */
  --text, --muted, --subtle           /* text hierarchy */
}
```

### Section Structure

`index.html` sections in order: nav, hero, services, portfolio (currently a "coming soon" placeholder), about, contact, footer.

Service pages follow the same pattern: nav, hero, content sections, FAQ (native `<details>`), CTA band linking to `index.html#contact`, footer.

### Responsive Design

The mobile breakpoint is `@media (max-width: 768px)` in every file. At mobile, nav links hide, section padding drops, and multi-column layouts stack.

## Contact Form

The form in `index.html` posts directly to Web3Forms (`https://api.web3forms.com/submit`) and redirects to `https://kdsystems.co/thanks.html`. The access key is in a hidden `access_key` input. Every field needs a `name` attribute or Web3Forms rejects the submission.

The form does not currently send anything to n8n. If the n8n lead intake pipeline is connected later, do it in a way that reports real failures to the visitor (a `no-cors` fetch always looks successful, even when the webhook is down).

## Brand and Style Rules

- **Typography:** `'Segoe UI', system-ui, sans-serif` on all pages, with the Manrope wordmark for the logo.
- **Interactive elements:** CSS `transition` on hover. No JavaScript event listeners.
- **Accordions:** native `<details>` and `<summary>`.
- **Scroll animations:** CSS scroll-driven animations inside `@supports (animation-timeline: view())`, so content stays visible in browsers without support.
- **No JS.** If a feature needs interactivity, use native HTML elements or a free third-party service.
- **Writing:** no em dashes, no emoji, and no other common AI writing tells in page copy or comments.

## Owner Preferences

- Ship working code fast. Skip theory explanations unless asked.
- No backend. Static HTML only. For form and email needs, use free services (Web3Forms, ImprovMX).
- When designing new demo pages, reference real competitor sites for layout ideas rather than inventing structure.
- Commands should be Windows and PowerShell friendly.
