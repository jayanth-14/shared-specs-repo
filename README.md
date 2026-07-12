# shared-specs-repo

Central store for OpenAPI specs contributed by service repos.

## Layout

```
specs/OpenApi/<source-repo-name>/<source-repo-name>-v<N>.json
```

Each source repo owns its own subfolder, created automatically the first
time it submits a spec. `v<N>` is bumped only when a change is classified
as breaking; non-breaking changes overwrite the current latest version
file in place.

## PR checks

Every PR is validated by `.github/workflows/validate-spec-pr.yml`:

1. **Spectral** lints the changed spec file(s) against `.spectral.yaml`
   (currently an empty placeholder ruleset).
2. **Specmatic** runs `backward-compatibility-check` against the PR's
   base branch.

If both pass, the PR is merged automatically. If either fails, the PR is
blocked.
