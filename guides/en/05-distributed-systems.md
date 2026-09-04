# Module 5: Distributed Systems and Asynchronous Architecture

A modern backend rarely consists of a single monolith and synchronous REST APIs. As a system grows, microservices, message queues, and distributed transactions appear. An analyst must know how to design such systems.

## 1. Event-Driven Architecture (EDA)
Instead of Service A calling Service B (synchronously, waiting for a response), Service A publishes an **Event** to a message broker (Kafka, RabbitMQ, NATS). Service B listens to this broker and reacts to the event.

*   **Pros:** Loose coupling. If Service B goes down, Service A will continue to work.
*   **Cons:** Harder to debug, eventual consistency.
*   **Analyst's Role:** Describe the event contracts (Event Schema). What exactly is in the JSON when the `OrderCreated` event occurs? How do we guarantee that the event schema won't break consumers upon updating (Schema Registry)?

## 2. AsyncAPI: Contracts for Message Brokers
If we use OpenAPI (Swagger) for REST APIs, the standard for event-driven architecture is **AsyncAPI**.
The analyst describes:
*   **Channels (Topics/Queues):** Where we write (e.g., `orders.events`).
*   **Publish/Subscribe:** Who writes to the topic, and who reads.
*   **Payload:** Message structure (JSON Schema).

## 3. Distributed Transaction Patterns
In a monolith with PostgreSQL, we use `BEGIN ... COMMIT`. You can't do that in microservices. The analyst must embed architectural patterns into the PRD:

### Saga Pattern
Breaks a large transaction into a series of local ones.
*   **Choreography:** Services communicate via events without a central controller. (Order Service -> Payment Service -> Inventory Service).
*   **Orchestration:** There is a single "Orchestrator" that commands the services.
*   *Crucial for the analyst:* You MUST design **Compensating Transactions** (What to do if the money was charged, but the item is not in stock? You need to refund the money).

### Transactional Outbox Pattern
How do you guarantee writing data to your DB and sending an event to Kafka without losing anything during a crash?
*   Instead of sending directly to Kafka, the service writes the event to a special `outbox` table in its own DB (within the same transaction as the business data).
*   A separate process (Relay) reads the `outbox` table and sends messages to Kafka.

---

## 🛠 Practical Assignment
**Task:** Design an asynchronous course purchase process.
1.  **Event Storming:** Write down 3 key events that occur after the student clicks "Pay". (e.g., `PaymentProcessed`, `CourseAccessGranted`).
2.  **Saga Architecture:** Describe a compensating transaction. What should happen if `PaymentProcessed` is successful, but the access provisioning service (`CourseAccessGranted`) crashes with a fatal error?
3.  **Contract:** Write a draft JSON payload for the `PaymentProcessed` event.

## 🤖 AI Assistant (Architect)
> "I am designing an asynchronous course purchase system using Kafka. My stack: Python, PostgreSQL. Act as a Software Architect. I decided to use the Saga pattern (Choreography). What race conditions might arise, and how should I describe their handling in the PRD?"

## 📚 Materials
*   [AsyncAPI Specification](https://www.asyncapi.com/)
*   [Saga Pattern (Microservices.io)](https://microservices.io/patterns/data/saga.html)
*   [Transactional Outbox](https://microservices.io/patterns/data/transactional-outbox.html)