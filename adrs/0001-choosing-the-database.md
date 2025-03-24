# ADR-0001: Choosing relational database for interview scheduling information

* **Status:** Accepted

## Context

The automatic interview scheduling application requires a database to store the interview scheduling information including:
- Interview and associated Interview Rounds information and associated meta data
- Interview Round holding the participant information - Interviewer, Interviewee locked timeslots, tech stack and round information
- Status for the Interview and Interview Rounds

The key system requirements include:
- Transactional consistency for the scheduling and rescheduling interviews
- Support for queries, filters and joins across tables
- Referential integrity between tables
- Support for capturing the CDC to enable 

## Decision

Relational Database as the primary datastore for persisting the transactional information in the platform

## Rationale

- Structured Schema: The information to be persisted naturally fits to normalized data structures
- ACID Transaction: Relational databases provided strong ACID compliance
- Query Support: SQL provides matured querying and indexing capabilitites joining multiple tables
- Community Support: Widely adopted and strong community support available with matured ecosystem
- CDC Compatability: Relational databases support CDC mechanisms (ex: Debezium) for streaming changes to other systems

## Consequences

- RDMS scales vertically by default. If the dataset grows rapidly properly scaling techniques should be applied to scale the system (ex: partionioning, views, read replicas etc)
- Sensitive information should be encryted and follow GDPR complaint storage mechanisms
