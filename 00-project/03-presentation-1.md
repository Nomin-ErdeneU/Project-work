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


## Problem

- Learners repeat all words equally
- Easy words waste time
- Hard words are forgotten
- The system should choose words based on mistakes

## Target users

- **Learner:** wants a personal practice list
- **Administrator:** manages words, topics, and difficulty

## Planned scope

- Database with 10+ related tables
- Stored procedures choose the next words
- Test data and speed measurements
- Simple web interface
- **Not included:** AI or machine learning, audio, notifications

## Initial user journeys

1. **Practice:** the learner starts a session, the database picks the words
2. **Answer:** the system saves the result and updates the priority
3. **Progress:** the learner sees accuracy over time
4. **Content:** the administrator adds and edits words

## Next steps

- Finalize the table design
- Write the stored procedures
- Generate test data for performance tests
