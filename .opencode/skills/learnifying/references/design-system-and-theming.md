# Design System and Mandatory Light/Dark Themes

This is a mandatory product requirement for every Learnifying application. Read it before choosing the visual identity, building shared components, or styling lesson content.

## 1. Product requirement

Every generated app must ship with all of the following:

- A complete **Light theme** and **Dark theme**. A dark-only or light-only app is not an acceptable default deliverable.
- A visible, discoverable theme control available from the main app shell on all major routes. A settings-only control is insufficient if the settings page is difficult to find; provide a persistent header/sidebar control or an equally obvious global entry point.
- A first-launch default of **System**: follow the operating system/browser `prefers-color-scheme` preference.
- A user override with at least `System`, `Light`, and `Dark` choices. A quick toggle between Light and Dark may supplement, but should not replace, the explicit System option.
- Immediate theme switching without page reload, route reset, loss of unsaved exercise input, or loss of learner progress.
- Persistence of the explicit theme choice across reloads and later launches whenever the browser permits storage. If persistence is blocked, the app must still run and clearly fall back to the current-session selection.
- All major interface components and instructional visualizations must support both themes; no dark-mode toggle that only changes the page background while leaving charts, code editors, canvases, or embedded controls unreadable.

The theme control and its labels must be in Russian in the learner-facing interface. Suggested labels: `Тема оформления`, `Как в системе`, `Светлая`, `Тёмная`.

## 2. Palette selection hierarchy

Choose the course-specific palette in this priority order:

1. **Legibility and accessibility** — text, controls, focus, chart marks, and state indicators must remain perceivable.
2. **Low visual noise and a clear hierarchy** — use a restrained background/surface system and reserve stronger accents for navigation, interaction, and meaningful instructional emphasis.
3. **Consistent semantics** — the same semantic role (success, warning, error, information, selected, disabled) must retain its meaning throughout the app and across themes.
4. **Subject identity** — use colors that evoke the discipline when appropriate, without compromising the first three priorities.

Do not claim that a particular hue intrinsically improves memory, intelligence, focus, or learning. There is no universal learning-enhancing palette. Design for readable content, low distraction, meaningful visual grouping, and stable semantic cues; treat subject-inspired color as an aesthetic layer rather than a cognitive shortcut.

Create related Light and Dark palettes from the same visual identity. They should feel like two deliberately designed expressions of one system, not a literal inversion of every color. Avoid pure white/black as large full-screen surfaces where softer neutrals improve comfort, but do not sacrifice contrast to achieve a fashionable look.

## 3. Design tokens — one source of truth

Implement themes using semantic design tokens, preferably CSS custom properties on a root theme attribute such as `data-theme="light"` / `data-theme="dark"`. Components must consume semantic tokens rather than hard-coded palette values.

At minimum define tokens for:

- page/background and elevated surfaces (surface 1/2/3);
- primary, secondary, muted, and inverse text;
- links and interactive accent states (default, hover, active, selected, disabled);
- borders, separators, subtle outlines, and focus indicators;
- success, warning, error, and informational feedback, including foreground and background variants;
- selection, code blocks, inline code, syntax highlighting, tables, callouts, formula blocks, tooltips, popovers, dialogs, and form controls;
- chart/diagram series, axes, gridlines, annotations, legends, and selection/highlight states;
- visualization canvas/background and any overlay/control surfaces.

A useful naming pattern is role-based (`--color-bg`, `--color-surface`, `--color-text`, `--color-muted`, `--color-border`, `--color-accent`, `--color-success`, etc.), not hue-based (`--purple-500`) in application components. Palette primitives may be hue-based inside the theme definition, but UI code should use semantic tokens.

Set the document's `color-scheme` consistently with the active theme so native form controls and browser-rendered widgets can adapt. Keep the theme attribute and CSS token source synchronized; do not allow separate components to maintain competing theme state.

## 4. Theme state and persistence behaviour

Use one central theme controller/store in the application shell:

1. On first launch, resolve `System` using `matchMedia('(prefers-color-scheme: dark)')`.
2. If the learner has explicitly chosen Light or Dark, that choice takes precedence over system changes.
3. If the learner chooses System, subscribe to system preference changes and update the app while the app is open.
4. Apply the resolved theme to the document root before or as early as possible during first paint to avoid a visible flash of the wrong theme. In a single-file build, the bootstrap code must be included in the final HTML and tested from `file://`.
5. Persist the **preference** (`system`, `light`, or `dark`), not only the resolved appearance. Use the app's storage abstraction where practical; catch storage errors and continue without crashing.
6. Switching themes must not remount or reset the course, lose typed but unsubmitted answers, restart a visualization, change progress, or navigate away from the current route.
7. Keep the setting alongside other app preferences and include it in app-settings export/import when that feature exists. Do not expose sensitive learner data.

Do not assume `localStorage`, IndexedDB, or any particular persistence API is guaranteed under every browser's `file://` implementation. Probe the selected storage path, catch exceptions, and provide a graceful in-session fallback. The theme switcher must remain functional even when persistence is unavailable. Report the exact persistence behaviour observed in the target browser; do not claim it is durable when it is not.

