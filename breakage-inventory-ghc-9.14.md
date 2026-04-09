# GHC 9.14 breakage inventory

A catalogue of all the non-trivial fixes (that is, not just bounds
bumps) required to upgrade Haskell code that worked with GHC 9.10 to
GHC 9.14.  The [GHC 9.14 migration
guide](https://gitlab.haskell.org/ghc/ghc/-/wikis/migration/9.14)
contains a list of changes that the GHC team anticipated ahead of time
were capable of causing breakage whereas this breakage inventory is a
report of breakage that actually happened in practice.

## `base`

### Regression in `$`

In corner cases, expressions using `$` which previously type checked
no longer type check.

This issue is fixed in GHC `HEAD` and the fix may be backported to a
GHC 9.14 point release.

#### Examples

[`proarrow`](https://gitlab.haskell.org/ghc/ghc/-/issues/26543)
