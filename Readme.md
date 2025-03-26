# HireIQ 
> AI-Powered Interview Matching and Scheduling Solution

## 🧭 **Table of Contents**

* 📖 **Overview**
    * 💡 [Our Understanding of the Problem](#-our-understanding-of-the-problem)
* 🚀 **Event Storming**
    * 📜 [Event Storming](#-event-storming)
* ✅ **NFR and Assumptions**
  * ⚡ [Non-Functional Requirements](#-non-functional-requirements)
  * 🚧 [Assumptions & Constraints](#-assumptions--constraints)
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
* 👥 **Team Members**
    * 👥 [Team Members](#-team-members)

## 📖 Overview

### 💡 Our Understanding of the Problem

**The Challenge**

The core problem is the significant inefficiency and complexity faced by MindCompute recruiters in scheduling technical interviews. The current process is manual, fragmented, and lacks the necessary integration and automation. This results in several key issues:

* **Inefficient Interviewer Identification:** Recruiters struggle to find the right interviewers with the necessary skills and availability.
* **Scheduling Conflicts and Manual Coordination:** The back-and-forth coordination between interviewers and interviewees leads to frequent errors and delays.
* **Lack of Integration and Data Visibility:** The absence of streamlined integration with existing systems hinders the flow of information and makes it difficult to track the interview process.
* **Lack of Automated Communication:** Manual communication introduces delays and the potential for miscommunication.
* **Difficult Reporting and Performance Tracking:** The inability to easily generate reports makes it hard to identify bottlenecks and improve the process.

**Our Proposal**

* These issues result in a time-consuming, error-prone, and frustrating experience for both recruiters and interviewees, ultimately impacting the efficiency of the hiring process.
* To address these issues and streamline the interview scheduling process, we propose an AI-powered interview scheduling solution that leverages automation, AI agents, and integration with existing systems. 
* The sections to follow capture the event storming, architecture, and design decisions made to build this solution.
  
## 🚀 Event Storming

We employed Event Storming, a collaborative technique from Domain-Driven Design (DDD), to discover domain requirements and model the system. Our process followed a structured approach: first identifying key domain events, then mapping commands, actors, and their relationships. Through multiple iterations, we derived the major business flows by analyzing the interactions between commands, aggregates, and events.

**What is Event Storming?** A collaborative workshop format for domain exploration that brings together domain experts and technical team members to create a shared understanding of business processes.

**Benefits:**
- Creates a common language between technical and business stakeholders
- Provides a visual representation of complex business processes
- Helps identify bounded contexts and aggregate roots for domain-driven design
- Enables quick exploration of business processes without technical details
- Surfaces inconsistencies and gaps in understanding early

### Event Storming Legend
![Event Storming Legend](images/event-storming/00-event-storming-legend.png)

Event Storming uses a standardized set of colored sticky notes to represent different elements of the business domain:
- **Orange**: Domain Events - Something that happened in the system
- **Blue**: Commands - Actions that trigger domain events
- **Yellow**: Actors - Users or systems that issue commands
- **Purple**: Policies - Business rules that react to events
- **Pink**: Aggregates - Clusters of related commands and events
### Event Identification
![Event Identification](images/event-storming/01-event-identification.png)
### Command, Event and Actor Identification
![Command, Event and Actor Identification](images/event-storming/03-aggregate-identification.png)
### Business Flows
After event storming, we identified five key business flows that represent the core processes of our system. Each flow consists of commands (actions), events (outcomes), and policies (business rules) that govern the process.
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
Through the event storming exercise, we discovered the domain and requirements for our solution. We identified two key aggregates that define our bounded contexts and transactional boundaries:

1. **Interview** - Manages the overall interview process for a interviewee
2. **Interview Round** - Handles individual interview sessions within the process

The event storming process helped us develop a ubiquitous language - a common vocabulary shared by all team members and stakeholders that eliminates translation between business and technical terminology.

For a more detailed report on the different iterations, business flows, and the complete event storming analysis, see [our detailed event storming documentation for HireIQ](pages/01-event-storming.md).

## ✅ NFR and Assumptions

### 🚧️ Assumptions & Constraints
* Assumptions
  * InterviewLogger Integration
    - InterviewLogger will trigger webhooks to the Interview Scheduling System when:
      - A new interviewee is shortlisted.
      - A interviewee advances to the next interview round.
    - Payload will include following information. This data will be collected offline and made available through the webhook.
      - Interviewee slot preferences
      - Preferred tech stack
      - Other interview-related information
  * MyMindComputeProfile Integration
    - MyMindComputeProfile Events/APIs will be leveraged/built for bulk and incremental load of the profile information carrying skill set and required details to vector database.
  * Communication & Scheduling
    - Email will be the primary communication method for both interviewers and interviewees.
    - Slot preferences and availability will be managed via MindComputeScheduler or an equivalent scheduling tool.
  * All interview invites will be sent from a generic system-owned email ID (e.g., recruitment-tw-noreply@gmail.com).
    This email ID will be used to create and manage calendar events, and will have Calendar Hub webhooks configured to
    listen for acceptance or rejection responses from both interviewees and interviewers.
* Constraints:
  * Limited control over external LLMs in terms of latency, downtime. Need explicit handling of rate limits and cost constraints
  * Automatic matching limitation during external system failures - If external systems like Calendar Hub,
    InterviewLogger, or MyMindLeave are unavailable, the platform may not be able to perform automatic match-making or scheduling.
    In such cases, fallback mechanisms (like manual intervention) will need to be taken by recruiters.
  * Limited explainability in AI-driven scheduling - Since match-making and scheduling decisions are influenced by AI agents
    (e.g., LLMs and vector-based retrieval), the reasoning behind certain decisions may not always be fully explainable in
    traditional rule-based terms.

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

* **Embedding Service and Vector DB:** These components enable semantic search and retrieval, allowing the system to understand the meaning of text and match interviewees or information more effectively.
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
* [ADR 5: Architectural Characteristics](adrs/0005-architectural-characteristics.md)

## 💻 Tech Stack

### 🛠️ Tech Stack

![Tech Stack](images/techstack/techstack.png)

## 📦 Deployment

### 🚀 Deployment & CI/CD Pipeline Overview

This diagram illustrates the end-to-end CI/CD workflow from code commit to deployment across environments. 
All services are Dockerized, published to a container registry, and automatically deployed through a multi-stage pipeline 
into dev, staging, and production environments with quality gates.

![Deployment Pipeline](images/deployment/ci-cd.png)

## 👥 Team Members

* **Balaji Sivakumar**
* **Pradeep Samuel Daniel**
* **Harini V S**