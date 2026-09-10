# Module 7: Quality, BDD, and Change Management

The PRD is written. How do you ensure it is high quality, and how do you guarantee that programmers will implement exactly what is written?

## 1. Requirements Quality Criteria
A requirement must be:
*   **Atomic:** One requirement = one thought.
*   **Unambiguous:** No words like "fast", "convenient", "usually".
*   **Testable:** Can you write an automated test for this requirement?
*   **Consistent:** Requirement A must not break Requirement B.

**These aren't just criteria for a good PRD — they're criteria for a good prompt.** When you write a requirement for an AI agent (Cursor, Claude Code, Copilot) instead of a fellow developer, these criteria apply literally: a non-atomic requirement gets silently split into subtasks the agent's own way; an ambiguous word like "fast" gets either ignored or replaced with a number the agent made up; an untestable requirement gets implemented in a way you can't prove satisfies it. The difference from a human developer is that a colleague usually asks when a requirement is unclear — an AI agent more often silently picks its own interpretation and produces confident-looking but wrong code. So in the age of AI code generation, a vague requirement doesn't "surface in code review" — it quietly slips into production unless you check the code against the original requirement.

## 2. BDD (Behavior-Driven Development) and Gherkin
BDD translates requirements into a format understood by both business and automated tests.
**Gherkin** syntax:
*   **Given:** Precondition (DB state).
*   **When:** User/system action.
*   **Then:** Expected result.

*Example:*
`Given` the user is authorized and has 100 USD on their balance.
`When` they buy a course for 100 USD.
`Then` the balance becomes 0 USD, `And` the course appears in the "My Courses" section.

### Alternatives and Evolution of BDD
*   **Specification by Example (SbE):** An approach where requirements are written as tables with specific examples of input and output data. Translates very easily into parameterized tests (`@pytest.mark.parametrize`).
*   **TDD (Test-Driven Development):** The developer writes a unit test before writing the code. BDD is an evolution of TDD, where tests are written at the level of business scenarios, not individual functions.

## 3. Traceability Matrix
How do you prove that the code covers the PRD?
A traceability matrix is a table linking:
`Business Goal` -> `User Story` -> `Use Case` -> `Function in Code` -> `Test Case`.
If a function in the code has no link to a business goal, it's "gold plating" (unnecessary code). If a Use Case has no Test Case, it's a potential bug in production.

**The same matrix is a code-review tool for AI-generated code — just run in reverse.** Normally you build it left to right: from requirement to code. But when the code was written by an AI agent, it's more useful to walk it right to left: take a function from the PR and ask — which Use Case and which business goal does it map to? If you can't find an answer, or only a strained one, that's exactly the "AI code technically works but solves the wrong problem" case: the agent wrote something syntactically correct and plausible-looking, but not covering the original business rule (or covering the wrong one).

---

## 🛠 Practical Assignment
**Task:** PRD Audit and Preparation for Development.
1.  **Audit:** Take any 3 requirements from your PRD (Module 6). Check them against the quality criteria (remove filler words).
2.  **BDD:** Write 3 Gherkin scenarios for the "Promo codes" feature (1 successful, 2 with validation errors).
3.  **Traceability:** Create a mini-traceability table: `Requirement ID | Description | BDD Scenario ID | Code Module (e.g., api/routers/promocodes.py)`.
4.  **AI as executor — an ambiguity experiment:** Take one of your BDD scenarios and hand it to an AI agent (Cursor, Claude Code, Copilot) asking it to generate an implementation. Deliberately leave one ambiguity in the scenario — for example, don't specify what to return if a promo code exists but expired exactly at the current second, or don't specify the error format (HTTP code, text, JSON structure). See how the agent handles it: does it silently guess its own way, or ask for clarification? Rewrite the requirement to remove the ambiguity, regenerate the code, and compare both results.
5.  **AI as code reviewer — reverse traceability:** Take the code generated in step 4. Walk the traceability matrix right to left: for each function, find which Use Case and which business goal it corresponds to. Flag any code that technically executes but doesn't cover the business rule that was in the original scenario.

## 🤖 AI Assistant

**Role 1 — Executor (generation from a requirement).**
> "Here is my BDD scenario in Gherkin for the Promo Codes feature. Stack: Python, FastAPI, PostgreSQL. Generate an implementation of the endpoint strictly following this scenario, without adding anything beyond what's written. If you don't have enough information for an unambiguous implementation, ask clarifying questions before writing code."

**Role 2 — Paranoid QA (scenario review).**
> "I am a Systems Analyst. Here are my BDD scenarios in Gherkin for the Promo Codes feature. Act as a Senior QA Automation Engineer. Find logical holes in my scenarios. Are the checks in the 'Then' blocks strict enough? What boundary values for the PostgreSQL database did I forget to check?"

**Role 3 — Code reviewer against the business requirement (reverse traceability).**
> "Here is the code [paste the function/PR] and here is the original BDD scenario it was supposed to be written from. Act as a Senior Backend Developer doing code review. Check line by line: does the code do exactly what the scenario says, or something similar in shape but different in meaning? Flag any discrepancy between the code and the business rule, even if the code doesn't technically fail and passes the obvious tests."

## 📚 Materials
*   [Cucumber Gherkin Reference](https://cucumber.io/docs/gherkin/reference/).
*   Karl Wiegers — "Software Requirements" (Chapters on Requirements Assessment and Traceability).