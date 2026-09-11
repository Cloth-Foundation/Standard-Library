# Cloth standard library roadmap

This roadmap owns implementation order inside the standard-library repository.
The compiler's completed Stage 45.5 contract owns the universal Object boundary
used by subsequent self-hosted compiler work.

## Stage discipline

Only work authorized by the active compiler stage enters the standard library.
Public APIs require an approved source contract, tests, documentation, and
explicit implementation authorization. A placeholder directory or proposed API
does not make that API supported.

## Stage 49.4: Frontend authority audit coordination

Status: **complete — coordinated 2026-09-10**

The complete self-hosted source graph passes x86-64 and wasm32 checking with
the paired `cloth` v0.6.0 distribution under development and Clang ASan/UBSan
bootstrap compilers. The authority transfer changes no standard-library source,
package identity, or compatibility boundary.

## Stage 49.3: Standard-error coordination

Status: **complete — coordinated 2026-09-10**

The self-hosted diagnostic renderer requires a public standard-error boundary
that does not redirect compiler diagnostics through ordinary program output.
`Console.WriteError(string)` and `Console.WriteErrorLine(string)` are backed by
one identity-checked private intrinsic. The paired distribution advances to
`cloth` v0.6.0 and runtime ABI 12; artifact format 8, compiler ABI 7, and schemas
2/1/1/1 remain unchanged. Rich diagnostic presentation is compiler-owned and
does not become a Console policy.

## Stage 45.5: Universal Object coordination

Status: **complete — coordinated 45.5d exit audit passed 2026-09-09**

Objective: make `cloth.lang.Object` and the primitive wrapper hierarchy the
source-owned public face of the compiler/runtime object model without exposing
layout, addresses, collector state, or unverified intrinsic access.

Deliverables:

1. **45.5a — Contract (complete).** Record exact declarations, hierarchy,
   equality, hashing, representation, compiler/runtime ownership, planned
   v0.5.0 selection, compatibility, and non-goals.
2. **45.5b — Root coordination (complete).** Publish the validated `Object`
   declaration only with compiler root binding and complete managed-descriptor
   dispatch.
3. **45.5c — Wrapper coordination (complete).** Publish `Number`, `Integer`,
   `FloatingPoint`, all concrete numeric wrappers, `Boolean`, and `Character`
   only with verified boxing/unboxing and runtime value behavior.
4. **45.5d — Exit audit (complete).** Close exact selection, source-free use, both targets,
   native execution, GC, equality/hash, printing, bootstrap, determinism,
   sanitizer, documentation, and repository gates.

The complete Object and primitive-wrapper surface is now published as the
compiler-paired `cloth` v0.5.0 distribution. Exact declaration validation,
source-free consumers, and both targets use coordinated
artifact/compiler/runtime 8/7/11.

## Stage 44: Self-hosted lexer coordination

Status: **complete — coordinated 44.4 exit audit passed 2026-09-08**

Objective: preserve the exact compiler-paired `cloth` v0.4.0 distribution while
the bootstrap consumes `File.ReadBytes` through its own source and lexer types.

Deliverables:

1. **44.1 — Contract (complete).** Record that tokens, spans, cursor rules,
   lexical diagnostics, and parity tests remain bootstrap-owned and add no
   public standard-library API.
2. **44.2 — Foundation coordination (complete).** Verify the unchanged distribution with
   both-target and native scanner-foundation consumers.
3. **44.3 — Literal coordination (complete).** Verify the unchanged
   distribution with the complete bootstrap lexer and malformed source inputs.
4. **44.4 — Exit audit (complete).** Close exact selection, source-free, deterministic,
   sanitizer, documentation, and repository gates.

Compatibility remains artifact/compiler/runtime 7/6/10, schemas 2/1/1/1, and
`cloth` v0.4.0. Stage 44 adds no byte-to-string conversion, text decoder,
source abstraction, token type, diagnostic type, or lexer helper to `cloth.*`.
The coordinated exit audit passed with the complete bootstrap lexer and exact
standard-library selection.

## Stage 43: Portable file-byte coordination

Status: **complete — coordinated 43.4 exit audit passed 2026-09-08**

Objective: add the bounded `cloth.io::File.ReadBytes(string): byte[] throws
IoError` surface through the existing compiler-paired distribution while
keeping native I/O, bootstrap source meaning, and package coordination in their
own layers.

Deliverables:

1. **43.1 — Contract (complete).** Record the exact public declaration,
   `std/src/io/File.co` ownership, existing `IoError`, private bridge, 64 MiB
   bound, planned version/ABI transition, documentation, and non-goals.
2. **43.2 — File foundation (complete).** Add `File.co`, advance `cloth` to
   v0.4.0 with runtime ABI 10, and verify declarations, effects, private bridge,
   exact package identity, reuse, invalidation, and source-free consumers.
3. **43.3 — Bootstrap coordination (complete).** Verify the unchanged public API
   against the real `F:\Cloth` `SourceFile` consumer without adding a compiler
   concept to the library.
4. **43.4 — Exit audit (complete).** Close source, artifact, native,
   cross-platform, source-free, determinism, failure-preservation, sanitizer,
   documentation, and repository gates.

Checkpoint 43.2 advances the active package to v0.4.0 and runtime ABI 10.
Artifact format 7, compiler ABI 6, and schemas 2/1/1/1 remain unchanged.
The coordinated exit audit passes exact paths, bytes, bounds, typed failures,
resources, GC, malformed state, both targets, native/source-free consumers,
package determinism, the real bootstrap, and all repository gates.

