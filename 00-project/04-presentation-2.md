---
project_outline: "[[00-project/01-project-outline]]"
---

<!-- 5xl -->
# Language Learning Assistant with Individual Progress Tracking

Author: Nomin-Erdene Ugiidalai  
Neptun: E8671V  
Supervisor: Anett LENART  
Project ID: 2026-LA-05  

---

## Specification summary

- **Users:** learner (main), administrator (secondary)
- **Idea:** the database remembers answers and decides the next words
- **Rule:** wrong answer raises priority, correct answer lowers it
- **Requirements:** 8 Must, 1 Should, 1 Could
- **Not included:** AI or machine learning, audio, notifications

---

## Main user journeys and requirements

1. **Practice:** the database picks the words
2. **Answer:** the result is saved, the priority is updated
3. **Progress:** accuracy over time and hardest words
4. **Content:** the administrator adds and edits words


**Key requirements:** two selection strategies, 10+ tables in 3NF, every answer recorded, sequence in under 1 second with 50,000+ answers

---

## Initial technical proposal

```text
Learner → C# web interface → stored procedures → SQL Server tables
```

- **Interface:** shows questions, sends answers, never chooses words
- **Database (T-SQL):** priority, selection, validation
- Invalid or empty input is rejected, learning state unchanged
- **Tools:** execution plans, `SET STATISTICS IO/TIME`, Git

---

### Data model: 13 related tables

- **Content:** Topics, DifficultyLevels, ItemTypes, LearningItems, Meanings, ExampleSentences
- **Practice:** Users, SelectionStrategies, PracticeSessions, ExerciseTypes, Exercises, UserAnswers
- **LearningStates:** per learner and word: attempts, wrong answers, last practice, interval, priority
- 3NF, keys, unique and check constraints in the database

---

### Priority calculation

`priority = 0.4·errors + 0.3·overdue + 0.2·difficulty + 0.1·newness`

- Wrong answer: errors rise, interval resets to 1 day
- Correct answer: interval doubles, the word waits longer
- Long break: overdue grows, priority grows

| Word | Errors | Overdue | Difficulty | Newness | Priority |
| --- | --- | --- | --- | --- | --- |
| although | 0.75 | 1.00 | 0.80 | 0.20 | **0.78** |
| borrow | 0.50 | 0.50 | 0.60 | 0.33 | **0.50** |
| apple | 0.00 | 0.19 | 0.20 | 0.17 | **0.11** |

- Wrong: interval resets to 1 day. Correct: interval doubles.
- Example weights, to be tuned on test data

---

### Two selection strategies

| | Rule-based | Weighted priority |
| --- | --- | --- |
| Idea | recent mistakes first, then longest unpracticed | highest score first |
| Strength | simple, fast, easy to explain | balances errors, time, difficulty, repetitions |
| Risk | ignores difficulty and intervals | weights need tuning |

- **Compare:** selected words, handling of errors, repetition, query speed, large data
- Then choose one and justify it

---

### Testing and performance

- **Test data:** one script, fixed seed, 50,000+ answers, strong and weak learners
- **10 SQL queries:** progress, problem words, by topic, over time, repetition, multi-table totals
- **5 queries optimized:** indexes, results before and after, execution plans
- **Target:** practice sequence in under 1 second

---

## Semester-2 implementation plan

1. Table design and database
2. Stored procedures: priority, two strategies, save answer
3. Reproducible test data
4. SQL queries, indexes, measurements
5. Simple web interface
6. Documentation and final testing

---

## Open risks and next steps

- **Risk:** priority formula picks poor words → compare strategies, adjust weights
- **Risk:** slow with large data → measure, add indexes, simplify
- **Risk:** learner identification without login → simple user selection
- **Risk:** growing scope → fixed out-of-scope list
  
**Next:** finalize the tables, write the first procedures
