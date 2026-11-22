# Distributed, Cumulative, and Spiral Review Architecture

Internal instructional-design and implementation standard. Internal planning and schemas are in English; all learner-facing labels, explanations, prompts, and feedback must be in Russian.

## 1. Core principle

**Revisit knowledge, not previously memorised answers.** A review must test whether the learner can retrieve and use an earlier concept after a delay, in a fresh task or representation. Never copy an earlier exercise verbatim or make a cosmetic edit that preserves the same answer path.

Review is part of the course architecture, not an optional pile of extra questions at the bottom of ordinary lessons. Plan it in the course map before writing lesson prose or implementing the app.

## 2. Four complementary review mechanisms

Use the mechanisms below where pedagogically appropriate. They solve different problems and must not be collapsed into one generic review queue.

### A. Interleaved review sections between topic blocks

Create named, visible review sections in the course roadmap between meaningful units or topic blocks. These are standalone course sections with their own identity, purpose, estimated time, completion state, and route/page. They should mix selected concepts from more than one earlier lesson when the learner has enough foundation for meaningful interleaving.

Examples of Russian learner-facing labels:
- `Повторение: фундаментальные понятия`
- `Практикум по пройденным темам`
- `Проверка связей между темами`

A review section is not a new theory lesson. It may include a very brief reminder or a link back to an explanation after the learner has attempted recall, but its main purpose is retrieval, application, diagnosis, and feedback. Do not introduce un-taught concepts as if they were review material.

Place these sections at natural transition points, such as after a cluster of related topics or before a more demanding unit. Frequency depends on course length, workload, concept density, and due items; do not force a review section after every lesson.

### B. Mid-course cumulative review section

For courses with enough duration/content, include a clearly visible, standalone cumulative review section around the transition between the first and second halves of the course. It should revisit high-value foundations and selected earlier outcomes, reveal weak prerequisite links, and prepare the learner for the more integrative second half.

Do not make this a high-stakes surprise exam. Give it a clear scope, realistic duration, varied tasks, actionable feedback, and a path to targeted remediation. For very short courses, use a compact cumulative checkpoint at the most meaningful midpoint instead of inventing a large review week. If a distinct midpoint section would consume disproportionate time, explain the trade-off and use a smaller checkpoint.

### C. Just-in-time prerequisite recall before dependent new topics

Use the prerequisite graph to identify when a forthcoming topic materially depends on knowledge taught earlier. Before the new topic's theory page, insert a short, separate `Prerequisite Recall` section/page (Russian label, for example, `Вспомним необходимое`) that asks the learner to retrieve the specific prerequisite concepts needed next.

The bridge must:
1. Name the prerequisite concepts in learner-friendly language without giving away their answers.
2. Ask for a genuine attempt before revealing explanations or hints.
3. Use a fresh prompt/task, not the old exercise.
4. Check only previously taught material; do not test the not-yet-taught new concept.
5. Give targeted feedback. If recall is weak, provide a concise refresher or link to the exact prior theory section, then use a different follow-up item.
6. Lead into the new topic by making the connection explicit: “this earlier idea is needed because…”

Do not insert a bridge mechanically before every lesson. Use it when there is a meaningful prerequisite dependency, a sufficiently important concept, a likely forgetting gap, a long delay, or evidence from the learner's history that recall is fragile. Keep it brief; it should activate knowledge, not become a second full lesson or an unnecessary gate that blocks all progress.

### D. Spiral deepening

Return to important concepts multiple times across the course, each time expanding what the learner can do with them. This is more than spacing the same recall question. Plan a progression from initial understanding to richer and more independent use.

Possible progression:
- First encounter: recognise, describe, or perform a small guided operation.
- First revisit: retrieve and explain the concept without the original explanation visible.
- Later revisit: use it in a new example, representation, or practical context.
- Deeper revisit: connect it to another concept, diagnose a misconception, compare alternatives, or handle a new constraint.
- Advanced revisit: transfer it to an unfamiliar problem, design a solution, justify trade-offs, or use it as a prerequisite for a more advanced concept.

Choose only stages appropriate to the concept and course scope. Do not inflate the curriculum by repeating every minor fact at every level. Concentrate spiral deepening on durable foundations, high-value skills, and concepts that unlock later learning.

## 3. Designing genuinely new review tasks

For every resurface of a concept/outcome, use a new exercise identity and a meaningfully different task. Never repeat the same prompt, exact data, code, diagram, answer options, or solution path 1:1.

