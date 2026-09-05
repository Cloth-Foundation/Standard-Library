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

Stage 35 is complete, including its coordinated exit audit. Shuttle
automatically supplies the exact distribution paired with the selected
compiler; applications do not declare a `cloth` manifest dependency.

The package is named `cloth` and has no executable target. Its source tree
starts directly with areas such as `src/math/`; repeating `src/cloth/` would
create incorrect `cloth.cloth.*` identities.

See [ROADMAP.md](ROADMAP.md) for the approved order and [TODO.md](TODO.md) for
the current work ledger. The coordinating contract lives in the compiler's
[`stage_35_standard_library_foundation.md`](https://github.com/Cloth-Foundation/cCloth/blob/master/docs/proposals/stage_35_standard_library_foundation.md)
proposal.

## License

Cloth's standard library is licensed under the Apache License 2.0. See
[LICENSE.txt](LICENSE.txt).
