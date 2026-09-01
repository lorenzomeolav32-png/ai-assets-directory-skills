# Build Spec

Output: ONE complete HTML file. All CSS and JavaScript inline. Nothing external except
the CDN libraries listed. Never produce explanation around the HTML. Just the file.

## Section Rhythm (non-negotiable)

```
Hero (dark) → Marquee (accent) → Stats (warm cream) → Services (dark)
→ How We Work (white) → Gallery (near-black) → Why Choose Us (dark navy)
→ Testimonials (dark ink) → CTA (cream) → Contact (white) → Footer (dark)
```

When dark sections are adjacent (Gallery, Why, Testimonials), differentiate them with
slightly different values: `#0A1628`, `#081120`, `#060D18`. The eye reads them as
different even if subtle.

## Required CDN Libraries

- Google Fonts via `@import` inside `<style>`
- AOS.js: `https://unpkg.com/aos@2.3.1/dist/aos.css` and `.../aos.js`
- GSAP 3.12: `https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js`
- Splitting.js: `https://unpkg.com/splitting/dist/splitting.min.css` and `.../splitting.min.js`
- Swiper.js 11: `https://cdn.jsdelivr.net/npm/swiper@11/swiper-bundle.min.css` and `.../swiper-bundle.min.js`
- Lenis: `https://cdn.jsdelivr.net/npm/@studio-freight/lenis@1.0.42/dist/lenis.min.js`
- Font Awesome 6.4: `https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css`
- tsParticles 2.12: `https://cdn.jsdelivr.net/npm/tsparticles@2.12.0/tsparticles.bundle.min.js`
- Vanilla Tilt 1.8: `https://cdnjs.cloudflare.com/ajax/libs/vanilla-tilt/1.8.1/vanilla-tilt.min.js`

## Premium Detail Rules (apply to every build)

These are the small details that separate v1 (functional) from v2 (premium):

1. **Section labels use editorial line treatment.** Every section label is
   `display: inline-flex; align-items: center; gap: 12px;` with a `::before` element
   that is a 28px wide accent-colored line: `content: ''; width: 28px; height: 2px;
   background: [accent];`. Output looks like: `─── WHAT WE DO`. This is the editorial
   magazine pattern.
2. **Animated logo dot.** Nav brand has a small accent-colored dot (8px circle) before
   the business name, pulsing on a 3s ease-in-out keyframe. Tiny detail, big premium
   signal.
3. **Hero gets a directional gradient overlay, not a flat one.** Use
   `linear-gradient(105deg, rgba(0,0,0,.88) 0%, rgba(0,0,0,.30) 100%)` so the left text
   side is fully readable but the right photo side breathes.
4. **Hero photo gets two floating elements layered on top:**
   - **Certification/trust badge** (top-right of photo): pill-shaped, dark background,
     accent border, content like "Licensed & Insured" or "★ 4.9 Google". Animates in
     with GSAP.
   - **Stats card** (bottom-left of photo): small card with one number + label, e.g.,
     "500+ Projects Completed". Subtle backdrop blur. Animates in with delay after the
     badge.
5. **Dark sections get a dot-grid texture overlay.**
   ```css
   background-image: radial-gradient(rgba(255,255,255,.04) 1px, transparent 1px);
   background-size: 28px 28px;
   ```
   Extremely subtle (4% opacity). Adds perceptible depth to flat dark backgrounds.
6. **Service icon containers.** Service card icons sit inside a 56x56 rounded square
   (border-radius 12px) with an accent-tinted background `rgba([accent], 0.12)` and
   accent border `1px solid rgba([accent], 0.3)`. Icon scales up slightly on card hover.
7. **Featured service card gets a "POPULAR" or "POPULÄR" badge** (translate to client
   language). Position: absolute, top-right, accent background, white text, 11px
   uppercase, padding 4px 10px, border-radius 100px.
8. **Why Choose Us checklist uses circular icon wrappers.** Each checkmark sits inside a
   26x26 circle, accent-tinted background `rgba([accent], 0.15)`, 1px accent border.
   Creates proper visual rhythm down the list.
9. **Rotating Google rating badge on Why Choose Us photo.** Circular badge absolutely
   positioned top-right of the photo, ~110px diameter, white background, content:
   "★ 4.9 Google Rating" wrapped in a circle. Slow rotation animation
   (`@keyframes rotateBadge { to { transform: rotate(360deg) } }`, 30s linear infinite).
