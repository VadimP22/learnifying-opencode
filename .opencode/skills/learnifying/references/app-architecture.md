# React Learning-App Architecture

## 1. Technical baseline

- React is the UI framework.
- `index.html` is the HTML entry point at the project root.
- Prefer Vite + React for a lightweight client-side app when the environment supports Node/package installation. Check current official setup guidance and choose mutually compatible, supported versions.
- The learner-facing release target is a **single self-contained `index.html`** that can be opened directly from the filesystem (`file://`) without running a dev server or local HTTP server. Use a maintained single-file bundling strategy (for example, a currently verified Vite single-file plugin or equivalent); verify its current API, compatibility, and license before use.
- Inline bundled JavaScript, CSS, fonts/icons where licensing permits, and required static assets. Disable runtime code-splitting and avoid asset URLs that point to sibling folders or external CDNs. Do not require a service worker, server-side route fallback, or remote script for the core course experience.
- Use hash-based client-side navigation (for example `index.html#/lesson/.../theory` and `index.html#/lesson/.../practice`) so routes work when opened from `file://`.
- Test the final built artifact from disk in an actual supported browser. A Vite dev-server preview or a built app served over HTTP is not proof that the `file://` deliverable works.
- Some APIs/libraries (Workers, WASM loaders, dynamic imports, storage implementations, remote APIs, WebGL/WebGPU) may have origin/security restrictions under `file://`. Verify each chosen dependency in the target environment. If a dependency cannot work locally from a single file, find a compatible approach or report the limitation and require a server only for that clearly identified optional feature.
- Pin dependency versions in the lockfile. Avoid unpinned CDN scripts for production course content.
- Do not add a backend unless the learner's requirements genuinely need accounts, cross-device sync, shared classrooms, server execution, or protected data.
- The app should still function for reading lessons if an optional advanced runtime is unavailable; explain the limitation.

## 2. Suggested project structure

Adapt to existing workspace conventions, but keep a clear separation:

```text
project/
  index.html
  package.json
  package-lock.json (or the package manager's lockfile)
  README.md
  docs/
    PROJECT_BRIEF.md
    COURSE_MAP.md
    SOURCE_REGISTER.md
    CLAIM_LEDGER.md
    QA_REPORT.md
  src/
    main.jsx
    App.jsx
    components/
      CourseSidebar.jsx
      ScheduleView.jsx
      LessonTheoryPage.jsx
      LessonPracticePage.jsx
      TheoryBlock.jsx
      VisualExplanation.jsx
      WorkedExample.jsx
      ExerciseHost.jsx
      ReviewQueue.jsx
      ReviewSectionPage.jsx
      ProgressDashboard.jsx
    data/
      course.json
      units/
      lessons/
      exercises/
    assessment-adapters/
      index.js
      ...domain-specific adapters...
    lib/
      scheduler.js
      review-planner.js
      progress-store.js
      validation.js
    styles/
      global.css
      theme-tokens.css
    lib/
      theme-controller.js
```

Avoid creating hundreds of tiny files for a small course. Split by meaningful responsibility and keep lesson content data-driven.

## 3. Minimum user experience

The app should include:
- course overview and stated end goal;
- unit/lesson navigation and progress status;
- calendar or week-by-week plan showing what to study and when;
- a dedicated theory page/route and a dedicated practice page/route for each lesson; never append the assigned practice set below the theory text;
- purposeful visual explanations integrated into theory (diagrams, charts, simulations, animations, interactive models, or live outputs where appropriate);
- exercise feedback, hints, retries, and completion state;
- a review queue that brings back earlier topics when due;
- distinct, named review sections in the course roadmap between topic blocks, including a midpoint cumulative review when justified;
- short prerequisite-recall bridge pages before new topics that meaningfully depend on earlier concepts;
- spiral-deepening tasks that revisit foundations in new contexts and at increasing levels of integration and transfer;
- progress dashboard showing completed, in-progress, due-for-review, and mastered concepts;
- settings for available study days/time or schedule adjustment where practical;
- persistence across reloads;
- visible “sources / version notes” for course content;
- complete Light and Dark themes, a visible global theme switcher, system preference detection on first launch, and persistence of explicit user preference.

