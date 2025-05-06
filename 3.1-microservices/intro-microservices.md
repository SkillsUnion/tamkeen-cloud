# **Introduction to Microservices**

## **What Are Microservices?**

**Microservices** are an architectural style where an application is structured as a collection of small, loosely coupled, and independently deployable services. Each service is aligned with a specific business function (e.g., user service, order service, payment service) and communicates over lightweight protocols like HTTP REST, gRPC, or asynchronous message queues (e.g., SQS, Kafka).


This approach contrasts with traditional monolithic applications, where all features are combined into a single codebase and deployment unit.

**Core Characteristics of Microservices**:
- **Independent Deployability**: Each service can be deployed on its own timeline.
- **Domain-Driven**: Services map to business capabilities.
- **Technology Agnostic**: Teams can use different programming languages, frameworks, or databases.
- **Resilient**: Failure in one service does not bring down the entire system.
- **Loosely Coupled & Highly Cohesive**: Each service is designed to do one thing well.

> **Quote**: “The microservice architectural style is an approach to developing a single application as a suite of small services…” — Martin Fowler

---

## **What Is a Monolith?**

A **monolithic application** is built as a single, unified unit where all components—user interface, business logic, and data access—are interconnected and deployed together. It's the traditional software architecture model and often the starting point for many early-stage applications.

{% include youtube.html id="IwT_pBcDmSI" %}

**Example**:  
In an e-commerce monolith, features like user authentication, product listing, checkout, and payment processing all reside in the same codebase and are deployed simultaneously.

**Key Characteristics**:
- **Single Codebase**: All modules and features live together.
- **Tightly Coupled**: Changes in one part may affect others.
- **Single Deployment Unit**: Even minor changes require redeploying the entire application.
- **Easier to Start**: Simpler to build, test, and deploy initially.

**When Monoliths Work Well**:
- Small teams or early-stage startups.
- Projects with limited scope or simpler domains.
- When speed of development matters more than scalability.

However, as complexity grows, monoliths often face challenges with team scaling, slow deployments, codebase maintainability, and risk of system-wide failure.

---

## **Monolith vs Microservices**

| Attribute           | Monolithic Architecture               | Microservices Architecture                     |
|---------------------|----------------------------------------|------------------------------------------------|
| Deployment           | Single deployment unit                | Independent deployments per service            |
| Scaling              | Entire application                    | Per service                                    |
| Development Speed    | Slower in large teams                 | Faster with small, autonomous teams            |
| Technology Choice    | Typically homogenous                  | Polyglot allowed per service                   |
| Fault Isolation      | Single point of failure               | Failure isolated to specific services          |
| Onboarding Time      | Long (entire codebase)                | Short (specific service only)                  |

**Illustration**:
- *Monolith*: All logic in one unit (UI, business logic, data access).
- *Microservices*: Independent services connected over APIs.


{% include youtube.html id="NdeTGlZ__Do" %}

---

## **Benefits of Microservices**

- **Agility**: Teams can develop, test, and deploy services independently.
- **Scalability**: Each service can scale based on its specific load.
- **Fault Isolation**: Crashes in one service don't affect the others.
- **Continuous Delivery**: Easier to automate testing and deployment of small services.
- **Tech Diversity**: Teams can experiment or optimize using different technologies.

This modularity helps large organizations evolve faster without being bottlenecked by centralized teams or large legacy codebases.


{% include youtube.html id="lTAcCNbJ7KE" %}

---

## **Challenges and Trade-Offs**

While microservices solve many problems of monoliths, they also introduce new complexities:

- **Operational Overhead**: More services = more deployments, configs, logs, and monitoring needs.
- **Network Latency**: Service-to-service calls add latency and may fail.
- **Distributed Complexity**: Harder to trace bugs across services.
- **Data Consistency**: No single database; managing distributed transactions is non-trivial.
- **Deployment Management**: Requires orchestration (ECS, Kubernetes, etc.)

> Adopting microservices requires strong DevOps maturity: CICD pipelines, infrastructure as code, centralized logging, and distributed tracing.

---

## **Real-World Use Cases**

- **Netflix**: Broke their monolithic DVD rental system into hundreds of microservices to serve millions of users globally, enabling dynamic scaling and high availability.
- **Amazon**: Scaled by decomposing their application into independent services, each owned by small "two-pizza" teams.
- **Uber**: Migrated from a monolith to microservices to meet rapid geographic expansion and product complexity.

These companies embraced microservices to scale teams, codebases, and customer experiences simultaneously.

---

## **Key Concepts to Understand**

- **Service Granularity**: Finding the right size and scope for a service.
- **Bounded Context**: A DDD (Domain-Driven Design) principle to define service boundaries.
- **API Contracts**: Clear communication rules between services; usually enforced with OpenAPI specs.
- **Service Registry**: Mechanism to register and discover services (e.g., AWS Cloud Map, Consul).
- **API Gateway**: A front door to all services—handles routing, authentication, throttling.

---

## **Recommended Reading**

### **Core Concepts**
1. [Martin Fowler – Microservices](https://martinfowler.com/articles/microservices.html)
2. [AWS – Microservices Whitepaper](https://docs.aws.amazon.com/whitepapers/latest/microservices-on-aws/microservices-on-aws.pdf)
3. [12 Factor App – Building Cloud-Native Microservices](https://12factor.net/)

### **Case Studies**
6. [Netflix Technology Blog – Evolution of Microservices](https://netflixtechblog.com/tagged/microservices)
7. [Amazon Builders’ Library – Decomposing Services](https://aws.amazon.com/builders-library/)

### **Optional Videos**
- [GOTO Conference – The Evolution of Microservices at Netflix](https://www.youtube.com/watch?v=57UK46qfBLY)

---