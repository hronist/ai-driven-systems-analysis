# Module 6: Spec Anatomy (Documentation Structure)

How do you gather all the artifacts (BPMN, Use Cases, ERD) into a single document that will become the contract for development?

## 1. Standards: GOST 34 vs IEEE 830 vs PRD
*   **GOST 34:** A heavy standard for the government sector (Russian/CIS).
*   **IEEE 830:** The classic Western standard for Software Requirements Specification (SRS).
*   **PRD (Product Requirements Document):** The modern product standard (used in Agile/Scrum).

We will use a hybrid PRD/SRS structure, ideal for commercial development.

### Alternatives for Developers: ADR and RFC
In modern IT companies (especially BigTech), classic PRDs are often replaced by engineering documents:
*   **ADR (Architecture Decision Record):** A short document capturing a single important technical decision. (e.g., "Why we chose PostgreSQL over MongoDB for analytics"). Contains Context, Decision, and Consequences.
*   **RFC (Request for Comments):** A practice from the Open Source world. An engineer writes a document proposing a new architecture or feature and sends it to the team for critique. After discussion, the RFC becomes a mini-PRD.

## 2. Mandatory Sections of a Modern PRD

1.  **Introduction and Business Context:** Why are we doing this? **Success Metrics (Unit Economics):** How will we know the feature is successful? (e.g., lower CAC, higher ARPU or Retention). Glossary of terms.
2.  **Role Model (RBAC/ABAC):** Who has access to the system? Access rights matrix (CRUD for each role).
3.  **Business Processes (AS-IS / TO-BE):** Insertion of BPMN diagrams with text descriptions.
4.  **Functional Requirements:**
    *   List of Use Cases (Main, Alternate, Exception).
    *   Business Rules (Formulas, constraints).
5.  **Data Requirements:**
    *   ER Diagram (DB Schema).
    *   Entity Lifecycles (State Machines).
6.  **Integrations and Interfaces:**
    *   API Description (link to Swagger/OpenAPI/AsyncAPI).
    *   Integrations with external systems (Stripe, SendGrid).
7.  **Non-Functional Requirements (NFRs) and Feasibility:**
    *   Here, we do not start the NFR checklist from scratch. We take those constraints (performance, security, SLA) that we identified with stakeholders in Module 1, and detail them into specific metrics.
    *   **Feasibility Analysis:** Estimating infrastructure costs (AWS/GCP). Build vs Buy decision (Do we write our own mailing microservice or buy a SaaS?).

---

## 🛠 Practical Assignment
**Task:** Assemble a PRD skeleton.
1.  Create a file `docs/PRD_Template.md`.
2.  Fill in the PRD structure for the feature from Module 3 (Promo codes).
3.  Write a **Glossary** (minimum 5 terms).
4.  Create an **Access Rights Matrix** (Roles: Anonymous, Student, Author, Admin. Entity: Promo code. Rights: Create, Read, Update, Delete).

## 🤖 AI Assistant (Template Generation)
> "Act as a Lead Systems Analyst. I am writing a PRD for a promo code system. Check my Access Rights Matrix. Are there any security conflicts? Help me formulate the 'Non-Functional Requirements' and 'Success Metrics' sections for this feature, considering the Python/PostgreSQL stack."

## 📚 Materials
*   [Atlassian PRD Templates (Confluence)](https://www.atlassian.com/software/confluence/templates/product-requirements-document).
*   Karl Wiegers — "Software Requirements" (Chapter on Documenting Requirements).