Do not show a progress percentage that counts merely opened lessons as mastered. Separate started, completed, and mastered.

## 4. Data and state

Separate content from UI. Validate loaded course data against a schema or runtime checks. Give units, lessons, outcomes, concepts, exercises, and source records stable IDs.

Persist at least:
- completed/attempted lesson state;
- exercise attempts and results;
- mastery status per outcome/concept;
- review due dates, intervals, last result, and concept-level mastery state;
- completed standalone review-section IDs and prerequisite-bridge state;
- task/variant IDs already attempted so the same review item is not accidentally assigned again;
- learner schedule preferences;
- app/course schema version.

Use a small storage abstraction. `localStorage` is sufficient for modest progress data; consider IndexedDB for larger artifacts. Include versioning/migration or a safe reset path. Provide data export/import when feasible so local progress is not trapped in one browser. Do not store passwords, API keys, or unnecessary personal information. Store the theme preference (`system`, `light`, or `dark`) in the same settings abstraction where possible; catch `file://` storage failures and preserve in-session switching.

## 5. Scheduling and adaptation

Read `distributed-and-spiral-review.md`. Keep scheduling logic in pure modules, separate from React components. `review-planner.js` should combine the authored review architecture, prerequisite graph, learner availability, concept-level mastery, past attempts, and due dates. It must surface standalone review sections and prerequisite bridges as distinct roadmap entries; it must not merely append old exercises to the current lesson. It should accept course structure, learner availability, start date, progress, and review state, then return a deterministic schedule. Make it possible to recompute the plan when the learner changes weekly availability without losing completed work.

Keep due reviews visible. Honour planned interleaved and midpoint review sections. Before a dependent new topic, surface its prerequisite-recall bridge. Avoid placing a large review burden on the same day as a demanding new lesson. Adapt review priorities without allowing an unbounded overdue queue. Provide a catch-up mechanism and never silently discard overdue items.

## 6. Review-section routes and theory/practice separation

- Use distinct routes/views and clear navigation for lesson theory and lesson practice. Preserve the learner's place when moving between them.
- Give every standalone review section its own route/view (for example `#/review/review-after-unit-02`); do not append it to the bottom of a lesson.
- Give prerequisite-recall bridges their own route/view and position them immediately before the dependent lesson theory.
- Distinguish interleaved review, midpoint cumulative review, prerequisite recall, spiral deepening, ordinary lesson practice, and final assessment in the roadmap.
- Theory pages may include annotated static visuals and exploratory interactive demonstrations that reveal how a concept works. These are instructional aids, not graded exercise tasks.
- Practice pages contain assigned problems, code editors, submissions, automated checks, scoring, hints, remediation, and practice feedback.
- Review pages prioritise retrieval before feedback. Every revisit uses a fresh task; never reuse the same prompt/data/code/options/solution path 1:1. Track exercise/variant IDs and document meaningful differences from earlier tasks.
- Visuals must have a stated teaching purpose and be connected to the prose by labels, captions, callouts, or guided prompts. Avoid decorative charts, irrelevant stock images, and visual clutter.
- Prefer interactive visualizations when manipulation or observation materially improves understanding; otherwise use a clear static diagram/graph. Always provide a usable non-interactive or reduced-motion fallback where possible.
- For charts and diagrams, label axes, units, legends, states, and important parts. Do not rely on colour alone to communicate meaning.
- For interactive models, make controls discoverable and keyboard-operable, provide sensible defaults/reset, show the relevant output/state, and explain what changes when a control is adjusted.

## 7. Design system and Light/Dark theme requirement

Read and follow `design-system-and-theming.md`. Light and Dark themes are mandatory, not optional polish. Use one semantic token system, make all routes and instructional renderers theme-aware, expose System/Light/Dark choices in a persistent visible control, and persist explicit choices where the browser permits. The initial preference is System. Theme changes must not reset route, learner progress, unsaved answers, or running demonstrations. Test the exact bundled `index.html` under `file://` with storage available and blocked.

