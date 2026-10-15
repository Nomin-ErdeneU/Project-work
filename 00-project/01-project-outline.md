---
name: Nomin-Erdene Ugiidalai
neptun: E8671V
id: 2026-LA-05
github: https://github.com/Nomin-ErdeneU/Project-work
trello: https://trello.com/b/placeholder
---

# Language Learning Assistant with Individual Progress Tracking

This project is a database-centered language learning assistant for English. The system stores vocabulary, users' answers, and practice history. Based on this history, a database-side stored procedure calculates a priority for each word and selects the words the learner should practice next. A simple web interface lets users start a practice session, submit answers, and view their progress.

## Objectives
- **Primary objective:** Deliver a working learning system where the database decides which words to practice next, based on previous results.
- **Target users / stakeholders:** Language learners; administrators who maintain the learning content; the course supervisor.
- **Measurable success criteria:** A user can start a session, submit answers, and see progress. The next session changes based on the previous answers. The system works with tens of thousands of stored answers.
- **Constraints:** Microsoft SQL Server with T-SQL; selection logic only in the database; at least 10 related tables; no credentials in the repository.

## Scope
### In scope
- Relational database for users, words, meanings, topics, difficulty, sessions, exercises, answers, and learning states.
- Stored procedures with at least two selection strategies.
- A simple interface for practice and progress.
- Test data, SQL queries, and performance measurements.

### Out of scope
- Machine learning or AI models.
- Audio or pronunciation exercises.
- Reminders and notifications.
- A complex e-learning platform.
