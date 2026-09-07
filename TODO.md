# Cloth standard library work ledger

`ROADMAP.md` defines the allowed order. The compiler's completed Stage 39 proposal
owns the shared Unicode string-traversal contract.

## Stage 35: Standard library foundation

- [x] Record the `std` repository as the source owner for library code.
- [x] Reserve `cloth` as the public import root while retaining compiler
  ownership of primitives, `Error`, `DivisionByZero`, and physical runtime
  contracts.
- [x] Record `src/math/Math.co` to `cloth.math::Math` as the canonical layout
  mapping for 35.2.
- [x] Change the package manifest from an application scaffold to the official
  executable-free `cloth` library package.
- [x] Move the bootstrap `src/cloth/` contents directly beneath `src/` without
  changing the intended public import spelling.
- [x] Validate and test every current `Math` declaration against the completed
  Stage 34 language and error rules. The 35.1 readiness check found dynamic `%`
  in `Gcd` and dynamic `/` in `Lcm`; resolve their `DivisionByZero` contracts
  deliberately rather than weakening compiler effect analysis.
- [x] Produce and consume interface artifacts on x86-64 and wasm32 and native
  x86-64 object artifacts through compiler-owned package verification.
- [x] Add dedicated consumer fixtures and library repository quality gates.
- [x] Integrate the selected package with Shuttle through compiler-paired
  metadata, implicit direct dependency injection, artifact reuse, and native
  consumer linking.
- [x] Complete the coordinated 35.4 exit audit.

## Stage 36: Standard-library prelude

- [x] Approve `src/lang/` as the canonical namespace tree for public prelude
  types while retaining normal file identity, capitalization, member
  qualification, and package compilation.
- [x] Keep production source unchanged during 36.2 while compiler fixtures
  prove whole-project and artifact-backed prelude resolution.

  Completed with compiler 36.2 on 2026-09-05. Tests use synthetic `lang`
  declarations in temporary inputs; this repository adds no production type or
  version change.
- [x] During 36.3, approve the exact initial API names, add only those
  declarations, select the corresponding package version, and add user and API
  documentation.

  Completed 2026-09-05 and amended 2026-09-06. Public types recursively beneath
  `src/lang/` enter the prelude and must have globally unique short names.
  `lang/errors/ArgumentError.co` and `lang/errors/StateError.co` define public,
  extensible errors with `()` and `(string message)` constructors. The package
  remains `0.2.0`; narrower operation-specific errors remain deferred until
  their owning APIs have typed failure contracts.
- [x] Complete the coordinated 36.4 exit audit.

  Completed 2026-09-06 with both 255-test compiler configurations, source-free
  artifacts, x86-64 native execution, x86-64/wasm32 LLVM verification,
  deterministic package checks, documentation links, and repository gates.

Stage 36 is complete.

## Stage 38: Portable text input and primitive parsing

- [x] Approve `cloth.io.Console`, `IoError`, and `ParseError` identities and
  signatures, line/Unicode and parsing behavior, private bridge ownership,
  runtime/library transitions, verification, and non-goals.

  Completed with compiler 38.1 on 2026-09-06. This checkpoint changes
  documentation only. The package remains v0.2.0 and production source is
  unchanged pending separate 38.2 authorization.
- [x] During 38.2, add `src/io/Console.co` and the two error declarations under
  `src/lang/errors/`, advance the package to v0.3.0, use only the private
  compiler-paired bridge, and verify runtime ABI-6 input/parsing status behavior.

  Completed 2026-09-06. The package declarations compile for both targets,
  preserve recursive prelude lookup for both new errors, and produce reusable
  whole and source-free artifacts. Native `Console.ReadLine` success and
  source-defined `IoError` propagation pass through the paired private bridge.
- [x] During 38.3, verify explicit Console imports, recursive-prelude errors,
  every primitive parse target and alias, whole/separate/source-free consumers,
  both targets, native/Shuttle execution, exact reuse and invalidation, and
  user/API documentation.

  Completed 2026-09-06. The paired source-defined `ParseError` backs every
  approved primitive and alias parse operation across whole and source-free
  consumers, both targets, native and Shuttle execution, editor support, and
  user documentation without changing package v0.3.0.
- [x] Complete the coordinated 38.4 exit audit across standard-library source,
  artifacts, Unicode, parsing, native/cross-target, determinism, consumer,
  sanitizer, documentation, and repository quality gates.

  Completed 2026-09-06. The paired v0.3.0 library passes exact invalidation,
  reuse, whole/source-free, both-target, native, Unicode, parsing, GC,
  determinism, consumer, documentation, sanitizer, and repository gates without
  a package-version change.

## Stage 39: Unicode string traversal

- [x] Record that Stage 39 changes no public standard-library declaration,
  retains `cloth` v0.3.0, rebuilds paired artifacts under format 6/runtime ABI
  7, and preserves exact compiler/library selection.

  Completed with compiler 39.1 on 2026-09-06. This checkpoint changes
  documentation only; active compatibility remains 5/5/6 and the production
  distribution is unchanged.
- [x] During 39.2, rebuild and verify the unchanged source distribution under
  artifact format 6/compiler ABI 5 across both targets, whole and source-free
  consumers, exact reuse, and invalidation.

  Completed 2026-09-06. The unchanged v0.3.0 source distribution rebuilds as
  format-6/compiler-ABI-5/runtime-ABI-6 artifacts on both targets and passes
  whole/source-free consumption, exact pairing, reuse, and invalidation.
- [x] During 39.3, carry runtime ABI 7 through paired artifacts, native
  consumers, Unicode indexing/iteration, GC, both targets, and Shuttle without
  adding library source or changing v0.3.0.

  Completed 2026-09-06. The unchanged v0.3.0 distribution rebuilds and pairs
  under 6/5/7 for whole, separate, source-free, native, and both-target
  consumers. Traversal remains compiler/runtime-owned; no library declaration
  or version changed.
- [x] Complete the coordinated 39.4 source, artifact, Unicode, traversal,
  consumer, determinism, sanitizer, documentation, and repository quality
  gates.

  Completed 2026-09-06. Both compiler targets, native and source-free
  consumers, exact package pairing, reuse, invalidation, determinism,
  sanitizers, documentation, and repository gates pass with the unchanged
  `cloth` v0.3.0 distribution under compatibility 6/5/7.
