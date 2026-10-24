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

Repos can add their own `packageRules` after the `extends`; they are applied
after the preset's rules.
