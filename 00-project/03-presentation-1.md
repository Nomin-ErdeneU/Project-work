
---
project_outline: "[[00-project/01-project-outline]]"
---

<!-- 5xl -->
# Language Learning Assistant with Individual Progress Tracking

Author: Nomin-Erdene Ugiidalai  
Neptun: E8671V  
Supervisor:  Anett LENART 
Project ID: 2026-LA-05  

---

<!-- 2xl -->
## The Problem

- When studying languages, learners usually review all words equally, which is inefficient.
- Traditional apps lack smart, personalized repetition based on individual mistakes and study gaps.
- Client-side selection logic can be unreliable and doesn't utilize centralized database performance.

---

<!-- 2xl -->
## Target Users

- **Language Learners:** Students studying foreign languages who need a smart, personalized vocabulary practice queue.
- **Course Administrators:** Instructors who maintain learning content, vocabulary items, and difficulty levels.

---

<!-- 2xl -->
## Planned Scope

- **Database Core:** At least 10 normalized tables (3NF) modeling users, items, practice sessions, and attempts.
- **Procedural Logic:** Database stored procedures (PL/SQL or T-SQL) handling rule-based and priority selection algorithms.
- **Data & Performance:** Test data generation and query execution optimization using database plans.
- **Application Interface:** A clean web interface connected to the database logic for taking practice sessions.

---

<!-- 2xl -->
## Initial User Journeys

1. **Start Practice:** Learner logs in and starts a session $\rightarrow$ database stored procedure computes priorities and returns the next words.
2. **Submit Answers:** Learner answers an exercise $\rightarrow$ system logs the result $\rightarrow$ database updates repetition counters and intervals.
3. **Track Progress:** Learner opens the dashboard $\rightarrow$ database executes queries to show accuracy trends over time.

---

<!-- 2xl -->
## Next Steps

- Finalize the database table structure and relationships.
- Develop the database stored procedures for word selection.
- Create sample test data for performance testing.
