# Administrator guide

The only editable site setting is **Enable feedback service**, under Local
plugins → QuestionTriage. Both during-attempt and post-submission feedback are
provided when enabled; there is no timing selector, paid key or remote account.
The retention policy is a notice, not a configurable expiry period or policy text.

## Permissions

| Capability | Context | Default archetypes |
|---|---|---|
| `local/questiontriage:submit` | Quiz module | Student |
| `local/questiontriage:view` | Quiz module | Teacher, editing teacher |
| `local/questiontriage:triage` | Quiz module | Editing teacher |
| `local/questiontriage:manage` | System | Manager |

Site administrators retain Moodle's native administrative access. These
capabilities do not bypass native enrolment, quiz access, attempt ownership,
group restrictions or question-editing capabilities. The manage capability does
not authorize a user to edit another student's feedback or substitute for the
view/triage checks. Review custom roles at the relevant context.

## Privacy and operation

Configure Moodle's data registry for course contexts. Process access/export and
erasure requests using Moodle's Privacy API tools. Staff can see student display
names beside permitted individual Dislike explanations; aggregates do not list
student identities. Explain this in the site's own privacy notice.

Ensure cron runs regularly. QuestionTriage's cleanup task is scheduled every ten
minutes and removes up to 500 orphaned rows per personal table per invocation.
Deletion events normally clean data after successful native deletion transactions;
the task recovers missed events and removed question identities. Monitor task logs
and retry failures after fixing their cause. Large backlogs take multiple runs.

Run the plugin's staging checks after Moodle or theme upgrades. During-attempt
placement depends on inspected native question containers; changed markup fails
closed and may leave feedback unavailable. Preserve native quiz operation and
report compatibility issues rather than patching core/theme files.

For missing controls, check enablement, JavaScript loading, student role and quiz
access, active non-preview attempt ownership and the tested theme combination.
For empty post-submission prompt text, first check review settings and the safe
prompt limits; missing text can be intentional. For a denied teacher page, check
view capability, visible quiz/course and current activity group membership.

See [privacy and backup details](../README.md#privacy-and-retention) and
[support reporting](../SUPPORT.md). Never include live feedback, private notes,
credentials or full database dumps in a public bug report.
