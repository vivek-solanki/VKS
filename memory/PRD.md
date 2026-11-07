# VKS CREATE — Portfolio Website PRD

## Original Problem Statement
Build a modern, premium, fully responsive single-page portfolio website for video editor & content creator brand "VKS CREATE" (Vivek Solanki, Khategaon, MP, India). Dark cinematic base #0B0B0F, sunset gradient (dusty blue-grey → warm peach/tan), Bebas Neue + Poppins, single index.html with all content in config variables at top, mobile-first (Instagram traffic), sections: Hero (typing + parallax floats), Viral Reels Showcase (9:16 cards, autoplay muted on scroll, lightbox with sound, view badges, Instagram CTA), About (bio + count-up stats), Services (5 tilt/glow cards), Software (CapCut, VN, Edits), Before/After draggable grade slider, Contact form (Formspree/EmailJS placeholder + WhatsApp pre-filled + direct buttons), Footer. Page-load intro, scroll reveals, glowing cursor (desktop), floating WhatsApp pulse, scroll progress bar, back-to-top. SEO + Open Graph with preview image.

## Architecture
- **Single-file site**: `/app/frontend/public/index.html` — full HTML+CSS+JS in one file (user's explicit format choice). Served at `/` by the React dev server / production build.
- **React shell**: `/app/frontend/src/App.js` renders `null`; `/app/frontend/src/index.css` neutralized — the site is 100% plain HTML/CSS/JS.
- **Images** (generated, cinematic sunset grade): `/app/frontend/public/{og-banner,about,grade,reel-1,reel-2,reel-3}.jpg`.
- **Libraries (CDN)**: Google Fonts (Bebas Neue, Poppins), Lenis 1.1.14 (smooth scroll, guarded fallback to native).
- **No backend usage** — form delivery is Formspree/EmailJS (user-pasted endpoint) with WhatsApp fallback.

## Key Config Block (top of index.html <script>)
SITE (name, tagline, contacts, socials, logoUrl slot), TYPING[], MARQUEE[], STATS[] (3+/100+/30+/1M+ counters), SERVICES[5], TOOLS[3], REELS[6] (url: MP4 or Instagram link or ""), FORM_CONFIG (formspreeEndpoint + emailjs slots), BUDGETS[].

## User Personas
- **Creators/brands** landing from Instagram: watch reels, judge quality, tap WhatsApp/call.
- **Vivek (owner)**: edits one index.html — config block for texts, reels, stats; pastes Formspree endpoint + logo file.

## Implemented (2026-10-24)
- Page-load intro (gimbal-mark draw + VKS CREATE mask reveal), custom SVG gimbal logo + favicon, footer watermark.
- Sticky glass navbar, section spy, mobile fullscreen menu; scroll progress bar; Lenis smooth scroll.
- Hero: animated sunset gradient + horizon glow + film grain, masked line-by-line name reveal, tagline, typing animation (5 services), 2 CTAs, 4 parallax floating shapes (film strip, play, camera, phone).
- Slow editorial marquee; Reels showcase (6 cards, horizontal scroll mobile / 3-col grid desktop, view badges, poster placeholders, IO autoplay-pause for MP4s, lightbox with MP4/Instagram-embed/empty states, prev-next-ESC, Instagram CTA).
- About: generated desk photo with clipped frame + 3+ years badge, exact bio, animated counters (compact M formatting).
- Services: 5 cards with 3D tilt + cursor-tracked glow; Tools: CapCut / VN / Edits cards.
- Before/After: draggable (pointer + keyboard) grade slider using one image with CSS "raw" filter (perfect alignment).
- Contact: full form (Name/Phone/Email/Service dropdown/Budget/Details), Formspree POST when endpoint set, EmailJS path, WhatsApp fallback (toast + pre-filled wa.me), success check animation, direct Call/WhatsApp/Email/Instagram/YouTube buttons.
- Footer (logo, quick links, socials, © VKS CREATE), floating WhatsApp pulse button, back-to-top, glowing custom cursor (desktop only), scroll reveals, reduced-motion support.
- SEO: title/description/keywords, OG + Twitter tags (/og-banner.jpg), JSON-LD Person, theme-color, lazy-loaded images.
- Fixed during verification: slide-reveal horizontal overflow (overflow-x clip), burger z-index vs menu overlay.

## Verified
- curl: root serves site HTML; images 200. Screenshots desktop 1440 + mobile 390. Mobile: menu open/close, lightbox open/ESC-close, form submit fallback → success animation + toast. No horizontal overflow (scrollW 390).

## Backlog
- **P0**: Owner pastes Formspree endpoint (FORM_CONFIG.formspreeEndpoint); upload logo file → set SITE.logoUrl; add real view counts to the 4 reels (currently "New").
- **P1**: og:url after deploy; real about photo of Vivek; more reels (add to REELS[] — grid auto-adapts via 4-col desktop layout).
- **P2**: Testimonials section; blog/journal; per-reel analytics links.

## Update (2026-10-24, later)
- Selected Work now shows 4 REAL client reels (user-uploaded MOVs transcoded HEVC 4K60 → H.264 MP4 720x1280, ~5-27MB, faststart, audio kept): Traditional Grace (saree portrait), Ritik & Komal (wedding film), Wedding Vows (ceremony), Garba Night (dance event). Posters are real first frames. Desktop grid 4-col; mobile horizontal snap-scroll. Verified: all MP4s serve 200 video/mp4 + full ffmpeg decode pass; headless test browser lacks H.264 codec (canPlayType NONE) which is a test-env limitation, real browsers decode natively.
