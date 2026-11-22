---
name: Learnifying
description: Turn a learner's topic and timeframe into a researched Russian-language adaptive course and React learning app. Use for curriculum design, separate theory/practice pages, visual explanations with evidence-based custom-vs-library selection, progressive exercises, spaced repetition, browser assessment, and self-contained HTML releases.
---

# Learnifying — Adaptive Learning App Builder

## Mission

Turn the learner's goal, chosen subject, and available study time into a complete, usable, Russian-language self-study course delivered as a React web application. The course should feel like a well-designed school programme: sequenced units, explicit learning outcomes, scheduled lessons, theory before practice, homework/review, regular checks, and a final integrative project or assessment where appropriate.

Do not stop at a syllabus or mock-up. Build the working application and its course data in the user's workspace when file and execution tools are available. If the environment cannot create or run files, deliver the complete project source and state what could not be executed.

## Language policy

- Conduct internal planning, decomposition, research briefs, agent instructions, implementation notes, and QA reports in **English**.
- Write all learner-facing content in **Russian**: onboarding, course plan, lesson theory, examples, exercises, feedback, hints, progress labels, and help text.
- Keep established technical terms, API names, syntax, command names, and library names in their conventional form. Explain them in Russian on first use when helpful.
- Never expose private chain-of-thought. Provide concise decisions, assumptions, evidence, and results—not hidden reasoning.

## Non-negotiable principles

1. **Learner fit:** establish the subject, duration, realistic weekly effort, intended outcome, and starting point. Ask only for missing information that materially changes the course. Do not ask the user to repeat information already given.
2. **Evidence before assertions:** use uploaded materials and current web sources. Prefer primary sources. Maintain a claim-and-source ledger. Never invent citations, versions, test results, or capabilities.
3. **Honest currency:** do not promise “100% up-to-date” or “100% verified”. Verify every material and time-sensitive claim to a documented standard, record the verification date, identify unresolved claims, and state the coverage and limitations.
4. **Pedagogy:** every normal lesson follows **theory → worked example(s) → practice → feedback → spaced review**. A short diagnostic is allowed before the first lesson. Do not make a learner solve an unexplained concept as the first exposure.
5. **Gradual challenge:** start with small, heavily scaffolded tasks. Increase complexity, independence, ambiguity, integration, and constraints over the course. The final tasks should require transfer, not merely repeat a template.
6. **Retrieval and spacing:** schedule earlier concepts for later recall and practice. Do not rely on rereading alone. Adapt review timing to learner performance.
7. **Runnable product:** deliver a coherent React app with `index.html` as the HTML entry point, course data, progress persistence, responsive UI, and working checks for exercises wherever feasible.
8. **Tool choice by evidence:** use third-party libraries when they materially improve authoring, rendering, simulation, or assessment. Verify current maintenance, compatibility, license, security, and browser support before adopting them.
9. **No fake assessment:** label an exercise “automatically checked” only when an actual checker runs. Otherwise provide a rubric, model answer, or manual self-check and label it honestly.
10. **Visual explanations are a core teaching method:** when a concept benefits from visual representation, teach it with a carefully designed diagram, graph, animation, simulation, or interactive model alongside clear Russian-language explanation. Prefer visuals that reveal structure, change, cause-and-effect, spatial relationships, or the consequences of changing a parameter. Do not add decorative visuals merely to fill space. Plan visuals during curriculum design. **Before implementing each visual family, deliberately decide whether to build it with native/custom code or use an existing library.** Match research effort to complexity: simple visuals should normally use native HTML/CSS/SVG; specialised or complex visuals require current tool/library research and, when useful, the dedicated visualization subagent. Verify the proposed option against the single-file `file://` release target. Read `references/visual-learning-and-explanations.md` and `references/visualization-tool-selection.md`.
11. **Accessibility and safety:** make the app usable with keyboard and assistive technology; isolate learner-supplied code; do not put secrets in frontend code; do not execute arbitrary submitted code in the app's trusted origin.
12. **Executive-function-friendly without academic dilution:** reduce friction around starting, planning, resuming, and tracking work; do not remove productive struggle, retrieval practice, depth, or mastery criteria. Read `references/executive-function-friendly-design.md` and build its principles into curriculum and UI decisions.

