---
name: geolab-design
description: Visual system for GeoLab's canvas-first mathematical workbench, its inspector, onboarding overlay, and help dialog. Applies to the light theme from wide desktop to the narrow drawer layout.
version: 2026-11-06
---

# GeoLab design

## 1. Scope and Priority

- Applies to the GeoLab workbench, its floating canvas controls, the inspector, the onboarding overlay, and the help dialog.
- Applies to the light theme only. A dark theme is not supported and must not be improvised.
- Does not apply to marketing pages, documentation sites, or a future account flow.
- Priority when rules conflict: user task and mathematical facts → accessibility and usability → reader task → project conventions → brand expression → decoration.
- The canvas is the primary surface. Chrome and inspector recede. A visual treatment that competes with plotted objects is wrong even if it is attractive.

## 2. Brand and Readers

- Brand traits: precise, calm, crafted.
  - Precise: values are tabular; labels align to the same edge; strokes use a 1px hairline or an exact 2px data stroke, never a 1.5px accident.
  - Calm: surfaces are white or near-white; one blue accent marks active, focused, or primary state; category colors appear only on plotted objects and their names.
  - Crafted: math is set in a serif face; controls have deliberate hover and focus states; floating surfaces use one restrained shadow.
- Readers: students, teachers, and technical users who read formulas and coordinates, work with a pointer and a keyboard, and need to compare many objects quickly. Desktop is the primary viewport; tablet and phone are secondary.
- Copy tone: terse Chinese UI, verb first, no exclamation marks, no marketing claims. Errors name the failed input and the correction. English is limited to the product name and the two eyebrows "Interactive Mathematics" and "GeoLab Manual".
- The interface must feel like a workbench, not a landing page: no hero, no card grid, no decorative illustrations, no stock imagery.

## 3. Page Structure and Composition

### Workbench

- The first viewport is the complete workbench: a `56px` top bar, a `56px` left tool rail, a flexible canvas, and a `352px` right inspector. The document does not scroll; only the inspector list scrolls.
- Primary content is the canvas. It fills all remaining width and height. Secondary content is the inspector. The tool rail is tertiary chrome.
- The inspector has three fixed bands: input header, a scrolling algebra list, and a footer pinned to the bottom edge.
- Floating surfaces over the canvas are limited to the onboarding overlay, zoom controls, status strip, tool hint, and toast.
- The canvas has no border or card container. The plotting surface is the page region itself.

### Onboarding overlay

- Shown only when the construction is empty. It is a single centered surface, `448px` wide, with a soft translucent white background and a blurred backdrop.
- It contains one eyebrow, one display title, one body paragraph, one row of example chips, and one tip row. It is not a card grid, and no other page type copies this centered composition.
- The overlay does not block canvas gestures outside its controls; only the chip buttons receive pointer events.

### Help dialog

- A centered modal over a blurred dim layer. The panel is `768px` wide and capped at `86vh`; its own content scrolls.
- Desktop uses a two-column help grid. At `900px` and below it becomes one column.
- Sections are separated by hairlines, not by cards.
- [MUST] Opening the dialog moves focus to its close control. Tab and Shift+Tab cycle inside the dialog. Closing restores focus to the control that opened it. The dialog is named by its visible heading.

### Narrow layout

- At `1080px` and below the inspector is `320px` wide.
- At `900px` and below the inspector becomes a right-side overlay drawer (`min(350px, 100% - 52px)`), opened by the top-bar toggle. It never covers the tool rail. The canvas takes the full width. The tool rail is `52px`; tool buttons reduce to `38px` square. The brand subtitle is hidden.
- At `900px` and below the help panel uses `21px 20px 18px` padding so its two-column content still fits as one column.
- At `560px` and below the top bar is `52px`; top-bar icon buttons are `31px`; the status strip is hidden; zoom buttons are `33px`; the onboarding surface uses `14px` page padding and `20px 17px` inner padding.
- Reflow must preserve readable sizes. Never compress the inspector into an unusable sliver.

## 4. Visual Rules

### Typography

