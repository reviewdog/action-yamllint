# GitHub Action: Run yamllint with reviewdog

[![Docker Image CI](https://github.com/reviewdog/action-yamllint/workflows/Docker%20Image%20CI/badge.svg)](https://github.com/reviewdog/action-yamllint/actions)
[![Release](https://img.shields.io/github/release/reviewdog/action-yamllint.svg?maxAge=43200)](https://github.com/reviewdog/action-yamllint/releases)

This action runs [yamllint](https://github.com/adrienverge/yamllint) with
[reviewdog](https://github.com/reviewdog/reviewdog) on pull requests to improve
code review experience.

[![github-pr-check sample](https://user-images.githubusercontent.com/8191198/72208542-0ddba200-34a4-11ea-90ce-c9508942420c.png)](https://github.com/reviewdog/action-yamllint/pull/1)
[![github-pr-review sample](https://user-images.githubusercontent.com/8191198/72208536-087e5780-34a4-11ea-8ac7-bc7161c9cc20.png)](https://github.com/reviewdog/action-yamllint/pull/1)

## Inputs

### `github_token`

Optional. `${{ github.token }}` is used by default.

### `level`

Optional. Report level for reviewdog [info,warning,error].
It's same as `-level` flag of reviewdog.

### `reporter`

Reporter of reviewdog command [github-pr-check,github-check,github-pr-review].
Default is github-pr-check.
It's same as `-reporter` flag of reviewdog.

github-pr-review can use Markdown and add a link to rule page in reviewdog reports.

### `yamllint_flags`

Optional. Flags and args of yamllint command. Default: '.'

## Example usage

You can create [yamllint
config](https://yamllint.readthedocs.io/en/stable/configuration.html)
and this action uses that config too.

### [.github/workflows/reviewdog.yml](.github/workflows/reviewdog.yml)

```yml
name: reviewdog
on: [pull_request]
jobs:
  yamllint:
    name: runner / yamllint
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v1
      - name: yamllint
        uses: reviewdog/action-yamllint@v1
        with:
          github_token: ${{ secrets.github_token }}
          reporter: github-pr-review # Change reporter.
          yamllint_flags: 'src/'
```
