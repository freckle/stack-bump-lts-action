# Stack Bump LTS Action

Automatically update a Stack-based Haskell project to latest LTS.

## Usage

This action just bumps and commits, so you will need to do something after it
runs. For example, you could use `create-pull-request`:

```yaml
jobs:
  bump:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2

      - id: bump
        uses: freckle/stack-bump-lts-action@main

      - name: Create PR
        if: ${{ steps.bump.outputs.newer-available }}
        uses: peter-evans/create-pull-request@v3
        with:
          branch: gh/bump-lts
          title: Bump Stackage LTS
          body: ${{ steps.bump.outputs.commit-message }}
```

## Options

If you use a path other than `stack.yaml`:

```yaml
- id: bump
  uses: freckle/stack-bump-lts-action@main
  with:
    stack-yaml: stack-default.yaml
```

If your `stack.yml` uses `resolver: ./other-file.yaml`:

```yaml
- id: bump
  uses: freckle/stack-bump-lts-action@main
  with:
    snapshot-yaml: other-file.yaml
```

To operate in a sub-directory:

```yaml
- id: bump
  uses: freckle/stack-bump-lts-action@main
  with:
    working-directory: backend
```

**NOTE**: Path options are relative to this.

## Package Diff

The commit message will link to a diff of packages changes between the
resolvers. For example,

https://www.stackage.org/diff/lts-16.29/lts-17.1

---

[LICENSE](./LICENSE)
