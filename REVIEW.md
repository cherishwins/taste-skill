# Review of the upstream skills (October 2026)

A review of the thirteen upstream skills as installed in npsi-site, juchegang and ipurpose, and the reason this fork adds `skills/slop-audit/`.

## Verdict

The upstream catalogue of AI design tells is sharp and mostly right. Its main sections are §9 of `skills/taste-skill/SKILL.md` and the audit list in `skills/redesign-skill/SKILL.md`. The tells include an eyebrow above every section, fake dashboards built from divs, decorative section numbering, Instrument Serif or beige-and-brass as the default "premium" look, three equal cards, and scroll cues. Models still drift into these, so a checklist earns its place.

The skills as delivered do not. Read before drafting, they impose one house aesthetic: React or Next with Tailwind, Geist or Satoshi, Phosphor icons, spring(100, 20), mandatory light and dark modes, and mandatory image generation. They also contradict each other and the brand rules of the sites they were installed in. `slop-audit` keeps the diagnosis and drops the prescriptions. It runs after drafting, and the brand kit and CLAUDE.md always win.

| Skill (install name) | Verdict | Why |
|---|---|---|
| `design-taste-frontend` | Distilled into slop-audit | Best tells catalogue; 1,206 lines (~22k tokens); contradicts itself; buggy GSAP skeletons |
| `design-taste-frontend-v1` | Retire | Superseded; its "perpetual loop in every card" Bento look is now a tell itself |
| `gpt-taste` | Retire | Written for GPT/Codex; "simulated Python RNG" layout picks; contradicts v2 on centred heroes |
| `high-end-visual-design` | Retire | Its signatures (double-bezel cards, arrow-in-circle buttons, pill nav, blur-up entries) are now tells; assumes paid fonts are installed |
| `minimalist-ui` | Only on request | Essentially Notion's palette; prescribes faux macOS window chrome that v2 bans |
| `industrial-brutalist-ui` | Keep for the right brief | Most coherent style skill; no accessibility guidance; uses ® and ™ as decoration |
| `redesign-existing-projects` | Distilled into slop-audit | Good audit list; no preserve-the-brand mode; "randomize blog dates to appear real" |
| `full-output-enforcement` | Retire | Targets the 2023 "lazy GPT-4" problem; in an agent with file tools it mostly adds length |
| `stitch-design-taste` | Only with Google Stitch | Recommends the serifs v2 bans; accent palette is stock Tailwind 500s |
| `image-to-code` | Not for Claude Code | Step one is "generate images yourself"; Claude Code has no image generator |
| `imagegen-frontend-web`, `imagegen-frontend-mobile`, `brandkit` | Keep in this library | Solid prompting for ChatGPT Images or Codex; irrelevant inside a code session |

## Evidence

Contradictions inside `skills/taste-skill/SKILL.md`:

- Line 618 says to use "organic, messy data (47.2%)"; line 327 bans AI-invented precise numbers.
- Line 641 allows a simple "Scroll" cue; line 682 bans scroll cues.
- Line 258 bans the split header; line 674 prescribes a clean two-column header.
- Line 214 recommends `divide-y`; line 307 calls it the lazy default.
- Line 143 says never hand-roll SVG; line 279 says to invent an SVG mark.
- Line 9 says nothing fires automatically; line 914 calls a 62-item checklist not optional.

Contradictions across skills:

- v2 bans Fraunces and Instrument Serif as defaults; stitch recommends exactly those.
- soft-skill puts a pill eyebrow above every heading; v2 allows one per three sections.
- soft-skill bans Lucide for being thick; minimalist bans it for being thin.
- Inter is banned in four skills and recommended in brutalist.

Code defects in the canonical skeletons:

- The sticky-stack applies CSS `sticky` and GSAP `pin` to the same element (lines 391 and 415).
- The horizontal pan captures `distance` once, so `invalidateOnRefresh` cannot fix it on resize (line 446).
- The GSAP skeleton imports Motion's hook, against line 779.
- `transition: all` contradicts the transform-and-opacity rule (line 562).
- gpt-taste wraps the page in `overflow-x-hidden`, which breaks `position: sticky`.
- `npm install uswds` is the deprecated package name; it is now `@uswds/uswds`.

Credibility hazards, all removed in slop-audit:

- Fabricating "messy" data so it looks real.
- Randomising dates.
- Real-company logo walls with no customer check.
- Decorative registration marks.
- Paid typefaces assumed available.

Collisions with installed brands:

- NPSI uses hand-authored HTML, Source Serif 4 and Google Fonts.
- JucheGang uses Playfair and is dark-only.
- Fit For Gov uses Instrument Serif on #F5F3EE with oxblood and copper, which is v2's banned "premium-consumer" palette plus a banned serif.

Where the pack worked: npsi-site commit 5b92895 (July 2026). It was used as an audit lens under the house rules and produced a light scheme, grain, and scroll-driven reveals with reduced-motion off-switches. That is the use slop-audit formalises.

## Still to do

Replace the pack with `slop-audit` in the three site repos. In each repo:

- delete `.agents/` and `skills-lock.json` (both contain only this pack);
- delete the pack's entries under `.claude/skills/`, keeping the repo's own skills;
- copy `skills/slop-audit/SKILL.md` to `.claude/skills/slop-audit/SKILL.md`.

This edits the skills an agent loads, so it is done by the owner, not by an agent.
