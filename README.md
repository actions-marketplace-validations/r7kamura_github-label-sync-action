# github-label-sync-action

Sync GitHub Labels with labels definition file.

## Usage

### .github/labels.yml

Add `.github/labels.yml` file:

```yaml
# .github/labels.yml
- name: add
  description: Add new features.
  color: "0e8a16"
- name: change
  description: Change existing functionality.
  color: "fbca04"
- name: deprecate
  description: Mark as soon-to-be removed features.
  color: "d93f0b"
- name: remove
  description: Remove features.
  color: "b60205"
- name: fix
  description: Fix bug.
  color: "5319e7"
- name: security
  description: In case of vulnerabilities.
  color: "0052cc"
```

### .github/workflows/github-label-sync.yml

Add workflow file to your repository:

```yaml
# .github/workflows/github-label-sync.yml
name: github-label-sync

on:
  push:
    branches:
      - main
    paths:
      - .github/labels.yml
      - .github/workflows/github-label-sync.yml
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: r7kamura/github-label-sync-action@v0
```

## Inputs

### `allow_added_labels`

By default, this action deletes the labels excluded in your labels definition file.

If you want to keep the existing additional labels, set this to `"true"`.

```yaml
- uses: r7kamura/github-label-sync-action@v0
  with:
    allow_added_labels: "true"
```

### `source_path`

The file path can be changed by `source_path` option.

```yaml
- uses: r7kamura/github-label-sync-action@v0
  with:
    source_path: .github/my-github-labels.yml
```

### `source_repository`

If you want to use labels definition file in another repository, use `source_repository` option.

```yaml
- uses: r7kamura/github-label-sync-action@v0
  with:
    source_repository: r7kamura/github-labels-keepachangelog
```

### `target_repository`

If you want to change labels in another repository, use `target_repository` option.

```yaml
- uses: r7kamura/github-label-sync-action@v0
  with:
    target_repository: foo/bar
```

## Notes

This is a wrapper action for [github-label-sync](https://github.com/Financial-Times/github-label-sync).
