# Cloth standard library work ledger

`ROADMAP.md` defines the allowed order. The compiler's completed Stage 36
proposal owns the shared prelude contract.

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
