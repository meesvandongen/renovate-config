# renovate-config

Shared [Renovate](https://docs.renovatebot.com/) preset for my repositories.

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["github>meesvandongen/renovate-config"]
}
```

What [`default.json`](./default.json) does:

- Runs weekly, on Monday before 6am (Europe/Amsterdam).
- Groups all non-major updates into one PR that automerges once CI passes.
  Major updates get their own PRs and wait for review.
- Waits 3 days after a release before using it (`minimumReleaseAge`). With
  `internalChecksFilter: strict` no branch is created, and no CI runs, until
  then.
- Rebases Renovate PRs only when they conflict, not every time the base
  branch moves.
- Runs lock file maintenance monthly, also automerged.
- Uses semantic commits scoped to the repo name. Updates to runtime
  `dependencies` commit as `fix(<repo>): …`, everything else as
  `chore(<repo>): …`. A grouped PR that contains at least one runtime update
  takes the `fix` type. Release tooling that reads conventional commits
  (Tegami, semantic-release) then ships a patch for runtime updates only. For
  Tegami the scope has to match the package name, so this works when the repo
  is named after its package.
- Assigns PRs to @meesvandongen. Automerging PRs stay unassigned unless
  their automerge fails (Renovate's default `assignAutomerge: false`).

Repos can add their own `packageRules` after the `extends`; they are applied
after the preset's rules.
