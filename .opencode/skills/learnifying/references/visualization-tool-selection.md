# Visualization Implementation Research and Selection Protocol

## Purpose

Before implementing a visual explanation, Learnifying must choose deliberately between:

1. a bespoke implementation using browser-native capabilities (HTML/CSS/SVG/Canvas/WebGL/WebGPU and a small React component); or
2. an existing library, renderer, engine, simulator, or domain-specific tool.

Do not default to either hand-coding or adding a dependency. Choose the least complex approach that can teach the concept accurately, interactively where useful, accessibly, safely, and within the release constraints.

The learner-facing deliverable is normally a self-contained `index.html` opened directly from disk (`file://`). This is a first-class selection constraint, not a final packaging detail.

## 1. Separate the teaching decision from the implementation decision

For each planned visual, first state:

- the concept and learning outcome it serves;
- what the learner should notice, compare, manipulate, or infer;
- whether it should be static, animated, interactive, or a live technical preview;
- the minimum functionality required;
- its accuracy and assessment requirements;
- the supported learner devices/browsers and offline/file-based constraints.

Only after the teaching purpose is clear should implementation options be compared. First inspect the existing app stack/dependencies and the native browser primitives that could meet the requirement. Even for Tier 0, make and record an explicit native/custom-vs-library decision; a brief inspection is enough and an external package search is normally unnecessary. For Tier 1/2, investigate current libraries when they could materially improve correctness, complexity, accessibility, reliability, or performance. Never choose a popular library first and invent a reason to use it afterwards.

## 2. Classify the implementation complexity

Use this practical scale; it is a decision aid, not a rigid score.

### Tier 0 — Simple visual

Examples: a labelled concept map, a small flowchart, a short timeline, a simple geometric sketch, a few annotated shapes, a static sequence of steps, or a small chart with a handful of values and no advanced interaction.

Default: implement with semantic HTML, CSS, inline SVG, or a small pure React component. Avoid adding a dependency unless the project already has a suitable one or a clear accessibility/maintenance benefit outweighs the cost.

A hand-built SVG is often preferable to a charting package for a small, fixed, pedagogical diagram. Keep it data-driven where that improves reuse, but do not build a generic charting framework for one illustration.

### Tier 1 — Bounded interactive visual

Examples: one or two sliders changing a simple model, a resettable step-through algorithm, a small state machine, a modest coordinate plot, a limited before/after comparison, or a compact interactive diagram.

Default: compare a small custom React component using native browser primitives against any already-installed library. A custom implementation is appropriate when the state model and rendering logic are small, deterministic, testable, and easy to explain. Prefer a library if it significantly reduces complexity, provides robust accessibility/interactions, or avoids reimplementing difficult domain behaviour.

### Tier 2 — Specialised or technically complex visual

Examples: shader editors/renderers, 3D scenes, physics or chemistry simulations, complex graph/network layouts, advanced mathematical plotting, waveform/audio tools, circuit simulators, CAD-like manipulation, geospatial maps, large interactive datasets, or complex time-dependent models.

Required: perform current tool/library research before implementation. Use the `learnifying-visualization-specialist` subagent when available, unless the same bounded investigation is already being performed by another specialist (for example, the assessment specialist researching the exact same runtime). Compare viable approaches and select based on evidence, not popularity.

Do not hand-roll a domain engine when a suitable, maintained library can safely provide the core rendering or simulation capability. Custom code may still be appropriate for the pedagogical model, UI controls, annotations, adapters, or a small domain-specific layer around the engine.

## 3. The custom-versus-library decision

Evaluate both paths against the actual requirements.

### Prefer a custom implementation when

- the visual is small and narrowly scoped;
- browser-native SVG/Canvas/DOM can represent it clearly;
- the state and rendering logic are straightforward and deterministic;
- there is no meaningful need for a domain engine or advanced interaction model;
- custom code is likely to be smaller and easier to validate than a dependency;
- keyboard access, labels, reduced motion, and mobile behaviour can be implemented reliably;
- the result can be embedded and tested in the single-file release.

