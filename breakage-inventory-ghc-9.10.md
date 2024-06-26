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

### `GHC.Num` is no longer `Safe`

It seems that `GHC.Num` used to be `Safe` [as in Safe
Haskell](https://ghc.gitlab.haskell.org/ghc/doc/users_guide/exts/safe_haskell.html)
but no longer is.  That can cause an error like the following if you
try to use it in modules marked `Safe`

```
src/Protolude/List.hs:23:1: error: [GHC-44360]
    GHC.Num: Can't be safely imported! The module itself isn't safe.
```

#### Examples

[`protolude`](https://github.com/protolude/protolude/issues/149)

#### References

[Safe
Haskell](https://ghc.gitlab.haskell.org/ghc/doc/users_guide/exts/safe_haskell.html)

## GHC

### Linear `do` pattern match

A failing pattern match in linear `do`-notation no longer counts as
"using" the matched value.  For example, this no longer compiles

```.hs
g :: a ⊸ Linear.IO a
g x = Linear.do
  (y, True) <- pure (f x)
  return y
```

#### Examples

[genghin/romes via
Discourse](https://discourse.haskell.org/t/please-contribute-to-the-ghc-9-10-breakage-inventory/9533/7?u=tomjaguarpaw)

### Spurious `-Wincomplete-record-selectors` warning

Sometimes `-Wincomplete-record-selectors` warns unnecessarily.

#### Examples

[`imp`](https://github.com/tfausak/imp/pull/24#issuecomment-2116480980)

## `template-haskell`

See [sand-wich's post on
Discourse](https://discourse.haskell.org/t/please-contribute-to-the-ghc-9-10-breakage-inventory/9533/6?u=tomjaguarpaw)
for more details of breakage in `template-haskell`, and its effects.

### Kind of `Code`

The kind of `Code` was changed from `forall r. (Type -> Type) -> TYPE r
-> Type` to `(Type -> Type) -> forall r. TYPE r -> Type`.

### `InfixD` now stores a `NamespaceSpecifier`