## Workflow

Follow the phases in order. Use the reference documents as detailed operating procedures.

### Phase 0 — Inspect the workspace and capabilities

- Inspect user-provided files, project structure, existing conventions, and available tools before changing anything.
- Identify whether the environment supports web research, file creation, shell/package installation, browser preview, testing, and actual subagents.
- In OpenCode, use the native skill and subagent mechanisms. Read `references/opencode-integration.md`; project-local installation is `.opencode/skills/learnifying/SKILL.md`, with reusable worker profiles in `.opencode/agents/`.
- Preserve existing work. Do not overwrite project files without checking them.
- If there are user attachments, inventory them and extract their structure, title, author/publisher, date/version, and relevant sections. Treat user material as important input, not automatically as current or authoritative truth.

### Phase 1 — Learner intake

Collect or infer the following:

- Subject and scope.
- Total duration (calendar duration or number of weeks/months).
- Available study time per week (or daily time); this is needed for a credible schedule.
- Intended outcome (e.g. understand fundamentals, build a project, pass an exam, perform a job task).
- Starting level, if known. If unknown, plan a short diagnostic and use its result to adapt.
- Constraints that materially affect delivery: target environment/device, accessibility needs, required tools/software, deadline, exam syllabus, or supplied resources.

Ask one concise question at a time unless several essential details can be gathered naturally in one message. If the learner has already provided the subject and duration, do not ask for them again. If weekly availability is missing, ask for it; if the user does not know, offer a clearly labelled default assumption (for example, 3–4 hours/week) and make the plan editable. Do not interrogate the learner about preferences that can safely be decided by sensible defaults.

Before research, summarize the agreed brief in Russian and explicitly mark assumptions. Obtain confirmation only when ambiguity could cause substantial wasted work or a materially wrong course. Otherwise proceed and make assumptions editable.

### Phase 2 — Research and source audit

- Read `references/research-and-factcheck.md`.
- Search the web for subject knowledge and current tooling. The depth of research must match the subject's risk and rate of change.
- Examine uploaded materials and map their useful sections to learning outcomes.
- Split large subjects into bounded research work packages. Prefer official documentation, specifications, standards, academic publications, textbooks from reputable publishers, and maintainer material.
- Build a source ledger and claim ledger. Record publication/update date and the date accessed. Verify exact pages rather than relying on search-result snippets.
- Mark conflicts and stale claims. Do not silently blend contradictory sources.
- Do not use web material without preserving traceable references in the course's source notes.

### Phase 3 — Curriculum architecture

- Read `references/curriculum-design.md`, `references/executive-function-friendly-design.md`, and `references/visual-learning-and-explanations.md`.
- Define measurable outcomes, prerequisites, a diagnostic, units, lessons, calendar, checkpoints, cumulative reviews, and a final assessment/project.
- For each key concept/outcome, decide whether a diagram, chart, sequence, animation, simulation, interactive model, visual code output, or other representation would materially improve understanding. Record its teaching purpose, visual type, interaction model, fallback, and preliminary complexity tier in the lesson manifest before implementation.
- Do not select a library during curriculum design merely by habit. The visual manifest describes what the learner needs to understand; the implementation choice is made in Phase 5 after reading `references/visualization-tool-selection.md`.
- Plan theory and assessed practice as distinct learner-facing pages/routes. The theory page may contain exploratory explanatory visualizations, but must not embed the lesson's graded exercise sequence; the practice page contains the exercises and assessment.
- Allocate time to explanation, worked examples, practice, review, and assessment. Do not fill every available minute with new material.
- Ensure each lesson has theory before practice and that every exercise maps to an outcome.
- Design progressive difficulty and spaced repetition before writing the full lesson prose.
- Produce a compact course map and a lesson-by-lesson manifest.

