# 🧩 HireIQ C4 Component Diagrams – Summary

This document provides a breakdown of the key components across multiple sub-systems in the HireIQ Interview matching and 
scheduling system. It covers scheduling automation, LangFlow-based agents, vector DB pipelines, and insights processing.

---

## 1. 📅 Interview Scheduling Components 

![Interview Scheduling Components](../c4-interview-service-scheduling.png)

- Triggers from InterviewLogger for new candidates or round progression initiate scheduling.
- LangFlow Assistant coordinates LLM, vector search, and availability lookups.
- Matches interviewers based on skill, experience, and preferences.
- Schedules the interview and updates internal state and event bus.

---

## 2. 🤖 LangFlow – Profile Search & Assistance Agent

![LangFlow – Profile Search & Assistance Agent](../c4-interview-service-scheduling.png)

- Handles recruiter prompts for skill search or general assistance via chatbot.
- Router component directs intent to profile matcher, assistant, or fallback.
- Uses vector DBs (skills + knowledge) to retrieve relevant profiles or guidance.
- Supports graceful fallback and multi-LLM support for intent routing.

---

## 3. 🔁 Embedding Service – Vector DB Pipeline

![Embedding Service – Vector DB Pipeline](../c4-interview-service-scheduling.png)

- MyMindComputeProfile sends profile data (incremental + full load).
- Embedding Service uses transformer models to convert text to vectors.
- Embeddings are stored in the vector DB to support downstream semantic search.
- Powers LangFlow agents for intelligent profile matching.

---

## 4. 📨 Interview Invite Handling (`c4-external-invites-handling.png`)

![Interview Invite Handling](../c4-interview-service-scheduling.png)

- Interview Service sends out calendar invites via Calendar Hub API.
- Webhooks notify the system on accept/reject actions.
- Events are processed to update the interview status in the DB and sync with InterviewLogger.
- Ensures round progression is tightly coupled with calendar status.

---

## 5. 📊 Insights for Recruiters (`c4-insights.png`)

![Insights for Recruiters](../c4-interview-service-scheduling.png)

- Ingests data from Interview Service, InterviewLogger, MindComputeScheduler, etc.
- Business Event Emitters and external ingestors populate the analytical DB.
- Insights Service exposes metrics, dashboards, and real-time interview views.
- Supports both dashboard queries and system KPIs using a query engine.

---

