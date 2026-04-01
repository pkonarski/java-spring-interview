# Senior Java Engineer Interview Prep — InPost Pay

Source: https://jobs.smartrecruiters.com/InPost/744000115650127-senior-java-engineer-m-f-n-

---

## Core Java

- [ ] What are the differences between `HashMap` and `ConcurrentHashMap`? When would you use each?
- [ ] How does the JVM handle memory? Explain heap, stack, metaspace, and GC generations.
- [ ] What's the difference between `CompletableFuture` and reactive streams? When would you pick one?
- [ ] Explain the happens-before relationship in the Java memory model.
- [ ] How do virtual threads (Project Loom) differ from platform threads, and what's their impact on throughput?

---

## Spring Boot / Microservices

- [ ] How does Spring Boot auto-configuration work under the hood?
- [ ] What's the difference between `@Component`, `@Service`, `@Repository` — is it just semantic?
- [ ] Explain Spring Security's filter chain. How would you implement JWT authentication?
- [ ] How do you handle distributed transactions across microservices without 2PC? (Saga pattern)
- [ ] How do you implement circuit breakers and bulkheads with Resilience4j? What's the difference between them?
- [ ] What are the common pitfalls of `@Transactional` in a distributed system? (self-invocation, wrong propagation, transaction boundaries across services)
- [ ] How do you version REST APIs and why does it matter?

---

## Kafka

- [ ] Explain the consumer group model. What happens when a consumer crashes mid-processing?
- [ ] What is exactly-once semantics in Kafka and when do you need it?
- [ ] How do you ensure message ordering in a distributed microservice environment?
- [ ] What's the difference between at-least-once and idempotent consumers? How do you implement idempotency?
- [ ] How would you handle a Kafka consumer that's falling behind (consumer lag)?
- [ ] What is a Poison Pill message? How do you detect it, isolate it, and prevent it from blocking the entire consumer?

---

## JPA / Hibernate

- [ ] What's the N+1 query problem and how do you fix it?
- [ ] Explain `EAGER` vs `LAZY` loading trade-offs in a REST context.
- [ ] What are the different `@Transactional` propagation levels? When does `REQUIRES_NEW` matter?
- [ ] What's optimistic vs pessimistic locking and when do you use each?
- [ ] What is the difference between `READ_COMMITTED` and `SERIALIZABLE` isolation levels? What are the performance implications on a high-write ledger table?
- [ ] How does the first/second-level cache work in Hibernate?

---

## System Design

- [ ] Design a payment processing system that handles 10k transactions/second with exactly-once guarantees.
- [ ] How would you design an idempotent API for order creation? How do you prevent double-charging during network retries?
- [ ] If a downstream provider returns HTTP 504 (Gateway Timeout), how does your service determine the final state of the transaction?
- [ ] How would you implement distributed rate limiting across microservice instances?
- [ ] How do you approach database schema migrations in a zero-downtime deployment for a table with millions of financial records?
- [ ] How do you implement database sharding at the application level once a single instance hits its write limit?
- [ ] How would you design an event-driven checkout flow across multiple services?

---

## Docker / Kubernetes / GCP

- [ ] What's the difference between a `Deployment`, `StatefulSet`, and `DaemonSet`?
- [ ] How do you configure liveness vs readiness probes and why does the distinction matter?
- [ ] Explain how Kubernetes handles rolling updates and rollbacks.
- [ ] What GCP services would you use for: message queuing, secrets management, distributed tracing?
- [ ] How do you manage secrets in a Kubernetes cluster securely?

---

## Performance & Reliability

- [ ] How do you profile and diagnose a memory leak in a production JVM service?
- [ ] How do you tune G1GC or ZGC to minimize Stop-the-World pauses in a latency-sensitive payment service?
- [ ] What tools/approaches do you use for distributed tracing? (OpenTelemetry, Jaeger, Cloud Trace)
- [ ] How do you implement graceful shutdown for a Spring Boot service consuming Kafka?
- [ ] What metrics would you define SLIs/SLOs around for a payment microservice?

