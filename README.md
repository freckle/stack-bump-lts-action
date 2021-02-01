# Stack Bump LTS Action

Update a Stack-based Haskell project to latest LTS and open a Pull Request with
Changelog outlining the difference from current.

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

If you're `stack.yml` uses `resolver: ./other-file.yaml`:

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

NOTE: Path options are relative to this.

---

[LICENSE](./LICENSE)
