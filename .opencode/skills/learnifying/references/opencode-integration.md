# OpenCode Integration

## 1. Native skill layout

The package is designed for OpenCode's current directory-based skill discovery:

```text
.opencode/
  skills/
    learnifying/
      SKILL.md
      references/
        ...
  agents/
    learnifying-researcher.md
    learnifying-curriculum-reviewer.md
    learnifying-assessment-specialist.md
    learnifying-app-implementer.md
    learnifying-auditor.md
```

The skill ID is `learnifying`, because the directory is `.opencode/skills/learnifying/`. The frontmatter `name` is only a display label. The skill can be explicitly loaded with `@learnifying`; OpenCode may also advertise it automatically based on its description and the current task.

OpenCode reference pages:
- Skills: https://opencode.ai/docs/skills
- Agents: https://opencode.ai/docs/agents/

Check these official pages again if the platform behaviour changes.

## 2. Install in a project

Unzip this package at the root of the target repository. It adds the `.opencode/skills/learnifying/` and `.opencode/agents/` directories. It does not overwrite an existing `opencode.json`/`opencode.jsonc` or unrelated agent definitions.

Then start OpenCode in that repository and invoke the skill explicitly:

```text
@learnifying
I want to learn [topic] in [timeframe]. I can study [time budget].
Please inspect the attached materials and build the course app.
```

The skill is also discoverable by description when the user's request matches, provided the selected agent has permission to load skills.

## 3. Install globally

Copy the folder `learnifying` from `.opencode/skills/` to:

```text
~/.config/opencode/skills/learnifying/
```

Copy the five files from `.opencode/agents/` to:

```text
~/.config/opencode/agents/
```

Global skills and agents are then available across projects. Keep the skill's `references/` folder beside its `SKILL.md`; references use relative paths from that skill directory.

## 4. Subagent strategy

The package defines five reusable OpenCode subagents:

- `learnifying-researcher` — one bounded subject research package or analysis of supplied learning materials.
- `learnifying-curriculum-reviewer` — independent review of prerequisites, workload, sequencing, difficulty, and spaced retrieval.
- `learnifying-assessment-specialist` — research of browser-based renderers, runtimes, and reliable exercise checkers for a specific task type.
- `learnifying-app-implementer` — implementation of one approved, isolated app slice against the canonical schema.
- `learnifying-auditor` — independent pre-release audit of evidence, pedagogy, UX, runtime, accessibility, and security.

Use OpenCode's documented native `subagent` tool. Do not invent a tool name or claim delegation occurred unless the subagent call succeeded.

The agent profiles intentionally omit a `model` field. OpenCode therefore uses the selected parent-session model unless the user configures a different model. This avoids hard-coding a provider/model that may not exist in the user's environment.

Use separate child sessions for bounded tasks. Each child receives a fresh context, so send only a compact task packet, the necessary file paths/URLs, the relevant course schema, and an explicit output contract. Do not copy the entire parent conversation or all course materials into every task.

Recommended staging:

1. **Research wave:** use 1–3 researcher instances for independent subject slices and/or supplied-material mapping; use the assessment specialist only if the task requires a specialised browser runtime.
2. **Curriculum gate:** after research findings are consolidated, ask the curriculum reviewer to audit the course map and workload.
3. **Build wave:** after the canonical schema and scope are fixed, use the app implementer for one isolated feature or component set. Never assign overlapping file ownership to parallel implementers.
4. **Release gate:** after integration, ask the auditor to review the actual project and the evidence/QA ledgers.

Do not run every role for every trivial course. Usually 2–4 workers in a wave are enough. The auditor should review the integrated result, not run in parallel with implementation of the same files.

## 5. Context discipline for weaker models

- Keep the parent agent as the only decision owner. Workers return evidence and bounded recommendations, not a new master plan.
- Give each task one goal, finite questions, exclusions, and a stop condition.
- Aim for a task packet of roughly 300–700 words; shorter is better when context is tight.
- Ask for concise reports with exact URLs, versions, dates, source sections, and uncertainty labels. A claim without its evidence trail is not accepted.
- Persist decisions and long-lived findings in project files such as `docs/PROJECT_BRIEF.md`, `docs/COURSE_MAP.md`, `docs/CLAIM_LEDGER.md`, `docs/SOURCE_REGISTER.md`, `docs/DECISIONS.md`, and `docs/QA_REPORT.md`.
- For a large course, store each lesson and exercise as separate structured data or small batches; never load the entire course into each worker.
- Before context compaction or switching phase, write a checkpoint with: phase, completed artifacts, decisions, unresolved questions, risks, next exact action, and acceptance criteria.
- If a worker cannot write to the shared workspace, have it return the complete concise report; the parent then persists the approved result.
- Independently verify important worker findings. Delegation does not transfer accountability.

## 6. Fallbacks

If custom agents are unavailable or disabled, use OpenCode's built-in `explore` for read-only repository inspection and `general` for bounded multi-step tasks when permitted. Otherwise perform the same roles sequentially in the parent session, saving a checkpoint between roles. Never describe sequential internal passes as independent subagents.

If the selected agent cannot load the skill, inspect its skill permissions and the OpenCode skill ID/path. If custom agents cannot be invoked, inspect its `subagent` permissions. Do not modify the user's global or project config without permission.

## 7. Security and ownership

- The orchestrator retains final ownership of course facts, content, app integration, and release claims.
- Do not let several workers edit the same files concurrently.
- Do not grant broader tool permissions than needed. Agent frontmatter here intentionally avoids a hard-coded permission policy; the user's OpenCode security configuration remains authoritative.
- Never ask a research agent to execute learner code, or an implementation agent to silently change evidence-backed teaching claims.
- Do not assume child agents share files unless confirmed by the environment; verify every created artifact before referencing it.
