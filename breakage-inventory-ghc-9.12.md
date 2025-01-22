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


## `Cabal`

### `readGenericPackageDescription` in `Distribution.Simple.PackageDescription` had its type changed

from the original
```haskell
readGenericPackageDescription :: Verbosity -> FilePath -> IO GenericPackageDescription 
```
to
```haskell
readGenericPackageDescription :: HasCallStack => Verbosity -> Maybe (SymbolicPath CWD (Dir Pkg)) -> SymbolicPath Pkg File -> IO GenericPackageDescription
```
The new argument allows overriding the CWD and the FilePath Argument was changed to make it explicitly a SymbolicPath.

To achieve old behaviour pass `Nothing` before the `SymbolicPath` and use `makeSymbolicPath` from `Distribution.Utils.Path` 
to convert your `FilePath` into a `SymbolicPath`

#### Examples

[`jailbreak-cabal`](https://github.com/NixOS/jailbreak-cabal/commit/280f530ef45709282290dbe9665da7f5ae49908b)

#### References 

[`Cabal` changelog](https://github.com/haskell/cabal/blob/master/release-notes/Cabal-3.14.1.0.md)
