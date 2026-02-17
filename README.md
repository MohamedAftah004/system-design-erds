# System Design ERDs

This repository contains a curated collection of **Entity-Relationship Diagram (ERD) designs** created while practicing and refining system design and data modeling skills.

The focus is on translating real-world business requirements into structured, scalable, and extensible database schemas—without framework or ORM bias.

---

## Purpose

This repository serves to:

- Practice real-world data modeling from requirements to schema
- Deepen understanding of relationships, constraints, and normalization
- Design with scalability and future extensibility in mind
- Document design decisions and trade-offs transparently

All ERDs are **conceptual designs** focused purely on data modeling—not implementation artifacts.

---

## Case Studies

| System                                                      | Domain         | Key Focus Areas                                                                       |
| ----------------------------------------------------------- | -------------- | ------------------------------------------------------------------------------------- |
| [`maintenance-service-system`](maintenance-service-system/) | Field Services | Request lifecycle, approval workflows, technician assignment, soft deletes            |
| [`e-learning-platform`](e-learning-platform/)               | EdTech         | Adaptive learning, progress tracking, AI-driven risk analysis, recommendation engines |

---

## Design Philosophy

Across all case studies, I consistently apply these principles:

✅ **Requirement-Driven**  
Start strictly from business requirements—no premature optimization or speculative tables.

✅ **Extensible State Management**  
Model states (e.g., request status, risk levels) as tables—not enums—to support future changes.

✅ **Relationship Integrity**  
Use proper cardinalities (1:N, M:N) with explicit junction tables where needed.

✅ **Auditability**  
Track historical changes (status transitions, attempts, sessions) via append-only tables.

✅ **Production-Readiness**  
Incorporate soft deletes, composite uniqueness constraints, and snapshot-based modeling where appropriate.

---

## Notes

These designs are part of an ongoing learning journey. As my understanding of system design evolves, so will these models.

Constructive feedback and suggestions are always welcome.

---

© 2026 Mohamed Abdelfattah  
_All designs are conceptual and for educational purposes._
