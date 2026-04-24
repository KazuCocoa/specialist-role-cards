Sandbox

This is a sandbox for testing out code snippets and ideas. You can use this space to experiment with different programming languages, libraries, and frameworks without affecting your main projects. Feel free to try out new concepts, debug code, or simply play around with coding in a safe environment. Happy coding!

---


# Specialist Role Cards

This repository contains a set of reusable specialist prompt cards under [`.github/prompts/`](/Users/kmatsuo1/github/specialist-role-cards/.github/prompts). Each card defines a focused software-delivery role with:

- metadata for discovery (`name`, `description`, `agent`, `argument-hint`)
- a role definition
- explicit `Do` / `Do not` constraints
- a required output structure
- handoff guidance to the next specialist

These cards are not an application by themselves. They are prompt definitions intended to be discovered and invoked by a host that supports `.prompt.md` files.

## How It Works

Each file in `.github/prompts/` is a role card. In practice, the host tool surfaces the card by name, and the user invokes it with a short task-specific argument.

The repository also includes a machine-readable workflow manifest at [`.github/specialist-workflow.json`](/Users/kmatsuo1/github/specialist-role-cards/.github/specialist-workflow.json), which captures the default entrypoints, language-to-implementation mappings, and post-implementation parallel specialists in one place.

The cards appear to fall into two usage styles:

- `agent`: execution or analysis roles that directly produce a substantial deliverable
- `ask`: clarification, planning, or decision-support roles that help the user refine the next move

This distinction comes from the prompt metadata in this repo. The runtime behavior depends on the host that loads these prompt files.

## Role Catalog

### Framing and Discovery

- `workflow-router-specialist`
  - Use when you are unsure which specialist should run next.
  - Produces: current stage assessment, next specialist, follow-up path, and language-aware routing.
- `goal-enabler-specialist`
  - Use when a request is still vague.
  - Produces: goal summary, constraints, flags, and decisions needed.
- `codebase-explorer-specialist`
  - Use when you need to understand an existing codebase before planning.
  - Produces: relevant files, flow, interfaces, patterns, and risks.
- `decision-support-specialist`
  - Use when there are multiple viable technical options.
  - Produces: option matrix, trade-off summary, decision criteria, and recommendation.

### Planning and Implementation

- `implementation-planner-specialist`
  - Use when a goal is approved and needs to become a spec and task plan.
  - Produces: Part 1 spec (`what`) and Part 2 implementation plan (`how`), including the recommended implementation specialist for the target language.
- `typescript-backend-specialist`
  - Use when implementing or editing a TypeScript backend.
  - Produces: implementation proposal, validation notes, assumptions, and decisions needed.
- `python-backend-specialist`
  - Use when implementing or editing a Python backend.
  - Produces: implementation proposal, validation notes, assumptions, and decisions needed.

### Review and Hardening

- `review-specialist`
  - Use before merge to review diffs, PRs, refactors, or design changes.
  - Produces: verdict, strengths, concerns, concrete suggestions, and review questions.
- `security-specialist`
  - Use for security audits across auth, validation, secrets, trust boundaries, and dependency risk.
  - Produces: verdict, severity-grouped findings, dependency risks, and risk decisions.
- `performance-specialist`
  - Use for slow endpoints, expensive jobs, memory pressure, throughput limits, or resource-efficiency issues.
  - Produces: bottleneck hypothesis, optimizations, measurement plan, trade-offs, and decisions needed for the current backend stack.
- `test-specialist`
  - Use to derive test scenarios and improve confidence in a change.
  - Produces: checklist, preconditions, expected results, and testing gaps.
- `documentation-specialist`
  - Use to write or audit docs against verified behavior.
  - Produces: draft docs or an audit verdict, gaps, and placement guidance.

### Debugging

- `root-cause-analyzer`
  - Use when investigating a bug, incident, or unexpected behavior.
  - Produces: symptom summary, hypothesis, evidence, contributing factors, fix, and verification steps.

## Suggested Workflow

For new feature work:

1. Start with `workflow-router-specialist` if you are unsure which specialist should run next.
2. Start with `goal-enabler-specialist` if the request is not yet concrete.
3. Use `codebase-explorer-specialist` to map the relevant part of the system.
4. Use `implementation-planner-specialist` to create the spec and implementation plan.
5. Implement with the language-matched specialist chosen in the plan, typically `typescript-backend-specialist` or `python-backend-specialist`.
6. Review with `review-specialist`.
7. Run `security-specialist`, `performance-specialist`, `test-specialist`, and `documentation-specialist` to harden the change.

For bug work:

1. Start with `workflow-router-specialist` if the next step is unclear.
2. Start with `root-cause-analyzer`.
3. If the system area is unclear, use `codebase-explorer-specialist`.
4. Implement the fix with the appropriate backend specialist.
5. Review and harden with `review-specialist`, `test-specialist`, `security-specialist`, and `documentation-specialist`.

Use `decision-support-specialist` at any point where trade-offs need to be made explicitly.

## Current Gaps

The repo now includes explicit routing guidance and a workflow manifest, but a few limitations are still worth knowing about:

- The repository still does not include a runtime executor that automatically invokes the next prompt card. Routing is documented and structured here, but the host still needs to execute the selected specialist.
- The language mappings in `.github/specialist-workflow.json` currently cover TypeScript/Node.js and Python backends only.

## Files

- [codebase-explorer-specialist.prompt.md](/Users/kmatsuo1/github/specialist-role-cards/.github/prompts/codebase-explorer-specialist.prompt.md)
- [decision-support-specialist.prompt.md](/Users/kmatsuo1/github/specialist-role-cards/.github/prompts/decision-support-specialist.prompt.md)
- [documentation-specialist.prompt.md](/Users/kmatsuo1/github/specialist-role-cards/.github/prompts/documentation-specialist.prompt.md)
- [goal-enabler-specialist.prompt.md](/Users/kmatsuo1/github/specialist-role-cards/.github/prompts/goal-enabler-specialist.prompt.md)
- [implementation-planner-specialist.prompt.md](/Users/kmatsuo1/github/specialist-role-cards/.github/prompts/implementation-planner-specialist.prompt.md)
- [performance-specialist.prompt.md](/Users/kmatsuo1/github/specialist-role-cards/.github/prompts/performance-specialist.prompt.md)
- [python-backend-specialist.prompt.md](/Users/kmatsuo1/github/specialist-role-cards/.github/prompts/python-backend-specialist.prompt.md)
- [review-specialist.prompt.md](/Users/kmatsuo1/github/specialist-role-cards/.github/prompts/review-specialist.prompt.md)
- [root-cause-analyzer.prompt.md](/Users/kmatsuo1/github/specialist-role-cards/.github/prompts/root-cause-analyzer.prompt.md)
- [security-specialist.prompt.md](/Users/kmatsuo1/github/specialist-role-cards/.github/prompts/security-specialist.prompt.md)
- [test-specialist.prompt.md](/Users/kmatsuo1/github/specialist-role-cards/.github/prompts/test-specialist.prompt.md)
- [typescript-backend-specialist.prompt.md](/Users/kmatsuo1/github/specialist-role-cards/.github/prompts/typescript-backend-specialist.prompt.md)
- [workflow-router-specialist.prompt.md](/Users/kmatsuo1/github/specialist-role-cards/.github/prompts/workflow-router-specialist.prompt.md)
