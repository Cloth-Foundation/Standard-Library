# Cloth standard library work ledger

`ROADMAP.md` defines the allowed order. The compiler's Stage 35 proposal owns
the shared contract.

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

New library APIs remain unscheduled until their own contract is approved.
