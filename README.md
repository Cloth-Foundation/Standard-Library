# Cloth Standard Library

The standard library is a Cloth project. All library source files live under
`cloth/`, with ordinary subfolders for each area of the library.

```text
build.toml
module.toml
cloth/
    Library.co
    collections/
        List.co
        Snapshot.co
```

The public generic [List](cloth/collections/README.md) is implemented in
`cloth/collections/List.co`, with independent value storage and explicit lifetime.
It supports direct foreach through `Snapshot<T>` in `cloth/collections/Snapshot.co`.

The module's source root is the repository root (`StandardLibrary = "."`), so
that file is imported as `using cloth.collections.List : List`.
The module identity is configuration metadata and is not an import prefix.
Ordinary subfolders do not need their own `module.toml` files. Importable
declarations must be `pub`.

## Validate the library sources

With Shuttle on your PATH, run from this repository:

```text
shuttle build --stdlib . --emit object
```

When checked out as the compiler's `Standard-Library/` submodule, run from the
compiler repository root:

```powershell
.\gradlew.bat :Shuttle:run --args="build --project Standard-Library --stdlib Standard-Library --emit object"
```

Shuttle currently requires `project.entryPoint` even for object builds. The
configured `StandardLibrary.cloth.Library.main` selects `cloth/Library.co`;
`--emit object` does not require a `main` declaration. The root imports the public
collections so standalone validation checks their generic declarations. Only
reachable sources are compiled. Consumers import each collection from its own
file under `cloth.collections`.
The output is `build/Cloth-Standard-Library.o`.

## Use library sources

Toolchains that bundle this library make its source root available automatically;
consumers still import each declaration explicitly. Select another checkout with
`--stdlib PATH` on either command. The
[collections guide](cloth/collections/README.md) covers List, Deque, Queue, and
Stack. These sources use user-defined generic classes and structs.

A project that configures this root explicitly can add it to `[modules]`, using
a path relative to its own `build.toml`:

```toml
[modules]
StandardLibrary = "../Standard-Library"
```

Keep the module identity `StandardLibrary` to match this repository's
`module.toml`. Sources then select public declarations through `cloth.*` paths.
Use `--stdlib PATH` for that same checkout so a bundled root is not attached in
conflict with the configured module.
The current toolchain compiles reachable library sources together with the
application; the object build does not provide a separately linked library or
package download support.
