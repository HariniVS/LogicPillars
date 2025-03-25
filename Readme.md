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

* Assumptions:
    * InterviewLogger System will invoke webhooks set up in the interview service for 2 actions
      * New Candidate short-listed for the recruitment process
      * Existing Candidate advanced to the next round
    * WebHooks invoked by InterviewLogger will carry the interviewee slot preferences, preferred tech stack and other required information for the interview process. This will be captured using offline process and made available through the WebHooks 
    * MyMindComputeProfile Events/APIs will be leveraged/built for bulk and incremental load of the profile information carrying skill set and required details to vector database.
    * Email be used as the primary means of communication for both Interviewer and Interviewee. The preferences will be captured and managed through MindComputeScheduler or equivalent system.

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
