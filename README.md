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
  Major updates get their own PRs, which also automerge once CI passes, so
  a breaking major that fails CI stays open for review on its own.
- Waits 3 days after a release before using it (`minimumReleaseAge`). With
  `internalChecksFilter: strict` no branch is created, and no CI runs, until
  then.
- Rebases Renovate PRs only when they conflict, not every time the base
  branch moves.
- Runs lock file maintenance monthly, also automerged.
- Assigns PRs to @meesvandongen. Automerging PRs stay unassigned unless
  their automerge fails (Renovate's default `assignAutomerge: false`).

Repos can add their own `packageRules` after the `extends`; they are applied
after the preset's rules.
