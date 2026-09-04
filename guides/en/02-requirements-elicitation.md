# Module 2: Requirements Elicitation and Business Processes

Requirements don't lie on the surface. They need to be "dug out" from stakeholders and current processes.

## 1. Customer Psychology and "The Mom Test"
Customers come with **solutions** ("Make me an 'Export to Excel' button"), not with **problems** ("I need to reconcile data for taxes").
*   **The Mom Test Rule:** Ask about the past, not the future. Don't ask "Do you need this feature?". Ask "How did you solve this problem last week?".
*   Listen more than you talk. Look for "pains" that the business is willing to pay for.

*Note:* The Mom Test perfectly covers the **Discovery** stage (see Module 1), validating that the problem is real. However, remember data triangulation: people often say one thing and do another. Always back up interview results with dry analytics (logs, tickets) and "field" observations (Shadowing).

## 2. Process Modeling: BPMN 2.0
BPMN (Business Process Model and Notation) is the global standard for describing business processes. If you don't understand the process, your code automates chaos.
*   **AS-IS:** How the business works now (often this involves sending Excel files via Telegram).
*   **TO-BE:** How the process will work after your system is implemented.

**Basic BPMN Elements:**
*   **Pools / Lanes:** Who performs the work (e.g., "Student" lane, "Python Backend" lane, "Manager" lane).
*   **Tasks:** Actions (User Task - done by a human, Service Task - done by a script).
*   **Gateways:** Branching (Exclusive "XOR", Parallel "AND").

### Alternative Process Notations (Broadening Horizons)
BPMN is the de facto standard, but in different companies you might encounter:
*   **UML Activity Diagram:** A more "programmer-centric" alternative to BPMN. Easier to learn, great for describing algorithms within a single service, but worse at handling cross-system interactions.
*   **EPC (Event-Driven Process Chain):** A historical standard from the SAP/ARIS world. Very strict, read top to bottom. Often found in banking and oil & gas.
*   **IDEF0:** An ancient standard for describing system functions (Inputs, Outputs, Controls, Mechanisms). Looks like factory blueprints. Rarely used in modern IT, but useful to know.

---

## 🛠 Practical Assignment
**Task:** "Course Refund" Process.
1.  **Interview:** Write 5 questions using The Mom Test methodology for a support manager to understand how they currently handle refunds (AS-IS).
2.  **BPMN TO-BE:** Describe in text (or draw in PlantUML/Mermaid) the refund process in the new system. 
    *   *Participants (Lanes):* Student, TS Frontend, Python Backend, Payment Gateway.
    *   *Condition (Gateway):* If more than 10% of the course is completed — deny refund. Otherwise — automatic refund.

## 🤖 AI Assistant (Roleplay)
> "Act as a support manager. I am an analyst gathering requirements for automating refunds. I will ask you questions based on 'The Mom Test'. Answer realistically: right now you do everything manually via the bank's admin panel and Excel. Let's begin!"

## 📚 Materials
*   Rob Fitzpatrick — "The Mom Test".
*   [BPMN 2.0 Tutorial (Camunda)](https://camunda.com/bpmn/).