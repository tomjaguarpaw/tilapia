# GHC 9.12 breakage inventory

A catalogue of all the non-trivial fixes (that is, not just bounds
bumps) required to upgrade Haskell code that worked with GHC 9.10 to
GHC 9.12.  The [GHC 9.12 migration
guide](https://gitlab.haskell.org/ghc/ghc/-/wikis/migration/9.12)
contains a list of changes that the GHC team anticipated ahead of time
were capable of causing breakage whereas this breakage inventory is a
report of breakage that actually happened in practice.

## `text`

### `show` exported from `Data.Text`

`show` is now exported from `Data.Text`.  This means that any module
which uses the identifier "`show`", and that imports `Data.Text`
unqualified (and `Prelude` unqualified, which is the default).

#### Examples

[`fsnotify`](https://github.com/haskell-fswatch/hfsnotify/issues/116)

#### References

* [`text` changelog](https://hackage.haskell.org/package/text-2.1.2/changelog)