---

## Immutability

- [ ] What makes a class truly immutable in Java? List all the rules (final class, private final fields, no setters, deep copy in constructor, unmodifiable/copy in getters).
- [ ] Why must a class be `final` to be truly immutable? What risk does subclassing introduce?
- [ ] Why are immutable objects inherently thread-safe?
- [ ] Why must objects used as `HashMap`/`HashSet` keys be immutable? What happens if their `hashCode()` changes?
- [ ] How do you design an immutable class with mutable fields (e.g., `List`, `Date`)? (deep copy in constructor, unmodifiable wrapper in getter)
- [ ] What's the difference between `final`, `effectively final`, and immutability?
- [ ] What is failure atomicity and how does immutability guarantee it?
- [ ] How does immutability improve security for sensitive data like payment amounts — what attack does it prevent?
- [ ] Why can immutable objects be safely shared across layers without defensive copies?
- [ ] What are Java Records? What do they give you for free and what must you still handle manually?
- [ ] What are the trade-offs of immutability in high-throughput systems (object allocation pressure vs. GC optimization for short-lived objects)?
- [ ] Why are immutable objects ideal for shared caches (Redis, local cache) in a multi-instance microservice?
- [ ] How do you handle immutability in a distributed system — e.g., immutable events on Kafka, immutable DTOs across services?
- [ ] How do you propagate state changes without mutating shared objects across service boundaries?
- [ ] What role does immutability play in event sourcing and financial audit trails?
- [ ] How does immutability relate to value objects in DDD?

---

## Design Patterns (GoF)

Source: https://www.geeksforgeeks.org/system-design/gang-of-four-gof-design-patterns/

### Creational
- [ ] **Factory Method** — When would you use Factory Method vs a direct constructor? Give a Spring example.
- [ ] **Abstract Factory** — How does Abstract Factory differ from Factory Method? When do you need families of objects?
- [ ] **Singleton** — How is Spring's default bean scope a Singleton? What are the thread-safety implications?
- [ ] **Builder** — When would you use Builder over a constructor? How does Lombok's `@Builder` implement it?
- [ ] **Prototype** — What is the Prototype pattern? How does Spring's `@Scope("prototype")` relate to it?

### Structural
- [ ] **Adapter** — What problem does Adapter solve? Give an example of wrapping a legacy API.
- [ ] **Bridge** — How does Bridge differ from Adapter? When would you decouple abstraction from implementation?
- [ ] **Composite** — Where would you use Composite in a tree-structured domain (e.g., order line items)?
- [ ] **Decorator** — How does Spring use Decorator? Compare with Proxy.
- [ ] **Facade** — How does a service layer act as a Facade over repositories and domain logic?
- [ ] **Flyweight** — When does Flyweight apply? Give an example involving a high-volume object (e.g., cached immutable configs).
- [ ] **Proxy** — How does Spring AOP use Proxy? What's the difference between JDK dynamic proxy and CGLIB?

### Behavioral
- [ ] **Chain of Responsibility** — How does Spring Security's filter chain implement this pattern?
- [ ] **Command** — How would you use Command to implement undo/redo or an audit log?
- [ ] **Iterator** — How does Java's `Iterable`/`Iterator` implement this pattern?
- [ ] **Mediator** — How does a message broker (Kafka) act as a Mediator between microservices?
- [ ] **Memento** — Where would Memento apply in a payment flow (e.g., saving/restoring transaction state)?
- [ ] **Observer** — How does Observer map to Kafka consumers and Spring's `ApplicationEvent`?
- [ ] **State** — How would you model an order lifecycle (PENDING → PAID → SHIPPED) using the State pattern?
- [ ] **Strategy** — Give a real example: swapping payment providers or discount calculation strategies at runtime.
- [ ] **Template Method** — How does `JdbcTemplate` or `AbstractController` use Template Method?
- [ ] **Visitor** — When would you use Visitor over adding methods to each class?
- [ ] **Interpreter** — Where does Interpreter appear in practice? (e.g., SpEL in Spring)

