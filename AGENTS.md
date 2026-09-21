# Gong Milestone — instructions for AI collaborators

This file is the entry point for any AI or human continuing this project. Read the required files below before proposing or making changes.

## Project purpose

Build a one-page milestone website as a gift for Gong Gong. It records her performance-related journey from 2017 to 2025 across Taiwan, Barcelona, France, and Kyoto. The experience must feel personal, polished, quiet, and contemporary, with mobile as the primary viewing context. It must also remain printable as an A4 PDF and deployable on GitHub Pages.

## Required reading order

1. `docs/CURRENT_STATUS.md` — current implementation, validation status, and remaining work.
2. `docs/CONTENT_SOURCE.md` — the only source of milestone copy.
3. `docs/DESIGN_SYSTEM.md` — current visual and interaction rules.
4. `docs/DECISIONS.md` — reasons behind the architecture and design choices.
5. `docs/PROJECT_BRIEF.md` — original scope and acceptance requirements.
6. `index.html` — canonical implementation.
7. `CHANGELOG.md` — chronological history.

Do not rely on an older conversation summary when these files provide newer project state.

## Source-of-truth hierarchy

When files conflict, use this order:

1. The user's newest explicit instruction.
2. `docs/CONTENT_SOURCE.md` for visible milestone copy.
3. This `AGENTS.md` for collaboration and engineering rules.
4. `docs/CURRENT_STATUS.md` for the latest implementation state.
5. `docs/DESIGN_SYSTEM.md` and `docs/DECISIONS.md`.
6. `docs/PROJECT_BRIEF.md` for original requirements.

Update conflicting documentation as part of the same change. Do not leave stale instructions behind.

## Current architecture

- `index.html` is the canonical website and the GitHub Pages entry point.
- `GongGong_Milestone.html` is a compatibility copy and must remain byte-identical to `index.html` while it exists.
- HTML, CSS, and JavaScript are embedded in the two HTML files.
- There is no build step, package manager, application framework, backend, database, or local asset pipeline. The `0916` client-side gate is a visual deterrent, not authentication.
- Google Fonts are the only runtime dependency.
- GitHub Pages publication targets `chihpao/gong-milestone`; consult `docs/CURRENT_STATUS.md` for the current deployment state.

The user permits a frontend framework or animation library if it materially improves the result. Do not add one by default: first explain why the existing static architecture cannot meet the requested change, and preserve GitHub Pages compatibility.

## Non-negotiable content rules

- Treat `docs/CONTENT_SOURCE.md` as the only source of milestone copy.
- Do not invent event titles, chapter titles, transitions, slogans, interpretations, emotional narration, or filler.
- The site title `龔龔里程碑` and functional access-gate labels are standing visible-text exceptions.
- Dates may be repeated as visual background typography only when they remain faithful to the source.
- Accessibility-only labels may describe controls, but must not become visible marketing or narrative copy.
- When content changes, update `docs/CONTENT_SOURCE.md` first, then both HTML files.

## Non-negotiable design rules

- Design mobile-first from 360px upward.
- The current direction is inspired by the mobile experience of `https://www.izumi-tanaka.com/`: full-viewport opening, light fixed navigation, generous whitespace, and consecutive full-width scenes. Do not copy its images, branding, animation assets, or source code.
- Use warm white, near-black, and cool mint green. Do not use orange or red-orange.
- Keep the site visually simple: no card grid, decorative icons, shadows, background texture, or unnecessary containers.
- Use Noto Sans TC for Chinese text and Montserrat for dates/Latin text.
- Preserve purposeful motion only. Always support `prefers-reduced-motion`.
- Preserve keyboard usability, touch targets, semantic HTML, and A4 print styles.

## Current page structure

1. Fixed header with site name.
2. A full-screen year menu opened by the fixed hamburger button at every viewport size.
3. Compact mobile opening screen (`20svh`, minimum 120px); `100svh` on desktop.
4. Ten consecutive milestone scenes grouped into four anchor sections; the 2020/03 return and 2020/03—2023/11 stay are one combined scene.
5. A combined `2024/09-2025/05` scene containing the France classes, monthly praise, and teacher quotation.
6. The 2025/06 mask-class scene.
7. A standalone `Shitty but proud.` scene as the final section, with the user-authored blessing appearing last.

## Editing protocol

1. Read the required files above.
2. Preserve every unrelated user change.
3. Edit `index.html` as the canonical implementation.
4. Synchronize the final result to `GongGong_Milestone.html` and confirm matching hashes.
5. Update `docs/CURRENT_STATUS.md`, relevant design/decision documents, and `CHANGELOG.md` when behavior, design, architecture, content, deployment status, or validation status changes.
6. Do not publish, create a repository, or change external state unless the user asks.

## Validation checklist

- JavaScript parses without syntax errors.
- Major HTML opening and closing tags remain balanced.
- `index.html` and `GongGong_Milestone.html` hashes match.
- No horizontal page overflow at 360px, 390px, or 430px.
- Mobile menu opens, locks background scrolling, closes, and jumps to the requested year.
- The hamburger button and full-screen year menu work at mobile and desktop widths.
- No browser console errors.
- All milestone text matches `docs/CONTENT_SOURCE.md`.
- No invented narrative copy or orange/red-orange design values are introduced.
- Reduced-motion and A4 print behavior remain intact.

## Completion and handoff

Before finishing a task, record the newest state in `docs/CURRENT_STATUS.md`. Clearly distinguish between locally completed work, validated work, and work that still requires the user or an external service, especially GitHub Pages publication.
