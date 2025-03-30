# ADR-0002: Choosing hybrid approach for match making of interviewer

* **Status:** Accepted

## Context

The interview scheduling system requires the capability to intelligently select the most suitable interviewer from a pre-filtered set of interviewers, by matching them against the interviewee's information and requirements.

The process is orchestrated through Lang Flow Agents. As predecessor for match-making the interviewer profiles are already filtered based on skill set, experience and availability. 

The key system requirements include:
- High accuracy in match-making
- High performance at scale
- Maintainable

## Options Considered

- LLM only approach
- Rule based or algorithm only approach
- Hybrid approach: Combine LLM reasoning with deterministic algorithm

## Decision

Hybrid approach: Combine LLM reasoning with deterministic algorithm

## Rationale

- Best of best worlds: LLMs handle ambiguity and edge cases, while algorithms ensure performance and explainability.
- Extensibility: Rules can evolve independently from prompts, and LangFlow chains can orchestrate both paths.
- Fallback support: If LLM response confidence is low or ambiguous, fallback to deterministic score-based matches.

## Consequences

- Design complexity increases: Orchestration logic to decide when to use LLM, algorithm, or both.
- Sensitive information should be masked when adding context to the LLM during match-making