The standard library owns the public `File.ReadBytes` declaration and reuses
`cloth.lang.errors::IoError`. It does not own native handles, runtime status
codes, compiler source locations, text decoding, paths as a data type, streams,
writes, directories, or bootstrap tokenization.

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

## Stage 40: Unicode string slicing

Status: **complete — coordinated 40.4 exit audit passed 2026-09-07**

Objective: preserve the exact compiler-paired standard-library distribution as
the compiler adds intrinsic Unicode-scalar string slicing and runtime ABI 8,
without adding a library string wrapper or public source declaration.

Deliverables:

1. **40.1 — Contract (complete).** Record unchanged public source and package
   version, intrinsic/compiler/runtime ownership, the runtime-ABI-8 transition,
   exact pairing, verification, and non-goals.
2. **40.2 — Compiler coordination (complete).** Retain the unchanged
   distribution while semantic and verified compiler IR work proceeds without
   a public library API or separately releasable partial feature.
3. **40.3 — Runtime/toolchain coordination (complete).** Rebuild and verify
   v0.3.0 under artifact/compiler/runtime 6/5/8 across both targets, native,
   packages, source-free consumers, reuse, and invalidation.
4. **40.4 — Exit audit (complete).** Pass source, artifact, slicing, consumer,
   determinism, documentation, sanitizer, and repository quality gates.

Checkpoint 40.3 advances compatibility to 6/5/8 while the package remains
v0.3.0. The unchanged distribution builds for both targets and is selected
exactly for native and source-free slicing consumers. Stage 40 adds no normal
string method, wrapper, range, view, slicing declaration, or public bridge.

The coordinated 40.4 audit closes source, artifact, both-target, native,
source-free, exact-selection, reuse, invalidation, determinism, sanitizer,
documentation, and repository gates. The unchanged package remains v0.3.0.

## Stage 41: Uniform-nullability coordination

Status: **complete — coordinated 41.4 exit audit passed 2026-09-07**

Objective: preserve the exact compiler-paired standard-library distribution as
the compiler adds tagged nullable values, safe instance calls, and safe meta
queries, without introducing a public wrapper, option type, or library
declaration.

Deliverables:

1. **41.1 — Contract (complete).** Record unchanged public source and package
   version, compiler/runtime ownership, the planned 7/6/9 transition, exact
   pairing, verification, and non-goals.
2. **41.2 — Compiler coordination (complete).** Retain the unchanged distribution while
   frontend and verified compiler IR work proceeds without a public library API
   or separately releasable partial feature.
3. **41.3 — Toolchain coordination (complete).** Rebuild and verify v0.3.0 under
   artifact/compiler/runtime 7/6/9 across both targets, native, packages,
   source-free consumers, reuse, and invalidation.
4. **41.4 — Exit audit (complete).** Pass source, artifact, nullable-value,
   consumer, determinism, documentation, sanitizer, and repository quality
   gates.

Checkpoint 41.3 rebuilds and verifies the unchanged distribution under 7/6/9
for both targets, native and source-free consumers, exact reuse, and affected
invalidation. The package remains v0.3.0. Stage 41 adds no standard-library
source, wrapper, option type, safe-operation declaration, or public bridge.

The coordinated 41.4 audit closes source, artifact, nullable-value, consumer,
both-target, native, source-free, determinism, sanitizer, documentation, and
repository gates. The distribution remains unchanged at v0.3.0.

## Stage 42: Runtime-sized fixed-array coordination

Status: **complete — coordinated 42.4 exit audit passed 2026-09-08**

Objective: preserve the exact compiler-paired standard-library distribution as
the compiler adds `T[:length]` construction and the first bootstrap token-buffer
consumer, without introducing a collection wrapper or public declaration.

Deliverables:

1. **42.1 — Contract (complete).** Record unchanged public source and package
   version, compiler/runtime ownership, planned unchanged 7/6/9 compatibility,
   exact pairing, bootstrap verification, and non-goals.
2. **42.2 — Compiler coordination (complete).** Retain the unchanged
   distribution while frontend and verified compiler IR work proceeds without
   a public library API or separately releasable partial feature.
3. **42.3 — Toolchain and bootstrap coordination (complete).** Verify v0.3.0
   under artifact/compiler/runtime 7/6/9 across both targets, native, packages,
   source-free consumers, reuse, invalidation, and the `F:\Cloth` token-buffer
   smoke path.
4. **42.4 — Exit audit (complete).** Pass source, artifact, runtime-sized array,
   bootstrap, consumer, determinism, documentation, sanitizer, and repository
   quality gates.

Stage 42 adds no standard-library source, collection type, defaulting helper,
runtime bridge, manifest change, or version increase. Checkpoint 42.3 required
no public library boundary.

Checkpoint 42.2 completed on 2026-09-08 without changing the `cloth` v0.3.0
source distribution. Runtime-sized construction and its release gate remain
compiler-owned; no standard-library declaration or wrapper was introduced.

Checkpoint 42.3 verifies the unchanged distribution through both targets,
native and source-free consumers, deterministic Shuttle builds, and the real
bootstrap project. Runtime-sized allocation remains compiler/runtime-owned;
the standard library still adds no declaration, helper, or version change.

The coordinated 42.4 audit passes the unchanged distribution through every
source, artifact, native, source-free, both-target, deterministic-build,
sanitizer, bootstrap, documentation, and repository gate. The package remains
v0.3.0 and adds no array declaration or runtime bridge.

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
