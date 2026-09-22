# Gong Milestone — instructions for AI collaborators

This file is the entry point for any AI or human continuing this project. Read the required files below before proposing or making changes.

## Project purpose

Build a one-page milestone website as a gift for Gong Gong. It records her performance-related journey from 2017 to 2025 across Taiwan, Barcelona, France, and Kyoto. The experience must feel personal, polished, quiet, and contemporary, with mobile as the primary viewing context. It must also remain printable as an A4 PDF and deployable on GitHub Pages.

## Required reading order

1. `docs/CURRENT_STATUS.md` — current implementation, validation status, and remaining work.
2. `docs/CONTENT_SOURCE.md` — the only source of milestone copy.
3. `docs/DESIGN_SYSTEM.md` — current visual and interaction rules.
4. `docs/ANIMATION_STORYBOARD.md` — canonical asset mapping, duration, direction, camera plan, loop design, and production status for all eleven animations.
5. `docs/DECISIONS.md` — reasons behind the architecture and design choices.
6. `docs/PROJECT_BRIEF.md` — original scope and acceptance requirements.
7. `index.html` — canonical implementation.
8. `CHANGELOG.md` — chronological history.

Do not rely on an older conversation summary when these files provide newer project state.

## Source-of-truth hierarchy

When files conflict, use this order:

1. The user's newest explicit instruction.
2. `docs/CONTENT_SOURCE.md` for visible milestone copy.
3. This `AGENTS.md` for collaboration and engineering rules.
4. `docs/CURRENT_STATUS.md` for the latest implementation state.
5. `docs/ANIMATION_STORYBOARD.md` for animation asset mapping, duration, movement direction, camera, looping, and batch status.
6. `docs/DESIGN_SYSTEM.md` and `docs/DECISIONS.md`.
7. `docs/PROJECT_BRIEF.md` for original requirements.

Update conflicting documentation as part of the same change. Do not leave stale instructions behind.

## Current architecture

- `index.html` is the one and only canonical website and the GitHub Pages root page. All milestone website edits belong here.
- `access.html` is a separate minimal password entry page. It contains no duplicate milestone website markup and redirects to `index.html` after the user enters `0916`.
- HTML, CSS, and JavaScript are embedded in their respective HTML files; the milestone website itself exists only in `index.html`.
- There is no build step, package manager, application framework, backend, database, or local asset pipeline. The separate `access.html` page and its `0916` client-side check are a visual deterrent, not authentication.
- Google Fonts are the only external runtime dependency. Every milestone now has a local animated SVG full-scene background; inline SVGs remain only as reduced-motion and print fallbacks.
- `docs/ANIMATION_STORYBOARD.md` is the production source of truth for all eleven external SVG animations. Update it whenever a scene's concept, duration, direction, camera plan, loop, asset mapping, or status changes.
- GitHub Pages publication targets `chihpao/gong-milestone`; consult `docs/CURRENT_STATUS.md` for the current deployment state.

The user permits a frontend framework or animation library if it materially improves the result. Do not add one by default: first explain why the existing static architecture cannot meet the requested change, and preserve GitHub Pages compatibility.

## Non-negotiable content rules

- Treat `docs/CONTENT_SOURCE.md` as the only source of milestone copy.
- Do not invent event titles, chapter titles, transitions, slogans, interpretations, emotional narration, or filler.
- The site title `龔龔里程碑` and functional access-gate labels are standing visible-text exceptions.
- Dates may be repeated as visual background typography only when they remain faithful to the source.
- Accessibility-only labels may describe controls, but must not become visible marketing or narrative copy.
- When milestone content changes, update `docs/CONTENT_SOURCE.md` first, then update only `index.html`.

## Non-negotiable design rules