10. **CTA banner gets large ghosted background text.** Behind the CTA content, a giant
    decorative word (industry-relevant: "VVS", "DENTAL", "PIZZA", etc.) at 300px
    font-size, color `rgba(0,0,0,0.055)`. Pure decoration, zero noise.

---

## SECTION 1: NAVIGATION

Sticky header. Fixed top. Full width. Z-index 1000.
Page load: transparent. Scroll past 80px: smooth 0.3s transition to solid persona dark
+ `backdrop-filter: blur(12px)` + `box-shadow: 0 2px 24px rgba(0,0,0,0.18)`. Height
shrinks 80px → 64px.

Left: brand. Includes the **animated 8px accent dot** before the business name, pulsing
3s ease-in-out infinite. Brand name: display font, 22px, bold.

Right: Nav links + phone number + CTA button.

- Nav link hover: directional underline (`::after` pseudo-element, slides in from left,
  slides out to the right).
- Phone in nav: subtle pulse every 6s (opacity 1 → 0.7 → 1, scale 1 → 1.02 → 1).
- CTA button "Get Free Quote": filled accent. Hover: background fills from left via
  `::before` with `transform: scaleX()`.

Mobile: hamburger animates to X. Full-screen overlay menu, centered links 32px display
font.

## SECTION 2: HERO

Full viewport height (100vh). Overflow hidden.

Particles div: `<div id="particles"></div>` with `position: absolute; inset: 0;
z-index: 1; pointer-events: none;`

Hero element: `position: relative;` background gradient fallback only.
```css
#hero { background: linear-gradient(135deg, [persona dark], [persona accent]); }
#hero::before {
  content: ''; position: absolute; inset: -10%;
  background-image: url('https://images.unsplash.com/photo-[verified hero ID]?w=1920&q=85');
  background-size: cover; background-position: center;
  animation: kenBurns 25s ease-in-out infinite alternate;
  z-index: 0; will-change: transform;
}
@keyframes kenBurns {
  0%   { transform: scale(1)    translate(0%, 0%); }
  33%  { transform: scale(1.06) translate(-2%, -1%); }
  66%  { transform: scale(1.04) translate(1.5%, -2%); }
  100% { transform: scale(1.08) translate(-1%, 1%); }
}
#hero::after {
  content: ''; position: absolute; inset: 0;
  background: linear-gradient(105deg, rgba(0,0,0,.88) 0%, rgba(0,0,0,.30) 100%);
  z-index: 1;
}
```

Hero content `.hero-inner`: `position: relative; z-index: 2;`

tsParticles config:
```js
tsParticles.load('particles', {
  particles: {
    number: { value: 28 },
    color: { value: '#ffffff' },
    opacity: { value: 0.18, random: true, animation: { enable: true, speed: 0.6, minimumValue: 0.05, sync: false } },
    size: { value: 2, random: true },
    move: { enable: true, speed: 0.5, direction: 'top', random: true, straight: false, outModes: 'out' },
    shape: { type: 'circle' }
  },
  detectRetina: true
});
```

Layout: Split. Left 55%, Right 45%. Centered vertically.

LEFT SIDE:
- Section label: editorial line treatment, "TRUSTED [BUSINESS TYPE] IN [CITY]" at 12px
  accent uppercase `letter-spacing: 0.15em`. Fades in first.
- Headline: 72px desktop / 42px mobile. Display font. Bold. White. `line-height: 1.1`.
  Punchy 4-6 words specific to this business.
- Splitting.js split + GSAP word stagger:
  ```js
  Splitting();
  gsap.from('.hero-headline .word', { y: 40, opacity: 0, duration: 0.8, stagger: 0.08, ease: 'power3.out' });
  ```
- Subheadline: 20px, 400 weight, white at 85%, `line-height: 1.6`. Slides in 0.3s after
  headline.
- Two CTAs side by side (stack on mobile):
  - Primary: "Get Your Free Quote" accent fill, white text, 16px, padding 14px 28px,
    border-radius 6px. Hover fill from left.
  - Secondary: "Call [Phone]" transparent, white border, white text. Same hover.
- Trust signal: "★★★★★  4.9 Rating · 200+ Projects Completed · Licensed & Insured" at
  13px white 65%.

