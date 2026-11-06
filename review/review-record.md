# GeoLab interface review record

Scenario: GeoLab workbench with a demo construction  
Input: 10 objects — slider `a = 2`, function `f(x) = a sin(x)`, point `O`, circle `c = Circle(O, 3)`, points A/B, segment s, midpoint M, two circle–segment intersections C/D  
Viewports: 1440 × 900 (desktop), 390 × 844 (narrow canvas + drawer + help dialog)  
Theme: light  
design.md version: 2026-11-06  
Generation context: current context that saw the source material (extract-and-refine; weaker evidence than a new-context generation)  
Review method: Chromium browser rendering, screenshots, `getComputedStyle`, DOM checks, keyboard focus traversal, modal focus checks, and a functional regression of slider, drag, and undo  
Result: pass after one recheck

## Checks

- Exactly one `h1` at 1440 and 390. Pass.
- `document.documentElement.scrollWidth` equals the viewport at 1440 and 390, with the drawer closed and open. Pass.
- No tables exist, so the column-alignment invariant is not applicable.
- All referenced assets return HTTP 200: `styles.css`, `js/parser.js`, `js/geom.js`, `js/app.js`, `preview.png`. Pass.
- Every referenced CSS custom property is defined and resolves. Pass.
- No duplicate element IDs. Pass.
- No visible interactive control lacks an accessible name. Pass.
- Exactly one tool exposes `aria-pressed="true"`; all other tools expose `false`. Pass.
- No visible text below `11px` in the default workbench state; keyboard legends and the eyebrow are `10px` by rule. Pass.
- Key text contrast (metadata, values, help copy, status, definitions, close control, kicker) is at least `4.5:1`. Pass; the measured minimum in the checked set is `4.68:1`.
- Series text colors meet `4.5:1` against both white and the selected-row `--accent-soft`. Pass.
- Keyboard focus is visible on top-bar actions, tools, the command input shell, row eye/delete actions, slider, footer, and mini link. Pass.
- The delete action is visible on keyboard focus (`opacity: 1`). A `@media (hover: none)` fallback exists in CSS; no touch hardware was available for visual confirmation.
- Help dialog: opening focuses the close control, Tab and Shift+Tab cycle inside, Escape closes and restores focus to the opener, and the panel is named by its heading. Pass.
- Functional regression: slider change and undo, point drag and undo, and object dependencies all behave as before. Pass.
- Default view at 390: 100% zoom, approximately 10.6 world units across, whole demo construction visible. Pass.
- Default view at 1440: 100% zoom, unchanged 64 px/unit desktop scale. Pass.
- Drawer at 390: left edge 52px (does not cover the tool rail), width 338px, no page overflow. Pass.
- Help dialog at 390: one column (302px), panel width 342px, no inner horizontal overflow. Pass.

## Violations found and fixed

- Implementation error / accessibility: the old keyboard focus outline used `rgba(37, 99, 235, 0.45)` and the focused input border was `#98b7ff`; both were below a clear focus-indicator contrast. Fixed with a solid `#2563eb` outline and accent input border.
- Implementation error / accessibility: delete was hover-only, with no focus reveal and no hover-none fallback. Fixed with `row-del:focus-visible` and a `@media (hover: none)` rule.
- Implementation error / accessibility: metadata at 9–10.5px used `#94a3b8`; several series colors failed 4.5:1 as text, and `--danger` failed on the selected-row background. Fixed with an 11px metadata floor, `--muted-2` metadata, `SERIES_TEXT_PALETTE`, deeper amber/lime variants, `--danger: #b91c1c`, and `--muted` values.
- Implementation error / accessibility: opening the help dialog left focus on the trigger behind the overlay. Fixed with initial focus, focus containment, labelled dialog semantics, and focus return.
- Implementation error / responsive: the mobile drawer covered part of the tool rail at 320–390px. Fixed with `width: min(350px, 100% - 52px)`, so it starts at the rail edge.
- Implementation error / responsive: the desktop 64 px/unit scale produced a too-narrow world on phones. Fixed with `clamp(canvasWidth / 16, 32, 64)` for initial and reset views; zoom percentage is relative to that default.
- Implementation error: the zoom readout did not refresh after a viewport change. Fixed by updating it from `resizeBoard`.
- Deviation / anti-pattern: every algebra row showed a 9px type pill and the object count used a pill. Removed the visible pills; type remains available through `.sr-only`. The object count is plain metadata.
- Deviation / copy: the cursor and zoom readout were two separate pills; merged into one status strip. The coordinate readout now uses `x = … · y = …`.
- Deviation / anti-pattern: the empty algebra area used a decorative blue icon tile. Removed; it is now a short text block.

## Remaining deviations (intentional)

- The onboarding surface stays centered and card-like. It is a transient empty state, not the default page structure; no other page uses a centered card or a card grid.
- English eyebrows remain only in onboarding (`Interactive Mathematics`) and help (`GeoLab Manual`). They are brand copy, not actionable labels.
- The interface is light-only. A dark theme is not partially styled or improvised.
- The graph is redrawn immediately and is not animated. The absence of chart animation is intentional.
- Deletion and point dragging on the canvas remain pointer-first; the inspector exposes hide/delete buttons for keyboard users. Full keyboard object selection is not implemented.

## Open questions

- Whether canvas object selection should gain a keyboard or sequential selection model in a future round.
- Whether a dark theme is needed; it would require a full palette and a new review.
- Whether very long formulas and very large coordinate values need additional truncation rules beyond `word-break` and horizontal containment.

## Limits

- Light theme only; no dark-theme review.
- No screen-reader or assistive-technology session; the review covers DOM semantics, accessible names, focus movement, and computed styles.
- No automated visual-diff baseline; screenshots and measured styles were inspected at the two viewports.
- The help dialog's background is not made `inert`; focus is contained by the Tab handler and the overlay blocks pointer input.
- No loading state exists, so loading was not reviewed.
- No touch-device session was available; the `hover: none` delete fallback is verified in code, not on hardware.
- The automation harness delivered Enter keydown/keyup to focused buttons but did not synthesize the browser's default click. Focus visibility, Tab traversal, and modal focus containment were verified; button activation by Enter is left to the browser default and was not observed end-to-end.
- Very long text and extreme numeric magnitudes were not exhaustively reviewed.

## Rule updates written to design.md

- Series text palette with 4.5:1 text variants; canvas strokes use the base palette.
- Metadata floor and token roles for secondary text, idle icons, and danger.
- Solid focus outline, accent input focus border, focus reveal for destructive actions.
- Help dialog focus management and labelled dialog semantics.
- Responsive drawer width and viewport-aware default graph scale.
- Status strip as one surface with the coordinate format.
- No visible type pills; visually hidden type context.
- `aria-pressed` on the active tool.
- Help-dialog focus movement, containment, and return.
- Documented component tints, overlay values, and the two icon-glyph exceptions.

## Artifacts

- `review/measurements.md` — pre-change measurement record.
- `review/before-desktop.png`, `review/before-narrow.png` — first render before the refactor.
- `review/after-desktop-final.png` — final desktop workbench.
- `review/after-narrow-final.png` — final narrow workbench.
- `review/after-narrow-drawer-final.png` — final narrow drawer.
- `review/after-empty.png` — final onboarding/empty state.
- `review/after-help.png`, `review/after-help-narrow.png` — help dialog at desktop and narrow widths.
- `review/focus-delete-keyboard.png` — keyboard focus on a row delete action.
- `preview.png` — final 1440 × 900 project preview.
