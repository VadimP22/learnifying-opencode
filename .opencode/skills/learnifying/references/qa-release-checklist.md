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
- [ ] Previously taught concepts reappear through due retrieval practice.
- [ ] Review load is manageable and overdue items are not silently dropped.
- [ ] Feedback explains why an answer is wrong and how to recover.
- [ ] Final assessment matches the advertised learning outcomes.
- [ ] Learner-facing copy is Russian, with conventional technical terminology where appropriate.

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

## 5. Minimum manual test journey

1. Open the app as a new learner.
2. Start and complete the diagnostic (if present).
3. Open the first lesson theory page; confirm it contains the intended explanations and visual aids, and does not contain the assigned graded practice set.
3a. Navigate to the separate practice page; confirm exercises, checking, hints, and feedback work there.
4. Submit a deliberately incorrect answer; confirm explanatory feedback and remediation.
5. Submit a correct answer; confirm the checker really executes and progress updates.
6. Reload the app; confirm progress persists.
7. Trigger or simulate a due review; confirm a previously learned concept appears.
8. Complete a review and check that its next due date changes appropriately.
9. Navigate to a later, harder lesson and confirm scaffolding has been reduced as designed.
10. Test any domain-specific renderer/runtime, including unsupported-device fallback; compare observed behaviour to `docs/VISUAL_IMPLEMENTATION_DECISIONS.md`.
11. Close the dev server, open the final `index.html` directly from disk (`file://`), and test reload, theory/practice navigation, visuals, and local progress storage.

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


## 7. Executive-function support without learning dilution

- [ ] A returning learner can see one clear next action and resume the exact unfinished step.
- [ ] Session time estimates are realistic and a task has an explicit stopping/completion condition.
- [ ] The schedule includes buffer capacity and handles absences without punitive resets or an unmanageable backlog.
- [ ] Optional timers/reminders do not interrupt, auto-submit, or penalise the learner.
- [ ] The default interface is calm and does not overload the learner with competing calls to action.
- [ ] Project breakdowns help action planning without fragmenting meaningful deep-work tasks.
- [ ] Graduated hints preserve an initial attempt and productive struggle; solutions are not exposed prematurely.
- [ ] Spaced retrieval, difficulty progression, independent practice, and mastery thresholds remain intact.
- [ ] No shame-based copy, forced streaks, social comparison, or manipulative engagement loops are present.
