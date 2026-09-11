# Cloth standard library work ledger

`ROADMAP.md` defines the allowed order. The compiler's Stage 45.5 universal
Object and value-wrapper boundary is complete.

## Stage 49.4: Frontend authority audit coordination

- [x] Verify the complete self-hosted compiler source graph against the exact
  `cloth` v0.6.0 distribution on x86-64 and wasm32 with development and Clang
  ASan/UBSan bootstrap compilers.

  Completed 2026-09-10 without a standard-library source or compatibility
  change.

## Stage 49.3: Standard-error coordination

- [x] Publish `Console.WriteError(string)` and
  `Console.WriteErrorLine(string)` through an identity-checked private bridge;
  verify public declarations, native lowering, bridge isolation, runtime
  failure handling, paired selection, and source-free consumption.

  Completed 2026-09-10 as `cloth` v0.6.0 with runtime ABI 12. Artifact format
  8, compiler ABI 7, and schemas 2/1/1/1 remain unchanged.

## Stage 45.5: Universal Object coordination

- [x] Approve the exact `Object` surface, lowercase alias relationship,
  wrapper hierarchy, equality/hash/string contracts, ownership split, planned
  v0.5.0 release, compatibility transition, and non-goals.

  Completed with compiler 45.5a on 2026-09-09. The pre-existing untracked
  `Object`, `Number`, and `Byte` drafts are intentionally not published: they
  fail the v0.4.0 package check and their placeholder hash/string/conversion
  behavior violates the approved contract.
- [x] During 45.5b, replace the Object draft with the exact compiler-paired
  declaration and verify root dispatch for classes, errors, strings, arrays,
  interfaces, direct builds, and source-free consumers.

  Completed with compiler 45.5b on 2026-09-09. `Object.co` now owns the exact
  `Equals(Object?)`, `HashCode(): uint64`, and `ToString(): string` surface and
  reaches only identity-checked private bridges. The compiler and runtime bind
  that surface to implicit ancestry and uniform managed virtual slots. Focused
  whole-project and source-free consumers pass on x86-64 and wasm32; numeric
  draft failures remain isolated to 45.5c.
- [x] During 45.5c, replace the numeric drafts with `Number`, `Integer`,
  `FloatingPoint`, `Byte`, `Int8` through `Int64`, `UInt8` through `UInt64`,
  `Float32`, `Float64`, `Boolean`, and `Character`; publish only with complete
  boxing/unboxing, payload behavior, tests, and the v0.5.0 transition.

  Completed with compiler 45.5c on 2026-09-09. The exact sealed wrapper
  hierarchy, payload fields, constructors, constants, and Object overrides are
  published as `cloth` v0.5.0 and validated from source and format-8 artifacts
  on x86-64 and wasm32.
- [x] Complete the coordinated 45.5d source, hash/equality, representation,
  GC, artifact, native, cross-target, source-free, Shuttle, bootstrap,
  determinism, sanitizer, documentation, and repository gates.

  Completed with compiler 45.5d on 2026-09-09. Exact source and format-8
  consumers, x86-64 and wasm32 checks, native value behavior, compiler-backed
  Shuttle runs, sanitized compilation, documentation, and repository quality
  gates pass for the complete `cloth` v0.5.0 distribution.

## Stage 44: Self-hosted lexer coordination

- [x] Record that source spans, cursor rules, tokens, lexical diagnostics, and
  parity records remain bootstrap-owned; retain `File.ReadBytes`, `cloth`
  v0.4.0, compatibility 7/6/10, and schemas 2/1/1/1 without adding a public
  source or text-decoding API.

  Completed with compiler 44.1 on 2026-09-08. Production library source and
  metadata are unchanged. Later lexer checkpoints remain separately
  authorized.
- [x] During 44.2, verify the unchanged library with both-target, native,
  source-free, exact-reuse, invalidation, and scanner-foundation consumers.

  Completed with compiler 44.2 on 2026-09-08. The unchanged v0.4.0 library
  supplies exact file bytes to both-target and development/sanitizer native
  lexer consumers without adding a source, token, or text-decoding API.
