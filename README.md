# QuestionTriage — Student Feedback for Moodle Quizzes

This public repository contains documentation and support information only.
Plugin source, tests and downloadable plugin ZIPs are not hosted here. Paid
Marketplace distribution is being prepared; no purchase or approved public
plugin release is available yet.

Student Like/Dislike feedback and private question triage for Moodle quizzes.
Version **0.6.2-manual-alpha**, component `local_questiontriage`, build
`2026110900`. This is an alpha review package, not a Marketplace-approved or
production release. See [compatibility and evidence limits](docs/compatibility.md).

Students can Like or Dislike eligible questions during their own quiz attempt,
add an optional explanation, and update feedback afterwards on one consolidated
page. That page shows only permitted safe prompt text and question numbers.
Restricted or unsupported prompts are omitted; their numbered feedback controls
remain. It never includes answer choices, responses, correct answers or grades.

Authorized teachers investigate version-specific feedback within their quiz and
group scope, record New / Under Review / Resolved / Dismissed status, and keep
private notes and history. Feedback does not edit quiz answers, questions or grades.
There is no Report action, AI service, messaging, notification or built-in checkout.

## Guides

- [Install, upgrade and uninstall](docs/installation.md)
- [Administrator guide](docs/administrator.md)
- [Student guide](docs/student.md)
- [Teacher guide](docs/teacher.md)
- [Privacy, retention and backups](#privacy-and-retention)
- [Compatibility and known limitations](docs/compatibility.md)
- [Changelog](CHANGES.md), [support](SUPPORT.md) and [security reporting](SECURITY.md)
- [License](COPYING.txt) and [third-party notices](THIRD_PARTY_NOTICES.md)

The code is licensed under GNU GPL v3 or later, without warranty. Moodle is a
trademark of its respective owner; QuestionTriage is independently developed by
AxioStack and does not claim Moodle endorsement or certification.

## Feedback after resolution

Resolved questions stay Resolved when students add feedback. Authorized teachers
see **New or updated Dislikes since resolution** in the dashboard and question
details. This counts active attempt-slot Dislikes added or materially edited after
resolution, including explanation changes and switches from Like. Repeated saves
do not increase the count. Switching to Like or removing feedback removes that
reaction from the count. Course, group, version and selected listing filters apply.
Private note edits do not clear the indicator: reopen and resolve the case again
after reviewing the feedback to establish a new baseline. Existing feedback is
the starting baseline on upgrade; previously resolved cases begin tracking new
changes after the feature is installed. There are no automatic reopenings or
notifications. Revision markers follow existing privacy and backup policies.


## Privacy and retention

Reactions contain the student ID, owned attempt/slot, resolved question/version,
Like/Dislike, optional explanation, timestamps and a plugin-only Dislike revision
marker. Private triage history contains
its staff author, status transition, optional note and timestamp. Cases retain
course/quiz/version/group scope, current status, revision, resolution baseline and modification time. The
plugin stores no quiz answers, grades or question text.

The approved retention policy keeps reactions until the user, attempt, quiz or
course is deleted, or Moodle approves a privacy erasure request. Staff history
belongs to its author and quiz: deleting a student's feedback does not erase
staff-authored question investigation. Deleting a staff author erases their
history entries, including notes and actor IDs. Other authors' history and
nonpersonal case state remain. Privacy erasure is an exception to the normal
append-only audit history; it does not reset the current case or revision.
Use notes to discuss the question; avoid including unrelated personal information.
Unstructured text about other people may need the site's privacy officer to
review it, as the plugin has no structured subject links inside free text.

Moodle Privacy API discovers, exports and deletes personal data in the **course
context**. Exports contain only the requesting student's reactions and/or that
staff author's own history; they never export another author's private text or
assessment answers. An approved whole-course deletion erases all plugin cases,
history and reactions for that course. Module/system/user contexts do not expand
that scope. Site administrators should configure Moodle's data registry for
course contexts and process requests through Moodle's privacy tools.

Native user, attempt, quiz and course deletion triggers plugin cleanup after a
successful native transaction. A scheduled task runs every ten minutes (when
cron works), deleting up to 500 orphaned rows per personal table per invocation.
It recovers missed deletion events and removed question/version identities;
backlogs can require multiple runs. Failed cleanup produces a generic diagnostic
without private text. Monitor task failures in Moodle's task logs and run the
cleanup task again after resolving the database problem. Disabling QuestionTriage
does not stop privacy operations or scheduled cleanup and does not erase data.
Renaming a question or creating a new version does not transfer old feedback.

## Backup, restore and duplication

As explicitly approved in ADR 0003, **all QuestionTriage reactions, private cases
and history are intentionally excluded** from Moodle course/quiz backup, restore,
course copy and activity duplication. There are no plugin backup/restore handlers.
A restored/copied quiz starts with no QuestionTriage feedback. Source-site user,
attempt and question IDs are never imported into new plugin records. Backing up
Moodle user/attempt data does not change this exclusion. Original feedback stays
on its original quiz until its retention/deletion rules apply.

This exclusion applies to Moodle course/activity backups. A full-site database
backup or database clone includes the plugin tables. Site operators must secure
and expire such backups separately. Moodle native logstores may retain minimal
QuestionTriage action events (actor/context/time/action, no explanation, note,
reaction value, attempt, slot, question ID or grade). Their export, deletion and
retention are handled by the selected logstore and site policy, separately from
plugin erasure. Do not promise that a plugin erasure request deletes historical
full-site backups or native Moodle logs.

## Install, upgrade and uninstall

Install the `questiontriage` directory in Moodle's `local` directory and run the
normal Moodle administration upgrade. The plugin uses standard XMLDB tables and
versioned migrations; no core patches or external runtime services are required.
The M6 upgrade registers events/tasks and backfills case course IDs from their
existing quizzes; private history for already-deleted quizzes is removed under
the deletion policy. Existing valid feedback and history remain unchanged.
Uninstall through Moodle's plugin administration to remove plugin tables,
configuration, capabilities, external functions and scheduled tasks. Moodle logs
and full-site backups remain subject to the separate site policies above.
