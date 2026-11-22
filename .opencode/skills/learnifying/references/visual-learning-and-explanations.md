# Visual Learning and Explanatory Media Standard

## Purpose

Visual explanations are a core teaching method in Learnifying, not decoration and not a substitute for clear prose. When a concept has a meaningful visual structure, process, spatial relationship, quantitative pattern, or cause-and-effect mechanism, expose that feature visually alongside the Russian-language explanation.

Do not make simplistic claims that every learner is a “visual learner” or that pictures are always better than text. Choose visuals because they make the particular concept easier to inspect, compare, manipulate, remember, or reason about. Keep the explanatory text: name the idea, guide attention to the relevant parts of the visual, and explain what the learner should notice.

## 1. Plan visuals during curriculum design

For every major learning outcome and foundational concept, ask:

1. What is hard to understand from prose alone?
2. What should the learner see: structure, hierarchy, spatial form, sequence, state change, causal relationship, quantitative trend, hidden/internal process, or the effect of a parameter?
3. Which visual form exposes that feature with the least unnecessary complexity?
4. Would interaction materially improve understanding, or would a static visual be clearer?
5. What caption, labels, units, legend, annotation, or guided prompt is needed?
6. What is the fallback if the browser or device cannot render the preferred visual?

Record the decision in the lesson manifest or a visual plan. Include: `conceptId`/outcome, learning purpose, visual type, key labels, source/derivation, interaction model, accessibility requirements, and fallback.

Do not force a visual into a concept when it would be misleading, trivial, or cognitively distracting. In such cases, record briefly why prose, worked examples, audio, physical practice, or another modality is more appropriate.

## 2. Match the visual form to the learning problem

| Learning need | Useful visual forms |
|---|---|
| Parts and relationships | labelled diagrams, concept maps, block diagrams, annotated illustrations |
| Sequence or chronology | timelines, step sequences, flow diagrams, state-transition diagrams |
| Change over time | animation, time-series chart, scrubber with pause/step controls |
| Quantitative relationships | labelled charts, graphs, coordinate plots, parameter sweeps |
| Spatial or geometric reasoning | 2D/3D models, manipulable geometry, cross-sections, camera controls |
| Invisible mechanisms | cutaways, layered diagrams, particle/system simulations, state visualizers |
| Algorithms and computation | traces, memory/state diagrams, step-through execution, variable inspectors |
| Code and creative technical output | live preview, shader canvas, waveform, rendered scene, interactive playground |
| Comparison and classification | side-by-side annotated views, matrices, sorting/grouping demonstrations |
| Cause and effect | interactive controls with visible input/output and a resettable baseline |

Use accurate domain-specific representations. Do not use a chart where the data type is unsuitable, a 3D model merely for spectacle, or an animation that hides important intermediate states.

## 3. Interactive visualizations in theory

When feasible and pedagogically justified, prefer a small interactive explanatory model over a passive image. Good patterns include:

- sliders or toggles that change one meaningful parameter and show the consequence;
- play, pause, step, and reset controls for a process;
- layer/visibility controls to reveal structure progressively;
- drag-to-manipulate diagrams or geometry where manipulation is essential;
- live preview of a concept or code fragment with explanatory annotations;
- comparison controls that show before/after or alternative states.

Interaction must serve an explicit question: “What changes when…?”, “How are these parts connected?”, or “Why does this output differ?”. Avoid interactions that add motor effort without adding insight.

Every interactive model should:
- start in a meaningful, understandable default state;
- explain its controls and what the learner should observe;
- allow reset to the default state;
- expose important state/output in text where practical;
- support keyboard operation and visible focus;
- avoid relying on colour alone;
- respect `prefers-reduced-motion` and offer pause/step controls for non-essential animation;
- provide a static diagram, sequence of frames, or written fallback when the interactive runtime is unavailable;
- avoid requiring network access unless the dependency genuinely needs it and the user has been informed.

## 4. Keep theory and graded practice separate

The theory and practice experiences are distinct pages/routes for each lesson.

**Theory page may contain:** explanatory diagrams, annotated examples, interactive simulations, manipulable models, step-through demonstrations, and ungraded “try changing this parameter and observe” exploration. These activities illustrate and explain the concept; they do not count as completion of the assigned exercise set or as proof of mastery.

**Practice page contains:** assigned questions and tasks, code editors, lab briefs, learner submissions, automatic checks, scoring, exercise hints, remediation, and practice feedback.

A short ungraded observation prompt on a theory page is allowed when it directs attention to the visualization. Do not place the actual graded practice sequence below the theory text as one long scrolling page. Provide clear navigation between the two routes and preserve learner progress when switching.

