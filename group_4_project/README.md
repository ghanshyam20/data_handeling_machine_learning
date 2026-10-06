# Group 4 Project – Success on the Next Quiz Attempt

## Project goal

The goal of this project is to predict whether a student's second quiz attempt will improve compared with their first attempt.

For this analysis, success was defined as:

- `1` = second attempt score is higher than the first attempt score
- `0` = second attempt score is equal to or lower than the first attempt score

## Data

The project uses the synthetic Edge-LMS dataset provided for the course. The data are fully artificial and do not contain real student information.

The main files used were:

- `quiz_attempts.jsonl`
- `quiz_item_responses.jsonl`
- `tasks.jsonl`

`quiz_items.jsonl` was also inspected during the initial data exploration.

The original quiz attempt data contained 551 attempts. After filtering eligible records and matching first and second attempts for the same student and quiz, the final analytical dataset contained 42 cases from 27 students.

## Data preparation

The analysis included:

- filtering records using `analysis_eligible`
- separating first and second quiz attempts
- matching attempts using `student_key` and `task_key`
- creating the target variable `success`
- calculating first-attempt item-level information
- adding quiz week and task information
- checking missing values and class distribution

The final target contained:

- 32 improved attempts
- 10 non-improved attempts

## Features

The final model used three features that were available before the second attempt:

- `score_percent_first`
- `duration_seconds_first`
- `week`

Second-attempt information was not used as a predictor because it would cause data leakage.

Some explored variables were not included in the final model. `avg_item_score` was effectively the same information as the first-attempt score, and `items_answered` was constant in the analytical data.

## Models

Three approaches were compared:

| Model | Accuracy |
|---|---:|
| Dummy baseline | 73% |
| Logistic Regression | 82% |
| Decision Tree | 73% |

Logistic Regression performed best in the initial train/test split.

Because the same student could have multiple observations, student-grouped validation was also used. This kept students in the test set completely separate from students used for training.

With the student-grouped split:

- Baseline accuracy: 44%
- Logistic Regression accuracy: 89%
- Logistic Regression correctly predicted 8 of 9 test cases
- Student overlap between training and test sets: 0

## Model interpretation

The Logistic Regression coefficients showed that the first-attempt score had the strongest relationship with the prediction.

The coefficients were approximately:

- first-attempt score: `-1.29`
- week: `-0.38`
- first-attempt duration: `-0.06`

A higher first-attempt score was associated with a lower probability of improvement.

This should be interpreted carefully because success was defined as improvement. Students who already had high first-attempt scores had less room to improve.

## Misclassified case

The grouped Logistic Regression made one incorrect prediction.

The student scored 32% on the first attempt and 20% on the second attempt. The model predicted improvement, but the actual score decreased.

This shows that the first-attempt score cannot explain every student's next attempt.

## Limitations

The analytical dataset is small, with only 42 second-attempt cases. The grouped test set contained only 9 cases, so a single prediction can change the accuracy considerably.

The success definition also creates a ceiling effect. For example, a student scoring 100% on both attempts is classified as no improvement even though the performance is high.

The dataset is fully artificial. The provided documentation does not give a completed reference analysis for this prediction task, so the relationships found in this project should not be assumed to be intentional causal relationships in the data-generation process.

The results describe patterns in this dataset and should not be interpreted as causal conclusions about student performance.

## Project structure

```text
group_4_project/
│
├── data/
│   ├── quiz_attempts.jsonl
│   ├── quiz_item_responses.jsonl
│   ├── quiz_items.jsonl
│   ├── tasks.jsonl
│   └── analytical_dataset.csv
│
├── group_4_project.ipynb
└── README.md
```

## Tools

The analysis was completed in Python using Jupyter Notebook.

Main libraries:

- pandas
- matplotlib
- scikit-learn
s
## Summary

The project showed that Logistic Regression could predict improvement better than the baseline in the tested data. The first-attempt score was the strongest predictor.

Student-grouped validation was used to reduce the risk of evaluating the model on students it had already seen. The final grouped result was 89% accuracy, but this result should be treated carefully because of the small dataset and the definition of success.