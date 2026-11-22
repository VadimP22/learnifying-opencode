# QA and Release Checklist

## 1. Pedagogy and content

- [ ] User goal and course scope are explicit.
- [ ] The calendar fits the chosen duration and available study time.
- [ ] Prerequisites appear before dependent lessons.
- [ ] Each learning outcome is taught and assessed.
- [ ] Every lesson has a dedicated theory page and a separate practice page; no assigned graded exercise sequence is appended below the theory.
- [ ] Theory includes purposeful visual explanations for key concepts where suitable, with a documented rationale when a visual adds no value.
- [ ] Visuals directly support the learning outcome, are accurate and clearly labelled, and are explained in the surrounding text.
- [ ] Interactive explanatory models work as intended, can be reset, are keyboard-operable, and have a static/stepwise fallback or an explicitly documented limitation.
- [ ] Each non-trivial visual has a documented native/custom-vs-library decision; complex choices have current primary-source research and a packaged `file://` proof-of-feasibility or a documented blocker.
- [ ] Early exercises are small and scaffolded; later tasks require increasing independence and integration.
- [ ] Previously taught concepts reappear through the approved standalone review architecture and adaptive due-retrieval mechanism.
- [ ] Repetition is not limited to old lesson exercises copied into a queue; review tasks are fresh and meaningfully varied.
- [ ] Review load is manageable and overdue items are not silently dropped.
- [ ] Feedback explains why an answer is wrong and how to recover.
- [ ] Final assessment matches the advertised learning outcomes.
- [ ] Learner-facing copy is Russian, with conventional technical terminology where appropriate.
- [ ] Both Light and Dark themes are fully designed; the palette prioritises legibility and low visual noise over decorative subject branding.

## 2. Fact-checking

- [ ] Material claims map to claim IDs.
- [ ] Important claims have direct, relevant evidence.
- [ ] Volatile claims include version/environment and a recent check date.
- [ ] Conflicts, missing evidence, and outdated material are marked.
- [ ] User-supplied material is mapped and not misrepresented as independently verified.
- [ ] Citations work and identify the real supporting source.
- [ ] No unsupported “100% accurate/current” claim appears.

## 3. Application functionality

- [ ] Root `index.html` is present and is the app entry point.
- [ ] The final production `index.html` is self-contained and opens from disk (`file://`) in a supported browser without a dev server or local HTTP server; test the exact deliverable, not only the dev build.
- [ ] Hash-based theory/practice navigation works when opened from `file://`.
- [ ] All required JS/CSS/assets are embedded; no required sibling asset folder, dynamic chunk, local server endpoint, or unpinned CDN dependency is needed for core learning flows.
- [ ] Fresh install/build succeeds, or the blocker is documented.
- [ ] Main navigation and all course routes/views work.
- [ ] Lessons display theory before examples and practice.
- [ ] Exercise input, submit, retry, hints, feedback, and completion work.
- [ ] An auto-check only reports pass/fail after a real checker executes.
- [ ] Review queue correctly schedules and surfaces due items.
- [ ] Standalone review sections appear as distinct roadmap entries and open on their own routes/pages.
- [ ] Prerequisite-recall bridges appear before dependent new-topic theory and correctly handle both successful recall and forgotten prerequisites.
- [ ] Spiral-deepening tasks revisit important concepts at a deeper/transfer level with fresh tasks.
- [ ] Progress persists after refresh and browser restart where expected.
- [ ] Export/import or recovery behaviour works if implemented.
- [ ] Schedule and progress remain coherent after changing availability.
- [ ] Runtime/library failure produces a useful fallback, not a false pass.
- [ ] No visual dependency was added without checking its exact API/version, licence, maintenance, security, browser support, accessibility, offline behaviour, and single-file packaging fit.

## 4. Security, privacy, accessibility

- [ ] Learner code is not run in the trusted app context.
- [ ] No secrets are shipped to the client.
- [ ] Imported content and learner input are validated/escaped.
- [ ] Any external data transfer is disclosed and approved where required.
- [ ] Keyboard-only navigation works for key flows.
- [ ] Focus, labels, semantic structure, contrast, and screen-reader feedback are reviewed.
- [ ] Mobile layout works at narrow widths.
- [ ] A visible, keyboard-operable theme control offers System, Light, and Dark; a fresh launch follows OS preference.
- [ ] Explicit theme choice persists across reload/reopen where supported; storage failure is handled without breaking the app.
- [ ] Theme switching is immediate and preserves route, progress, unsaved answers, and running visualizations.
- [ ] Every major page, chart, diagram, editor, canvas, and third-party widget is checked in both themes.
- [ ] Contrast meets WCAG 2.2 AA thresholds for text and applicable non-text UI/graphics in both themes; focus and status are not conveyed by color alone.

