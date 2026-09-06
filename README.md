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

The package is currently version `0.2.0`. Its prelude contains the ordinary,
extensible errors `cloth.lang.errors.ArgumentError` and
`cloth.lang.errors.StateError`, each with default and message constructors.
Public types anywhere beneath `src/lang/` are available by short name as a
low-priority compiler fallback. Their short names must be unique across that
tree. Other areas, including `cloth.math`, remain explicit imports.

See [ROADMAP.md](ROADMAP.md) for the approved order and [TODO.md](TODO.md) for
the current work ledger. The completed coordinating contract is the compiler's
[`stage_36_standard_library_prelude.md`](https://github.com/Cloth-Foundation/cCloth/blob/master/docs/proposals/stage_36_standard_library_prelude.md)
proposal; Stage 35's distribution contract remains its prerequisite.

## License

Cloth's standard library is licensed under the Apache License 2.0. See
[LICENSE.txt](LICENSE.txt).
