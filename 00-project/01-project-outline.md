---
name: Nomin-Erdene Ugiidalai
neptun: E8671V
id: 2026-LA-05
github: https://github.com/Nomin-ErdeneU/Project-work
trello: https://trello.com/b/placeholder
---
# Language Learning Assistant with Individual Progress Tracking

The goal of this project is to design and build a database-centered language learning assistant that tracks individual student progress and dynamically adjusts practice sets based on performance history. Instead of relying on client-side logic, the core selection algorithm, priority scoring, and repetition intervals are calculated directly inside the database using procedural programming (PL/SQL or T-SQL).

## Objectives
- **Primary objective:** Deliver a working, database-centered language learning system with automated priority selection for spaced repetition.
- **Target users / stakeholders:** Language learners, self-directed students, and course administrators.
- **Measurable success criteria:** The system correctly stores practice histories, calculates priority scores via database procedures, and generates custom practice sequences based on past performance.
- **Constraints:** Oracle (SQL & PL/SQL) or MS SQL Server (SQL & T-SQL); database-side selection logic; at least 10 normalized tables; simple web/mobile frontend interface.

## Scope
### In scope
- Relational database schema with 10+ related tables (users, items, sessions, answers, progress states).
- Stored procedures/functions for item selection (at least rule-based and weighted-priority strategies).
- Test data generation (tens of thousands of simulated practice events).
- Performance benchmarking for complex aggregation queries and execution plan optimization.
- A simple frontend interface for users to run practice sessions and view progress dashboards.

### Out of scope
- Artificial intelligence or machine learning models.
- Complex e-learning platforms, video/audio streaming, or live chat features.
- Advanced speech or pronunciation recognition software.

## Notes
The primary focus of this thesis work is on database architecture, procedural SQL logic, and query optimization rather than complex frontend design.