### Enterprise / Distributed (beyond GoF but expected)
- [ ] **Outbox Pattern** — Why is it critical for reliable Kafka publishing alongside a DB write?
- [ ] **Saga Pattern** — Choreography vs orchestration: trade-offs for a payment flow?

---

## Distributed Systems Operations

- [ ] What is the CAP theorem and what trade-offs does it force in practice?
- [ ] What is eventual consistency and how do you reason about it in a payment flow?
- [ ] How do you handle partial failures in a chain of microservice calls?
- [ ] What is the Two Generals Problem and why does it matter for distributed commits?
- [ ] How do you implement idempotency keys to safely retry failed operations?
- [ ] When do you use a distributed lock (Redis/Redlock) vs database-level optimistic locking? What are the failure modes of each?
- [ ] How do you achieve consensus across distributed nodes? (Raft, Paxos — conceptual level)
- [ ] What is a split-brain scenario and how do you prevent it?
- [ ] How do you handle clock skew between distributed services? (logical clocks, vector clocks)
- [ ] What's the difference between synchronous and asynchronous replication trade-offs?
- [ ] How do you design for graceful degradation when a downstream service is unavailable?

---

## SQL / NoSQL

- [ ] When would you choose a NoSQL store over PostgreSQL in a microservices context?
- [ ] How do you handle schema evolution in an event-sourced system?
- [ ] What's your approach to database indexing strategy for high-read payment queries?

---

## Testing

- [ ] How do you test Kafka consumers/producers without a running broker? (Testcontainers vs EmbeddedKafka)
- [ ] What's the difference between `@SpringBootTest`, `@WebMvcTest`, and `@DataJpaTest`? When do you use each?
- [ ] How do you test idempotency in an integration test?

---

## Payment / Security

- [ ] How do you protect sensitive payment data in transit and at rest in a microservice architecture?
- [ ] What is PCI DSS and what technical controls does it require? How does tokenization help achieve compliance without storing raw card data?
- [ ] Compare AES (symmetric) vs RSA (asymmetric) encryption — when would you use each for securing payment payloads?
- [ ] How would you implement audit logging that cannot be tampered with?

---

## Concurrency (Deep Dive)

- [ ] What is the difference between `synchronized`, `ReentrantLock`, and `StampedLock`? When would you choose each?
- [ ] What does `volatile` guarantee and when is it not enough?
- [ ] What are the pitfalls of `ThreadLocal`? How can it cause memory leaks in thread-pool environments?
- [ ] How do you size a thread pool? What's the formula for CPU-bound vs I/O-bound workloads?
- [ ] What is the difference between `Executors.newFixedThreadPool` and `ForkJoinPool`?
- [ ] How do you detect and prevent deadlocks in a Java application?
- [ ] What are `CountDownLatch`, `CyclicBarrier`, and `Semaphore` — when do you use each?

---

## DDD — Domain-Driven Design

- [ ] What is the difference between an Entity, a Value Object, and an Aggregate?
- [ ] What are the rules of an Aggregate Root? Why should you only reference aggregates by ID across boundaries?
- [ ] What is the difference between a Domain Event and an Integration Event?
- [ ] How do Bounded Contexts map to microservices?
- [ ] What is an Anti-Corruption Layer and when do you need one?
- [ ] How does the Repository pattern in DDD differ from a Spring Data JPA repository?
- [ ] How would you model a payment transaction as a DDD aggregate?

---

## CQRS + Event Sourcing

- [ ] What is CQRS and what problem does it solve?
- [ ] How do you keep the read model in sync with the write model?
- [ ] What is Event Sourcing? How does it differ from storing current state?
- [ ] How do you rebuild a read model projection from an event stream?
- [ ] What are the trade-offs of Event Sourcing — what makes it hard to operate?
- [ ] How does Event Sourcing provide a natural audit trail for financial transactions?
- [ ] How do CQRS and Event Sourcing work together with Kafka?

---

## SOLID + Clean Architecture

