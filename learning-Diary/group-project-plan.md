# Project Data Plan — Group 4

## 1. Problem

We want to predict whether a student’s next quiz attempt will be successful using only their earlier quiz activity. Success means that the next completed quiz attempt has a score of at least 70%.

## 2. Unit of Analysis

One observation represents one upcoming quiz attempt by one student. The target is whether that next attempt is successful.

## 3. Data Sources

- Quiz attempt records / `quiz_attempts.jsonl`
- Question or item-result records
- Quiz start and submission timestamps
- Student and quiz/course identifiers
- Earlier quiz-performance records

## 4. Variables

- student_key, quiz_key, attempt_key: directly stored identifiers
- Previous quiz score: directly stored
- Number of earlier attempts: derived
- Previous item/question results: directly stored
- Time since previous attempt: derived from timestamps
- Earlier average quiz score: derived
- Next-attempt success: derived target variable from the next quiz score

## 5. Relationships

Data will be connected using `student_key`, `quiz_key` and `attempt_key`. One student can have many quiz attempts. One quiz attempt can have many question-result records.

## 6. Data Problems

- Raw quiz logs may contain duplicate records for one logical attempt.
- Scores, submissions or timestamps may be missing.
- Attempt states and timestamps may be inconsistent.
- Features must only use information available before the predicted attempt.
- Repeated attempts by the same student are not independent.
- Student data must remain pseudonymous.

## 7. Data Gap

The data may not show why a student retries a quiz or whether they read feedback before retrying. Previous scores, attempt count and time between attempts can be derived from existing records.

If feedback-view data is not already available, Edge-LMS could record it automatically as an activity event. This could help explain improvement without adding manual work for students or teachers.

## 8. Next Step

Inspect the quiz-attempt and question-result files. Identify the keys, remove duplicate records, order attempts by time and define which attempts are eligible for prediction.