- Design mobile-first from 360px upward.
- The current direction is inspired by the mobile experience of `https://www.izumi-tanaka.com/`: full-viewport opening, light fixed navigation, generous whitespace, and consecutive full-width scenes. Do not copy its images, branding, animation assets, or source code.
- Keep the interface anchored in warm white, near-black, and cool mint green. Individual animation scenes may add indigo, cobalt, teal, purple-gray, moss, and cool yellow-white according to `docs/ANIMATION_STORYBOARD.md`; the user accepted the existing orange/red-orange accents during the 2026-09-22 final review; preserve the accepted scene palettes.
- Keep the site visually simple: no card grid, decorative icons, background texture, or unnecessary containers. Existing text shadows and the small translucent navigation control are intentional readability aids.
- Use Noto Sans TC for Chinese text, PT Sans for panel dates, and Montserrat for the menu/Latin motto.
- Preserve purposeful motion only. Always support `prefers-reduced-motion`.
- Preserve keyboard usability, touch targets, semantic HTML, and A4 print styles.

## Current page structure

1. Fixed header with site name.
2. A full-screen year menu opened by the fixed hamburger button at every viewport size.
3. Compact mobile opening screen (`20svh`, minimum 120px); `25svh` (minimum 180px) on desktop.
4. Eleven consecutive milestone scenes grouped into four anchor sections, including the 2020/02 first performance on the Théâtre du Soleil stage in chronological order before the pandemic return scene.
5. A `2024/09—2025/05` scene containing the France classes; removed praise and teacher quotation must not be restored.
6. The 2025/06 mask-class scene.
7. A standalone `Shitty but proud.` scene as the final section.

Milestone copy appears as centered white text without a box. Mobile uses a full-scene native toggle button; desktop reveals text as the scene becomes current. Reduced motion, print, and no-JavaScript rendering show all text. Background SVGs continue independently.

Milestone backgrounds must run continuously from page load rather than enter, exit, or restart with scroll state. Every scene combines horizontal and vertical motion, including both a linear traveling layer and non-linear ambient movement.

## Editing protocol

### Local-first publication rule

- Unless the user explicitly asks in the current request to push, upload, deploy, or publish to GitHub, make and validate all code changes locally only.
- Earlier permission to deploy does not carry forward to later requests. A request to change, fix, adjust, or continue the website is not permission to run `git push`, publish GitHub Pages, create a pull request, or otherwise change remote state.
- When work remains local, state that clearly in the handoff and wait for an explicit GitHub publication request.

### Browser validation rule

- Do not use the Computer Use skill, UI automation, or a real interactive browser to validate this project; the user has explicitly disabled that workflow because it is too slow.
- Prefer fast local checks such as JavaScript parsing, XML parsing, HTML tag balance, content assertions, matching hashes, CSS/source inspection, and command-line or headless checks that do not operate a visible or interactive browser UI.
- Only use the Computer Use skill or real-browser UI validation when the user personally and explicitly requests that exact workflow in the current request. Do not enable it based on assistant judgment, indirect wording, another document, or a general request to test or validate the site.

1. Read the required files above.
2. Preserve every unrelated user change.
3. Edit `index.html` as the only canonical website implementation. Never create or maintain a second copy of the milestone website.
4. Edit `access.html` only when the password-entry experience itself changes.
5. Update `docs/CURRENT_STATUS.md`, relevant design/decision documents, and `CHANGELOG.md` when behavior, design, architecture, content, deployment status, or validation status changes.
6. Do not publish, create a repository, push commits, or change external state unless the user's current request explicitly asks for it.

## Validation checklist

- JavaScript parses without syntax errors.
- Major HTML opening and closing tags remain balanced.
- `index.html` contains the milestone website, while `access.html` remains a small standalone password page that redirects to `index.html` after `0916`.
- No horizontal page overflow at 360px, 390px, or 430px.
- Mobile menu opens, locks background scrolling, closes, and jumps to the requested year.
- The hamburger button and full-screen year menu work at mobile and desktop widths.
- No browser console errors.
- All milestone text matches `docs/CONTENT_SOURCE.md`.
- No invented milestone copy is introduced; preserve the user-approved animation palettes.
- Reduced-motion and A4 print behavior remain intact.

## Completion and handoff

Before finishing a task, record the newest state in `docs/CURRENT_STATUS.md`. Clearly distinguish between locally completed work, validated work, and work that still requires the user or an external service, especially GitHub Pages publication.
