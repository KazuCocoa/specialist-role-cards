# Test Design Review vs Test Generation

This repository includes a UI flow test engineer skill because test quality is not only about generating test cases or automation code. Many important testing decisions happen before anything is written.

## Why This Skill Exists

Most generation-oriented testing tools work best when the behavior is already clear. They can produce useful artifacts quickly, but they often inherit the assumptions of the source they generate from.

The UI flow test engineer skill sits earlier in the workflow. Its purpose is to help a test engineer ask:

- What viewpoint am I missing?
- What behavior is ambiguous or absent from the spec?
- Which states, transitions, and error paths are not represented?
- What needs to be clarified before manual cases or automation code are written?
- What should be manual, automated, mocked, or deferred?

This is a test design thinking aid, not a replacement for test engineers.

## Earlier-Stage Focus

This skill is intentionally earlier than many common testing skills. It is not mainly a "generate tests from code" or "generate Playwright from a scenario" skill. Its value is in the moment before the team is ready to write cases or automation.

That earlier stage is where test engineers often add the most judgment:

- noticing that the spec only describes the happy path
- asking what happens when the user cannot complete an action
- finding missing loading, empty, error, disabled, and recovery states
- identifying ambiguous screen transitions or state persistence
- deciding what needs product/design clarification
- deciding what should later become manual testing, automation, mocks, or follow-up questions

This makes the skill more like a design-review companion for test engineers than a generation tool. Generation skills accelerate known work; this skill helps discover whether the known work is complete enough to generate from.

## Where Generation Skills Fit

Generation skills are still valuable, but they are downstream from test design.

| Skill type | Good at | Risk if used too early |
|---|---|---|
| Code-derived test generation | Locking current behavior, covering branches, scaffolding unit/API/integration tests | May confirm the implementation's assumptions instead of validating the intended behavior |
| API/unit/integration test generation | Producing repeatable checks when contracts and code are clear | May miss product requirements, omitted cases, or incorrect assumptions in the implementation |
| Playwright/Appium automation generation | Turning known UI scenarios into executable browser/mobile automation | May automate the visible happy path before selectors, data, assertions, and risk areas are understood |
| UI flow test design review | Finding missing viewpoints before cases/code exist | Does not produce final executable tests by default |

## Example: Code-Derived Tests

A code-generation skill might inspect production code and create tests for:

- branches and validation paths
- API request/response handling
- known exceptions
- data transformation logic
- regression coverage for current behavior

That is useful for confidence after implementation exists. But if the production code forgot a requirement, code-derived tests may simply preserve the same gap. They answer, "Does the code behave consistently with itself?" They do not reliably answer, "Is this the right behavior for the user?"

## Example: Playwright Automation Generation

A Playwright generation skill might create automation for:

- opening a page
- clicking visible controls
- filling forms
- asserting visible text
- checking navigation

That is useful after the test design is clear. Before automation, a test engineer still needs to decide:

- Which flow matters most?
- What data setup is needed?
- Which selectors or accessibility IDs are stable?
- What assertions prove the behavior, not just the UI shape?
- Which states are flaky because of animation, async loading, or third-party dependencies?
- Which checks are better left manual or exploratory?

## Practical Workflow

1. Use UI flow test design review to find missing viewpoints and clarify risk.
2. Use test-case generation when the expected behavior is clear enough to write manual cases.
3. Use Playwright/Appium generation when scenarios, selectors, data, and assertions are clear.
4. Use code-derived tests to lock implementation behavior and protect regressions.

The goal is not to avoid generation. The goal is to avoid generating polished tests for an incomplete understanding.

## Related Public Examples (GitHub)

The exact name and positioning of this skill (UI flow test design before test generation) appears uncommon, but adjacent patterns are present in public repositories.

### GitHub Awesome Copilot (adjacent examples)

- Playwright test generation from a provided scenario:
	- https://github.com/github/awesome-copilot/blob/main/skills/playwright-generate-test/SKILL.md
- Website exploration first, then test case proposal:
	- https://github.com/github/awesome-copilot/blob/main/skills/playwright-explore-website/SKILL.md
- Browser-based web app testing workflow:
	- https://github.com/github/awesome-copilot/blob/main/skills/webapp-testing/SKILL.md
- UI/design review and visual issue detection:
	- https://github.com/github/awesome-copilot/blob/main/skills/web-design-reviewer/SKILL.md
- Test planning and QA process scaffolding:
	- https://github.com/github/awesome-copilot/blob/main/skills/breakdown-test/SKILL.md

### OpenAI Skills Collection (adjacent examples)

- Playwright CLI automation workflow:
	- https://github.com/openai/skills/blob/main/skills/.curated/playwright/SKILL.md
- Playwright interactive debugging and visual QA workflow:
	- https://github.com/openai/skills/blob/main/skills/.curated/playwright-interactive/SKILL.md

### Structure/Packaging References

If you are designing or iterating skills, these references are useful for metadata, triggering, and packaging conventions:

- Skills in OpenAI API (concepts and packaging):
	- https://github.com/openai/openai-cookbook/blob/main/examples/skills_in_api.ipynb
- Agent Skills authoring guidance (GitHub Awesome Copilot):
	- https://github.com/github/awesome-copilot/blob/main/instructions/agent-skills.instructions.md

### Comparison Note

Most linked skills are either generation-first or execution-first. This repository's ui-flow-test-engineer focus remains intentionally earlier-stage: identify missing viewpoints and design risks before test case or automation generation.
