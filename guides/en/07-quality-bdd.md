# Module 7: Quality, BDD, and Change Management

The PRD is written. How do you ensure it is high quality, and how do you guarantee that programmers will implement exactly what is written?

## 1. Requirements Quality Criteria
A requirement must be:
*   **Atomic:** One requirement = one thought.
*   **Unambiguous:** No words like "fast", "convenient", "usually".
*   **Testable:** Can you write an automated test for this requirement?
*   **Consistent:** Requirement A must not break Requirement B.

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

---

## 🛠 Practical Assignment
**Task:** PRD Audit and Preparation for Development.
1.  **Audit:** Take any 3 requirements from your PRD (Module 6). Check them against the quality criteria (remove filler words).
2.  **BDD:** Write 3 Gherkin scenarios for the "Promo codes" feature (1 successful, 2 with validation errors).
3.  **Traceability:** Create a mini-traceability table: `Requirement ID | Description | BDD Scenario ID | Code Module (e.g., api/routers/promocodes.py)`.

## 🤖 AI Assistant (Paranoid QA)
> "I am a Systems Analyst. Here are my BDD scenarios in Gherkin for the Promo Codes feature. Act as a Senior QA Automation Engineer. Find logical holes in my scenarios. Are the checks in the 'Then' blocks strict enough? What boundary values for the PostgreSQL database did I forget to check?"

## 📚 Materials
*   [Cucumber Gherkin Reference](https://cucumber.io/docs/gherkin/reference/).
*   Karl Wiegers — "Software Requirements" (Chapters on Requirements Assessment and Traceability).