# HireIQ 
> Streamlining interviewer matching and interview scheduling

## 🧭 **Table of Contents**

* 📖 **Overview**
    * 💡 [Our Understanding of the Problem](#-our-understanding-of-the-problem)
    * 👥 [Team Members](#-team-members)
    * 🚧 [Assumptions & Constraints](#-assumptions--constraints)
* 🚀 **Event Storming**
    * 📜 [Event Storming](#-event-storming)
* 🏗️ **Architecture & Design**
    * ✨ [Architectural Characteristics](#-architectural-characteristics)
    * 🗺️ [Architectural Style](#-architectural-style)
    * 🏢 [C4 Architecture](#-c4-architecture)
    * 🌐 [System Context Diagram](#-system-context-diagram)
    * 📦 [Container Diagrams](#-container-diagrams)
    * 🧩 [Component Diagrams](#-component-diagrams)
* 📝 **Architecture Decision Records**
    * 📜 [ADRs](#-architecture-decision-records--adrs-)
* 💻 **Tech Stack**
    * 🛠️ [Tech Stack](#-tech-stack)
* 📦 **Deployment**
    * 🚀 [Deployment](#-deployment)

## 📖 Overview

### 💡 Our Understanding of the Problem

This solution aims to...

* Provide a solution for...
* Address the need for...
* Be developed using...

### 👥 Team Members

* **Balaji Sivakumar**
* **Pradeep Samuel Daniel**
* **Harini V S**

### 🚧️ Assumptions & Constraints
* Assumptions
  * InterviewLogger Integration
    - InterviewLogger will trigger webhooks to the Interview Scheduling System when:
      - A new candidate is shortlisted.
      - A candidate advances to the next interview round.
    - Payload will include following information. This data will be collected offline and made available through the webhook.
      - Interviewee slot preferences
      - Preferred tech stack
      - Other interview-related information
  * MyMindComputeProfile Integration
    - MyMindComputeProfile Events/APIs will be leveraged/built for bulk and incremental load of the profile information carrying skill set and required details to vector database.
  * Communication & Scheduling
    - Email will be the primary communication method for both interviewers and interviewees.
    - Slot preferences and availability will be managed via MindComputeScheduler or an equivalent scheduling tool.
* Constraints:
  * Limited control over external LLMs in terms of latency, downtime. Need explicit handling of rate limits and cost constraints
  * Automatic matching limitation during external system failures - If external systems like Calendar Hub,
    InterviewLogger, or MyMindLeave are unavailable, the platform may not be able to perform automatic match-making or scheduling.
    In such cases, fallback mechanisms (like manual intervention) will need to be taken by recruiters.
  * Limited explainability in AI-driven scheduling - Since match-making and scheduling decisions are influenced by AI agents
    (e.g., LLMs and vector-based retrieval), the reasoning behind certain decisions may not always be fully explainable in
    traditional rule-based terms.
  
## 🚀 Event Storming

We employed Event Storming, a collaborative technique from Domain-Driven Design (DDD), to discover domain requirements and model the system. Our process followed a structured approach: first identifying key domain events, then mapping commands, actors, and their relationships. Through multiple iterations, we derived the major business flows by analyzing the interactions between commands, aggregates, and events.

### Event Storming Legend
![Event Storming Legend](images/event-storming/00-event-storming-legend.png)
### Event Identification
![Event Identification](images/event-storming/01-event-identification.png)
### Command, Event and Actor Identification
![Command, Event and Actor Identification](images/event-storming/03-aggregate-identification.png)
### Flows
After event storming we have narrowed down on the different business flows
#### 1. Starting Interview
![Starting Interview](images/event-storming/flows/01-starting-interview-flow.png)

#### 2. Interviewer Matching
![Interviewer Matching](images/event-storming/flows/02-interviewer-matching-flow.png)

#### 3. Interview Scheduling
![Interview Scheduling](images/event-storming/flows/03-scheduling-interview-round-flow.png)

#### 4. Interview Rescheduling
![Interview Rescheduling](images/event-storming/flows/04-rescheduling-and-manual-selection-flow.png)

#### 5. Interview Process
![Interview Process](images/event-storming/flows/05-interview-process-flow.png)

#### Conclusion
As a result of the event storming excercise we have discovered the domain and the requirements for the solution. we have identified two aggregates listed below as the most significant in terms of definite bounded functionalities and transactional boundaries.

1. Interview
2. Interview Round

for a more detailed report on the different iterations and business flows can be found [here](pages/01-event-storming.md).

## 🏗️ Architecture & Design

### ✨ Architectural Characteristics

![Architectural Characteristics](images/architecture/architecture-characteristics.png)

### 🗺️ Architectural Style

#### Key Architectural Styles

The system is built upon a distributed architecture, incorporating several key styles:

* **Microservices Architecture:** The system is decomposed into a suite of services (as seen in the "Services" container), each handling specific business functions. This promotes:
  * Modularity
  * Independent deployment
  * Scalability
* **API-Driven Architecture:** The system heavily relies on APIs for communication between different components. This enables:
  * Loose coupling
  * Re-usability
  * Integration with external systems
* **Event-Driven Architecture:** The system uses an "Event Bus," suggesting an event-driven approach. Components communicate asynchronously by producing and consuming events. This improves:
  * Scalability
  * Fault tolerance
  * Responsiveness

#### AI Focus

The architecture highlights a strong emphasis on AI:

* **Embedding Service and Vector DB:** These components enable semantic search and retrieval, allowing the system to understand the meaning of text and match candidates or information more effectively.
* **LangFlow and AI Agents:** The system uses a workflow engine (LangFlow) to orchestrate AI agents, automating tasks and decision-making.

#### Summary

In summary, the system employs a distributed, microservices-based architecture with a strong focus on APIs and event-driven communication. It leverages AI components to automate and enhance the recruitment process, providing a modern and efficient solution.

### 🏢 C4 Architecture

A high-level overview of the system architecture using the C4 model.

### 🌐 System Context Diagram

A diagram showing the system and its external interactions.

![HireIQ Application System Context](images/architecture/c4-context-diagram.png)

### 📦 Container Diagrams

![HireIQ Application Containers](images/architecture/c3-container-diagram.png)

### 🧩 Component Diagrams

#### 1. **Interview Service - Scheduling Components**

![Interview Scheduling Components](images/architecture/c3-interview-service-scheduling.png)

#### 2. **Profile Search & Assistant Langflow Agent**

![Profile Search & Assistant Langflow Agent](images/architecture/c3-langflowsevice-assistance.png)

#### 3. **DataPipeline for Vector DB**

![DataPipeline for Vector DB](images/architecture/c3-embedding-component.png)

#### 4. **Interview Service - Interview Invites Handling**

![Interview Service - Interview Invites Handling](images/architecture/c3-external-invites-handling.png)

#### 5. **Insights for Recruiters**

![Insights for Recruiters](images/architecture/c3-insights.png)

## 📝 Architecture Decision Records (ADRs)

* [ADR 1: Choosing the Database](adrs/0001-choosing-the-database.md)
* [ADR 2: Hybrid approach for match-making](adrs/0002-choosing-hybrid-approach-matchmaking.md)
* [ADR 3: Selection of Langflow for AI Agent Creation](adrs/0003-selection-of-langflow-for-ai-agent-creation.md)
* [ADR 4: Vector Database](adrs/0004-vector-database.md)
## 💻 Tech Stack

### 🛠️ Tech Stack

* Programming Language: Python

## 📦 Deployment

### 🚀 Deployment & CI/CD Pipeline Overview

This diagram illustrates the end-to-end CI/CD workflow from code commit to deployment across environments. 
All services are Dockerized, published to a container registry, and automatically deployed through a multi-stage pipeline 
into dev, staging, and production environments with quality gates.

![Deployment Pipeline](images/deployment/ci-cd.png)