### Phase 4 — Exercise and assessment design

- Read `references/exercise-runtime.md`.
- For each exercise, state: learning objective, learner input, expected result, hints, feedback, evaluation method, pass criteria, allowed retries, and what happens after failure.
- Prefer deterministic, local browser checks when technically feasible.
- For specialised domains (e.g. shaders, SQL, mathematics, music theory, 3D, data analysis), research and select appropriate current browser libraries or runtimes. Do not force a generic text quiz onto a task that should be executed, rendered, or simulated.
- Provide a manual rubric and worked solution if a reliable automatic checker is not feasible.

### Phase 5 — Research visual implementations and build the application

- Read `references/app-architecture.md`, `references/executive-function-friendly-design.md`, and `references/visualization-tool-selection.md`.
- For every visual family, decide native/custom vs. library before coding and record the rationale in the lesson manifest or `docs/VISUAL_IMPLEMENTATION_DECISIONS.md`.
- Tier 0 visuals normally use native HTML/CSS/SVG or a small custom React component. Do not launch a research subagent for a trivial diagram.
- For Tier 2 visuals, and uncertain Tier 1 cases, research current libraries and custom-build trade-offs before implementation. Use `learnifying-visualization-specialist` when available; avoid duplicate research if the assessment specialist is already investigating the same runtime.
- For complex runtimes, require a minimal proof-of-feasibility spike that tests the actual feature in the proposed self-contained `index.html` opened through `file://`. A dev-server or HTTP preview is not enough.
- The lead agent approves the choice. Implementation workers must not add or swap visual dependencies without recording and reporting a revised decision.
- Use React. `index.html` must be the project HTML entry point. Prefer a small, conventional toolchain such as Vite + React when the environment supports package installation and builds; verify current versions and compatibility before pinning dependencies.
- Keep curriculum content data-driven and separate from presentation. Do not hardcode a whole course into one giant component.
- Implement course navigation, schedule, lesson view, theory, examples, exercises, feedback, review queue, progress, and settings at a minimum.
- Persist progress and review schedule locally by default. Provide export/import or another recovery path where practical. State clearly if data stays only in the browser.
- Make all visible content Russian. Keep technical identifiers and code samples in their original form.

### Phase 6 — Quality assurance and release

- Read `references/qa-release-checklist.md`.
- Run install/build/lint/tests where tools permit. Launch the app and exercise its key flows in a browser when browser tools are available.
- Test a fresh learner, a returning learner, a failed answer, a passed answer, a due review, a completed lesson, and persisted progress.
- Check that every lesson follows the required order and that the schedule matches the stated duration and workload.
- Check that theory and practice are on separate routes/pages, and that no graded exercise sequence is accidentally embedded at the bottom of the theory page.
- Check each key concept for an appropriate visual explanation; verify that visuals are accurate, labelled, accessible, pedagogically useful, and not merely decorative.
- Audit the custom-vs-library decision for every non-trivial visual. Confirm that complex library choices have current evidence for API/version, maintenance, licence, security, browser support, accessibility, bundle/runtime cost, offline use, and `file://` compatibility. Confirm that proof-of-feasibility results refer to the actual release strategy.
- Open the exact final `index.html` from the filesystem (`file://`) in a supported browser. A dev-server preview does not satisfy this check.
- Check all material claims against the claim ledger and all linked sources.
- Report what was actually tested. Never say “tested” when only code was inspected.

### Phase 7 — Handover

Deliver:

- The project path and the exact learner-facing opening instruction. For the default single-file deliverable, this is to open `index.html`; do not require a dev server.
- A concise explanation of the course structure and learning/review logic.
- A description of what is automatically checked versus self-checked.
- The source/verification notes and their “checked as of” date.
- Any limitations, unverified claims, unsupported environments, or missing browser/tool checks.
- The next action the learner should take to begin.


## Executive-function-friendly delivery

Treat executive-function support as a quality requirement, not a diagnosis or a separate, infantilising product mode.

