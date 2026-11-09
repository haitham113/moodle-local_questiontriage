# Teacher guide

Open a quiz, then **Question triage** from its settings/navigation menu (often
under More). The quiz selector lists permitted quizzes; the group selector obeys
current Moodle group membership and access-all-groups capability. The dashboard
is quiz-scoped, not a cross-site question bank report.

Filter by question name, reaction, triage status and activity dates. Sort by
Dislikes, recent activity or question name. Question rows represent actual
question versions used in eligible attempts, including resolved random questions.
Different versions are not merged automatically. Follow a row to inspect it.

Counts distinguish feedback records, eligible attempts and unique students.
Repeated attempts can contribute separate attempt-slot reactions. An updated
reaction replaces its existing vote; it does not add a second active vote.
Filters affect the displayed totals; do not interpret attempt-level counts as
the number of distinct students.

Authorized staff can inspect individual Dislike explanations and student display
names within the permitted scope. Staff with triage capability can choose
**New**, **Under Review**, **Resolved** or **Dismissed**, add an optional private
note (up to 2,000 characters), and save. History records staff actions and time.
Students cannot read these notes. If another teacher saved first, reload and
reconcile the displayed conflict instead of overwriting their work.

Resolved questions remain Resolved after new feedback. **New or updated Dislikes
since resolution** counts currently active Dislikes added or materially changed
since resolution, including explanation edits and Like-to-Dislike switches.
Repeated identical saves do not increase it. Removing feedback or switching to
Like removes it from the count. Listing filters restrict its listing count;
the detail page shows the full permitted scope.

After reviewing renewed feedback, reopen and resolve the case again to establish
a new baseline. Adding a private note alone does not clear the indicator.
An upgrade starts historical feedback at a zero activity baseline, without
reconstructing prior changes. There are no automatic reopenings or notifications.

Use **Open in Moodle question editor** where offered and where your native
question permissions permit it. QuestionTriage itself never edits source
questions, answers, grades or attempts. Changes to quiz group mode do not merge
old cases. Course/quiz restore or duplication does not carry feedback or notes.
