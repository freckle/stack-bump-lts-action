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

## Resolver Changelog

The commit message will link to another project of ours, [Resolver
Changelog][rcl]. For example,

[rcl]: https://github.com/freckle/rcl

https://rcl.freckle.com?from=lts-16.29&to-lts-17.1

This service displays the packages added, removed, or changed between the given
two resolvers. And, where possible, the section of each dependency's Changelog
relevant for the update.

---

[LICENSE](./LICENSE)