- UI font stack: `--sans` (`-apple-system, BlinkMacSystemFont, "Segoe UI", "PingFang SC", "Hiragino Sans GB", "Microsoft YaHei", sans-serif`).
- Math font stack: `--math` (`"Cambria Math", "STIX Two Math", Georgia, "Times New Roman", serif`).
- Numeric and coordinate readouts use `--mono` for the status strip and tabular numerals elsewhere.
- Type roles:
  - Kicker: `10px`, weight `800`, uppercase, `0.16em` tracking, accent color. Only onboarding and help eyebrows use this role.
  - Brand: `15px`, weight `700`.
  - Display: `22px`, weight `700`, `-0.02em` tracking. Onboarding title only.
  - Dialog title: `21px`, weight `700`, `-0.02em` tracking.
  - Section label: `12px`, weight `700`, normal case for Chinese; `0.04em` tracking where English is used.
  - UI text: `13px` for input, chips, body copy.
  - Math row: `13.5px`, `1.45` line height, serif. Names are italic `700`; definitions are `400` in `--ink-math`.
  - Value text: `12px`, `1.5` line height, sans, tabular numerals, `--muted`.
  - Metadata and help copy: `11px`, `1.5` line height, `--muted-2`.
  - Keyboard legend: `10px`, sans, `--muted`.
  - Status: `11px`, mono, tabular.
  - Toast and tool hint: `12px`.
- [MUST] Primary, interactive, and informational text is at least `11px` and meets `4.5:1` contrast against its surface. Only uppercase kickers and keyboard legends may use `10px`, and they must not carry primary information.
- [SHOULD] Do not use `#94a3b8` for informational text. Use `--muted-2` (`#64748b`) for body metadata, values, placeholders, and help copy. Reserve `--muted-3` (`#7b8ba3`) for idle non-text icons, and `--disabled` (`#9aa8bb`) for disabled controls only. (Decision; source: measurement record shows 9–10.5px metadata at low contrast.)
- [SHOULD] Math is never uppercased, condensed, or letter-spaced. Object names are italic; definitions and values are upright.
- Two icon glyphs sit outside the text scale: the command `ƒ` at `16px` in the input prefix, and the dialog close `×` at `20px`. They are ornaments, not type roles.

### Color

- Surfaces: `--bg #edf2f9` page, `--board #fbfcff` canvas, `--panel #ffffff` chrome, `--panel-soft #f6f9fd` input and empty algebra area, `--panel-footer #fcfdff` inspector footer.
- Text: `--ink #0f172a`, `--ink-soft #334155`, `--ink-math #40506a`, `--muted #52627a`, `--muted-2 #64748b`, `--muted-3 #7b8ba3`.
- Lines: `--line #e5ebf3`, `--line-strong #d7e0ec`, `--line-soft #edf1f7`.
- Accent: `--accent #2563eb`, `--accent-strong #1d4ed8`, `--accent-soft #eaf1ff`.
- Feedback: `--danger #b91c1c` for error text and borders, `--success #059669` for success borders. These are not series colors.
- Series palette, in order: `#2563eb`, `#059669`, `#dc2626`, `#d97706`, `#7c3aed`, `#0891b2`, `#db2777`, `#65a30d`, `#ea580c`, `#4f46e5`.
- Series text palette, mapped from the same order: `#1d4ed8`, `#047857`, `#b91c1c`, `#92400e`, `#6d28d9`, `#0e7490`, `#be185d`, `#3f6212`, `#c2410c`, `#4338ca`. These darkened variants meet `4.5:1` against both white and `--accent-soft` and are the only series colors permitted for text.
- [MUST] Canvas strokes, point fills, and select glows use `SERIES_PALETTE`. Inspector object names and canvas labels use `SERIES_TEXT_PALETTE`. Neither palette colors page chrome, buttons, borders, or status feedback.
- [MUST] The accent is the only hue for active, selected, focused, and primary controls. Selected rows use `--accent-soft` with a 1px inset `rgba(37, 99, 235, 0.13)` line.
- [SHOULD] The logo is the only gradient in the product. Do not add decorative gradients to cards, buttons, or headers.
- Canvas: background `#fbfcff`, minor grid `#f1f5fa`, major grid `#e4eaf3`, axis `#93a4bb`, ticks and axis labels `#64748b`, label halo `rgba(251, 252, 255, 0.94)`. These are exposed as `PLOT` in `js/app.js`.
- The status strip uses `rgba(255, 255, 255, 0.92)` and the standard hairline. It is a single surface, not a row of pills.