When possible, vary at least two meaningful dimensions, including at least one beyond changing numbers or names:
- context or domain scenario;
- representation (text, diagram, graph, code, data table, physical model, or verbal explanation);
- direction of reasoning (derive an output vs infer an input; diagnose vs construct; predict vs explain);
- cognitive operation (identify, explain, calculate, implement, debug, compare, justify, design);
- constraints, boundary cases, assumptions, or available information;
- task format (short answer, practical build, oral-style explanation, simulation, critique, multi-step problem).

A changed number alone is not sufficient variation for a high-value concept. For narrow factual recall where a different cognitive operation would be artificial, vary the prompt/context/answer format and ensure the exact item is not duplicated.

Maintain item lineage so the authoring/QA process can compare repeated tasks:
- `exerciseId`: unique task instance;
- `conceptIds` and `outcomeIds`: what the item measures;
- `variantFamilyId`: optional family of parallel tasks measuring the same target;
- `reviewPurpose`: spaced, cumulative, prerequisite-bridge, or spiral-deepening;
- `variationNotes`: what changed from earlier tasks and why the new task tests transfer rather than answer memory.

Use a semantic duplicate review in addition to ID/hash checks. Exact string hashes catch exact copies but cannot detect near-identical tasks with superficial edits. Compare prompt, inputs, answer choices, required reasoning, and solution path. Never use an identical task merely because the learner previously got it wrong: diagnose the gap and create a fresh parallel task.

Do not reveal the old answer before a fresh attempt. A post-attempt explanation may explicitly connect the result to the earlier concept or show the earlier worked example as a comparison, but that comparison must not substitute for a new assessment item.

## 4. Build the review map from concepts and dependencies

Before generating review questions:
1. Create stable IDs for concepts, skills, learning outcomes, lessons, and units.
2. Build a prerequisite/dependency graph and mark high-value foundations.
3. Map each lesson's new concepts to previously taught prerequisites.
4. Identify course transition points and the approximate midpoint.
5. Allocate each important concept to one or more later review events and, where useful, deeper spiral applications.
6. Ensure review events collectively cover required outcomes, not just easy-to-quiz facts.
7. Check the time budget. Reserve time for review, practice, assessment, and catch-up rather than treating review as unlimited extra workload.

Create a concise `docs/REVIEW_ARCHITECTURE.md` containing:
- review-section schedule and rationale;
- concept/outcome coverage map;
- prerequisite bridges and the new topics they prepare for;
- spiral progression for foundational concepts;
- initial intervals and adaptation rules;
- workload estimate and queue limits;
- known gaps/trade-offs.

The canonical course map and lesson manifest must link to this review architecture using stable IDs. Do not keep the only copy of the schedule inside an agent transcript.

## 5. Adaptive spacing and learner performance

Use active retrieval rather than passive rereading. A configurable starting interval ladder may be 1, 3, 7, 14, and 30 days after successful retrieval, but treat it as a heuristic, not a universal law. Compress or expand it to fit the course duration and learner schedule. Schedule also by meaningful course transitions, not only by elapsed days.

Suggested adjustment:
- Incorrect, blank, or guessed: provide specific feedback and schedule an earlier, fresh attempt. If a critical prerequisite is missing, place a short remediation before or alongside the dependent topic.
- Correct with a hint or substantial effort: use a shorter interval and a different prompt/representation.
- Correct independently with a sound explanation: move to a longer interval or the next spiral application.
- Fluent, accurate, and transferable: revisit later in an integrated task rather than repeatedly drilling the same simple format.

Track learner confidence only as an optional self-report; never use confidence alone to infer mastery. Keep attempted, completed, and mastered states distinct. A single correct multiple-choice response is not sufficient evidence of practical mastery.

Avoid a punitive or unbounded queue. Prioritise by:
1. prerequisite-critical concepts needed by an upcoming topic;
2. overdue high-value foundations;
3. concepts with recent errors or fragile recall;
4. planned cumulative/spiral review events;
5. lower-priority enrichment.

Cap the amount of review presented in one session according to the learner's time budget. Carry excess forward with a transparent plan; do not silently drop it, flood the learner with overdue work, or block all new learning. After missed sessions, recalculate priorities without shame or loss of established mastery.

## 6. Course navigation and interaction model

Review sections must be visible as distinct entries in the course roadmap and calendar, not disguised as ordinary new lessons or buried at the bottom of practice pages. Use dedicated hash routes, for example:
- `index.html#/review/review-after-unit-02`
- `index.html#/review/mid-course-cumulative`
- `index.html#/review/prerequisite-bridge-unit-04`

The exact route convention may follow the project, but each review section needs a stable ID and its own page/view. A prerequisite bridge appears immediately before the dependent lesson in the learning path. Preserve separate theory and practice routes for ordinary lessons; do not move an ordinary lesson's assigned practice into its theory page.

