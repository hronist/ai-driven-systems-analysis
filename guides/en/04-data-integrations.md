# Module 4: System Design: Data and Integrations

An IT analyst must speak the language of data and APIs. A PRD without a data schema and API contracts is just an essay.

## 1. Data Design: ERD (Entity-Relationship Diagram)
Before writing SQLAlchemy/Django models, the analyst designs an ER diagram.
*   **Entities:** Tables (User, Course, Order).
*   **Attributes:** Fields (email, price, created_at).
*   **Relationships:** 1:1, 1:N, M:N.
*   *Important:* The analyst MUST specify business constraints. For example, `email` must be unique, and `price` >= 0. These constraints are not invented on the fly — they must strictly follow from the business rules and NFRs identified back in Module 1. (For example, the requirement for email uniqueness is a direct consequence of the business rule "one account = one payer", not just a whim of the DB designer).

## 2. API Visualization: Sequence Diagrams
A Sequence Diagram (Mermaid) shows how systems communicate over time.
*   Helps identify redundant requests (the N+1 problem).
*   Shows where logic is synchronous (HTTP) and where it is asynchronous (Kafka/RabbitMQ/Celery).

## 3. Contract-First Approach (OpenAPI/Swagger)
Modern analysis includes designing the API before writing code.
The analyst (or Lead Dev together with the analyst) describes the endpoints, request formats (JSON), and responses in OpenAPI (Swagger) format. This allows frontend (TS) and backend (Python) developers to work in parallel.

### Alternatives and Additions to API Contracts
*   **AsyncAPI:** If your system communicates via message brokers (Kafka, RabbitMQ, Redis Pub/Sub), OpenAPI won't work. AsyncAPI is the standard for describing asynchronous contracts (what events we publish, what we subscribe to).
*   **gRPC / Protobuf:** For high-load internal microservices. The contract is a `.proto` file, from which classes for Python and TS are automatically generated.
*   **UML Class Diagram:** An alternative to ERD. While an ERD describes tables in a relational DB, a class diagram describes objects in code (OOP). Useful if you are using NoSQL (MongoDB) or complex in-memory business logic.

---

## 🛠 Practical Assignment
**Task:** Design a "Course Reviews" module.
1.  **ERD:** Write Mermaid code (`erDiagram` type) for the `Users`, `Courses`, and `Reviews` tables. Specify relationships and data types (UUID, VARCHAR, INT).
2.  **Sequence Diagram:** Draw the "Leave a Review" process. Participants: `Client (TS)` -> `API (FastAPI)` -> `DB (PostgreSQL)`. Include the check: "Did the user buy this course?".
3.  **API Contract:** Write an example JSON request (Payload) for the `POST /api/reviews` endpoint and an example JSON response for a validation error.

## 🤖 AI Assistant (Architecture Review)
> "I have designed an ER diagram and a Sequence diagram for a review system. Check my ER diagram for normalization (up to 3NF). Check the Sequence diagram: is the load distributed optimally, are there any bottlenecks when writing to the DB?"

## 📚 Materials
*   [Mermaid ER Diagrams](https://mermaid.js.org/syntax/entityRelationshipDiagram.html).
*   [OpenAPI Specification](https://swagger.io/specification/).