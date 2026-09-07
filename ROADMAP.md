# Cloth standard library roadmap

This roadmap owns implementation order inside the standard-library repository.
The compiler's completed Stage 39 contract owns the cross-repository Unicode
scalar, artifact, runtime, and toolchain behavior. A coordinated checkpoint
closes only after the compiler, Shuttle, and standard-library requirements pass
together.

## Stage discipline

Only work authorized by the active compiler stage enters the standard library.
Public APIs require an approved source contract, tests, documentation, and
explicit implementation authorization. A placeholder directory or proposed API
does not make that API supported.

## Stage 35: Standard library foundation

Status: **complete — coordinated exit audit passed 2026-09-05**

Objective: establish this repository as the deterministic source and
distribution unit for Cloth library code under the reserved `cloth` import
root.

Deliverables:

1. **35.1 — Contract (complete).** Approve ownership, namespace, package
   layout, import, compatibility, distribution, and verification boundaries.
2. **35.2 — Bootstrap (complete).** Normalize the manifest and source root, validate the
   existing `Math` surface with the current language, and produce verified
   interface and object artifacts without an executable target.
3. **35.3 — Toolchain integration (complete).** Participate in Shuttle selection,
   injection, reuse, consumer linking, and documentation without duplicating
   compiler or package-manager policy.
4. **35.4 — Exit audit (complete).** Pass library source, artifact, native, cross-target,
   determinism, consumer, documentation, and repository quality gates.

Stage 35 adds no console input, parsing, formatting, collections, filesystem,
networking, prelude, registry, or package-download API. Those require later
approved stages after this distribution boundary is complete.

## Stage 36: Standard-library prelude

Status: **complete — coordinated 36.4 exit audit passed 2026-09-06**

Objective: establish the `cloth.lang` namespace tree as a focused, recursive
prelude of ordinary public Cloth file types without duplicating compiler-owned
core symbols or turning library source into intrinsics.

Deliverables:

1. **36.1 — Prelude contract (complete).** Approve layout, declaration
   eligibility, lookup, ownership, compatibility, evolution, verification, and
   non-goals.
2. **36.2 — Prelude resolution (complete).** Coordinate compiler lookup and
   artifact tests without adding an unapproved public library declaration.
3. **36.3 — Initial `lang` API slice (complete, amended).** Make all public
   types beneath `src/lang/` recursively eligible with unique short names, add
   `ArgumentError` and `StateError` beneath `src/lang/errors/`, advance the
   package to `0.2.0`, and verify their constructors and extensibility.
4. **36.4 — Exit audit (complete).** Pass bootstrap, consumer, artifact,
   native, cross-target, determinism, documentation, and repository quality
   gates.

Stage 36 is complete. The coordinated audit passes bootstrap, source-free,
native, both-target, determinism, documentation, and repository gates with the
production prelude's two source-defined general errors.

## Stage 38: Portable text input and primitive parsing

Status: **complete — coordinated 38.4 exit audit passed 2026-09-06**

Objective: own the source-defined `cloth.io.Console`, `IoError`, and
`ParseError` APIs while relying on a narrow compiler-paired runtime bridge for
operations that cannot be expressed faithfully in Cloth yet.

Deliverables:

1. **38.1 — Contract (complete).** Approve public identities and signatures,
   line/Unicode and parse semantics, library/compiler/runtime ownership,
   compatibility, verification, and non-goals without changing production
   source.
2. **38.2 — Library and runtime foundation (complete).** Add `src/io/Console.co`,
   `src/lang/errors/IoError.co`, and `src/lang/errors/ParseError.co`; advance
   the package to v0.3.0; compile through the private paired-library bridge;
   and verify complete runtime ABI-6 input/parsing operations.
3. **38.3 — Consumer integration (complete).** Verify all primitive parse targets,
   prelude errors, explicit `Console` imports, whole/source-free artifacts,
   both targets, native and Shuttle execution, exact invalidation, reuse, and
   user/API documentation.
4. **38.4 — Exit audit (complete).** Pass Unicode, grammar, rounding,
   resource, GC, compatibility, determinism, consumer, documentation,
   sanitizer, and repository quality gates.

The coordinated audit closes every approved input/parsing, artifact, consumer,
determinism, sanitizer, documentation, and repository matrix. The bridge is not
public Cloth syntax or arbitrary FFI, and the native runtime does not own the
source-defined error layouts. The package remains v0.3.0.

## Stage 39: Unicode string traversal

Status: **complete — coordinated 39.4 exit audit passed 2026-09-06**

Objective: preserve the exact compiler-paired standard-library distribution as
the compiler widens character constants and adds runtime string traversal,
without inventing a library string wrapper or changing public source APIs.

Deliverables:

1. **39.1 — Contract (complete).** Record library ownership, unchanged public
   source, artifact/runtime transitions, exact pairing, verification, and
   non-goals.
2. **39.2 — Scalar artifact coordination (complete).** Rebuild and verify the
   unchanged v0.3.0 source distribution under artifact format 6 and compiler
   ABI 5.
3. **39.3 — Traversal coordination (complete).** Carry runtime ABI 7 through paired
   artifacts, consumers, both targets, native execution, reuse, and
   invalidation without adding public library declarations.
4. **39.4 — Exit audit (complete).** Pass source, artifact, Unicode, traversal,
   consumer, determinism, documentation, sanitizer, and repository quality
   gates.

Stage 39 carries the unchanged package under artifact/compiler/runtime 6/5/7.
The coordinated 39.4 source, artifact, traversal, consumer, determinism,
sanitizer, and repository matrices pass. The package remains v0.3.0. Stage 39
adds no normal string methods, wrapper type, slicing, collection API, or public
bridge.
