# Research and Fact-Checking Protocol

## 1. Scope and honesty

The objective is high-coverage, traceable, current evidence—not an impossible guarantee of absolute correctness. Never claim “100% accurate”, “100% current”, or “all facts verified”. Report:
- what topics/claims were checked;
- which sources were used;
- source publication/version dates where available;
- the access/check date;
- unresolved, disputed, context-dependent, or unverified claims;
- what would need another check before the learner relies on it.

Use an explicit “Проверено по источникам на: YYYY-MM-DD” note in source documentation. For rapidly changing claims, include the exact version/date/environment.

## 2. Source hierarchy

Prefer, in order (subject to applicability):
1. official standards, specifications, laws, API/reference docs, release notes, project documentation, and primary datasets;
2. peer-reviewed research and original papers;
3. authoritative textbooks and materials from reputable educational/research institutions;
4. maintainer-authored technical explanations and high-quality specialist publications;
5. community discussions for practical edge cases, clearly labelled as anecdotal and corroborated where possible.

Search rankings, snippets, generated summaries, social posts, and AI answers are discovery aids, not sufficient evidence for material claims.

## 3. Research workflow

1. Turn course outcomes into research questions.
2. Classify each question as stable foundational knowledge, version-sensitive technical detail, rapidly changing fact, safety/legal/high-stakes information, or learner-specific material.
3. Search for primary sources and current versions. Prefer official documentation for APIs, commands, browser capabilities, and package behaviour.
4. Open and inspect the source itself. Confirm that it directly supports the statement and applies to the selected version/context.
5. For high-impact or volatile claims, cross-check with a second independent authoritative source when possible. Two pages copying the same source are not independent.
6. Check publication/update/release dates and note when a page has no date.
7. Compare the evidence with user-provided materials. Preserve the distinction between “the supplied material says…” and “the current evidence indicates…”.
8. Record every material fact that affects teaching, assessment, installation, safety, or expected output.
9. Re-check volatile details immediately before finalising the app and again after dependency installation/build if applicable.

## 4. Claim ledger

Create `docs/CLAIM_LEDGER.md` with one row or entry per material claim:

| Field | Meaning |
|---|---|
| Claim ID | Stable identifier, e.g. C-014 |
| Exact claim | The narrow factual statement used in the course/app |
| Course location | Unit/lesson/component that depends on it |
| Status | verified / partially verified / conflicting / outdated / unverified |
| Primary evidence | URL, title, publisher, exact section, version/date |
| Secondary evidence | Independent corroboration if applicable |
| Checked on | ISO date |
| Context | Browser, OS, library version, jurisdiction, assumptions |
| Caveat/action | What remains uncertain or what must be rechecked |

One row should not combine several independently verifiable claims. Split compound statements.

## 5. Source register

Create `docs/SOURCE_REGISTER.md` with:
- source ID;
- title and author/organisation;
- direct URL or uploaded-file path;
- publication/update/version date (or “not stated”);
- date accessed;
- source type and authority rationale;
- relevant chapter/section/page;
- claims and lessons supported;
- caveats or known scope limits.

Cite sources in learner-facing lessons where a learner may need to go deeper or where facts are version-sensitive. Use a small “Источники и дополнительные материалы” section rather than interrupting every sentence.

## 6. User-supplied materials

- Inventory every attachment and preserve its filename.
- Map useful chapters/pages to the course map.
- Note edition, publication date, software version, and apparent freshness.
- Distinguish the user's required syllabus/material from external factual authority.
- If sources conflict, state the disagreement and explain which is more current/applicable; never silently change the user's material.
- If a supplied file is incomplete, unreadable, image-only, or inaccessible, say so.
- Respect copyright: do not reproduce substantial textbook or paid-course passages. Teach the concepts in original wording, use brief quotations only when appropriate, and cite the source.

## 7. What counts as a fact-check

For each claim ask:
- Is the claim precise enough to verify?
- Does the source directly support it, or is it an inference?
- Is this source authoritative for this kind of claim?
- Is its date/version applicable to this course?
- Are there important exceptions, environment differences, or jurisdiction differences?
- Do independent sources agree?
- Is the statement still true at the time the learner will use it?

For software/tooling:
- verify current supported release and installation instructions;
- check API names and examples against the exact documented version;
- check browser/device support;
- check maintenance/last release where relevant;
- inspect license and security posture;
- confirm compatibility with the chosen React/build versions;
- avoid deprecated APIs or clearly label them if teaching legacy material.

For maths/science: independently recompute formulas, units, worked examples, edge cases, and numerical outputs. For legal/medical/financial/safety-related topics, use authoritative jurisdiction-specific sources and conservative caveats; do not present a general course as personalised professional advice.

## 8. Confidence labels

Use clear labels internally and, when useful, in source notes:
- **Verified:** supported by applicable primary evidence; key details checked.
- **Partially verified:** some parts supported, but applicability or completeness remains uncertain.
- **Conflicting:** credible sources disagree or versions differ.
- **Outdated:** evidence is no longer applicable to current use, but may be useful for historical teaching.
- **Unverified:** no adequate evidence found.

Do not convert absence of contradictory search results into verification.

## 9. Release audit

Before release, sample every unit and re-check all high-impact/version-specific claims. Ensure each learner-facing citation points to the actual supporting source. Remove claims that cannot be substantiated, qualify them, or mark them unresolved. State research coverage honestly; do not imply exhaustive verification if only a subset was audited.
