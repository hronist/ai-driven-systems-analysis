# Appendix to Module 1: Alternative Notations

Optional material. In [Module 1](./01-system-boundaries.md), C4 is used to document system boundaries — this is sufficient for most developer tasks. Below are alternatives that might be required in specific companies or contexts. Like C4, these are languages for recording a decision that has already been made, not methods of analysis.

## UML (Unified Modeling Language)
The classic standard. For system boundaries, they use the **UML Use Case Diagram** (a rectangle for system boundaries, functions inside, actors outside) or the **Component Diagram**. Understood worldwide, often mandatory in fintech and outsourcing.

* [UML Use Case Diagrams — reference](https://www.uml-diagrams.org/use-case-diagrams.html)

## DFD Level 0 (Data Flow Diagram)
Unlike C4, which shows dependencies, DFD shows *data flows*. The system is in the center, and arrows show exactly what data (e.g., a JSON profile) flies in and out. Convenient for designing DTOs.

## ArchiMate (in conjunction with TOGAF)
Heavy artillery for Enterprise Architecture. Allows you to link a business process, a specific API, and a physical server in a data center on a single diagram. Mostly relevant for large enterprise companies with a dedicated architect role.

---

If your company does not specifically require these notations, you can skip this and return to [Module 1](./01-system-boundaries.md).