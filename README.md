# Vanakkam DSA webinar landing page: developer handoff

**Reference design (live):** https://dineshkumarsd.github.io/vanakkam-dsa-webinar-demo/
**Source:** `index.html` in this repo, one self-contained file (HTML + CSS + JS, no build step).

Please rebuild this page on the Vanakkam DSA site (e.g. `vanakkamdsa.com/webinar`) so it looks and behaves exactly like the reference, and keep it as a **reusable template**: for every new webinar we should only need to change the date, time and register link in one place.

---

## 1. The one place to edit for each webinar

Near the top of `index.html` there is a single settings block:

```js
window.WEBINAR = {
  date: "2026-11-22",        // YYYY-MM-DD
  time: "17:00",             // start time in IST, 24-hour HH:MM
  durationHrs: 3,
  registerUrl: "#register",  // TagMango checkout link for EVERY Register button
  price: 199,                // rupees
  seats: 100
};
```

Changing these values updates every place on the page automatically:

| Setting | Where it appears |
|---|---|
| `date` + `time` | Header ("LIVE · 22 NOV 2026"), hero pills ("Sun, 22 Nov", "5 PM IST"), FAQ reminder line, closing section ("Sunday, 22 November · 5:00 PM IST"), floating bar ("22 Nov, 5:00 PM IST") |
| `durationHrs` | Hero pill and hero button ("3 hrs live") |
| `registerUrl` | All 5 Register buttons: hero, "FREE with ₹199" badge, "Claim bonuses", closing CTA, floating bar |
| `price` | Every "₹199" on buttons, bonus total and floating bar |
| `seats` | Reserved (not displayed right now) |

How it works: elements carry `data-w="…"` (text slots) and `data-register` (links). A small script at the end of the page formats the date/time in IST and fills them in. The static text in the HTML stays as a fallback.

**If you move this into a CMS / WordPress / Next.js:** expose these six values as page fields (or a JSON/front-matter file) and render the same slots server-side. Server-side rendering is preferred so the correct date shows instantly and in link previews.

Test: change `date` to `2026-12-06`, `time` to `18:30`, `price` to `299`. The page should read "6 Dec", "6:30 PM IST", "₹299" everywhere, with no other edits.

---

## 2. Must-match details

- **Theme:** graphite background (`#141417`), champagne-gold accents from the Hayan Tech logo. All colours are CSS variables at the top of `<style>`.
- **Fonts:** Sora (headings), Manrope (body), JetBrains Mono (labels) from Google Fonts.
- **First screen (no scroll):** headline, detail pills, video and Register button must all be visible on a 360×640 phone. Please re-check on real devices and in the Instagram / Facebook in-app browser.
- **Glowing CTAs:** pulsing halo + light sweep (`@keyframes glow` / `shine`); disabled for users with reduced-motion on.
- **Floating Register bar:** hidden until the hero CTA scrolls out of view (IntersectionObserver), then floats above the bottom edge.
- **Logo strip:** Google, Amazon, Meta + "13 more" (official marks from Simple Icons). Keep the label "Learn interview patterns from FAANG and top product companies". Don't change it to "our students work at" unless placements are verified.
- **Student stories carousel:** swipe / arrows / dots, auto-advances every 5 s, stops on touch.
- **Single footer disclaimer** (Meta + trademarks + results). Keep it; it's needed for Meta ad review.

---

## 3. Hero video

| File | Spec |
|---|---|
| `hero-teaser.mp4` | 10–15 s cut of Hareesh's intro, 1280×720, H.264, ~1 Mbps (~2 MB), burned-in captions |
| `hero-poster.jpg` | Still frame, 1280×720, under 40 KB |

- The `<video>` already uses `autoplay muted loop playsinline preload="metadata"` (muted is required for phone autoplay; playsinline stops iPhone fullscreen).
- "Tap for sound" restarts from 0:00 with sound and controls.
- Delete the sample `<div class="poster">` frame once the real files are in. Host the MP4 on a CDN (Bunny / Cloudflare) for speed.

---

## 4. Replace before launch

- [ ] Student stories carousel is built but hidden (`hidden` on `#stories`). Add real names, outcomes, quotes and photos (16:10 WebP, under 60 KB) with written consent, then remove `hidden`.
- [ ] Confirm the 15 LPA+ figure in the stats row.
- [ ] "Where our students work now" logos: only companies with verified placements.
- [ ] Footer links: Privacy Policy, Terms, Refund Policy, Contact → real pages (Meta checks these).
- [ ] Add Meta Pixel + Conversions API; fire `Lead`/`InitiateCheckout` on Register click, and `Purchase` from TagMango.
- [ ] Remove `<meta name="robots" content="noindex">` only if the page should be indexed.
- [ ] Mentor photo is embedded as base64. Swap it for a normal image file on your server if you prefer.