- [x] During 44.3, verify the unchanged library with complete lexer and
  malformed-input consumers without interpreting source bytes.

  Completed with compiler 44.3 on 2026-09-08. The unchanged v0.4.0 library
  supplies exact file bytes to complete both-target and development/sanitizer
  native lexer consumers. Malformed in-memory bytes remain bootstrap-owned; no
  source, token, decoder, diagnostic, or lexer API was added to `cloth.*`.
- [x] Complete the coordinated 44.4 source, artifact, bootstrap, determinism,
  sanitizer, documentation, and repository gates.

  Completed with compiler 44.4 on 2026-09-08. Exact v0.4.0 selection,
  source-free use, deterministic lexer parity, sanitizer, documentation, and
  repository gates passed without a standard-library API change.

## Stage 43: Portable file-byte coordination

- [x] Record `std/src/io/File.co` as owner of
  `File.ReadBytes(string): byte[] throws IoError`, including exact bytes, the
  64 MiB limit, private compiler bridge, existing error identity, planned
  runtime ABI 10 and v0.4.0 transition, and non-goals.

  Completed with compiler 43.1 on 2026-09-08. At that checkpoint, production
  source and package metadata remained at v0.3.0 and compatibility 7/6/9,
  2/1/1/1.
- [x] During 43.2, add `src/io/File.co`, advance the package to v0.4.0, and
  verify the public declaration, typed effect, canonical private bridge, exact
  package selection, both targets, native and source-free consumers, reuse,
  invalidation, and failed-output preservation.

  Completed with compiler 43.2 on 2026-09-08. The v0.4.0 distribution and
  runtime ABI 10 pass declaration, effect, bridge-isolation, both-target,
  native, source-free, exact reuse, and failure-preservation coverage.
- [x] During 43.3, verify `File.ReadBytes` with the bootstrap-owned
  `frontend.source::SourceFile` consumer without adding source or lexer policy
  to the standard library.

  Completed with compiler 43.3 on 2026-09-08. The unchanged v0.4.0 API passes
  real bootstrap, direct, both-target, native, sanitizer, source-free, reuse,
  and failure-preservation checks without adding compiler policy to the library.
- [x] Complete the coordinated 43.4 platform, source, artifact, runtime,
  bootstrap, determinism, sanitizer, documentation, and repository gates.

  Completed with compiler 43.4 on 2026-09-08. The unchanged v0.4.0 library
  passes exact path/byte/bound, typed-effect, private-bridge, malformed-state,
  native, both-target, source-free, package-determinism, bootstrap, sanitizer,
  documentation, and repository coverage.

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

## Stage 40: Unicode string slicing

- [x] Record that slicing remains compiler/runtime-owned, adds no public
  standard-library declaration, retains `cloth` v0.3.0, advances only runtime
  ABI 7 to 8 during 40.3, and preserves exact compiler/library selection.

  Completed with compiler 40.1 on 2026-09-06. This checkpoint changes
  documentation only; active compatibility remains 6/5/7 and the production
  distribution is unchanged.
- [x] During 40.2, verify the unchanged distribution while compiler semantic
  and IR work remains internal and no partial library feature is published.

  Completed with compiler 40.2 on 2026-09-06. The v0.3.0 source distribution
  is unchanged, frontend and coordinated suites pass, and native slicing
  remains unavailable until the compiler/runtime transition in 40.3.
- [x] During 40.3, rebuild and verify the unchanged source distribution under
  runtime ABI 8 across both targets, native and source-free consumers, exact
  reuse, and invalidation.

  Completed with compiler 40.3 on 2026-09-07. The unchanged v0.3.0 source
  distribution rebuilds under artifact/compiler/runtime 6/5/8 for x86-64 and
  wasm32. Native, whole, separate, source-free, reuse, invalidation, and exact
  compiler/library-selection coverage passes without adding a library API.