### Component tints and overlays

These values are part of the system. Do not substitute near-duplicate tints.

| Role | Value | Use |
|---|---|---|
| Tool hover | `#f1f5fa` | `.tool:hover` |
| Top-bar icon hover | `#f0f4fa` | `.icon-btn:hover` |
| Row hover | `#f7f9fd` | `.obj-row:hover` |
| Row icon hover | `#edf2f8` | `.row-eye:hover` |
| Zoom hover | `#f4f8fd` | `.zoom-controls button:hover` |
| Accent wash | `#f6faff` | Chip hover background |
| Help code wash | `#f3f7fe` | `.example code` background |
| Help hover / note surface | `#f6f9ff` | `.example:hover`, `.modal-note` |
| Keyboard key surface | `#f8fafc` | `kbd` |
| Quiet control surface | `#f4f7fb` | `.modal-close` background |
| Danger hover surface | `#fee9e9` | `.row-del:hover` |
| Slider track | `#dce6f5` | `.slider` background |
| Chip hover border | `#a8c4ff` | `.chip:hover` border |
| Foot-button hover surface | `#f4f8ff` | `.foot-btn:hover` background |
| Foot-button hover border | `#b9ceff` | `.foot-btn:hover` border |
| Note border | `#e4edff` | `.modal-note` border |
| Hover icon ink | `#475569` | Row and control icon hover |
| Hint Esc ink | `#aebbd0` | `.hint-esc` on the dark hint |
| Top-bar glass | `rgba(255, 255, 255, 0.94)` | `.topbar` |
| Onboarding glass | `rgba(255, 255, 255, 0.90)` | `.empty-card` |
| Status glass | `rgba(255, 255, 255, 0.92)` | `.statusbar` |
| Zoom glass | `rgba(255, 255, 255, 0.96)` | `.zoom-controls` |
| Toast glass | `rgba(255, 255, 255, 0.97)` | `.toast` |
| Modal dim | `rgba(15, 23, 42, 0.40)` | `.modal` overlay |
| Dark tooltip | `rgba(15, 23, 42, 0.94)` | Toolbar tooltip |
| Dark hint | `rgba(15, 23, 42, 0.92)` | Tool hint |
| Dark drag tooltip | `rgba(15, 23, 42, 0.90)` | Canvas drag readout |

### Layout, borders, radii, shadows

- Page uses `4px` as the spacing unit. Documented component values: top bar `56px`; tool rail `56px`; inspector `352px`; top-bar padding `16px`; list padding `8px`; object row `8px`; row gap `8px`; control gap `5px`; input shell padding `3px 4px 3px 10px`; footer padding `10px 13px 11px`; empty surface `448px` wide with `26px 28px 22px`; help panel `768px` wide with `26px 28px 22px`.
- Radii: `6px` row icon buttons, `8px` small buttons/status, `9px` icon buttons, `10px` rows, `11px` tool buttons, `12px` input shell/zoom/panels, `20px` onboarding surface, `22px` help panel, `99px` tool hint and slider track.
- Borders are `1px` `--line` on structural edges, `1px` `--line-strong` on chips and foot buttons, and `1.5px` on the input shell. No 2px structural borders.
- [SHOULD] Shadows are only for floating surfaces: zoom controls, toast, tool hint, modal, and the onboarding surface. Tool buttons may use one accent shadow when active. Rows, inspector bands, and the canvas never use shadows. (Decision; source: current implementation overuses no row shadows, but the rule keeps it that way.)
- Inspector bands are separated by `1px` hairlines. Do not stack a card inside a band.

### Canvas data display

