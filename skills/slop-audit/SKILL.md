---
name: slop-audit
description: Post-draft audit for web pages and UI that catches the patterns that make AI-built design look generic or untrustworthy - layout habits, default font and palette choices, fabricated data, copy tells, and broken motion or accessibility mechanics. Use after a page, section or component has been drafted or redesigned, when reviewing existing frontend work, or when asked whether something looks AI-made, generic or templated. It is an audit, not a style guide - it prescribes no stack, typeface or palette, and the project's brand kit and CLAUDE.md always override it.
---

# Slop audit

A check you run on a draft, not a recipe you follow before drafting. Design from the brief and the brand first. Then run this list against what you actually built, fix what it catches, and report what you kept on purpose.

## Precedence

1. The user's explicit request.
2. The project's CLAUDE.md, brand-kit skill and house style (typefaces, palette, punctuation, motion rules, page chrome).
3. This audit.

When a check conflicts with 1 or 2, the brand wins and the check is skipped; say so in one line of the report. A brand that chose a serif, a cream ground or em-dashes in its prose has made a decision. A draft that drifted into them by default has not. The audit targets only the second.

The audit removes defaults. It never demands motion, imagery, dark mode or effects the brief didn't ask for.

## How to run it

1. Look at the rendered page, not only the source. If a browser is available (Playwright with Chromium), check at 390px and 1280px wide. If not, say the visual checks were done from source.
2. Go through sections A to G. For each hit, note what it is, where it is (file:line or section), and the fix.
3. Always fix section A hits unless the user overrides. Fix the rest unless the brand overrides.
4. Report in the format at the end.

## A. Credibility: never ship these

- **Invented figures presented as real.** Statistics, specs, prices, dates or counts with no source. Label sample data as sample data in the UI, or leave a visible placeholder. Never make fake data look more real (messy decimals, randomised dates).
- **People and praise no one gave.** Testimonials, quotes, reviews, names or photo credits without a real source.
- **Borrowed endorsement.** "Trusted by" or "Used by" walls of real companies that are not customers. A real logo implies a real relationship.
- **Legal marks as decoration.** ®, ™ and © are claims, not ornaments.
- **Unlicensed fonts.** Most foundry faces (Söhne, GT America, Tiempos, Canela, PP Editorial New, Neue Haas Grotesk) need a paid licence. Use what the project licenses or free faces (Google Fonts, Fontshare, OFL). Never name a paid face in CSS hoping it is installed: the reader gets a fallback.
- **Fake product UI.** A dashboard, terminal or app screen built from styled divs and presented as the real product.
- **Unflagged placeholders.** Picsum or stock images, lorem ipsum or `href="#"` links left in a production build.
- **Contradictions across the site.** Disclosure, affiliation, pricing, legal or consent text that disagrees with another page of the same site.

## B. Layout habits

- **Eyebrows everywhere.** A small uppercase tracked label above every section heading. Keep one only where it says something the heading doesn't. Most pages need between none and three.
- **Numbering as decoration.** `01 / Services`, `002 · Capabilities`, `01 / 4` on images, "Step 1, Step 2" where the step names would do. Numbering that is navigation (reports, papers, legal documents) is fine.
- **Three equal cards** as the default feature section.
- **One layout repeated.** Image-and-text splits alternating three or more times in a row, or the same section shape reused down the page.
- **Bento with filler.** N items get N cells, with no empty or decorative cells.
- **Overstuffed hero.** More than a headline, one line of support and one or two actions. Trust strips, pricing teasers, feature bullets and avatar rows go in sections of their own. The headline is two or three lines at most, and the primary action is visible without scrolling at 1280×720 and 390×844.
- **Unrequested decoration.** Word strips along the bottom of the hero (`DESIGN · BUILD · SHIP`), locale, time or weather strips, "Scroll to explore", decorative status dots, pills laid over photos, version or build stamps on a marketing page, grid lines with nothing to organise.
- **Floating corner paragraph.** A heading with a small paragraph stranded in the opposite corner. Put it under the heading or give it a real column.
- **Hairline on every row** of a long list. Group the items, chunk them, or use a different component.
- **More than one marquee** on a page.
- **Nested boxes.** Cards inside cards inside cards; containers that exist only to have a border.
- **Theme flips.** A light section dropped into a dark page, or the reverse, with no deliberate reason.
- **Duplicate CTA intent.** "Get in touch" and "Let's talk" on one site. One label per intent, everywhere.

## C. Type, colour and surface defaults

These are tells only when they arrived by default. If the brand chose them, skip.