### Prefer an existing library when

- the visual requires a non-trivial rendering engine, domain model, parser/compiler, layout algorithm, numerical method, interaction system, or device abstraction;
- implementing the required behaviour manually would be error-prone or consume more code than a suitable library;
- a maintained library provides tested functionality, accessibility, performance, or cross-browser handling that would be costly to reproduce;
- the library's licence, security posture, API, browser support, and packaging model are acceptable;
- a minimal integration spike confirms the required features work in the actual release environment.

### Avoid a library when

- it is merely fashionable or visually impressive but adds no teaching value;
- the required feature is only a small static diagram;
- the package is abandoned, poorly documented, incompatible, insecure, or has an unsuitable licence;
- it requires a server, remote CDN, account, API key, or network dependency that the learner did not agree to;
- it cannot function in the intended single-file `file://` app and no acceptable fallback exists;
- its bundle/runtime cost, complexity, or accessibility limitations outweigh its benefits.

## 4. Research procedure for Tier 2 and uncertain Tier 1 cases

Search the web using the tools actually available. Prefer primary evidence in this order:

1. Official documentation for the exact feature/API and supported versions.
2. Official repository, release notes, issue tracker, and maintainer guidance.
3. Package registry metadata for current version, dependency tree, and licence declaration.
4. Security advisories and browser compatibility references.
5. Independent technical material only to clarify trade-offs, not to replace primary evidence.

Compare two or three plausible candidates when more than one exists. Do not pad the comparison with irrelevant alternatives. If no library is justified, document why a native/custom solution is better.

Verify the following, to the extent applicable:

- exact current version and release/activity status;
- documented APIs for the required capability (not just a package description);
- maintenance signals: recent releases, issue handling, compatibility policy, maintainer status;
- licence text and any attribution/redistribution obligations;
- security advisories and risky transitive dependencies;
- browser/device support, including the likely learner target;
- React integration and compatibility with the chosen React/toolchain versions;
- offline operation and whether assets are fetched remotely;
- single-file packaging and `file://` constraints;
- use of dynamic imports, workers, WASM, external assets, fonts, or network fetches;
- keyboard support, focus management, semantic labels, screen-reader behaviour, reduced-motion support, and mobile/touch interactions;
- approximate bundle/runtime cost and startup/performance implications;
- fallback behaviour when WebGL/WebGPU, storage, workers, or other APIs are unavailable.

For `file://` compatibility, do not rely on general browser-support statements. Build a minimal isolated spike that exercises the critical feature and package it using the proposed final single-file strategy. Open the exact spike from disk in the target browser. A dev-server preview or a successful HTTP preview is insufficient evidence.

If a critical capability cannot be tested in the available environment, label it unverified and do not present it as supported. Choose a lower-risk fallback or clearly disclose that the feature needs a local/remote server.

## 5. Decision matrix

Use this matrix to guide, not mechanically automate, the decision:

| Criterion | Native/custom approach | Existing library |
|---|---|---|
| Small static diagram | Usually best | Usually unnecessary |
| Small, deterministic interaction | Often best | Consider if it removes meaningful complexity |
| Complex domain rendering/simulation | Often expensive/risky to build | Usually investigate first |
| Accessibility requirements | Must be implemented and tested | Verify actual library support; do not assume |
| `file://` single-file target | Often straightforward for DOM/SVG; still test | Must verify dynamic assets/workers/WASM/imports |
| Maintenance burden | Owned by this app | Shared with maintainers; verify project health |
| Bundle size | Can be very small | Measure actual production contribution |
| Accuracy | Depends on our model and tests | Depends on library semantics plus our model/adaptation |

A library is not automatically more correct. The domain assumptions, units, coordinate systems, numerical precision, and educational simplifications still need independent validation.

## 6. Minimal proof-of-feasibility spike

Before integrating a Tier 2 dependency:

