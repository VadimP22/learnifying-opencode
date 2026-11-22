# React Learning-App Architecture

## 1. Technical baseline

- React is the UI framework.
- `index.html` is the HTML entry point at the project root.
- Prefer Vite + React for a lightweight client-side app when the environment supports Node/package installation. Check current official setup guidance and choose mutually compatible, supported versions.
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
      LessonView.jsx
      TheoryBlock.jsx
      WorkedExample.jsx
      ExerciseHost.jsx
      ReviewQueue.jsx
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
      progress-store.js
      validation.js
    styles/
      global.css
```

Avoid creating hundreds of tiny files for a small course. Split by meaningful responsibility and keep lesson content data-driven.

## 3. Minimum user experience

The app should include:
- course overview and stated end goal;
- unit/lesson navigation and progress status;
- calendar or week-by-week plan showing what to study and when;
- lesson screen with theory, example, then exercises;
- exercise feedback, hints, retries, and completion state;
- a review queue that brings back earlier topics when due;
- progress dashboard showing completed, in-progress, due-for-review, and mastered concepts;
- settings for available study days/time or schedule adjustment where practical;
- persistence across reloads;
- visible “sources / version notes” for course content.

Do not show a progress percentage that counts merely opened lessons as mastered. Separate started, completed, and mastered.

## 4. Data and state

Separate content from UI. Validate loaded course data against a schema or runtime checks. Give units, lessons, outcomes, concepts, exercises, and source records stable IDs.

Persist at least:
- completed/attempted lesson state;
- exercise attempts and results;
- mastery status per outcome/concept;
- review due dates, intervals, and last result;
- learner schedule preferences;
- app/course schema version.

Use a small storage abstraction. `localStorage` is sufficient for modest progress data; consider IndexedDB for larger artifacts. Include versioning/migration or a safe reset path. Provide data export/import when feasible so local progress is not trapped in one browser. Do not store passwords, API keys, or unnecessary personal information.

## 5. Scheduling and adaptation

Keep scheduling logic in a pure module, separate from React components. It should accept course structure, learner availability, start date, progress, and review state, then return a deterministic schedule. Make it possible to recompute the plan when the learner changes weekly availability without losing completed work.

Keep due reviews visible. Avoid placing a large review burden on the same day as a demanding new lesson. Provide a catch-up mechanism and never silently discard overdue items.

## 6. Responsive design and accessibility

- Mobile-first responsive layout; no horizontal scrolling for normal content.
- Semantic headings, buttons, form labels, landmarks, and lists.
- Full keyboard navigation, visible focus indicators, sufficient contrast, and screen-reader labels.
- Do not communicate correctness using colour alone.
- Use `aria-live` carefully for assessment feedback.
- Support reduced motion; avoid unnecessary animations.
- Provide readable line length, font sizing, and code blocks that can scroll horizontally without breaking the page.
- Use Russian copy consistently; ensure fonts render Cyrillic correctly.

## 7. Dependency decision record

Before adding a library, write a short entry in `docs/DECISIONS.md` or `README.md`:
- problem it solves;
- alternatives considered;
- official source checked and date;
- current version selected;
- license;
- maintenance/security/compatibility considerations;
- bundle/runtime cost;
- fallback if it fails.

Prefer fewer dependencies. Do not choose a library solely because a search result recommends it. Check its official docs and package metadata.

## 8. Security rules

- Never put API tokens, private keys, or privileged credentials in browser code.
- Do not use `eval` or `new Function` to execute learner submissions in the app's trusted page.
- For learner code, use a sandboxed iframe with a restrictive `sandbox` attribute, a Worker, or a dedicated isolated runtime, with timeouts, resource limits, and a narrow message protocol. Do not grant same-origin access unless strictly required and reviewed.
- Treat exercise data, imported course files, and learner input as untrusted. Escape rendered text; validate structured data.
- Avoid `dangerouslySetInnerHTML` unless content is trusted, sanitised, and genuinely needs HTML.
- Check licenses and security advisories for dependencies. Avoid loading arbitrary remote scripts at runtime.
- If an online judge or external API is required, disclose the network/data flow and obtain user approval before sending learner code or data.

## 9. Reliability and failure states

- Handle missing WebGL/WebGPU, blocked storage, offline mode, dependency load failure, compilation errors, and malformed course data gracefully.
- Give learner-facing Russian error messages with actionable recovery steps.
- Do not mark an exercise passed when a runtime failed to run.
- Make progress persistence observable (e.g. “Сохранено локально”) without overstating cloud sync.


## 9. Executive-function-friendly interaction layer

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