## 5. Minimum manual test journey

1. Open the app as a new learner.
2. Start and complete the diagnostic (if present).
3. Open the first lesson theory page; confirm it contains the intended explanations and visual aids, and does not contain the assigned graded practice set.
3a. Navigate to the separate practice page; confirm exercises, checking, hints, and feedback work there.
4. Submit a deliberately incorrect answer; confirm explanatory feedback and remediation.
5. Submit a correct answer; confirm the checker really executes and progress updates.
6. Reload the app; confirm progress persists.
7. Open a standalone interleaved review section from the course roadmap; complete a mixed set of fresh tasks.
8. Open a prerequisite-recall bridge immediately before a dependent new topic; test both successful recall and a forgotten-prerequisite remediation path.
9. Complete a spiral-deepening task and confirm that it uses a new context/representation/reasoning demand rather than an old prompt.
10. Trigger or simulate a due review; confirm a previously learned concept appears and the next due date changes after completion.
11. Open the midpoint cumulative review when present and inspect its earlier-concept coverage.
12. Navigate to a later, harder lesson and confirm scaffolding has been reduced as designed.
13. Test any domain-specific renderer/runtime, including unsupported-device fallback; compare observed behaviour to `docs/VISUAL_IMPLEMENTATION_DECISIONS.md`.
14. Close the dev server, open the final `index.html` directly from disk (`file://`), and test reload, theory/practice navigation, visuals, and local progress storage.
15. Test a fresh profile with system Light and Dark; verify System/Light/Dark selection, reload persistence, OS-change response in System mode, blocked-storage fallback, and theme switching while an exercise/visualization is active.
16. Inspect every major route and interactive/embedded visual in both themes; verify contrast, focus, keyboard operation, and print stylesheet.

## 6. Test reporting

In `docs/QA_REPORT.md`, distinguish:
- automated tests run and their results;
- build/lint/typecheck results;
- browser/manual tests actually performed;
- code reviewed but not executed;
- untested browsers/devices;
- known defects and severity;
- residual risks and next recommended checks.

Never claim browser verification if no browser was launched. Never claim a build passed if dependencies could not be installed. Report command output faithfully and fix failures where possible before handover.


## 7. Distributed, cumulative, and spiral review QA

- [ ] The roadmap visibly places standalone review sections between appropriate topic blocks; each has an ID, scope, time estimate, completion state, and separate route/page.
- [ ] A midpoint cumulative review exists when the course length/content justifies it; a justified omission or compact checkpoint is documented for very short courses.
- [ ] Each meaningful prerequisite dependency has a just-in-time recall bridge before the new topic's theory page when pedagogically useful. The bridge tests only already-taught material and does not reveal answers before an attempt.
- [ ] High-value foundations return through spiral deepening (new context/representation, integration, explanation, debugging, design, or transfer), not merely repeated low-level recall.
- [ ] Review tasks are not copied 1:1 from earlier lesson exercises. Check IDs and exact hashes, then manually inspect semantic similarity: context, data, prompt, options, cognitive operation, and solution path. Number changes alone do not count as meaningful variation for substantive skills.
- [ ] Every required outcome is revisited in an assessment format that can actually demonstrate it.
- [ ] Feedback/remediation after failed recall uses a fresh parallel task; the original answer is not simply re-presented as a new attempt.
- [ ] The schedule includes review workload and catch-up capacity; due items do not create an endless queue or silently block all new learning.
- [ ] Review due dates, attempts, section completion, and concept mastery survive reload where storage permits and are included in export/import where practical.
- [ ] The app has been tested for a learner who remembers prerequisites and one who has forgotten them; the latter receives targeted refresh/remediation before proceeding to dependent advanced work.

## 8. Executive-function support without learning dilution

- [ ] A returning learner can see one clear next action and resume the exact unfinished step.
- [ ] Session time estimates are realistic and a task has an explicit stopping/completion condition.
- [ ] The schedule includes buffer capacity and handles absences without punitive resets or an unmanageable backlog.
- [ ] Optional timers/reminders do not interrupt, auto-submit, or penalise the learner.
- [ ] The default interface is calm and does not overload the learner with competing calls to action.
- [ ] Project breakdowns help action planning without fragmenting meaningful deep-work tasks.
- [ ] Graduated hints preserve an initial attempt and productive struggle; solutions are not exposed prematurely.
- [ ] Distributed review, prerequisite activation, spiral deepening, difficulty progression, independent practice, and mastery thresholds remain intact.
- [ ] No shame-based copy, forced streaks, social comparison, or manipulative engagement loops are present.
