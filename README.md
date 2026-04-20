# EDC · RIT — Recruitment Website

A single-file, production-ready recruitment site for the **Entrepreneurship Development Cell at Ramaiah Institute of Technology**. Built with vanilla HTML/CSS/JS plus Three.js for interactive elements. No build step. No framework. Open it in a browser and it works.

---

## Table of Contents

- [Quick Start](#quick-start)
- [What's Inside](#whats-inside)
- [File Structure](#file-structure)
- [How to Edit Content](#how-to-edit-content)
- [How to Add Photos](#how-to-add-photos)
- [Theme & Colors](#theme--colors)
- [Interactive Elements](#interactive-elements)
- [Deployment](#deployment)
- [Browser Support](#browser-support)
- [Troubleshooting](#troubleshooting)
- [Credits](#credits)

---

## Quick Start

1. **Download** `edc.html` (that's it — the whole site is one file).
2. **Open** it in any modern browser by double-clicking, or via a local server.
3. **Edit** the file directly in VS Code, Sublime, or any text editor. Reload the browser to see changes.

### Running a local server (optional but recommended)

If you want clean URL behavior and hot reload, run a local server from the folder containing `edc.html`:

```bash
# Python (pre-installed on most machines)
python3 -m http.server 8000

# Node.js
npx serve .

# VS Code: install "Live Server" extension, right-click the file, "Open with Live Server"
```

Then visit `http://localhost:8000/edc.html`.

---

## What's Inside

A scrollytelling recruitment trailer with the following sections:

1. **Hero** — animated morphing glass orb (Three.js), animated headline reveal, live "recruitment open" indicator, primary CTA to the Google Form
2. **Manifesto (About)** — who EDC is, written as a statement
3. **Kinetic BUILD moment** — huge sticky-scrolling gradient text that grows as you scroll (trailer-style)
4. **What We Do** — four glass cards covering mentorship, validation, office space, talent & funding
5. **Events** — horizontal-scroll carousel of 5 flagship events (Pradarshana, Goal for a Cause, Startup Summit, Hackathon, TUFF)
6. **Podcast + Compete** — two-up card layout
7. **Roles** — all 12 recruitment roles in a grid (Upstarters, Event Management, Operations, PR & Sponsorship, Publicity, IT, Documentation, Logistics, Design, Video Editing, Social Media, Coverage)
8. **Gallery** — asymmetric bento grid of 6 moments (photo placeholders)
9. **Marquee** — scrolling "Build · Dream · Dare · Ship · Pitch · Fail · Try again · Win"
10. **CTA** — large glass card linking to the Google Form
11. **Contact Us** — Instagram + LinkedIn chips and three coordinator cards with tappable phone numbers
12. **Footer** — navigation links, social icons, copyright

### Key Features

- **Light + dark mode** with a toggle in the nav (respects system preference, persists via localStorage)
- **5 floating decorative Three.js orbs** scattered throughout the page, each reacting to cursor movement with parallax
- **Glassmorphism** on all cards (high blur, saturation, reflective top-edge stroke)
- **Pastel mesh gradient** background with subtle grain overlay
- **Scroll-driven animations** — headlines scale as they enter view, hero orb morphs with scroll progress, kinetic text scales 0.2× → 1.8×
- **Fully responsive** — works from 360px phones to 4K desktops with dedicated breakpoints at 420, 560, 720, 820, 860, 900, 980px
- **Accessibility** — respects `prefers-reduced-motion`, semantic HTML, ARIA labels, proper focus states, tappable phone links (`tel:`)

---

## File Structure

```
edc.html                 ← The entire site, one file (~76 KB)
images/                  ← (You create this) folder for gallery photos
├── pradarshana.jpg
├── startup-summit.jpg
└── ...
README.md                ← This file
```

Inside `edc.html` the order is:

```
<head>
  ├── font imports (Fraunces, General Sans, JetBrains Mono)
  └── <style> — all CSS (~750 lines)
       ├── tokens (light + dark theme variables)
       ├── navigation
       ├── hero
       ├── manifesto
       ├── kinetic trailer text
       ├── what-we-do grid
       ├── events carousel
       ├── podcast/compete duo
       ├── roles grid
       ├── gallery bento
       ├── marquee
       ├── CTA
       ├── contact us
       ├── footer
       └── responsive media queries

<body>
  ├── background (mesh + grain + floating mini orbs)
  ├── nav
  ├── all sections in order
  ├── footer
  └── <script> blocks (5 total)
       ├── Three.js CDN
       ├── hero orb + particles
       ├── mini decorative orbs (cursor-reactive)
       ├── kinetic scroll text transform
       ├── theme toggle (light/dark)
       └── intersection observer reveals
```

---

## How to Edit Content

All content is directly in the HTML — no CMS, no database, no config file. Open `edc.html` in a text editor and use Ctrl+F (Cmd+F on Mac) to find what you want to change.

### Change the Google Form link

Search for `forms.gle/hcDQcRXv8YULfRvF7`. It appears in 4 places:

- Nav "Apply" pill
- Hero "Start your application" button
- Big CTA button
- Footer "Apply" link

Replace all 4 occurrences with your new URL.

### Update coordinator info

Search for `coord-card`. You'll find three blocks like this:

```html
<div class="coord-card">
  <div class="who">
    <div class="avatar">SP</div>
    <div>
      <div class="name">Siddharth Priyatam</div>
      <div class="role-label">Coordinator</div>
    </div>
  </div>
  <a class="phone" href="tel:+919030226998">
    <svg>...</svg>
    90302 26998
  </a>
</div>
```

To edit:
- **Name** → change the `.name` text
- **Initials** → change the `.avatar` text (keep it 2 letters)
- **Phone** → change **both** the `href="tel:+91..."` AND the visible number
- **Role/title** → change the `.role-label` text (e.g., "Lead", "Core Member")

To add a 4th coordinator, copy one block and change the avatar class to `v1`, `v2`, or `v3` for different gradient colors.

### Update social media links

Search for `instagram.com/ecell_ramaiah` and `linkedin.com/company/ecell-rit` — each appears in 2 places (Contact section + footer). Update all occurrences.

### Edit role descriptions

Search for the role name (e.g., `Upstarters`). Each role is a `.role` div:

```html
<div class="role reveal">
  <div class="plus">+</div>
  <div class="idx">R / 01</div>
  <h4>Upstarters</h4>
  <p>The people building startups...</p>
</div>
```

Change `<h4>` for the title and `<p>` for the description. The `.idx` shows R/01, R/02, etc — keep these in order.

### Edit event cards

Search for `event-card a1`. Each card has:
- A `.hero-art` block (the colored gradient on top — replace with a photo)
- A `.tag` (e.g., "Flagship · Annual")
- An `<h3>` (event name)
- A `<p>` (description)
- A `.foot` with month + number

To reorder events, just rearrange the `<article>` blocks inside `.events-track`.

### Change the kinetic "BUILD." word

Search for `data-kinetic`. Change the text inside:

```html
<div class="kinetic-word" data-kinetic>BUILD.</div>
<div class="kinetic-sub" data-kinetic-sub>or step aside.</div>
```

Keep it short (1–2 words + short subtitle) — longer text breaks the scale animation.

### Change marquee words

Search for `marquee-track`. Replace the `<span>` items:

```html
<span>Build</span><span>Dream</span><span>Dare</span>...
```

The words repeat twice — copy the full list and paste it directly after itself to keep the seamless loop. If you change the word count, the loop will still work.

---

## How to Add Photos

The site has **6 gallery tiles** and **5 event card heroes** currently using colored gradients as placeholders. Here's how to swap them for real photos.

### Step 1: Create an `images/` folder

Put it right next to `edc.html`:

```
your-project/
├── edc.html
└── images/
    ├── pradarshana.jpg
    ├── startup-summit.jpg
    ├── hackathon.jpg
    ├── tuff.jpg
    ├── podcast-ep12.jpg
    └── goal-for-a-cause.jpg
```

### Step 2: Replace gallery tile backgrounds

Search for `.tile.t1` in the CSS. You'll find:

```css
.tile.t1{ grid-column: span 3; grid-row: span 2; background: linear-gradient(135deg, #ffd7c2, #ffb89b 55%, #e4d4ff); }
```

Replace the `background:` value:

```css
.tile.t1{ grid-column: span 3; grid-row: span 2; background: url('images/pradarshana.jpg') center/cover; }
```

`center/cover` crops the photo to fill the tile cleanly regardless of aspect ratio.

Do the same for `.tile.t2` through `.tile.t6`.

### Step 3: Replace event card heroes (optional)

Search for `.event-card.a1 .hero-art`:

```css
.event-card.a1 .hero-art{ background: radial-gradient(circle at 30% 30%, #ffd7c2, #ffb89b 60%, #f79b78); }
```

Change to:

```css
.event-card.a1 .hero-art{ background: url('images/pradarshana-hero.jpg') center/cover; }
```

### Recommended image sizes

| Tile | Size (px) | Aspect | Use |
|------|-----------|--------|-----|
| t1, t5 (big) | 1200×800 | Landscape/square | Hero photos |
| t2, t6 (wide) | 1600×400 | Very landscape | Group shots, panoramas |
| t3, t4 (small) | 800×400 | Landscape | Detail shots |
| Event hero art | 800×300 | Wide landscape | Event visuals |

### Keep file sizes small

- Use **JPG** for photos, **WebP** if your target browsers support it
- Aim for **<300KB per image**, ideally <150KB
- Tools: [Squoosh.app](https://squoosh.app/) (drag & drop, free, instant)

### Readability overlay (optional)

If a photo has bright whites in the bottom-left corner where the label pill sits, add a subtle dark gradient overlay:

```css
.tile.t1{ 
  background: 
    linear-gradient(to top, rgba(0,0,0,0.35), transparent 50%),
    url('images/pradarshana.jpg') center/cover; 
}
```

The overlay only darkens the bottom portion — keeps the photo punchy everywhere else.

### Hosting photos externally (alternative)

Instead of a local folder, you can host images on:
- **Cloudinary** / **Imgix** (free tier, auto-resizing)
- **GitHub** (push to a repo, use the raw URL)
- **Cloudflare R2** / **AWS S3** (paid, production-grade)

Reference them by full URL:

```css
background: url('https://res.cloudinary.com/your-account/image/upload/v123/pradarshana.jpg') center/cover;
```

---

## Theme & Colors

### Light vs dark mode

The site has a full dark mode. Toggle lives in the nav (sun/moon icon). It:

- Respects system preference on first visit (`prefers-color-scheme: dark`)
- Remembers your explicit choice across reloads (localStorage)
- Retints the Three.js orbs automatically to match the theme

### Color tokens

All colors are defined as CSS custom properties at the top of the `<style>` block. To change the palette:

```css
:root{
  --peach:   #ffd7c2;   /* primary warm */
  --peach-2: #ffb89b;
  --lilac:   #e4d4ff;   /* primary cool */
  --lilac-2: #c8b0ff;
  --mint:    #c8f0dc;   /* accent */
  --mint-2:  #a0e6c6;
  --cream:   #fff7ee;   /* warm white */
  --ink:     #1b1630;   /* primary text */
  /* ...etc */
}
```

Change these values and the whole site updates — buttons, accents, gradients, avatars, glass tints, all of it.

Dark mode overrides are in `[data-theme="dark"]` right below.

### Typography

Three typefaces, all loaded from Google Fonts:

- **Fraunces** — display headlines (with italics for accents)
- **General Sans** — body text (via Fontshare CDN)
- **JetBrains Mono** — labels, eyebrows, metadata

To swap a font, update the `<link>` import at the top and change the `--f-display`, `--f-body`, or `--f-mono` variable.

---

## Interactive Elements

### Hero orb (Three.js)

- Custom GLSL shader with simplex noise displacement
- Morphs more aggressively as you scroll (ties into kinetic section)
- Subtle cursor parallax
- Surrounded by ~180 floating particles
- Retints when theme changes
- Auto-repositions on mobile (centered vs right-offset)

### Mini decorative orbs

5 small orbs (80–140px) at strategic scroll positions:
- Each uses the same noise shader (lighter geometry for perf)
- All parallax **opposite** to cursor movement
- Different palettes (peach, lilac, mint, mixed)
- IntersectionObserver culling — only visible orbs render
- Hidden below 420px screen width
- Respect `prefers-reduced-motion`

### Kinetic scroll text

The giant "BUILD." section uses scroll position to:
- Scale text from 0.2× → 1.8× → 1.5×
- Rotate subtly
- Fade in/out at the edges
- Reveal a subtitle in the middle

Uses `requestAnimationFrame` throttling for smooth 60fps.

### Theme toggle

One-line API:

```js
window.dispatchEvent(new CustomEvent('edc:themechange', { detail: { theme: 'dark' }}));
```

All theme-aware components listen for this event. Useful if you ever want to trigger theme changes from elsewhere (e.g., a keyboard shortcut).

---

## Deployment

The site is a single static HTML file. Deploy anywhere that serves static files:

### Option 1: GitHub Pages (free, easiest)

1. Create a GitHub repo, push `edc.html` + `images/` folder
2. Settings → Pages → Source: your main branch → Save
3. Visit `https://<your-username>.github.io/<repo-name>/edc.html`

Rename `edc.html` → `index.html` to get a clean root URL.

### Option 2: Netlify (free, instant)

1. Go to [app.netlify.com](https://app.netlify.com)
2. Drag your folder onto the dashboard
3. Live in ~10 seconds, with a free `*.netlify.app` subdomain
4. Add a custom domain from settings

### Option 3: Vercel (free, instant)

Same as Netlify — drag-and-drop deploy, free subdomain, custom domain support.

### Option 4: Cloudflare Pages (free)

Connect a GitHub repo → automatic deploys on every push.

### Option 5: Any web host

Since this is plain HTML, **any** hosting provider works — InfinityFree, Hostinger, college server, anywhere that serves files.

---

## Browser Support

| Browser | Status |
|---------|--------|
| Chrome 90+ | Full support |
| Safari 15+ | Full support |
| Firefox 88+ | Full support |
| Edge 90+ | Full support |
| Mobile Safari (iOS 15+) | Full support |
| Mobile Chrome (Android 10+) | Full support |
| IE 11 | Not supported (Three.js requires ES6) |

Required browser features: WebGL, CSS custom properties, CSS `backdrop-filter`, IntersectionObserver, ES6 modules. All shipped in 2021.

---

## Troubleshooting

**The mesh background looks flat / washed out**
Your browser may not support `backdrop-filter`. Safari needs `-webkit-backdrop-filter` (already included). Very old browsers will see a simpler version — not broken, just less glassy.

**The Three.js orb isn't showing up**
Check the browser console (F12). Likely causes:
- No WebGL support (very rare on 2020+ devices)
- The Three.js CDN is blocked (e.g., on an offline demo). Download `three.min.js r128` and host locally.

**Fonts aren't loading**
The site uses Google Fonts + Fontshare. If you're on a very strict network (some campus wifis), fonts may be blocked. Fallbacks (Georgia, system-ui) will kick in automatically.

**Images don't appear after I added them**
- Check the file path exactly matches: `images/filename.jpg` (case-sensitive on some servers)
- Verify the file exists in the `images/` folder
- Open the browser console → Network tab → look for 404 errors

**The page scrolls horizontally on mobile**
Check if you added any elements that exceed 100vw. The site is set to `overflow-x: hidden` on body to prevent this, but inline styles or very wide `width:` values can still cause issues.

**Dark mode won't stick**
Browsers clear localStorage in private/incognito mode, so the theme resets every visit. This is expected browser behavior.

**The coordinator phone links don't dial on desktop**
`tel:` links only work on devices that can make calls (phones, tablets with cellular, some Mac + iPhone via Handoff). On other desktops, clicking does nothing — that's fine.

---

## Credits

- **Design & build:** Claude (Anthropic) with direction from the EDC team
- **Fonts:** Fraunces (SIL OFL), General Sans (Fontshare), JetBrains Mono (Apache 2.0)
- **3D graphics:** [Three.js r128](https://threejs.org/) (MIT)
- **Noise function:** Simplex noise by Stefan Gustavson, Ian McEwan (MIT)

---

## License

This site is built for the Entrepreneurship Development Cell at Ramaiah Institute of Technology. Internal use, modify freely.

---

*Built for builders.*