- The default view uses `clamp(canvasWidth / 16, 32, 64)` pixels per world unit. Desktop and tablet show roughly 16 world units across; very narrow phones keep a 32 px/unit floor for legible objects. Reset returns to this scale, and the zoom readout is relative to it.
- Series curves use a `2px` stroke with round joins. Selected or hovered objects add a `+7px` translucent stroke at `16%` alpha, never a dashed outline.
- Points use a `5px` radius (`5.8px` when selected), fill with the series color, and a `2px` white ring. Labels sit up-right with a subtle white halo and use the series text color.
- Grid: one major line per `niceStep(90 / scale)` world unit; five minor subdivisions are drawn only when they are at least `11px` apart. Minor lines never exceed the major-line contrast.
- Axis lines are `1.4px` `PLOT.axis`; tick labels are `11px` sans `PLOT.tick`. Labels use the math face with a `3.4px` halo stroke.
- Object labels use the object name only and the series text color. Full definitions live in the inspector. Do not print equations on the canvas.
- Undefined geometry is hidden from the canvas, not drawn as a placeholder. Its inspector row shows `未定义` in `--danger`.
- A hidden object is absent from the canvas and dimmed in the inspector (`opacity: 0.42` on the row body). Its eye button switches to an eye-off icon.

### Controls and states

- Tools: `40px` square, `11px` radius, monochrome icon. Hover uses `#f1f5fa`; active uses `--accent` with white icon and a soft accent shadow. The active state is the only filled tool state.
- Top-bar icon buttons: `34px` square, `9px` radius, transparent, `#52627a` icon. Hover background `#f0f4fa`. Disabled opacity `0.3`.
- Input shell: `41px` high, `12px` radius, `1.5px` `--line-strong`, soft background. Focus border is `--accent` with a `4px` `--focus-ring`; the input itself has no separate outline.
- Submit button: `30px` square, `9px` radius, accent background, white arrow. Hover uses `--accent-strong`.
- Chips: `32px` high, `10px` radius, white surface, `--line-strong` border, serif formula at `13px`. Hover raises by `1px` at most and changes text to accent; focus uses the global ring.
- Algebra row: `10px` radius, transparent surface, hover `#f7f9fd`, selected `--accent-soft`. No visible type label; the definition and the colored name carry identity. Use a visually hidden type for assistive technology.
- Row value: one line at `12px`; use `--muted`; `未定义` is `--danger`.
- Slider: `4px` track, `14px` accent thumb with a white `2px` ring. The value to the right is `12px`, weight `700`, accent, tabular.
- Eye and delete controls: `23px` square, `6px` radius. Idle icon `--muted-3`. Delete is revealed on row hover **and** on keyboard focus; under `@media (hover: none)` it is always visible. Never make a destructive control reachable only through hover.
- Status strip: one translucent surface with a hairline and a `1px` internal divider. Items are `11px` mono. The coordinate readout formats as `x = … · y = …`; the zoom percentage is a separate item. If the coordinate readout is empty, hide its item and the divider.
- Toast: `12px`, white, hairline, `3px` left border in `--danger`/`--success`/`--accent`; maximum width `min(520px, calc(100% - 40px))`; auto-hide after `3.2s`.
- Tool hint: dark `rgba(15, 23, 42, 0.92)` pill, `12px` white text, a `6px` blue dot, and a `10px` Esc badge. It disappears for the move tool and when no tool is pending.
- Help examples: a transparent row button, `8px` radius, serif formula in accent on `#f3f7fe`, description at `11px` `--muted-2`. Focus ring is mandatory.
- [MUST] Every focusable element shows a visible focus indicator. Use a `2px` solid `--accent` outline at `2px` offset for buttons and links; use the accent shell border plus ring for the command input; use the same outline at `6px` offset for the slider.
- [MUST] Hover is never the only affordance for an action. All hover-revealed actions also appear on focus and on non-hover devices.
- Disabled controls use `opacity: 0.3`, retain their accessible name, and show no hover surface.
- Error state: the input shakes once for `360ms`; the toast states the parse/runtime correction. Do not mark valid objects as errors.
- Empty state: no objects → onboarding surface; no algebra rows → a short text block. Never fabricate loading skeletons or charts.
- Loading state: none exists in this product. Do not add a spinner or progress bar for local computation.

### Motion

- Hover/focus transitions: `120–160ms ease`.
- Selection and row state: `120ms ease`.
- Floating surfaces: onboarding opacity `280ms`; modal opacity `200ms` with an `8px` rise; drawer transform `240ms ease`.
- No bouncing, springy, or looping motion. No graph-value animation. Respect `prefers-reduced-motion: reduce` by reducing all animation and transition durations to near zero.

