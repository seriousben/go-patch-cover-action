# go-patch-cover-action

This action runs [go-patch-cover](https://github.com/seriousben/go-patch-cover) to display test coverage for code changed within a pull request.

![Comment example](docs/comment-example.png#gh-dark-mode-only)
![Comment example](docs/comment-example-light.png#gh-light-mode-only)

## Permissions

- `pull-requests: write` for writing comments on pull requests.
- `contents: write` for the git-notes prev_coverage_mode to maintain the coverage within git notes.

## Usage

Just add `seriousben/go-patch-cover-action` as a step in your existing workflow.

A workflow might look like this:

```yaml
name: "CI"

on: ["push", "pull_request"]

permissions:
  contents: write
  pull-requests: write

jobs:
  ci:
    name: "Run CI"
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - uses: WillAbides/setup-go-faster@v1.7.0
      with:
        go-version: "*"
    - run: "go test -coverprofile=coverage.out -covermode=count ./..."
    - uses: seriousben/go-patch-cover-action@v1
```

Please see [GitHub's documentation on Actions](https://docs.github.com/en/actions) for extensive
documentation on how to write and tweak workflows.

## Thanks

This project took inspiration from https://github.com/marocchino/sticky-pull-request-comment and from https://github.com/dominikh/staticcheck-action.
