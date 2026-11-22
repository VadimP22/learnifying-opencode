# Executive-Function-Friendly Learning Design

## Purpose and boundary

Design the learning experience to reduce avoidable friction associated with task initiation, working-memory load, time estimation, prioritisation, transitions, and returning after interruptions. These are broad design considerations, not diagnostic criteria. Do not infer that a learner has ADHD, request medical disclosure, or present the app as treatment.

The product should be useful to many learners, including learners who experience executive-function difficulties. Use neutral names such as `Фокус и организация` rather than a mandatory `ADHD mode`.

**Core rule: reduce organisational friction, not intellectual challenge.** Keep the same learning outcomes, adequate practice, retrieval effort, and mastery standards unless the learner explicitly needs a legitimate accessibility accommodation that changes the delivery method.

## 1. Starting friction

- Show one primary next action at a time on the home screen.
- Make the first action concrete and small: open the lesson, answer one recall prompt, or run the first example.
- Display an honest time estimate and what counts as “done”.
- Provide a short-entry option (for example, a brief restart/warm-up) that helps the learner begin. Do not count setup or orientation as mastery.
- Avoid onboarding questionnaires with many optional preference questions. Ask only for information that changes the course; use editable defaults for the rest.

## 2. Working memory and task clarity

- Use predictable lesson structure and stable navigation.
- Keep instructions visible while the learner works; avoid requiring them to remember a long instruction from another screen.
- Convert large assignments into milestones with concrete deliverables and dependencies.
- Use checklists for multi-step setup, project work, and submission criteria.
- Show necessary prerequisites and relevant earlier concepts at the point of use.
- Use progressive disclosure: expose detail when it becomes relevant, while preserving access to the full course map.
- Avoid excess badges, dashboards, simultaneous calls to action, decorative animations, and dense walls of text.

## 3. Time, pacing, and scheduling

- State duration estimates as estimates, not deadlines. Calibrate them against task complexity and user feedback.
- Offer a small number of session choices, with an obvious default. For instance: a brief start/re-entry session and a regular session. A deep-work block may be available when the subject requires it.
- Timers are optional, non-punitive, and never auto-submit, hide work, or interrupt an active assessment.
- Include buffer/catch-up capacity in the initial plan.
- Let learners move sessions without losing completed progress.
- After missed sessions, recalculate the plan around remaining time and learning priorities. Do not demand that every missed minute be “paid back”.
- Keep reviews visible, but prioritise due concepts so the queue does not become an intimidating wall of overdue tasks. Never silently delete overdue material.

## 4. Resuming after interruption

Provide a concise re-entry card:

- `Где остановились` — last completed/attempted lesson and exercise.
- `Что уже получается` — genuinely demonstrated outcomes, not generic praise.
- `Что важно вспомнить` — one or two high-value recall prompts, when appropriate.
- `Следующий шаг` — one concrete action and estimated time.

Do not restart the course from zero, shame the learner, or reset mastery because of elapsed calendar time. Reassess mastery only when evidence from retrieval/practice justifies it.

## 5. Motivation and feedback

- Use neutral, specific, actionable feedback: describe what worked, what is missing, and the next useful move.
- Treat errors as information for adaptation, not moral failure.
- Make progress visible by outcomes, skills, and completed work.
- Avoid compulsory streaks, loss aversion, leaderboards, public comparison, fake urgency, and guilt-inducing reminders.
- Notifications and reminders should be optional, easy to pause, and respectful of user control.
- Never imply that the learner is lazy, undisciplined, or at fault for missed study time.

## 6. Preserve deep learning

Accommodations must not hollow out the learning design:

- Keep the sequence **theory → worked example → practice** for new content.
- Keep retrieval practice: the learner should attempt to recall before seeing the answer.
- Use graduated hints. Early hints point to a relevant concept or next step; later hints become more specific. Reveal the worked solution only after a reasonable attempt or an explicit learner request.
- Keep increasing task complexity and fading scaffolding across the course.
- Do not turn every exercise into a sequence of trivial clicks. Some tasks need a continuous period of sustained reasoning.
- Do not replace independent performance with repeated multiple choice if the outcome requires construction, explanation, debugging, or transfer.
- Provide breaks at natural boundaries, not during a learner's active reasoning or assessment unless requested.
- Keep review timing based on memory and performance, not only on convenient calendar chunks.

## 7. Sensory and interface choices

- Use a calm visual hierarchy, readable typography, clear focus states, and consistent controls.
- Respect reduced-motion settings; avoid flashing, auto-playing media, and unnecessary sound.
- Allow optional control over visual density, theme/contrast, timer, and reminders where practical.
- Keyboard navigation and screen-reader semantics are baseline accessibility, not premium focus features.
- Do not make the UI childish, medicalised, or overly gamified.

## 8. Personalisation without over-questioning

- Do not assume every learner with ADHD has the same needs; do not assume every executive-function difficulty is ADHD.
- Ask about concrete learning constraints only when they materially affect scheduling or delivery (for example, typical available session length, device constraints, or a need for reduced motion).
- Let the learner opt into or out of organisational aids without affecting course completion or mastery.
- Prefer sensible defaults and make them easy to adjust.

## 9. Acceptance tests

Before release, test at least these scenarios:

1. A new learner sees one obvious first action and understands how long it may take.
2. A learner leaves halfway through a multi-step exercise and returns to the exact unfinished step.
3. A learner misses several planned sessions and receives a manageable revised plan without shame or a massive backlog.
4. A learner uses a brief-entry session and is then guided toward meaningful learning, not falsely marked as having mastered the lesson.
5. A learner uses a timer; it does not interrupt or submit work.
6. A learner requests hints; the hint ladder helps without immediately giving away the solution.
7. A long-form task retains an uninterrupted work area and is not fragmented into unnecessary micro-steps.
8. Turning off optional reminders, timers, sound, or motion does not break the learning experience.

A design passes only if executive-function friction is lower while the learning objectives and assessment integrity remain intact.