## 5. Available Primitives

Pages use only the following public names. Do not guess unlisted names. Page-specific styles, if ever added, use the `geo-*` namespace. Page-specific styles may compose published primitives but must not change their layout, typography, borders, or surfaces.

### Tokens (style entry point: `styles.css` `:root`)

| Role | Implementation name or value | Source or path | Usage condition | Status |
|---|---|---|---|---|
| Page surface | `--bg: #edf2f9` | `styles.css` | App background | Implemented |
| Canvas surface | `--board: #fbfcff` | `styles.css`, `PLOT.background` | Plotting region | Implemented |
| Panel surface | `--panel: #ffffff` | `styles.css` | Top bar, rail, inspector, modal | Implemented |
| Soft surface | `--panel-soft: #f6f9fd` | `styles.css` | Input shell, empty algebra | Implemented |
| Footer surface | `--panel-footer: #fcfdff` | `styles.css` | Inspector footer | Implemented |
| Primary text | `--ink: #0f172a` | `styles.css` | Headings, primary copy | Implemented |
| Soft ink | `--ink-soft: #334155` | `styles.css` | Math row title | Implemented |
| Math ink | `--ink-math: #40506a` | `styles.css` | Definitions | Implemented |
| Body secondary | `--muted: #52627a` | `styles.css` | Body secondary copy | Implemented |
| Metadata | `--muted-2: #64748b` | `styles.css` | Values, help copy, status | Implemented |
| Idle icon | `--muted-3: #7b8ba3` | `styles.css` | Idle eye/delete icons (non-text, 3:1) | Implemented |
| Disabled | `--disabled: #9aa8bb` | `styles.css` | Disabled controls only | Implemented |
| Hairline | `--line: #e5ebf3` | `styles.css` | Structural borders | Implemented |
| Strong hairline | `--line-strong: #d7e0ec` | `styles.css` | Inputs, chips, small buttons | Implemented |
| Soft hairline | `--line-soft: #edf1f7` | `styles.css` | Internal separators | Implemented |
| Accent | `--accent: #2563eb` | `styles.css` | Primary/active/focus | Implemented |
| Accent strong | `--accent-strong: #1d4ed8` | `styles.css` | Hover of primary action | Implemented |
| Accent soft | `--accent-soft: #eaf1ff` | `styles.css` | Selected row, quiet accent surface | Implemented |
| Focus outline | `--focus: #2563eb` | `styles.css` | All focus-visible outlines | Implemented |
| Focus ring | `--focus-ring: rgba(37, 99, 235, 0.08)` | `styles.css` | Input shell halo | Implemented |
| Danger | `--danger: #b91c1c` | `styles.css` | Error text, delete hover | Implemented |
| Success | `--success: #059669` | `styles.css` | Success toast | Implemented |
| UI type scale | `--fs-xs: 11px`, `--fs-sm: 12px`, `--fs-ui: 13px`, `--fs-math: 13.5px`, `--fs-brand: 15px`, `--fs-dialog: 21px`, `--fs-display: 22px`, `--fs-kicker: 10px` | `styles.css` | Roles in §4 | Implemented |
| Layout | `--topbar-h: 56px`, `--toolbar-w: 56px`, `--inspector-w: 352px` | `styles.css` | Workbench shell | Implemented |
| Radii | `--radius-xs: 6px`, `--radius-sm: 8px`, `--radius-md: 10px`, `--radius-lg: 12px`, `--radius-xl: 22px` | `styles.css` | Components | Implemented |
| Popover shadow | `--shadow: 0 12px 32px rgba(15, 23, 42, 0.09)` | `styles.css` | Zoom, toast, tool hint | Implemented |
| Floating shadow | `--shadow-float: 0 30px 70px rgba(15, 23, 42, 0.11), 0 2px 8px rgba(15, 23, 42, 0.03)` | `styles.css` | Onboarding surface | Implemented |
| Modal shadow | `--shadow-modal: 0 35px 90px rgba(15, 23, 42, 0.28)` | `styles.css` | Help dialog | Implemented |
| Series palette | `SERIES_PALETTE` (10 values, §4) | `js/app.js` | Canvas strokes, point fills, select glows | Implemented |
| Series text palette | `SERIES_TEXT_PALETTE` (10 mapped values, §4) | `js/app.js` | Inspector object names, canvas labels | Implemented |
| Plot tokens | `PLOT`: `background #fbfcff`, `minorGrid #f1f5fa`, `majorGrid #e4eaf3`, `axis #93a4bb`, `tick #64748b`, `label #64748b`, `labelHalo rgba(251, 252, 255, 0.94)`, `pointStroke #ffffff` | `js/app.js` | Canvas rendering | Implemented |

