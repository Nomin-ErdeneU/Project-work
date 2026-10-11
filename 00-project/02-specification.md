---
project_outline: "[[00-project/01-project-outline]]"
---

# Language Learning Assistant Specification

## 1. Actors and permissions
| Role | Needs | Responsibility / access |
| --- | --- | --- |
| Learner | Practice vocabulary/grammar and view personal progress | Starts practice sessions, submits answers, and views progress statistics |
| Administrator | Manage content and monitor system performance | Adds or updates vocabulary words, meanings, topics, and difficulty levels |

## 2. Use cases / user stories
### Practice session and answer processing
- **Actor:** Learner
- **Precondition:** The learner is logged into the application.
- **Main flow:**
  1. The learner starts a new practice session.
  2. The database computes priority scores based on past attempts and retrieves the next set of words.
  3. The learner submits an answer to a question.
  4. The system records the response, updates the learner's progress state, and adjusts the item's review priority.
  5. The system displays immediate feedback and moves to the next question.
- **Alternative flow:** If no urgent review items are pending, the system provides general practice items based on past accuracy.

## 3. Functional requirements
| Requirement | Acceptance criteria | Priority |
| --- | --- | --- |
| Smart item selection in the database | Given a learner's history, the database stored procedure picks the next words to practice based on past mistakes and study timing. | Must |
| Answer history logging | Given a submitted answer, the database logs accuracy, time taken, and timestamp, updating repetition counters. | Must |
| Well-organized database structure | The database must use at least 10 related tables to store users, words, attempts, and progress records cleanly. | Must |
| Multiple selection strategies | The system must include at least two selection approaches (a simple rule-based approach and a weighted-priority approach). | Must |
| Progress reporting | The database executes aggregation queries to show accuracy and mastery trends over time. | Must |

Priority: **Must** = required for the final product; **Should** = important; **Could** = optional if time permits.

## 4. Business rules and constraints
| Rule or constraint | Rationale |
| --- | --- |
| Selection logic executes inside the database | Keeps the core practice logic centralized in stored procedures (PL/SQL or T-SQL). |
| Correct answers lower practice frequency | Mastered words appear less often so the learner can focus on weaker items. |
| Incorrect answers increase practice frequency | Words answered incorrectly are re-queued quickly for review. |

## 5. Non-functional requirements
| Requirement | How it will be verified |
| --- | --- |
| Database performance | Stored procedures are tested against a generated dataset of tens of thousands of practice logs to ensure fast execution. |
| Query optimization | Performance of at least 5 complex queries is compared before and after adding indexes using execution plans (`EXPLAIN PLAN` / `Actual Execution Plan`). |

## 6. Initial technical proposal
### Technology direction
| Area | Candidate technology / approach | Reason for consideration |
| --- | --- | --- |
| Database | Oracle Database (PL/SQL) or MS SQL Server (T-SQL) | Provides the required procedural features for database-side logic. |
| User Interface | Simple Web application (C# / Web interface) | Provides a clear screen for taking practice sessions and viewing progress. |

### Initial architecture sketch
```mermaid
flowchart LR
  U[Learner Interface] --> API[Backend API]
  API --> SP[Database Stored Procedures]
  SP --> DB[(Relational DB - 10+ Tables)]
