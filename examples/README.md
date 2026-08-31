# Artificial record examples

Every value here is invented. `SYN001`, `SYN002`, `COURSE-DEMO`, people, text, scores, timestamps, hashes, paths, and assessment content do not come from a real Edge-LMS deployment. The examples illustrate confirmed source shapes; they are not a proposed anonymization method and do not cover every task-specific extension.

| File | Illustrates | Implementation source |
|---|---|---|
| `users.json` | Accounts and ID domains | [registration record](../../../lms_core/api/routes_auth.py#L358) |
| `groups.json` | Group members use `studentID` | [group model](../../../lms_core/groups/models.py#L23) |
| `last_seen-SYN001.json` | Overwriteable activity snapshot | [middleware](../../../lms_core/middleware/last_seen.py#L17) |
| `activity-SYN001.jsonl` | Generic and mixed detailed quiz log rows | [activity logger](../../../lms_core/activity_logging.py#L143), [quiz helper](../../../lms_core/utils.py#L90) |
| `submission-SYN001.txt` | Ordinary text artifact | [task route](../../../lms_core/api/routes_tasks.py#L1879) |
| `pow-SYN001.json` | Learning-diary process evidence | [POW builder](../../../lms_core/pow/service.py#L193) |
| `concept-measure-SYN001.json` | Derived concept measurement | [evaluator](../../../lms_core/concepts/evaluate_concepts.py#L764) |
| `grade-v1-SYN001.json` | Aggregate grade and feedback | [GradeRecord](../../../lms_core/grading/models.py#L55) |
| `grade-v2-SYN001.json` | Attempt-level grade | [V2 schema](../../../lms_core/grading_v2/models.py#L28) |
| `structure-metrics.jsonl` | Deidentified-but-linkable structure log | [writer](../../../lms_core/grading_v2/structure_metrics_log.py#L75) |
| `quiz-session-SYN001.json` | Temporary quiz state | [quiz session](../../../lms_core/quiz_engine/quiz_session.py#L122) |
| `exam-session-SYN002.json` / `exam-results-SYN002.jsonl` | Durable exam state/result | [exam route](../../../lms_core/api/routes_exam.py#L143) |
| `attendance-sessions.json` / `attendance-session-DEMO-W01.json` | Attendance index/detail | [attendance service](../../../lms_core/text_grading/attendance.py#L151) |
| `announcement-SYN001.json` | Student-targeted message state | [announcement service](../../../lms_core/announcements/service.py#L211) |

JSONL files contain one complete JSON object per line. The duplicate-looking quiz rows intentionally show why raw activity-log line count is not attempt count.