## 5. Visual quality and cognitive load

- One visual should have one primary teaching purpose.
- Place it near the text that explains it; avoid making the learner search elsewhere for the explanation.
- Use labels, callouts, units, legends, arrows, and consistent notation.
- Remove irrelevant decoration, redundant visual noise, and competing accent colours.
- Reveal complex diagrams progressively only when progressive disclosure helps; do not hide essential relationships behind unexplained controls.
- Do not duplicate every sentence as on-screen text inside a diagram. Keep labels concise and make the prose add explanation, interpretation, and causal reasoning.
- Use consistent visual conventions across the course (the same symbol or colour should retain the same meaning).
- Ensure diagrams and charts remain legible at mobile widths and when zoomed.
- Use authentic screenshots only when the exact interface matters; date/version them when software UIs may change.

## 6. Accuracy and evidence

Visuals are factual claims too. Verify their labels, geometry, data, units, colour mapping, state transitions, equations, and output. For scientific, mathematical, technical, or historical diagrams, keep source/derivation metadata in the course content or project documentation. Do not use an attractive but simplified visual if the simplification creates a misconception; label the model's limits.

For generated illustrations, distinguish conceptual illustration from data-accurate diagram. Never present a generated image as a measured graph, exact schematic, authentic screenshot, or evidence source.

## 7. Choose how to implement each visual before writing it

Pedagogical design and technical implementation selection are separate steps. First define what the learner must see or discover. Then decide whether the visual should be hand-built with browser-native tools or implemented using a third-party library.

- **Simple static visuals** (small diagrams, flowcharts, timelines, basic charts) should normally use HTML/CSS/SVG and a small React component. Avoid a dependency without a clear benefit.
- **Bounded interactions** (a few sliders, toggles, step controls, or a small parameterised model) may be custom-built when state and rendering are simple and testable. Compare suitable libraries when they materially reduce complexity or improve accessibility/reliability.
- **Specialised visuals** (3D scenes, shader rendering, complex plotting, domain simulations, audio/waveforms, large graph layouts, CAD-like interaction, etc.) require current research into existing engines/libraries before attempting to recreate the system manually.

Read `references/visualization-tool-selection.md` before implementation. For complex or uncertain cases, use the `learnifying-visualization-specialist` subagent with a bounded requirements packet. The research must check exact APIs and versions, maintenance, licence, security, browser support, accessibility, offline behaviour, bundle/runtime cost, and compatibility with the single-file `file://` release target. Do not infer file-based compatibility from a dev server or HTTP preview. Record the decision and test a minimal packaged spike before adopting a complex runtime.

The default is the smallest reliable solution, not “always write it yourself” or “always use a library”. Do not research libraries for a trivial native SVG diagram unless there is a concrete reason.

## 8. Suggested data model

A theory block may support a discriminated type such as:

```ts
 type VisualExplanation = {
   id: string;
   type: "diagram" | "chart" | "sequence" | "animation" | "simulation" | "interactive-model" | "live-preview";
   title: string;
   purpose: string;
   caption: string;
   labels?: string[];
   sourceIds?: string[];
   interaction?: {
     controls: Array<{ id: string; label: string; kind: "slider" | "toggle" | "select" | "playback" }>;
     resettable: boolean;
   };
   fallback: { kind: "static" | "steps" | "text"; content: string };
   implementationDecision?: {
     complexityTier: 0 | 1 | 2;
     approach: "native" | "custom-react" | "library";
     rationale: string;
     libraryName?: string;
     libraryVersion?: string;
     decisionRecordId?: string;
   };
   accessibility: { textAlternative: string; keyboardOperable: boolean; reducedMotionSafe: boolean };
 };
```

Adapt the schema to the actual implementation and avoid making fields mandatory when irrelevant. Keep executable code out of untrusted course data; use reviewed components/adapters.

## 9. Acceptance checks

Before release, verify:

- each foundational concept has a useful visual where appropriate, or a documented reason for omission;
- every non-trivial visual has a documented custom-vs-library decision proportionate to its complexity;
- complex library/runtime choices have primary-source research and a `file://` single-file proof-of-feasibility or a documented blocker;
- every visual supports a stated learning outcome and is explained by nearby Russian text;
- labels, units, axes, legends, state transitions, and colour meanings are accurate;
- interactive models respond correctly, reset correctly, and never mark graded work as completed;
- interactive controls work by keyboard and on mobile;
- reduced-motion preferences are respected;
- fallback content is available when rendering or device support fails;
- visual content does not replace the separate practice page or weaken retrieval/assessment;
- the exact final self-contained `index.html` can render the visual from disk (`file://`) in the supported browser, or the limitation is documented honestly.
