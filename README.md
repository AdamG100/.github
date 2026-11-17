# Shared workflows

[`dependency-updates.yml`](.github/workflows/dependency-updates.yml) holds the rules for
Dependabot's pull requests in every repository that calls it. Every open one ends
up merged or closed. Change `MIN_UPDATES`, `MAX_WAIT_DAYS` or `STALE_DAYS` there and
they change everywhere.

| Pull request | What happens |
| --- | --- |
| Security fix | Merged as soon as the repository's checks pass |
| Other updates | Merged once 3 are waiting, or one has been out 14 days, and the checks pass |
| One package that a group also updates | Closed |
| One package whose checks failed twice | Closed; Dependabot offers the next version |
| A group or security fix whose checks failed | Left open for a person |
| No check result, or a conflict, for 3 days | Closed; Dependabot opens a fresh one if needed |

Minor and patch updates come in one group pull request; each major update comes on
its own. Dependabot looks for updates every two days, from each repository's
`.github/dependabot.yml`.

Updates of GitHub Actions change workflow files, which a workflow's own token can't
merge. They are merged when the repository or organization has a
`DEPENDENCY_MERGE_TOKEN` secret: a fine-grained token with read and write access to
contents, pull requests and workflows. Without it, they wait for a person.