## 5. Accessible theme control

- Use a real button, radio group, or select with a programmatic accessible name and keyboard operation.
- Show the currently selected preference and distinguish the explicit choice from the resolved theme (for example, `Как в системе · сейчас тёмная`).
- Do not communicate the selected state through color or icon alone.
- Keep visible focus indicators in both themes.
- Avoid a tiny icon-only control unless it has a reliable accessible name, tooltip, and adequate hit target; visible text is preferred where space allows.
- Switching must not unexpectedly move keyboard focus.

## 6. Contrast, color, and visual hierarchy

Target WCAG 2.2 AA contrast as a minimum:

- Normal text: at least 4.5:1.
- Large text: at least 3:1.
- Meaningful non-text UI components and graphical objects: at least 3:1 against adjacent colors where the criterion applies.

Check contrast independently for both themes and for all meaningful states: default, hover, active, focus, disabled, selected, success, warning, and error. Do not lower contrast to preserve a brand color; adjust the color, surface, weight, or size instead.

Never rely on color alone to convey correctness, error, progress, chart categories, or state. Pair color with text, iconography, shape, pattern, border, or another redundant cue. Keep semantic colors stable across themes even if their exact hex values differ.

Do not fill every card with a saturated accent color. The course topic can inform a small accent palette while neutral surfaces preserve the reading environment. Use typography, spacing, headings, and layout—not color alone—to create hierarchy.

## 7. Charts, code editors, and instructional visualizations

Every visual subsystem must be theme-aware:

- Charts: adapt plot background, axes, ticks, gridlines, labels, legends, series colors, annotations, and tooltip surfaces. Preserve the meaning/order of series across themes.
- SVG/HTML diagrams: use CSS variables/currentColor where possible; verify labels, arrows, borders, and selected nodes in both themes.
- Canvas/WebGL/WebGPU/ shader output: explicitly pass theme tokens or visualization theme settings to the renderer. A CSS background change does not recolor pixels drawn into a canvas. Ensure controls and labels outside the canvas also adapt.
- Code editors and syntax highlighters: select a compatible light/dark theme and keep syntax colors readable; do not theme only the editor chrome.
- Embedded third-party widgets: investigate their theme API and exact integration behaviour before adoption. If they cannot adapt reliably, wrap them with an intentional high-contrast frame or choose a different renderer. Do not ship a widget that is unreadable in one mode.
- Mathematical notation, formula blocks, code samples, exercise feedback, and hint panels must remain legible in both themes.

The visualization-tool-selection process must include theming support in the comparison for any third-party component. For complex renderers, verify theme changes at runtime without destroying learner state, and record limitations in `docs/VISUAL_IMPLEMENTATION_DECISIONS.md`.

## 8. Motion and theme changes

- Theme changes should be immediate. A short, subtle transition on colors is acceptable only when it does not delay interaction or create visual noise.
- Respect `prefers-reduced-motion`; disable non-essential transitions and animations where requested.
- Do not animate every component individually during a theme change.
- Preserve the state and timing of educational animations and interactive experiments when the theme changes; theme changes must not count as learner actions or reset an experiment.

## 9. Print and fallback behaviour

- Provide a readable print stylesheet, normally using a light page background and dark text regardless of the active on-screen theme.
- If a browser does not support `prefers-color-scheme`, default to Light and keep the manual switcher functional.
- If stored preferences are malformed or unavailable, fall back safely to System and never block app startup.
- If a third-party visualization cannot be themed, prefer an accessible static fallback over an unreadable interactive component.

## 10. Acceptance tests

The implementation is not complete until all applicable tests pass on the exact final `index.html` opened directly from disk (`file://`) in the declared target browser(s):

1. Fresh profile, OS in Light: app starts Light and preference is System.
2. Fresh profile, OS in Dark: app starts Dark and preference is System.
3. Explicitly select Light: appearance updates immediately without reload or route/state loss.
4. Explicitly select Dark: appearance updates immediately without reload or route/state loss.
5. Explicitly select System: app follows the OS preference and responds to a system preference change.
6. Reload/reopen: explicit selection persists where storage is supported; System remains the saved preference when selected.
7. Block/deny storage: app still starts, theme switching still works for the session, and no unhandled exception occurs.
8. Visit every major route and inspect navigation, theory, practice, feedback, settings, dialogs, charts, code editors, and visualizations in both themes.
9. Check contrast for text, focus indicators, controls, chart marks, and state feedback in both themes.
10. Check keyboard and screen-reader operation of the theme control.
11. Check that switching theme while an exercise contains unsaved input or an interactive model is running does not reset it.
12. Open the final single-file deliverable from disk after closing the dev server; do not accept an HTTP preview as proof of `file://` compatibility.

Document the browsers, OS theme states, routes, and storage conditions actually tested in `docs/QA_REPORT.md`. Mark any untested item explicitly.
