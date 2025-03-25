# Your Main Project Heading

## 🧭 **Table of Contents**

* 📖 **Overview**
    * 💡 [Our Understanding of the Problem](#-our-understanding-of-the-problem)
    * 👥 [Team Members](#-team-members)
    * 🚧 [Assumptions & Constraints](#-assumptions--constraints)
* 🚀 **Event Storming**
    * 📜 [Event Storming](#-event-storming)
* 🏗️ **Architecture & Design**
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

## 🏗️ Architecture & Design

### 🏢 C4 Architecture

A high-level overview of the system architecture using the C4 model.

### 🌐 System Context Diagram

A diagram showing the system and its external interactions.

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

## 💻 Tech Stack

### 🛠️ Tech Stack

* Programming Language: Python

## 🧪 Testing

### 🔬 Test Cases

* Unit tests for core components.
* Integration tests for API endpoints.
* End-to-end tests for user flows.

## 📦 Deployment

### 🚀 Deployment

![Deployment Pipeline](images/deployment/ci-cd.png)
