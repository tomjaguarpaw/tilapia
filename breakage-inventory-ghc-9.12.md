# GHC 9.12 breakage inventory

A catalogue of all the non-trivial fixes (that is, not just bounds
bumps) required to upgrade Haskell code that worked with GHC 9.10 to
GHC 9.12.  The [GHC 9.12 migration
guide](https://gitlab.haskell.org/ghc/ghc/-/wikis/migration/9.12)
contains a list of changes that the GHC team anticipated ahead of time
were capable of causing breakage whereas this breakage inventory is a
report of breakage that actually happened in practice.

## `base`

### `ErrorCallWithLocation` deprecated and field removed

The type `ErrorCall` used to have a constructor
"`ErrorCallWithLocation`".  The constructor has become a pattern
synonym, has been deprecated, and its field containing the error
location now throws an error when accessed.

#### Examples

[`shake`](https://github.com/ndmitchell/shake/actions/runs/12547126432)

#### References

* [`ErrorCall` in `base-4.20`](https://hackage.haskell.org/package/base-4.20.0.1/docs/Control-Exception.html#t:ErrorCall)

* [`ErrorCall` in `base-4.21`](https://hackage.haskell.org/package/base-4.21.0.0/docs/Control-Exception.html#t:ErrorCall)

* [CLC proposal where this change was discussed and approved](https://github.com/haskell/core-libraries-committee/issues/285#issuecomment-2571268376)

## `text`

### `show` exported from `Data.Text`

`show` is now exported from `Data.Text`.  This means that any module
which uses the identifier "`show`", and that imports `Data.Text`
unqualified (and `Prelude` unqualified, which is the default).

#### Examples

[`fsnotify`](https://github.com/haskell-fswatch/hfsnotify/issues/116)

#### References

* [`text` changelog](https://hackage.haskell.org/package/text-2.1.2/changelog)
