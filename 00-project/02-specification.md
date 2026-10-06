---
project_outline: "[[00-project/01-project-outline]]"
---

# Language Learning Assistant with Individual Progress Tracking

## 1. Actors and permissions
| Role | Needs | Responsibility / access |
| --- | --- | --- |
| Learner | Practice vocabulary/grammar and view personal progress | Starts practice sessions, submits answers, views statistics |
| Administrator | Manage content and monitor system performance | Adds/updates learning items, topics, and difficulty levels |

## 2. Use cases / user stories
### Start practice session and process answers
- **Actor:** Learner
- **Precondition:** The learner is logged into the application.
- **Main flow:**
  1. The learner requests a new practice session.
  2. The system calls a database stored procedure to compute priority scores and retrieve the next item sequence.
  3. The learner submits an answer for an exercise.
  4. The system records the attempt, updates the user's learning state, and recalculates item priority.
  5. The system shows immediate feedback and the next exercise item.
- **Alternative flow:** If no new items are due, the system provides review items based on weighted performance history.

## 3. Functional requirements
| Requirement | Acceptance criteria | Priority |
| --- | --- | --- |
| Database-side item selection | Given a user's practice history, when a session is initiated, the database stored procedure generates a practice sequence based on past accuracy and interval. | Must |
| Answer recording and history tracking | Given a submitted answer, the database logs correctness, time taken, attempt timestamp, and updates repetition counters. | Must |
| Normalized data storage | Given system data, the schema must implement at least 10 normalized tables (3NF) enforcing referential integrity. | Must |
| Multiple selection strategies | Given system configuration, the database provides at least two practice selection algorithms (rule-based and weighted-priority). | Must |
| User progress reporting | Given a learner's history, the database executes complex aggregation queries to present accuracy and mastery over time. | Must |

Priority: **Must** = required for the final product; **Should** = important; **Could** = optional if time permits.

## 4. Business rules and constraints
| Rule or constraint | Rationale |
| --- | --- |
| Selection logic must execute inside the database | Core requirement of the project brief; the frontend serves strictly as an execution interface. |
| Spaced repetition intervals increase upon correct answers | Encourages retention by reducing frequency for mastered items. |
| Incorrect answers lower item priority score immediately | Ensures weak vocabulary or concepts are re-queued rapidly. |

## 5. Non-functional requirements
| Requirement | How it will be verified |
| --- | --- |
| Scalable stored procedure performance | Query execution times measured across tens of thousands of generated test history records. |
| Query optimization | Performance of at least 5 complex queries compared before and after indexing using database execution plans (`EXPLAIN PLAN` / `Actual Execution Plan`). |

## 6. Initial technical proposal
### Technology direction
| Area | Candidate technology / approach | Reason for consideration |
| --- | --- | --- |
| Database | Oracle Database (PL/SQL) or MS SQL Server (T-SQL) | Required procedural language capabilities for database-side logic. |
| Frontend Interface | Simple Web application (C# / Web interface) | Provides a clean interface for answer submission and progress visualization. |

### Initial architecture sketch
```mermaid
flowchart LR
  U[Learner Interface] --> API[Backend API]
  API --> SP[Database Stored Procedures]
  SP --> DB[(Relational DB - 10+ Tables)]
