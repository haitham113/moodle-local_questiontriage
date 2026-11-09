# Compatibility and evidence boundaries

This alpha declares minimum Moodle build `2024100700` and Quiz build
`2024100700`. A minimum version check is not proof of support for every newer
release. There is no stable commercial support promise in this review package.

## Executed laboratory combinations

| Moodle source | PHP | Databases | Themes tested in the final Milestone 7 matrix |
|---|---|---|---|
| 5.3+ build 20261021, commit aa930e26fbdd08dd8ba70f53298838a8d306ee57 | 8.3.6 | PostgreSQL 18.6; MySQL 9.7.4 | Boost 2026100500; Boost Union v5.3-r1; Academi v5.3 |
| 4.5.15+ build 20261030, commit c0690bbc765fccacd4956452cbff3f6aacad77c5 | 8.3.6 | PostgreSQL 18.6; MySQL 9.7.4 | Boost 2024100700; Boost Union v4.5-r51; Academi v4.5.1 |

The 2026-11-08 independent matrix ran on plugin build **2026110800**: twelve
theme/database cells, English/Arabic, native quiz flows, keyboard/layout/contrast,
failure isolation and restricted-review checks. These are historical tests of
those exact combinations, not tests of arbitrary versions or themes.

The packaged build **2026110900** subsequently passed four-cell plugin PHPUnit,
Privacy API, fresh unit-schema and native upgrade checks; one Boost/5.3/PostgreSQL
browser workflow; and PostgreSQL/MySQL activity races. The unavailable-message
correction also passed focused browser and four-cell service checks. The owner
reported successful manual testing on 2026-11-09 and explicitly chose to proceed
without repeating the complete earlier matrix. The full theme/RTL/quiz-failure
matrix was not rerun for this build. No fresh automated whole-matrix PASS is claimed.

The source includes a GitHub Actions workflow. Hosted Actions execution and its
MySQL 8.4 combination are not verified by the local results. Other PHP versions,
Moodle 5.0–5.2, MariaDB, arbitrary/future themes, full WCAG certification and
production capacity are not established by these tests. Moove is excluded from
the selected matrix by owner decision after native Arabic overflow was observed.

## Product limits

- During-attempt controls use supported output hooks plus inspected native
  question-container markup. No dedicated per-question insertion API or universal
  theme contract is claimed. Unknown/replaced markup does not get controls.
- JavaScript is required for feedback. Native quiz answering remains Moodle's
  responsibility and does not depend on a successful feedback request.
- Post-submission entry is an explicit link, not automatic redirection.
- Prompt text is allowlisted for exact core multiple-choice, true/false,
  short-answer and essay definitions. Plain text or simple attribute-free
  HTML formatting is flattened safely. Review restrictions still apply.
- Unsupported types/subclasses, rich/media/linked content, filters, formulas,
  malformed or oversized text yield numbered controls without prompt text.
  Cloze, matching, drag-and-drop and calculated types are not prompt-rendering claims.
- Course/activity backup, restore and duplication exclude all plugin feedback,
  cases and history. Full-site backups are different; see the privacy policy.
- English language strings ship with the plugin. Arabic/RTL layout testing does
  not mean an official complete Arabic translation is bundled.

Independent verification of the actual ZIP and Marketplace review are separate
release steps. Neither Marketplace approval nor paid publication readiness is
claimed here.