- **Current model defaults.** Inter on slate grey. Instrument Serif or Fraunces for "premium". Cream or beige with brass, clay or oxblood and espresso-brown text for "premium consumer". Purple-to-blue glow gradients. Gradient-filled headline text.
- **The anti-slop look, now a tell too.** Geist or Satoshi on everything, Phosphor icons with a single emerald accent, double-bezel cards, an arrow-in-a-circle inside every button, a floating glass pill nav, a blur-up entrance on every element.
- **Second-typeface emphasis.** One word in a different family inside a headline. Emphasis uses italic or weight of the same family unless the brand says otherwise.
- **Colour drift.** More accents than the brand defines, warm and cool greys mixed, or an accent that changes between sections.
- **Radius drift.** Mixed corner radii with no rule behind them.
- **Pure #000 or #FFF** for large grounds or body text.
- **Clipped italics.** Italic display type losing its descenders (y, g, j, p, q) at tight line-height.
- **Measure.** Body text lines outside roughly 60 to 80 characters.

## D. Copy tells

Read every visible string, including button labels, alt text, captions and error messages.

- **Filler words.** Elevate, seamless, unleash, unlock, empower, next-gen, game-changer, delve, tapestry, "in today's fast-paced world".
- **Cute but wrong.** Wordplay that doesn't parse, metaphors that don't track, sentences with no referent. If a line would need explaining, replace it with a plain sentence.
- **Performed craft.** "Field notes", "On the bench", "Quietly trusted by", fake archival captions ("Plate 03 · House archive").
- **Micro-meta sentences** under headings that explain the section instead of being it.
- **Placeholder identities.** John Doe, Jane Smith, Acme, Nexus.
- **Em-dashes.** None in UI strings (buttons, nav, labels, captions, alt text). In prose, follow the house style. With no house style, more than about one per paragraph reads as machine-written. En-dashes in ranges are correct typography and stay.
- **Tone slips.** Exclamation marks in system messages, "Oops!" errors, Title Case On Every Heading (unless house style).

## E. Motion

- **Unmotivated motion.** Every animation should signal hierarchy, sequence, feedback or a change of state. Remove the rest. An entrance animation on every element is a tell.
- **Reduced motion.** Honour `prefers-reduced-motion` for anything beyond hover and focus feedback. Loops, parallax, pinning and scroll-linked effects become static.
- **Cheap properties only.** Animate `transform` and `opacity`. Not `transition: all`, not width, height, top or left, and not `filter: blur()` on large elements.
- **No scroll listeners driving state.** Use IntersectionObserver, CSS scroll-driven animations, or the animation library's scroll hooks.
- **No scroll hijacking.** No "inertia" smooth-scroll replacing native scrolling.
- **Loops only for live content.**
- **GSAP specifics.** Don't pin an element that also has `position: sticky`. Compute sizes inside function-based values so `invalidateOnRefresh` can recompute them on resize. Clean up with `ctx.revert()` or `useGSAP`.

## F. Mechanics and accessibility

- **Contrast.** WCAG AA: 4.5:1 for body text, 3:1 for large text. That includes buttons, placeholders, focus rings, helper and error text, and text over images.
- **Keyboard.** Visible focus, a skip link, landmarks (header, nav, main, footer), and one h1.
- **Forms.** Labels above inputs, never placeholder-as-label, errors inline beside the field.
- **Viewport height.** Full-height sections use `min-height: 100dvh` (or `svh`), not `100vh`.
- **Sticky survives.** Page wrappers use `overflow-x: clip`, not `hidden`. `hidden` breaks `position: sticky` inside it.
- **Overflow.** No horizontal scroll from 320px up. Every multi-column layout states how it collapses on narrow screens.
- **One-line controls.** Desktop navigation fits on one line, and CTA labels don't wrap.
- **Touch.** Tap targets are at least 44×44px.
- **Images.** Meaningful alt text, `alt=""` for decorative images, space reserved so nothing shifts on load.
- **Dependencies.** Every import exists in the dependency file before it is used.
- **States.** Loading, empty and error states exist wherever data can be absent.

## G. Redesigns: never change silently

Ask before changing any of these: URLs and slugs, anchor IDs, primary nav labels, form field names and order, the logo or wordmark, brand tokens (colour and type), legal, consent or disclosure copy, analytics event names and IDs, structured data, and meta titles. Keep the copy voice unless asked to rewrite it. Don't regress existing accessibility.

## Report format

```
Slop audit: <page or component>
Checked: 390px and 1280px, rendered   (or: source only)
Fixed:   A  Invented figures: "47% faster" had no source, removed (index.html:212)
         B  Eyebrows everywhere: 7 of 8 sections had one, kept on hero and pricing
Kept:    C  Instrument Serif display; the brand kit specifies it
Not run: F  Contrast over the hero photo; no browser available
```