1. Create a tiny isolated reproduction of the required visual capability.
2. Pin the candidate version and record its licence.
3. Exercise the essential interaction/rendering path, not just import the package.
4. Confirm expected output and at least one failure/unsupported-device path.
5. Bundle it using the intended single-file release process.
6. Open the result directly with `file://` in the target browser.
7. Record the exact commands, browser/version, result, and limitations.

Do not build the whole course on an unproven runtime. If the spike fails, try a different implementation or document the need for an explicitly approved server-dependent feature.

## 7. Record the decision

Persist decisions in `docs/VISUAL_IMPLEMENTATION_DECISIONS.md`. Do not leave the rationale only in chat or in a subagent report.

Use one entry per visual family or technically distinct renderer, not one entry for every repeated copy of the same component.

```markdown
# Visual implementation decision: <ID / family>
- Date checked (ISO):
- Lesson/concept/outcome IDs:
- Teaching purpose:
- Visual type and interaction:
- Complexity tier: 0 / 1 / 2
- Requirements and target browser/device:
- Options considered: custom/native; [candidate libraries]
- Selected approach:
- Why this is the smallest reliable option:
- Exact package/version (if any):
- Official API/docs and evidence URLs:
- Licence:
- Maintenance/security findings:
- Accessibility and mobile findings:
- Offline / single-file / `file://` findings:
- Bundle/runtime impact (measured or clearly marked estimate):
- Proof-of-feasibility commands and results:
- Known limitations and fallback:
- Unverified items:
```

For Tier 0, a compact record in the lesson manifest is enough; do not create unnecessary research paperwork. For Tier 2, the decision record and evidence are mandatory.

## 8. Context-efficient delegation

Use a specialist subagent only when the choice is genuinely non-trivial: Tier 2, uncertain Tier 1, multiple candidate libraries, browser/API constraints, or a high-risk dependency.

The parent should first create a small visual requirements brief. Send the visual specialist only:

- relevant subject and learner outcome;
- the exact visual(s) and must-have interactions;
- target browser/device and offline/`file://` constraints;
- current app stack and already-installed dependencies;
- exact relevant source/reference paths;
- questions to answer and output path/schema.

Do not send the entire course, all attachments, or the whole conversation. Ask for a concise recommendation and a durable evidence report, normally no more than about 800 words excluding source URLs/tables. Ask the specialist to stop when a defensible choice is established; it must not design the whole course or implement the app.

Avoid duplicate research. If the assessment specialist is already testing the same library/runtime for both rendering and exercise checking, combine those bounded questions into one work package and record both uses. The parent remains responsible for the final decision and independent verification of critical claims.

If subagents are unavailable, run this as one bounded research pass in the parent session and save the same decision record.

## 9. Implementation handoff

Only after the choice is recorded:

- implement the selected approach against the visual manifest;
- wrap third-party tools behind small app-owned components/adapters so course content is not coupled to vendor APIs;
- keep explanatory model parameters, units, equations, and expected behaviours explicit and testable;
- never execute untrusted learner code in the trusted app origin;
- provide a static/text fallback for critical learning information;
- record dependency versions in the lockfile and decision record;
- measure actual production bundle contribution when feasible;
- run the visual's behavioural tests and the final `file://` release test.

The implementation agent must not silently replace the approved library with another dependency or convert a researched library decision into an unreviewed custom engine. It must report any incompatibility to the orchestrator and request a revised decision.

## 10. Acceptance criteria

A visual implementation is not ready until:

- its teaching purpose and learner outcome are explicit;
- custom-vs-library choice is recorded, with a reason proportionate to complexity;
- all adopted libraries have current-version, licence, maintenance, security, and compatibility checks;
- complex runtime choices have a successful proof-of-feasibility spike or an explicitly disclosed blocker;
- the visual's mathematical/domain behaviour and labels are validated;
- interaction, keyboard/touch access, reduced motion, and fallback behave as specified;
- no unnecessary dependency or remote service was introduced;
- the exact final `index.html` has been tested from disk for that visual, or its limitation is stated honestly.
