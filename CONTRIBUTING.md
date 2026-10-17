# Contributing to a grim unit

Every repository in this organisation named `grim-<module>`, `grim-theme-<name>` or `grim-core` is a
**unit**: a module, a theme or the core of grim, released on its own and installed into projects
with [grim](https://grim.grimoiry.com).

These repositories are private. Access is by invitation, and no licence is granted beyond that.

## Do not open a pull request here

A unit repository is written by the release pipeline alone. The source of every unit is the
monorepo, and each release copies the unit from there, so a pull request opened here would be
overwritten by the next release and is never merged.

Change the unit from a grim project instead, and let grim send the change to the right place:

```
grim push Cart --dry-run
grim push Cart -m "fix(cart): keep the coupon after login"
```

`grim push` opens the pull request against the monorepo with exactly your change in it. A core
module (for example Users or Admin) travels with core as one change:

```
grim push --core -m "fix(users): redirect to the page that asked for login"
```

The whole path, from the edit to the release, is the recipe
[Change a module and send it back](https://grim.grimoiry.com/recipes/change-module).

## What the pull request has to pass

- **Title = conventional commit**: `type(scope): subject`, at most 100 characters, the scope is
  usually the unit in lower case. The title becomes the squashed commit.
- **Style and lint**: Pint for PHP, ESLint for JavaScript and Vue.
- **Coupling**: a unit may not start depending on a unit it did not depend on before.
- **Unit check**: the unit's own tests in a throwaway project, see
  [Unit check](https://grim.grimoiry.com/recipes/unit-check).

## After the merge

The release pipeline tags the units you touched with a new patch version. Bring it into your
project with `grim update`. A change to core moves the train, which is announced.