- [x] Complete the coordinated 40.4 source, artifact, slicing, consumer,
  determinism, sanitizer, documentation, and repository quality gates.

  Completed with compiler 40.4 on 2026-09-07. The unchanged v0.3.0 package
  passes source, artifact, both-target, native, source-free, exact-selection,
  reuse, invalidation, determinism, sanitizer, documentation, and repository
  gates without adding a public declaration or changing compatibility.

## Stage 41: Uniform-nullability coordination

- [x] Record that nullable values and safe operations remain
  compiler/runtime-owned, add no public standard-library declaration, retain
  `cloth` v0.3.0, plan the artifact/compiler/runtime 7/6/9 transition, and
  preserve exact compiler/library selection.

  Completed with compiler 41.1 on 2026-09-07. This checkpoint changes
  documentation only; compatibility remains 6/5/8 and the production
  distribution is unchanged.
- [x] During 41.2, verify the unchanged distribution while compiler frontend
  and IR work remains internal and no partial library feature is published.

  Completed with compiler 41.2 on 2026-09-07. Development and sanitizer
  configurations each pass all 312 compiler CTests while the native/artifact
  gate prevents partial publication. Standard-library source, `cloth` v0.3.0,
  and compatibility 6/5/8 remain unchanged.
- [x] During 41.3, rebuild and verify the unchanged source distribution under
  artifact/compiler/runtime 7/6/9 across both targets, native and source-free
  consumers, exact reuse, and invalidation.

  Completed with compiler 41.3 on 2026-09-07. The unchanged v0.3.0 source
  distribution rebuilds under 7/6/9 for x86-64 and wasm32 and passes native,
  package, source-free, exact-reuse, and affected-invalidation coverage. No
  public standard-library declaration was added.
- [x] Complete the coordinated 41.4 source, artifact, nullable-value, consumer,
  determinism, sanitizer, documentation, and repository quality gates.

  Completed with compiler 41.4 on 2026-09-07. Both 335-test compiler
  configurations pass the unchanged v0.3.0 distribution through source,
  format-7 artifacts, exact selection, both targets, native and source-free
  consumers, reuse, invalidation, determinism, sanitizer, documentation, and
  repository gates without adding a public declaration.

## Stage 42: Runtime-sized fixed-array coordination

- [x] Record that runtime-sized fixed-array construction remains
  compiler/runtime-owned, adds no public standard-library declaration, retains
  `cloth` v0.3.0 and compatibility 7/6/9, and preserves exact compiler/library
  selection.

  Completed with compiler 42.1 on 2026-09-07. This documentation-only
  checkpoint leaves production source, package version, artifacts, and runtime
  behavior unchanged.
- [x] During 42.2, verify the unchanged distribution while compiler frontend
  and IR work remains internal and no partial library feature is published.

  Completed with compiler 42.2 on 2026-09-08. The `cloth` v0.3.0 source tree,
  public declarations, and exact compiler pairing remain unchanged; the
  compiler owns both runtime-sized construction and its 42.3 publication gate.
- [x] During 42.3, verify the unchanged source distribution under 7/6/9 across
  both targets, native, packages, source-free consumers, exact reuse,
  invalidation, and the `F:\Cloth` token-buffer smoke path.

  Completed with compiler 42.3 on 2026-09-08. The unchanged v0.3.0 source
  distribution passes both targets, native and source-free consumers,
  deterministic package scheduling, exact reuse, affected invalidation, and
  bootstrap Shuttle integration without adding a public array API.
- [x] Complete the coordinated 42.4 source, artifact, runtime-sized array,
  bootstrap, consumer, determinism, sanitizer, documentation, and repository
  quality gates.

  Completed with compiler 42.4 on 2026-09-08. The unchanged v0.3.0 source
  distribution passes both compiler configurations, both targets, native and
  source-free consumers, distinct-root deterministic builds, exact reuse,
  affected invalidation, bootstrap verification, documentation, and repository
  gates without adding a public declaration or changing compatibility.

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
