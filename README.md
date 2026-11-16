# Shared workflows

[`dependency-updates.yml`](.github/workflows/dependency-updates.yml) holds the rules for
merging Dependabot's package updates in every repository that calls it. Change
`MIN_UPDATES` or `MAX_WAIT_DAYS` there and they change everywhere.

| Update | When it is merged |
| --- | --- |
| Security fix | As soon as the repository's checks pass |
| Other updates | Once 3 are waiting, or one has been out 14 days, and the checks pass |

Dependabot looks for updates every two days, from each repository's `.github/dependabot.yml`.