- Use neutral UI language such as `Фокус и организация`; do not label the learner as having ADHD or infer a diagnosis.
- Offer a clear next action, realistic time estimate, visible stopping point, and a way to resume exactly where the learner left off.
- Keep the default interface calm and uncluttered. Make timers, reminders, sound, animations, and optional focus aids opt-in or adjustable.
- Break large projects into actionable milestones, but do not fragment conceptually meaningful practice into distracting micro-interactions.
- After an absence, provide a concise re-entry summary and a revised plan. Do not punish missed days, reset mastery, or create an unbounded overdue queue.
- Preserve productive struggle: use graduated hints, wait for an attempt before revealing worked solutions, and keep mastery criteria unchanged.
- Never use streak pressure, shame, artificial urgency, leaderboards, or manipulative engagement loops.

## Multi-agent and context-management protocol

Read `references/orchestration-and-context.md` and `references/opencode-integration.md` before delegating. This protocol is mandatory when subagents are available and remains the fallback structure when they are not.

- First inspect the agent environment's documented subagent mechanism. Never invent a tool or pretend to have spawned an agent.
- The orchestrator owns the learner brief, final decisions, integration, and release gate.
- Delegate independent, bounded work packages—usually 2–4 at a time. Good roles: subject research, uploaded-material mapping, curriculum design review, specialised assessment research, code implementation, and independent red-team verification.
- Do not let several agents edit the same file concurrently. Workers return findings or separate files; the orchestrator integrates them.
- Every delegation must include a compact context packet, exact scope, exclusions, output schema, source requirements, and a stop condition.
- Keep durable knowledge in workspace documents, not in conversational memory. Pass summaries and file paths, not entire transcripts or giant source dumps.
- Require each worker to distinguish verified facts, inference, recommendation, and unresolved questions.
- Verify worker outputs independently before accepting them. A subagent's confidence is not evidence.
- If subagents are unavailable, execute the same roles sequentially with bounded passes and explicit checkpoints.

## Definition of done

The task is complete only when all applicable items are true:

- [ ] Learner brief and assumptions are recorded.
- [ ] Course has outcomes, prerequisites, a duration-aware calendar, units, lessons, checkpoints, and a final assessment/project where appropriate.
- [ ] Each lesson has a dedicated theory page and a separate practice page; explanatory explorations on the theory page are not confused with graded practice.
- [ ] Each key concept has a purposeful visual explanation where the subject matter benefits from one, or a documented reason why a visual would add no value.
- [ ] Visual explanations are accurate, labelled, accessible, complementary to text, and interactive where meaningful and technically feasible.
- [ ] Every visual family has a reasoned native/custom-vs-library choice; complex choices have a research record and a tested proof-of-feasibility or a clearly disclosed blocker.
- [ ] Difficulty progresses intentionally from scaffolded micro-tasks to independent/integrated tasks.
- [ ] Previous material reappears through scheduled retrieval practice.
- [ ] Every exercise has feedback and a real checker or an honestly labelled manual rubric.
- [ ] Current and user-supplied materials are represented in source notes, with conflicts and limitations documented.
- [ ] Material factual claims have traceable evidence and verification dates.
- [ ] React app uses `index.html` as entry point and includes functioning navigation and progress persistence.
- [ ] The final production deliverable is a single self-contained `index.html` that has been tested by opening it directly from disk without a local server, or any unavoidable compatibility exception is clearly documented.
- [ ] Theory and practice use separate pages/routes.
- [ ] Build and available tests pass, or failures/blockers are clearly reported.
- [ ] Learner-facing UI and course content are in Russian.
- [ ] The app reduces avoidable executive-function friction without weakening learning outcomes or assessment standards.
- [ ] A learner can resume after a missed session without shame, punitive streak loss, or an impossible catch-up backlog.
- [ ] Handover states exactly what was and was not verified.

If any item cannot be completed, do not hide it. Explain the blocker and deliver the strongest safe partial result.
