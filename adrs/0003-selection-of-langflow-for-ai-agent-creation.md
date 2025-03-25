# ADR-0003: Selection of Langflow for AI Agent Creation

**Status:** Accepted

## Context

We need to select a suitable tool or framework for building AI agents to streamline and enhance the interview process. Several options have been considered, including LangChain, AutoGen, Azure AI Agent Service, and Vertex AI Agent Builder. This ADR focuses on the decision to use Langflow.

## Options considered

* **LangFlow:** A visual, low-code tool for building agentic applications.
* **LangChain (code-first):** Offers maximum flexibility but requires more extensive coding.
* **AutoGen:** Strong for building collaborative multi-agent systems but might have a steeper learning curve for initial prototyping.
* **Azure AI Agent Service:** A fully managed cloud service that simplifies deployment but could lead to vendor lock-in.
* **Vertex AI Agent Builder:** Emphasizes ease of use and data grounding but might offer less customization compared to Langflow.

## Decision

We have decided to use Langflow as the primary tool for creating AI agents for our application.

## Rationale

 - Langflow provides a visual, low-code approach for building agentic applications, which can significantly accelerate the development and prototyping of AI agent workflows 
 - Its user-friendly interface simplifies the integration of Large Language Models (LLMs) into our application
 - By utilizing Langflow, we can leverage the modularity and extensive integrations offered by LangChain without the need for extensive coding.
 - This ease of use and visual nature can empower a broader team, including members with varying levels of coding expertise, to contribute to the development of these AI agents
 - Furthermore, Langflow grants us access to a wide array of functionalities such as prompt engineering, Retrieval Augmented Generation (RAG), and memory management, which are essential for creating effective AI agents

## Consequences

* **Positive:**
    * Faster development and prototyping of AI agents due to the visual interface.
    * Lower barrier to entry for team members with less coding experience.
    * Access to the comprehensive ecosystem and capabilities of LangChain.
    * Facilitates easier collaboration between technical and non-technical team members.
* **Negative:**
    * May present limitations in handling highly complex or custom logic compared to a purely code-based approach.
    * Reliance on the ongoing development and support of the Langflow project.
    * Potential costs associated with the underlying LLMs utilized.