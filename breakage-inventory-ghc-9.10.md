# GHC 9.10 breakage inventory

A catalogue of all the non-trivial fixes (that is, not just bounds
bumps) required to upgrade Haskell code that worked with GHC 9.8 to
GHC 9.10.  The [GHC 9.10 migration
guide](https://gitlab.haskell.org/ghc/ghc/-/wikis/migration/9.10)
contains a list of changes that the GHC team anticipated ahead of time
were capable of causing breakage whereas this breakage inventory is a
report of breakage that actually happened in practice.

## `base`

### `foldl'` exported from `Prelude`

`Data.Foldble.foldl'` is now exported from `Prelude`.  This means that
any module that uses its own, or any another module than
`Data.Foldable`'s, `foldl'` unqualified will fail to compile.

#### Examples

[`short-text`](https://github.com/haskell-hvr/text-short/pull/43/files)

#### References

* [CLC migration guide](https://discourse.haskell.org/t/prelude-foldl-migration-guide/6950)

* [Haddock for
  `foldl'`](https://hackage.haskell.org/package/base-4.19.1.0/docs/Data-Foldable.html#v:foldl-39-)
  (for GHC 9.8)
