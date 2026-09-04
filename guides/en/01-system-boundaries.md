# Module 1: System Boundaries and Architectural Context

Any development starts with understanding: **why are we doing this** and **where does our responsibility end**. If an analyst doesn't define the boundaries, the project will turn into an endless monolith, and requirements will suffer from Scope Creep.

This module is not about how to draw a system beautifully. It's about how to understand it. The diagrams at the end of the module are a tool for capturing the result, not a method for obtaining it.

## 1. The Idea Lifecycle: From Problem to Ticket

Developers are used to thinking in Jira entities (Epic → Story → Task). But this hierarchy is just a way to *decompose an already agreed-upon solution* (more on this in Module 3). Systems analysis starts much earlier — where there is no solution yet, only a business problem.

The lifecycle of an idea before the first ticket:

1. **Problem Framing:** Who is hurting and why? We are not doing "gamification." We are solving a problem: "students drop the course at the 3rd lesson due to a lack of visible progress."
2. **Discovery & Research:** Validating the problem. Is it really widespread? How do competitors solve it? What do the data and users say?
3. **Scope Definition:** Strictly fixing what we are doing, and more importantly — what we are **consciously NOT doing**.
4. **System Design:** Architecture of processes, data flows, and integrations.
5. **Validation:** Stress-testing the architecture before writing code (edge cases, NFRs, security).
6. **Delivery:** Only here does the idea turn into an Epic and go into development.

If you skip steps 1–5 and immediately create an Epic, you risk designing the perfect architecture for a feature nobody needs.

## 2. The Core of Analysis: Mining Facts, Not Opinions

This is the toolkit for the Problem Framing and Discovery stages. Your task is to turn a hypothesis ("it seems there is a problem here") into a proven fact.

* **The "5 Whys" Method:** A stakeholder asks for an "Export to Excel" button. Ask "why?" five times. It turns out the real pain is manual data reconciliation with the tax office. The solution won't be an Excel file, but an automated integration. This method separates the **symptom** (request for a button) from the **root cause** (need for reconciliation).
* **Data Triangulation:** Interviews (e.g., The Mom Test from Module 2) are a powerful tool, but they only show what people *say*. Supplement words with facts:
  * **Analytics and Logs:** Study support tickets, drop-off charts, and error logs. This is objective reality.
  * **Shadowing:** Sit next to the user. Often, the stated process drastically differs from how the person actually clicks on the screen.
  * **Cross-functional Workshops:** Bring stakeholders from different departments together. Contradictions in their requirements will surface in an hour, rather than after a month of emails.
* **Working with Trade-offs:** Requirements from different departments always conflict. Support demands strict promo code validation, while Sales wants flexibility for VIP clients. The analyst's job is not to hide this conflict in vague PRD wording, but to highlight it and force the Product Owner to make a conscious architectural decision before development starts.

## 3. Stakeholder Analysis: Who Controls the Boundaries

Before drawing the architecture, you need to understand who actually has the right to dictate requirements.

* **Participant Map:** Stakeholders are not just the "client" and the "user." They include security, legal, support, finance, and teams of adjacent microservices.
* **Power/Interest Grid:** 
  * *High interest, low power (users):* they need to be researched, but they don't approve the scope. 
  * *High power, low interest (top management):* they need short, precise approvals without diving into details.
* **Conflict Resolution:** Ignoring conflicts of interest (e.g., between security and UX) generates 50% of all architectural bugs. Identify and resolve them upfront. Without stakeholder analysis, the system boundaries will be determined either by whoever shouts the loudest on a call, or by the developer themselves (which are equally bad).

## 4. Non-Functional Requirements (NFRs) as Part of Architecture

NFRs are not a formal sign-off at the end of a PRD. They are strict boundaries that directly dictate the choice of technologies and architectural patterns.

Where NFRs come from (they are not invented out of thin air):
* **Performance and Scalability:** Dictated by the business context (DAU, MAU, peak loads on Black Friday).
* **Security and Compliance:** Dictated by regulators (PCI DSS for payments, GDPR for personal data).
* **Reliability (Availability/SLA):** Dictated by contracts (B2B SLA) or product metrics.
* **Infrastructure Constraints:** Dictated by the company's current IT landscape and budget.

**The Golden Rule of NFRs:** Every non-functional requirement must have a **source** (a specific stakeholder or document). If there is no source, it's an analyst's hallucination that any developer will easily challenge.

## 5. Designing System Boundaries

Once the problem, stakeholders, and NFRs are locked in, we move on to designing the boundaries.

### External Boundaries (Integrations)
Determined through the stakeholders' touchpoints with the system. Which external APIs, legacy databases, and roles will exchange data with your service? This is the result of analytical work, which is later visualized via the C4 Context.

### Internal Boundaries (Microservices and Modules)
* **DDD (Bounded Contexts):** Don't create "God Objects." The `User` entity in the billing module is a payer (needs card linking). In the learning module, it's a student (needs progress tracking). Separate data models by contexts.
* **Event Storming:** The practice of finding boundaries through events. Write down business events on sticky notes (`OrderPlaced`, `PaymentFailed`). The logical gaps between these events are ideal places to slice a monolith into microservices.

## 6. Documenting the Result: C4 Model

Diagrams are a language for capturing accepted decisions, not a way to find them. 

**C4 Model (Level 1: System Context)** — this is your system in the center (black box) and everything that interacts with it.
* **Weak scenario:** Drawing a diagram just for a pretty picture in the PRD, skipping steps 1–5.
* **Strong scenario:** Using the diagram for verification. If an arrow to Stripe appears on the diagram, it automatically triggers the creation of security NFRs (PCI DSS) and Use Cases for handling webhooks. Also, C4 code (Mermaid) feeds perfectly into an LLM to find architectural inconsistencies.

*(Alternative notations like UML, DFD, and ArchiMate are moved to [Appendix 01a](./01a-alternative-notations.md) to avoid overloading the module).*

---

## 🛠 Practical Assignment
**Project:** Online Course Platform (Course Analytics).
**Task:** The business wants to introduce "Gamification" (achievements for completed lessons) to increase engagement.

1. **Problem framing + 5 Whys:** Formulate the problem in user terms (not "we need gamification," but what exactly hurts and for whom) and run it through the 5 Whys to check if you are solving a symptom instead of the root cause.
2. **Stakeholders:** List at least 4 stakeholders for this feature (not just "student" and "product manager") and for each — their interest and power level. Note at least one conflict of interest between them.
3. **NFRs:** Formulate 3 non-functional requirements for the gamification feature and indicate the source of each.
4. **C4 Context:** Write Mermaid code (`C4Context` or `graph TD`) showing which external systems or roles the Gamification service will interact with.

## 🤖 AI Assistant (Verification)
> "Here is the problem (passed through 5 Whys), a list of stakeholders with conflicts of interest, and NFRs for the 'Gamification' feature in an online course platform. Act as a skeptical Systems Analyst: has the real user problem been lost behind the solution? Did I forget a significant stakeholder or a conflict of interest between them? Are the NFRs realistic and is their source justified?"

## 📚 Materials
* Karl Wiegers, Joy Beatty — "Software Requirements" (methodology for eliciting business rules).
* [C4 Model (Official Site)](https://c4model.com/)
* [Event Storming (Alberto Brandolini)](https://www.eventstorming.com/)
* Vaughn Vernon — "Domain-Driven Design Distilled".
* [Appendix: Alternative Notations](./01a-alternative-notations.md) (UML, DFD, ArchiMate)