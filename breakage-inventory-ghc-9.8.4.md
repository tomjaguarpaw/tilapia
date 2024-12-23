# GHC 9.8.4 breakage inventory

A catalogue of all the non-trivial fixes (that is, not just bounds
bumps) required to upgrade Haskell code that worked with an earlier
version of GHC 9.8 to GHC 9.8.4.  I am not aware of any migration
guide for these changes.

## `ghc-lib-parser`

### Type of `getkey`

In `ghc-lib-parser` 9.8.3...., [`getKey :: Unique ->
Int`](https://hackage.haskell.org/package/ghc-lib-parser-9.8.3.20241103/docs/GHC-Types-Unique.html#v:getKey).
In 9.8.4...., [`getKey :: Unique ->
Word64`](https://hackage.haskell.org/package/ghc-lib-parser-9.8.4.20241130/docs/GHC-Types-Unique.html#v:getKey).
This appears to be a PVP violation.  The type of an exported
identifier should not change with a minor version bump.

#### Examples

* [`clash-lib`](https://github.com/clash-lang/clash-compiler/issues/2852)

* [`calligraphy`](https://github.com/jonascarpay/calligraphy/issues/40)

* [`ghc-typelits-presburger`](https://github.com/konn/ghc-typelits-presburger/issues/30)

## `deepseq`

### Added `Control.DeepSeq.Unit`

`deepseq` added `Control.DeepSeq.Unit` which collides with
`GHC.Unit.Types.Unit` when `Control.DeepSeq` is imported unqualified.

#### Examples

* [`ghc`](https://gitlab.haskell.org/ghc/ghc/-/issues/25411)

* [`haskell-language-server`](https://github.com/haskell/haskell-language-server/pull/4459)
