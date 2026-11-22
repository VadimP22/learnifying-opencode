# Agent Prompt Templates

Use these templates only through the platform's documented delegation mechanism. Keep prompts in English; request Russian only for learner-facing examples.

## A. Subject research scout

```text
ROLE: Subject-matter research scout
TASK: Research the assigned slice of the course and produce evidence-backed findings.
LEARNER/PROJECT CONTEXT: [topic, learner level, course goal, relevant constraints]
SCOPE: [finite questions and concepts]
OUT OF SCOPE: Whole-course design, UI implementation, unrelated history.
INPUTS: [uploaded-file paths/sections, existing claim IDs, official URLs]
METHOD: Search primary sources first; inspect source pages; verify dates/versions; cross-check high-impact or volatile claims.
EVIDENCE RULES: Search snippets are not evidence. Separate fact, inference, and recommendation. Do not claim certainty without support. Preserve direct URLs and exact section/version/date.
OUTPUT FILE/PATH: docs/research/[work-package].md
OUTPUT SCHEMA: Use the research worker schema in orchestration-and-context.md.
UNRESOLVED QUESTIONS: List explicitly.
STOP CONDITION: Assigned questions have evidence-backed answers or further verification is blocked; do not broaden the scope.
```

## B. Attachment analyst

```text
ROLE: User-material analyst
TASK: Map supplied materials to concepts, learning outcomes, and candidate lessons; identify edition/version/date and possible stale claims.
LEARNER/PROJECT CONTEXT: [brief]
SCOPE: Only supplied files [list] and specified sections.
OUT OF SCOPE: Reproducing copyrighted text; declaring unsupported claims correct.
INPUTS: Exact file paths.
METHOD: Inventory, inspect table of contents/sections, extract a concise concept map, note gaps and conflicts with current evidence if available.
EVIDENCE RULES: Cite filename and page/chapter/heading. Mark unreadable or inaccessible areas.
OUTPUT FILE/PATH: docs/research/attachment-map.md
OUTPUT SCHEMA: File inventory; concept map; outcome mapping; dated/versioned claims; gaps; conflicts; recommended citations.
UNRESOLVED QUESTIONS: List explicitly.
STOP CONDITION: All supplied files are inventoried and relevant sections mapped, or access limits are documented.
```

## C. Curriculum reviewer

```text
ROLE: Independent instructional-design reviewer
TASK: Audit the proposed course map for sequencing, pacing, outcome coverage, difficulty progression, distributed/cumulative review, prerequisite bridges, spiral deepening, and exercise uniqueness.
LEARNER/PROJECT CONTEXT: [brief]
SCOPE: Review [course map/lesson manifest].
OUT OF SCOPE: Inventing subject facts or implementing the app.
INPUTS: docs/PROJECT_BRIEF.md, docs/COURSE_MAP.md, course manifest.
METHOD: Trace prerequisites and outcomes; estimate workload; inspect every lesson's theory-example-practice order; inspect standalone review sections between topic blocks, midpoint cumulative review where justified, prerequisite-recall bridges before dependent new topics, spiral progressions, and review recurrence. Compare repeated exercise IDs/prompts/data/options/solution paths to detect 1:1 or cosmetic reuse. Verify later tasks require fresh retrieval or transfer.
EVIDENCE RULES: Ground feedback in specific lesson/outcome IDs. Distinguish blocking issues from recommendations.
OUTPUT FILE/PATH: docs/reviews/curriculum-review.md
OUTPUT SCHEMA: Critical defects; high-priority fixes; optional improvements; outcome coverage gaps; workload estimate; review-architecture assessment (interleaved sections, midpoint review, bridges, spiral deepening, task uniqueness); pass/fail recommendation.
UNRESOLVED QUESTIONS: List explicitly.
STOP CONDITION: Every unit and outcome has been checked against acceptance criteria.
```

## D. Review architecture specialist (optional; long or highly interconnected courses only)

```text
ROLE: Distributed and spiral review architect
TASK: Produce a compact review architecture from the approved concept graph and course map.
LEARNER/PROJECT CONTEXT: [topic, learner level, course goal, duration, weekly study budget]
SCOPE: Standalone interleaved review sections; midpoint cumulative review if justified; prerequisite-recall bridges before dependent new topics; spiral-deepening paths; adaptive spacing and workload.
OUT OF SCOPE: Writing full lesson prose, researching the entire subject, implementing UI, editing exercise files, rewriting the course map, or spawning agents.
INPUTS: docs/PROJECT_BRIEF.md, docs/COURSE_MAP.md, concept/outcome IDs, prerequisite edges, lesson schedule, relevant exercise metadata, references/distributed-and-spiral-review.md. Do not request full uploaded source documents or every lesson text unless a specific uniqueness issue requires it.
METHOD: Map high-value foundations to later review events; place visible review sections at natural topic boundaries and around mid-course when justified; insert just-in-time recall bridges before lessons with meaningful prerequisites; plan increasing-depth spiral revisits; allocate realistic time; propose fresh task variation dimensions and review item lineage.
EVIDENCE RULES: Use only concepts already taught for review; do not invent subject facts. Do not reuse prompts 1:1. Distinguish proposed schedule from learner-adaptive due dates.
OUTPUT FILE/PATH: docs/REVIEW_ARCHITECTURE.md
OUTPUT SCHEMA: Course-level review schedule; review section table (ID, placement, kind, target concepts/outcomes, minutes, rationale); prerequisite bridge map; spiral progression map; initial/adaptive interval policy; workload/queue limits; task-variation plan; unresolved risks.
UNRESOLVED QUESTIONS: List explicitly.
STOP CONDITION: Every high-value foundation and required outcome has an appropriate later revisit, or a specific omission and reason are recorded.
```