RIGHT SIDE (the photo):
- Image: verified right panel photo. Format `https://images.unsplash.com/photo-[ID]?w=900&q=85`.
- CSS gradient fallback on same element.
- `clip-path: polygon(8% 0%, 100% 0%, 100% 100%, 0% 100%)` for diagonal left edge. Or
  `border-radius: 0 24px 24px 0` if clip looks off.
- Slides in from right (translateX 60px → 0, opacity 0 → 1) with 0.4s delay after
  headline.
- Container slow float: `animation: heroFloat 8s ease-in-out infinite`
  ```css
  @keyframes heroFloat { 0%,100% { transform: translateY(0) translateX(0) } 33% { transform: translateY(-10px) translateX(3px) } 66% { transform: translateY(-6px) translateX(-3px) } }
  ```

**TWO floating elements on the photo:**

A. **Certification badge (top-right of photo):**
- Pill, content: "★ 4.9 Google Rating" or "Licensed & Insured" or "[Cert]"
- Dark background `rgba(0,0,0,0.78)`, 1px accent border, white text 13px bold, padding
  8px 16px, border-radius 100px
- Animates in via GSAP: `gsap.from('.hero-cert-badge', { opacity: 0, y: -10, duration: 0.6, delay: 1.2 })`
- Pulse: `animation: badgePulse 3s ease-in-out infinite`

B. **Stats card (bottom-left of photo):**
- Small card: dark glass `rgba(0,0,0,0.6)` with `backdrop-filter: blur(8px)`, accent
  left border 3px, padding 14px 18px, border-radius 8px
- Content: one big number (28px display font, white) + label below (12px white 70%,
  uppercase, letter-spacing 0.1em). E.g., "500+ / Projects Completed" or
  "[Years] / Years in Business"
- GSAP delay 1.5s, slide up + fade

```css
@keyframes badgePulse { 0%,100% { box-shadow: 0 0 0 0 rgba([accent],0.4) } 50% { box-shadow: 0 0 0 8px rgba([accent],0) } }
```

Below 768px: hide right panel and floating elements. Stack hero, center left content.

## SECTION 3: SOCIAL PROOF MARQUEE

Directly below hero. Zero gap.
Background: accent color or near-black. Padding 14px vertical. `overflow: hidden`.
CSS-only infinite scroll, two identical sets,
`@keyframes marquee { from { transform: translateX(0); } to { transform: translateX(-50%); } }`
28s linear infinite.

Items: ⭐ 4.9 Google Rating · ✓ Licensed & Insured · 🏆 BBB Accredited · ✓ [X]+ Years in
Business · ⭐ 5-Star Rated · ✓ #1 Rated [Type] in [City] · ✓ 500+ Satisfied Customers ·

Style: 12px uppercase `letter-spacing: 0.1em` white or dark on accent. " · " spacers.

## SECTION 4: TRUST BAR

Light background (persona warm cream `#F5F3EF` for trades, persona light section
otherwise). Padding 80px vertical.
5 stats in a row. Mobile: 2x2 + 1 centered.

Each stat:
- Font Awesome icon, 28px, accent
- Number, 56px bold display font, persona dark
- Label, 13px uppercase `letter-spacing: 0.1em` muted grey

Thin vertical separators (1px, `rgba(0,0,0,0.1)`) between stats.

Fifth stat is always "4.9 ★" + "Google Rating" + star icon in accent.

Animation: Intersection Observer + GSAP counter from 0 to target with `expo.out` easing.
Never AOS. Never linear.
```js
gsap.to(counterEl, { innerHTML: targetValue, duration: 2, ease: 'expo.out', snap: { innerHTML: 1 }, onUpdate: () => counterEl.textContent = Math.round(gsap.getProperty(counterEl, 'innerHTML')) });
```

## SECTION 5: SERVICES

Background: persona dark with gradient (e.g., `linear-gradient(135deg, #0a1628, #0D1B2A)`)
**plus the dot-grid texture overlay** (28px grid, 4% white dots).
Padding 100px vertical.

Header (left-aligned):
- Label: editorial line treatment, "WHAT WE DO" at 12px accent uppercase. Translate to
  client language if needed (e.g., "VAD VI GÖR").
- Headline: 52px desktop / 34px mobile, display font, bold, white
- Subline: 18px body muted, `max-width: 560px`

