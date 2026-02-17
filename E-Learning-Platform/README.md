# AI-Powered Adaptive Learning Platform – ERD

## Overview

This project models a scalable, AI-driven educational platform designed to support personalized learning experiences. The ERD captures core domains including course delivery, assessment management, student progress tracking, risk analysis, and adaptive recommendations.

The focus is strictly on **database structure and domain modeling**—not implementation details.

---

## Actors

- **Student**: Learns courses, takes assessments, receives recommendations
- **Instructor**: Creates and manages courses, modules, and lessons
- **Admin**: Manages platform configuration and user roles

---

## Core Domains & Requirements

### 1. User Management

- Unified `User` entity with role-based access (Student, Instructor, Admin)
- Separate profile tables (`StudentProfile`, `InstructorProfile`) linked 1:1 to `User`
- Soft delete support for user accounts

### 2. Course & Content Structure

- Hierarchical content model: `Course` → `Module` → `Lesson`
- Instructors own and manage their courses
- Students enroll via `CourseEnrollment` (many-to-many with composite uniqueness on `(student_id, course_id)`)

### 3. Assessment System

- Assessments attached to lessons with multiple questions
- Questions support multiple answer options with designated correct answers
- Immutable `AssessmentAttempt` records per student per assessment
- `StudentAnswer` tracks selected options and awarded scores per question

### 4. Learning Progress Tracking

- Aggregate root `LearningProgress` (one per student per course) tracking:
  - Overall completion percentage
  - Engagement score (derived from activity frequency/duration)
  - Last activity timestamp
- Append-only `StudySession` log capturing duration and activity count for analytics

### 5. AI-Powered Risk Analysis

- Periodic `RiskProfile` snapshots per student containing:
  - `RiskScore` (numerical) and `RiskLevel` (e.g., Low/Medium/High)
  - Timestamp of calculation (`calculated_at`)
- `RiskFactor` entities explain contributors to risk (e.g., "low engagement", "missed deadlines")
- `AlertHistory` tracks notifications sent to instructors/admins
- `InterventionPlan` for high-risk students (status-tracked mitigation strategy)

### 6. Personalized Recommendations

- Snapshot-based `Recommendation` entities generated periodically:
  - Priority level and status (e.g., Active, Completed)
  - Timestamp of generation
- Linked entities provide actionable guidance:
  - `RecommendedContent`: Specific lessons/modules to review
  - `StudyPlan`: Time-bound learning schedule
  - `SkillGapAnalysis`: Proficiency vs. target level per skill

---

## Key Design Decisions

| Decision                                  | Rationale                                                                                 |
| ----------------------------------------- | ----------------------------------------------------------------------------------------- |
| **Snapshot-based Risk & Recommendations** | Preserves historical state for auditing and trend analysis; avoids mutable aggregates     |
| **Separate Profile Tables**               | Normalizes role-specific attributes; avoids sparse columns in `User`                      |
| **Immutable Assessment Attempts**         | Ensures academic integrity; enables reliable analytics on performance trends              |
| **Aggregate Root for Progress**           | Centralizes derived metrics (`OverallProgress`, `EngagementScore`) for efficient querying |
| **Append-Only Study Sessions**            | Enables accurate activity analytics without update anomalies                              |

---

## Constraints & Assumptions

- Risk profiles and recommendations are generated asynchronously by AI services (not modeled in ERD)
- Assessment scoring logic is external to the schema (stored results only)
- Course content (videos, text) is stored externally; schema references only metadata
- All core entities support soft deletion for audit compliance

---

## Design Characteristics

- Follows Domain-Driven Design (DDD) principles with clear aggregate boundaries
- Composite uniqueness constraints enforced where business rules require it
- Designed for horizontal scalability (e.g., partitioning by `student_id` or `course_id`)
- Extensible for future features (badges, social learning, live sessions)

---

> 💡 **Note**: This is a conceptual data model created for system design practice. Implementation details (indexes, partitioning, caching) would be addressed during actual development.

---

© 2026 Mohamed Abdelfattah  
_All Rights Reserved_
