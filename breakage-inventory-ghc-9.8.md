# GHC 9.8 breakage inventory

A catalogue of all the non-trivial fixes (that is, not just bounds
bumps) required to upgrade Haskell code that worked with GHC 9.6 to
GHC 9.8.  The [GHC 9.8 migration
guide](https://gitlab.haskell.org/ghc/ghc/-/wikis/migration/9.8)
contains a list of changes that the GHC team anticipated ahead of time
were capable of causing breakage whereas this breakage inventory is a
report of breakage that actually happened in practice.

## `base`

### `head` and `tail` gain a warning

Use of `head` and `tail` now incurs an `x-partial` warning.  If
continuing to use `head` and `tail`, successful compilation with
`-Werror` requires some form of conditional compilation to suppress
the warning.

#### Examples

* [`haskell-hedgehog`](https://github.com/hedgehogqa/haskell-hedgehog/pull/504/files#diff-b8ed06757045fac949c89f2139a862498ad2b6d1f82c61a31e7c91d6cf0eaa70)
  uses `.cabal` file conditional compilation.

#### References

* [CLC migration guide](https://github.com/haskell/core-libraries-committee/blob/main/guides/warning-for-head-and-tail.md#how)

* Haddock for [`head`](https://hackage.haskell.org/package/base-4.19.0.0/docs/Prelude.html#v:head)

* Haddock for [`tail`](https://hackage.haskell.org/package/base-4.19.0.0/docs/Prelude.html#v:tail)

### `Data.Functor.unzip` added

`Data.Functor` now exports a general form of `unzip` which clashes
with `Prelude.unzip` if `Data.Functor` is exported unqualified.

#### Examples

* [`hspec-core`](https://github.com/hspec/hspec/issues/867)

#### References

* Haddock for [`Data.Functor.unzip`](https://hackage.haskell.org/package/base-4.19.0.0/docs/Data-Functor.html#v:unzip)

* Haddock for [`Prelude.unzip`](https://hackage.haskell.org/package/base-4.19.0.0/docs/Prelude.html#v:unzip)

## GHC API (`ghc`)

### `(,)` to `Tuple2`

The internal name of `(,)` was changed to `Tuple2`

#### Examples

* `stan` uses `Tuple2` in
  [`Stan.Pattern.Type`](https://github.com/kowainik/stan/commit/aff7e69d671d22fde0a0236e6bd511804c0605af#diff-4137c7c9af7e0110e8dd00dd181ef3a7a087c5383f9d7b064ff470cf5a7be82d)

* `swagger2` [tests broke](https://github.com/GetShopTV/swagger2/issues/248)

### `GreName` removed

`GreName` was removed in favour of `Name`

#### References

#### Examples

* `stan` no longer uses `GreName` in
  [`Stan.Hie.Debug908`](https://github.com/kowainik/stan/commit/aff7e69d671d22fde0a0236e6bd511804c0605af#diff-662049c88be7c05c4bce952bd8ab029bf513bf1b00aa92822ef968f02ca42a29)

#### References

* Haddock for [`ghc-9.6.3`](https://hackage.haskell.org/package/ghc-9.6.3/candidate/docs/GHC-Types-Avail.html#t:AvailInfo)

* Haddock for [`ghc-9.8.1`](https://hackage.haskell.org/package/ghc-9.8.1/candidate/docs/GHC-Types-Avail.html#t:AvailInfo)

### `formatBulleted` signature changed

`formatBulleted` used to take an `SDocContext` but now it doesn't

#### References

#### Examples

* [`ghc-parser`](https://github.com/IHaskell/IHaskell/blob/902c5609601693b27814e38c9712bce7c27c151c/ghc-parser/generic-src/Language/Haskell/GHC/Parser.hs#L239) and [`ihaskell`](https://github.com/IHaskell/IHaskell/blob/902c5609601693b27814e38c9712bce7c27c151c/src/IHaskell/Eval/Util.hs#L341) use `formatBulleted`

#### References

* Haddock for [`ghc-9.6.3`](https://hackage.haskell.org/package/ghc-9.6.3/docs/GHC-Utils-Error.html#v:formatBulleted)

* Haddock for [`ghc-9.8.1`](https://hackage.haskell.org/package/ghc-9.8.1/docs/GHC-Utils-Error.html#v:formatBulleted)

## `template-haskell`

### `TyVarBndr ()` changed to `TyVarBndr BndrVis` in multiple places

The type `TyVarBndr ()` was changed to `TyVarBndr BndrVis` in
multiple places, including `DataD`, `NewtypeD`, `TypeDataD`,
`TypeSynD` and `ClassD`.

#### Examples

* [`th-extras`](https://github.com/erikd/th-extras/commit/b0f1907d6aa887b77339d85ba8aed25846f7ea13)

* [`template-haskell-optics`](https://github.com/well-typed/optics/pull/499/commits/3ee3632418458cb62831e9b88f0185be9ae76032), note how `DataInstD` is not using `BndrVis`

#### References

* Haddock for
  [`template-haskell-2.20.0.0`](https://hackage.haskell.org/package/template-haskell-2.20.0.0/docs/Language-Haskell-TH-Syntax.html#v:DataD)

* Haddock for
  [`template-haskell-2.21.0.0`](https://hackage.haskell.org/package/template-haskell-2.21.0.0/docs/Language-Haskell-TH-Syntax.html#v:DataD)
