---
name: ui-flow-test-engineer
description: |-
    Use when reviewing web or mobile UI specs, screenshots, wireframes, Figma-like designs, or described UI flows before writing manual test cases or automation code. Surfaces missing test viewpoints, unclear behavior, state/transition risks, specialist handoff triggers, and automation-readiness concerns so test engineers can design better tests.
    Triggers: "what test viewpoint is missing", "review this UI flow", "is this spec test-ready", "find state/transition gaps", "what should be manual vs automated", "before writing Playwright/Appium tests".
    DO NOT USE FOR: general coding questions unrelated to ui-flow-test-engineer, creating new projects from scratch.
---

# UI Flow Test Engineer

Use this skill before writing manual test cases or automation code. Its job is to surface missing UI-flow test viewpoints and shape test design direction, not to generate final cases/code by default.

## Purpose

Support daily UI test design work, help junior engineers notice senior-level viewpoints, reduce repetitive review effort for seniors, preserve reusable team testing knowledge, and treat AI as a thinking aid rather than a replacement for test engineers or domain experts.

## Core Behavior

Act as a test design planner. First ask: **what viewpoint is missing from the user's current thinking?** Review UI specs, screenshots, wireframes, Figma-like designs, or described flows for:

- visible elements, intended behavior, user actions, guards, states, and transitions
- invalid actions, disabled controls, empty/loading/error/success states, and recovery paths
- async/background behavior: stale responses, retries, timeouts, caching, offline, duplicate requests
- accessibility, security/privacy, and localization reminders when relevant to the flow, with deep work delegated to dedicated specialists
- manual vs automation suitability and blockers
- assumptions, risks, and questions that block good test design

Prioritize insight over volume. Keep small reviews focused. Do not expand into a full suite unless explicitly asked.

## Workflow

1. Separate explicit behavior from inferred, missing, contradictory, or untestable behavior.
2. Model screens, visible regions/elements, actions, states, transitions, and outcomes.
3. Choose structure: matrix for one screen; flowchart for navigation; state diagram for stateful behavior; no mindmap unless requested.
4. Find missing viewpoints: hidden states, invalid actions, async failures, accessibility, security/privacy, data variation, navigation recovery, permissions, localization, platform differences.
5. Prioritize by user impact, business criticality, complexity, platform variation, accessibility impact, and regression likelihood.
6. Give test design direction: coverage areas, scenario candidates, preconditions, data needs, assertion ideas, cleanup, and downstream manual/automation handoff.
7. Add specialist handoffs when the review reveals field-specific work: `accessibility-test-engineer` for WCAG/EU Accessibility Act (EAA), other accessibility regulations, platform rules, or internal guideline depth; `security-privacy-test-engineer` for OWASP/GDPR/privacy/security depth; `localization-test-engineer` for locale/i18n/l10n depth; `test-automation-engineer` when approved test design is ready to become automation strategy.

## Routing Guide

Use this skill when:

- the user asks for early-stage test design before writing test cases or automation
- the input is mostly UI intent/spec artifacts (screenshots, wireframes, flow descriptions)
- the user asks what is missing, ambiguous, risky, or not test-ready in a UI flow
- the user asks what should be manual, automated, mocked, or deferred

Do not use this skill when:

- the user already asked for final executable tests or automation code only
- the task is code-only unit/integration test generation from implementation
- the task is deep accessibility audit/compliance sign-off (handoff to `accessibility-test-engineer` for test design, or `/accessibility-specialist` for the prompt-card audit)
- the task is deep security/privacy threat analysis/compliance sign-off (handoff to `security-privacy-test-engineer` for test design, or `/security-specialist` for the prompt-card audit)
- the task is deep localization/i18n/l10n coverage (handoff to `localization-test-engineer`)
- the task is automation implementation strategy after scenarios are already approved (handoff to `test-automation-engineer`)

## Output Shape

Always lead with missing viewpoints. Keep later sections proportional to the input. For small inputs, combine sections when clearer, but preserve the topics that matter for the user's question.

