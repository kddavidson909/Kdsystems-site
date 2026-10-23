# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Kevin Davidson's freelance site for KD Systems (`kdsystems.co`): a main landing page, three service pages, and a thank-you page. The homepage has no portfolio section until a new demo project is built. Plain HTML and CSS, with JavaScript only where it earns its place (see the JavaScript Rule below). No frameworks and no build step.

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
| `privacy.html` | Privacy policy (effective October 22, 2026), linked from every footer and under the contact form. Update it, including the effective date, before adding anything that collects or shares visitor data, such as analytics, a newsletter, or sending form leads to n8n or an AI service |
| `404.html` | Custom "page not found" page. GitHub Pages serves it for any missing URL, so every link and asset in it must use root-relative paths (`/automation.html`, not `automation.html`) |
| `sitemap.xml`, `robots.txt`, `googleb2b4515427ab4fed.html` | SEO and Google Search Console verification |
| `favicon.svg`, `kd_systems_logo.png` | Favicon (SVG, with the PNG as fallback) |
| `_config.yml` | Tells GitHub Pages which repo files to leave off the live site (`CLAUDE.md`, `README.md`, `KD_sys_logo.html`). Add any new internal file there too. |

Images live in `assets/images/`. `og-image.jpg` there is the 1200x630 link preview image used by the `og:image` and `twitter:image` tags on every public page.

`KD_sys_logo.html` is a logo design file, not a page. It stays in the repo but is kept off the live site by `_config.yml`.

Every public page has a `<link rel="canonical">` tag right after its `<title>`, pointing to its full address (`https://kdsystems.co/` for the homepage, `https://kdsystems.co/automation.html` and so on). This tells Google which address is the real one, since GitHub Pages also serves the same pages at `/index.html` and at addresses without `.html`. Add one to any new public page. The noindex pages (`thanks.html`, `404.html`) don't need one.

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

`index.html` sections in order: nav, hero, services, about, contact, footer. The portfolio section (`id="work"`) and its "Work" nav links were removed until the new demo exists; the `.portfolio` CSS is still in the file. When it comes back between services and about, give `.about` back its `var(--surface)` background and top border so the section colors keep alternating, and point the hero's second button back at it.

Service pages follow the same pattern: nav, hero, content sections, FAQ (native `<details>`), CTA band linking to `index.html#contact`, footer.

### Responsive Design

The mobile breakpoint is `@media (max-width: 768px)` in every file. At mobile, nav links hide, section padding drops, and multi-column layouts stack.

## Service Area

Kevin is based in Los Angeles County and serves Los Angeles, Orange County, and the Inland Empire (Riverside and San Bernardino counties) in person, and clients anywhere else remotely. This appears in the About section and footer of `index.html`, the footers of the three service pages, the homepage descriptions, and a `ProfessionalService` JSON-LD block in the homepage `<head>` (structured data for search engines, not executable JavaScript). Don't publish his home city or street address.

## Contact Form

The form in `index.html` posts directly to Web3Forms (`https://api.web3forms.com/submit`) and redirects to `https://kdsystems.co/thanks.html`. The access key is in a hidden `access_key` input. Every field needs a `name` attribute or Web3Forms rejects the submission. Hidden `subject` and `from_name` inputs make the notification email arrive as "New lead from kdsystems.co" from "KD Systems website". Notifications go to Kevin's personal Gmail, not to kevin@kdsystems.co.

Spam protection is Web3Forms' free hCaptcha: a `<div class="h-captcha" data-captcha="true">` above the Send button, rendered by `https://web3forms.com/client/script.js` (no hCaptcha account or keys needed). A small inline script at the end of `index.html` stops the form from sending until the box is checked, and does nothing if the captcha never loads, so the form still works. A `<noscript>` note points people with JavaScript off to the email address. Web3Forms only publishes that client script at one unversioned URL, so it is the one allowed exception to the "pin an exact version" rule.

The form does not currently send anything to n8n. If the n8n lead intake pipeline is connected later, do it in a way that reports real failures to the visitor (a `no-cors` fetch always looks successful, even when the webhook is down).

## Email

`kevin@kdsystems.co` forwards to Kevin's personal Gmail through Namecheap's free email forwarding (Namecheap is the domain registrar), with a catch-all for any other address at the domain. In Namecheap, the domain's Mail Settings must stay on "Email Forwarding", and the SPF record Namecheap adds must not be deleted, or mail to the domain will bounce. ImprovMX is no longer used.

## Visit Counting

Every public page, plus `thanks.html` (counts form submissions) and `404.html` (shows broken links people hit), loads GoatCounter's pinned script `https://gc.zgo.at/count.v5.js` just before `</body>`, with a `<noscript>` image as a fallback for visitors with JavaScript off. GoatCounter uses no cookies and stores no IP addresses, and the privacy policy describes it. Kevin's dashboard is at his GoatCounter site address. To stop counting his own visits on a device, he opens `kdsystems.co/#toggle-goatcounter` once in that browser. Any new page needs the same snippet.

## Brand and Style Rules

- **Typography:** `'Segoe UI', system-ui, sans-serif` on all pages, with the Manrope wordmark for the logo.
- **Hover effects:** CSS `transition`.
- **Accordions:** native `<details>` and `<summary>`.
- **Scroll animations:** CSS scroll-driven animations inside `@supports (animation-timeline: view())`, so content stays visible in browsers without support.
- **Writing:** no em dashes, no emoji, and no other common AI writing tells in page copy or comments.

## JavaScript Rule

Plain HTML and CSS is the default. JavaScript is allowed only when it clearly earns its place, for example a form that confirms it sent without leaving the page, spam protection such as hCaptcha, or a live demo of an automation responding. When adding it:

- **The page must still work without it.** Build the plain HTML version first and let the script improve it. The contact form, for example, must still submit and land on `thanks.html` if the script fails to load.
- **Try native HTML and CSS first.** Use `<details>`, built-in form validation, and CSS before reaching for a script.
- **Vanilla JavaScript only.** No frameworks or libraries (React, Vue, jQuery) and no build step.
- **Keep it small and close to where it's used.** A `<script>` block at the end of the page that needs it, or one file in `assets/js/` if several pages share it.
- **Third-party scripts only when the feature needs them.** Load them with `defer` and pin an exact version. Never use `@latest`.
- **No tracking or analytics scripts without Kevin's approval,** since they affect privacy and page speed.

## Owner Preferences

- Ship working code fast. Skip theory explanations unless asked.
- No backend of our own. The site stays static files on GitHub Pages. Forms and automations use outside services (Web3Forms for the contact form, n8n for automations).
- When designing new demo pages, reference real competitor sites for layout ideas rather than inventing structure.
- Commands should be Windows and PowerShell friendly.
