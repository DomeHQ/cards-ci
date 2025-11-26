# Cards CI workflows

Reusable GitHub workflows for building and releasing webapp cards.  
Cards should reference these workflows via tags so they can pin to a known-good version or track the latest stable release.

## Using the workflow

```yaml
jobs:
  release:
    uses: InTouchSO/cards-ci/.github/workflows/card-release.yml@stable
    with:
      node-version: '20'
    secrets:
      WEBAPP_DEPLOY_TOKEN: ${{ secrets.WEBAPP_DEPLOY_TOKEN }}
```

- Use a concrete tag such as `@v1.2.3` to pin to an exact release.
- Use the movable `@stable` tag to always consume the most recent version.

## Publishing new versions

1. Merge your workflow changes to `release`.
2. Open **Actions → Publish Workflow Version** and run the workflow:
   - `version`: SemVer string (`v1.2.3` or `1.2.3`).
   - `mark-stable`: Set to `true` only if this version should become the new `stable`.
3. The workflow creates (and pushes) the annotated `vX.Y.Z` tag.  
   When `mark-stable` is `true`, it also force-updates the `stable` tag to the same commit.

Consumers can immediately reference the new `vX.Y.Z` tag or opt into the refreshed `stable` tag.
