# Curriculum Design Standard

## 1. Start with the learner and the outcome

Convert the learner's goal into observable capabilities. Avoid vague objectives such as “understand shaders”. Prefer “write a fragment shader that applies a time-varying colour effect, explain the role of uniforms, and diagnose a compile error”.

Record:
- learner goal and target audience/context;
- assumed or diagnosed starting level;
- prerequisites and prerequisite gaps;
- total calendar duration;
- weekly study budget and session length;
- constraints (software, hardware, exam syllabus, accessibility, deadline);
- measurable end-state and proof of competence.

If level is unknown, include a short, low-stakes diagnostic with explanations. Do not use the diagnostic to shame or label the learner; use it to set a suitable starting point.

## 2. Build the prerequisite graph

Break the subject into concepts and skills. Mark each as:
- prerequisite;
- core concept;
- procedural skill;
- integration/transfer skill;
- optional enrichment.

Represent dependencies as a directed graph or explicit prerequisite list. Teach prerequisites before dependent tasks. Avoid a course map that is merely a list of topic headings.

## 3. Define measurable learning outcomes

Each outcome should include an observable verb, an object, conditions, and a quality criterion where appropriate. Use verbs such as identify, explain, compare, calculate, implement, debug, evaluate, design, and justify. Match evaluation to the verb: a multiple-choice question cannot establish that a learner can independently implement a feature.

Map every lesson and exercise to one or more outcomes. Every required outcome must be assessed at least once and revisited later.

## 4. Plan duration and workload

Convert the user's time budget into available study minutes. Subtract sensible time for review, checkpoints, and catch-up; do not allocate 100% to new content.

A reasonable default lesson unit may be 25–50 minutes, but adapt to the domain and learner. Longer labs can span multiple blocks. Include:
- new material;
- worked examples;
- independent practice;
- short retrieval checks;
- spaced reviews;
- checkpoint assessments;
- buffer/catch-up time.

For a calendar plan, explicitly show week/day, lesson title, estimated duration, learning outcome, and whether it is new learning, practice, review, or assessment. Make dates relative to a stated start date or label the plan by Week 1, Day 1 if no start date is known.

## 5. Standard lesson sequence

Every regular lesson uses this order:

1. **Цели урока** — what the learner will be able to do.
2. **Связь с предыдущими темами** — prerequisites and a short recall prompt if useful.
3. **Теория** — structured explanation, definitions, intuition, purposeful diagrams/graphs/animations or interactive explanatory models where useful, common misconceptions, and source notes. The theory is delivered on its own page/route.
4. **Разобранный пример** — a fully worked example with intermediate steps and commentary, still within the theory/teaching experience.
5. **Практика** — exercises ordered from guided to independent, on a separate page/route from theory. Do not append a long exercise list beneath the theory text.
6. **Проверка и обратная связь** — actual automatic checks or a transparent manual rubric, with hints and explanations.
7. **Повторение** — due retrieval questions from older lessons, not just a summary to reread.
8. **Итог и следующий шаг** — concise recap, completion criteria, and preview.

A diagnostic can precede the first lesson. A short recall prompt at the start of a later lesson is permitted, but it does not replace that lesson's theory-before-practice order for new concepts.

## 6. Difficulty ramp

Design difficulty across several independent dimensions:

- scaffold level: worked solution → partial scaffold → independent;
- task size: one small operation → multi-step task → complete workflow;
- conceptual depth: direct application → explain why → compare alternatives;
- ambiguity: fully specified → choose method → interpret an open brief;
- integration: one concept → several prior concepts together;
- constraints: ideal conditions → debugging, performance, edge cases, or trade-offs;
- transfer: familiar example → unfamiliar context.

Early tasks should be small and forgiving. Remove scaffolding gradually. Increase one or two dimensions at a time; do not jump from a tutorial copy exercise to a large unassisted project. The final assessment should combine several outcomes and require explanation or reflection, not just mechanical repetition.

Example progression:
- Level 1: identify or change one value in a supplied example;
- Level 2: complete a partially prepared task;
- Level 3: create a small result from a clear specification;
- Level 4: debug a flawed example and explain the defect;
- Level 5: solve a multi-step problem with fewer hints;
- Level 6: integrate earlier skills in a new, realistic task and justify trade-offs.

Adapt the progression to the topic; levels are not a fixed number of lessons.

## 7. Spaced repetition and retrieval practice

Use active recall: ask the learner to retrieve, explain, calculate, implement, or distinguish an earlier concept before showing the answer. Prefer short mixed review sets over passive rereading.

