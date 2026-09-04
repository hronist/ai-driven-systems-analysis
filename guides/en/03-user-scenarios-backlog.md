# Module 3: User Scenarios and Backlog

Once we have a business process (BPMN), we need to slice it into chunks that can be handed over to development without losing the big picture.

## 1. User Story Mapping
A Jira backlog is a flat list. It's easy to lose the essence of the product in it. Jeff Patton invented User Story Mapping:
*   **Backbone:** User steps from left to right (Find course -> Pay -> Complete -> Get certificate).
*   **Walking Skeleton:** The thinnest version of the product (MVP) that allows you to go from start to finish.
*   **Releases (Slices):** Horizontal lines separating the MVP from "future" features.

### Backlog Prioritization
An analyst must be able to defend the MVP from business "wishlists". If you can't say "no", your backlog will turn into a dump.
*   **MoSCoW:** Must have, Should have, Could have, Won't have (this time).
*   **RICE:** Reach × Impact × Confidence / Effort. A mathematical approach to feature selection.

## 2. Rapid Prototyping (Wireframing)
Developers often think in DB tables, while customers think in interfaces.
Before writing a Use Case, sketch a rough UI (in Figma, Balsamiq, or Excalidraw). Often, it's during the interface drawing stage that hidden business rules surface (e.g., "Where will the user's balance come from on this screen?"). A prototype is the cheapest way to test a hypothesis before writing code.

## 3. Use Cases
A User Story ("I want to pay for a course") is too small for a PRD. A Use Case describes a **strict algorithm**.

**Use Case Structure for a Backend Developer:**
1.  **Pre-conditions:** (Token is valid, course exists). -> *Middleware in FastAPI.*
2.  **Main Success Scenario:** The happy path.
3.  **Alternate Flows:** User entered a promo code. -> *Additional logic branch.*
4.  **Exception Flows:** Card expired, DB unavailable. -> *Try-except blocks, HTTP 400/500.*
5.  **Post-conditions:** Record created in DB.

**How to find Exception Flows (and not just invent them):**
Don't rely on intuition. Go through the boundaries of every value and state (boundary analysis):
*   What if the quantity is at the boundary (0, maximum)?
*   What if the action is repeated twice in a row (idempotency)?
*   What if two requests arrive simultaneously (race condition)?
*   What if the external system (payment gateway, DB) responds with a delay or times out?

*Note:* This same analysis will be useful in Module 7 when writing BDD scenarios, but you need to lay the groundwork for it here, at the Use Case design stage.

### Alternatives: Job Stories (JTBD) and CJM
*   **Job Stories (Jobs To Be Done):** A great replacement for classic User Stories. Instead of roles, the focus is on **context and motivation**. 
    *   *Format:* `When [situation], I want to [motivation], so I can [outcome]`.
    *   *Example:* "When I am riding the subway with bad internet (situation), I want to download the lesson in advance (motivation), so I can study without interruptions (outcome)." This gives the developer much more context (offline mode and caching are needed).
*   **CJM (Customer Journey Map):** A UX tool. A map of user emotions and touchpoints with the product. Analysts use it to find bottlenecks (e.g., where the user gets angry due to long loading times).

---

## 🛠 Practical Assignment
**Task:** "Apply Promo Code at Checkout" Feature.
1.  **Story Mapping:** Identify 3 steps (backbone) for the purchase process and outline 2 releases (MVP and V2) below them.
2.  **Use Case:** Write a detailed Use Case for applying a promo code. Pay special attention to **Exception Flows** (promo code expired, promo code already used by this user, promo code not for this course).

## 🤖 AI Assistant (Use Case Verification)
> "Here is my Use Case for applying a promo code. My stack: Python, PostgreSQL. Act as a Senior Backend Developer. Check the exception flows. What other edge cases have I missed in terms of concurrent requests (race conditions) and DB transactionality?"

## 📚 Materials
*   Jeff Patton — "User Story Mapping".
*   Alistair Cockburn — "Writing Effective Use Cases".