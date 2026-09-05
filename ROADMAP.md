# Cloth standard library roadmap

This roadmap owns implementation order inside the standard-library repository.
The compiler's Stage 35 contract owns cross-repository namespace, artifact, and
toolchain behavior. A coordinated checkpoint closes only after the compiler,
Shuttle, and standard-library requirements pass together.

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
