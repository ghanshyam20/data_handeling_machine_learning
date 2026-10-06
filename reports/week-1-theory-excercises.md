# Understanding Data: Types, Meaning and Valid Operations

## Exercise 1

| Variable | Meaning and type | Useful operations | Can the technical type mislead? |
|---|---|---|---|
| Student number | Identifier for one student | Match records and count students | Yes. Even if it is numbers, it is not for calculating an average. |
| Age | Numerical, discrete | Mean, median, minimum and maximum | Normally no. |
| Study programme | Nominal category | Count programmes or find the most common one | Yes. It could be stored as a number code. |
| Satisfaction | Ordinal rating from 1 to 5 | Compare order, median and distribution | Yes. The gap between ratings may not be equal. |
| Completed courses | Numerical count | Sum, mean and comparison | Normally no. |
| Registration date | Datetime | Sort dates and calculate time differences | Yes. A date can be stored as text. |
| Student feedback | Text | Search words and find common themes | Yes. It is text, not a category. |

## Exercise 2

1. Mean age: meaningful.  
2. Mean student ID: not meaningful because it is only an identifier.  
3. Most common city: meaningful.  
4. Highest satisfaction category: meaningful, but it does not show the typical satisfaction level.  
5. Difference between two timestamps: meaningful because it shows a duration.  
6. `"Helsinki" × 3`: not meaningful as maths.  
7. Ratio between two weights: meaningful because weight has a real zero.  
8. Average postcode: not meaningful because postcodes are codes, not measurements.  

## Exercise 3

The city values are only codes. A result of `2.1` is not an “average city” and has no useful meaning.

## Exercise 4

1. Remove rows with missing study hours. This can give a biased result if one group has more missing values.  
2. Fill missing values with the mean or median. This can hide real differences between students.  
3. Estimate values from similar students. This can be wrong if the reason for missing data is different.  
4. Mark missing values separately. This can be misleading if the value is missing because of a system error.  


# Getting, Storing and Retrieving Data: Files, JSON and Databases

## Exercise 1

1. One table with 100 measurements: CSV, because it is simple table data.  
2. Many application events arriving continuously: JSONL, because one event can be saved on each line.  
3. A customer with many addresses and phone numbers: JSON, because it supports nested information.  
4. Students, courses and enrollments used often: relational database, because it handles relationships and repeated queries well.  
5. A prepared table for Excel: CSV, because spreadsheet programs can open it easily.  

## Exercise 2

1. One row is one student’s score for one quiz.  
2. There are two students: `STU_A` and `STU_B`.  
3. There are three quiz-result records.  
4. `student_key` connects the quiz result to the student table.  

## Exercise 3

Source values are `student_key`, `quiz_score` and `submitted_at`.

Derived values are `average_score`, `days_since_submission` and `number_of_attempts`.

This should be documented so it is clear what came from the source and what was calculated later.

## Exercise 4

The student row is repeated five times, once for every task attempt. This can make counts and averages wrong if the repeated rows are not handled carefully.

## Exercise 5

I would keep the JSONL files as raw data and load the needed data into prepared tables or SQLite. This makes joins and repeated searches easier. I would use student and group keys to connect quiz attempts and task grades.