- [ ] Explain each SOLID principle with a concrete Java example.
- [ ] What is the Dependency Inversion Principle and how does Spring enforce it?
- [ ] What is Hexagonal Architecture (Ports & Adapters)? How do you map it to a Spring Boot service?
- [ ] How do you separate domain logic from infrastructure concerns in a Spring Boot app?
- [ ] What is the difference between anemic and rich domain models?

---

## Observability

- [ ] How do you propagate a correlation ID across microservices for end-to-end tracing?
- [ ] What is MDC (Mapped Diagnostic Context) and how do you use it with structured logging?
- [ ] How do you expose custom business metrics with Micrometer and Prometheus?
- [ ] What is the difference between a counter, gauge, histogram, and summary in Prometheus?
- [ ] How would you trace a single payment request across 5 microservices end-to-end?

---

## Modern Java (17–21)

- [ ] What are sealed classes and how do they improve exhaustive pattern matching?
- [ ] How does pattern matching for `switch` (Java 21) change how you handle polymorphism?
- [ ] What are the common misuses of `Optional`? How should it NOT be used?
- [ ] What are the pitfalls of parallel streams? When should you avoid them?
- [ ] What advanced `Collectors` are available in the Stream API? (groupingBy, teeing, etc.)

---

## REST / API Design

- [ ] What is the Richardson Maturity Model? What does Level 3 (HATEOAS) add?
- [ ] When would you choose gRPC over REST for internal microservice communication?
- [ ] What are the trade-offs of gRPC (proto contracts, streaming) vs REST (discoverability, tooling)?
- [ ] How do you implement API rate limiting? Explain token bucket vs leaky bucket algorithms.
- [ ] How do you design a backward-compatible API change vs a breaking change?

---

## Code Quality / Review

- [ ] How do you integrate SonarQube or SpotBugs into a CI pipeline? What metrics do you track?
- [ ] What do you look for as a senior engineer when reviewing a pull request?
- [ ] How do you enforce architecture rules (e.g., no domain layer importing infrastructure) in code?
- [ ] What is the difference between code coverage and test quality?

---

## Resilience Patterns

- [ ] How do you implement retry with exponential backoff? Why does adding jitter matter?
- [ ] What is the difference between a timeout and a deadline? Why is deadline propagation important across service chains?
- [ ] What is the Bulkhead pattern? When would you use thread-pool isolation vs semaphore isolation in Resilience4j?
- [ ] How do you combine Circuit Breaker + Retry + Timeout in Resilience4j without creating unexpected interactions?
- [ ] What is the difference between fail-fast and fail-silent strategies? When is each appropriate?

---

## Multi-Tenancy

- [ ] What are the main multi-tenancy models: schema-per-tenant, database-per-tenant, shared schema with tenant ID?
- [ ] How do you enforce tenant data isolation at the application level in a shared-schema Spring Boot service?
- [ ] How do you handle tenant-specific configuration (e.g., different payment providers per country) in a microservice?
- [ ] What are the risks of missing tenant context in a async/Kafka consumer thread?

---

## Java Memory Model (Edge Cases)

- [ ] What is safe publication? What are the four ways to safely publish an object to other threads?
- [ ] Is double-checked locking safe in modern Java? What role does `volatile` play in it?
- [ ] What is the difference between `final` field semantics and `volatile` for safe publication?
- [ ] Can a thread see a partially constructed object? Under what conditions?

---

## AI Tooling

- [ ] How do you use AI tools in your daily development workflow?
- [ ] Have you integrated LLM APIs into any services?

---

## Behavioral / Leadership

- [ ] Describe a time you prevented a production incident through code review or architectural feedback.
- [ ] How do you approach onboarding a junior engineer to a complex codebase?
- [ ] How do you handle disagreements on technical direction with peers?

---

## Kotlin (if asked)

> Not a focus area. If raised: "I haven't worked with Kotlin professionally, but given my Java background the transition is straightforward — I'm familiar with the concepts and could pick it up quickly on the job."