### Components

- `.topbar` + `.brand` + `.top-actions` + `.icon-btn`.
- `.toolbar` + `.tool` + `.tool-sep`.
- `.canvas-wrap` + `#board` + `.empty-state` + `.empty-card` + `.chip` + `.empty-tip`.
- `.zoom-controls`; `.statusbar` + `.status-item` + `.status-divider`.
- `.tool-hint`; `.toast`.
- `.sidebar` + `.sidebar-head` + `.input-shell` + `#cmdInput` + `#cmdSubmit` + `.input-help` + `.mini-link`.
- `.algebra-head` + `#objCount` + `.algebra` + `.obj-row` + `.obj-title` + `.obj-value` + `.row-eye` + `.row-del` + `.slider` + `.slider-val`.
- `.sidebar-foot` + `.foot-btn` + `.foot-hint`.
- `.modal` + `.modal-panel` + `.modal-head` + `.modal-close` + `.help-grid` + `.help-section` + `.example` + `.shortcut` + `kbd` + `.modal-note`.
- `.sr-only` for type context and other non-visual labels.

### Canvas methods

- `drawGrid`, `drawExplicit`, `drawImplicit`, `drawPoint`, `drawLineObject`, `drawCircleObject`, `drawPolygonObject`, `drawLabel`, `drawPreview`, `drawDragTooltip` in `js/app.js`.
- A new graph treatment must reuse `PLOT`, `SERIES_PALETTE`, and `drawLabel`; do not hardcode new canvas colors.

## 6. Copy and Number Formats

- Chinese UI. Button labels are 2–4 Chinese characters. Icon-only buttons require an `aria-label` and a title/tooltip.
- Error copy: state the failed input, then the correction or supported form. No exclamation marks. Example: "未定义的变量：a" and "请选择两个不同的点".
- Empty copy: "还没有对象" plus one concrete next step, not a feature list.
- Number formatting:
  - Display values use at most 3 decimals in definitions and 2 decimals in quick readouts; strip trailing zeros.
  - Use the Unicode minus `−` in displayed equations and text, while accepting ASCII `-` in input.
  - Coordinates use `(x, y)` with a comma and one space.
  - Measured values use label + value: `长度 = 5.099`, `半径 = 3`, `面积 = 3.5`. Do not append units inside the number.
  - Use tabular numerals for coordinates, values, and status readouts.
  - Do not add thousands separators inside mathematical expressions.
- Dates, times, data sources, and uncertainty are not part of this interface. Do not invent them.
- English eyebrows are permitted only in the onboarding overlay and help dialog. All actionable copy is Chinese.

## 7. Anti-Patterns

Start from the neutral generator habits and keep the adaptations below.

