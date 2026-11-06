# GeoLab measurement record

- Source: `index.html`, `styles.css`, `js/app.js` (before the 2026-11-06 interface refinement)
- Sample: workbench with demo construction (10 objects, slider, function, circle, segment, intersections)
- Viewport: 1440 × 900, light theme, desktop density
- Additional checks: narrow layout at 390 × 844 and 820 × 700 in browser screenshots
- Measurement method: rendered page + `getComputedStyle`; canvas colors read from `js/app.js`
- Coverage limit: light theme only; no dark theme exists; no async loading state exists

## Text roles

| Text role | Sample element | font-family | font-size | font-weight | line-height | Viewport |
|---|---|---|---|---|---|---|
| Brand title | `.brand-text h1` | system sans | 15.5px | 700 | 17.05px | 1440×900 |
| Brand subtitle | `.brand-text p` | system sans | 10.5px | 400 | normal | 1440×900 |
| Command input | `#cmdInput` | system sans | 13.5px | 400 | normal | 1440×900 |
| Inspector section label | `.algebra-head` | system sans | 10.5px | 700 | normal | 1440×900 |
| Math row title | `.obj-title` | Cambria Math / Georgia serif | 13.5px | 400 | 19.575px | 1440×900 |
| Object name | `.obj-name` | Cambria Math / Georgia serif | 13.5px | 700 | 19.575px | 1440×900 |
| Row metadata value | `.obj-value` | system sans | 10.5px | 400 | 15.225px | 1440×900 |
| Object type tag | `.obj-type` | system sans | 9px | 500 | normal | 1440×900 |
| Onboarding title | `.empty-card h2` | system sans | 23px | 700 | normal | 1440×900 |
| Onboarding body | `.empty-card > p` | system sans | 12.5px | 400 | 21.875px | 1440×900 |
| Onboarding eyebrow | `.empty-kicker` | system sans | 9.5px | 800 | normal | 1440×900 |
| Help dialog title | `.modal-head h2` | system sans | 21px | 700 | normal | 1440×900 |
| Help example code | `.example code` | Cambria Math / Georgia serif | 12px | 400 | normal | 1440×900 |
| Help example description | `.example span` | system sans | 10.5px | 400 | 14.175px | 1440×900 |
| Keyboard legend | `kbd` | system sans | 9.5px | 400 | 12.35px | 1440×900 |
| Status readout | `.status-pill` | SFMono / Menlo | 10.5px | 400 | normal | 1440×900 |

## Color roles

| Color role | Computed value | Location | Theme |
|---|---|---|---|
| Page background | `#edf2f9` | `body` | light |
| Canvas background | `#fbfcff` | `PLOT` / canvas fill | light |
| Panel background | `#ffffff` | `.sidebar`, `.topbar`, `.toolbar` | light |
| Primary text | `#0f172a` | `body`, headings | light |
| Math definition text | `#40506a` | `.obj-def` | light |
| Primary button / active tool | `#2563eb` | `--accent`, `.tool.is-active` | light |
| Primary action hover | `#1d4ed8` | `--accent-strong` | light |
| Selected row | `#eaf1ff` | `.obj-row.is-selected` | light |
| Border | `#e5ebf3` | panels, rows | light |
| Strong border | `#d7e0ec` | inputs, chips | light |
| Secondary text | `#64748b` | most metadata | light |
| Tertiary text | `#94a3b8` | input help, foot hint, type tags | light |
| Danger | `#dc2626` | errors, delete hover | light |
| Success | `#059669` | success toast | light |
| Series palette | `#2563eb #059669 #dc2626 #d97706 #7c3aed #0891b2 #db2777 #65a30d #ea580c #4f46e5` | `PALETTE` in `js/app.js` | light |
| Minor grid | `#eef2f8` | canvas | light |
| Major grid | `#e1e8f2` | canvas | light |
| Axis | `#93a4bb` | canvas | light |
| Axis tick labels | `#7b8ba3` | canvas | light |

## Spacing and layout

| Relation | Value | Viewport |
|---|---|---|
| Top bar height | 58px | 1440×900 |
| Tool rail width | 58px | 1440×900 |
| Inspector width | 352px | 1440×900 |
| Canvas width | 1030px | 1440×900 |
| Object row padding | 8px 7px | 1440×900 |
| Object row gap | 6px | 1440×900 |
| Inspector horizontal padding | 16px header, 8px list | 1440×900 |
| Input shell height | 41px | 1440×900 |
| Empty card width | 450px | 1440×900 |
| Empty card padding | 27px 28px 22px | 1440×900 |
| Help dialog width | 780px | 1440×900 |
| Help dialog padding | 25px 28px 22px | 1440×900 |
| Breakpoints | 1080px, 900px, 560px | from `styles.css` |
| Dark theme | not supported | — |

## Observed states

- Default workbench, selected row, hidden row, undefined intersection, empty onboarding, help dialog, tool hint, toast, focus-within input.
- The selected row uses accent-soft background plus a 1px inset accent line.
- The delete button is opacity 0 until row hover; it has no focus-visible reveal and no hover-none fallback.
- Metadata text uses `#94a3b8` at 9–10.5px in several places, including type tags and input help.
- Object type is printed as a small pill in every algebra row while the definition already exposes the type.
- Input focus is shown by the `.input-shell` border and 4px accent ring; the input itself has `outline: 0`.

## Facts vs inferences

- Observation: The visual system is a canvas-first workbench with a restrained blue accent, hairlines, rounded floating surfaces, serif math, and a categorical series palette.
- Observation: The application has no dark theme, no data-loading screen, and no decorative illustrations.
- Inference: Readers need the canvas to stay dominant; removing non-essential pills and increasing metadata contrast should improve scan speed. This was treated as a `[SHOULD]` decision in `design.md`.
- Decision: The centered onboarding card is a transient empty state, not the default page template. It may stay centered.