Service cards (glassmorphism, asymmetric grid):
```css
background: rgba(255,255,255,0.05);
backdrop-filter: blur(12px);
border: 1px solid rgba(255,255,255,0.1);
color: white;
```
Featured card: `background: rgba([accent],0.15); border: 1px solid rgba([accent],0.4);`
PLUS the **"POPULAR" badge** (top-right, accent fill, white text, 11px uppercase,
padding 4px 10px, border-radius 100px). Translate badge to client language.

Vanilla Tilt on every card:
```js
VanillaTilt.init(document.querySelectorAll('.service-card'), { max: 6, speed: 400, glare: true, 'max-glare': 0.15, perspective: 800 });
```

Grid: `grid-template-columns: 1.4fr 1fr`. Featured card spans 2 rows (`grid-row: span 2`)
in left column. Two standard stack right. Never uniform 3-column. Asymmetry is the design.

Each card:
- **Icon container**: 56x56 rounded square (border-radius 12px), `background: rgba([accent], 0.12)`,
  `border: 1px solid rgba([accent], 0.3)`. Font Awesome icon inside, 28px, accent color.
  On card hover, icon scales 1.0 → 1.08.
- Service name: 22px bold display
- 2-line description: 15px body muted, `line-height: 1.6`
- "Learn More →" link, accent, 14px
- Animated bottom border: 3px solid accent, `width: 0` → `width: 100%` on hover,
  `transition: width 0.35s ease`
- Card lifts 8px on hover with shadow

All cards: `data-aos="fade-up"`, 80ms stagger.

## SECTION 5.5: HOW WE WORK (3-step process)

White background. Padding 90px vertical. Sits between dark Services and dark Gallery to
break the rhythm correctly.

Header (centered):
- Label: editorial line treatment, "HOW WE WORK" at 12px accent. Translate to client
  language.
- Headline: 44px display font, dark, centered
- Subline: 17px muted, `max-width: 560px`, centered

3 steps in horizontal row (stack on mobile):

Each step:
- **Number**: 64px display font in accent color, top of the step. E.g., "01", "02", "03"
- **Step title**: 20px bold display, dark
- **Step description**: 15px body muted, 2-3 sentences, specific to the business
- Step content centered

**Horizontal connector**: between step 1→2 and 2→3, an accent dashed line (1px, dashed,
~80% width of gap) sits at the level of the numbers. Hidden below 768px.
```css
.process-step:not(:last-child)::after {
  content: ''; position: absolute; top: 32px; left: 50%; width: 100%; height: 1px;
  border-top: 1px dashed [accent]; opacity: 0.4;
}
@media (max-width: 768px) { .process-step::after { display: none; } }
```

Steps `data-aos="fade-up"` with 120ms stagger. Write the 3 steps specifically for the
business: e.g., for a trades site → "01 Free Inspection · 02 Clear Quote · 03 We Get to
Work". For a dental site → "01 Book Online · 02 First Visit Plan · 03 Treatment That
Fits".

## SECTION 6: GALLERY (4-image asymmetric grid)

Near-black background `#060D18` (slightly different value than services dark for
adjacent dark sections). Padding 100px vertical. Includes dot-grid texture.

Header (centered):
- Label: editorial line treatment, "OUR WORK" or "PROJECTS" or "GALLERY" — translate
- Headline: 52px display font, white, centered
- Subline: 17px white 65%, centered

Grid: 4 images. CSS Grid: `grid-template-columns: 1.4fr 1fr 1fr; grid-template-rows: 1fr 1fr;`.
- Image 1 (verified gallery photo 1): spans 2 rows in column 1
  (`grid-column: 1; grid-row: 1 / span 2`). The flagship/largest.
- Image 2: column 2, row 1
- Image 3: column 3, row 1
- Image 4: column 2 / span 2, row 2 (`grid-column: 2 / span 2; grid-row: 2`)

Mobile: stack into single column, all equal height.

Each image:
- Wrapper: `position: relative; overflow: hidden; border-radius: 8px;` Background
  gradient fallback.
- `<img>` with `object-fit: cover; width: 100%; height: 100%; transition: transform 0.6s ease;`
- Hover: `transform: scale(1.05)` on the image
- **Hover overlay** (`::after`): semi-dark gradient bottom up
  `linear-gradient(to top, rgba(0,0,0,0.85) 0%, transparent 60%)`, `opacity: 0` default,
  `opacity: 1` on hover. Inside the overlay (positioned absolute bottom-left, 20px
  padding):
  - Category tag (10px uppercase accent letter-spacing 0.15em): e.g., "BATHROOM"
  - Caption (15px white bold): e.g., "Full bathroom remodel, [City]"