- [SHOULD] Do not use a centered hero with a card grid as the default page structure. The single onboarding surface is a transient empty state; it is the only centered composition and it is not a page template.
- [SHOULD] Do not put cards inside cards. Help uses sections and hairlines; the inspector uses bands, not cards.
- [SHOULD] Do not use decorative icon tiles, colored icon backgrounds, or illustration blobs. The logo gradient is the only brand ornament.
- [SHOULD] Do not introduce font sizes, weights, or colors outside the roles and component values in §4–§5. (Decision; source: the previous UI used 9.5–10.5px metadata and several near-duplicate grays.)
- [MUST] Do not set primary, interactive, or informational text below `11px` or below `4.5:1` contrast. (Accessibility requirement.)
- [SHOULD] Do not use pills for ordinary metadata. No object-type pills, no object-count pill, no per-row tags. Reserve pill geometry for the tool hint and the slider track.
- [SHOULD] Do not repeat information already carried by the definition, such as a visible "点/函数/直线" tag next to a formula that already identifies itself. Keep it visually hidden for assistive technology.
- [SHOULD] Do not make delete or any destructive action hover-only. It must also appear on focus and on `hover: none` devices.
- [SHOULD] Do not use shadows on inline rows, inspector bands, or the canvas. Shadows belong to floating surfaces.
- [SHOULD] Do not use series colors in chrome or status feedback. Use a series color as text only when it comes from `SERIES_TEXT_PALETTE`. Do not use accent color for data series by default.
- [SHOULD] Do not use more than one accent hue for state. Selected, focused, and primary all use `--accent` with different surfaces.
- [SHOULD] Do not use all-caps or letter-spaced metadata. Uppercase is limited to the onboarding/help eyebrow.
- [SHOULD] Do not animate graph values, coordinates, or slider results. Motion is only for overlays and interaction feedback.
- [SHOULD] Do not fabricate loading states, skeleton screens, charts, metrics, or testimonials. The product has no loading state and no marketing surface.
- [SHOULD] Do not use more than one prominent shadow or more than one primary button in the same viewport.
- [SHOULD] Do not use raw `outline: none` without an equivalent visible focus treatment.
- [SHOULD] Do not use dark panels, glass cards, or neon accents; the interface is a light workbench.

## 8. Implementation and Integration

- Style entry point: `styles.css`. Tokens live in `:root`; no CSS-in-JS and no external stylesheet.
- Canvas data tokens: `PLOT` and `SERIES_PALETTE` at the top of `js/app.js`. Canvas drawing functions read those objects; UI chrome reads CSS variables.
- Fonts: system stacks only. No web-font request, no font file, no external asset. `--sans` and `--math` are the only font families for UI and data. `--mono` is for the status readout.
- Theme: light only. Do not add a theme switch or a partially implemented dark mode. A dark theme requires a full palette and a separate review.
- Icons: inline SVG with `1.7–1.9` stroke width. Tool icons are monochrome; the active tool inverts to white on accent. No icon font and no external icon package.
- Motion: CSS transitions only. Honor `prefers-reduced-motion: reduce`.
- Page-specific extension: use the `geo-*` prefix if a future page needs a scoped class. Do not override `.obj-row`, `.tool`, `.sidebar`, `.modal-panel`, or other public primitives from a page-specific namespace.
- Available states are implemented in `js/app.js` and `styles.css`: empty, selected, hover, hidden, undefined, focused, error toast, success toast, pending tool, narrow drawer. Loading is intentionally absent.
- Accessibility entry points: `aria-label` on icon buttons, `aria-pressed` on the active tool, `aria-live` on the toast, a labelled `role="dialog"` plus focus containment on the help panel, labels on inputs and sliders, visible focus rings, and `sr-only` type context. The canvas is pointer-driven; algebraic actions remain available from the inspector.

## Glossary

| Concept | Name used in this file | Implementation |
|---|---|---|
| Full-canvas editor layout | Workbench | `.topbar`, `.toolbar`, `.canvas-wrap`, `.sidebar` |
| Right-side property/list panel | Inspector | `.sidebar`, `.algebra`, `.obj-row` |
| Single first-run surface | Onboarding overlay | `.empty-state`, `.empty-card`, `.chip` |
| Floating help surface | Help dialog | `.modal`, `.modal-panel` |
| Formula/definition row | Math row | `.obj-row`, `.obj-title`, `.obj-name`, `.obj-def` |
| Numeric readout row | Value row | `.obj-value`, `.slider-val` |
| Canvas command feedback | Tool hint | `.tool-hint` |
| Bottom-left view readout | Status strip | `.statusbar`, `.status-item`, `.status-divider` |
| Object identity color | Series color | `SERIES_PALETTE` |
| Text-safe identity color | Series text color | `SERIES_TEXT_PALETTE` |
| Canvas appearance tokens | Plot tokens | `PLOT` in `js/app.js` |
| Visually hidden assistive text | Screen-reader context | `.sr-only` |
