# 🏗️ **3-Month System Design + Distributed Systems + Cloud Architecture Study Plan**

---

# 📆 Month 1: System Design Core + Basics of Distributed Systems

## **Week 1: Introduction to System Design**

- 🎯 Topics:
  - System Design Basics (Latency, Throughput, Scalability, Availability)
  - Load Balancers (L4 vs L7, HAProxy, AWS ALB)
- 📚 Resources:
  - _System Design Interview Vol 1_ — Alex Xu (Ch 1-2)
  - [High Scalability Blog](http://highscalability.com/)
  - [Load Balancing Explained](https://youtu.be/-nYh5c4e9V4)
- ✅ Tasks:
  - Write notes on trade-offs: latency vs throughput
  - Sketch Load Balancer deployment in a simple system (e.g., Web App)

---

## **Week 2: Caching Strategies Deep Dive**

- 🎯 Topics:
  - Read/Write Caching
  - CDN vs Application Cache
  - Cache Invalidation Patterns
- 📚 Resources:
  - _System Design Interview Vol 2_ — Caching Chapter
  - [AWS Caching Guide](https://aws.amazon.com/caching/)
- ✅ Tasks:
  - Design a system with Redis caching layer (e.g., user profile cache)
  - Answer: When does caching hurt performance?

---

## **Week 3: Databases and Storage**

- 🎯 Topics:
  - SQL vs NoSQL Databases
  - Indexing Strategies
  - RDBMS Internals (ACID properties)
- 📚 Resources:
  - _Designing Data-Intensive Applications_ — Ch 3-5
  - [MongoDB NoSQL Explanation](https://www.mongodb.com/nosql-explained)
- ✅ Tasks:
  - Build ER diagram for a simple service (e.g., Instagram user & posts)

---

## **Week 4: Rate Limiting and APIs**

- 🎯 Topics:
  - API Gateway Design
  - Rate Limiting (Leaky Bucket, Token Bucket)
- 📚 Resources:
  - [KongHQ Rate Limiting Design](https://konghq.com/blog/how-to-design-a-rate-limiting-algorithm/)
  - _System Design Interview Vol 2_ — API Rate Limiting Chapter
- ✅ Tasks:
  - Sketch API Gateway in a service diagram.
  - Build pseudocode for Token Bucket algorithm.

---

# 📆 Month 2: Distributed Systems Core + Cloud Basics

## **Week 5: CAP Theorem and PACELC**

- 🎯 Topics:
  - CAP Trade-offs
  - PACELC Theorem (Latency vs Consistency)
- 📚 Resources:
  - _DDIA_ — Ch 8
  - [PACELC Explained](https://medium.com/@abhisheksingh/understanding-pacelc-theorem-6b9f5698d00b)
- ✅ Tasks:
  - Pick 3 systems (e.g., DynamoDB, Cassandra, MongoDB) — Identify their CAP properties.

---

## **Week 6: Consensus Algorithms**

- 🎯 Topics:
  - Paxos and Raft Deep Dive
  - How Leader Election Works
- 📚 Resources:
  - _Distributed Systems_ — Tanenbaum (Ch 5)
  - [The Secret Lives of Data - Raft Demo](http://thesecretlivesofdata.com/raft/)
- ✅ Tasks:
  - Simulate Raft Leader Election (paper exercise).

---

## **Week 7: Distributed Transactions and Event-Driven Systems**

- 🎯 Topics:
  - Two-Phase Commit (2PC), Three-Phase Commit (3PC)
  - Saga Pattern: Choreography vs Orchestration
- 📚 Resources:
  - _Designing Distributed Systems_ — Brendan Burns
  - [Microservices.io - Saga Pattern](https://microservices.io/patterns/data/saga.html)
- ✅ Tasks:
  - Create a flow diagram for Saga-based order processing.

---

## **Week 8: Service Discovery and Distributed Coordination**

- 🎯 Topics:
  - Eureka, Consul, ZooKeeper Basics
  - Heartbeats, TTLs
- 📚 Resources:
  - [Service Discovery Patterns](https://learn.microsoft.com/en-us/azure/architecture/patterns/service-discovery)
- ✅ Tasks:
  - Sketch simple Service Discovery Diagram.

---

# 📆 Month 3: Cloud Architecture + Advanced Topics (Observability, Security)

## **Week 9: Microservices Patterns**

- 🎯 Topics:
  - API Gateway
  - BFF Pattern
  - Database per Service Pattern
- 📚 Resources:
  - _Building Microservices_ — Sam Newman
  - [Microsoft Microservices Guide](https://learn.microsoft.com/en-us/azure/architecture/microservices/)
- ✅ Tasks:
  - Draw Microservices diagram for an E-commerce system.

---

## **Week 10: Serverless and Event-Driven Architectures**

- 🎯 Topics:
  - Serverless Basics
  - Event-Driven Design (SNS/SQS/Kafka)
- 📚 Resources:
  - _Cloud Native Patterns_ — Cornelia Davis
  - [Serverless Patterns Collection](https://serverlessland.com/patterns)
- ✅ Tasks:
  - Design serverless backend for Image Upload Service.

---

## **Week 11: Observability & Reliability Engineering**

- 🎯 Topics:
  - Metrics, Logs, Traces
  - Distributed Tracing (OpenTelemetry, Jaeger)
  - Circuit Breaker, Retry, Bulkhead Patterns
- 📚 Resources:
  - _Site Reliability Engineering_ (Google SRE Book) — Monitoring Chapter
  - [Prometheus Monitoring Docs](https://prometheus.io/docs/introduction/overview/)
- ✅ Tasks:
  - Setup Prometheus + Grafana locally and track simple API.

---

## **Week 12: Security and Final Real-World Designs**

- 🎯 Topics:
  - OAuth2 / OpenID Connect
  - TLS/mTLS in Microservices
  - Secrets Management
- 📚 Resources:
  - _Security Engineering_ — Ross Anderson (Selected Chapters)
  - [Google Zero Trust Security Basics](https://cloud.google.com/zero-trust)
- ✅ Tasks:
  - Design a secure Authentication System using OAuth2.

---

# 🎯 At the End of 3 Months:

- You’ll know **theory + real world patterns**.
- You’ll **build**, **draw**, and **simulate** real distributed cloud systems.
- You’ll be ready for **serious interviews** (FAANG / Cloud Architect roles).

---

# 🧠 BONUS Weekly Habit

- 2 hours Reading 📖
- 2 hours Video Learning 🎥
- 2 hours Practical Building/Whiteboarding 🛠️
- 1 hour Summary / Revision 📝

---

# 📈 Quick View Progress Tracker

| Week | Focus                 | Practical                       |
| :--- | :-------------------- | :------------------------------ |
| 1-4  | System Design         | Small System Sketches           |
| 5-8  | Distributed Systems   | Flow Diagrams, Algorithms       |
| 9-12 | Cloud + Observability | Deploy, Monitor, Secure Systems |