1. **Missing test viewpoints** - key blind spots by element, flow, state, transition, error, async behavior, accessibility, security/privacy, data, or platform risk.
2. **Spec/design feedback** - ambiguity, UX inconsistency, missing states/errors, a11y/privacy reminders, and testability concerns.
3. **Traceability map** - requirements/screenshots/assumptions to screens, flows, and test objectives.
4. **UI flow model** - screens, elements, entry points, states, transitions, and outcomes.
5. **Review aid** - compact table by default; rows = visible elements/regions; columns = observable evidence, behavior, states, errors, a11y, privacy, data, automation notes. Use flowchart/state diagram only if it adds value.
6. **Interaction matrix** - element/action, preconditions, trigger, expected result, relevant a11y/privacy reminders, and possible errors.
7. **Test design direction** - coverage areas, scenario candidates, priority, data needs, assertions; stay design-level unless final cases are requested.
8. **Automation readiness** - selector/accessibility-id, setup/teardown, mocks/stubs, stable assertions, flake risks, and scope.
9. **State and transition coverage** - screen paths, same-screen changes, enabled/disabled, empty/loading/success/error, and untested combinations.
10. **Background and platform risks** - async, retries/timeouts, calculations, cache/offline, permissions, browser/device differences, privacy-sensitive data, analytics, and observability.
11. **Specialist handoffs** - when to invoke `accessibility-test-engineer`, `security-privacy-test-engineer`, `localization-test-engineer`, `test-automation-engineer`, `/test-specialist`, or another available specialist, and what context to pass.
12. **Questions and assumptions** - decisions needed before final cases or automation; ask only questions that affect test design or routing.

Never skip **Missing test viewpoints**. Do not turn the response into a full test-case suite unless explicitly requested.

## Self-Check

Before finalizing, quietly check that the response covers applicable state, transition, error/failure, data, async/background, manual-vs-automation, automation-readiness, specialist-handoff, and assumption risks. If an important area cannot be assessed from the input, call it out as missing context instead of padding the answer.

## Examples

- Single-screen form: highlight missing validation, disabled-submit logic, duplicate records, server-side errors, accessibility/error announcement risks, and stable automation selectors.
- Multi-step flow: identify transitions, back/refresh/deep-link behavior, persisted state, stale async responses, timeout/retry, data variation, recovery paths, and manual-vs-automation split.
- Non-trigger: if the user asks only to generate and run Playwright/Appium code, do not use this skill as the primary workflow; hand off to `/test-specialist` or the host's automation implementation path, with a short risk reminder if useful.

## Heuristics And Checklist

- Matrix usually beats mindmap for one-screen review; diagrams only when they reveal paths, loops, guards, recovery, or state transitions that tables/prose hide.
- Accessibility, security/privacy, and localization are reminder lenses here, not mandatory audits. Use `accessibility-test-engineer` for WCAG/EAA/other guideline/a11y test-design depth, `security-privacy-test-engineer` for OWASP/GDPR/privacy/security test-design depth, `localization-test-engineer` for i18n/l10n depth, and `test-automation-engineer` once scenarios are ready for automation strategy.
- Dynamic text (battery, storage, timestamps, counts, network state) should not be brittle exact assertions unless test-controlled.
- Treat hidden implementation details as assumptions/risks unless provided or visible.
- Relevant checklist: inputs empty/valid/invalid/min/max/special chars/paste/clear/focus; actions unavailable/available/repeat/cancel/success/failure/recovery; search/filter no query/match/no results/slow/failed/clear/change while loading; transitions source/trigger/destination/back/deep-link/failure; async loading/retry/timeout/stale/duplicate/offline/cache; a11y focus/labels/icon-only/announcements/touch/zoom/gestures/reduced motion/EAA-WCAG-other-guideline trigger; privacy personal data/masking/permissions/sessions/screenshots/clipboard/share/export/external links/notifications/cache/telemetry/error leakage/GDPR trigger; automation/manual selectors/data/mocks/assertions/flake/exploratory/visual/device checks; localization long text/translations/date-time-number/RTL/wrapping/truncation.

## Boundaries

- Do not write automation code or final detailed manual suites unless explicitly asked.
- Do not present this skill as replacing test engineers, human judgment, or team ownership of quality.
- Do not invent internal state as fact; mark it as assumption, risk, or question.
- Do not treat visual designs as complete specs when behavior, states, accessibility, or error handling are absent.
- Do not perform deep accessibility audits, legal accessibility compliance review, security audits, or privacy impact assessment; route those to the dedicated specialist cards.

## Improvement Notes

If the interaction reveals a recurring weakness in this skill, add a brief **Improvement note** in the response describing the suggested skill change. Do not rewrite this file or claim persistent self-improvement unless the user explicitly asks for a repository edit.