Use an adaptive schedule, not a rigid claim that one forgetting curve fits everyone. A simple default interval ladder is 1, 3, 7, 14, and 30 days after successful retrieval; adjust to course length and remaining time. A practical grading rule:
- Again / incorrect or guessed: show targeted feedback and schedule soon (e.g. next day or same session for a prerequisite-critical error);
- Hard / correct only with major effort or hint: repeat in a shorter interval (e.g. 1–3 days);
- Good / correct independently: move to the next interval;
- Easy / fluent and explained accurately: move farther along the interval ladder.

These are configurable defaults, not universal psychological constants. If a course is shorter than the interval, compress intervals to fit while retaining spacing. If a learner repeatedly fails, reduce difficulty, reteach the prerequisite, and then test again with a new example.

Review queue rules:
- resurface high-value concepts after initial learning;
- mix older concepts with current material once the learner has a foundation;
- prioritise due reviews and prerequisite-critical errors;
- do not overload a day—cap the review queue and carry excess forward;
- explain why an item is being reviewed (topic/lesson) without revealing the answer;
- store last attempt, result, interval, due date, and difficulty rating.

## 8. Mastery and remediation

Set explicit completion criteria per lesson and unit. A suggested starting point is 80% on objective checks plus successful completion of a core practical task without step-by-step hints; adjust for subject risk and task type. Do not let a high quiz score substitute for a required practical skill.

After failure:
1. identify the underlying misconception or missing prerequisite;
2. give specific explanatory feedback, not only “wrong”;
3. offer a hint or simpler worked example;
4. present a parallel exercise with different values/context;
5. schedule a later retrieval check.

Avoid infinite locked progression. Allow learners to revisit content and distinguish “attempted” from “mastered”.

## 9. Course manifest schema

Use a stable, data-driven schema. A lesson record should include at least:

```json
{
  "id": "unit-01-lesson-01",
  "unitId": "unit-01",
  "title": "...",
  "estimatedMinutes": 35,
  "scheduledFor": "week-01-day-01",
  "outcomes": ["LO-01"],
  "prerequisites": [],
  "difficulty": 1,
  "theory": [{"id": "t1", "type": "text", "title": "...", "body": "...", "sourceIds": ["S-01"]}],
  "workedExamples": [{"id": "ex1", "title": "...", "steps": []}],
  "exercises": ["exercise-01"],
  "reviewConceptIds": [],
  "completionCriteria": ["..."]
}
```

Exercise records should be separate and include `type`, `prompt`, `inputSpec`, `expected`, `hints`, `feedback`, `checker`, `rubric`, `outcomes`, and `difficulty`. Do not store executable user code as trusted course configuration.

## 10. Final assessment

Use a cumulative assessment that maps to the course outcomes. For practical subjects, prefer a capstone, portfolio artifact, experiment, implementation, or realistic scenario plus a short explanation. Include a rubric with criteria and levels. A learner should know what “finished” means before beginning the final task.


## 10. Executive-function-friendly course design

Read `executive-function-friendly-design.md` for the full interaction policy. Apply it while planning the calendar and lesson structure:

- Give each session a named purpose, realistic duration, concrete first action, and clear completion condition.
- Include buffer/catch-up capacity in the schedule. Do not schedule every available minute as new instruction.
- Prefer a predictable lesson structure and explicit transitions between theory, examples, practice, and review.
- Use optional short-entry tasks to help the learner begin, but do not count an orientation/setup action as mastery of the lesson outcome.
- Retain sufficiently long uninterrupted blocks for deep work when the outcome requires it.
- After missed sessions, preserve learned mastery, identify the most important next action, and reschedule only what is pedagogically necessary.
- Keep low-stakes retrieval and cumulative review. A supportive tone must not turn recall into passive rereading or reveal answers before a genuine attempt.


## 11. Visual explanation planning

Treat visual explanations as a core instructional design decision. For every major concept, ask what the learner needs to see to understand it: structure, relationships, spatial form, change over time, causality, quantitative trend, algorithmic state, or the result of manipulating a parameter. Choose a representation that directly exposes that feature. Examples include labelled diagrams, concept maps, timelines, annotated graphs, state-transition diagrams, step-by-step illustrations, interactive parameter controls, simulations, and live rendered output.

Record the visual choice in the lesson specification (concept/outcome, learning purpose, visual form, learner interaction if any, caption/labels, source or derivation, and fallback). Prefer one clear, well-integrated visual over a collection of unrelated images. Explain what to notice and connect the visual explicitly to the accompanying prose.

The theory page may contain exploratory interactions that explain a mechanism (for example, changing a shader uniform and observing its output). These are explanatory demonstrations, not the assigned graded exercise. Keep assessed tasks, submissions, scoring, and practice feedback on the separate practice page. Read `visual-learning-and-explanations.md` for implementation and accessibility requirements.