Cards: `data-aos="fade-up"` with 100ms stagger.

## SECTION 7: WHY CHOOSE US

Dark navy background (persona dark, slightly different value than gallery: `#081120`).
Padding 100px vertical. Dot-grid texture.
Split layout. Left 48%, Right 48%, 4% gap.

LEFT (image):
- Verified Why Choose Us photo. Format `?w=900&q=85`. Gradient fallback.
- `border-radius: 16px`, `object-fit: cover`
- `data-aos="fade-right"`
- **Rotating Google rating badge**: circular ~110px, white background, dark text,
  content arranged radially: "★ 4.9 GOOGLE RATING ★ 4.9 GOOGLE RATING" wrapped circular
  OR a simpler design: large center "4.9 ★" with smaller text "GOOGLE" below. Absolutely
  positioned top-right of the photo, offset -32px / -32px so it overlaps the corner.
  Rotates slowly:
  ```css
  @keyframes rotateBadge { to { transform: rotate(360deg); } }
  .google-badge { animation: rotateBadge 30s linear infinite; }
  ```

RIGHT (content):
- Label: editorial line treatment "WHY CHOOSE US" at 12px accent. Translate.
- Headline: 46px desktop / 30px mobile, display, white, `line-height: 1.15`.
  `data-aos="fade-left"`
- Bold stat line: ONE compelling number with context. "15 Years. Zero Callbacks." or
  "Rated 4.9 by 340 Customers." 20px white bold. Delay 100ms.
- Checklist (5-6 items). Each item:
  - **26x26 circular icon wrapper**: `background: rgba([accent], 0.15); border: 1px solid rgba([accent], 0.4); border-radius: 50%; display: flex; align-items: center; justify-content: center;`
    containing a Font Awesome `fa-check` at 12px accent
  - Item text: white, 17px, `line-height: 1.5`. Specific benefits, not generic.
  - `data-aos="fade-left"` 100ms stagger
- CTA button "Get Started Today" accent fill.

## SECTION 8: TESTIMONIALS

Dark ink background `#0A1628`. Full width. Padding 100px vertical. Dot-grid texture.

Header centered:
- Label: editorial line treatment "WHAT CLIENTS SAY"
- Headline: 52px display white centered
- Subline: 18px white 65% centered

Swiper carousel:
```js
new Swiper('.testimonials-swiper', {
  loop: true, spaceBetween: 24, grabCursor: true, centeredSlides: true,
  autoplay: { delay: 3500, disableOnInteraction: false, pauseOnMouseEnter: true },
  breakpoints: {
    0:    { slidesPerView: 1.15, centeredSlides: true },
    768:  { slidesPerView: 2.2,  centeredSlides: false },
    1024: { slidesPerView: 3,    centeredSlides: false }
  }
});
```
No pagination dots. No nav arrows.

Each card:
- `background: rgba(255,255,255,0.06); border: 1px solid rgba(255,255,255,0.08); border-radius: 16px; padding: 32px;`
- Stars top: "★★★★★" 22px accent `letter-spacing: 2px`
- Quote: 16px white 85% `line-height: 1.75` italic, 3-4 sentences. Specific service
  mentions, specific outcomes, real-person voice.
- Separator: 1px `rgba(255,255,255,0.12)` `margin: 20px 0`
- Customer name: 15px bold white
- "G via Google Reviews" badge: 12px muted with `fa-google` G icon. Never "Google
  Verified" (not real).

Write 5 unique testimonials. Each mentions: a specific service, a specific detail or
outcome, sounds like a real person.

## SECTION 9: CTA BANNER

Light cream background (persona warm cream). Padding 100px vertical. Centered. Subtle
dot texture or 135deg light gradient.

**Large ghosted background text:** absolutely positioned, centered, behind all content.
300px font-size, display font, bold, color `rgba(0,0,0,0.055)`, `pointer-events: none`,
`user-select: none`, `z-index: 0`. The word: industry-relevant, e.g., "VVS", "DENTAL",
"PIZZA", "CROSSFIT", "REAL ESTATE". Line-height 1, single word.

CTA content sits at `position: relative; z-index: 1`:
- Label: editorial line treatment "READY TO GET STARTED?" 12px accent. Translate.
- Headline: 52px desktop / 32px mobile display dark bold `max-width: 700px`. Specific
  compelling offer: "Get a Free In-Home Estimate This Week"
