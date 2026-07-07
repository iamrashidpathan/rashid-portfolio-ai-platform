# Rashid Reyaz Khan — Portfolio (AI Platform Engineer)

A single-file, zero-build personal portfolio centered on who you are and what you've built — not tuned to any one job posting. Theme: **Control Plane** — a calm, editorial "infrastructure you can observe" look, with an animated service-graph hero (nodes with data pulsing along the edges), a warm serif display face, and a single deep-indigo accent. Light-first with a dark toggle.

Everything is in `index.html` — all CSS/JS inline, **no external runtime dependency** (only Google Fonts via `<link>`), vanilla JS only.

## Run locally
```
python3 -m http.server 8000   # http://localhost:8000
# or just open index.html
```

## Host it on GitHub Pages (free, shareable link)

**Browser route — no terminal:**
1. Create a new **public** repo at github.com (e.g. `portfolio`). Don't add a README.
2. On the empty repo page, click **uploading an existing file** and drag in `index.html`, `README.md`, `og-image.png` (export the PNG first — see below). Commit.
3. **Settings → Pages** → Source: *Deploy from a branch* → Branch: **main** / **/(root)** → Save.
4. Wait ~1 min. Your link appears there: `https://iamrashidpathan.github.io/portfolio/`

**Terminal route:**
```
git init
git add index.html README.md og-image.png
git commit -m "Portfolio site"
git branch -M main
git remote add origin https://github.com/iamrashidpathan/portfolio.git
git push -u origin main
```
Then do step 3 above in the browser.

**Tip:** name the repo `iamrashidpathan.github.io` instead of `portfolio` to get the cleaner root URL `https://iamrashidpathan.github.io/` (no sub-path). You can attach a custom domain later under the same Pages settings.

**Right after it's live**, update these two lines in `<head>` so link previews work, pointing at your real URL:
```html
<meta property="og:url"   content="https://iamrashidpathan.github.io/portfolio/" />
<meta property="og:image" content="https://iamrashidpathan.github.io/portfolio/og-image.png" />
```

## Deploy elsewhere
- **Netlify:** drag the folder onto the dashboard, or `netlify deploy`.
- **Vercel:** run `vercel`, accept the static defaults.

## Customize — where things live
- **Colors & fonts:** CSS custom properties under `:root` (light) and `[data-theme="dark"]`, at the top of `<style>`. One accent — `--signal` — spent deliberately; change it once and it propagates, including the hero graph (the canvas reads `--signal` so it re-themes automatically).
- **Content:** plain HTML in `<main>` — hero, About + facts, Capabilities strip, Experience (`.job`), Stack (`.skill`), Recognition & Education (`.award`), contact links.
- **Config constants** (top of the `<script>` IIFE):
  - `CALENDLY_URL` — empty = email-only booking; set your scheduler link and an **"Open scheduler"** button appears (never a dead link).
  - `EMAIL` — used by booking, command palette, and contact.
- **Assistant knowledge:** the `KB` array — `{k:[keywords], a:"answer"}`. Runs 100% client-side (no backend, no key).

### Upgrade the assistant to a real LLM (optional)
Keep the key server-side. Swap `answer()` for a `fetch()` to your own serverless proxy:
```js
async function answer(q){
  const r = await fetch("/api/chat", {
    method:"POST", headers:{"Content-Type":"application/json"},
    body: JSON.stringify({ message:q })
  });
  return (await r.json()).reply;
}
```
Never put an API key in `index.html`.

## Features
Boot sequence · animated canvas control-plane hero · side rail with scroll progress · reveal-on-scroll (IntersectionObserver) · light/dark toggle (in-memory) · command palette (Ctrl/Cmd-K) · client-side assistant · mailto booking with optional Calendly · responsive (1200 / 860 / 480 px) · keyboard-navigable, visible focus · `prefers-reduced-motion` respected · canvas in try/catch with graceful hide · dpr capped at 2 · rendering paused when tab hidden.

## Social preview
`og-image.svg` (1200×630) is the source. Export to PNG for reliable sharing:
```
rsvg-convert -w 1200 -h 630 og-image.svg -o og-image.png
#   or: npx svgexport og-image.svg og-image.png 1200:630
#   or open the SVG in a browser and screenshot at 1200×630
```

## Honesty note
All content comes from your provided resume — no invented employers, titles, or metrics. This is your third variant: the AI-Platform framing (RAG/agents/Terraform/K8s/Kafka/AWS). The earlier resumes framed the same roles differently (e.g. Oracle as i18n/text-library work, EXL as healthcare). Keep whichever framing matches the version of yourself you want public — just make sure the live site and the résumé you send tell a consistent story.
