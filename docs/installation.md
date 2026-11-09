# Installation, upgrade and removal

Use this alpha on a staging site with synthetic data. First read
[compatibility.md](compatibility.md). Moodle Quiz (`mod_quiz`) is required;
there is no additional runtime plugin or remote service dependency. The package
includes readable PHP and AMD source plus Moodle-loadable compiled JavaScript.

## Install

1. Back up the site's database, Moodle data directory and code as one recoverable
   set. Course backups intentionally exclude QuestionTriage data.
2. As a site administrator, open **Site administration → Plugins → Install
   plugins** and upload the supplied ZIP. It contains one `questiontriage/` root.
3. Review Moodle's validation results and complete installation at Notifications.
   For manual deployment, extract `questiontriage/` into the installation's
   `local/` plugin directory (under `public/` on a split-webroot installation).
   The resulting path must be `local/questiontriage/version.php`, without an
   extra parent folder. An operator may run the normal Moodle
   `admin/cli/upgrade.php --non-interactive` instead of the web upgrade.
4. Open **Site administration → Plugins → Local plugins → QuestionTriage**.
   Check the enable setting and retention notice. Confirm Moodle cron works.
5. Use a student test account and a teacher test account in a disposable quiz.
   Check saving during an attempt, opening the completed-attempt feedback link,
   and opening Question triage from the quiz navigation. Teacher preview is not
   a student attempt and does not grant feedback ownership.

Keep installed plugin code read-only to web users where deployment permits.
Installation requires no Moodle core/theme patch or application shell access.

## Upgrade

Back up the full site first and test on a staging copy. Replace the plugin code
with the complete new directory, preserving site configuration outside it, then
run Moodle Notifications/the normal upgrade command. Purge Moodle caches if an
old interface remains. Do not change Moodle core or directly edit plugin tables.

This package retains version `2026110900`: a site already on that version needs
no new schema upgrade for these documentation additions. Earlier versions use
the versioned XMLDB migrations. The `2026110900` migration adds default-zero
Dislike activity and resolution baseline fields; existing feedback is the
starting baseline, with no invented historical activity. Valid existing reactions,
notes and assessment records are preserved. A failed upgrade must be investigated
and resumed through Moodle, not bypassed by editing the installed version number.

Downgrading plugin code is unsupported. Restore the coordinated database, code
and data backup to roll back; copying older PHP over a newer schema is unsafe.

## Disable or uninstall

Disabling the feedback service stops normal feedback use and hides its entry
points, while preserving records, privacy operations and orphan cleanup.
To remove the plugin, use **Site administration → Plugins → Plugins overview →
QuestionTriage → Uninstall**, complete Moodle's confirmation, and remove its
code directory if Moodle instructs you to do so. Uninstall erases plugin tables,
settings, capabilities, registered external functions and task registrations.

Full-site backups and Moodle native logstores have separate retention policies;
uninstall cannot erase those copies. Course restore, quiz duplication and course
copy start without feedback, triage cases or notes. See the [privacy policy](../README.md#privacy-and-retention).
