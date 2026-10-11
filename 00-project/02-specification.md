---
project_outline: "[[00-project/01-project-outline]]"
---

# Language Learning Assistant with Individual Progress Tracking

## 1. Actors and permissions
| Role | Needs | Responsibility / access |
| --- | --- | --- |
| Learner | Practice vocabulary and check personal progress | Starts practice sessions, answers questions, and views score statistics |
| Administrator | Manage content and monitor data | Adds or updates learning words, categories, and difficulty levels |

## 2. Use cases / user stories
### Run a practice session and record answers
- **Actor:** Learner
- **Precondition:** The learner is logged into the application.
- **Main flow:**
  1. The learner requests a new practice session.
  2. The database runs a stored procedure to pick the next words to practice based on past mistakes and study schedule.
  3. The learner submits an answer.
  4. The system logs the result, updates the learner's status, and adjusts when the word should be reviewed again.
  5. The system shows immediate feedback and loads the next question.
- **Alternative flow:** If no scheduled review words are due, the system provides standard practice items based on past accuracy.

## 3. Functional requirements
| Requirement | Acceptance criteria | Priority |
| --- | --- | --- |
| Database-side word selection | Given a learner's history, the database stored procedure generates a practice sequence based on previous accuracy and timing. | Must |
| Answer history tracking | Given a submitted answer, the database logs correctness, time taken, and timestamp, updating repetition counts. | Must |
| Normalized database structure | The database must use at least 10 normalized tables (3NF) to keep users, items, and attempts organized. | Must |
| Multiple selection strategies | The system must support at least two selection approaches (a rule-based method and a weighted-priority method). | Must |
| Progress reporting | The database must run queries to present historical accuracy and mastery trends to the learner. | Must |

Priority: **Must** = required for the final product; **Should** = important; **Could** = optional if time permits.

## 4. Business rules and constraints
| Rule or constraint | Rationale |
| --- | --- |
| Selection logic runs inside the database | Keeps core business logic centralized in procedural database components (PL/SQL or T-SQL). |
| Adaptive review spacing | Correct answers increase the review interval so well-known words appear less often. |
| Quick re-queue for mistakes | Incorrect answers lower the priority score immediately so weak words are practiced again sooner. |

## 5. Non-functional requirements
| Requirement | How it will be verified |
| --- | --- |
| Stored procedure performance | Execution times will be checked using a test dataset of tens of thousands of practice logs. |
| Query optimization | Performance of at least 5 complex queries will be compared before and after adding indexes using execution plans (`EXPLAIN PLAN` / `Actual Execution Plan`). |

## 6. Initial technical proposal
### Technology direction
| Area | Candidate technology / approach | Reason for consideration |
| --- | --- | --- |
| Database | Oracle Database (PL/SQL) or MS SQL Server (T-SQL) | Provides the required procedural programming tools for database-side logic. |
| User Interface | Simple Web application (C# / Web interface) | Provides a clean interface for taking practice sessions and viewing progress. |

### Initial architecture sketch
```mermaid
flowchart LR
  U[Learner Interface] --> API[Backend API]
  API --> SP[Database Stored Procedures]
  SP --> DB[(Relational DB - 10+ Tables)]