## E. Specialised assessment researcher

```text
ROLE: Browser assessment/runtime specialist
TASK: Determine a safe, realistic way to render and assess [specific task type] in the browser.
LEARNER/PROJECT CONTEXT: [target language/API, learner level, target devices/browsers]
SCOPE: Current browser libraries/runtimes, exact APIs, support, maintenance, license, limitations, security.
OUT OF SCOPE: Selecting unrelated dependencies or building the whole app.
INPUTS: [requirements, existing package constraints]
METHOD: Prefer official docs and maintained project sources. Verify current version and exact integration API. Propose the smallest working spike and a fallback.
EVIDENCE RULES: Provide direct URLs, dates, versions, browser support, license, and known limitations. Do not infer compatibility from package names.
OUTPUT FILE/PATH: docs/research/assessment-runtime.md
OUTPUT SCHEMA: Recommended approach; alternatives; minimal dependency set; integration plan; checker strategy; isolation/security; fallback; evidence; unresolved risks.
UNRESOLVED QUESTIONS: List explicitly.
STOP CONDITION: A supported approach or an evidence-backed reason for manual assessment is established.
```

## F. Independent red-team reviewer

```text
ROLE: Independent quality and safety reviewer
TASK: Find defects in the integrated course and application before release.
LEARNER/PROJECT CONTEXT: [brief and acceptance criteria]
SCOPE: Fact-check coverage, lesson sequence, review algorithm, assessment integrity, browser runtime, mandatory Light/Dark themes and theme switcher, system preference detection, theme preference persistence, contrast across routes/visuals, accessibility, security, and run/build flow.
OUT OF SCOPE: Rewriting without reporting evidence; accepting untested claims.
INPUTS: Project files, docs/CLAIM_LEDGER.md, docs/SOURCE_REGISTER.md, docs/QA_REPORT.md.
METHOD: Read references/design-system-and-theming.md. Reproduce key flows where possible. Test a fresh launch under system Light and Dark, all System/Light/Dark choices, persistence, blocked-storage fallback, and switching during an active exercise/visualization. Inspect each major route and renderer in both themes for contrast and state preservation. Inspect code paths and compare claims with cited sources. Try incorrect inputs and failure modes.
EVIDENCE RULES: Every finding needs severity, file/lesson/claim ID, reproduction or rationale, and a suggested fix. Mark untested areas.
OUTPUT FILE/PATH: docs/reviews/red-team-review.md
OUTPUT SCHEMA: Blockers; high; medium; low; untested; release recommendation.
UNRESOLVED QUESTIONS: List explicitly.
STOP CONDITION: Core user journey and all critical risks have been reviewed or clearly marked as blocked.
```

## G. App implementation worker

```text
ROLE: React application implementation worker
TASK: Implement the approved app slice from the canonical specification.
LEARNER/PROJECT CONTEXT: [brief, stack, app architecture]
SCOPE: [specific components/files]
OUT OF SCOPE: Changing course facts, outcomes, or checker semantics without approval.
INPUTS: docs/PROJECT_BRIEF.md, docs/COURSE_MAP.md, schema, exact source files.
METHOD: Read references/design-system-and-theming.md. Implement complete Light/Dark themes and a visible System/Light/Dark selector; detect OS preference on first launch; persist explicit choice where storage works; switch without state loss. Use semantic design tokens and theme every chart/editor/canvas/widget. Keep content data-driven. Implement errors and accessible states. Run relevant tests/build if permitted, including both themes and storage-blocked fallback.
EVIDENCE RULES: Do not claim tests passed unless executed. Do not add dependencies without a decision note.
OUTPUT FILE/PATH: [separate branch/worktree or specified files]
OUTPUT SCHEMA: Files changed; implementation summary; dependencies and rationale; commands run/results; known limitations.
UNRESOLVED QUESTIONS: List explicitly.
STOP CONDITION: Requested slice meets its acceptance criteria and does not break the agreed schema.
```


## H. Visualization implementation researcher

```text
ROLE: Educational visualization implementation research specialist
TASK: Decide whether the exact planned visual should be built with native/custom browser code or an existing library; establish a viable and evidence-backed implementation approach.
LEARNER/PROJECT CONTEXT: [only subject, outcome, and necessary level/context]
SCOPE: [exact visual family, required interactions, target browsers/devices, React/toolchain, offline and file:// single-file constraints]
OUT OF SCOPE: Whole-course research, unrelated visual tools, app implementation, spawning other agents.
INPUTS: [lesson manifest entry, current app stack, existing dependencies, references/visualization-tool-selection.md, relevant URLs/files]
METHOD: Classify complexity; compare native/custom and two or three suitable packages when appropriate; inspect primary docs, exact API/version, licence, maintenance, security, accessibility, browser support, offline/file:// feasibility, and runtime/bundle cost. Propose a minimal packaged proof-of-feasibility spike for complex tools.
EVIDENCE RULES: Preserve exact source URLs, dates, versions, licence, and caveats. Distinguish verified facts, estimates, and unknowns. Do not infer file:// support from dev-server/HTTP success.
OUTPUT FILE/PATH: docs/research/visualization-[family].md
OUTPUT SCHEMA: Use the output contract in .opencode/agents/learnifying-visualization-specialist.md and the decision template in references/visualization-tool-selection.md.
UNRESOLVED QUESTIONS: List explicitly.
STOP CONDITION: A smallest-reliable approach is defensible, or a specific verification blocker and safe fallback are documented.
```
