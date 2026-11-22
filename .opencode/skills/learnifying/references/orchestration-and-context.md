# Orchestration and Context Management

Internal operating document. Write plans and agent instructions in English. Do not expose hidden chain-of-thought to the learner.

## 1. Orchestrator responsibilities

The lead agent is the single owner of:
- learner brief and assumptions;
- task decomposition and dependency order;
- canonical course specification and evidence ledger;
- acceptance criteria and integration decisions;
- final quality gate and user handover.

Workers are specialists, not decision owners. The lead agent resolves disagreements and checks outputs against the brief.

## 2. Capability discovery

For OpenCode, read `opencode-integration.md` and use the documented native `subagent` tool. Reusable worker profiles are provided in `.opencode/agents/`; their IDs are the filenames without `.md`. Agent profiles do not pin a model, so they inherit the model selected for the parent session unless the user configures otherwise.


Before delegation:
1. Inspect available tools/instructions for a documented subagent or task-delegation capability.
2. Determine whether workers share a filesystem, can browse, can run code, and can return files.
3. Use only documented capabilities. Do not guess a tool name or fabricate worker results.
4. If no subagents are available, simulate the roles as sequential bounded passes; do not describe those passes as independent agents.

## 3. Recommended roles

OpenCode worker profiles provided by this package: `learnifying-researcher`, `learnifying-curriculum-reviewer`, `learnifying-assessment-specialist`, `learnifying-app-implementer`, and `learnifying-auditor`. Use the role descriptions below to select only the agents needed for the current phase.


Use only roles that add value to the subject. Usually 2–4 concurrent work packages are enough.

| Role | Owns | Must not do |
|---|---|---|
| Research scout | Evidence for one bounded subject area; source/claim ledger entries | Design the whole course or assert unsupported facts |
| Attachment analyst | Map user files to concepts, outcomes, gaps, and possible outdated material | Treat every uploaded statement as current truth |
| Curriculum architect | Outcomes, prerequisites, pacing, lesson map, review schedule | Write unsupported subject facts or implement UI |
| Assessment specialist | Exercise formats, browser execution/checking options, rubrics | Call an exercise auto-checked without a runnable checker |
| App builder | Implement agreed course schema and UX | Change learning outcomes or invent lesson content silently |
| Independent reviewer | Find factual, pedagogical, accessibility, security, and runtime defects | Rewrite the project wholesale without reporting findings |

A single agent may own more than one role if capacity is limited, but keep the passes separate and maintain the same output contracts.

## 4. Work decomposition

Decompose by independent subject modules or questions, not by arbitrary word count. Each research task should answer a finite set of questions and stop when its scope is covered or sources become unavailable.

Good work packages:
- “Verify the current WebGL2 shader compilation workflow in browsers and identify supported test strategies.”
- “Map the supplied chapters 2–4 to beginner learning outcomes; flag any version-specific claims.”
- “Review whether the proposed 8-week schedule provides enough retrieval practice and a smooth difficulty ramp.”

Bad work packages:
- “Research everything about programming.”
- “Build the entire course and app.”
- “Make sure all facts are 100% true.”

## 5. Context budget rules

- Reserve enough context for final integration and QA; do not let research consume the whole window.
- Aim to keep each handoff to a compact brief (roughly 300–700 words) plus links/paths to durable files. Adjust for model/context limits.
- Do not paste entire uploaded books, long web pages, logs, or transcripts into every agent prompt. Extract relevant sections and keep source paths/URLs.
- Store long-lived knowledge in files such as `docs/PROJECT_BRIEF.md`, `docs/COURSE_MAP.md`, `docs/CLAIM_LEDGER.md`, `docs/SOURCE_REGISTER.md`, `docs/DECISIONS.md`, and structured course data.
- Keep each lesson in a separate data object/file or small batch so the agent can author and review lessons without loading the entire course.
- Use one canonical schema. Do not let agents invent incompatible JSON shapes.
- Summarise only after preserving source references and relevant details. Summaries are not replacements for evidence.
- Before context compaction or handoff, write a checkpoint containing: current phase, decisions, completed files, unresolved questions, risks, next exact action, and acceptance criteria.

## 6. Required delegation packet

Every worker prompt must contain:

```text
ROLE:
TASK:
LEARNER/PROJECT CONTEXT: (only the facts needed for this task)
SCOPE:
OUT OF SCOPE:
INPUTS: (file paths, URLs, exact sections)
METHOD:
EVIDENCE RULES:
OUTPUT FILE/PATH:
OUTPUT SCHEMA:
UNRESOLVED QUESTIONS:
STOP CONDITION:
```

Keep the worker's planning and report in English. Any learner-facing sample text must be in Russian.

## 7. Research worker output schema

Each worker returns a Markdown file using this structure:

```markdown
# Work package: <short name>
## Scope and date
- Scope:
- Checked on (ISO date):
- Coverage:
## Findings
- Finding ID:
- Statement:
- Status: verified / partially verified / conflicting / unverified
- Evidence: exact source URL, title, publisher, version/publication date, relevant section
- Why this source is suitable:
- Caveat:
## Recommendations
## Conflicts and unresolved questions
## Suggested lesson/outcome mapping
## Sources
```

Workers must quote sparingly, paraphrase, and retain URLs. Search snippets alone are not evidence. For fast-changing APIs, identify the exact version and browser/runtime conditions.

## 8. Merge and review

1. The lead agent reads each worker output and checks that it answers the assigned question.
2. Remove duplicate claims, preserve distinct evidence, and reconcile naming/version mismatches.
3. Re-open the most important primary sources independently, especially for high-impact or volatile claims.
4. Record accepted decisions in `DECISIONS.md`; record unresolved disagreements in the claim ledger.
5. Never average conflicting facts. Resolve by source authority, version applicability, and date; otherwise label the conflict.
6. Ask an independent reviewer to audit the integrated result, not just the individual worker outputs.

## 9. OpenCode-specific execution rules

- Use the native `subagent` tool, not a guessed `Task`, `spawn`, or shell-based substitute.
- Child agents run in fresh child sessions and can return reports over multiple rounds. Treat a worker as complete only after its report is received and checked.
- The orchestrator must send a finite context packet and a stop condition. Never assume the child has automatically loaded the full skill or reference files; include the exact paths it must read.
- Do not pin a model in the packaged worker definitions. Let each worker inherit the parent model unless the user explicitly configures a different model.
- The main agent remains responsible for source verification, integration, and user-facing claims.

## 10. Failure fallback

If delegation fails, time is short, or workers return low-quality output:
- reduce parallelism;
- narrow the scope to the course's learning outcomes;
- prioritise high-impact and fast-changing claims;
- proceed sequentially with short, saved checkpoints;
- disclose any reduced research coverage.

Do not compensate for weak subagents by adding huge prompts. Use stricter schemas, smaller scopes, and independent verification.
