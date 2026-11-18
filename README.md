# Vanakkam DSA workshop landing page (demo)

Model landing page for the 22 Nov Vanakkam DSA live workshop. Everything is in `index.html` (no build step).
Live demo: https://dineshkumarsd.github.io/vanakkam-dsa-webinar-demo/

## Hero video setup

The hero uses a short muted teaser that autoplays, with a "Tap for sound" button.

| File | Spec |
|---|---|
| `hero-teaser.mp4` | 10–15 s cut of Hareesh's intro, 1280×720, H.264 MP4, ~1 Mbps, about 2 MB, first 2 s should hook without sound (add captions) |
| `hero-poster.jpg` | Still frame from the video, 1280×720 JPG, under 40 KB |

Steps:
1. Put both files in the same folder as `index.html`.
2. The `<video>` tag already has `autoplay muted loop playsinline preload="metadata"`:
   - `muted` is required for autoplay on phones
   - `playsinline` stops iPhones opening the video fullscreen
   - `preload="metadata"` keeps the first screen fast
3. "Tap for sound" restarts the video from 0:00 with sound, turns off looping and shows the player controls.
4. If you want the full-length intro after unmute, swap the `src` to the full video inside the click handler at the bottom of the page.
5. Delete the `<div class="poster">…</div>` sample frame inside `.video` once the real files are live.
6. For extra speed, host the MP4 on a CDN (Bunny, Cloudflare R2/Stream) and use that URL in `<source src>`.

## Student stories carousel

- Each slide has a "Student photo" box. Replace the `<div class="shot">…</div>` with
  `<img class="shot" src="students/arun.webp" alt="Arun Kumar" loading="lazy" width="800" height="500">` (16:10, WebP, under 60 KB).
- Use real names, outcomes and quotes only, with each student's written consent, and remove the "Sample" tags.
- The carousel auto-advances every 5 s, stops when the visitor touches it, and supports swipe, arrows and dots.

## Before going live

- Replace sample stats, testimonials and mentor credentials with real ones.
- Point the Register buttons to the TagMango checkout link.
- Link Privacy Policy, Terms and Refund Policy to real pages (needed for Meta ad review).
- Add the Meta Pixel / Conversions API snippet.
- Remove `<meta name="robots" content="noindex">` only if you want the page indexed.
