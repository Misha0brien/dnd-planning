# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A static HTML personal site synthesizing D&D and game design theory from YouTube creators. Each page is a self-contained `.html` file — no build system, no package manager, no dependencies beyond Google Fonts. Open files directly in a browser to view.

All content must credit the original creator(s) in the footer attribution block. No content is original; all methodology is sourced and cited.

## Architecture

Each page is a **single self-contained HTML file** with:
- Inline `<style>` block in `<head>` — all CSS lives here, never in external files
- Semantic HTML body content
- Inline `<script>` block at the bottom of `<body>` — all JS lives here

`index.html` is the canonical template. All new pages must match its design system exactly — colors, fonts, spacing, and component patterns.

## Design System (from `index.html`)

### CSS Custom Properties
```css
--ink: #0D0F1A        /* page background */
--deep: #131525       /* nested backgrounds */
--slate: #1C1F35      /* card backgrounds */
--panel: #22263D      /* elevated panels */
--border: #2E3356     /* all borders */
--gold: #C9A84C       /* primary accent, headings */
--gold-dim: #8A6B2A   /* subdued gold */
--gold-glow: rgba(201,168,76,0.18)
--amber: #E8C46A      /* h3 headings */
--crimson: #8B2635    /* danger/failure */
--mist: #8B92B8       /* secondary text, em */
--pale: #C8CCDF       /* body text */
--white: #EEF0F8      /* strong/emphasized text */
--meta-col: #7B5EA7   /* meta loop — purple */
--prog-col: #2E7D6B   /* progress loop — teal */
--core-col: #8B5E3C   /* core loop — brown */
```

### Typography
- **Google Fonts:** `Cinzel` (all UI labels, nav, headers), `Cinzel Decorative` (page `<h1>` only), `Crimson Pro` (body text)
- `h1`: Cinzel Decorative, clamp(28px, 5vw, 52px), `--white`
- `h2`: Cinzel, 13px, uppercase, letter-spacing 0.18em, `--gold` — section titles
- `h3`: Cinzel, 13px, `--amber` — subsection titles
- `h4`: Cinzel, 11px, uppercase, `--mist` — minor labels
- Body: Crimson Pro, 18px, line-height 1.7, `--pale`

### Reusable Components

**Step Cards** — `<details class="step-card">` with `<summary class="step-header">` containing `.step-number`, `.step-title`, `.step-chevron`. Body is `.step-body` with 92px left padding.

**Badges** — `<span class="badge meta|prog|core">` — inline colored labels for loop types.

**Callouts** — `.callout` (gold), `.callout.example` (purple), `.callout.warning` (brown). Always include a `.callout-label` div.

**Flowcharts** — `.flow-wrap` container (click-to-expand lightbox) containing `.flow-node` elements. Node variants: `.trigger`, `.outcome-good`, `.outcome-bad`, `.loop-back`. The `data-title` attribute on `.flow-wrap` populates the modal title.

**Tables** — wrap in `.table-wrap` for horizontal scroll. Use `<th>` with Cinzel styling; `<td>` with 15px font.

**Lightbox Modal** — `#flow-modal` with `openModal(this)` passed from `.flow-wrap` onclick. Required DOM: `#flow-modal`, `#flow-modal-inner`, `#flow-modal-title`, `#flow-modal-close`, `#flow-modal-content`.

**Divider** — `<hr class="divider">` renders a centered `✦` glyph.

**Progress tracks** — `.progress-tracks` 2-col grid of `.track-card` with `.track-name` and `.track-steps` > `.track-step`.

**Theory block** — `.theory-block` — used for non-step reference sections (e.g., intro theory, reference summary).

### Navigation
Hero section contains `.step-nav` with `.nav-pill` anchor links (`href="#section-id"`). Every new major section should get a nav pill.

## Content Standards

- **Tone:** Engaging and educational — the register of a well-delivered TED talk. Not academic, not conversational. Vary sentence length for rhythm; complex constructions are appropriate when the idea warrants them. Assume reader familiarity with D&D and game design vocabulary.
- **Attribution:** Every page footer must credit the specific YouTube creator and link to the source video and channel.
- **Examples:** Use `.callout.example` blocks with `✦ Example — [Campaign Name]` labels to ground abstract principles in concrete cases.
- **Design order:** When adding new framework content, mirror the outside-in structure: theory block → numbered step cards → reference summary.

## Writing Style Rules

- **No em-dash asides.** Do not use `—` to insert parenthetical clarifications mid-sentence. Restructure into a separate sentence instead.
- **No similes.** Do not use "like" or "as" comparisons to explain concepts. State things directly.
- **In analysis sections, suggest tendencies rather than assert certainties.** Use "can," "tends to," "may," and "often" rather than "is" or "will." Every observation about how types or players interact should briefly state the mechanism — why the dynamic could emerge — not just declare that it does.
