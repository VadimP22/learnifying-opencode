# Exercise Runtime and Browser Assessment

## 1. Choose the assessment that matches the skill

For every exercise, decide whether success is best judged by:
- exact answer / numeric tolerance;
- multiple choice or classification;
- written explanation with rubric;
- code unit tests;
- compilation/type checking;
- visual rendering or interaction;
- simulation/experiment result;
- project rubric and reflection.

Do not force every subject into a text input and “correct/incorrect” response.

## 2. Assessment contract

Each exercise must define:
- ID and learning outcome(s);
- learner-facing prompt in Russian;
- input format and constraints;
- expected output or rubric;
- hints that reveal progressively more information;
- deterministic checker specification, or a manual-check label;
- pass criteria and tolerances;
- specific feedback for common wrong answers;
- retry/remediation behaviour;
- whether the exercise is formative, summative, or review.

Separate the content from checker code. Use a registry of trusted checker adapters keyed by a known exercise type. Never allow course JSON or imported content to inject arbitrary executable checker code.

## 3. Assessment quality

- Unit tests should test the intended concept, not incidental formatting, unless formatting is the skill.
- Include edge cases and negative cases.
- Avoid a checker that reveals the answer through its error messages.
- For numeric tasks, define units, precision, rounding, and tolerance.
- For open-ended responses, use a transparent rubric and examples of acceptable answers; do not pretend keyword matching is semantic understanding.
- For code tasks, test behaviour and constraints, not only string equality.
- Provide a model solution after a suitable attempt or when the learner requests it; distinguish solution from feedback.

## 4. Browser execution and isolation

When executing learner-supplied code:
- do not execute it in the trusted React app context;
- prefer a Worker for pure computation or a sandboxed iframe for DOM/rendering tasks;
- set execution timeouts and terminate runaway workers;
- constrain memory and external network access where possible;
- use a narrow `postMessage` protocol with origin/source validation;
- limit output size;
- never expose parent application state or secrets;
- clearly explain when the browser cannot safely support a task.

For high-risk or untrusted code, use a server-side sandbox only if an approved backend/tool exists and the data flow has been explained. Do not build an unsafe server execution endpoint as a shortcut.

## 5. Specialised domains

Research current browser-capable libraries and choose by the task, not by habit. Examples of possible approaches (not automatic endorsements; verify current APIs, compatibility, license, and support before use):

- **GLSL/WebGL shaders:** a code editor such as CodeMirror or Monaco; a WebGL/WebGL2 canvas or Three.js `ShaderMaterial` for live rendering; browser shader compilation/linking for syntax and compile feedback; visual test scenes and controlled uniforms for behavioural tasks. Check the exact current Three.js/WebGL APIs and target-browser support. Do not assume a shader rendering library also provides meaningful semantic grading.
- **WGSL/WebGPU:** use an actual WebGPU-capable runtime and feature-detect support. Check browser availability and current API documentation; provide a fallback lesson or non-rendering task where unsupported.
- **JavaScript/TypeScript:** a Worker or isolated iframe for execution, with unit tests and timeouts; use current compiler/type-check tooling only when necessary.
- **Python:** a browser Python runtime such as a WebAssembly-based interpreter may be suitable; verify current support, package constraints, memory cost, and startup time. Otherwise use an explicit manual or external-runner workflow.
- **SQL:** an in-browser SQLite/WebAssembly engine can check queries against a seeded database; ensure the exercise dialect is explicit and matches the runtime.
- **Mathematics:** exact/numeric evaluators, symbolic algebra, graphing, or geometry libraries may help; verify domain restrictions and precision. Keep derivations/rubrics for proof and reasoning tasks.
- **3D/visual design:** browser rendering/scene libraries can provide interactive tasks; use objective geometry/state checks where feasible and a rubric for aesthetic decisions.

The list is illustrative. Do not install all of these libraries. For a given course, choose the smallest reliable toolset.

## 6. Shader-specific implementation checklist

If the learner wants to study shaders:
1. Ask or infer target: GLSL ES/WebGL1, GLSL ES 3.00/WebGL2, WGSL/WebGPU, or a specific engine's shader language. Do not mix them silently.
2. Verify current target browser/device support and the chosen engine/library's exact shader API.
3. Provide a preview canvas with a known-good starter shader and clearly separated vertex/fragment (or WGSL) code as appropriate.
4. Compile using the real graphics API/runtime and capture compile/link diagnostics. Keep renderer logs distinct from educational feedback.
5. Provide uniform controls (e.g. time, resolution, mouse position) when useful, with deterministic reset values.
6. Add practical tests: shader compiles; output is non-empty; expected colour/shape/property appears under defined test conditions; visual regression checks only when stable and meaningful.
7. Explain limitations: visual similarity checks can be brittle across GPUs, drivers, colour spaces, and browser implementations. Do not label subjective visual quality as objectively proven.
8. Add a no-WebGL/WebGPU fallback: code reading, pseudocode, screenshots, or a manual test plan.
9. Keep user code isolated and provide reset/recovery controls.

## 7. External services

Use an external service only when local browser tools cannot reasonably accomplish the task. Before using it:
- verify current availability, pricing/limits, privacy terms, and required credentials;
- explain what code or personal data is transmitted;
- never embed private API keys in the client;
- ask for consent if data leaves the browser;
- provide a fallback when the service is unavailable.

## 8. Manual assessment fallback

When automatic evaluation is not reliable, provide:
- explicit rubric (criteria and levels);
- example of a strong answer/product;
- self-review checklist;
- peer/mentor review option where useful;
- a transparent label such as “Самопроверка по критериям” rather than “Автопроверка”.