- Subline: 20px muted. "No pressure. No obligation. We show up on time or it's free."
- Phone large: 44px accent bold click-to-call.
- CTA button: "Book Your Free Quote Today" 18px padding 16px 36px accent fill hover from
  left.
- Reassurance: "Typically responds within 2 hours · Licensed & Insured · Serving [City]
  Since [Year]" 13px muted.

All `data-aos="fade-up"` staggered 80ms.

## SECTION 10: CONTACT

White background. Padding 80px vertical.
Headline: "Get In Touch" 48px display dark left-aligned. Translate.

Two columns (stack on mobile):

LEFT (Contact Info):
- "Ready to talk?" 28px bold
- Service area: "Proudly serving [City] and surrounding areas" 17px muted
- Phone: large accent click-to-call with `fa-phone`
- Email: `fa-envelope`
- Hours: realistic for business type
- Area list: "Also serving: [3-4 nearby suburbs]" small bullet list 14px muted

RIGHT (Contact Form, 4 fields only):
- Full Name (text)
- Phone Number (tel)
- Service Needed (select listing all services)
- Message (textarea, optional, label "Anything else we should know? (optional)")
- Submit: full width accent "Send My Request →" 16px

Form: 1px border, 8px border-radius, 14px padding. Focus: border transitions to accent +
`box-shadow: 0 0 0 3px rgba(accent, 0.15)`.

Submit handler (no backend):
```js
form.addEventListener('submit', function(e) {
  e.preventDefault();
  form.innerHTML = '<div style="text-align:center;padding:40px 0;"><p style="font-size:24px;font-weight:700;color:[accent];">Got it. We will be in touch within 2 hours.</p><p style="font-size:16px;color:#666;margin-top:8px;">Check your phone, we usually call first.</p></div>';
});
```

## SECTION 11: FOOTER

Dark background (same as hero). Full width.
Accent top border: 3px solid accent, full width. Visual handoff from contact.
Padding 64px top, 32px bottom (above bottom bar).

4-column grid (mobile 2x2, then single):

Col 1 (Brand): business name 24px display bold white, with the **animated dot before it**
to match nav. Tagline 14px white 60%, specific. Social icons: `fa-facebook-f`,
`fa-instagram`, `fa-google` 20px each, hover transitions to accent.

Col 2 (Services): heading 13px uppercase `letter-spacing: 0.1em` accent. All services as
links 14px white 75% hover white. Translate heading.

Col 3 (Contact): heading same style. Phone with `fa-phone` click-to-call. Email with
`fa-envelope`. Service area with `fa-map-marker-alt`.

Col 4 (Quick Links): heading same. Home, About, Services, Contact, Privacy. Translate.

Thin divider `rgba(255,255,255,0.08)` above bottom bar.
Bottom bar: "© 2025 [Business Name]. All rights reserved. · Licensed & Insured" 13px
white 40% centered. Translate.

## FIXED ELEMENT: Click-to-Call Button

Fixed bottom-right, 20px offsets. Z-index 9999. Circular 58px diameter. Accent fill.
`box-shadow: 0 4px 20px rgba(accent, 0.5)`.
Phone icon `fa-phone` white 22px centered.
Pulse 2.5s ease infinite:
```css
@keyframes pulse { 0%, 100% { box-shadow: 0 0 0 0 rgba(accent, 0.5) } 50% { box-shadow: 0 0 0 12px rgba(accent, 0) } }
```
Stay circular always (no expand on hover, breaks at small sizes).
Tooltip on hover (desktop): dark bg "Call Now" white text border-radius 6px small
downward arrow via `::before`/`::after`.
`href="tel:[phone]"`.

## ANIMATION HIERARCHY (one approach per type)

1. **On load**: Splitting.js + GSAP for headline word stagger + GSAP entrance for hero
   floating elements only.
2. **On scroll**: AOS only. `data-aos` attributes, init AFTER Lenis.
3. **Counter animations**: Intersection Observer + GSAP `expo.out`. Never AOS. Never
   vanilla.
4. **Marquee**: CSS keyframes only.
5. **Hover effects**: CSS only.
6. **Smooth scroll**: Lenis FIRST, in a RAF loop:
   ```js
   const lenis = new Lenis({ lerp: 0.08 });
   function raf(t) { lenis.raf(t); requestAnimationFrame(raf); }
   requestAnimationFrame(raf);
   ```
   Without the RAF loop, Lenis does nothing.