The roadmap should distinguish visually between:
- new learning;
- ordinary lesson practice;
- standalone review sections;
- prerequisite recall bridges;
- cumulative checkpoints;
- final assessment.

Display a concise reason for each review in Russian (for example, `Повторяем основы функций перед изучением производных`). Do not reveal answers in the reason label.

## 7. Suggested course data model

Keep the schema compact and validate it. Use stable IDs and references instead of duplicating long lesson content.

A section can be represented as:

```json
{
  "id": "review-mid-course",
  "type": "review",
  "reviewKind": "midcourse-cumulative",
  "title": "Большое повторение: основы курса",
  "estimatedMinutes": 30,
  "positionAfterUnitId": "unit-03",
  "targetConceptIds": ["concept-functions", "concept-derivatives"],
  "targetOutcomeIds": ["LO-02", "LO-05"],
  "exerciseIds": ["review-ex-01", "review-ex-02"],
  "prerequisiteForLessonIds": [],
  "completionCriteria": ["..."],
  "reason": "Подготовка к объединению ранее изученных методов"
}
```

A prerequisite bridge can reuse the same section type with `reviewKind: "prerequisite-bridge"`, a `prerequisiteForLessonIds` target, and only concepts already taught.

Review tasks use the normal exercise schema plus review metadata:

```json
{
  "id": "review-ex-01",
  "conceptIds": ["concept-functions"],
  "outcomeIds": ["LO-02"],
  "reviewPurpose": "spiral-deepening",
  "variantFamilyId": "functions-transfer-family",
  "variationNotes": "Switch from evaluating a supplied function to diagnosing a function model from a graph in a new context.",
  "difficulty": 3,
  "scaffoldLevel": 1
}
```

Track review state separately from authored course content, for example:
- `lastAttemptAt`, `lastResult`, `hintUsed`, `confidence` (optional);
- `intervalIndex`, `dueAt`, `nextReviewAt`;
- `masteryState`, `attemptCount`;
- `completedReviewSectionIds`;
- task IDs/variant families already attempted, to avoid accidental duplicate assignment.

Do not store answer keys in learner-facing progress exports unless required by the app design; never expose solutions before the attempt.

## 8. Context-efficient orchestration

The lead agent owns the final review design and course integration. Do not make every subagent read every lesson to reason about repetition.

- For a short course with few dependencies, the lead agent can build the review map directly from the concept graph and course map.
- For a long course, many units, or a dense prerequisite graph, optionally delegate a single bounded package to `learnifying-review-architect`.
- Give that worker only: learner brief summary, course duration/time budget, unit and lesson IDs, concept/outcome IDs, prerequisite edges, learning objectives, topic transition points, and the planned lesson schedule. Include the full lesson prose only when a specific item needs review for uniqueness; normally it does not.
- Ask for `docs/REVIEW_ARCHITECTURE.md`, not a complete rewritten course. Require stable ID references and a compact table.
- Do not run the review architect and curriculum reviewer as concurrent authors of the same review file. The architect proposes; the parent integrates; the reviewer later audits.
- The curriculum reviewer should inspect the review map using the same compact concept graph, not reread every source document or exercise unless investigating a suspected duplicate or coverage defect.
- Pass the approved review map and only the relevant task variant records to implementers.
- The final auditor samples and traces high-value concept paths end-to-end, checks all review-section placements and duplicate-detection reports, and records untested areas. Do not paste the entire course into its prompt if it can inspect workspace files.

If subagents are unavailable, the main agent performs the same bounded steps and saves the review architecture before authoring all lesson prose.

## 9. Acceptance criteria

The design passes only if:
- Standalone review sections appear at meaningful points between topic blocks when course length permits.
- A distinct midpoint cumulative review exists for courses where it is pedagogically and temporally justified.
- Important prerequisite concepts are retrieved before dependent new concepts when a meaningful dependency exists and review is useful.
- Foundational concepts return through spiral deepening, not only identical flashcards or same-level quizzes.
- Every required outcome is revisited in an appropriate assessment format.
- No exact or near-identical exercise is reused as if it were a new review task; variation is documented.
- Review attempts precede answer reveal and feedback is actionable.
- Review workload is visible, realistic, adaptive, and not punitive.
- Progress and review state persist where the chosen browser storage supports it, with export/recovery where practical.
- Review sections are distinct in navigation and are not appended to normal lesson theory pages.
- The curriculum reviewer and final auditor have checked the review map, prerequisite bridges, spiral progressions, and task uniqueness.
