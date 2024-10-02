# Template GitHub Composite Actions

A template for GitHub Template GitHub Composite Actions

[![license][license-img]][license-url]
[![release][release-img]][release-url]

## Instructions

- Add the comment `<!--START_SECTION:activity-->` (entry point) within `README.md`. You can find an example [here][].

- It's the time to create a workflow file.

`.github/workflows/update-readme.yml`

``` yml
name: Update README
on:
  schedule:
    - cron: "*/30 * * * *"
  workflow_dispatch:
jobs:
  build:
    name: Update this repo's README with recent activity
    runs-on: ubuntu-latest
    permissions:
      contents: write

    steps:
      - uses: actions/checkout@v3
      - uses: khulnasoft-lab/activity-readme-action@master
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

The above job runs every half an hour, you can change it as you wish based on the [cron syntax][].

Please note that only those public events that belong to the following list show up:-

- `IssueEvent`
- `ReleaseEvent`
- `IssueCommentEvent`
- `PullRequestEvent`

You can find an example [here][1].

### Override defaults

Use the following `input params` to customize it for your use case:-

| Input Param        | Default Value                                                            | Description                                               |
|--------------------|--------------------------------------------------------------------------|-----------------------------------------------------------|
| `GH_USERNAME`      | Your GitHub username                                                     | Username for which to generate the activity overview      |
| `COMMIT_NAME`      | github-actions\[bot\]                                                    | Name of the committer                                     |
| `COMMIT_EMAIL`     | 41898282+github-actions\[bot\]@users.noreply.github.com                  | Email of the committer                                    |
| `COMMIT_MSG`       | :zap: Update README with the recent activity                             | Commit message used while committing to the repo          |
| `EMPTY_COMMIT_MSG` | :memo: empty commit to keep workflow active after 60 days of no activity | Commit message used when there are no updates             |
| `MAX_LINES`        | 5                                                                        | The maximum number of lines populated in your readme file |
| `TARGET_FILE`      | README.md                                                                | The file to insert recent activity into                   |

``` yml
name: Update README
on:
  schedule:
    - cron: "*/30 * * * *"
  workflow_dispatch:
jobs:
  build:
    name: Update this repo's README with recent activity
    runs-on: ubuntu-latest
    permissions:
      contents: write

    steps:
      - uses: actions/checkout@v3
      - uses: khulnasoft-lab/activity-readme-action@master
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        with:
          COMMIT_MSG: "Specify a custom commit message"
          MAX_LINES: 10
          COMMIT_NAME: GitHub Activity Readme
```

  [here]: https://github.com/khulnasoft-lab/khulnasoft-lab/blob/master/README.md
  [cron syntax]: https://jasonet.co/posts/scheduled-actions/#the-cron-syntax
  [1]: https://github.com/khulnasoft-lab/khulnasoft-lab/blob/master/.github/workflows/update-readme.yml

----
> Author: [KhulnaSoft Ltd](https://www.khulnasoft.com/) &bull;
> Twitter: [@KhulnaSoft](https://twitter.com/khulnasoft)

[license-url]: LICENSE
[license-img]: https://badgen.net/github/license/khulnasoft/action-composite-template

[release-url]: https://github.com/khulnasoft/action-composite-template/releases
[release-img]: https://badgen.net/github/release/khulnasoft/action-composite-template