7. **Carousel**: Swiper only.
8. **3D tilt**: VanillaTilt with `data-tilt`, init after DOMContentLoaded.
9. **Scroll progress bar**: `<div id="scroll-progress">` fixed top, `width: 0%` → fills
   on scroll. JS updates `width = scrollY / (body.scrollHeight - innerHeight) * 100 + '%'`.
10. **Restraint**: ≤60% of elements per section animated. Some things just appear.
    Overanimated = cheap.
11. AOS init: `AOS.init({ duration: 700, once: true, offset: 80 })`

## TYPOGRAPHY SCALE (non-negotiable)

- Hero headline: 72px / 42px mobile
- Section headlines: 52px / 34px mobile
- "How We Work" headline: 44px (slightly smaller)
- Card titles: 22px
- Body text: 17-18px `line-height: 1.7`
- Labels, captions, badges: 13-14px `letter-spacing: 0.08em`
- Stat numbers: 56px
- CTA banner phone: 44px
- Process step numbers: 64px
- Ghosted background word: 300px

Never default to 48px. Never use 16px body. Those settings make AI sites look generic.

## HARD COPY RULES

These apply to every word the customer reads on the site:

- **Never use em-dashes (—) or en-dashes (–) in website copy.** Use commas, colons, or
  restructure.
- No AI-sounding phrases: "elevate your business", "unlock the potential", "in today's
  fast-paced world", "we strive to deliver", "your trusted partner".
- No lorem ipsum.
- Every word for this specific business in this specific city.
- Headlines punchy and human, not corporate.
- Testimonials sound like real people, not marketing copy.
- Translate UI strings (buttons, section labels, headings) to the client's language when
  the business is non-English.

## QUALITY GATE (verify before outputting)

- [ ] Photo discovery actually ran. 7 verified photo IDs in use, not the persona fallbacks.
- [ ] Each photo IS appropriate for the actual business type (a plumber site shows real plumbing work, not a guy in a suit).
- [ ] Scroll progress bar fixed at top
- [ ] Sticky header transparent → solid with blur on scroll
- [ ] Hero has Ken Burns on `::before`
- [ ] Hero overlay is **directional** (105deg gradient), not flat
- [ ] Hero photo has 2 floating elements (cert badge + stats card) animating in
- [ ] tsParticles dots in hero
- [ ] Hero right panel floating (heroFloat)
- [ ] Hero headline animates word-by-word
- [ ] Animated dot before brand name in nav
- [ ] All section labels use editorial line treatment (28px accent line + uppercase label)
- [ ] Marquee scrolls infinitely CSS-only
- [ ] Trust bar counters use Intersection Observer + GSAP expo.out
- [ ] Services section has dark gradient + dot-grid texture
- [ ] Service cards use glassmorphism + Vanilla Tilt
- [ ] Service icons sit in 56x56 rounded containers with accent tint
- [ ] Featured service card has POPULAR badge top-right
- [ ] How We Work section between services and gallery (3 steps + dashed connector)
- [ ] Gallery section: 4-image asymmetric grid (1 large + 3 smaller)
- [ ] Gallery cards have hover overlays with category tag + caption
- [ ] Why Choose Us has rotating Google badge on the photo
- [ ] Why Choose Us checklist uses 26x26 circular icon wrappers (not flat checkmarks)
- [ ] Testimonials in Swiper carousel (not static grid)
- [ ] All 5 testimonials are specific (service, detail, outcome)
- [ ] CTA banner has large ghosted background word (300px, 5.5% opacity)
- [ ] CTA phone 44px
- [ ] Click-to-call button fixed, pulsing, circular
- [ ] All adjacent dark sections use slightly different values (#0A1628, #081120, #060D18)
- [ ] All dark sections include the dot-grid texture overlay
- [ ] All images have CSS gradient fallbacks
- [ ] Section rhythm correct (dark/light/dark/light alternation)
- [ ] Footer 4-column with accent top border
- [ ] Font scale correct (72/52/44/22/17-18/13-14/56/44/64/300)
- [ ] Lenis smooth scroll initialized in RAF loop
- [ ] Zero placeholder text. Every word specific to this business.
- [ ] Copy is in the correct language for the client (Swedish business → Swedish copy)
