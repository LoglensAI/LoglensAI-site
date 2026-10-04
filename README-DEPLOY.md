# LogLens AI — Vercel deploy bundle

Static site (Claude Design export + `support.js` runtime). **No build step.** Design
and pages are unchanged — only `vercel.json` was added and the Web3Forms key needs to be set.

## 1. Set your Web3Forms access key (required for the forms to work)

The contact/waitlist forms on **Home** and **Pricing** already POST to Web3Forms
(AJAX, honeypot, success/error toast — all wired in `support.js`). They just need your key.

Get a free key at https://web3forms.com (enter your email → copy the access key), then
replace the placeholder in both files:

```bash
# from the bundle root
grep -rl YOUR_WEB3FORMS_ACCESS_KEY .                # shows the 2 files
sed -i 's/YOUR_WEB3FORMS_ACCESS_KEY/<your-key>/' "LogLens Home.dc.html" "LogLens Pricing.dc.html"
```

(On macOS use `sed -i '' 's/.../.../'`.) Submissions go to the email tied to the key.

## 2. Deploy to Vercel

Any of these work — it's a static site:

**CLI**
```bash
npm i -g vercel
vercel          # preview
vercel --prod   # production
```
When asked for settings: Framework = **Other**, Build Command = **(none)**, Output Dir = **./**.

**Dashboard:** vercel.com → Add New → Project → import this folder/repo → deploy
(no build settings needed).

## What `vercel.json` does

- Serves the home page at `/` (the files use spaces + `.dc.html`, so `/` is rewritten to
  `LogLens Home.dc.html`).
- Adds clean entry routes: `/home` `/tour` `/pricing` `/docs` `/compare` `/academy`.
- Long-cache headers for `/assets/*`.

Nothing else was modified. In-page navigation still uses the original `LogLens *.dc.html`
links, which Vercel serves directly.

## Note

The original export's `uploads/` folder (duplicate, unreferenced videos) was omitted to keep
the deploy small. The referenced media lives in `assets/`.
