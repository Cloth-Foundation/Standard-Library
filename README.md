# Cloth standard library

This repository owns the source implementation of Cloth's standard library.
It is included in the compiler workspace as the `std` submodule and distributed
as a versioned part of the Cloth toolchain.

Stage 35 established the production package boundary. The public import root is
reserved as `cloth`, with imports such as:

```cloth
import cloth.math::Math;
```

The compiler continues to own primitives, `object`, `Error`,
`DivisionByZero`, memory management, and physical ABI behavior. Reusable APIs
that can be implemented faithfully in Cloth belong here.

## Repository state

Shuttle automatically supplies the exact distribution paired with the selected
compiler; applications do not declare a `cloth` manifest dependency.

The package is named `cloth` and has no executable target. Its source tree
starts directly with areas such as `src/math/`; repeating `src/cloth/` would
create incorrect `cloth.cloth.*` identities.

The package is currently version `0.4.0`. Its prelude contains the ordinary,
extensible errors `cloth.lang.errors.ArgumentError`,
`cloth.lang.errors.StateError`, `cloth.lang.errors.IoError`, and
`cloth.lang.errors.ParseError`, each with default and message constructors.
Public types anywhere beneath `src/lang/` are available by short name as a
low-priority compiler fallback. Their short names must be unique across that
tree. Other areas, including `cloth.math` and `cloth.io`, remain explicit
imports. `cloth.io.Console.ReadLine` is the first portable input API.
`cloth.io.File.ReadBytes` performs bounded, exact binary reads of regular
files.
Strict lowercase primitive meta operations such as `int32::parse(text)` use the
paired source-defined `cloth.lang.errors.ParseError` and require the caller to
cover that typed effect.

See [ROADMAP.md](ROADMAP.md) for the approved order and [TODO.md](TODO.md) for
the current work ledger. The active coordinating contract is the compiler's
[`stage_43_file_bytes_and_source.md`](https://github.com/Cloth-Foundation/cCloth/blob/master/docs/proposals/stage_43_file_bytes_and_source.md)
proposal; the Stage 35 distribution and Stage 36 prelude contracts remain its
prerequisites.

## License

Cloth's standard library is licensed under the Apache License 2.0. See
[LICENSE.txt](LICENSE.txt).