## 8. Responsive design and accessibility

- Mobile-first responsive layout; no horizontal scrolling for normal content.
- Semantic headings, buttons, form labels, landmarks, and lists.
- Full keyboard navigation, visible focus indicators, sufficient contrast, and screen-reader labels.
- Do not communicate correctness using colour alone.
- Use `aria-live` carefully for assessment feedback.
- Support reduced motion; avoid unnecessary animations.
- Provide readable line length, font sizing, and code blocks that can scroll horizontally without breaking the page.
- Use Russian copy consistently; ensure fonts render Cyrillic correctly.

## 9. Dependency and visualization decision records

Before implementing any non-trivial visual, read `visualization-tool-selection.md` and decide whether native/custom code or an existing library is the smallest reliable option. Tier 0 visuals normally use native HTML/CSS/SVG; Tier 2 visuals require current tool research and a packaged proof-of-feasibility spike. Use the dedicated visualization specialist for genuinely complex or uncertain decisions, not for simple diagrams.

Before adding any library, write a short entry in `docs/DECISIONS.md` or `docs/VISUAL_IMPLEMENTATION_DECISIONS.md`:
- visual/problem and teaching outcome it supports (when relevant);
- problem it solves;
- alternatives considered (including a native/custom solution);
- official source checked and date;
- current version selected;
- license;
- maintenance/security/compatibility considerations;
- bundle/runtime cost (measured where feasible);
- offline and `file://` single-file compatibility evidence;
- fallback if it fails.

Prefer fewer dependencies. Do not choose a library solely because a search result recommends it. Check its official docs and package metadata.

## 10. Security rules

- Never put API tokens, private keys, or privileged credentials in browser code.
- Do not use `eval` or `new Function` to execute learner submissions in the app's trusted page.
- For learner code, use a sandboxed iframe with a restrictive `sandbox` attribute, a Worker, or a dedicated isolated runtime, with timeouts, resource limits, and a narrow message protocol. Do not grant same-origin access unless strictly required and reviewed.
- Treat exercise data, imported course files, and learner input as untrusted. Escape rendered text; validate structured data.
- Avoid `dangerouslySetInnerHTML` unless content is trusted, sanitised, and genuinely needs HTML.
- Check licenses and security advisories for dependencies. Avoid loading arbitrary remote scripts at runtime.
- If an online judge or external API is required, disclose the network/data flow and obtain user approval before sending learner code or data.

## 11. Reliability and failure states

- Handle missing WebGL/WebGPU, blocked storage, offline mode, dependency load failure, compilation errors, and malformed course data gracefully.
- Give learner-facing Russian error messages with actionable recovery steps.
- Do not mark an exercise passed when a runtime failed to run.
- Make progress persistence observable (e.g. “Сохранено локально”) without overstating cloud sync.


## 12. Executive-function-friendly interaction layer

Use `executive-function-friendly-design.md` as the product standard. In addition to the core app views, consider implementing:

- A home screen with one primary `Продолжить` / `Начать следующий шаг` action.
- A visible `Следующий шаг` panel with a short description, estimated time, and definition of done.
- Session presets such as a brief entry session and a normal study session; keep the number of choices small and the default obvious.
- Exact resume state: last open section, unfinished exercise, current hint level, and next actionable step.
- A calm re-entry view after absence: what was last studied, what remains important, and one recommended next action.
- An editable schedule with catch-up buffers and a review queue that prioritises rather than overwhelms.
- Optional focus timer, reminder, reduced-motion, sound, and visual-density settings. Timers must never interrupt or auto-submit an exercise.
- Short checklists for multi-step projects and visible progress by outcome/mastery, not only by time spent or screens opened.

Do not implement every feature automatically. Choose only features that directly reduce friction for this learner and subject, and validate that they do not interrupt sustained reasoning or hide important course structure.
