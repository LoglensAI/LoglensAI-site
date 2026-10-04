# SEO applied — what changed (and what did NOT)

## What did NOT change
- No prerendering. That is what broke your animations before (it makes support.js
  render twice). It is gone.
- No design, layout, animation, or runtime code. Every page is **+23 lines, −0 lines**:
  the additions are all inert `<head>` metadata plus an invisible `<noscript>` block.
  Real visitors see exactly the same site.

## What was added
Per page (`.dc.html`):
- Real `<title>`, meta description, and canonical in the static `<head>`, **mirrored
  verbatim from your existing helmet** so values match and nothing conflicts.
- Open Graph + Twitter tags (nice link previews when shared).
- JSON-LD structured data (Organization + WebSite everywhere; SoftwareApplication +
  FAQ on Home; FAQ on Pricing) — this is what AI engines read.
- An invisible `<noscript>` with the H1, description, and nav links, so crawlers that
  don't run JavaScript still get real content. It never shows when JS is on.

Site root:
- `robots.txt`, `sitemap.xml`, `llms.txt` (URLs match your canonicals).
- `vercel.json` updated so your canonical routes resolve (`/learn`,
  `/compare/splunk-alternative`, plus `/tour`, `/pricing`, `/docs`, `/`).

## Deploy
Redeploy this folder to Vercel (`vercel --prod`, or drag it into the dashboard). No
build step.

## Remaining steps (do after deploy)
1. **Google Search Console** + **Bing Webmaster Tools** → add the site, submit
   `https://www.loglensai.com/sitemap.xml`.
2. Test a page: Rich Results Test (https://search.google.com/test/rich-results) to
   confirm the structured data is read.
3. Build the `/errors` pages from the starter-kit template to start pulling traffic.

## A note on limits
Because the page body is still rendered by support.js, Google (which runs JS) will
index everything, and all engines now get your title, description, and JSON-LD plus
the noscript text. For the strongest possible crawlability you would eventually want
true server-side rendering — but that is a bigger change, and this gets you the large
majority of the benefit with zero risk to your design.
